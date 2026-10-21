# OpenUPI merchant integration

**Proposed contracts only. No script, SDK, API server or package is available.**

## Order authority

The merchant backend owns order ID, amount and currency. Browser attributes are display/invocation inputs, never trusted pricing. The payment API must bind a checkout to server-validated order data. Customer authentication belongs to hosted checkout.

## Planned integration surfaces

| Surface | OpenUPI identifier | Purpose |
| --- | --- | --- |
| Browser bundle | /openupi.js | Hosted universal checkout script |
| Public merchant attribute | data-openupi-key | Non-secret merchant identifier |
| Payment trigger | data-openupi-pay | Bind a checkout button |
| Browser entry point | OpenUPI.pay | Programmatic modal/drawer invocation |
| Backend client | OpenUPIPaymentClient | Payment creation, lookup and webhook verification |
| Candidate package scope | @openupi/merchant-sdk | Reserved design name only; ownership/publication unverified |
| UI events | openupi:payment:success / failed / suspicious / expired / cancelled | Update storefront presentation |
| Merchant callback route | /api/openupi-webhook | Merchant-chosen receiver, not a mandatory URL |

Never put a merchant secret, observer token or admin token into script tags, browser storage or public attributes.

## Checkout inputs

The planned declarative interface retains data-order-id, data-amount, data-currency, data-name, data-description, data-customer-name, data-customer-email, data-customer-phone and data-metadata. Redirect attributes cover success, failed, suspicious, expired and cancelled pages. Customer fields are hints; verification and private profile access still require authentication.

The browser API should accept the hosted checkout URL, trusted order/session reference, display details and handler/onFailed/onClose callbacks. Closing a modal must not falsely claim the backend payment was cancelled.

## Proposed REST surface

| Method and path | Intended behavior |
| --- | --- |
| POST /api/v1/payments | Create a merchant-scoped order payment and checkout URL |
| GET /api/v1/payments/:id | Return a redacted public status or authorized private view |
| GET /api/v1/checkout/:id/state | Return current checkout state within caller permissions |
| GET /api/v1/payments/:id/cod | Retrieve permitted COD state |
| GET /api/v1/orders/:orderId/cod | Retrieve merchant-scoped COD information |

Creation fields: orderId, exact decimal amount or integer amountPaise, INR currency, method, absolute returnUrl and optional metadata. The future versioned API must resolve input precedence and reject contradictory amounts. Creation and retries need idempotency semantics before release.

A returnUrl must be an allowed absolute HTTP(S) URL, with HTTPS required outside local testing. Relative storefront redirects can be resolved by the SDK against the merchant origin before submission.

## Authentication and privacy

Use separate private merchant credentials, customer sessions, observer credentials and admin credentials. X-Merchant-Id or data-openupi-key identifies a merchant but is not authorization. The reference's X-Merchant-Key convention can inform a future private API, but OpenUPI must not reuse webhook secrets as broad browser credentials. Public status must omit customer contact data, internal risk notes and private metadata.

## Webhook contract

Planned headers: X-Gateway-Signature, X-Gateway-Event, X-Gateway-Delivery-Id and X-Gateway-Timestamp. Proposed event fields include event, paymentId, orderId, amount, amountPaise, currency, method, utr/reference, completedAt and merchant-approved metadata. References must preserve bank-supplied formats rather than assume every reference has twelve digits.

Planned outcomes: SUCCESS, FAILED, EXPIRED and CANCELLED, plus a review indication and PAYMENT.LATE_DETECTED. The final API must define exact event names and schemas before shipping.

Receiver requirements:

1. Verify HMAC-SHA256 using raw bytes and constant-time comparison.
2. Authenticate timestamp and delivery ID as part of the signed envelope; reject stale or replayed deliveries.
3. Verify merchant/order identity, expected amount, currency and allowed state transition.
4. Apply each business event once, even if transport retries use a new delivery attempt.
5. Persist receipt before acknowledging. Retry failures with bounded backoff and operator visibility.
6. Reconcile against official bank records under the merchant's policy.

A valid signature proves the message came from a holder of the signing key. It does not prove bank settlement. Browser callbacks are presentation signals only.

## Outcome pages

/order-success shows the accepted result and reference; /order-failed explains verification could not complete; /order-suspicious explains review; /order-expired explains the checkout deadline; /order-cancelled explains cancellation. Failed, expired and cancelled pages must provide help if the customer already paid. None may guarantee that no money was deducted.
