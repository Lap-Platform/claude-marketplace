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

- "How do I send a payout to a card?" -> POST /payout
- "How do I confirm a third-party payout?" -> POST /confirmThirdParty
- "How do I decline or cancel a pending third-party payout?" -> POST /declineThirdParty
- "How do I store a shopper's bank account or card for future payouts?" -> POST /storeDetail
- "How do I store payment details and submit a third-party payout in one call?" -> POST /storeDetailAndSubmitThirdParty
- "How do I submit a payout using previously stored details?" -> POST /submitThirdParty
- "How do I pay out to a bank account (IBAN) instead of a card?" -> POST /storeDetailAndSubmitThirdParty (provide `bank` with `iban`/`ownerName`)
- "How do I set up recurring payouts for a shopper?" -> POST /storeDetail (with `recurring.contract` set), then POST /submitThirdParty
- "How do I check if a payout was refused?" -> Inspect `resultCode` and `refusalReason` in the response from POST /payout, /storeDetailAndSubmitThirdParty, or /submitThirdParty
- "How do I pay out to a person vs. a company?" -> POST /storeDetail or /storeDetailAndSubmitThirdParty with `entityType` set to `NaturalPerson` or `Company`
- "How do I reference a previous payout to confirm or decline it?" -> POST /confirmThirdParty or /declineThirdParty with `originalReference` set to the `pspReference` from the original submission
- "How do I send a payout with fraud scoring?" -> POST /payout with `fraudOffset` and/or `fundSource` fields populated
- "What shopper details do I need to store payment info?" -> POST /storeDetail requires `dateOfBirth`, `entityType`, `nationality`, `shopperEmail`, `shopperReference`, and `recurring`

## Response Tips

- **confirmThirdParty / declineThirdParty**: Check `response` field for `[confirm-received]` or `[decline-received]`; `pspReference` is the confirmation's own reference, not the original payout's.
- **payout**: `resultCode` indicates outcome (Authorised, Refused, Error); if refused, `refusalReason` explains why. `dccAmount` only appears for cross-currency payouts. `fraudResult.accountScore` is cumulative risk; inspect `results` array for individual rule triggers.
- **storeDetail**: `recurringDetailReference` is the token you need for future /submitThirdParty calls; persist it alongside `shopperReference`.
- **storeDetailAndSubmitThirdParty / submitThirdParty**: `resultCode` of `[payout-submit-received]` means queued, not completed; final status arrives via webhook notification. A non-empty `refusalReason` with a received result still means the submission was accepted for processing.
- **All endpoints**: `additionalData` is a freeform key-value map that varies by payment method and configuration; do not rely on fixed keys without checking your Adyen account setup. HTTP 422 typically indicates validation failure with a descriptive error body.

## Anomaly Flags

- **Refused payouts**: Surface immediately when `resultCode` is `Refused` -- include `refusalReason` and `pspReference` for investigation.
- **HTTP 422 responses**: Validation errors often indicate malformed amounts, missing required nested fields (e.g., `currency` without `value`), or invalid enum values for `entityType`/`shopperInteraction` -- surface the full error body.
- **Missing recurringDetailReference**: If `/storeDetail` returns successfully but `recurringDetailReference` is empty or absent, flag it -- subsequent `/submitThirdParty` calls will fail.
- **Fraud score spikes**: When `fraudResult.accountScore` exceeds your configured threshold or `fraudResult.results` contains triggered rules, surface the score and rule names.
- **Unexpected resultCode values**: Flag any `resultCode` that is not `Authorised`, `[payout-submit-received]`, or `Refused` -- these may indicate integration issues or new Adyen-side states.
- **HTTP 401/403 errors**: Authentication or permission failures -- flag that the API key may be invalid, expired, or lacking payout permissions for the merchant account.
- **Cross-currency payouts**: When `dccAmount` appears in `/payout` responses, surface the currency conversion details so the user can verify the exchange rate.

## Playbook

### 1. Direct Card Payout (Instant)

1. Call `POST /payout` with `amount` (currency + value in minor units), `reference`, `merchantAccount`, and `card` details.
2. Check `resultCode` in the response -- `Authorised` means funds are being sent.
3. If `Refused`, read `refusalReason` and adjust the request (e.g., check card number, amount limits).
4. Store `pspReference` for reconciliation and dispute tracking.

### 2. Third-Party Payout with Stored Details (Two-Step)

1. Call `POST /storeDetail` with shopper info (`dateOfBirth`, `entityType`, `nationality`, `shopperEmail`, `shopperReference`), `recurring` contract, and either `bank` (IBAN details) or `card` details.
2. Save the returned `recurringDetailReference`.
3. Call `POST /submitThirdParty` with `amount`, `reference`, `shopperEmail`, `shopperReference`, `selectedRecurringDetailReference` (from step 2), and the same `recurring` block.
4. Confirm `resultCode` is `[payout-submit-received]` -- the payout is now queued.
5. Await webhook notification for final settlement status.

### 3. Store and Submit in One Call

1. Call `POST /storeDetailAndSubmitThirdParty` with all required fields: `amount`, `reference`, `dateOfBirth`, `entityType`, `nationality`, `shopperEmail`, `shopperReference`, `recurring`, plus `bank` or `card` details.
2. Check `resultCode` for `[payout-submit-received]`.
3. If `refusalReason` is present but result is still received, the payout is queued -- monitor via webhooks.
4. Store `pspReference` for tracking.

### 4. Confirm or Decline a Pending Third-Party Payout

1. After submitting a third-party payout, retrieve the `pspReference` from the submission response.
2. To approve: call `POST /confirmThirdParty` with `originalReference` set to that `pspReference`.
3. To reject: call `POST /declineThirdParty` with `originalReference` set to that `pspReference`.
4. Verify the `response` field contains `[confirm-received]` or `[decline-received]` respectively.

### 5. Recurring Payout Setup and Execution

1. Call `POST /storeDetail` with `recurring.contract` set to `PAYOUT`, shopper identity fields, and payment method details.
2. Save `recurringDetailReference` from the response.
3. For each scheduled payout, call `POST /submitThirdParty` with the stored `selectedRecurringDetailReference`, a unique `reference`, and the payout `amount`.
4. Monitor `resultCode` and `refusalReason` on each submission.
5. If a payout is refused repeatedly, call `POST /storeDetail` again to update payment details and obtain a new `recurringDetailReference`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
