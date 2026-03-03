---
name: adyen-binlookup-api
description: "Adyen BinLookup API skill. Use when working with Adyen BinLookup for get3dsAvailability, getCostEstimate. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Adyen BinLookup API
API version: 54

## Auth
ApiKey X-API-Key in header | Bearer basic

## Base URL
https://pal-test.adyen.com/pal/servlet/BinLookup/v54

## Setup
1. Set Authorization header with your Bearer token
3. POST /get3dsAvailability -- create first get3dsAvailability

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### get3dsAvailability
| Method | Path | Description |
|--------|------|-------------|
| POST | /get3dsAvailability | Check if 3D Secure is available |

### getCostEstimate
| Method | Path | Description |
|--------|------|-------------|
| POST | /getCostEstimate | Get a fees cost estimate |

## Enhanced Skill Content
## Question Mapping

- "Is 3D Secure available for this card?" -> POST /get3dsAvailability
- "Does this card support 3DS2?" -> POST /get3dsAvailability
- "What 3DS version should I use for this BIN?" -> POST /get3dsAvailability
- "Check if a stored card supports 3D Secure" -> POST /get3dsAvailability (using recurringDetailReference + shopperReference)
- "What country issued this card?" -> POST /get3dsAvailability (check binDetails.issuerCountry) or POST /getCostEstimate (check cardBin.issuingCountry)
- "How much will processing this payment cost?" -> POST /getCostEstimate
- "What are the interchange fees for this card?" -> POST /getCostEstimate
- "Is this card commercial or consumer?" -> POST /getCostEstimate (check cardBin.commercial)
- "What funding source does this card use - credit or debit?" -> POST /getCostEstimate (check cardBin.fundingSource)
- "Can this card be used for payouts?" -> POST /getCostEstimate (check cardBin.payoutEligible)
- "Estimate cost for a recurring/subscription payment" -> POST /getCostEstimate (with recurring block and shopperInteraction: ContAuth)
- "What's the cost difference with and without 3DS?" -> POST /getCostEstimate twice (toggle assume3DSecureAuthenticated)
- "Estimate cost for an installment payment" -> POST /getCostEstimate (with assumptions.installments)
- "What payment method does this card number map to?" -> POST /getCostEstimate (check cardBin.paymentMethod)

## Response Tips

- **3DS Availability**: Check both `threeDS1Supported` and `threeDS2supported` (note lowercase 's') to determine which flow to implement; `threeDS2CardRangeDetails` contains per-range protocol data needed for 3DS2 fingerprinting.
- **Cost Estimate**: `costEstimateAmount` returns the fee in minor units (cents), not the transaction amount; `resultCode` indicates whether the estimate is final or approximate.
- **Card BIN details**: `cardBin` fields may be partially populated depending on BIN coverage; `fundsAvailability` and `payoutEligible` can be empty strings rather than null when data is unavailable.
- **Errors**: 422 indicates valid JSON but semantically invalid input (bad card number, unknown merchant account); 401/403 distinguish between missing credentials and insufficient permissions.

## Anomaly Flags

- **3DS2 unsupported**: Surface when `threeDS2supported` is false but `threeDS1Supported` is true -- merchant should prepare a 3DS1 fallback flow.
- **Neither 3DS version supported**: Alert when both `threeDS1Supported` and `threeDS2supported` are false -- card cannot be strongly authenticated, which may block transactions in SCA-regulated regions.
- **Commercial card detected**: Flag when `cardBin.commercial` is true -- surcharging rules and interchange rates differ significantly.
- **Payout ineligible**: Surface when `cardBin.payoutEligible` is not "Y" if the merchant plans to issue refunds-to-card or payouts.
- **Cost estimate missing**: Flag when `costEstimateAmount` is absent or zero -- may indicate the BIN is unrecognized or the MCC is misconfigured.
- **Auth errors (401/403)**: Proactively check if the API key has BinLookup permissions enabled in the Adyen Customer Area.
- **Issuing country mismatch**: Surface when `cardBin.issuingCountry` differs from the shopper's billing country -- potential cross-border fee implications.

## Playbook

### 1. Determine the Right 3DS Flow Before Payment

1. Call `POST /get3dsAvailability` with `merchantAccount` and `cardNumber`.
2. Check `threeDS2supported` -- if true, initiate a 3DS2 authentication flow.
3. If false, check `threeDS1Supported` -- if true, fall back to 3DS1.
4. If neither is supported, proceed without 3DS (or block in SCA-regulated regions).
5. Use `threeDS2CardRangeDetails` to configure the 3DS2 SDK with the correct directory server data.

### 2. Estimate Processing Cost Before Checkout

1. Build the `amount` object with the transaction `currency` (ISO 4217) and `value` (minor units, e.g., 1000 = 10.00 EUR).
2. Call `POST /getCostEstimate` with `amount`, `merchantAccount`, and `cardNumber`.
3. Read `costEstimateAmount.value` to get the estimated fee in minor units.
4. Optionally set `assumptions.assume3DSecureAuthenticated: true` to see how 3DS reduces interchange.
5. Display or log the cost breakdown using `cardBin` metadata (funding source, issuing country, payment method).

### 3. Evaluate a Stored Card for Recurring Payments

1. Call `POST /get3dsAvailability` with `recurringDetailReference`, `shopperReference`, and `merchantAccount` to check 3DS support without re-entering the card number.
2. Call `POST /getCostEstimate` with `selectedRecurringDetailReference`, `shopperInteraction: "ContAuth"`, and a `recurring` block specifying the contract type.
3. Compare the cost estimate against a one-time payment estimate (`shopperInteraction: "Ecommerce"`) to understand recurring fee differences.

### 4. Cross-Border Fee Analysis

1. Call `POST /getCostEstimate` with the card number and your `merchantDetails` (including `countryCode` and `mcc`).
2. Check `cardBin.issuingCountry` against `merchantDetails.countryCode`.
3. If they differ, the transaction is cross-border -- expect higher interchange.
4. Repeat with `assumptions.assumeLevel3Data: true` to see if providing Level 3 data (line-item details) reduces the cost.
5. Log the `costEstimateReference` for reconciliation with actual settlement costs.

### 5. BIN Intelligence Lookup

1. Call `POST /getCostEstimate` with a minimal payload: `amount`, `merchantAccount`, and `cardNumber` (first 6-8 digits suffice).
2. Extract `cardBin` fields: `issuingBank`, `issuingCountry`, `fundingSource` (credit/debit/prepaid), `commercial`, `paymentMethod`.
3. Use `payoutEligible` to determine if the card can receive funds.
4. Use `fundsAvailability` to understand settlement timing characteristics.
5. Cache results by BIN prefix to reduce redundant lookups for cards from the same issuer.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
