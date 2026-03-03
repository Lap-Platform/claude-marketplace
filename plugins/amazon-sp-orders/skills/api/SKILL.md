---
name: the-selling-partner-api-for-orders
description: "The Selling Partner API for Orders API skill. Use when working with The Selling Partner API for Orders for orders. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# The Selling Partner API for Orders
API version: 2026-01-01

## Auth
No authentication required.

## Base URL
https://sellingpartnerapi-na.amazon.com

## Setup
1. No auth setup needed
2. GET /orders/2026-01-01/orders -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /orders/2026-01-01/orders | Returns orders that are created or updated during the time period that you specify. You can filter the response for specific types of orders. |
| GET | /orders/2026-01-01/orders/{orderId} | Returns the order that you specify. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my recent orders?" -> GET /orders/2026-01-01/orders
- "Show me orders created in the last 7 days" -> GET /orders/2026-01-01/orders (with createdAfter/createdBefore)
- "Which orders were updated since yesterday?" -> GET /orders/2026-01-01/orders (with lastUpdatedAfter)
- "Get details for a specific order" -> GET /orders/2026-01-01/orders/{orderId}
- "Show me all pending orders" -> GET /orders/2026-01-01/orders (with fulfillmentStatuses)
- "List orders fulfilled by Amazon (FBA)" -> GET /orders/2026-01-01/orders (with fulfilledBy=AFN)
- "List orders fulfilled by merchant (FBM)" -> GET /orders/2026-01-01/orders (with fulfilledBy=MFN)
- "How do I paginate through a large order list?" -> GET /orders/2026-01-01/orders (with paginationToken from previous response)
- "Show orders for a specific marketplace" -> GET /orders/2026-01-01/orders (with marketplaceIds)
- "Get order details including buyer info and shipping address" -> GET /orders/2026-01-01/orders/{orderId} (with includedData)
- "How many orders do I have today?" -> GET /orders/2026-01-01/orders (with createdAfter set to start of day)
- "Find orders between two dates across multiple marketplaces" -> GET /orders/2026-01-01/orders (with createdAfter, createdBefore, marketplaceIds)

## Response Tips

- **Order lists**: Results are paginated. Check for a `NextToken` or `paginationToken` in the response -- if present, pass it as `paginationToken` in the next request to fetch more pages. Respect `maxResultsPerPage` (default may vary).
- **Single order**: Returns the full order object. Use `includedData` to control which nested objects (buyer info, shipping address, order items) are included; omitting it returns a minimal response.
- **Errors**: 429 means you hit the rate limit -- back off and retry with exponential delay. 503 indicates a temporary service issue -- retry after a short wait. 400 typically means a malformed parameter (check date formats and enum values). 413 means the request payload or query is too large.

## Anomaly Flags

- **Rate limiting (429)**: Surface immediately with retry-after timing. SP-API has strict per-endpoint burst and restore rates -- warn when multiple 429s occur in sequence.
- **503 Service Unavailable**: Flag repeated 503s as a potential Amazon-side outage; suggest checking Seller Central status page.
- **Empty result sets**: If a broad query (no date filters) returns zero orders, flag as unexpected -- the seller account may lack permissions or the marketplace ID may be wrong.
- **Pagination loops**: Detect if the same paginationToken is returned twice in a row, indicating a potential API issue -- surface rather than looping infinitely.
- **Missing includedData fields**: If requested included data (e.g., buyer info) comes back null or absent on an order, flag it -- this often indicates PII restrictions or a pending order state.
- **400 on date parameters**: Date format mismatches are a frequent cause -- surface the expected ISO 8601 format proactively when the user provides dates.

## Playbook

### 1. Export All Orders for a Date Range

1. Call `GET /orders/2026-01-01/orders` with `createdAfter` and `createdBefore` set to the desired range, plus `marketplaceIds` for the target marketplace.
2. Collect the orders from the response.
3. If a `paginationToken` is present in the response, call the same endpoint again with the token.
4. Repeat step 3 until no more pagination tokens are returned.
5. Optionally, for each order, call `GET /orders/2026-01-01/orders/{orderId}` with `includedData` to fetch full details.

### 2. Monitor New Orders in Real Time

1. Record the current timestamp as `lastCheck`.
2. Periodically call `GET /orders/2026-01-01/orders` with `createdAfter` set to `lastCheck`.
3. Process any returned orders.
4. Update `lastCheck` to the current timestamp.
5. Respect rate limits -- space polling intervals at least 60 seconds apart to avoid 429 errors.

### 3. Get Complete Order Details with Buyer Info

1. Call `GET /orders/2026-01-01/orders/{orderId}` with `includedData` set to include buyer and shipping information.
2. Extract the buyer name, shipping address, and order items from the response.
3. If buyer info is restricted (null), note that PII access requires additional SP-API authorization (Restricted Data Token).

### 4. Audit Fulfillment Channel Split

1. Call `GET /orders/2026-01-01/orders` with `fulfilledBy=AFN` and desired date filters to get FBA orders. Paginate to completion.
2. Call `GET /orders/2026-01-01/orders` with `fulfilledBy=MFN` and the same date filters to get FBM orders. Paginate to completion.
3. Compare counts to understand the fulfillment channel distribution.

### 5. Track Recently Updated Orders

1. Call `GET /orders/2026-01-01/orders` with `lastUpdatedAfter` set to the last sync timestamp.
2. For each returned order, call `GET /orders/2026-01-01/orders/{orderId}` to get the current full state.
3. Compare against local records to identify status changes (shipped, cancelled, returned).
4. Paginate through all results before updating the sync timestamp.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
