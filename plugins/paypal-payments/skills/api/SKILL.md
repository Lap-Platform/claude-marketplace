---
name: payments
description: "Payments API skill. Use when working with Payments for payments. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Payments
API version: 2.8

## Auth
OAuth2

## Base URL
https://api-m.sandbox.paypal.com

## Setup
1. Configure auth: OAuth2
2. GET /v2/payments/authorizations/{authorization_id} -- verify access
3. POST /v2/payments/authorizations/{authorization_id}/capture -- create first capture

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/payments/authorizations/{authorization_id} | Show details for authorized payment |
| POST | /v2/payments/authorizations/{authorization_id}/capture | Capture authorized payment |
| POST | /v2/payments/authorizations/{authorization_id}/reauthorize | Reauthorize authorized payment |
| POST | /v2/payments/authorizations/{authorization_id}/void | Void authorized payment |
| GET | /v2/payments/captures/{capture_id} | Show captured payment details |
| POST | /v2/payments/captures/{capture_id}/refund | Refund captured payment |
| GET | /v2/payments/refunds/{refund_id} | Show refund details |

## Enhanced Skill Content
## Question Mapping

- "How do I check the status of a payment authorization?" -> GET /v2/payments/authorizations/{authorization_id}
- "How do I capture an authorized payment?" -> POST /v2/payments/authorizations/{authorization_id}/capture
- "Can I extend an authorization that's about to expire?" -> POST /v2/payments/authorizations/{authorization_id}/reauthorize
- "How do I cancel an authorization I no longer need?" -> POST /v2/payments/authorizations/{authorization_id}/void
- "How do I look up details of a captured payment?" -> GET /v2/payments/captures/{capture_id}
- "How do I refund a customer?" -> POST /v2/payments/captures/{capture_id}/refund
- "Can I do a partial refund?" -> POST /v2/payments/captures/{capture_id}/refund (pass `amount` with partial value)
- "How do I check the status of a refund?" -> GET /v2/payments/refunds/{refund_id}
- "How do I capture a payment for a different amount than authorized?" -> POST /v2/payments/authorizations/{authorization_id}/capture (include amount in body)
- "How do I void an authorization after a failed capture attempt?" -> POST /v2/payments/authorizations/{authorization_id}/void
- "How do I issue a refund with a note to the buyer?" -> POST /v2/payments/captures/{capture_id}/refund (pass `note_to_payer`)
- "How do I reauthorize with a different amount?" -> POST /v2/payments/authorizations/{authorization_id}/reauthorize (pass `amount`)
- "How do I process a refund and track it against my invoice?" -> POST /v2/payments/captures/{capture_id}/refund (pass `invoice_id`)
- "How do I make an API call on behalf of a merchant?" -> Any endpoint, pass `PayPal-Auth-Assertion` header

## Response Tips

- **Authorizations** (GET/POST): Response includes `status` field (CREATED, CAPTURED, VOIDED, EXPIRED, PENDING) -- always check this before attempting capture or void. The `amount` object nests `currency_code` and `value` as strings, not numbers.
- **Captures** (GET/POST): Capture responses return 200 for existing or 201 for newly created; check both. The `status` field can be COMPLETED, DECLINED, PARTIALLY_REFUNDED, PENDING, REFUNDED. Links in `_links` array provide HATEOAS navigation to related refund and authorization resources.
- **Refunds** (GET/POST): Refund `status` can be CANCELLED, FAILED, PENDING, COMPLETED. The `seller_payable_breakdown` object contains the net amount, PayPal fee, and total refunded -- use this for reconciliation rather than the top-level `amount`.
- **Errors**: All error responses follow the PayPal error schema with `name`, `message`, and `details[]` array. The `details[].issue` field gives the machine-readable error code; `details[].description` gives human-readable guidance. 422 errors mean the request was syntactically valid but semantically rejected (e.g., refund exceeds capture amount).
- **Idempotency**: POST endpoints accept `PayPal-Request-Id` for idempotent retries. If you replay the same request ID, you get the original response back rather than a duplicate action.

