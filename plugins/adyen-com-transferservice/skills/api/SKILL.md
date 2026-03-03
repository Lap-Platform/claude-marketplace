---
name: transfers-api
description: "Transfers API skill. Use when working with Transfers for grants, transactions, transfers. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# Transfers API
API version: 3

## Auth
ApiKey X-API-Key in header | Bearer basic | ApiKey clientKey in query

## Base URL
https://balanceplatform-api-test.adyen.com/btl/v3

## Setup
1. Set Authorization header with your Bearer token
2. GET /grants -- verify access
3. POST /grants -- create first grants

## Endpoints

9 endpoints across 3 groups. See references/api-spec.lap for full details.

### grants
| Method | Path | Description |
|--------|------|-------------|
| GET | /grants | Get a capital account |
| POST | /grants | Request a grant payout |
| GET | /grants/{id} | Get grant reference details |

### transactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /transactions | Get all transactions |
| GET | /transactions/{id} | Get a transaction |

### transfers
| Method | Path | Description |
|--------|------|-------------|
| POST | /transfers | Transfer funds |
| POST | /transfers/approve | Approve initiated transfers |
| POST | /transfers/cancel | Cancel initiated transfers |
| POST | /transfers/{transferId}/returns | Return a transfer |

## Enhanced Skill Content
## Question Mapping

- "How do I send money to another balance account?" -> POST /transfers
- "Show me all transactions from last week" -> GET /transactions
- "What grants are available for this account holder?" -> GET /grants
- "How do I apply for a grant?" -> POST /grants
- "What is the status of grant {id}?" -> GET /grants/{id}
- "Can I cancel a pending transfer?" -> POST /transfers/cancel
- "How do I return funds from a completed transfer?" -> POST /transfers/{transferId}/returns
- "How do I approve a transfer that requires review?" -> POST /transfers/approve
- "Show me the details of transaction {id}" -> GET /transactions/{id}
- "List all transactions for a specific balance account" -> GET /transactions (with balanceAccountId filter)
- "How do I schedule a transfer for a future date?" -> POST /transfers (with executionDate)
- "What is the repayment schedule on my grant?" -> GET /grants/{id}
- "How do I make an instant bank transfer?" -> POST /transfers (with priority: instant)
- "How do I paginate through a large transaction list?" -> GET /transactions (with cursor and limit)

## Response Tips

- **Grants**: `POST /grants` returns nested `balances` (fee/principal/total) and `repayment.term` with estimated vs maximum days -- always check both. `GET /grants` returns a flat `grants` array of maps.
- **Transactions**: Paginated via `_links.next.href` and `_links.prev.href` cursors -- follow `href` directly rather than constructing URLs. The `amount.value` is in minor units (cents). Note `createdAt` vs `creationDate` and `bookingDate` vs `valueDate` -- they represent different stages of processing.
- **Transfers**: `POST /transfers` returns **202 Accepted** (not 200) -- the transfer is queued, not complete. Check `status` field for actual state. Approve/cancel endpoints return empty 200 bodies on success.
- **Errors**: All endpoints share 401/403/500. Grants and transfers additionally return 400/404/422. A 422 typically means validation failure -- inspect the response body for field-level details.

## Anomaly Flags

- **202 vs 200 on transfer creation**: Surface that the transfer is asynchronous and not yet settled. Prompt the user to check status or set up a webhook.
- **Grant repayment threshold**: When `repayment.threshold.amount` is present, flag that automatic repayment triggers exist and explain the basis points rate.
- **Missing Idempotency-Key on writes**: If the user omits `Idempotency-Key` on POST /grants, POST /transfers, or return/approve/cancel calls, warn about potential duplicate operations on retry.
- **Transfer review required**: When a transfer response includes `review.numberOfApprovalsRequired > 0`, proactively surface that the transfer is pending approval and needs a follow-up `POST /transfers/approve`.
- **Transaction date range required**: `GET /transactions` requires both `createdSince` and `createdUntil` -- flag if the user tries to list transactions without a time window.
- **Unexpected 403**: Could indicate the API credential lacks permission for the specific balance platform or account holder -- suggest checking API credential scope in the Adyen dashboard.

## Playbook

### 1. Send Money to a Bank Account

1. Prepare the transfer payload with `amount` (currency + value in minor units), `category: "bank"`, and `counterparty.bankAccount` details
2. Set an `Idempotency-Key` header to prevent duplicates
3. Call `POST /transfers` -- expect a 202 response
4. Check the `status` field in the response (e.g., `authorised`, `pending`)
5. If `review.numberOfApprovalsRequired` is present, call `POST /transfers/approve` with the `transferId` to complete the flow

### 2. Apply for and Monitor a Grant

1. Call `GET /grants` with `counterpartyAccountHolderId` to see available grants and retrieve the `grantOfferId`
2. Call `POST /grants` with `grantAccountId` and `grantOfferId` (include `Idempotency-Key`)
3. Note the returned `id`, `status`, and `repayment` terms (basis points, estimated days, threshold)
4. Periodically call `GET /grants/{id}` to monitor `balances` (principal remaining, fees accrued, total outstanding)

### 3. Paginate Through Transaction History

1. Call `GET /transactions` with `createdSince` and `createdUntil` for your date range, and `limit` for page size (e.g., 50)
2. Process the `data` array in the response
3. If `_links.next.href` exists, use its value as the URL for the next page (it includes the cursor)
4. Repeat until `_links.next` is absent

### 4. Return Funds from a Transfer

1. Identify the `transferId` of the original completed transfer
2. Call `POST /transfers/{transferId}/returns` with `amount` (currency + value) -- partial returns are supported
3. Include a `reference` for reconciliation and an `Idempotency-Key` for safety
4. Check the response `status` to confirm the return was accepted

### 5. Bulk Approve or Cancel Pending Transfers

1. Collect the `id` values of transfers in a reviewable/pending state
2. To approve: call `POST /transfers/approve` with `transferIds` array (include `Idempotency-Key`)
3. To cancel: call `POST /transfers/cancel` with `transferIds` array (include `Idempotency-Key`)
4. Both endpoints return 200 on success with no body -- confirm by fetching individual transfer details if needed


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
