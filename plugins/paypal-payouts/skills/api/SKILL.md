---
name: payouts
description: "Payouts API skill. Use when working with Payouts for payments. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Payouts
API version: 1.9

## Auth
OAuth2

## Base URL
https://api-m.sandbox.paypal.com

## Setup
1. Configure auth: OAuth2
2. GET /v1/payments/payouts/{id} -- verify access
3. POST /v1/payments/payouts -- create first payouts

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### payments
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/payments/payouts | Create batch payout |
| GET | /v1/payments/payouts/{id} | Show payout batch details |
| GET | /v1/payments/payouts-item/{payout_item_id} | Show payout item details |
| POST | /v1/payments/payouts-item/{payout_item_id}/cancel | Cancel unclaimed payout item |

## Enhanced Skill Content
## Question Mapping

- "How do I send money to multiple people at once?" -> POST /v1/payments/payouts
- "How do I check the status of a batch payout?" -> GET /v1/payments/payouts/{id}
- "What happened to a specific payout item?" -> GET /v1/payments/payouts-item/{payout_item_id}
- "Can I cancel a payout that hasn't been claimed yet?" -> POST /v1/payments/payouts-item/{payout_item_id}/cancel
- "How do I send payouts to Venmo wallets?" -> POST /v1/payments/payouts (set `recipient_wallet` to `VENMO`)
- "How do I paginate through a large batch payout?" -> GET /v1/payments/payouts/{id} (use `page`, `page_size`, `total_required`)
- "What fees were charged on a payout item?" -> GET /v1/payments/payouts-item/{payout_item_id} (check `payout_item_fee`)
- "What exchange rate was applied to a cross-currency payout?" -> GET /v1/payments/payouts-item/{payout_item_id} (check `currency_conversion`)
- "Why did a payout item fail?" -> GET /v1/payments/payouts-item/{payout_item_id} (check `errors` and `transaction_status`)
- "How do I make my payout request idempotent?" -> POST /v1/payments/payouts (set `PayPal-Request-Id` header)
- "How do I know when a batch payout is fully processed?" -> GET /v1/payments/payouts/{id} (poll until `batch_status` is `SUCCESS` or `DENIED`)
- "How do I send payouts by phone number instead of email?" -> POST /v1/payments/payouts (set `recipient_type` to `PHONE`)
- "What's the total amount and fees for an entire batch?" -> GET /v1/payments/payouts/{id} (check `batch_header.amount` and `batch_header.fees`)

## Response Tips

- **Batch creation (POST /payouts):** Returns 201 with `payout_batch_id` in `batch_header` -- store this ID for all subsequent status checks. `batch_status` will initially be `PENDING`; the batch is not yet processed.
- **Batch status (GET /payouts/{id}):** Paginated -- set `total_required=true` to get `total_items` and `total_pages`. Items array contains individual payout statuses. Default `page=1`; iterate through all pages for complete results.
- **Item detail (GET /payouts-item/{id}):** `transaction_status` is the definitive state (`SUCCESS`, `FAILED`, `UNCLAIMED`, `RETURNED`, `ONHOLD`, `BLOCKED`, `REFUNDED`, `REVERSED`). The `errors` object is only present on failed items.
- **Item cancel (POST /payouts-item/{id}/cancel):** Returns the full item object with updated `transaction_status`. Only works on `UNCLAIMED` items -- other statuses return 400.

## Anomaly Flags

- **Batch status `DENIED`**: The entire batch was rejected -- surface immediately with the batch header details so the user can investigate sender account issues.
- **Item `transaction_status` of `ONHOLD` or `BLOCKED`**: Funds are frozen, likely due to compliance review -- flag for manual follow-up.
- **`RETURNED` or `REVERSED` items**: Money came back -- surface the count and total amount so the user can decide whether to retry.
- **Currency conversion with unfavorable `exchange_rate`**: When `currency_conversion` is present, flag the rate so the user can evaluate cost impact on cross-currency payouts.
- **`UNCLAIMED` items approaching expiry**: Items sitting in `UNCLAIMED` status for extended periods should be flagged as candidates for cancellation.
- **High `payout_item_fee` relative to `amount`**: Flag when fees exceed a significant percentage of the payout value (e.g., small-value payouts).
- **400 errors on batch creation**: Often indicate malformed `sender_batch_id` (must be unique) or invalid recipient data -- surface the specific validation error from the response body.
- **Pagination mismatch**: If `total_items` doesn't match the sum of items across all pages, flag a possible data consistency issue.

## Playbook

### 1. Send a Batch Payout and Monitor to Completion

1. Generate a unique `sender_batch_id` (e.g., UUID or timestamp-based).
2. POST `/v1/payments/payouts` with the batch header and items array. Include `PayPal-Request-Id` for idempotency.
3. Store the returned `payout_batch_id` from the 201 response.
4. Poll GET `/v1/payments/payouts/{payout_batch_id}` with `total_required=true`.
5. Continue polling (with backoff) until `batch_status` is `SUCCESS`, `DENIED`, or `CANCELED`.
6. If `SUCCESS`, iterate through pages to verify individual item statuses.

### 2. Investigate and Resolve Failed Payout Items

1. GET `/v1/payments/payouts/{batch_id}` with `total_required=true` to get the full item list.
2. Iterate through all pages, filtering items where `transaction_status` is `FAILED`.
3. For each failed item, GET `/v1/payments/payouts-item/{payout_item_id}` to retrieve the `errors` object.
4. Review `errors.name` and `errors.details` for the root cause (invalid email, insufficient funds, compliance block).
5. Correct the recipient data and include the failed items in a new batch payout with a fresh `sender_batch_id`.

### 3. Cancel Unclaimed Payout Items

1. GET `/v1/payments/payouts/{batch_id}` to list all items in the batch.
2. Filter items with `transaction_status` equal to `UNCLAIMED`.
3. For each unclaimed item, POST `/v1/payments/payouts-item/{payout_item_id}/cancel`.
4. Verify the response shows `transaction_status` updated to `RETURNED`.
5. If cancel returns 400, the item may have been claimed between check and cancel -- re-fetch to confirm current status.

### 4. Reconcile a Cross-Currency Batch Payout

1. GET `/v1/payments/payouts/{batch_id}` to retrieve `batch_header.amount` (total sent) and `batch_header.fees` (total fees).
2. Paginate through all items, collecting each item's `payout_item_fee` and `currency_conversion` data.
3. For items with `currency_conversion`, record `from_amount`, `to_amount`, and `exchange_rate`.
4. Sum all `payout_item_fee` values and compare against `batch_header.fees` as a sanity check.
5. Generate a reconciliation report mapping each `sender_item_id` to its final delivered amount and conversion details.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
