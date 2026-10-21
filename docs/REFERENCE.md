# OpenUPI reference and scope notes

## Research source

Feature research used [youpi-pg/YouPI-PG](https://github.com/youpi-pg/YouPI-PG). The branch head observed during research was [3a35c98bdc39b45f9c0197c5ff7bb60a15a2d8c2](https://github.com/youpi-pg/YouPI-PG/commit/3a35c98bdc39b45f9c0197c5ff7bb60a15a2d8c2). Individual documents were retrieved from the moving main branch, so this is a research reference point rather than a claim of a fully pinned source audit.

Materials read: README.md, ARCHITECTURE.md, package.json, and these documentation files: ANDROID_MOBILE_APP.md, CONFIGURATION.md, DEPLOYMENT.md, DEVELOPER_INTEGRATION.md, INSTALLATION.md, MERCHANT_INTEGRATION.md, OBSERVERS_SETUP.md, OPERATIONS_TROUBLESHOOTING.md, WHITE_LABEL.md and google_cloud_console_setup_guide.md.

The reference README credits Gaurav as original creator and Zenuxs as maintainer. Those credits refer to the reference project, not an assertion that either author maintains or endorses OpenUPI.

## Coverage mapping

| Reference topic | OpenUPI specification |
| --- | --- |
| Product overview and features | README.md and FEATURES.md |
| System architecture and queue | ARCHITECTURE.md |
| SDK, REST and browser integration | MERCHANT_INTEGRATION.md |
| Android, Gmail and Google Messages | OBSERVERS.md |
| Environment and secrets | CONFIGURATION.md |
| Installation and hosting | DEPLOYMENT.md |
| Admin, COD, cashier and support | MERCHANT_OPERATIONS.md |
| White-label customization | BRANDING.md |
| Reliability and privacy | SECURITY.md |
| Recovery and troubleshooting | OPERATIONS.md |
| Regression and concurrency testing | ROADMAP.md |

Links in this table refer to sibling files under docs, except the project README at ../README.md. The [documentation index](README.md) provides navigable links.

## Differences resolved in this specification

- The reference documents give different Node.js minima. OpenUPI targets Node.js 24+, subject to actual implementation.
- SQLite is the baseline. PostgreSQL/Redis claims are not inherited as established support.
- References to container files and container availability conflict. OpenUPI promises no container artifact at this stage.
- Android submission paths differ between documents. A single future versioned contract is required.
- Evidence descriptions vary between two levels with a five-second grace period and three-channel tiers. OpenUPI specifies evidence records and leaves final timing policy for implementation.
- Payment status lists vary. OpenUPI separates core lifecycle states from review flags and COD/counter workflows.
- Some reference instructions treat timeout as proof that funds were not deducted. OpenUPI explicitly avoids that assertion.
- Domain lists, APK checksums, live demos and published-package claims are not copied as OpenUPI validation.
- The reference contains differing test-suite counts. OpenUPI claims no executed tests.
- The reference exposes overlapping secret/auth conventions. OpenUPI requires distinct least-privilege credentials and no private merchant secret in a browser.

## Attribution and reuse boundaries

These are newly written product and engineering specifications describing a planned OpenUPI implementation. This commit contains no upstream source, assets, APKs or executable examples. The OpenUPI branding does not change rights to the reference material.

The reviewed upstream package metadata labels its license Commercial, while the README points to a LICENSE file. This is not a verified permission grant. Before importing or modifying upstream implementation, review the applicable license at the chosen revision and obtain any required permission. Original OpenUPI repository material is now governed by the custom [ZYRIX Dev Review and Contribution License](../LICENSE); see [permissions](../PERMISSIONS.md). That license does not cover upstream material or grant rights the project does not hold. “Open” in its name does not make the license OSI-approved.

This is feature/document research, not a full source-code, security, bank-integration or legal audit.
