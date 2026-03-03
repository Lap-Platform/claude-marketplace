---
name: sync-for-expenses-api
description: "Sync for Expenses API skill. Use when working with Sync for Expenses for companies. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# Sync for Expenses API
API version: prealpha

## Auth
ApiKey Authorization in header

## Base URL
https://api.codat.io

## Setup
1. Set your API key in the appropriate header
2. GET /companies/{companyId}/sync/expenses/config -- verify access
3. POST /companies/{companyId}/sync/expenses/config -- create first config

## Endpoints

14 endpoints across 1 groups. See references/api-spec.lap for full details.

### companies
| Method | Path | Description |
|--------|------|-------------|
| GET | /companies/{companyId}/sync/expenses/config | Get company configuration |
| POST | /companies/{companyId}/sync/expenses/config | Set company configuration |
| POST | /companies/{companyId}/sync/expenses/connections/partnerExpense | Create Partner Expense connection |
| GET | /companies/{companyId}/sync/expenses/mappingOptions | Mapping options |
| POST | /companies/{companyId}/sync/expenses/syncs | Initiate sync |
| GET | /companies/{companyId}/sync/expenses/syncs/lastSuccessful/status | Last successful sync |
| GET | /companies/{companyId}/sync/expenses/syncs/latest/status | Latest sync status |
| GET | /companies/{companyId}/sync/expenses/syncs/list/status | List sync statuses |
| GET | /companies/{companyId}/sync/expenses/syncs/{syncId}/status | Get Sync status |
| GET | /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions | Get Sync transactions |
| GET | /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions/{transactionId} | Get Sync Transaction |
| POST | /companies/{companyId}/sync/expenses/data/expense-transactions | Create expense-transactions |
| PUT | /companies/{companyId}/sync/expenses/expense-transactions/{transactionId} | Update expense-transactions |
| POST | /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions/{transactionId}/attachments | Upload attachment |

## Enhanced Skill Content
## Question Mapping

- "How do I configure expense sync for a company?" -> GET /companies/{companyId}/sync/expenses/config
- "How do I update the bank account, supplier, or customer mapping for expense sync?" -> POST /companies/{companyId}/sync/expenses/config
- "How do I connect a partner expense source to a company?" -> POST /companies/{companyId}/sync/expenses/connections/partnerExpense
- "What accounts, tax rates, and tracking categories can I map expenses to?" -> GET /companies/{companyId}/sync/expenses/mappingOptions
- "How do I trigger an expense sync?" -> POST /companies/{companyId}/sync/expenses/syncs
- "What was the last successful sync status?" -> GET /companies/{companyId}/sync/expenses/syncs/lastSuccessful/status
- "Is the most recent sync still running or did it fail?" -> GET /companies/{companyId}/sync/expenses/syncs/latest/status
- "How do I check the status of a specific sync?" -> GET /companies/{companyId}/sync/expenses/syncs/{syncId}/status
- "Can I see the history of all syncs for a company?" -> GET /companies/{companyId}/sync/expenses/syncs/list/status
- "How do I view transactions pushed in a particular sync?" -> GET /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions
- "How do I get details for a single synced transaction?" -> GET /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions/{transactionId}
- "How do I push new expense transactions to the platform?" -> POST /companies/{companyId}/sync/expenses/data/expense-transactions
- "How do I update an existing expense transaction?" -> PUT /companies/{companyId}/sync/expenses/expense-transactions/{transactionId}
- "How do I attach a receipt or file to a synced transaction?" -> POST /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions/{transactionId}/attachments

## Response Tips

- **Config endpoints (GET/POST config):** Response mirrors the request shape -- `bankAccount`, `supplier`, and `customer` each contain an `id` field inside a map; a null or missing sub-object means that mapping is not yet configured.
- **Connection endpoint (POST partnerExpense):** Returns the full data connection object; check `status` for connection health and `dataConnectionErrors` array for issues -- an empty array means clean.
- **Mapping options (GET mappingOptions):** All fields are nullable; a null `accounts` or `taxRates` array means the integration does not support that mapping dimension.
- **Sync trigger (POST syncs):** Returns 202 (accepted, not complete) with a `syncId` -- you must poll the status endpoint to track completion.
- **Status endpoints (GET status variants):** `syncStatusCode` is an integer enum and `syncStatus` is its human-readable label; `dataPushed` indicates whether any data actually reached the target platform; `errorMessage` and `syncExceptionMessage` are null on success.
- **Transactions list (GET transactions):** Paginated with `page` (default 1) and `pageSize` (default 100) query params; always check if there are more pages.
- **Expense push (POST expense-transactions):** Returns a `datasetId` (not a `syncId`) -- use this to track the batch; each item in `items` requires `id`, `type`, `issueDate`, and `currency` plus at least one line with `netAmount`, `taxAmount`, and `accountRef`.
- **Update transaction (PUT):** Returns 202 with a `syncId`; the `type` field is a closed enum (Payment, Refund, Reward, Chargeback, TransferIn, TransferOut, AdjustmentIn, AdjustmentOut).
- **Attachments (POST attachments):** Returns the attachment metadata including generated `id`; the file content is sent as the request body (not JSON).

