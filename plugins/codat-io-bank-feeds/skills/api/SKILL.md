---
name: bank-feeds
description: "Bank Feeds API skill. Use when working with Bank Feeds for companies. Covers 32 endpoints."
version: 1.0.0
generator: lapsh
---

# Bank Feeds
API version: 3.0.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.codat.io

## Setup
1. Set your API key in the appropriate header
2. GET /companies -- verify access
3. POST /companies -- create first companies

## Endpoints

32 endpoints across 1 groups. See references/api-spec.lap for full details.

### companies
| Method | Path | Description |
|--------|------|-------------|
| POST | /companies | Create company |
| GET | /companies | List companies |
| GET | /companies/{companyId} | Get company |
| DELETE | /companies/{companyId} | Delete a company |
| PUT | /companies/{companyId} | Replace company |
| PATCH | /companies/{companyId} | Update company |
| GET | /companies/{companyId}/accessToken | Get company access token |
| GET | /companies/{companyId}/connections | List connections |
| POST | /companies/{companyId}/connections | Create connection |
| GET | /companies/{companyId}/connections/{connectionId} | Get connection |
| DELETE | /companies/{companyId}/connections/{connectionId} | Delete connection |
| PATCH | /companies/{companyId}/connections/{connectionId} | Unlink connection |
| GET | /companies/{companyId}/connections/{connectionId}/data/bankAccounts | List bank accounts |
| GET | /companies/{companyId}/connections/{connectionId}/options/bankAccounts | Get create/update bank account model |
| POST | /companies/{companyId}/connections/{connectionId}/push/bankAccounts | Create bank account |
| POST | /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts/batch | Create source accounts |
| POST | /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts | Create single source account |
| GET | /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts | List source accounts |
| PATCH | /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts/{accountId} | Update source account |
| DELETE | /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts/{accountId} | Delete source account |
| POST | /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts/credentials | Generate source account credentials |
| DELETE | /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts/credentials | Delete all source account credentials |
| GET | /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/mapping | List bank feed accounts |
| POST | /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/mapping | Create bank feed account mapping |
| GET | /companies/{companyId}/connections/{connectionId}/bankFeeds/info | Get company information |
| POST | /companies/{companyId}/connections/{connectionId}/push/bankAccounts/{accountId}/bankTransactions | Create bank transactions |
| GET | /companies/{companyId}/connections/{connectionId}/options/bankAccounts/{accountId}/bankTransactions | Get create bank transactions model |
| GET | /companies/{companyId}/push/{pushOperationKey} | Get create operation |
| GET | /companies/{companyId}/push | List create operations |
| GET | /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/{sourceAccountId}/managedBankFeeds/syncs/{syncId} | Get sync |
| GET | /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/{sourceAccountId}/managedBankFeeds/syncs/latest | Get latest sync |
| POST | /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/{sourceAccountId}/managedBankFeeds/syncs | Run ad-hoc sync |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new company?" -> POST /companies
- "List all my companies" -> GET /companies
- "Get details for a specific company" -> GET /companies/{companyId}
- "How do I delete a company?" -> DELETE /companies/{companyId}
- "How do I connect a company to a bank feed platform?" -> POST /companies/{companyId}/connections
- "What bank accounts are available for a connection?" -> GET /companies/{companyId}/connections/{connectionId}/data/bankAccounts
- "How do I push bank transactions into the accounting platform?" -> POST /companies/{companyId}/connections/{connectionId}/push/bankAccounts/{accountId}/bankTransactions
- "How do I map a source bank account to a target account?" -> POST /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/mapping
- "What currencies does this company support?" -> GET /companies/{companyId}/connections/{connectionId}/bankFeeds/info
- "How do I check the status of a push operation?" -> GET /companies/{companyId}/push/{pushOperationKey}
- "How do I set up bank feed account credentials?" -> POST /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts/credentials
- "How do I create multiple bank feed accounts at once?" -> POST /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts/batch
- "What fields are required to push bank transactions?" -> GET /companies/{companyId}/connections/{connectionId}/options/bankAccounts/{accountId}/bankTransactions
- "How do I check the latest sync status for a bank feed?" -> GET /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/{sourceAccountId}/managedBankFeeds/syncs/latest
- "How do I disconnect a company's data connection?" -> DELETE /companies/{companyId}/connections/{connectionId}

## Response Tips

