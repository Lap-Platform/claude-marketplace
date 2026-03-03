---
name: on-demand-flight-status
description: "On-Demand Flight Status API skill. Use when working with On-Demand Flight Status for schedule. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# On-Demand Flight Status
API version: 2.0.2

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v2

## Setup
1. No auth setup needed
2. GET /schedule/flights -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### schedule
| Method | Path | Description |
|--------|------|-------------|
| GET | /schedule/flights | Retrieves a unique flight by search criteria. |

## Enhanced Skill Content
## Question Mapping

- "What is the status of flight BA123 today?" -> GET /schedule/flights
- "Is my Lufthansa flight LH456 on time for March 15?" -> GET /schedule/flights
- "What gate is Delta flight DL789 departing from?" -> GET /schedule/flights
- "Has United UA100 been delayed or cancelled?" -> GET /schedule/flights
- "What time does AA587 actually depart vs scheduled?" -> GET /schedule/flights
- "Show me the flight schedule for QR901 on 2026-03-10" -> GET /schedule/flights
- "What aircraft type is operating EK202 today?" -> GET /schedule/flights
- "Is there an operational suffix for flight IB3456?" -> GET /schedule/flights
- "What terminal does SQ321 arrive at?" -> GET /schedule/flights
- "Track AF1680 departure and arrival times" -> GET /schedule/flights
- "Was JL5 diverted or rerouted today?" -> GET /schedule/flights
- "Check if SW1234 has a codeshare operating carrier" -> GET /schedule/flights
- "What is the estimated arrival time for NH7 on March 5?" -> GET /schedule/flights

## Response Tips

- **Schedule flights**: Response nests flight segments under `data[]`. Each entry contains `flightDesignator`, `flightPoints[]` (departure/arrival with timestamps and terminals), and `legs[]` with aircraft info. Always check `scheduledDepartureDate` vs actual times in `timings[]` where `qualifier` distinguishes scheduled, estimated, and actual values.

## Anomaly Flags

- **401 Unauthorized**: Token expired or missing. Surface immediately and prompt for re-authentication via OAuth2 token refresh.
- **400 Bad Request**: Likely malformed `carrierCode` (must be 2-char IATA), invalid `flightNumber` (numeric, 1-4 digits), or `scheduledDepartureDate` not in YYYY-MM-DD format. Parse the `errors[].detail` field and suggest corrections.
- **Empty `data[]` array**: Flight exists but no schedule found for the given date. Suggest checking adjacent dates or verifying the carrier/flight number combination.
- **Multiple entries in `data[]`**: Flight has multiple segments or legs (e.g., connecting flights under one flight number). Surface this so the user knows which segment they care about.
- **`operationalSuffix` present in response**: Indicates a modified or duplicate flight operation. Flag when the suffix differs from what was queried or when it appears unexpectedly.
- **Departure date in the past**: API may return stale or no data for historical flights. Warn when the queried date is more than a few days old.

## Playbook

### 1. Check if a specific flight is on time

1. Identify the 2-character IATA carrier code (e.g., `BA` for British Airways)
2. Extract the numeric flight number (e.g., `123`)
3. Call `GET /schedule/flights?carrierCode=BA&flightNumber=123&scheduledDepartureDate=2026-03-03`
4. In the response, locate `flightPoints[].departure.timings[]` and compare `qualifier: "STD"` (scheduled) vs `qualifier: "ETD"` (estimated)
5. Report the difference as the delay, or confirm on-time status

### 2. Get full gate and terminal information

1. Call `GET /schedule/flights` with the carrier, flight number, and date
2. Navigate to `data[].flightPoints[]` for each stop
3. Extract `departure.terminal` and `departure.gate` for the origin
4. Extract `arrival.terminal` and `arrival.gate` for the destination
5. Note: gate info may be absent if not yet assigned by the airport

### 3. Identify the operating aircraft

1. Call `GET /schedule/flights` with required parameters
2. In the response, inspect `data[].legs[].aircraftEquipment.aircraftType`
3. Cross-reference the IATA aircraft code (e.g., `788` = Boeing 787-8) if the user needs the common name
4. Check `legs[].boardPointIataCode` and `legs[].offPointIataCode` to confirm the correct leg

### 4. Handle authentication and retry on 401

1. Obtain an OAuth2 token from `https://test.api.amadeus.com/v1/security/oauth2/token` using client credentials grant
2. Include the token as `Authorization: Bearer <token>` in the flight status request
3. If a 401 is returned, the token has expired - request a new token and retry once
4. If 401 persists, verify client ID and secret are correct

### 5. Look up a flight with an operational suffix

1. Some airlines use operational suffixes (e.g., `A`, `B`) to distinguish duplicate flight numbers on the same day
2. Call `GET /schedule/flights` with `carrierCode`, `flightNumber`, `scheduledDepartureDate`, and `operationalSuffix`
3. If unsure of the suffix, first call without it to see all variants returned in `data[]`
4. Each result's `flightDesignator.operationalSuffix` field confirms which variant it represents


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
