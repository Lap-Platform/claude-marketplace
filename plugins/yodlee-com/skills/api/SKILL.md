---
name: yodlee-core-apis
description: "Yodlee Core APIs API skill. Use when working with Yodlee Core APIs for transactions, cobrand, dataExtracts. Covers 70 endpoints."
version: 1.0.0
generator: lapsh
---

# Yodlee Core APIs
API version: 1.1.0

## Auth
Requires API key (key parameter)

## Base URL
/

## Setup
1. Include your API key via the key parameter
2. GET /transactions -- verify access
3. POST /cobrand/login -- create first login

## Endpoints

70 endpoints across 15 groups. See references/api-spec.lap for full details.

### transactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /transactions | Get Transactions |
| PUT | /transactions/categories/rules/{ruleId} | Update Transaction Categorization Rule |
| POST | /transactions/categories/rules/{ruleId} | Run Transaction Categorization Rule |
| DELETE | /transactions/categories/rules/{ruleId} | Delete Transaction Categorization Rule |
| GET | /transactions/count | Get Transactions Count |
| GET | /transactions/categories/txnRules | Get Transaction Categorization Rules |
| DELETE | /transactions/categories/{categoryId} | Delete Category |
| GET | /transactions/categories | Get Transaction Category List |
| PUT | /transactions/categories | Update Category |
| POST | /transactions/categories | Create Category |
| GET | /transactions/categories/rules | Get Transaction Categorization Rules |
| POST | /transactions/categories/rules | Create or Run Transaction Categorization Rule |
| PUT | /transactions/{transactionId} | Update Transaction |

### cobrand
| Method | Path | Description |
|--------|------|-------------|
| POST | /cobrand/login | Cobrand Login |
| PUT | /cobrand/config/notifications/events/{eventName} | Update Subscription |
| POST | /cobrand/config/notifications/events/{eventName} | Subscribe Event |
| DELETE | /cobrand/config/notifications/events/{eventName} | Delete Subscription |
| POST | /cobrand/logout | Cobrand Logout |
| GET | /cobrand/config/notifications/events | Get Subscribed Events |
| GET | /cobrand/publicKey | Get Public Key |

### dataExtracts
| Method | Path | Description |
|--------|------|-------------|
| GET | /dataExtracts/userData | Get userData |
| GET | /dataExtracts/events | Get Events |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers | Get Providers |
| GET | /providers/{providerId} | Get Provider Details |
| GET | /providers/count | Get Providers Count |

### configs
| Method | Path | Description |
|--------|------|-------------|
| GET | /configs/notifications/events | Get Subscribed Notification Events |
| GET | /configs/publicKey | Get Public Key |
| PUT | /configs/notifications/events/{eventName} | Update Notification Subscription |
| POST | /configs/notifications/events/{eventName} | Subscribe For Notification Event |
| DELETE | /configs/notifications/events/{eventName} | Delete Notification Subscription |

### derived
| Method | Path | Description |
|--------|------|-------------|
| GET | /derived/networth | Get Networth Summary |
| GET | /derived/transactionSummary | Get Transaction Summary |
| GET | /derived/holdingSummary | Get Holding Summary |

### user
| Method | Path | Description |
|--------|------|-------------|
| POST | /user/samlLogin | Saml Login |
| GET | /user/accessTokens | Get Access Tokens |
| GET | /user | Get User Details |
| PUT | /user | Update User Details |
| DELETE | /user/unregister | Delete User |
| POST | /user/register | Register User |
| POST | /user/logout | User Logout |

### documents
| Method | Path | Description |
|--------|------|-------------|
| GET | /documents/{documentId} | Download a Document |
| DELETE | /documents/{documentId} | Delete Document |
| GET | /documents | Get Documents |

### providerAccounts
| Method | Path | Description |
|--------|------|-------------|
| PUT | /providerAccounts/{providerAccountId}/preferences | Update Preferences |
| GET | /providerAccounts/{providerAccountId} | Get Provider Account Details |
| DELETE | /providerAccounts/{providerAccountId} | Delete Provider Account |
| GET | /providerAccounts | Get Provider Accounts |
| PUT | /providerAccounts | Update Account |
| GET | /providerAccounts/profile | Get User Profile Details |

### auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /auth/token | Generate Access Token |
| DELETE | /auth/token | Delete Token |
| DELETE | /auth/apiKey/{key} | Delete API Key |
| GET | /auth/apiKey | Get API Keys |
| POST | /auth/apiKey | Generate API Key |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | Get Accounts |
| POST | /accounts | Add Manual Account |
| POST | /accounts/evaluateAddress | Evaluate Address |
| GET | /accounts/{accountId} | Get Account Details |
| PUT | /accounts/{accountId} | Update Account |
| DELETE | /accounts/{accountId} | Delete Account |
| GET | /accounts/historicalBalances | Get Historical Balances |

### holdings
| Method | Path | Description |
|--------|------|-------------|
| GET | /holdings/assetClassificationList | Get Asset Classification List |
| GET | /holdings/securities | Get Security Details |
| GET | /holdings | Get Holdings |
| GET | /holdings/holdingTypeList | Get Holding Type List |

### verifyAccount
| Method | Path | Description |
|--------|------|-------------|
| POST | /verifyAccount/{providerAccountId} | Verify Accounts Using Transactions |

### verification
| Method | Path | Description |
|--------|------|-------------|
| GET | /verification | Get Verification Status |
| PUT | /verification | Verify Challenge Deposit |
| POST | /verification | Initiaite Matching Service and Challenge Deposit |

