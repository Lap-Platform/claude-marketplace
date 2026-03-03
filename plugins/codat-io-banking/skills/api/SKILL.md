---
name: banking-api
description: "Banking API skill. Use when working with Banking for companies. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Banking API
API version: 3.0.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.codat.io

## Setup
1. Set your API key in the appropriate header
2. GET /companies/{companyId}/connections/{connectionId}/data/banking-accountBalances -- verify access

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### companies
| Method | Path | Description |
|--------|------|-------------|
| GET | /companies/{companyId}/connections/{connectionId}/data/banking-accountBalances | List account balances |
| GET | /companies/{companyId}/connections/{connectionId}/data/banking-accounts | List accounts |
| GET | /companies/{companyId}/connections/{connectionId}/data/banking-accounts/{accountId} | Get account |
| GET | /companies/{companyId}/connections/{connectionId}/data/banking-transactionCategories | List transaction categories |
| GET | /companies/{companyId}/connections/{connectionId}/data/banking-transactionCategories/{transactionCategoryId} | Get transaction category |
| GET | /companies/{companyId}/connections/{connectionId}/data/banking-transactions | List transactions |
| GET | /companies/{companyId}/data/banking-transactions | List banking transactions |
| GET | /companies/{companyId}/connections/{connectionId}/data/banking-transactions/{transactionId} | Get bank transaction |

## Enhanced Skill Content
## Question Mapping

- "What are the account balances for this company?" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-accountBalances
- "List all banking accounts connected to a company" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-accounts
- "Get details for a specific bank account" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-accounts/{accountId}
- "What transaction categories are available?" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-transactionCategories
- "Look up a specific transaction category by ID" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-transactionCategories/{transactionCategoryId}
- "Show me recent banking transactions for a connection" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-transactions
- "List all transactions across all connections for a company" -> GET /companies/{companyId}/data/banking-transactions
- "Get details of a specific transaction" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-transactions/{transactionId}
- "How many bank accounts does this company have?" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-accounts (check pagination totals)
- "Search transactions matching a specific query?" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-transactions with `query` param
- "Get the second page of account balances?" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-accountBalances with `page=2`
- "Sort transactions by date?" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-transactions with `orderBy` param
- "What is the balance across all accounts for a company?" -> GET /companies/{companyId}/connections/{connectionId}/data/banking-accountBalances (aggregate results client-side)
- "Get transactions for a company without specifying a connection?" -> GET /companies/{companyId}/data/banking-transactions

## Response Tips

- **List endpoints** (accounts, balances, transactions, categories): Responses are paginated. Check `pageNumber`, `pageSize`, and `totalResults` in the response envelope. Default page size is 100.
- **Single-resource endpoints** (account by ID, transaction by ID, category by ID): Return the object directly. A 404 means the ID does not exist under that company/connection.
- **Error responses**: All endpoints share a consistent error model. 400 indicates bad query/filter syntax, 402 means the feature is not available on the current plan, 409 signals a data sync conflict, 429 is rate limiting.

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately. Back off and retry with exponential delay. Alert user that rate limits are being hit.
- **402 Payment Required**: Proactively warn that the company's Codat plan may not include banking data access.
- **409 Conflict**: Flag that data may be mid-sync. Suggest retrying after the data connection finishes syncing.
- **503 Service Unavailable**: Upstream banking provider may be down. Surface the issue and recommend checking connection health.
- **Empty paginated results with totalResults > 0**: Indicates the requested page is out of range. Suggest adjusting the `page` parameter.
- **400 on query/orderBy**: The Codat query syntax is specific. Surface the malformed query and suggest checking the Codat query language docs.
- **404 on connection or company IDs**: Proactively confirm whether the UUIDs are valid before retrying.

## Playbook

### 1. Retrieve a Full Financial Snapshot for a Company

1. Call GET `/companies/{companyId}/connections/{connectionId}/data/banking-accounts` to list all accounts
2. Call GET `/companies/{companyId}/connections/{connectionId}/data/banking-accountBalances` to get current balances
3. For each account of interest, call GET `/companies/{companyId}/connections/{connectionId}/data/banking-transactions` with a `query` filter for that account
4. Combine accounts, balances, and transactions into a unified view

### 2. Page Through All Transactions

1. Call GET `/companies/{companyId}/connections/{connectionId}/data/banking-transactions` with `page=1&pageSize=100`
2. Read `totalResults` from the response to calculate total pages
3. Loop from `page=2` to the last page, collecting all results
4. Optionally use `orderBy` to sort by date for chronological ordering

### 3. Categorize Transactions

1. Call GET `/companies/{companyId}/connections/{connectionId}/data/banking-transactionCategories` to fetch all categories
2. Call GET `/companies/{companyId}/connections/{connectionId}/data/banking-transactions` to fetch transactions
3. Match each transaction's category ID against the category list
4. Group and summarize transactions by category name

### 4. Cross-Connection Transaction Search

1. Call GET `/companies/{companyId}/data/banking-transactions` (no connectionId) to search across all connections
2. Use the `query` parameter to filter by amount, date range, or description
3. Use `orderBy` to sort results as needed
4. Page through results if `totalResults` exceeds `pageSize`

### 5. Investigate a Specific Transaction

1. Call GET `/companies/{companyId}/connections/{connectionId}/data/banking-transactions/{transactionId}` to get full details
2. Note the transaction's category ID, then call GET `/companies/{companyId}/connections/{connectionId}/data/banking-transactionCategories/{transactionCategoryId}` to resolve the category name
3. Call GET `/companies/{companyId}/connections/{connectionId}/data/banking-accounts/{accountId}` using the transaction's account ID to get account context


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
