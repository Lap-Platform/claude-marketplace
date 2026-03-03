---
name: transaction-search
description: "Transaction Search API skill. Use when working with Transaction Search for reporting. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Transaction Search
API version: 1.9

## Auth
OAuth2

## Base URL
https://api-m.sandbox.paypal.com

## Setup
1. Configure auth: OAuth2
2. GET /v1/reporting/transactions -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### reporting
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/reporting/transactions | List transactions |
| GET | /v1/reporting/balances | List all balances |

## Enhanced Skill Content
## Question Mapping

- "Show me recent PayPal transactions" -> GET /v1/reporting/transactions
- "Find a transaction by ID" -> GET /v1/reporting/transactions (with transaction_id filter)
- "What transactions happened last week?" -> GET /v1/reporting/transactions (with start_date/end_date)
- "Show only completed payments" -> GET /v1/reporting/transactions (with transaction_status=S)
- "List all refunds in a date range" -> GET /v1/reporting/transactions (with transaction_type=T0002)
- "What's my current PayPal balance?" -> GET /v1/reporting/balances
- "Get my balance in EUR" -> GET /v1/reporting/balances (with currency_code=EUR)
- "How many transactions did a specific store process?" -> GET /v1/reporting/transactions (with store_id)
- "Show credit card payments only" -> GET /v1/reporting/transactions (with payment_instrument_type)
- "What was my balance yesterday?" -> GET /v1/reporting/balances (with as_of_time)
- "Get the next page of transaction results" -> GET /v1/reporting/transactions (with page=N)
- "Show all transactions that affected my balance" -> GET /v1/reporting/transactions (with balance_affecting_records_only=Y)
- "Find transactions from a specific terminal" -> GET /v1/reporting/transactions (with terminal_id)
- "Get full transaction details including payer and cart info" -> GET /v1/reporting/transactions (with fields=all)

## Response Tips

- **Transactions**: Results are paginated -- check `total_pages` and `total_items` to know if more pages exist. Use `page` param to iterate. The `links` array contains HATEOAS navigation URIs. Each entry in `transaction_details` is a nested map with sub-objects (transaction_info, payer_info, shipping_info, cart_info) depending on the `fields` param.
- **Balances**: The `balances` array contains one entry per currency held. `as_of_time` and `last_refresh_time` indicate data freshness -- balances are not real-time. A missing `currency_code` param returns all currency balances.
- **Errors**: 400 means malformed dates or invalid filter values -- check that dates use ISO 8601 format (e.g., `2024-01-01T00:00:00-0700`). 403 indicates missing OAuth scope (needs `https://uri.paypal.com/services/reporting/search/read`). 500 is transient -- retry with backoff.

## Anomaly Flags

- **Stale data**: If `last_refreshed_datetime` (transactions) or `last_refresh_time` (balances) is more than 24 hours old, warn the user that results may not reflect recent activity.
- **Truncated results**: If `total_items` exceeds `page_size * total_pages` or if `total_items` hits the 2147483647 cap, flag that results may be incomplete -- narrow the date range.
- **Date range limits**: PayPal restricts transaction searches to a 31-day window. If the user requests a wider range, proactively split into multiple sequential calls.
- **Empty results with filters**: If a filtered query returns zero `transaction_details` but an unfiltered query for the same range returns results, surface this mismatch -- the filter value may be malformed.
- **Balance currency gaps**: If the user expects a specific currency in `balances` but it is absent, flag that no funds are held in that currency.
- **HTTP 403 on first call**: Likely an OAuth scope issue -- prompt the user to verify their app permissions before retrying.

## Playbook

### 1. Reconcile Transactions for a Date Range

1. Call `GET /v1/reporting/transactions` with `start_date`, `end_date`, and `fields=all` to get full detail.
2. Check `total_pages` in the response. If greater than 1, loop through pages by incrementing `page`.
3. Collect all `transaction_details` entries across pages.
4. Call `GET /v1/reporting/balances` with `as_of_time` set to the `end_date` to get the closing balance.
5. Compare the sum of balance-affecting transactions against the reported balance.

### 2. Investigate a Specific Transaction

1. Call `GET /v1/reporting/transactions` with the `transaction_id` and a broad date range (up to 31 days around the expected date).
2. If no results, widen the date range or check that the ID format is correct.
3. Set `fields=all` to retrieve payer info, shipping info, and cart info in a single call.
4. Review `transaction_status` and `transaction_type` in the response to understand the current state.

### 3. Daily Balance Snapshot

1. Call `GET /v1/reporting/balances` without params to get current balances in all currencies.
2. Note the `last_refresh_time` to confirm data freshness.
3. To compare against a prior day, call again with `as_of_time` set to the target date.
4. Diff the `balances` arrays to identify changes per currency.

### 4. Filter Transactions by Payment Method and Store

1. Call `GET /v1/reporting/transactions` with `start_date`, `end_date`, `store_id`, and `payment_instrument_type` (e.g., `CREDITCARD`).
2. Set `page_size=100` for efficient pagination.
3. Iterate through all pages, collecting results.
4. Aggregate totals from `transaction_amount` fields within each `transaction_details` entry.

### 5. Export All Balance-Affecting Transactions

1. Determine the target month. Split into 31-day windows if needed.
2. Call `GET /v1/reporting/transactions` with `balance_affecting_records_only=Y`, `fields=transaction_info`, and the date window.
3. Page through all results using `page` until `page` equals `total_pages`.
4. Concatenate all `transaction_details` arrays into a single dataset for export.
5. Validate the count matches `total_items` from the first response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
