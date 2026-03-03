---
name: orders
description: "Orders API skill. Use when working with Orders for checkout. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# Orders
API version: 2.25

## Auth
OAuth2

## Base URL
https://api-m.sandbox.paypal.com

## Setup
1. Configure auth: OAuth2
2. GET /v2/checkout/orders/{id} -- verify access
3. POST /v2/checkout/orders -- create first orders

## Endpoints

9 endpoints across 1 groups. See references/api-spec.lap for full details.

### checkout
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/checkout/orders | Create order |
| GET | /v2/checkout/orders/{id} | Show order details |
| PATCH | /v2/checkout/orders/{id} | Update order |
| POST | /v2/checkout/orders/{id}/confirm-payment-source | Confirm the Order |
| POST | /v2/checkout/orders/{id}/authorize | Authorize payment for order |
| POST | /v2/checkout/orders/{id}/capture | Capture payment for order |
| POST | /v2/checkout/orders/{id}/track | Add tracking information for an Order. |
| PATCH | /v2/checkout/orders/{id}/trackers/{tracker_id} | Update or cancel tracking information for an order |
| POST | /v2/checkout/orders/order-update-callback | Receive updated order information via callback URL |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new PayPal order?" -> POST /v2/checkout/orders
- "How do I capture payment for an order?" -> POST /v2/checkout/orders/{id}/capture
- "How do I authorize a payment without capturing it?" -> POST /v2/checkout/orders/{id}/authorize
- "How do I look up the details of an existing order?" -> GET /v2/checkout/orders/{id}
- "How do I update an order after it's been created?" -> PATCH /v2/checkout/orders/{id}
- "How do I confirm which payment method the buyer is using?" -> POST /v2/checkout/orders/{id}/confirm-payment-source
- "How do I add shipment tracking to a captured order?" -> POST /v2/checkout/orders/{id}/track
- "How do I update tracking information for a shipment?" -> PATCH /v2/checkout/orders/{id}/trackers/{tracker_id}
- "How do I handle shipping address changes during checkout?" -> POST /v2/checkout/orders/order-update-callback
- "How do I create an order that uses Apple Pay or Google Pay?" -> POST /v2/checkout/orders (with `payment_source.apple_pay` or `payment_source.google_pay`)
- "How do I set up a two-step payment (authorize then capture)?" -> POST /v2/checkout/orders (intent=AUTHORIZE), then POST /v2/checkout/orders/{id}/authorize, then capture later
- "How do I create an order with multiple items and shipping?" -> POST /v2/checkout/orders (with `purchase_units[].items[]` and `purchase_units[].shipping`)
- "How do I vault a card for future payments?" -> POST /v2/checkout/orders (with `payment_source.card.attributes` vault config)
- "How do I use a stored payment method for a returning customer?" -> POST /v2/checkout/orders (with `payment_source.card.vault_id` or `payment_source.paypal.vault_id`)

## Response Tips

- **Order creation/retrieval** (POST/GET /orders): Response includes nested `purchase_units[]` with `payments.captures[]` and `payments.authorizations[]` -- always drill into these for transaction IDs and statuses.
- **Capture/Authorize** (POST /orders/{id}/capture, /authorize): Returns 200 or 201; check the order `status` field (COMPLETED, APPROVED, VOIDED) and `purchase_units[].payments` for individual capture/authorization details.
- **Patch** (PATCH /orders/{id}): Returns 204 No Content on success -- absence of a body IS the success signal.
- **Tracking** (POST /track, PATCH /trackers): Returns the full order object on 200/201; look for `purchase_units[].shipping.trackers[]` to confirm tracking was attached.
- **Errors** (400/401/403/404/422/500): Response body contains `name`, `message`, and `details[]` array with `field`, `value`, `issue`, and `description` per validation failure -- iterate `details` to surface all problems, not just the first.

## Anomaly Flags

- **422 UNPROCESSABLE_ENTITY**: Surface the `details[].issue` codes immediately -- common issues include `DUPLICATE_INVOICE_ID`, `ORDER_NOT_APPROVED`, `ORDER_ALREADY_CAPTURED`, and `INSTRUMENT_DECLINED` which each require different remediation.
- **401 AUTHENTICATION_FAILURE**: OAuth2 token may be expired; agent should proactively suggest refreshing the access token before retrying.
- **Intent mismatch**: If an order was created with `intent=AUTHORIZE` but a capture is attempted (or vice versa), flag this before the call to avoid a 422.
- **Missing payment_source on capture/authorize**: If no `payment_source` was set during order creation and none is passed to capture/authorize, the call will fail -- flag when both are absent.
- **Idempotency header absent**: For POST endpoints, flag when `PayPal-Request-Id` is missing on retries, as duplicate orders/captures could result.
- **Sandbox vs production base URL**: Flag if the base URL is `sandbox.paypal.com` when the user appears to intend production use, or vice versa.
- **Deprecated `application_context`**: The `application_context` field on order creation overlaps with `payment_source.*.experience_context` -- flag usage of both simultaneously as it can cause conflicts.

## Playbook

### 1. Standard Checkout (Create and Capture)

1. POST /v2/checkout/orders with `intent: "CAPTURE"`, `purchase_units` containing item details and amounts
2. Redirect the buyer to the `approve` link from the response HATEOAS links
3. After buyer approval, POST /v2/checkout/orders/{id}/capture with the order ID
4. Check `status: "COMPLETED"` and extract `purchase_units[0].payments.captures[0].id` as the transaction ID
5. Store the capture ID for refunds or tracking

### 2. Authorize Then Capture Later

1. POST /v2/checkout/orders with `intent: "AUTHORIZE"` and purchase unit details
2. Redirect buyer to approve; after approval, POST /v2/checkout/orders/{id}/authorize
3. Store `purchase_units[0].payments.authorizations[0].id` -- the authorization is valid for up to 29 days
4. When ready to fulfill, use the Payments API to capture against the authorization ID
5. Optionally void the authorization if the order is canceled

### 3. Add Shipment Tracking After Capture

1. Capture the order first (see Playbook 1)
2. POST /v2/checkout/orders/{id}/track with `capture_id`, `tracking_number`, `carrier` (use the enum value matching your carrier), and `notify_payer: true`
3. Confirm the tracker appears in the response under `purchase_units[].shipping.trackers[]`
4. If tracking info changes, PATCH /v2/checkout/orders/{id}/trackers/{tracker_id} to update

### 4. Checkout with Alternative Payment Method (e.g., Bancontact, iDEAL)

1. POST /v2/checkout/orders with `intent: "CAPTURE"` and the relevant `payment_source` block (e.g., `payment_source.ideal` with `name`, `country_code`, and `experience_context` including `return_url` and `cancel_url`)
2. Follow the redirect link in the response to send the buyer to the payment provider
3. On callback to your `return_url`, GET /v2/checkout/orders/{id} to check status
4. If status is `APPROVED`, POST /v2/checkout/orders/{id}/capture to complete payment

### 5. Confirm Payment Source Mid-Flow

1. POST /v2/checkout/orders to create the order without specifying `payment_source`
2. Collect payment details from the buyer in your own UI
3. POST /v2/checkout/orders/{id}/confirm-payment-source with the chosen `payment_source` (card, PayPal, etc.)
4. If the response includes a `payer_action` link (e.g., 3D Secure), redirect the buyer
5. After confirmation, POST /v2/checkout/orders/{id}/capture to finalize


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
