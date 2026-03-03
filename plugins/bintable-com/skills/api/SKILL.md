---
name: bin-lookup-api
description: "BIN Lookup API skill. Use when working with BIN Lookup for {bin}, balance. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# BIN Lookup API
API version: 1.0.0-oas3

## Auth
ApiKey api_key in query

## Base URL
https://api.bintable.com/v1

## Setup
1. Set your API key in the appropriate header
2. GET /balance -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### {bin}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{bin} | Lookup for bin |

### balance
| Method | Path | Description |
|--------|------|-------------|
| GET | /balance | Check Balance |

## Enhanced Skill Content
## Question Mapping

- "What bank issued this card?" -> GET /{bin}
- "Look up BIN 453201" -> GET /{bin}
- "What card network is this number on?" -> GET /{bin}
- "Is this a credit or debit card?" -> GET /{bin}
- "What country is this card from?" -> GET /{bin}
- "Check if BIN 535316 is prepaid" -> GET /{bin}
- "How many API lookups do I have left?" -> GET /balance
- "Check my BIN API quota" -> GET /balance
- "What card brand does 411111 belong to?" -> GET /{bin}
- "Identify the issuing bank for multiple BINs" -> GET /{bin} (loop)
- "Verify my API key is working" -> GET /balance
- "Is this a commercial or personal card?" -> GET /{bin}
- "What card level is BIN 601100?" -> GET /{bin}

## Response Tips

- **BIN Lookup (GET /{bin})**: Response contains nested bank object (name, city, url, phone), card metadata (scheme, type, category, country). Country is an object with fields like name, alpha2, latitude, longitude. A `null` bank object means issuer data is unavailable, not an error.
- **Balance (GET /balance)**: Returns remaining lookup credits. Check this before batch operations to avoid mid-run 403 errors.
- **Errors**: 401 means missing or malformed api_key. 403 means key is valid but quota exhausted or access denied. 422 means the BIN value is malformed (not 6-8 digits).

## Anomaly Flags

- **Low balance**: After each lookup, if a balance check shows fewer than 10 remaining credits, warn the user before continuing batch operations.
- **422 on lookup**: Surface that the BIN must be 6 to 8 digits. Leading zeros matter -- do not trim them.
- **403 after prior success**: Quota likely exhausted mid-session. Proactively check balance and report remaining credits.
- **Null or empty fields**: If bank name, country, or scheme come back null, flag that the BIN may be unregistered, newly issued, or from a region with limited coverage.
- **Repeated 401**: API key may have been revoked or rotated. Prompt the user to verify their key.

## Playbook

### 1. Look Up a Single BIN

1. Call `GET /balance?api_key={key}` to confirm credits are available.
2. Call `GET /{bin}?api_key={key}` with the 6-8 digit BIN.
3. Extract card scheme, type, issuing bank name, and country from the response.
4. Present a concise summary: brand, type (credit/debit), bank, and country.

### 2. Batch BIN Validation

1. Call `GET /balance?api_key={key}` and note remaining credits.
2. Compare credit count against the number of BINs to process. Warn if insufficient.
3. Loop through each BIN, calling `GET /{bin}?api_key={key}`.
4. Collect results into a table with columns: BIN, Brand, Type, Bank, Country.
5. Call `GET /balance?api_key={key}` again and report credits consumed.

### 3. Verify API Key and Connectivity

1. Call `GET /balance?api_key={key}`.
2. If 200: key is valid -- report remaining credits.
3. If 401: key is missing or malformed -- prompt user to provide a valid key.
4. If 403: key recognized but access denied -- suggest checking account status at bintable.com.

### 4. Identify Card Origin Country for Fraud Review

1. Collect the BIN (first 6-8 digits of the card number).
2. Call `GET /{bin}?api_key={key}`.
3. Extract `country.alpha2` and `country.name` from the response.
4. Compare against the expected transaction country.
5. Flag a mismatch as a potential fraud signal, noting the issuing bank for context.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
