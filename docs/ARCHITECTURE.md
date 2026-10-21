# OpenUPI architecture

**Proposed design. No services or database exist in this repository yet.**

## Service boundaries

| Component | Responsibility |
| --- | --- |
| Merchant storefront | Owns catalogue, trusted order amount and fulfillment |
| Checkout portal | Renders identity, queue, QR, counters and outcomes |
| Payment API | Owns authorization, session state, timing, matching and webhook delivery |
| Identity adapter | Sends WhatsApp OTP and manages customer sessions |
| Observer services | Collect and normalize alert evidence; never decide fulfillment |
| Merchant admin | Controls receiving accounts, devices, till requests, branding and review |
| Payment help | Handles authorized customer support and payment inquiries |
| Control Center | Supervises processes and shows health/logs |
| Demo store | Demonstrates integration without representing a stored-value banking product |

## Data flow

Customer UPI apps transfer funds to the merchant's bank through existing UPI rails. OpenUPI observes alerts; it neither creates settlement nor holds funds in this design.

Checkout asks the API for a session. Authentication precedes queue admission. Observers submit signed evidence to the API, which validates source, timestamps, duplicate status and association with a receiving account. State changes are persisted before UI updates and webhook delivery.

## Payment lifecycle

| State | Meaning | Next handling |
| --- | --- | --- |
| INITIATED | Merchant-created checkout | Request customer authentication |
| AUTH_PENDING | Customer verification pending | Verify or abandon |
| AUTHENTICATED | Customer session established | Allocate or queue |
| QUEUED | Receiving account occupied | Promote atomically when available |
| ACTIVE | Customer may pay | Process, cancel or expire |
| PROCESSING | Verification window open | Record eligible evidence or failed verification |
| SUCCESS | Backend accepted payment evidence | Merchant policy and reconciliation still apply |
| FAILED | Verification deadline passed | Permit support/review; do not assert no debit |
| EXPIRED | Payment window ended | Release slot; retain history for late evidence |
| CANCELLED | Explicit cancellation recorded | Release slot; preserve evidence and history |

SUSPICIOUS is a review outcome/flag, not proof of fraud. COD address states and cashier approval states are separate from UPI evidence states.

## Core rules

1. Store money as integer paise; ₹499.00 is 49,900 paise. Validate range and decimal input at boundaries.
2. Allocate one ACTIVE/PROCESSING slot per VPA using atomic database operations.
3. Persist queue position and deadlines. Browser clocks and localStorage cannot change payment authority.
4. A default ACTIVE deadline is five minutes. PROCESSING has a separate thirty-second deadline.
5. Normalize account, amount, reference, source and timestamps before attribution.
6. Deduplicate observations and fulfillment, including across restarts and repeated webhooks.
7. Late or conflicting evidence must not silently pay a newer order.
8. Identity, admin, observer and merchant credentials have distinct scopes.
9. A committed payment outcome must survive process failure before notifications finish.

## Planned storage

Baseline: embedded SQLite in WAL mode, foreign-key enforcement and transactional writes. Proposed file: data/openupi.sqlite. PostgreSQL/Redis are not baseline requirements and need a separate design and tests before support is claimed.

| Entity | Main data |
| --- | --- |
| merchants | Business identity, public identifier, private credentials and branding |
| receiving_accounts | Merchant scope, VPA, payee, enabled status, limits and slot ownership |
| customers | Minimal identity/profile and review status |
| customer_sessions | Hashed session credentials, expiry and revocation |
| payment_sessions | Order, merchant, account, amount, method, state and deadlines |
| observations | Source, normalized fields, deduplication reference and review state |
| devices | Merchant binding, protected secret material, liveness and revocation |
| webhook_deliveries | Event identity, attempts, status and acknowledgment |
| support_tickets | Late/mismatched payment inquiries and operator resolution |
| audit_logs | Actor, action, entity and time with sensitive values redacted |

Indexes, retention, migrations and signed protocol versioning remain implementation work. Do not copy schemas blindly from the reference.
