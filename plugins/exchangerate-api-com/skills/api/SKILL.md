---
name: exchangerate-api
description: "ExchangeRate-API API skill. Use when working with ExchangeRate-API for latest. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# ExchangeRate-API
API version: 4

## Auth
No authentication required.

## Base URL
https://api.exchangerate-api.com/v4

## Setup
1. No auth setup needed
2. GET /latest/{base_currency} -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### latest
| Method | Path | Description |
|--------|------|-------------|
| GET | /latest/{base_currency} | Returns latest exchange rates in parameter-supplied base currency. |

## Enhanced Skill Content
## Question Mapping

- "What is the current exchange rate from USD to EUR?" -> GET /latest/{base_currency}
- "How much is 1 GBP worth in JPY right now?" -> GET /latest/{base_currency}
- "Show me all exchange rates based on EUR" -> GET /latest/{base_currency}
- "What currencies are available for conversion?" -> GET /latest/{base_currency}
- "Convert 500 USD to CAD" -> GET /latest/{base_currency}
- "What is the USD to INR rate today?" -> GET /latest/{base_currency}
- "Get the latest forex rates for Swiss Franc" -> GET /latest/{base_currency}
- "Is the EUR stronger than the GBP right now?" -> GET /latest/{base_currency} (fetch both, compare)
- "When were the exchange rates last updated?" -> GET /latest/{base_currency}
- "List all rates relative to the Japanese Yen" -> GET /latest/{base_currency}
- "What is the cross rate between CAD and AUD?" -> GET /latest/{base_currency} (derive from shared base)
- "How many currencies does this API support?" -> GET /latest/{base_currency} (count keys in rates map)

## Response Tips

- **Latest rates**: Response `rates` is a flat map of currency code to numeric rate. Multiply amount by `rates[target]` to convert. The `date` field is YYYY-MM-DD and `time_last_updated` is a Unix timestamp -- use the timestamp for precision, the date for display.
- **Errors**: A 404 means the `base_currency` code is invalid or unsupported -- always use uppercase 3-letter ISO 4217 codes (e.g., USD, EUR, GBP).

## Anomaly Flags

- **Stale data**: If `time_last_updated` is more than 24 hours old, warn the user that rates may be outdated.
- **Missing currency**: If a target currency is absent from the `rates` map, flag it -- the currency may have been delisted or is unsupported.
- **Unusual rate values**: Flag rates that are exactly 0 or negative, as these indicate data anomalies.
- **404 on valid-looking codes**: Surface when a seemingly valid ISO currency code returns 404 -- the API may not cover that currency.
- **Rate of 1.0 for non-base currency**: If any currency other than the base shows a rate of exactly 1.0, flag as potentially suspicious data.

## Playbook

### Convert an Amount Between Two Currencies

1. Call `GET /latest/{source_currency}` with the source currency as the base.
2. Extract `rates[target_currency]` from the response.
3. Multiply the amount by that rate: `converted = amount * rates[target]`.
4. Report the result along with the `date` for context.

### Compare Two Currencies Against a Common Base

1. Call `GET /latest/USD` (or any neutral base).
2. Extract `rates[currency_A]` and `rates[currency_B]`.
3. Compute the cross rate: `A_to_B = rates[currency_B] / rates[currency_A]`.
4. Present both the individual rates and the derived cross rate.

### Check Data Freshness Before Using Rates

1. Call `GET /latest/{base_currency}`.
2. Parse `time_last_updated` as a Unix timestamp.
3. Compare against the current time -- if the difference exceeds 24 hours, warn the user.
4. Proceed with the rates only after confirming acceptable freshness.

### List All Supported Currencies

1. Call `GET /latest/USD`.
2. Extract all keys from the `rates` map.
3. Sort alphabetically and present as a list.
4. Note: the base currency (USD) will have a rate of 1.0 and is also supported.

### Build a Multi-Currency Conversion Table

1. Choose a base currency and call `GET /latest/{base_currency}`.
2. Select the desired target currencies from the `rates` map.
3. For each target, calculate conversions for standard amounts (1, 10, 100, 1000).
4. Format as a table with columns for each amount tier.
5. Include the `date` as a header note for when the rates apply.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
