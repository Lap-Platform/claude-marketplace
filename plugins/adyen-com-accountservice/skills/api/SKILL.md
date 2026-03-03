---
name: account-api
description: "Account API skill. Use when working with Account for checkAccountHolder, closeAccount, closeAccountHolder. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# Account API
API version: 6

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://cal-test.adyen.com/cal/services/Account/v6

## Setup
1. Set Authorization header with your Bearer token
3. POST /checkAccountHolder -- create first checkAccountHolder

## Endpoints

20 endpoints across 20 groups. See references/api-spec.lap for full details.

### checkAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /checkAccountHolder | Trigger verification |

### closeAccount
| Method | Path | Description |
|--------|------|-------------|
| POST | /closeAccount | Close an account |

### closeAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /closeAccountHolder | Close an account holder |

### closeStores
| Method | Path | Description |
|--------|------|-------------|
| POST | /closeStores | Close stores |

### createAccount
| Method | Path | Description |
|--------|------|-------------|
| POST | /createAccount | Create an account |

### createAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /createAccountHolder | Create an account holder |

### deleteBankAccounts
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteBankAccounts | Delete bank accounts |

### deleteLegalArrangements
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteLegalArrangements | Delete legal arrangements |

### deletePayoutMethods
| Method | Path | Description |
|--------|------|-------------|
| POST | /deletePayoutMethods | Delete payout methods |

### deleteShareholders
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteShareholders | Delete shareholders |

### deleteSignatories
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteSignatories | Delete signatories |

### getAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /getAccountHolder | Get an account holder |

### getTaxForm
| Method | Path | Description |
|--------|------|-------------|
| POST | /getTaxForm | Get a tax form |

### getUploadedDocuments
| Method | Path | Description |
|--------|------|-------------|
| POST | /getUploadedDocuments | Get documents |

### suspendAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /suspendAccountHolder | Suspend an account holder |

### unSuspendAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /unSuspendAccountHolder | Unsuspend an account holder |

### updateAccount
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateAccount | Update an account |

### updateAccountHolder
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateAccountHolder | Update an account holder |

### updateAccountHolderState
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateAccountHolderState | Update payout or processing state |

### uploadDocument
| Method | Path | Description |
|--------|------|-------------|
| POST | /uploadDocument | Upload a document |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new account holder for a business?" -> POST /createAccountHolder
- "How do I add a sub-account under an existing account holder?" -> POST /createAccount
- "What are the details and status of my account holder?" -> POST /getAccountHolder
- "How do I check if an account holder is eligible for payouts at a given tier?" -> POST /checkAccountHolder
- "How do I update the bank account or address on an account holder?" -> POST /updateAccountHolder
- "How do I change the payout schedule or speed for an account?" -> POST /updateAccount
- "How do I suspend a merchant that violated terms?" -> POST /suspendAccountHolder
- "How do I reactivate a previously suspended account holder?" -> POST /unSuspendAccountHolder
- "How do I close a sub-account without closing the whole account holder?" -> POST /closeAccount
- "How do I remove a bank account from an account holder?" -> POST /deleteBankAccounts
- "How do I upload a verification document like an ID or proof of address?" -> POST /uploadDocument
- "What documents have already been uploaded for an account holder?" -> POST /getUploadedDocuments
- "How do I download a tax form (e.g., 1099) for an account holder?" -> POST /getTaxForm
- "How do I enable or disable payout/processing capabilities for an account holder?" -> POST /updateAccountHolderState
- "How do I close specific stores associated with an account holder?" -> POST /closeStores

## Response Tips

- **All endpoints**: Every response includes `pspReference` (use for support inquiries) and `resultCode` (check for "Success"); an `invalidFields` array is always present -- if non-empty, iterate it to find exactly which fields failed validation.
- **Account holder responses** (`createAccountHolder`, `getAccountHolder`, `updateAccountHolder`, `uploadDocument`): Contain deeply nested `accountHolderStatus` with separate `payoutState` and `processingState` objects -- check `disabled` and `disableReason` in each to understand current capabilities.
- **Verification responses**: The `verification` object nests checks under `accountHolder.checks`, `shareholders`, `signatories`, and `legalArrangements` -- each is an array of check result maps that must be iterated individually.
- **202 vs 200**: Many endpoints return either 200 (processed synchronously) or 202 (accepted, processing asynchronously) with identical schemas -- always handle both; a 202 means you should poll via `getAccountHolder` for final state.
- **Tax forms**: The `content` field is base64-encoded (`str(byte)`) and `contentType` indicates the MIME type -- decode before saving to file.
- **Error responses (400, 422)**: Typically include `invalidFields` with field paths and failure reasons -- parse these to build actionable user-facing error messages.

