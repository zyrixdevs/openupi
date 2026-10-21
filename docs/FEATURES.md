# OpenUPI feature catalogue

**Every item is planned.** This catalogue captures the feature scope described in the reference project's README, architecture and operator/developer documents. It does not assert that upstream features were independently tested.

## Checkout and customer identity

| ID | Feature | Target behavior |
| --- | --- | --- |
| C01 | Hosted checkout | A session URL opens the gateway-owned customer flow |
| C02 | Desktop modal | Embedded checkout with a centered modal and background overlay |
| C03 | Mobile bottom sheet | Responsive checkout drawer with usable touch targets |
| C04 | Dynamic SVG QR | Generate a standards-compatible QR from receiving VPA, payee, amount, INR and note |
| C05 | UPI app intents | Offer supported links for GPay, PhonePe, Paytm, CRED and generic UPI; keep QR fallback |
| C06 | Live status | Stream payment state and queue changes with reconnect support and polling fallback |
| C07 | Dual countdowns | Default five-minute payment window and separate thirty-second processing window |
| C08 | Cancel and close | Distinguish modal dismissal from an explicit server-side cancellation |
| C09 | Outcome pages | Success, failed verification, suspicious/review, expired and cancelled |
| A01 | WhatsApp OTP | Deliver a cryptographically random six-digit code before slot allocation |
| A02 | Sign-in/sign-up | Mobile identity, new-customer profile capture and optional email |
| A03 | Remembered profiles | Up to two locally remembered profiles with account switching and logout |
| A04 | Customer sessions | Expiring, revocable sessions; profile cache is not authentication |
| A05 | WhatsApp pairing | Operator-managed connection lifecycle for the planned messaging adapter |

The reference describes a Baileys/Berry messaging connection. OpenUPI retains WhatsApp OTP in scope, but adapter selection and applicable provider terms must be resolved before implementation. Phone possession does not establish payer identity or eliminate fraud.

## Payments, queues and evidence

| ID | Feature | Target behavior |
| --- | --- | --- |
| P01 | Direct UPI receipt | Customer pays the merchant's configured receiving account |
| P02 | No platform transaction fee | Target OpenUPI fee model; no promise about other service costs |
| P03 | Receiving accounts | Manage payee details, enabled accounts, limits and slot availability |
| P04 | Single-slot arbitration | At most one ACTIVE or PROCESSING session per receiving VPA |
| P05 | FIFO queue | Persist waiting order and promote the next eligible customer atomically |
| P06 | Server-owned timing | Persist deadlines across refreshes and process restarts |
| P07 | Exact amount matching | Match integer paise and account, supplemented by references and timing |
| P08 | Observation normalization | Extract amount, account, UTR/reference, payer VPA when available and timestamps |
| P09 | Duplicate suppression | Correlate repeated SMS, push and email evidence without double credit |
| P10 | Evidence levels | Record L1 single-source, L2 two-source and L3 three-source evidence where available |
| P11 | Late observations | Quarantine ambiguous late credit; open review and emit a late-detection event |
| P12 | Restart recovery | Restore pending timers, expire overdue sessions and repair vacant queue slots |
| P13 | Audit trail | Record payment, device, review, queue and webhook changes |
| P14 | Risk controls | Fallible device/browser risk signals, rate limiting, review and reversible restrictions |
| P15 | Durable financial state | SQLite WAL, foreign keys, transactions and integer monetary values |

Cross-channel corroboration is additional evidence, not independent bank settlement certification. Amount equality and a queue do not uniquely identify a payer.

## Observers

