---
name: taxratesio-api
description: "Taxrates.io API skill. Use when working with Taxrates.io for tax. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Taxrates.io API

## Auth
ApiKey Authorization in header

## Base URL
https://api.taxrates.io/api

## Setup
1. Set your API key in the appropriate header
2. GET /v3/tax/rates -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### tax
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/tax/rates | All tax rates |
| GET | /v1/tax/ip | Tax rates by IP address |
| GET | /v1/tax/countrycode | Tax rates by Country Code |

## Enhanced Skill Content
## Question Mapping

- "What are the tax rates for a specific zip code?" -> GET /v3/tax/rates
- "How do I look up tax rates by product code?" -> GET /v3/tax/rates
- "What taxes apply to an IP address?" -> GET /v1/tax/ip
- "Can I get tax rates for a specific country?" -> GET /v1/tax/countrycode
- "What is the sales tax in a US state?" -> GET /v3/tax/rates
- "How do I paginate through tax rate results?" -> GET /v3/tax/rates (use `cursor`)
- "What tax applies to a visitor from a given IP?" -> GET /v1/tax/ip
- "What are the VAT rates for a country code on a specific date?" -> GET /v1/tax/countrycode
- "How do I filter tax rates by product category?" -> GET /v3/tax/rates (use `filter` + `Product_code`)
- "What taxes apply to a digital product sold to a customer in Germany?" -> GET /v1/tax/countrycode (country_code=DE, set product filter)
- "How do I determine tax jurisdiction from a zip code and domain?" -> GET /v3/tax/rates
- "Can I look up historical tax rates for a country?" -> GET /v1/tax/countrycode (use `date`)
- "What tax rate applies to a customer whose location I only know by IP?" -> GET /v1/tax/ip, then optionally GET /v1/tax/countrycode for detail

## Response Tips

- **/v3/tax/rates**: Response contains `rates` as an array of maps -- each entry may represent a different tax jurisdiction (state, county, city). Sum relevant rate values for the effective total rate. Use `cursor` in subsequent requests to page through large result sets.
- **/v1/tax/ip**: Returns `country_name` and a `taxes` array. Multiple tax entries may apply (e.g., federal + regional). The IP lookup resolves geolocation server-side -- no coordinates needed.
- **/v1/tax/countrycode**: Similar shape to the IP endpoint. The `taxes` array can contain multiple tax types (VAT, GST, sales tax). When `date` is provided, rates reflect the historical value for that date.
- **Errors**: 404 means no tax data found for the given parameters (not a malformed request). 500 indicates a server-side issue -- retry with backoff.

## Anomaly Flags

- **404 on valid-looking queries**: Surface when a country code, zip, or IP returns no data -- the user may have a typo or the jurisdiction may not be covered yet.
- **500 errors**: Alert immediately; these are server-side failures. Suggest retry after a short delay and flag if repeated.
- **Empty `rates` or `taxes` arrays**: A 200 with an empty tax array is suspicious -- flag that the product code or filter may be excluding all results.
- **Inconsistent `Product_code` casing**: The v3 endpoint uses `Product_code` (capital P) while v1 uses `product_code` (lowercase). Flag if the user mixes them up -- the wrong casing will silently fail or be ignored.
- **Missing `date` parameter**: When querying historical rates via `/v1/tax/countrycode`, omitting `date` returns current rates. Flag if the user's context implies they need a past date.
- **Cursor exhaustion**: If a paginated `/v3/tax/rates` response returns no cursor, all results have been fetched. Surface this so the caller stops looping.

## Playbook

### 1. Look Up Tax Rate for a US Transaction

1. Call `GET /v3/tax/rates` with `domain`, `filter` set to your tax category, `Product_code` for the item, and `zip` for the buyer's location.
2. Inspect the `rates` array -- sum applicable jurisdiction rates (state, county, city) for the total effective rate.
3. If results are paginated, repeat with the returned `cursor` until no cursor is returned.

### 2. Determine Tax for an Anonymous Website Visitor

1. Capture the visitor's IP address from the request headers.
2. Call `GET /v1/tax/ip` with the `ip`, your `domain`, and relevant `filter`/`product_code`.
3. Read `country_name` to confirm geolocation, then use the `taxes` array to apply the correct rate.
4. If more granular rates are needed, follow up with `GET /v1/tax/countrycode` using the resolved country code and the buyer's `zip` if known.

### 3. Display Tax Rates for an International Storefront

1. For each country you sell to, call `GET /v1/tax/countrycode` with the appropriate `country_code` and `domain`.
2. Use the `filter` parameter to narrow results to your product type.
3. Cache the `taxes` array per country -- refresh periodically or when `date` changes (e.g., new tax year).

### 4. Audit Historical Tax Rates

1. Identify the transaction date and country.
2. Call `GET /v1/tax/countrycode` with the `country_code` and the `date` parameter set to the transaction date.
3. Compare the returned `taxes` against what was charged -- flag discrepancies for review.
4. Repeat across all relevant jurisdictions if the transaction spans multiple countries.

### 5. Paginate Through All Rates for a Domain

1. Call `GET /v3/tax/rates` with `domain`, `filter`, and `Product_code`. Omit `cursor` for the first request.
2. Process the `rates` array from the response.
3. If the response includes a `cursor` value, call the same endpoint again with that `cursor`.
4. Repeat until no `cursor` is returned, indicating all results have been consumed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