## Anomaly Flags

- **`invalidFields` non-empty on 200/202**: The call "succeeded" but some fields were rejected -- surface these immediately as they indicate partial updates or data that was silently ignored.
- **`accountHolderStatus.status` changed unexpectedly**: After any mutation, compare the returned status against the previous known state; flag if it shifted to `Suspended` or `Closed` without an explicit suspend/close call.
- **`payoutState.disabled: true` or `processingState.disabled: true`**: Proactively warn the user -- payouts or processing are blocked, and `disableReason`/`notAllowedReason` explains why.
- **`verification.accountHolder.checks` contains failed checks**: After document upload or account holder creation, surface any verification failures so the user can remediate immediately.
- **422 Unprocessable Entity**: Often means a business rule violation (e.g., closing an account with pending balance) -- surface the full error body, not just the status code.
- **`migrationData.migrated: true`** in `getAccountHolder`: This account holder has been migrated to the Balance Platform -- flag this as most Account API operations may behave differently or be deprecated for migrated entities.
- **`tierNumber` changes**: If `payoutState.tierNumber` or `processingState.tierNumber` drops after an update, alert the user that their processing/payout limits may have decreased.

## Playbook

### Onboard a New Business Merchant

1. Call `POST /createAccountHolder` with `legalEntity: "Business"`, the `accountHolderCode`, business details (legal name, registration number, address), and `createDefaultAccount: true`.
2. Check the response `verification.accountHolder.checks` for any required KYC documents.
3. Call `POST /uploadDocument` for each required document (e.g., registration extract, ID of shareholder) with the correct `documentType`.
4. Call `POST /getAccountHolder` with `showDetails: true` to confirm verification status has progressed.
5. If `payoutState.disabled` is `true`, review `disableReason` and submit additional documents or data as needed.

### Change Payout Schedule and Bank Account

1. Call `POST /getAccountHolder` to retrieve current `bankAccountDetails` and identify the `bankAccountUUID` to use.
2. If needed, call `POST /updateAccountHolder` to add a new bank account via `accountHolderDetails.bankAccountDetails`.
3. Call `POST /updateAccount` with the `accountCode`, the desired `bankAccountUUID`, and the new `payoutSchedule` (e.g., `{ "schedule": "DAILY_EU", "action": "UPSERT" }`).
4. Verify the response `payoutSchedule.nextScheduledPayout` reflects the expected next payout date.

### Suspend and Reinstate an Account Holder

1. Call `POST /suspendAccountHolder` with the `accountHolderCode`.
2. Confirm the response shows `accountHolderStatus.status` is now `Suspended` and both `payoutState.disabled` and `processingState.disabled` are `true`.
3. Investigate and resolve the issue (e.g., upload missing compliance documents via `POST /uploadDocument`).
4. Call `POST /unSuspendAccountHolder` with the same `accountHolderCode`.
5. Verify `accountHolderStatus.status` returns to `Active` and `disabled` flags are `false`.

### Remove Outdated Shareholders and Bank Accounts

1. Call `POST /getAccountHolder` with `showDetails: true` to list all current shareholders and bank accounts.
2. Identify the `shareholderCodes` and `bankAccountUUIDs` to remove.
3. Call `POST /deleteShareholders` and `POST /deleteBankAccounts` in parallel with the respective codes/UUIDs.
4. Check both responses for empty `invalidFields` and `resultCode: "Success"`.
5. Call `POST /getAccountHolder` again to confirm the entities have been removed.

### Close Down a Merchant Completely

1. Call `POST /getAccountHolder` to list all sub-accounts under the account holder.
2. For each sub-account, call `POST /closeAccount` with its `accountCode` and verify `status` is `Closed`.
3. If the account holder has stores, call `POST /closeStores` with all store codes.
4. Call `POST /closeAccountHolder` with the `accountHolderCode`.
5. Confirm the response `accountHolderStatus.status` is `Closed` -- note this action is irreversible.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
