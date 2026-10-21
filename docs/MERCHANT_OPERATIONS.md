# OpenUPI merchant operations

**Planned dashboard and workflows. No admin panel exists yet.**

## Dashboard scope

| Area | Planned operator actions |
| --- | --- |
| Overview | View payment totals/statuses, queue activity and observer health |
| Receiving accounts | Add/edit payee details, enable/disable VPA, set limits and inspect slots |
| Transactions | Search orders, amounts, references, methods and payment states |
| Customers | Inspect authorized profile data, sessions and review history |
| Observers & pairing | Issue enrollment tokens, inspect heartbeat, revoke devices and reconnect Gmail/SMS |
| WhatsApp | Pair the messaging adapter and diagnose OTP delivery |
| Cashier desk | Review pending cash/card counter requests and approve or decline |
| Branding | Configure name, logo, colors, support details and domain settings |
| Support/reconciliation | Review late/conflicting evidence and record a reasoned resolution |
| Audit | Inspect actor, action, time and affected order without exposing secrets |

Admin access must be authenticated and scoped. Multiple merchant accounts must not see each other's orders, credentials or support records.

## Online mode

Offer UPI and COD. UPI follows the account queue and evidence pipeline. COD verifies the customer and gathers the necessary shipping/address confirmation separately. Confirming a COD order is not collecting payment; record the eventual collection state independently.

## Counter mode

Offer UPI, CASH_COUNTER and CARD_COUNTER. Cashier confirmation records receipt of physical cash or the result of a separate POS terminal. Live approval/decline should reach the customer through server events. Decline, timeout and duplicate cashier actions must be handled idempotently.

OpenUPI does not acquire card transactions in this specification. Do not store card numbers, PINs or terminal credentials.

## Queue controls

Show account occupancy and FIFO position. Disabling an account, operator overrides and stale-slot repair must preserve an audit trail. Do not allow manual actions to allocate two active sessions on the same VPA.

## Review and customer help

Review cases include suspicious sessions, wrong amounts, unmatched references and delayed alerts. A support ticket should link to the order, sanitized evidence and operator decision. Verify customer identity before revealing private order details.

For a customer who says they paid, request an appropriate payment reference through the authorized support process and compare it with official bank records. Record manual fulfillment or a separately executed refund without inventing an automated refund capability.

Never tell a customer that funds were not deducted solely because checkout expired or verification failed.
