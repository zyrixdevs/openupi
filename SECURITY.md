# OpenUPI security policy

## Current scope

OpenUPI is in the documentation stage. There are no released applications, supported runtime versions, hosted payment services or security-audited binaries. Reports about unsafe requirements, privacy gaps, misleading security claims and exposed repository secrets are welcome.

| Material | Report handling |
| --- | --- |
| Current main-branch documentation and repository assets | In scope for maintainer review |
| OpenUPI application releases | None available |
| Third-party services and the reference project | Report to their respective owners |

This is a reporting policy. Technical security requirements live in [docs/SECURITY.md](docs/SECURITY.md).

## Report safely

Do not publish exploit details, credentials, customer information, bank alerts or real transaction data in issues or pull requests.

A dedicated private security address and verified private advisory intake have not yet been established. If GitHub displays a “Report a vulnerability” action in this repository's Security tab, use that private action. Otherwise, open a minimal issue titled “Private security contact requested” with no vulnerability details. Wait for a maintainer to establish a private route before sharing sensitive evidence.

If the problem belongs to GitHub itself, use GitHub's reporting channels. If a secret has leaked, its owner should revoke or rotate it promptly rather than rely on removing a public file.

## Useful private report contents

Once a private route is confirmed, provide the affected file/revision, a concise impact statement, reproduction using synthetic data, any preconditions and a suggested fix. State whether anything was already disclosed elsewhere. Share only the information needed to understand the issue.

## Handling and disclosure

Maintainers should acknowledge a report, assess scope, agree on a private communication route and coordinate a fix and disclosure where applicable. No response-time SLA, bounty or compensation is promised.

Avoid testing against real bank accounts, third-party infrastructure or customer data. This policy does not grant legal authorization to test systems you do not own or control.

See [SUPPORT.md](SUPPORT.md) for ordinary questions.