## Anomaly Flags

- **409 Conflict on capture or void**: The authorization has already been captured, voided, or expired -- surface the current `status` from a follow-up GET call so the user understands what happened.
- **422 Unprocessable Entity on refund**: Typically means refund amount exceeds the remaining capturable/refundable balance. Surface the `details[].issue` value (e.g., `REFUND_AMOUNT_EXCEEDED`, `CAPTURE_FULLY_REFUNDED`).
- **Authorization nearing expiry**: PayPal authorizations expire after ~3 days (standard) or ~29 days (honor period). If a GET on an authorization shows `expiration_time` approaching, proactively suggest reauthorization or capture.
- **PENDING status on captures or refunds**: Indicates PayPal is still processing. Agent should recommend polling the GET endpoint and warn the user not to retry the POST.
- **403 Forbidden**: Usually means the caller lacks permission for the resource (wrong merchant context). Surface this as a credentials/scope issue, not a resource-not-found problem.
- **Deprecated `Prefer: return=minimal`**: If PayPal starts returning full representations despite this header, flag it as a potential API version change.
- **Missing `PayPal-Request-Id` on POST calls**: Proactively warn that without idempotency keys, network retries risk duplicate captures or refunds.

## Playbook

### 1. Capture an Authorized Payment

1. Retrieve the authorization: `GET /v2/payments/authorizations/{authorization_id}`
2. Verify `status` is `CREATED` or `APPROVED` (not `VOIDED` or `EXPIRED`)
3. Capture the payment: `POST /v2/payments/authorizations/{authorization_id}/capture` with a unique `PayPal-Request-Id`
4. Check response status -- 201 means success; inspect `status` field for `COMPLETED` vs `PENDING`
5. Store the returned `capture_id` for future refund or lookup operations

### 2. Issue a Partial Refund

1. Look up the capture: `GET /v2/payments/captures/{capture_id}`
2. Confirm `status` is `COMPLETED` and note the captured `amount`
3. Submit partial refund: `POST /v2/payments/captures/{capture_id}/refund` with `amount: { currency_code: "USD", value: "10.00" }` and a unique `PayPal-Request-Id`
4. Optionally include `note_to_payer` and `invoice_id` for tracking
5. Verify the refund: `GET /v2/payments/refunds/{refund_id}` and confirm `status` is `COMPLETED`

### 3. Void an Unused Authorization

1. Retrieve the authorization: `GET /v2/payments/authorizations/{authorization_id}`
2. Confirm `status` is `CREATED` (cannot void a captured or already-voided authorization)
3. Void it: `POST /v2/payments/authorizations/{authorization_id}/void` with a `PayPal-Request-Id`
4. Expect a 204 (no content) on success; re-fetch with GET to confirm `status` is now `VOIDED`

### 4. Reauthorize an Expiring Payment

1. Check the authorization: `GET /v2/payments/authorizations/{authorization_id}`
2. Inspect `expiration_time` -- if within 24 hours of expiry, proceed
3. Reauthorize: `POST /v2/payments/authorizations/{authorization_id}/reauthorize` with the same or updated `amount`
4. A 201 response provides a new authorization with a fresh expiration window
5. Capture using the new authorization ID before it also expires

### 5. Multi-step Order Fulfillment (Authorize, Capture, Refund)

1. Start with an authorization ID from a completed checkout flow
2. Verify authorization status: `GET /v2/payments/authorizations/{authorization_id}`
3. Capture when ready to ship: `POST /v2/payments/authorizations/{authorization_id}/capture`
4. If the customer requests a return, look up the capture: `GET /v2/payments/captures/{capture_id}`
5. Issue refund: `POST /v2/payments/captures/{capture_id}/refund` (full or partial amount)
6. Confirm refund processed: `GET /v2/payments/refunds/{refund_id}` and verify `status` is `COMPLETED`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
