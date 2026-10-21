# OpenUPI observers

**Planned evidence collection. No OpenUPI Android binary or observer service is supplied.**

## Android observer

Target a Kotlin Android app branded OpenUPI Observer, with candidate application ID com.openupi.observer. Package ownership and release signing must be established before distribution.

The app should capture permitted SMS and bank/UPI notifications, parse credit evidence, sign submissions and report heartbeats. It must not declare an order paid itself.

Enrollment uses a short-lived, single-use QR/manual token issued by Merchant Admin. Bind a unique device ID and individual secret to a merchant. Protect device secrets using Android Keystore-backed storage. Support revocation, re-enrollment and credential rotation.

Use HMAC-SHA256 over an unambiguous versioned envelope containing the exact payload bytes and authenticated timestamp. Proposed request metadata: X-Device-Id, X-Timestamp and X-Signature. A sixty-second freshness tolerance is a design starting point; replay detection must also track event identity.

Planned lifecycle features include foreground execution, reboot recovery, visible connection state, permissions guidance and sixty-second heartbeats. Initial disconnected timeout: 180 seconds. Diagnose battery restrictions and permissions without promising continuous delivery.

Use HTTPS outside explicitly isolated loopback/emulator testing. Grant notification/SMS access only on an authorized device, limit captured sources and avoid unrelated notifications. Build prerequisites are planned JDK 17+ and a supported Android SDK, finalized against the actual implementation. No APK checksum exists for OpenUPI yet.

## Gmail observer

Preferred path: scoped Gmail API access using an operator-owned Google Cloud project and OAuth web client. Register the actual OpenUPI observer callback, authorize the bank-alert mailbox, protect refresh tokens, test the connection and make revocation available.

Target the minimum read scope necessary. Poll incrementally with deduplication, backoff and quota awareness. One-second polling and a five-second corroboration grace period are reference behaviors to evaluate, not guaranteed OpenUPI settings.

An optional Gmail browser adapter remains in scope, with explicit session health and safe reconnection. It cannot silently substitute for a failed or revoked OAuth connection.

Sender-domain allowlists alone do not authenticate email. Evaluate delivery/authentication evidence, parser confidence and account ownership; quarantine uncertain messages. Do not claim verified support for every bank or every .bank.in domain.

## SMS / Google Messages Web observer

Plan an authorized paired Messages Web session with parser rules for known bank senders, amount and payment references. Ignore debit and unrelated alerts. Surface expired pairings and browser-session outages. Protect browser profiles as credentials.

## Shared evidence pipeline

Normalize amountPaise, receivingAccount, reference/utr, senderVpa when present, source and event/ingestion times. Reject malformed or unauthorized submissions. Keep a stable event identity and account-scoped deduplication across channels and restarts.

Evidence tiers indicate one, two or three corroborating sources. SMS and push from one device may be correlated, so source counts must not be presented as three independent settlement checks.

## Endpoint decisions still required

The reference documents use both observer-style and poller-style paths for Android and other inputs. OpenUPI must choose one versioned contract before implementation; neither family is currently a live OpenUPI API.

## Acceptance scenarios

Use synthetic credit and debit alerts, duplicate notifications, delayed delivery, conflicting account/amount/reference, expired enrollment, revoked devices, replayed submissions, lost connectivity, OAuth revocation and quota errors. Fixtures must contain no real customer or bank data.
