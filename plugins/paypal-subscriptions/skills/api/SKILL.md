---
name: subscriptions
description: "Subscriptions API skill. Use when working with Subscriptions for billing. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# Subscriptions
API version: 1.8

## Auth
OAuth2

## Base URL
https://api-m.sandbox.paypal.com

## Setup
1. Configure auth: OAuth2
2. GET /v1/billing/plans -- verify access
3. POST /v1/billing/plans -- create first plans

## Endpoints

16 endpoints across 1 groups. See references/api-spec.lap for full details.

### billing
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/billing/plans | Create plan |
| GET | /v1/billing/plans | List plans |
| GET | /v1/billing/plans/{id} | Show plan details |
| PATCH | /v1/billing/plans/{id} | Update plan |
| POST | /v1/billing/plans/{id}/activate | Activate plan |
| POST | /v1/billing/plans/{id}/deactivate | Deactivate plan |
| POST | /v1/billing/plans/{id}/update-pricing-schemes | Update pricing |
| POST | /v1/billing/subscriptions | Create subscription |
| GET | /v1/billing/subscriptions/{id} | Show subscription details |
| PATCH | /v1/billing/subscriptions/{id} | Update subscription |
| POST | /v1/billing/subscriptions/{id}/revise | Revise plan or quantity of subscription |
| POST | /v1/billing/subscriptions/{id}/suspend | Suspend subscription |
| POST | /v1/billing/subscriptions/{id}/cancel | Cancel subscription |
| POST | /v1/billing/subscriptions/{id}/activate | Activate subscription |
| POST | /v1/billing/subscriptions/{id}/capture | Capture authorized payment on subscription |
| GET | /v1/billing/subscriptions/{id}/transactions | List transactions for subscription |

## Enhanced Skill Content
## Question Mapping

- "How do I create a billing plan?" -> POST /v1/billing/plans
- "List all my billing plans" -> GET /v1/billing/plans
- "Get details for a specific plan" -> GET /v1/billing/plans/{id}
- "How do I update a billing plan?" -> PATCH /v1/billing/plans/{id}
- "Activate an inactive plan" -> POST /v1/billing/plans/{id}/activate
- "Deactivate a plan so no new subscribers can join" -> POST /v1/billing/plans/{id}/deactivate
- "Change the pricing on an existing plan" -> POST /v1/billing/plans/{id}/update-pricing-schemes
- "Create a new subscription for a customer" -> POST /v1/billing/subscriptions
- "Get subscription details and current status" -> GET /v1/billing/subscriptions/{id}
- "Update subscriber information on a subscription" -> PATCH /v1/billing/subscriptions/{id}
- "Change a subscriber's plan or quantity" -> POST /v1/billing/subscriptions/{id}/revise
- "Pause a subscription temporarily" -> POST /v1/billing/subscriptions/{id}/suspend
- "Cancel a subscription permanently" -> POST /v1/billing/subscriptions/{id}/cancel
- "Reactivate a suspended subscription" -> POST /v1/billing/subscriptions/{id}/activate
- "Charge an outstanding balance on a subscription" -> POST /v1/billing/subscriptions/{id}/capture

## Response Tips

- **Plans list** (`GET /plans`): Paginated via `page` and `page_size` (default 10); set `total_required=true` to get `total_items` and `total_pages` -- without it these fields may be absent. Follow `links` array for HATEOAS navigation.
- **Plan detail** (`GET /plans/{id}`): `billing_cycles` is an array ordered by `sequence`; each cycle contains nested `pricing_scheme.fixed_price` and `frequency` maps. Check `status` field for CREATED/ACTIVE/INACTIVE.
- **Plan mutations** (`PATCH`, activate, deactivate, update-pricing): Return 204 No Content on success -- no response body. Any non-204 indicates failure.
- **Subscription creation** (`POST /subscriptions`): May return 200 or 201; both are success. Response includes HATEOAS `links` with an `approve` URL the subscriber must visit. Use `Prefer: return=representation` header to get the full object back.
- **Subscription transactions** (`GET /subscriptions/{id}/transactions`): Paginated like plans; requires `start_time` and `end_time` as ISO 8601 strings. Response `transactions` array contains payment records.
- **Capture** (`POST /subscriptions/{id}/capture`): Returns 200 with `amount_with_breakdown` containing `gross_amount`, `fee_amount`, `net_amount`, etc. A 202 means the capture is still processing asynchronously.
- **Error responses** (400, 422): Contain structured error details with `name`, `message`, and `details` array pinpointing which fields failed validation.