### statements
| Method | Path | Description |
|--------|------|-------------|
| GET | /statements | Get Statements |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate my cobrand session?" -> POST /cobrand/login
- "What transactions happened in my account last month?" -> GET /transactions
- "How many transactions match a specific category?" -> GET /transactions/count
- "What financial providers are available for linking?" -> GET /providers
- "How do I link a new bank account?" -> PUT /providerAccounts
- "What is my current net worth across all accounts?" -> GET /derived/networth
- "How do I register a new user?" -> POST /user/register
- "How do I categorize a transaction differently?" -> PUT /transactions/{transactionId}
- "What are my investment holdings?" -> GET /holdings
- "How do I verify a newly linked account with micro-deposits?" -> POST /verification
- "What notification webhooks are configured?" -> GET /configs/notifications/events
- "How do I get a summary of spending by category?" -> GET /derived/transactionSummary
- "How do I download a specific document or statement?" -> GET /documents/{documentId}
- "What historical balances does my account have?" -> GET /accounts/historicalBalances
- "How do I delete a linked provider account?" -> DELETE /providerAccounts/{providerAccountId}

## Response Tips

- **Transactions**: Results use `skip`/`top` for pagination; always check `transactions.count` first to size your iteration. Amounts are nested `{amount, currency}` objects.
- **Accounts**: The `include` param controls which nested objects (e.g., profile, holder) appear; omitting it returns a slim payload. Status field values drive account lifecycle.
- **Providers**: Large result sets; use `skip`/`top` and `name` filter to narrow. `providerId` is required for detail calls and linking flows.
- **Holdings**: Securities and holdings are separate endpoints; join on `holdingId`. Classification types come from `/holdings/assetClassificationList`.
- **Derived**: Summary endpoints require `groupBy` and return nested interval arrays. Date ranges are mandatory for meaningful results.
- **Auth/Cobrand**: Login returns session tokens (cobSession, userSession) used as headers in all subsequent calls. 204 responses have no body.
- **Verification**: Response contains verification status and matched transactions. The `verificationType` field determines the flow (matching, challenge-deposit).
- **Errors**: All endpoints return 400 (bad request), 401 (expired or missing session), or 404 (resource not found). Parse the `errorCode` and `errorMessage` fields in the error body.

## Anomaly Flags

- **401 on any call**: Session token has expired. Surface immediately and suggest re-authenticating via `POST /cobrand/login` then `POST /auth/token`.
- **Repeated 400 errors on provider linking**: Provider login form fields may have changed. Recommend refreshing provider details via `GET /providers/{providerId}`.
- **Empty transaction results with valid date range**: Account refresh may still be in progress. Check provider account status via `GET /providerAccounts/{providerAccountId}` and surface the `refreshInfo` status.
- **Net worth returning unexpected values**: Flag if `includeInNetWorth` is inconsistent across accounts; suggest reviewing via `GET /accounts`.
- **Notification event callbacks returning 404**: Webhook URL may be unreachable. Surface when `GET /configs/notifications/events` returns no registered events after a create call returned 201.
- **Data extract queries returning empty for valid date ranges**: User may not have data extracts enabled. Check provider account preferences (`isDataExtractsEnabled`).
- **Verification stuck in pending state**: Flag if `PUT /verification` status has not advanced after expected timeframe; suggest checking with `GET /verification`.

## Playbook

### 1. Initial Setup and Authentication

1. Authenticate the cobrand: `POST /cobrand/login` with cobrandLogin and cobrandPassword
2. Register a new user: `POST /user/register` with loginName and optional profile fields
3. Generate a user session token: `POST /auth/token`
4. Store both `cobSession` and `userSession` tokens for all subsequent API headers

### 2. Link a Financial Institution

1. Search for the provider: `GET /providers?name=BankName`
2. Get provider login form: `GET /providers/{providerId}` to retrieve required credential fields
3. Submit credentials: `PUT /providerAccounts` with the provider's login form fields populated
4. Poll for status: `GET /providerAccounts/{providerAccountId}` until `refreshInfo.status` is `SUCCESS` or `FAILED`
5. Verify the account if needed: `POST /verification` or `POST /verifyAccount/{providerAccountId}`

### 3. Retrieve and Categorize Transactions

1. Get total count: `GET /transactions/count?fromDate=YYYY-MM-DD&toDate=YYYY-MM-DD`
2. Fetch transactions in pages: `GET /transactions?fromDate=...&toDate=...&skip=0&top=100`
3. Review existing categories: `GET /transactions/categories`
4. Create a custom category if needed: `POST /transactions/categories` with parentCategoryId
5. Recategorize a transaction: `PUT /transactions/{transactionId}` with new categoryId
6. Optionally create an auto-categorization rule: `POST /transactions/categories/rules`

### 4. Monitor Net Worth and Holdings

1. Fetch all linked accounts: `GET /accounts`
2. Get current net worth: `GET /derived/networth?interval=M&fromDate=...&toDate=...`
3. Review investment holdings: `GET /holdings?include=assetClassification`
4. Get holding summary by classification: `GET /derived/holdingSummary?classificationType=assetCategory`
5. Check historical account balances: `GET /accounts/historicalBalances?fromDate=...&toDate=...&interval=M`

### 5. Set Up Webhook Notifications

1. Check existing notification subscriptions: `GET /configs/notifications/events`
2. Subscribe to refresh events: `POST /configs/notifications/events/REFRESH` with your callbackUrl
3. Subscribe to data update events: `POST /configs/notifications/events/DATA_UPDATES` with callbackUrl
4. Update a callback URL if it changes: `PUT /configs/notifications/events/{eventName}`
5. Remove a subscription when no longer needed: `DELETE /configs/notifications/events/{eventName}`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
