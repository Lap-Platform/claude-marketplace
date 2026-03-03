---
name: fund-api
description: "Fund API skill. Use when working with Fund for accountHolderBalance, accountHolderTransactionList, debitAccountHolder. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Fund API
API version: 6

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://cal-test.adyen.com/cal/services/Fund/v6

## Setup
1. Set Authorization header with your Bearer token
3. POST /accountHolderBalance -- create first accountHolderBalance

## Endpoints

8 endpoints across 8 groups. See references/api-spec.lap for full details.

### accountHolderBalance
| Method | Path | Description |
|--------|------|-------------|
| POST | /accountHolderBalance | Get the balances of an account holder |

### accountHolderTransactionList
| Method | Path | Description |
|--------|------|-------------|
| POST | /accountHolderTransactionList | Get a list of transactions |

### debitAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /debitAccountHolder | Send a direct debit request |

### payoutAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /payoutAccountHolder | Pay out from an account to the account holder |

### refundFundsTransfer
| Method | Path | Description |
|--------|------|-------------|
| POST | /refundFundsTransfer | Refund a funds transfer |

### refundNotPaidOutTransfers
| Method | Path | Description |
|--------|------|-------------|
| POST | /refundNotPaidOutTransfers | Refund all transactions of an account since the most recent payout |

### setupBeneficiary
| Method | Path | Description |
|--------|------|-------------|
| POST | /setupBeneficiary | Designate a beneficiary account and transfer the benefactor's current balance |

### transferFunds
| Method | Path | Description |
|--------|------|-------------|
| POST | /transferFunds | Transfer funds between platform accounts |

## Enhanced Skill Content
## Question Mapping

- "What is the balance for an account holder?" -> POST /accountHolderBalance
- "How much money is pending or on hold for this account?" -> POST /accountHolderBalance
- "Show me the transactions for an account holder" -> POST /accountHolderTransactionList
- "List transactions filtered by status for a specific account" -> POST /accountHolderTransactionList
- "How do I debit funds from an account holder's bank account?" -> POST /debitAccountHolder
- "Pay out funds to an account holder's bank account" -> POST /payoutAccountHolder
- "Can I send an instant payout to an account holder?" -> POST /payoutAccountHolder (payoutSpeed=INSTANT)
- "How do I reverse a funds transfer?" -> POST /refundFundsTransfer
- "Refund all transfers that haven't been paid out yet" -> POST /refundNotPaidOutTransfers
- "How do I set up a beneficiary relationship between two accounts?" -> POST /setupBeneficiary
- "Transfer funds between two accounts on the platform" -> POST /transferFunds
- "How do I split a debit across multiple accounts?" -> POST /debitAccountHolder (using splits array)
- "What page of transactions should I request next?" -> POST /accountHolderTransactionList (page parameter in transactionListsPerAccount)
- "How do I track a payout I initiated?" -> POST /payoutAccountHolder (check merchantReference and pspReference in response)

## Response Tips

- **Balances** (`accountHolderBalance`): Check `totalBalance` for aggregate view across sub-fields `balance`, `onHoldBalance`, and `pendingBalance` -- each is an array of currency-amount maps. Per-account breakdown is in `balancePerAccount`.
- **Transactions** (`accountHolderTransactionList`): Results are nested inside `accountTransactionLists`, grouped per account. Use `page` in the request to paginate; there is no cursor or next-page token, so increment page until the list returns empty.
- **Debits and Payouts** (`debitAccountHolder`, `payoutAccountHolder`): Both 200 and 202 share the same schema -- a 202 means the request is accepted but processing asynchronously. Always store the `pspReference` for reconciliation.
- **Refunds** (`refundFundsTransfer`, `refundNotPaidOutTransfers`): The `message` field on refundFundsTransfer provides human-readable status detail; refundNotPaidOutTransfers has no message field.
- **All endpoints**: `invalidFields` is always present in responses -- a non-empty array indicates partial validation issues even on a 200/202. `resultCode` confirms the outcome.

## Anomaly Flags

- **`invalidFields` is non-empty on a 200/202**: The request succeeded but some fields were ignored or flagged -- surface these to the user immediately as they may indicate silent data issues.
- **202 instead of 200**: The operation is queued, not completed. Flag this so the user knows to poll or await a webhook for confirmation.
- **`resultCode` is not "Success"**: Even on a 200, the result code may indicate a business-level rejection. Always check and surface unexpected values.
- **422 Unprocessable Entity**: Indicates the request was syntactically valid but semantically wrong (e.g., insufficient funds, invalid account code). Surface the response body for actionable detail.
- **Amount value of 0 or negative in requests**: The API uses `int64` for amounts -- flag if a user constructs a zero or negative debit/transfer/payout as this is almost certainly an error.
- **Missing `pspReference` in response**: Every successful response should include one. Its absence suggests a malformed or intercepted response.
- **`payoutSpeed` set to INSTANT**: Flag that instant payouts may incur additional fees or have different availability depending on the payment method.

## Playbook

### 1. Check Balance and Pay Out Available Funds

1. Call `POST /accountHolderBalance` with the `accountHolderCode` to retrieve current balances.
2. Inspect `totalBalance.balance` for available funds and `totalBalance.onHoldBalance` for held amounts.
3. Determine the payout amount (available minus on-hold minus any desired reserve).
4. Call `POST /payoutAccountHolder` with `accountCode`, `accountHolderCode`, the calculated `amount`, and optionally `bankAccountUUID` and `payoutSpeed`.
5. Store the returned `pspReference` and `merchantReference` for tracking.

### 2. Transfer Funds Between Platform Accounts

1. Call `POST /setupBeneficiary` with `sourceAccountCode` and `destinationAccountCode` to establish the transfer relationship (one-time setup).
2. Confirm `resultCode` is "Success" and `invalidFields` is empty.
3. Call `POST /transferFunds` with `sourceAccountCode`, `destinationAccountCode`, `amount`, and a unique `transferCode`.
4. Record the `pspReference` for reconciliation.

### 3. Refund a Failed or Disputed Transfer

1. Locate the `pspReference` of the original transfer from your records.
2. Call `POST /refundFundsTransfer` with the `originalReference` set to that `pspReference` and the `amount` to refund.
3. Check the `resultCode` and `message` in the response for confirmation.
4. If the response is 202, monitor asynchronously for completion.

### 4. Audit Account Holder Transactions

1. Call `POST /accountHolderTransactionList` with the `accountHolderCode`.
2. Optionally filter by `transactionStatuses` (e.g., only completed or pending).
3. To paginate, include `transactionListsPerAccount` with the specific `accountCode` and `page` number starting at 1.
4. Increment `page` and repeat until the returned transaction list is empty.
5. Cross-reference totals against `POST /accountHolderBalance` to verify consistency.

### 5. Debit an Account Holder with Split Payments

1. Call `POST /debitAccountHolder` with `accountHolderCode`, `amount`, `bankAccountUUID`, and `merchantAccount`.
2. Populate the `splits` array to distribute the debit across multiple accounts (e.g., platform fee split, marketplace commission).
3. Each split requires a `type` (e.g., "MarketPlace", "Commission") and optionally an `account`, `amount`, and `description`.
4. Verify `resultCode` is "Success" and check `invalidFields` for any rejected split entries.
5. Store `pspReference` and `merchantReferences` for reconciliation across all split destinations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
