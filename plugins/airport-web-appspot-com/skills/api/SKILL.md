---
name: airportsapi
description: "airportsapi API skill. Use when working with airportsapi for airportsapi. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# airportsapi
API version: v1

## Auth
OAuth2

## Base URL
https://airport-web.appspot.com/_ah/api

## Setup
1. Configure auth: OAuth2
2. GET /airportsapi/v1/airports/{icao_code} -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### airportsapi
| Method | Path | Description |
|--------|------|-------------|
| GET | /airportsapi/v1/airports/{icao_code} |  |

## Enhanced Skill Content
## Question Mapping

- "What information is available for a specific airport?" -> GET /airportsapi/v1/airports/{icao_code}
- "Look up airport details by ICAO code" -> GET /airportsapi/v1/airports/{icao_code}
- "What are the details for KJFK?" -> GET /airportsapi/v1/airports/KJFK
- "Get data for Heathrow airport" -> GET /airportsapi/v1/airports/EGLL
- "Find airport info using its four-letter code" -> GET /airportsapi/v1/airports/{icao_code}
- "Is this ICAO code valid?" -> GET /airportsapi/v1/airports/{icao_code} (check for error response)
- "What continent or country is airport LFPG in?" -> GET /airportsapi/v1/airports/LFPG
- "Get coordinates for a specific airport" -> GET /airportsapi/v1/airports/{icao_code}
- "Compare two airports' details" -> GET /airportsapi/v1/airports/{icao_code} (call twice, compare results)
- "What is the IATA code for this ICAO code?" -> GET /airportsapi/v1/airports/{icao_code}
- "Does this airport have international service?" -> GET /airportsapi/v1/airports/{icao_code}
- "Verify an airport exists before using it in another system" -> GET /airportsapi/v1/airports/{icao_code}

## Response Tips

- **Airport lookups**: Response contains airport metadata keyed by ICAO code. Expect fields like name, IATA code, location, coordinates, country, and elevation. A 200 with empty or null fields may indicate a valid but sparsely documented airport. Non-200 responses typically mean the ICAO code is unrecognized.

## Anomaly Flags

- **Invalid ICAO code**: Surface when user provides a code that is not exactly 4 uppercase letters (standard ICAO format), warn before making the request.
- **Empty response body on 200**: Flag when the API returns 200 but the payload is empty or missing expected fields -- the code may be valid but unsupported.
- **OAuth2 token expiry**: Proactively warn when authentication fails with 401/403, as OAuth2 tokens may have expired and need refresh.
- **Unexpected status codes**: Surface 429 (rate limiting), 503 (service unavailable), or any 5xx errors -- this is a Google App Engine-hosted service and may have quota limits.
- **Deprecated API host**: Flag if the `appspot.com` endpoint returns redirect responses, as Google App Engine apps occasionally migrate.

## Playbook

### 1. Look Up a Single Airport

1. Confirm the user has a valid 4-letter ICAO code (e.g., KJFK, EGLL, LFPG).
2. Call `GET /airportsapi/v1/airports/{icao_code}` with OAuth2 credentials.
3. Parse the 200 response for airport name, location, and coordinates.
4. Present key fields: name, IATA code, country, latitude/longitude, elevation.

### 2. Validate an ICAO Code

1. Take the user-provided code and normalize to uppercase.
2. Call `GET /airportsapi/v1/airports/{icao_code}`.
3. If 200 with populated data: code is valid -- return airport name as confirmation.
4. If error or empty response: inform the user the code is unrecognized and suggest checking the format (4 uppercase letters, e.g., KJFK).

### 3. Compare Two Airports

1. Collect both ICAO codes from the user.
2. Call `GET /airportsapi/v1/airports/{icao_code}` for each (in parallel if possible).
3. Extract matching fields from both responses (name, country, coordinates, elevation).
4. Present a side-by-side comparison.
5. Optionally calculate distance between the two airports using their coordinates.

### 4. Batch Airport Research

1. Gather a list of ICAO codes the user needs information on.
2. Iterate through each code, calling `GET /airportsapi/v1/airports/{icao_code}` per code.
3. Watch for rate limiting (429 responses) -- back off and retry if encountered.
4. Aggregate results into a summary table with key fields per airport.
5. Flag any codes that returned errors or empty data.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