- **Companies (list)**: Paginated with `page` and `pageSize` params (default 100). Check total results in response metadata to know if more pages exist.
- **Connections**: Response includes `status` (PendingAuth/Linked/Unlinked/Deauthorized), `dataConnectionErrors` array (nullable), and `linkUrl` for auth flows. Always check status before operating on a connection.
- **Push operations**: Returns async status (Pending/Success/Failed). Poll GET /companies/{companyId}/push/{pushOperationKey} for completion. Check `validation.errors` and `validation.warnings` arrays for field-level issues.
- **Bank feed accounts**: The `status` field uses lowercase values (pending/connected/connecting/disconnected/unknown), distinct from connection-level status casing.
- **Batch bank feed accounts**: May return 201 (all succeeded) or 207 (partial success). On 207, inspect individual item statuses in the response body.
- **Options endpoints**: Return schema metadata (type, required, properties, validation) -- use these to discover valid field values before pushing data.
- **Managed syncs**: Sync responses include `errorMessage` and `errorCode` when status indicates failure. The `pushOperationKeys` array links to individual push operations for detailed tracking.
- **Delete operations**: Return 204 with no body on success. Any other status indicates failure.

## Anomaly Flags

- **429 Too Many Requests**: All endpoints can return 429. Surface rate limit headers and recommend backoff before retrying.
- **402 Payment Required**: Appears across all endpoints. Flag immediately -- indicates a billing or subscription issue that blocks all API usage.
- **409 Conflict**: Returned by batch bank feed account creation and managed sync triggers. Surface when a sync is already in progress or accounts conflict.
- **Connection status drift**: If a connection returns `Deauthorized` or `Unlinked` status, proactively warn that operations on that connection will fail until re-authorized.
- **Push operation timeout**: Push endpoints accept `timeoutInMinutes`. If a push operation remains in Pending status beyond the timeout window, surface the stalled operation.
- **207 Multi-Status on batch**: Always flag partial failures on batch bank feed account creation -- some accounts succeeded while others failed.
- **Sync error codes**: When GET latest sync returns `errorMessage` or `errorCode`, surface these before attempting new syncs on the same account.
- **503 Service Unavailable**: Indicates upstream platform issues. Distinguish from 500 (Codat-side) when advising retry strategy.
- **Empty 204 on latest sync**: The latest sync endpoint can return 204 (no sync exists yet). Flag this to avoid confusion with successful empty responses.

## Playbook

### 1. Onboard a New Company and Connect Bank Feeds

1. Create a company: POST /companies with `name` (and optional `description`, `tags`)
2. Note the returned `companyId`
3. Create a connection: POST /companies/{companyId}/connections with `platformKey` for the target accounting platform
4. Direct the user to the `linkUrl` in the response to complete OAuth/auth
5. Verify connection status: GET /companies/{companyId}/connections/{connectionId} -- confirm `status` is `Linked`
6. Check company bank feed info: GET /companies/{companyId}/connections/{connectionId}/bankFeeds/info to confirm supported currencies

### 2. Set Up Bank Feed Accounts and Map to Target Accounts

1. Create bank feed accounts: POST /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts (single) or .../batch (multiple)
2. List created accounts: GET /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts
3. Get available target accounts: GET /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/mapping
4. Map source to target: POST /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/mapping with `sourceAccountId` and `targetAccountId`
5. Verify mapping status in the response -- check `status` and `error` fields

### 3. Push Bank Transactions and Monitor

1. Check push options: GET /companies/{companyId}/connections/{connectionId}/options/bankAccounts/{accountId}/bankTransactions to discover required fields
2. Push transactions: POST /companies/{companyId}/connections/{connectionId}/push/bankAccounts/{accountId}/bankTransactions with `transactions` array (each needs id, date, description, amount, balance, transactionType)
3. Note the returned `pushOperationKey`
4. Poll status: GET /companies/{companyId}/push/{pushOperationKey} until `status` is no longer Pending
5. Check `validation.errors` and `validation.warnings` for any field-level issues
6. Optionally list all push history: GET /companies/{companyId}/push with pagination

### 4. Trigger and Monitor Managed Bank Feed Syncs

1. Trigger a sync: POST /companies/{companyId}/connections/{connectionId}/bankFeedAccounts/{sourceAccountId}/managedBankFeeds/syncs
2. Note the returned `syncId`
3. Check sync status: GET .../managedBankFeeds/syncs/{syncId} -- look at `status`, `errorMessage`, `errorCode`
4. Alternatively, check latest sync: GET .../managedBankFeeds/syncs/latest (returns 204 if no syncs exist)
5. If sync succeeded, review `pushOperationKeys` array to track individual push results via GET /companies/{companyId}/push/{pushOperationKey}

### 5. Manage Credentials for Bank Feed Accounts

1. Generate credentials: POST /companies/{companyId}/connections/{connectionId}/connectionInfo/bankFeedAccounts/credentials
2. Store the returned `username` and `password` securely -- these are used by the bank feed provider
3. To rotate credentials, delete existing: DELETE .../bankFeedAccounts/credentials
4. Re-generate with a new POST to the credentials endpoint
5. Update any external systems that consume these credentials


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
