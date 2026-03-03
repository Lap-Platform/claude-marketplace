---
name: fire-financial-services-business-api
description: "Fire Financial Services Business API skill. Use when working with Fire Financial Services Business for apps, accounts, activities. Covers 63 endpoints."
version: 1.0.0
generator: lapsh
---

# Fire Financial Services Business API
API version: 1.0

## Auth
Bearer bearer

## Base URL
https://api.fire.com/business

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/accounts -- verify access
3. POST /v1/apps/accesstokens -- create first accesstokens

## Endpoints

63 endpoints across 17 groups. See references/api-spec.lap for full details.

### apps
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/apps/accesstokens | Authenticate with the API. |
| GET | /v1/apps | List all API applications |
| POST | /v1/apps | Create an API Application |
| GET | /v1/apps/{applicationId}/permissions | List all permissions for an API application |
| GET | /v1/apps/permissions | List all permissions for API applications |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/accounts | List accounts |
| POST | /v1/accounts | Create a new Fire Account. |
| GET | /v2/accounts | List accounts (V2) |
| GET | /v2/accounts/{ican} | Get details of an account (V2) |
| PUT | /v2/accounts/{ican} | Update account configuration |
| PUT | /v2/accounts/{ican}/internationaldetails | Request international account details |
| GET | /v1/accounts/{ican} | Get details of an account |
| GET | /v3/accounts/{ican}/transactions | List transactions for an account |

### activities
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/activities | Get activity |

### cards
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/cards | List debit cards |
| POST | /v1/cards | Create a new Fire debit card |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/me/cards/{cardId}/transactions | Get a list of debit card transactions |
| POST | /v1/me/cards/{cardId}/block | Block a Fire debit card |
| POST | /v1/me/cards/{cardId}/unblock | Unblock a Fire debit card |

### paymentrequests
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/paymentrequests | Create a payment request |
| GET | /v1/paymentrequests/{paymentRequestCode} | Get payment request details |
| GET | /v2/paymentrequests/{paymentRequestCode}/payments | Get list of all payment attempts related to a payment request |
| GET | /v2/paymentrequests/{paymentRequestCode}/reports | Get a report from a payment request |
| GET | /v2/paymentrequests/sent | Get a list of payment request transactions |
| GET | /v2/paymentrequests/{paymentRequestCode}/public | List details of a public payment request |
| PUT | /v2/paymentrequests/{paymentRequestCode}/status | Update the status of a payment request |

### fx
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/fx/rate | Get FX rates |

### limits
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/limits | List all limits |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/webhooks/{webhookId}/events/{event}/test | Send test webhooks |
| GET | /v2/webhooks | List all webhooks |

### batches
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/batches/{batchUuid}/newpayees | List new payees in a batch |
| POST | /v1/batches | Create a new batch |
| GET | /v1/batches | List all batches |
| POST | /v1/batches/{batchUuid}/internaltransfers | Add an internal transfer to a Batch |
| GET | /v1/batches/{batchUuid}/internaltransfers | List items for an internal transfer batch |
| POST | /v1/batches/{batchUuid}/banktransfers | Add a bank transfer to a batch. |
| GET | /v1/batches/{batchUuid}/banktransfers | List items for a bank transfer batch |
| POST | /v2/batches/{batchUuid}/internationaltransfers | Add an international transfer to a Batch |
| GET | /v2/batches/{batchUuid}/internationaltransfers | List items for an international transfer batch |
| DELETE | /v1/batches/{batchUuid}/internaltransfers/{itemUuid} | Remove an internal transfer from a batch |
| DELETE | /v1/batches/{batchUuid}/banktransfers/{itemUuid} | Remove a bank transfer from a batch. |
| DELETE | /v2/batches/{batchUuid}/internationaltransfers/{itemUuid} | Remove an international transfer from a batch |
| DELETE | /v1/batches/{batchUuid} | Cancel a batch |
| GET | /v1/batches/{batchUuid} | Get the details of a batch |
| PUT | /v1/batches/{batchUuid} | Submit a batch |
| GET | /v1/batches/{batchUuid}/approvals | List approvals for a batch. |

### payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/payments/{paymentUuid} | Get payment details |

### aspsps
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/aspsps | Get list of ASPSPs / Banks |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/users | List all users |
| GET | /v1/users/{userId} | Get the details of a user |
| GET | /v2/users/{userId}/address | Get the address of a user |

### payees
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/payees | List payees |
| GET | /v1/payees/{payeeId} | Get details of a payee |
| GET | /v1/payees/{payeeId}/transactions | List transaction for a payee account |

### directdebits
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/directdebits | List all direct debits |
| GET | /v1/directdebits/{directDebitUuid} | Get the details of a direct debit |
| POST | /v1/directdebits/{directDebitUuid}/reject | Reject a direct debit |

### mandates
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/mandates | List all direct debit mandates |
| GET | /v1/mandates/{mandateUuid} | Get the details of a direct debit mandate |
| PUT | /v1/mandates/{mandateUuid} | Update direct debit mandate alias |
| POST | /v1/mandates/{mandateUuid}/cancel | Cancel a direct debit mandate |
| POST | /v1/mandates/{mandateUuid}/activate | Activate a direct debit mandate |

### services
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/services | Get service Fees and info |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the Fire API?" -> POST /v1/apps/accesstokens
- "What accounts do I have?" -> GET /v1/accounts
- "What is the balance of account 12345?" -> GET /v2/accounts/{ican}
- "Show me recent transactions for an account" -> GET /v3/accounts/{ican}/transactions
- "How do I create a payment request?" -> POST /v1/paymentrequests
- "What is the status of payment request ABC123?" -> GET /v1/paymentrequests/{paymentRequestCode}
- "What is the current EUR/GBP exchange rate?" -> GET /v2/fx/rate
- "List all my payees" -> GET /v1/payees
- "How do I send a batch of bank transfers?" -> POST /v1/batches then POST /v1/batches/{batchUuid}/banktransfers
- "Block a lost card immediately" -> POST /v1/me/cards/{cardId}/block
- "What direct debits are active on a mandate?" -> GET /v1/directdebits
- "Cancel a direct debit mandate" -> POST /v1/mandates/{mandateUuid}/cancel
- "What banks are available for open banking payments?" -> GET /v1/aspsps
- "Who are the users on my business account?" -> GET /v1/users
- "What are my current spending limits?" -> GET /v2/limits

## Response Tips

- **Accounts/Payees/Batches**: List endpoints return `{total, items/accounts/fundingSources}` -- always check `total` for pagination; use `offset`+`limit` params where available.
- **Transactions**: `/v3/accounts/{ican}/transactions` uses cursor-based pagination via `startAfter` and returns `{links, content}` -- follow `links` for next page rather than computing offsets.
- **Payment Requests**: Responses include detailed analytics counters (`countTimesViewed*`, `countTimesConsented`, `totalAmountPaid`) -- these track the full payment funnel.
- **Payments**: Payment objects nest `currency`, `to.account.account`, and `bank` as deep maps -- destructure carefully, especially `to` which is triple-nested.
- **Batches**: Batch detail returns separate succeeded/failed/submitted counts and values -- compare `numberOfItemsSubmitted` vs `numberOfItemsSucceeded` + `numberOfItemsFailed` to detect in-progress items.
- **204 responses**: PUT/POST actions (rename account, block card, cancel mandate, reject direct debit) return empty 204 -- success means no body, do not attempt to parse.
- **Errors**: All endpoints share the same error set (400/401/403) -- 401 means expired token (re-authenticate via `/v1/apps/accesstokens`), 403 means insufficient permissions.

## Anomaly Flags

