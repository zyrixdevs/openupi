# OpenUPI brand and naming

**OpenUPI is the product name. openupi is the repository and technical slug.**

## Canonical identifiers

| Surface | Proposed OpenUPI name |
| --- | --- |
| Product | OpenUPI |
| Project organization | ZYRIX Dev / GitHub zyrixdevs |
| Repository | zyrixdevs/openupi |
| Browser bundle | openupi.js |
| Browser namespace | OpenUPI |
| Browser invocation | OpenUPI.pay |
| Declarative trigger | data-openupi-pay |
| Public merchant identifier | data-openupi-key |
| Browser event prefix | openupi:payment: |
| Merchant client | OpenUPIPaymentClient |
| Candidate package namespace | @openupi/*; not reserved or published |
| Local database | data/openupi.sqlite |
| Android display name | OpenUPI Observer |
| Candidate Android package | com.openupi.observer; ownership to verify |
| Candidate APK filename | openupi-observer.apk; no binary available |
| Product-specific environment prefix | OPENUPI_ |

Do not claim backward compatibility with another project's browser globals, package names, device enrollment or database paths. Those require deliberate migration work.

## Merchant customization

Plan merchant-specific app/business name, subtitle, logo URL, favicon, accent color, header gradient, support email and phone. Apply branding consistently to checkout, payment help and outcome pages. Validate and safely render user-supplied text, URLs and colors.

Use merchant-owned HTTPS domains through a reverse proxy or tunnel. Example domain names in docs are placeholders; no public domain or DNS ownership is implied.

Merchants may choose product attribution in the UI, subject to applicable license/notice requirements. UI branding settings do not grant permission to erase third-party copyright notices or portray another project's work as original OpenUPI code.

## Documentation rules

Use OpenUPI throughout product descriptions and proposed technical contracts. Keep the reference project's actual name only in attribution, reference links and explicit research comparisons. Do not copy upstream screenshots, demo videos, APK checksums, test badges, approval claims or release numbers into OpenUPI marketing.
