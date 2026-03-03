---
name: commerce-api
description: "Commerce API skill. Use when working with Commerce for companies. Covers 21 endpoints."
version: 1.0.0
generator: lapsh
---

# Commerce API
API version: 3.0.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.codat.io

## Setup
1. Set your API key in the appropriate header
2. GET /companies/{companyId}/connections/{connectionId}/data/commerce-customers -- verify access

## Endpoints

21 endpoints across 1 groups. See references/api-spec.lap for full details.

### companies
| Method | Path | Description |
|--------|------|-------------|
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-customers | List customers |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-customers/{customerId} | Get customer |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-disputes | List disputes |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-disputes/{disputeId} | Get dispute |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-info | Get company info |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-locations | List locations |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-locations/{locationId} | Get location |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-orders | List orders |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-orders/{orderId} | Get order |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-payments | List payments |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-payments/{paymentId} | Get payment |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-paymentMethods | List payment methods |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-paymentMethods/{paymentMethodId} | Get payment method |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-products | List products |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-products/{productId} | Get product |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-transactions | List transactions |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-transactions/{transactionId} | Get transaction |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-productCategories | List product categories |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-productCategories/{productId} | Get product category |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-taxComponents | List tax components |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-taxComponents/{taxId} | Get tax component |

## Enhanced Skill Content
## Question Mapping

- "List all customers for a commerce connection?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-customers
- "Get details for a specific customer?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-customers/{customerId}
- "Show me all orders with pagination?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-orders
- "Look up a specific order by ID?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-orders/{orderId}
- "What payment methods does this company accept?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-paymentMethods
- "List all open disputes for a connection?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-disputes
- "Get the details of a specific dispute?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-disputes/{disputeId}
- "What products does a company sell?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-products
- "Get commerce store info for a connection?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-info
- "List all store locations?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-locations
- "Show recent payments for a connection?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-payments
- "What product categories exist?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-productCategories
- "List all transactions for a connection?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-transactions
- "What tax components apply to this company's commerce data?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-taxComponents
- "Get details on a specific payment?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-payments/{paymentId}

## Response Tips

- **Paginated lists** (customers, orders, products, disputes, payments, transactions, payment methods, product categories, tax components): Responses include page metadata. Default `page=1`, `pageSize=100`. Use `query` for server-side filtering and `orderBy` for sorting. Always check if more pages exist before assuming the dataset is complete.
- **Single-resource lookups** (by customerId, orderId, etc.): Return the full object directly. A 404 means the ID does not exist within that company/connection scope -- double-check both `companyId` and `connectionId`.
- **Commerce info and locations**: Non-paginated. Info returns a single object with store-level metadata. Locations list may not support pagination parameters.
- **Error responses**: 400 = bad query/filter syntax, 402 = billing/plan issue, 409 = data conflict or sync in progress, 429 = rate limited, 503 = upstream commerce platform unavailable.

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately with retry-after guidance. All 21 endpoints can return this -- batch operations should include backoff logic.
- **402 Payment Required**: Indicates a Codat plan or billing issue. Alert the user that their account may need attention before retrying.
- **409 Conflict**: Often signals a data sync is in progress. Suggest waiting and retrying rather than treating as a permanent failure.
- **503 Service Unavailable**: The upstream commerce platform (Shopify, Stripe, etc.) may be down. Flag as external dependency issue, not a Codat API problem.
- **400 on list endpoints only**: Bad `query` or `orderBy` syntax. Surface the likely parameter causing the issue since detail endpoints never return 400.
- **Empty paginated results**: If page 1 returns zero results, flag that the connection may not have synced commerce data yet or the data type is unsupported by the platform.
- **Stale data patterns**: If commerce-info returns old timestamps, proactively note that a data refresh/sync may be needed.

## Playbook

### 1. Full Commerce Data Audit for a Company

1. Call GET `/companies/{companyId}/connections/{connectionId}/data/commerce-info` to confirm the connection is active and check last sync time.
2. Call GET `.../commerce-locations` to enumerate all store locations.
3. Call GET `.../commerce-products?pageSize=100` and paginate through all pages to build a full product catalog.
4. Call GET `.../commerce-productCategories?pageSize=100` to map category IDs to names.
5. Call GET `.../commerce-orders?pageSize=100&orderBy=-createdDate` to pull recent orders.
6. Cross-reference product IDs in orders against the product catalog for a complete audit view.

### 2. Dispute Investigation Workflow

1. Call GET `.../commerce-disputes?pageSize=100` to list all disputes.
2. Filter results by status (using the `query` parameter if supported) to isolate open/unresolved disputes.
3. For each dispute of interest, call GET `.../commerce-disputes/{disputeId}` to get full details including reason and evidence.
4. Call GET `.../commerce-orders/{orderId}` for the linked order to understand the original transaction context.
5. Call GET `.../commerce-payments/{paymentId}` if the dispute references a specific payment.

### 3. Payment Reconciliation

1. Call GET `.../commerce-payments?pageSize=100&orderBy=-date` to list recent payments, paginating as needed.
2. Call GET `.../commerce-paymentMethods?pageSize=100` to build a lookup of payment method IDs to names/types.
3. Call GET `.../commerce-transactions?pageSize=100` to get the transaction ledger.
4. Match payments to transactions using shared reference IDs.
5. Flag any transactions without a matching payment or vice versa for manual review.

### 4. Product Catalog Sync

1. Call GET `.../commerce-productCategories?pageSize=100` and paginate to retrieve all categories.
2. Call GET `.../commerce-products?pageSize=100` and paginate through the full product list.
3. For any product needing enrichment, call GET `.../commerce-products/{productId}` for complete details.
4. Call GET `.../commerce-taxComponents?pageSize=100` to retrieve tax rules that apply to products.
5. Map tax component IDs from products to their full definitions for a complete catalog export.

### 5. Multi-Location Revenue Overview

1. Call GET `.../commerce-locations` to list all store locations and their IDs.
2. Call GET `.../commerce-orders?pageSize=100&orderBy=-createdDate` and paginate through orders.
3. Group orders by location ID from the order data.
4. Call GET `.../commerce-payments?pageSize=100` and correlate payments to orders.
5. Aggregate payment totals per location to build a revenue-by-location summary.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