## Anomaly Flags

- **429 Too Many Requests:** Every endpoint can return 429 -- surface rate limit hits immediately and suggest backing off before retrying.
- **Sync stuck or failed:** If `GET .../latest/status` returns a `syncStatus` other than success and `errorMessage` is non-null, flag the error message and exception to the user proactively.
- **Data not pushed:** When `dataPushed: false` on a completed sync, warn that the sync finished but no data reached the target platform -- likely a mapping or configuration issue.
- **422 Unprocessable Entity:** Returned by sync trigger and transaction update -- indicates a validation failure on the platform side (not a client format error like 400); surface the response body as it contains platform-specific rejection reasons.
- **Connection errors array:** After creating a partner expense connection, check `dataConnectionErrors` -- a non-empty array means the connection has issues that will block syncs.
- **Null mapping options:** If `GET mappingOptions` returns null for `accounts` or `taxRates`, flag that the connected platform may not support full expense categorization.
- **Pre-alpha version:** This API is marked `prealpha` -- endpoints, schemas, and behavior may change without notice.

## Playbook

### 1. Initial Setup: Configure and Connect Expense Sync

1. Call `GET /companies/{companyId}/sync/expenses/mappingOptions` to discover available accounts, tax rates, and tracking categories.
2. Call `POST /companies/{companyId}/sync/expenses/connections/partnerExpense` to establish the data connection; verify `status` is healthy and `dataConnectionErrors` is empty.
3. Build a config object using IDs from the mapping options and call `POST /companies/{companyId}/sync/expenses/config` to set the bank account, supplier, and customer mappings.
4. Confirm with `GET /companies/{companyId}/sync/expenses/config` that the configuration persisted correctly.

### 2. Push Expenses and Trigger a Sync

1. Call `POST /companies/{companyId}/sync/expenses/data/expense-transactions` with the batch of expense items (each needs `id`, `type`, `issueDate`, `currency`, and at least one line with `netAmount`, `taxAmount`, and `accountRef`). Capture the returned `datasetId`.
2. Call `POST /companies/{companyId}/sync/expenses/syncs` with `datasetIds` containing the `datasetId` from step 1. Capture the returned `syncId`.
3. Poll `GET /companies/{companyId}/sync/expenses/syncs/{syncId}/status` until `syncStatus` indicates completion or failure.
4. If successful, optionally call `GET /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions` to verify individual transaction outcomes.

### 3. Monitor and Troubleshoot Syncs

1. Call `GET /companies/{companyId}/sync/expenses/syncs/latest/status` to check the most recent sync.
2. If `syncStatus` indicates failure, read `errorMessage` and `syncExceptionMessage` for details.
3. Compare against `GET /companies/{companyId}/sync/expenses/syncs/lastSuccessful/status` to see when things last worked.
4. Call `GET /companies/{companyId}/sync/expenses/syncs/list/status` to review the full sync history and identify whether failures are recurring.
5. For a specific failing sync, drill into `GET /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions` and inspect individual transaction statuses to isolate the problem records.

### 4. Update a Transaction and Attach a Receipt

1. Call `PUT /companies/{companyId}/sync/expenses/expense-transactions/{transactionId}` with corrected fields (must include `type` and `issueDate` at minimum). Capture the returned `syncId`.
2. Poll `GET /companies/{companyId}/sync/expenses/syncs/{syncId}/status` until the update sync completes.
3. Call `POST /companies/{companyId}/sync/expenses/syncs/{syncId}/transactions/{transactionId}/attachments` with the receipt file as the request body.
4. Verify the attachment response contains the expected `transactionId` and a generated `id`.

### 5. Verify Configuration After Changes

1. Call `GET /companies/{companyId}/sync/expenses/config` to retrieve the current bank account, supplier, and customer mappings.
2. Call `GET /companies/{companyId}/sync/expenses/mappingOptions` to confirm the available mapping targets have not changed.
3. If mappings look stale or incomplete, call `POST /companies/{companyId}/sync/expenses/config` with updated values and re-verify.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
