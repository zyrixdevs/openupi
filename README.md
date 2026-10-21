# OpenUPI

**Self-hosted UPI checkout and merchant payment operations, planned by ZYRIX Dev.**

Direct-to-bank UPI payments · WhatsApp OTP · Dynamic QR checkout · Android, Gmail and SMS observers · Online and counter payments · Merchant branding

> **Documentation stage.** This repository currently contains the OpenUPI product specification and documentation only. Every feature below is planned, not implemented or tested here. There is no application, SDK, Android APK, deployment package or live payment service to install.

## What we are building

OpenUPI is intended to let merchants host their own checkout, receive UPI transfers into their own accounts, and connect observed bank alerts to orders. The target model charges no OpenUPI per-transaction platform fee. Hosting, messaging, domains, banking and maintenance may still cost money.

The design covers the documented feature scope of the [YouPI-PG reference project](https://github.com/youpi-pg/YouPI-PG), expressed as an OpenUPI specification. This repository does not claim to be that project's official successor, an implemented fork or an approved payment provider.

## Planned features

| Area | Scope |
| --- | --- |
| Customer checkout | Desktop modal, mobile bottom sheet, hosted checkout, SVG UPI QR, UPI app links and live status |
| Authentication | Six-digit WhatsApp OTP, sign-in/sign-up, customer sessions and two remembered profiles |
| Payment engine | One active payment slot per receiving VPA, FIFO queue, exact amount matching and server-owned timers |
| Bank observations | Android SMS and notifications, Gmail API/browser observation, Google Messages Web observation |
| Verification | Amount/UTR normalization, duplicate detection, channel evidence levels and manual review for ambiguity |
| Online payments | UPI and Cash on Delivery with separate address confirmation |
| Counter payments | UPI, cashier-confirmed cash and external card terminal payments |
| Merchant operations | Receiving accounts, transaction views, live queues, device pairing, risk review, support and reconciliation |
| Integration | Single-script checkout, declarative buttons, browser API, planned merchant SDK, REST API and signed webhooks |
| Branding | Merchant name, subtitle, logo, favicon, colors, support details and custom domains |
| Reliability | Durable state, restart recovery, late-payment handling, health checks, logs and backups |
| Developer experience | Demo storefront, five outcome pages, simulators and planned regression coverage |

See the [complete feature catalogue](docs/FEATURES.md) for the detailed scope and acceptance criteria.

## Intended payment flow

1. The merchant backend creates an order with a trusted price.
2. The customer opens OpenUPI checkout and verifies their phone.
3. OpenUPI assigns a receiving-account slot or shows the queue position.
4. The customer pays the displayed QR or opens a UPI app.
5. Observers submit bank-alert evidence to the backend.
6. The backend evaluates the evidence, records the result and notifies the merchant.
7. The merchant validates the webhook and reconciles the payment before fulfillment under its payment policy.

An alert or signed webhook alone is not conclusive proof of bank settlement.

## Documentation

| Document | Contents |
| --- | --- |
| [Documentation index](docs/README.md) | Reading order and project status |
| [Features](docs/FEATURES.md) | Complete planned feature scope |
| [Architecture](docs/ARCHITECTURE.md) | Services, data, boundaries and payment states |
| [Merchant integration](docs/MERCHANT_INTEGRATION.md) | Planned browser, SDK, REST and webhook contracts |
| [Observers](docs/OBSERVERS.md) | Android, Gmail and SMS evidence collection |
| [Configuration](docs/CONFIGURATION.md) | Proposed configuration and secret handling |
| [Deployment](docs/DEPLOYMENT.md) | Future hosting model and service ports |
| [Merchant operations](docs/MERCHANT_OPERATIONS.md) | Admin workflows, COD and cashier operations |
| [Branding](docs/BRANDING.md) | OpenUPI naming and merchant customization |
| [Security and reliability](docs/SECURITY.md) | Trust model, privacy and failure handling |
| [Operations](docs/OPERATIONS.md) | Recovery, reconciliation and troubleshooting |
| [Roadmap](docs/ROADMAP.md) | Implementation phases and acceptance gates |
| [Reference and scope](docs/REFERENCE.md) | Reference materials, unresolved differences and attribution |

## Current availability

Only Markdown documents are included. Installation commands, downloadable binaries, package publication and supported bank lists will be added after implementation and validation. Proposed identifiers in these documents are design targets, not working interfaces.

## Research boundaries

OpenUPI is not represented as NPCI-approved, RBI-approved, bank-approved, audited or production-ready. Bank alerts can be delayed, missing, duplicated or misleading. A timed-out checkout does not establish that no funds moved. Receiving-account eligibility and any required approvals must be confirmed before real customer use.

## Attribution and licensing

The feature research references YouPI-PG, originally created by Gaurav and described by its README as maintained by Zenuxs. OpenUPI branding does not transfer ownership of upstream work or remove applicable attribution requirements. These documents are newly written specifications; no upstream source code, media or binaries are included. No software license is selected or implied by the OpenUPI name. See [reference notes](docs/REFERENCE.md).
