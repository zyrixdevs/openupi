# OpenUPI configuration

**Proposed settings. No .env template or runtime configuration loader is included.**

## Service and storage settings

| Setting | Proposed value/purpose |
| --- | --- |
| NODE_ENV | development or production; enforce production restrictions server-side |
| PAYMENT_API_PORT | 6100 |
| CHECKOUT_PORTAL_PORT | 7000 |
| MERCHANT_ADMIN_PORT | 6001 |
| HELP_PORTAL_PORT | 3000 |
| CONTROL_CENTER_PORT | 8090 |
| SMS_OBSERVER_PORT | 6002 |
| GMAIL_OBSERVER_PORT | 6003 |
| DEMO_STORE_PORT | 5000 |
| SQLITE_DB_PATH | data/openupi.sqlite |
| BASE_PAYMENT_API_URL | Public/private API origin appropriate to the deployment |
| BASE_CHECKOUT_URL | Customer-facing checkout origin |
| BASE_ADMIN_URL / BASE_HELP_URL / BASE_DEMO_STORE_URL | Corresponding service origins |
| PAYMENT_ACTIVE_WINDOW_MS | 300000; five-minute payment window |
| PAYMENT_PROCESSING_WINDOW_MS | 30000; thirty-second verification window |
| LATE_OBSERVATION_WINDOW_MS | 1800000; thirty-minute review search horizon |
| ANDROID_HEARTBEAT_TIMEOUT_MS | 180000; disconnected-device threshold |
| CHECKOUT_FRAME_ANCESTORS | Explicit merchant origins permitted to embed checkout |

The late-observation horizon is not permission to assign an old credit automatically to a newer session. Additional timing and reference policy is required.

## Secrets and connection settings

| Setting | Intended purpose |
| --- | --- |
| ENCRYPTION_MASTER_KEY | Independent high-entropy 256-bit key for protected credentials |
| JWT_SECRET | Only if signed session tokens are selected; otherwise use opaque server-side sessions |
| ADMIN_API_TOKEN | Operator authorization with restricted scope |
| OBSERVER_API_TOKEN | Observer ingestion authorization, not unrestricted customer-data access |
| ANDROID_ENROLLMENT_SECRET | Enrollment protection; never embedded in a public APK |
| OPENUPI_WEBHOOK_SECRET | Merchant-specific webhook signing, stored server-side |
| OPENUPI_DEMO_WEBHOOK_SECRET | Isolated demo merchant credential |
| GMAIL_CLIENT_ID / GMAIL_CLIENT_SECRET | Operator-owned OAuth client credentials |
| GMAIL_REDIRECT_URI | Registered callback, proposed localhost observer path /oauth/callback on port 6003 |
| OPENUPI_EXPOSE_DEV_OTP | Local development only; refuse in production |
| OPENUPI_ALLOW_DEV_TOOLS | Isolated simulator access; disable production exposure |
| OPENUPI_ALLOW_PRIVATE_WEBHOOKS | Explicit controlled exception for LAN integrations; off by default |

No generated values or default credentials are provided here. The implementation must refuse insecure production defaults, redact credentials from logs, protect secret files and support rotation. Source control, browser attributes and screenshots are not secret stores.

## URL and origin rules

Allowlist merchant origins for embedding and redirects. Validate outbound webhook destinations, including DNS resolution and redirect behavior, to prevent SSRF. A private-webhook exception must not disable authentication or URL validation.

The baseline is SQLite. DATABASE_URL, PostgreSQL fallback and Redis settings are deliberately not advertised as working configuration; they require a separately validated backend.

See [Deployment](DEPLOYMENT.md) and [Security](SECURITY.md).
