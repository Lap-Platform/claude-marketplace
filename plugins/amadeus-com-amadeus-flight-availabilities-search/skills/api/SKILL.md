---
name: flight-availibilities-search
description: "Flight Availibilities Search API skill. Use when working with Flight Availibilities Search for shopping. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Availibilities Search
API version: 1.0.2

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v1

## Setup
1. No auth setup needed
3. POST /shopping/availability/flight-availabilities -- create first flight-availabilities

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### shopping
| Method | Path | Description |
|--------|------|-------------|
| POST | /shopping/availability/flight-availabilities | Return list of Flight Availabilities based on posted searching criteria. |

## Enhanced Skill Content
## Question Mapping

- "How do I search for available flights?" -> POST /shopping/availability/flight-availabilities
- "Are there seats available on flights from Paris to New York?" -> POST /shopping/availability/flight-availabilities
- "How do I check flight availability for a specific date?" -> POST /shopping/availability/flight-availabilities
- "Can I search for round-trip flight availability?" -> POST /shopping/availability/flight-availabilities
- "How do I find available cabin classes on a route?" -> POST /shopping/availability/flight-availabilities
- "What flights have open seats between two cities?" -> POST /shopping/availability/flight-availabilities
- "How do I search availability for multi-segment itineraries?" -> POST /shopping/availability/flight-availabilities
- "Can I filter flight availability by airline?" -> POST /shopping/availability/flight-availabilities
- "How do I check seat availability across multiple fare classes?" -> POST /shopping/availability/flight-availabilities
- "What is the X-HTTP-Method-Override header used for?" -> POST /shopping/availability/flight-availabilities
- "How do I search for one-way flight availability?" -> POST /shopping/availability/flight-availabilities
- "Can I request availability for a specific number of passengers?" -> POST /shopping/availability/flight-availabilities

## Response Tips

- **Shopping/Availability**: Responses return nested `data[]` arrays with flight segments, cabin availability, and booking class details. Check `dictionaries` for carrier/aircraft code lookups. 400 errors include an `errors[]` array with `detail` and `source.pointer` fields pointing to the invalid request parameter.

## Anomaly Flags

- **400 validation errors**: Surface the `source.pointer` field to pinpoint exactly which part of the request body is malformed
- **Missing X-HTTP-Method-Override header**: This header is required -- flag immediately if omitted, as the request will fail
- **Empty availability results**: Alert when `data[]` returns empty, suggesting the route, date, or cabin class has no availability
- **Rate limiting (429)**: Amadeus test environment has strict rate limits -- surface approaching thresholds and suggest backoff
- **Token expiration**: Amadeus uses OAuth2; flag 401 responses and prompt re-authentication before retrying
- **Deprecated API version**: Flag if response headers indicate a newer API version is available

## Playbook

### 1. Search One-Way Flight Availability

1. Authenticate via `POST /v1/security/oauth2/token` to obtain a Bearer token
2. Build the request body with `originDestinations` specifying departure city, arrival city, and date
3. Set `travelers` array with passenger count and type
4. Include header `X-HTTP-Method-Override: GET`
5. Send `POST /shopping/availability/flight-availabilities` with the body
6. Parse `data[]` for available segments and cabin class availability

### 2. Search Round-Trip Availability

1. Obtain a valid access token
2. Build request body with two entries in `originDestinations`: outbound and return legs
3. Set `travelers` with passenger details
4. Add `X-HTTP-Method-Override: GET` header
5. Send `POST /shopping/availability/flight-availabilities`
6. Match outbound and return segments in the response by `originDestinationId`

### 3. Handle Validation Errors

1. Send the availability search request
2. If a 400 response is returned, read the `errors[]` array
3. Check `errors[].source.pointer` to identify the invalid field
4. Check `errors[].detail` for a human-readable explanation
5. Correct the request body and retry

### 4. Filter by Cabin Class

1. Authenticate and prepare the base request body
2. Add `sources` array to specify data providers (e.g., `GDS`)
3. Include `searchCriteria.flightFilters.cabinRestrictions` with desired cabin (ECONOMY, BUSINESS, FIRST)
4. Set coverage and origDestination scope for the cabin filter
5. Send `POST /shopping/availability/flight-availabilities`
6. Review returned `availabilityClasses` within each segment for matching cabin inventory

### 5. Paginate Large Result Sets

1. Send the initial availability search request
2. Check response `meta` object for `count` and pagination links
3. If more results exist, use the `next` link or adjust `searchCriteria.maxFlightOffers`
4. Repeat until all relevant availability data is collected
5. Deduplicate results by segment identifiers if combining across requests


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
