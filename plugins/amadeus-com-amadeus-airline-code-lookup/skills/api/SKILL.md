---
name: airline-code-lookup-api
description: "Airline Code Lookup API skill. Use when working with Airline Code Lookup for reference-data. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Airline Code Lookup API
API version: 1.2.1

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
2. GET /reference-data/airlines -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### reference-data
| Method | Path | Description |
|--------|------|-------------|
| GET | /reference-data/airlines | Return airlines information. |

## Enhanced Skill Content
## Question Mapping

- "What airline has the code BA?" -> GET /reference-data/airlines?airlineCodes=BA
- "Look up airline code DL" -> GET /reference-data/airlines?airlineCodes=DL
- "What airline does the IATA code QF belong to?" -> GET /reference-data/airlines?airlineCodes=QF
- "Find information about multiple airlines AA and UA" -> GET /reference-data/airlines?airlineCodes=AA,UA
- "List all known airlines" -> GET /reference-data/airlines
- "Is LH a valid airline code?" -> GET /reference-data/airlines?airlineCodes=LH
- "What is the full name of airline code EK?" -> GET /reference-data/airlines?airlineCodes=EK
- "Resolve these IATA codes to airline names: FR, U2, W6" -> GET /reference-data/airlines?airlineCodes=FR,U2,W6
- "Which airline operates under code NH?" -> GET /reference-data/airlines?airlineCodes=NH
- "Verify if XY is a real airline code" -> GET /reference-data/airlines?airlineCodes=XY
- "Get details for Southwest Airlines by code WN" -> GET /reference-data/airlines?airlineCodes=WN
- "I have a booking with airline code CX, who is that?" -> GET /reference-data/airlines?airlineCodes=CX

## Response Tips

- **GET /reference-data/airlines**: Response wraps results in a `data` array; each entry contains `iataCode`, `icaoCode`, `businessName`, and `commonName`. An empty `data` array means no match -- not an error. When querying multiple codes, results may return fewer items than requested if some codes are invalid.

## Anomaly Flags

- **Empty results for valid-looking codes**: Surface when `data` is an empty array -- the code may be retired, seasonal, or a codeshare alias. Suggest the user double-check the code or try without filters to browse.
- **400 Bad Request**: Likely malformed `airlineCodes` parameter (wrong format, special characters, or exceeding max length). Surface the `errors[].detail` message from the response body.
- **500 Internal Server Error**: Amadeus service disruption. Surface immediately and suggest retrying after a short delay.
- **OAuth token expiry**: This API requires an Amadeus OAuth2 bearer token. If a 401 is returned, surface that the token has expired and needs refresh via `POST /v1/security/oauth2/token`.
- **Test vs production base URL**: The spec uses `test.api.amadeus.com`. Flag if the user appears to expect production data -- test environment has limited/synthetic data.

## Playbook

### 1. Look Up a Single Airline by IATA Code

1. Call `GET /reference-data/airlines?airlineCodes=BA`
2. Parse `data[0].businessName` and `data[0].commonName` from the response
3. If `data` is empty, inform the user the code was not found
4. Present the airline's business name, common name, and ICAO code

### 2. Batch-Resolve Multiple Airline Codes

1. Collect all IATA codes from the user (e.g., from a flight itinerary)
2. Join them as a comma-separated string: `AA,DL,UA`
3. Call `GET /reference-data/airlines?airlineCodes=AA,DL,UA`
4. Map each returned entry by `iataCode` to build a lookup table
5. Flag any requested codes missing from the response as unrecognized

### 3. Validate an Unknown Airline Code

1. Call `GET /reference-data/airlines?airlineCodes=XY`
2. Check if `data` array is non-empty
3. If empty, report the code as invalid or unrecognized
4. If found, confirm the airline identity and present its details

### 4. Browse All Airlines

1. Call `GET /reference-data/airlines` with no parameters
2. Iterate through the `data` array to list all available airlines
3. Note: the test environment may return a subset of real-world airlines
4. Use results to build a reference table or autocomplete source

### 5. Enrich a Flight Booking with Airline Details

1. Extract the airline code from the booking's carrier field (e.g., `EK`)
2. Call `GET /reference-data/airlines?airlineCodes=EK`
3. Merge `businessName` and `commonName` into the booking display
4. If the code is a codeshare, note that the operating carrier may differ


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