- **Token expiry approaching**: The access token response includes an `expiry` datetime -- surface a warning when it is within 5 minutes of expiring and prompt re-authentication.
- **Batch partial failures**: When `numberOfItemsFailed > 0` on a batch, proactively alert the user with the failure count and value rather than silently reporting success.
- **Payment request underpayment**: If `totalAmountPaid < amount` on a payment request that has `countTimesPaid > 0`, flag that partial payment was received.
- **Direct debit rejection codes**: When `schemeRejectReason` or `schemeRejectReasonCode` is populated on a direct debit, surface the reason immediately -- these indicate bank-level failures.
- **Mandate cancellation by scheme**: If a mandate has `schemeCancelReason` populated but was not user-cancelled, alert that the mandate was terminated externally.
- **FX rate staleness**: The `/v2/fx/rate` response has no timestamp -- warn the user that rates are indicative and may change between quote and execution.
- **Account status changes**: If an account's `status` is anything other than active, flag it when listing accounts so the user does not attempt operations on a frozen or closed account.
- **403 on write operations**: May indicate the API app lacks required permissions -- suggest checking `/v1/apps/{applicationId}/permissions` to diagnose.

## Playbook

### 1. Authenticate and List Accounts

1. Call `POST /v1/apps/accesstokens` with your `clientId`, `clientSecret`, and `refreshToken` (grant type `AccessToken`).
2. Store the returned `accessToken` and note the `expiry` timestamp.
3. Set the `Authorization: Bearer {accessToken}` header for all subsequent requests.
4. Call `GET /v2/accounts` to retrieve all accounts with full details.
5. For any specific account, call `GET /v2/accounts/{ican}` to get balance, IBAN, and account details.

### 2. Create and Track a Payment Request

1. Call `POST /v1/paymentrequests` with `currency`, `type`, `icanTo`, `amount`, `myRef`, and `description`.
2. Store the returned `code` -- this is the payment request identifier.
3. Share the payment link with the payer or redirect them using `returnUrl`.
4. Poll `GET /v1/paymentrequests/{code}` to monitor `status`, `countTimesPaid`, and `totalAmountPaid`.
5. Once fully paid, call `GET /v2/paymentrequests/{code}/payments` for detailed payment records.
6. Optionally close the request with `PUT /v2/paymentrequests/{code}/status` setting status to closed.

### 3. Execute a Batch Payment Run

1. Call `POST /v1/batches` with `type` (e.g., `BANK_TRANSFER`), `currency`, and `batchName`.
2. Store the returned `batchUuid`.
3. Add items: call `POST /v1/batches/{batchUuid}/banktransfers` (or `internaltransfers`/`internationaltransfers`) for each payment.
4. Review the batch with `GET /v1/batches/{batchUuid}` -- verify `numberOfItemsSubmitted` matches expectations.
5. Submit the batch for approval with `PUT /v1/batches/{batchUuid}`.
6. Check approval status via `GET /v1/batches/{batchUuid}/approvals`.
7. Monitor completion: poll `GET /v1/batches/{batchUuid}` until `numberOfItemsSucceeded + numberOfItemsFailed == numberOfItemsSubmitted`.

### 4. Manage Direct Debit Mandates

1. Call `GET /v1/mandates` to list all mandates and their statuses.
2. For a specific mandate, call `GET /v1/mandates/{mandateUuid}` to see collection history and amounts.
3. To rename a mandate for internal tracking, call `PUT /v1/mandates/{mandateUuid}` with a new `alias`.
4. To activate a pending mandate, call `POST /v1/mandates/{mandateUuid}/activate`.
5. To view collections under a mandate, call `GET /v1/directdebits` with `mandateUuid`.
6. To reject a specific collection, call `POST /v1/directdebits/{directDebitUuid}/reject`.
7. To cancel the mandate entirely, call `POST /v1/mandates/{mandateUuid}/cancel`.

### 5. Issue and Manage Cards

1. Call `GET /v1/users` to find the `userId` for the cardholder.
2. Call `POST /v1/cards` with `userId`, `cardPin`, linked `eurIcan`/`gbpIcan`, and `addressType`.
3. Store the returned `cardId` and `maskedPan`.
4. View card transactions with `GET /v1/me/cards/{cardId}/transactions` (supports `limit`/`offset` pagination).
5. If a card is lost or compromised, immediately call `POST /v1/me/cards/{cardId}/block`.
6. Once resolved, reactivate with `POST /v1/me/cards/{cardId}/unblock`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
