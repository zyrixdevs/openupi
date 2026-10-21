# Contributing to OpenUPI

Thanks for helping improve OpenUPI. The repository is currently a product specification: documentation, community files and original visual assets. Application implementation has not started.

## Before you begin

Read the [README](README.md), [feature catalogue](docs/FEATURES.md), [roadmap](docs/ROADMAP.md), [license](LICENSE) and [code of conduct](CODE_OF_CONDUCT.md). The custom license permits contributions but does not grant unrestricted commercial reuse.

Useful contributions now include clearer requirements, missing failure scenarios, consistent API terminology, accessibility improvements, documentation corrections and original SVG assets. Propose large scope changes in an issue first. Do not submit application source, dependencies, APKs or deployment automation during this documentation phase.

## Reporting an issue

Use the appropriate issue template. Describe the affected document, expected behavior, actual gap and a concrete example. Link feature IDs when relevant. Check existing issues before opening a duplicate.

Use synthetic data. Never post credentials, OTPs, bank messages, real payment references or customer records. Follow [SECURITY.md](SECURITY.md) for suspected vulnerabilities.

## Pull request workflow

1. Fork the repository and create a descriptive branch such as docs/checkout-states.
2. Make one focused change. Keep product names and proposed contracts consistent.
3. Update any related feature, architecture, operation or reference documents.
4. Check relative links, tables, spelling and rendered SVGs.
5. Open a pull request using the template. Explain the problem, change and validation.
6. Address review comments. A maintainer decides whether and when to merge.

No local application build is required. Do not claim runtime tests passed when only documentation was reviewed.

## Writing and asset conventions

Use OpenUPI for the product and openupi for technical slugs. Use short headings, direct sentences and descriptive link text. Mark unavailable features as planned. Do not add approval, performance, bank-coverage or release claims without evidence.

Keep SVGs self-contained and accessible with a title and description. Avoid scripts, foreignObject, embedded credentials, remote fonts, remote images and external resources. Inspect at mobile and desktop widths.

Preserve third-party notices and cite research sources. Do not copy code, text, logos or media without the necessary rights. No dependency or license changes should be hidden inside an unrelated documentation edit.

## Contribution rights

You retain ownership of your contribution. By deliberately submitting a contribution for inclusion, you confirm you have the right to do so and grant the project and recipients the permissions stated in [LICENSE](LICENSE) for that contribution. You also grant zyrixdevs a non-exclusive, worldwide, perpetual, irrevocable, royalty-free copyright license to reproduce, modify, distribute, sublicense and commercially license that submitted contribution as part of OpenUPI.

This is not a copyright assignment. It does not cover third-party material you cannot license, your unrelated work, or a separate patent or trademark license. Identify any third-party material and its terms before review. If you cannot grant these permissions, discuss that before submitting a contribution.

## Review and communication

Maintainers may request changes, defer implementation proposals or close duplicates and out-of-scope submissions with a reason. Follow [SUPPORT.md](SUPPORT.md) for help and [GOVERNANCE.md](GOVERNANCE.md) for decision-making.
