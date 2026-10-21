# OpenUPI roadmap

**Documentation baseline created. All product implementation phases remain planned.**

| Phase | Scope | Exit evidence |
| --- | --- | --- |
| 0 — Specification | README, feature catalogue, architecture and operations docs | Consistent names, linked documents and clear implementation status |
| 1 — Foundation | Workspace, contracts, SQLite schema, scoped auth and secret handling | Migrations, tenant-isolation and monetary-boundary checks |
| 2 — Payment engine | Sessions, single-slot queue, deadlines, attribution and recovery | Parallel allocation, expiry, restart and late-evidence scenarios |
| 3 — Checkout and identity | Hosted/modal/mobile UI, SVG QR, WhatsApp OTP and profiles | Device/browser flows, session expiry and abuse-control checks |
| 4 — Observers | Android, Gmail, Messages Web, normalization and evidence levels | Replay, duplicate, spoofed/malformed and disconnected-source scenarios |
| 5 — Merchant operations | Admin, COD, cashier desk, branding and support | Role checks, COD slot isolation and idempotent cashier actions |
| 6 — Integration | openupi.js, backend SDK, REST and webhooks | Trusted order creation, raw-body signatures and exactly-once business processing |
| 7 — Operational review | Packaging, monitoring, backups, privacy and reconciliation | Restore drill, outage exercises and independent security review |

## Feature acceptance gates

- Checkout: desktop and mobile flows remain usable; app intents retain QR fallback.
- Identity: OTP abuse controls work; remembered profiles cannot bypass authentication.
- Queue: simultaneous requests never allocate two active sessions on one VPA.
- Money: decimal parsing rejects invalid amounts and safely converts to bounded integer paise.
- Attribution: duplicate, mismatched, wrong-account and late evidence never silently pays a different order.
- Observers: rejected/revoked credentials and replayed payloads cannot create accepted payment evidence.
- Merchant isolation: one merchant cannot read or modify another merchant's private records.
- Webhooks: altered bytes, stale signed envelopes and duplicate events cannot cause fulfillment.
- COD/counter: unpaid COD and external cashier confirmations remain distinct from UPI receipt.
- Recovery: restart retains deadlines, queue order, evidence and delivery history.
- Branding: settings are validated; product identifiers use OpenUPI consistently.
- Customer outcomes: timeouts never claim funds were definitely not deducted.
- Release: runnable commands, package names, APK provenance and supported versions are documented only once real artifacts are validated.

## Open design decisions

Finalize OTP adapter, API/observer routes, evidence grace timing, risk-review transitions, secret/key rotation, refund responsibilities and any future license changes. The current repository license is recorded in [LICENSE](../LICENSE). Decide whether any future code will be independently implemented or reused under verified upstream permission.

Do not assign completion percentages or passing test counts until implementation evidence exists.
