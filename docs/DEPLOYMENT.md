# OpenUPI deployment plan

**Not an installation guide for a released application. Only documentation exists.**

## Intended host model

Baseline: Node.js 24+ on Linux, macOS or Windows, npm workspace services and embedded SQLite. Final supported versions must be confirmed when dependencies and source exist. A native host should not require PostgreSQL, Redis or Docker.

Container packaging is a possible later delivery option. No Dockerfile, Compose configuration, package manifest, startup script, database migration, APK or deployable artifact is included in this repository.

## Proposed topology

| Service | Default port | Exposure |
| --- | --- | --- |
| Payment API | 6100 | Only routes required by merchants/checkout; restrict operator routes |
| Checkout portal | 7000 | Customer-facing HTTPS |
| Merchant admin | 6001 | Authenticated operator access |
| Demo storefront | 5000 | Isolated test/demo use |
| Payment help | 3000 | Authorized customer assistance |
| SMS observer | 6002 | Private operator service |
| Gmail observer | 6003 | Private service plus explicitly routed OAuth callback |
| Control Center | 8090 | Private operator supervision |
| Android observer | None | Outbound authenticated HTTPS to gateway |

Each host service should provide a non-sensitive /health endpoint. Readiness should verify dependencies and migrations without disclosing tokens or bank data.

## Future setup sequence

1. Select a tested OpenUPI release and verify its provenance.
2. Prepare supported Node.js, persistent storage and a dedicated unprivileged service account.
3. Configure unique secrets, service origins and allowed merchant domains.
4. Provision the SQLite schema and isolated development merchant idempotently.
5. Configure a receiving account and enroll authorized observers.
6. Set up a TLS proxy or tunnel with access restrictions for private services.
7. Validate a synthetic checkout, signed webhook, restart recovery and backup restoration.
8. Consider real-money evaluation only after the applicable bank, security and operational reviews.

Actual install/start/test commands will be added with executable source. Do not run upstream commands expecting this repository to work.

## Network and persistence

Terminate HTTPS through a configured reverse proxy or tunnel. Preserve SSE connections and trusted proxy metadata. Configure separate checkout, API, admin and help origins as needed; domain ownership and routing are operator responsibilities. No hosted OpenUPI domain is promised.

Keep database, WAL-related storage, secrets, OAuth state and device state outside ephemeral build output. Back up consistently, restrict file permissions and test restoration. Preserve event/idempotency history during upgrades.

See [Configuration](CONFIGURATION.md) for proposed names and [Operations](OPERATIONS.md) for failure handling.
