# OpenUPI operations and troubleshooting

**Future runbook. No running OpenUPI services or operational guarantees exist.**

## Startup and restart recovery

Read persisted deadlines rather than resetting them. Expire overdue ACTIVE sessions; record failed verification for overdue PROCESSING sessions; release slots transactionally. Re-register timers for sessions still in their windows and promote eligible queued orders on vacant accounts. Reconcile incomplete webhook deliveries without repeating fulfillment.

State repair must preserve evidence and audit records. A process restart cannot prove that no payment arrived.

## Late-payment workflow

Search recent failed/expired sessions using the configured review horizon. Associate late evidence only when the reference/account/order identity is sufficiently established. Otherwise keep it unmatched. Open a review ticket and emit the planned PAYMENT.LATE_DETECTED event rather than silently paying a new active session with the same amount.

The operator compares official bank records, communicates through authorized support and records fulfillment or a separately executed refund.

## Operational signals

Monitor service readiness, observer heartbeat age, parser errors, unmatched/late evidence, queue age, payment deadlines, webhook attempts, storage health, OAuth failures and support backlog. Logs should use order/event identifiers and redact tokens and unnecessary customer data.

## Backup and restoration

Use a database-consistent SQLite backup method that accounts for WAL state. Protect encryption keys separately, retain required device/OAuth state securely and test restored sessions and deduplication history in isolation. Do not advertise PostgreSQL backup commands before that backend exists.

Before an upgrade, verify backup recovery, schema compatibility and observer/API protocol versions. Rollback must not lose payments or reprocess historical events.

## Troubleshooting matrix

| Symptom | Investigate | Safe response |
| --- | --- | --- |
| OTP missing | Messaging session, delivery, throttles and expiry | Explain delay; offer retry within limits |
| QR never appears | Authentication, receiving-account availability and queue | Inspect authoritative session state |
| Checkout blocked in iframe | Allowed origins, HTTPS and framing policy | Correct explicit merchant origin configuration |
| Android disconnected | Network, permissions, foreground service, battery and enrollment | Reconnect or revoke/re-enroll authorized device |
| Gmail stopped | OAuth expiry/revocation, quota and parser changes | Back off and reauthorize through the operator flow |
| Repeated alerts | Stable event identity and cross-channel correlation | Deduplicate; never repeat fulfillment |
| Customer paid but session failed | Official bank reference, late alert and timestamps | Open review and reconcile before retry advice |
| Webhook rejected | Raw bytes, secret version, timestamp and event identity | Diagnose without disabling validation |
| Queue stuck after restart | Slot ownership, expired sessions and atomic promotion | Repair under an audited operator workflow |
| Wrong order matched | Conflicting reference, equal amount and late evidence | Pause automatic attribution and investigate |

Refund/dispute handling, support ownership, retention periods and incident escalation must be established before a real-money release.
