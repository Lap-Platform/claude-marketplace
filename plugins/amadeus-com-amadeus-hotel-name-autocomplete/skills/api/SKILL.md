---
name: hotel-name-autocomplete
description: "Hotel Name Autocomplete API skill. Use when working with Hotel Name Autocomplete for reference-data. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Hotel Name Autocomplete
API version: 1.0.3

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /reference-data/locations/hotel -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### reference-data
| Method | Path | Description |
|--------|------|-------------|
| GET | /reference-data/locations/hotel | Returns a list of hotels matching a given keyword. |

## Enhanced Skill Content
## Question Mapping

- "Search for hotels by name?" -> GET /reference-data/locations/hotel
- "Autocomplete a hotel name?" -> GET /reference-data/locations/hotel
- "Find hotels matching a keyword?" -> GET /reference-data/locations/hotel
- "Look up hotel names in a specific country?" -> GET /reference-data/locations/hotel
- "What hotel subtypes can I search for?" -> GET /reference-data/locations/hotel
- "Get hotel suggestions in French?" -> GET /reference-data/locations/hotel
- "Limit hotel autocomplete results to 5?" -> GET /reference-data/locations/hotel
- "Find hotels starting with 'Hilton' in the US?" -> GET /reference-data/locations/hotel
- "Search for hotel chains by partial name?" -> GET /reference-data/locations/hotel
- "What hotels match 'Mar' in Spain?" -> GET /reference-data/locations/hotel
- "Get localized hotel names in German?" -> GET /reference-data/locations/hotel
- "How do I narrow hotel search to a country?" -> GET /reference-data/locations/hotel

## Response Tips

- **Hotel results (200):** Response contains a `data` array of location objects. Each entry includes hotel name, IATA code, and geographic details. Use `max` to control result count; defaults may return many matches.
- **Validation errors (400):** Returned when `keyword` or `subType` is missing or malformed. Check `errors[].detail` for the specific field that failed validation.
- **Server errors (500):** Transient Amadeus platform issues. Retry with exponential backoff.

## Anomaly Flags

- **Missing required params:** Surface immediately if `keyword` or `subType` is omitted -- the API will reject with 400.
- **Empty result sets:** Flag when a reasonable keyword returns zero matches; may indicate wrong `countryCode` filter or a typo.
- **Rate limiting (429):** Amadeus enforces per-key rate limits. Surface when responses include rate-limit headers approaching threshold.
- **Auth expiry:** Amadeus uses OAuth2 tokens with short TTLs. Flag 401 responses and prompt token refresh.
- **Deprecated subType values:** Watch for warning headers indicating deprecated `subType` enum values.
- **Unusually slow responses (>2s):** May indicate Amadeus platform degradation.

## Playbook

### 1. Basic Hotel Name Autocomplete

1. Obtain an OAuth2 access token from `POST /v1/security/oauth2/token`
2. Call `GET /reference-data/locations/hotel` with `keyword` (e.g., "Hilt") and `subType` (e.g., "HOTEL_LEISURE")
3. Parse the `data` array from the 200 response
4. Present matching hotel names and their location codes to the user

### 2. Country-Scoped Hotel Search

1. Authenticate via OAuth2
2. Call `GET /reference-data/locations/hotel` with `keyword`, `subType`, and `countryCode` (ISO 3166-1 alpha-2, e.g., "FR")
3. Review results -- if empty, retry without `countryCode` to confirm the keyword has global matches
4. Use `lang` param (e.g., "FR") to get localized hotel names matching the country

### 3. Building a Search-As-You-Type UI

1. Authenticate and cache the access token (refresh before expiry)
2. On each keystroke (debounced ~300ms), call `GET /reference-data/locations/hotel` with current input as `keyword`, `subType` set appropriately, and `max=5` to limit payload
3. Parse `data` array and render suggestions in a dropdown
4. On selection, extract the hotel's unique identifier for downstream booking calls

### 4. Handling Errors Gracefully

1. Send request to `GET /reference-data/locations/hotel`
2. If 400: read `errors[].detail` to identify the invalid parameter, fix it, and retry
3. If 401: refresh the OAuth2 token and retry the original request
4. If 500: wait 1-2 seconds and retry up to 3 times with exponential backoff
5. If all retries fail, surface the error to the user with the Amadeus status detail


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