## Anomaly Flags

- **422 Unprocessable Entity**: Surface the `details` array -- it contains field-level validation errors that are not obvious from the status code alone.
- **202 Accepted on capture**: The payment is not yet complete. Alert the user that they need to poll or check later for the final capture status.
- **Plan status mismatch**: If a user tries to create a subscription against an INACTIVE or CREATED plan, flag that the plan must be ACTIVE first.
- **Missing `total_items` in list responses**: If `total_required` was not set to `true`, pagination metadata is incomplete. Proactively suggest adding it.
- **`setup_fee_failure_action`**: When set to `CANCEL`, a failed setup fee will auto-cancel the subscription. Surface this if the user has it configured, as it may cause unexpected cancellations.
- **`payment_failure_threshold` at 0**: This means the subscription cancels on the very first failed payment. Flag if this seems unintentional.
- **Idempotency header missing**: If `PayPal-Request-Id` is omitted on POST requests (create plan, create subscription, capture), warn that retries could create duplicates.
- **Deprecated or unusual `billing_cycles` config**: If `total_cycles` is set to 0 (infinite) on a TRIAL tenure type, flag that the trial will never end.

## Playbook

### 1. Set Up a Recurring Subscription from Scratch

1. Create a billing plan with `POST /v1/billing/plans`, specifying `product_id`, `name`, `billing_cycles` (with frequency and pricing), and `payment_preferences`.
2. Note the returned plan `id` and confirm `status` is ACTIVE (or activate it with `POST /v1/billing/plans/{id}/activate`).
3. Create a subscription with `POST /v1/billing/subscriptions`, passing the `plan_id` and an `application_context` with `return_url` and `cancel_url`.
4. Extract the `approve` link from the response `links` array and redirect the subscriber to it.
5. After subscriber approval, verify the subscription status with `GET /v1/billing/subscriptions/{id}`.

### 2. Change Pricing on an Active Plan

1. Retrieve current plan details with `GET /v1/billing/plans/{id}` to review existing `billing_cycles` and their `sequence` numbers.
2. Call `POST /v1/billing/plans/{id}/update-pricing-schemes` with `pricing_schemes` array, matching each entry's `billing_cycle_sequence` to the cycle you want to update.
3. Verify the update by fetching the plan again with `GET /v1/billing/plans/{id}`.
4. Note: existing subscribers keep their current pricing unless you revise their individual subscriptions.

### 3. Suspend and Later Reactivate a Subscription

1. Suspend the subscription with `POST /v1/billing/subscriptions/{id}/suspend`, providing a `reason` string (required).
2. Confirm suspension by checking `GET /v1/billing/subscriptions/{id}` -- status should be SUSPENDED.
3. When ready to resume, call `POST /v1/billing/subscriptions/{id}/activate` with an optional `reason`.
4. Verify reactivation via `GET /v1/billing/subscriptions/{id}` -- status should return to ACTIVE.

### 4. Upgrade or Downgrade a Subscriber

1. Get the current subscription details with `GET /v1/billing/subscriptions/{id}`.
2. Call `POST /v1/billing/subscriptions/{id}/revise` with the new `plan_id` and/or updated `quantity`, `shipping_amount`, or overridden `plan.billing_cycles`.
3. Check `plan_overridden` in the response to confirm whether plan-level overrides were applied.
4. If the response includes an `approve` link in `links`, redirect the subscriber for approval of the revised terms.

### 5. Capture an Outstanding Balance and Review Transactions

1. Capture the outstanding amount with `POST /v1/billing/subscriptions/{id}/capture`, providing `note`, `capture_type` (e.g., `OUTSTANDING_BALANCE`), and `amount` with `currency_code` and `value`.
2. Include a `PayPal-Request-Id` header for idempotency.
3. If you receive 202 instead of 200, the capture is processing -- check back later.
4. Review all transactions with `GET /v1/billing/subscriptions/{id}/transactions`, passing `start_time` and `end_time` as ISO 8601 date strings.
5. Inspect `amount_with_breakdown` on each transaction for fee, tax, and net amount details.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
