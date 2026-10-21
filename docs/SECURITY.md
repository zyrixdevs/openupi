# OpenUPI security and reliability requirements

**Design requirements, not implemented safeguards or a security certification.**

## Trust model

An observer reports a message it saw. A valid device HMAC identifies a holder of a device secret; it does not authenticate the underlying bank event. A signed gateway webhook authenticates a gateway message; it does not establish settlement. Browser callbacks, screenshots, QR rendering and OTP verification also do not prove receipt of funds.

## Required controls

| Area | Requirement |
| --- | --- |
| Order integrity | Merchant backend owns amount, currency and order identity |
| Authentication | Expiring/revocable customer sessions and separate merchant/admin/observer scopes |
| OTP abuse | Attempt limits, expiry, resend throttles, secure randomness and no production OTP exposure |
| Device intake | Merchant binding, signed payload/timestamp, replay checks, revocation and protected keys |
| Payment matching | Account/amount/reference/time validation; quarantine conflicts and late evidence |
| Webhooks | Signed envelope, freshness, stable event identity, idempotency, retries and delivery audit |
| Browser integration | Origin validation, secure iframe messaging, framing policy and sanitized redirects |
| Outbound requests | SSRF controls on webhooks, OAuth/configured URLs and user-supplied assets |
| Admin operations | Authorization on every action, audit trails and stronger authentication before release |
| Secrets | Independent keys, encryption where appropriate, rotation and log redaction |
| Data | Tenant isolation, minimum collection, controlled retention and deletion procedures |
| Storage | Transactions, validated migrations, backups and restore drills |

## Reliability boundaries

Exact amounts and single-slot queues reduce one type of collision, but cannot eliminate delayed or mistaken attribution. OTP proves access to a delivery channel, not legal identity or payer ownership. Device/browser fingerprints are fallible review signals, not grounds for irreversible automated fraud decisions.

A failed or expired checkout is not evidence of no debit. Keep a help path, reconcile the receiving bank and review late observations. Multiple alerts can reflect one shared or compromised source.

## Evaluation and deployment

Use synthetic bank alerts and test accounts first. Before customer use, validate failure paths, independent bank reconciliation, refund/support procedures, privacy handling and the receiving bank's applicable terms and requirements.

The reference suggests twenty or fewer daily attempts per receiving account for controlled experiments. That is its project guideline, not an official universal UPI limit or a guarantee that any use below it is permitted. OpenUPI does not set or certify regulatory limits.

OpenUPI is not represented as an authorized aggregator or as endorsed by NPCI, RBI, banks or UPI apps. This design does not cover collecting, pooling or routing funds for unrelated merchants.

## Reporting future issues

Until a private reporting channel is established, never include secrets, bank messages or customer data in public GitHub issues. Describe a suspected issue with synthetic evidence and request a private disclosure path. Do not invent a security mailbox or response-time guarantee.