| ID | Feature | Target behavior |
| --- | --- | --- |
| O01 | Android SMS | Collect permitted incoming bank SMS on an authorized merchant device |
| O02 | Android notifications | Read allowed bank/UPI credit notifications through notification access |
| O03 | Device enrollment | Short-lived QR/manual token, individual device ID and signing secret |
| O04 | Signed submission | HMAC-SHA256 payloads, authenticated timestamps and replay checks |
| O05 | Device liveness | Heartbeats, last-seen time and disconnected status |
| O06 | Background continuity | Foreground service, reboot recovery and visible permission/battery diagnostics |
| O07 | Gmail API | Read authorized credit-alert mail through scoped OAuth access |
| O08 | Gmail browser adapter | Optional browser observation path with visible connection health |
| O09 | Google Messages Web | Paired browser SMS observer and parser |
| O10 | Parser rules | Versioned source/account rules; ignore debit and unrelated messages |
| O11 | Test simulation | Synthetic notifications, signed test observations and heartbeat scenarios |

## Selling modes and merchant operations

| ID | Feature | Target behavior |
| --- | --- | --- |
| M01 | Online UPI | Customer checkout associated with a merchant order |
| M02 | Cash on Delivery | Verified customer and separate address/order-confirmation lifecycle |
| M03 | COD isolation | Address confirmation must not monopolize a UPI receiving slot |
| M04 | Counter UPI | Customer-facing QR for in-store checkout |
| M05 | Cash at till | Cashier confirms physical cash receipt using CASH_COUNTER |
| M06 | Card at terminal | Cashier records external POS terminal outcome using CARD_COUNTER |
| M07 | Cashier dock | Live pending requests, approve/decline and customer status updates |
| M08 | Admin dashboard | Payment history, queues, accounts, devices, configuration and branding |
| M09 | Review and support | Suspicious and late-payment tickets with audited operator decisions |
| M10 | Payment help | Customer-facing payment lookup/help subject to identity checks |
| M11 | Reconciliation | Compare alert-derived state with official bank records; track discrepancies |
| M12 | Refund workflow | Record and track operator-managed refunds; automatic bank refund execution is not promised |

Card-at-counter means recording an existing external card terminal result. It does not mean OpenUPI processes cards or stores card details.

## Integration, branding and developer tooling

| ID | Feature | Target behavior |
| --- | --- | --- |
| I01 | Single-script embed | Planned openupi.js with merchant public identifier |
| I02 | Declarative button | Planned data-openupi-pay trigger and documented display/redirect attributes |
| I03 | Browser API | Planned OpenUPI.pay entry point with UI callbacks |
| I04 | Browser events | Namespaced success, failed, suspicious, expired and cancelled UI events |
| I05 | Merchant SDK | Planned OpenUPIPaymentClient for backend payment creation and webhook verification |
| I06 | REST API | Payment creation, scoped status, checkout state and authorized COD operations |
| I07 | Signed webhooks | Raw-body HMAC, delivery IDs, signed freshness data and idempotent handling |
| I08 | Framework neutrality | Integration targets include plain HTML, React, Next.js, Vue, Nuxt, Angular and Svelte |
| I09 | Response privacy | Anonymous status is redacted; private data requires scoped credentials |
| B01 | Brand settings | Business name, subtitle, logo, favicon, accent and gradient |
| B02 | Support settings | Merchant support email/phone and help page details |
| B03 | Domain mapping | Merchant-controlled HTTPS domains through a proxy or tunnel |
| B04 | White-label checkout | Configurable product attribution on UI, subject to applicable rights |
| D01 | Control Center | Start/stop supervision, service status and aggregated logs |
| D02 | Demo storefront | Reference merchant purchase flow and five outcome demonstrations |
| D03 | Native host model | Node.js services; no external database or container engine required for baseline |
| D04 | Database bootstrap | Idempotent schema provisioning and non-sensitive development seeds |
| D05 | Documentation | Configuration, observer, integration and operator guides |
| D06 | Validation | Unit, integration, concurrency, recovery, parser and checkout tests before release |

## Completion rule

Each feature requires an implementation link, applicable acceptance evidence and an updated status. No test-suite count, performance figure, bank-coverage claim, live demo or published package is claimed for OpenUPI at this stage.

Detailed acceptance gates are in the [roadmap](ROADMAP.md).
