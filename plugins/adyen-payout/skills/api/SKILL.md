---
name: adyen-payout-api
description: "Adyen Payout API skill. Use when working with Adyen Payout for confirmThirdParty, declineThirdParty, payout. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Adyen Payout API
API version: 68

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://pal-test.adyen.com/pal/servlet/Payout/v68

## Setup
1. Set Authorization header with your Bearer token
3. POST /confirmThirdParty -- create first confirmThirdParty

## Endpoints

6 endpoints across 6 groups. See references/api-spec.lap for full details.

### confirmThirdParty
| Method | Path | Description |
|--------|------|-------------|
| POST | /confirmThirdParty | Confirm a payout |

### declineThirdParty
| Method | Path | Description |
|--------|------|-------------|
| POST | /declineThirdParty | Cancel a payout |

### payout
| Method | Path | Description |
|--------|------|-------------|
| POST | /payout | Make an instant card payout |

### storeDetail
| Method | Path | Description |
|--------|------|-------------|
| POST | /storeDetail | Store payout details |

### storeDetailAndSubmitThirdParty
| Method | Path | Description |
|--------|------|-------------|
| POST | /storeDetailAndSubmitThirdParty | Store details and submit a payout |

### submitThirdParty
| Method | Path | Description |
|--------|------|-------------|
| POST | /submitThirdParty | Submit a payout |

## Enhanced Skill Content
## Question Mapping

- "How do I send a payout directly to a card?" -> POST /payout
- "How do I approve a third-party payout request?" -> POST /confirmThirdParty
- "How do I reject a pending third-party payout?" -> POST /declineThirdParty
- "How do I save a shopper's bank account for future payouts?" -> POST /storeDetail
- "How do I store payment details and immediately submit a third-party payout?" -> POST /storeDetailAndSubmitThirdParty
- "How do I submit a payout using previously stored payment details?" -> POST /submitThirdParty
- "How do I pay out to a bank account (IBAN) instead of a card?" -> POST /payout (with bank details in fundSource) or POST /storeDetailAndSubmitThirdParty (with bank object)
- "How do I set up recurring payouts for a shopper?" -> POST /storeDetail (store with recurring contract) then POST /submitThirdParty
- "How do I confirm or decline a payout I submitted earlier?" -> POST /confirmThirdParty or POST /declineThirdParty (using originalReference from submit response)
- "How do I issue a payout to a natural person vs a company?" -> POST /storeDetail or POST /storeDetailAndSubmitThirdParty (set entityType to NaturalPerson or Company)
- "How do I include fraud scoring in a payout?" -> POST /payout (include fraudOffset in request)
- "What reference do I use to confirm a previously submitted payout?" -> POST /confirmThirdParty (originalReference = pspReference from the submit call)
- "How do I pay out to a shopper in a specific currency?" -> POST /payout (set amount.currency and amount.value)

## Response Tips

- **confirmThirdParty / declineThirdParty**: Check `response` field for `[payout-confirm-received]` or `[payout-decline-received]`; `pspReference` is the unique transaction ID for reconciliation.
- **payout**: `resultCode` indicates outcome (Authorised, Refused, Error); if Refused, inspect `refusalReason` for details; `fraudResult.accountScore` indicates risk level when present.
- **storeDetail**: `recurringDetailReference` is the token needed for future `submitThirdParty` calls; store it alongside `shopperReference`.
- **storeDetailAndSubmitThirdParty / submitThirdParty**: `resultCode` of `[payout-submit-received]` means queued, not completed; watch for `refusalReason` on failures.
- **All endpoints**: HTTP 422 signals validation errors (check response body for field-level details); 401/403 indicate API key or permission issues.

## Anomaly Flags

- **Unexpected resultCode**: Surface immediately if `resultCode` is anything other than `Authorised` or `[payout-submit-received]` -- especially `Refused` or `Error`.
- **refusalReason present**: Always surface `refusalReason` to the user; common values include `Not enough balance`, `Declined`, and `FRAUD`.
- **fraudResult.accountScore threshold**: Flag when `accountScore` exceeds typical baseline (>50) as the payout may be under review or at risk of claw-back.
- **HTTP 422 on valid-looking requests**: Often indicates a merchant account configuration issue (missing payout permission, wrong entityType, or unsupported currency) -- surface the full error body.
- **Missing recurringDetailReference in storeDetail response**: Indicates the detail was not stored successfully despite a 200; verify `resultCode` before proceeding.
- **Deprecated fields**: Watch for unknown keys in `additionalData` maps -- Adyen uses this for feature flags and deprecation notices; surface any keys prefixed with `deprecated` or `migration`.

## Playbook

### 1. One-time Direct Payout to a Card

1. Call `POST /payout` with `amount` (currency + value in minor units), `reference` (your unique ID), `card` details, and `merchantAccount`.
2. Check `resultCode` in the response -- `Authorised` means success.
3. Store `pspReference` for reconciliation and dispute tracking.
4. If `refusalReason` is present, log it and notify the user with the reason.

### 2. Store Details Then Pay Out Later (Third-Party Flow)

1. Call `POST /storeDetail` with shopper info (`dateOfBirth`, `entityType`, `nationality`, `shopperEmail`, `shopperReference`), `recurring` contract, and either `bank` or `card` details.
2. Save the returned `recurringDetailReference` -- this is the stored payment token.
3. When ready to pay, call `POST /submitThirdParty` with `amount`, `reference`, `selectedRecurringDetailReference` (from step 2), `shopperEmail`, `shopperReference`, and the same `recurring` contract.
4. Note the `pspReference` from the response.
5. Call `POST /confirmThirdParty` with `originalReference` set to the `pspReference` from step 4 to finalize, or `POST /declineThirdParty` to cancel.

### 3. Store and Submit in One Call

1. Call `POST /storeDetailAndSubmitThirdParty` with all required fields: `amount`, `dateOfBirth`, `entityType`, `nationality`, `recurring`, `reference`, `shopperEmail`, `shopperReference`, plus `bank` or `card` details.
2. Verify `resultCode` is `[payout-submit-received]`.
3. Use the returned `pspReference` to call `POST /confirmThirdParty` to approve the payout.

### 4. Declining a Suspicious Payout

1. Identify the payout's `pspReference` from the original submit response or from your records.
2. Call `POST /declineThirdParty` with `originalReference` set to that `pspReference`.
3. Confirm `response` is `[payout-decline-received]`.
4. Log the `pspReference` from the decline response for audit trail.

### 5. Paying Out to a Bank Account via IBAN

1. Call `POST /storeDetail` (or `POST /storeDetailAndSubmitThirdParty`) with the `bank` object populated: set `iban`, `ownerName`, `countryCode`, and optionally `bic`.
2. Set `entityType` to `NaturalPerson` or `Company` as appropriate.
3. Include `billingAddress` with the beneficiary's address (required by many acquiring regions).
4. If using `storeDetail`, follow up with `POST /submitThirdParty` using the returned `recurringDetailReference`.
5. Confirm the payout with `POST /confirmThirdParty`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
