---
name: furkot-trips
description: "Furkot Trips API skill. Use when working with Furkot Trips for trip. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Furkot Trips
API version: 1.0.0

## Auth
OAuth2 | OAuth2

## Base URL
https://trips.furkot.com/pub/api

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /trip -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### trip
| Method | Path | Description |
|--------|------|-------------|
| GET | /trip | list user's trips |
| GET | /trip/{trip_id}/stop | list stops for a trip identified by {trip_id} |
| GET | /trip/{trip_id}/skipped | list of skipped stops for a trip identified by {trip_id} |

## Enhanced Skill Content


## Question Mapping

- "What trips do I have?" -> GET /trip
- "Show me all my Furkot trips" -> GET /trip
- "List my travel itineraries" -> GET /trip
- "What are the stops on my trip?" -> GET /trip/{trip_id}/stop
- "Show me the itinerary for trip ABC123" -> GET /trip/{trip_id}/stop
- "What places am I visiting on this trip?" -> GET /trip/{trip_id}/stop
- "Which stops did I skip on my trip?" -> GET /trip/{trip_id}/skipped
- "Show me removed or skipped waypoints" -> GET /trip/{trip_id}/skipped
- "Are there any stops I decided not to visit?" -> GET /trip/{trip_id}/skipped
- "Get the full details of a specific trip's route" -> GET /trip/{trip_id}/stop
- "How many trips have I planned?" -> GET /trip
- "I need the trip ID first, then show me its stops" -> GET /trip then GET /trip/{trip_id}/stop
- "Compare planned vs skipped stops for a trip" -> GET /trip/{trip_id}/stop + GET /trip/{trip_id}/skipped

## Response Tips

- **Trips (GET /trip):** Returns a list of trip objects; extract `trip_id` from each to query stops or skipped endpoints.
- **Stops (GET /trip/{trip_id}/stop):** Returns ordered waypoints for a trip; expect location coordinates, names, and sequencing info.
- **Skipped (GET /trip/{trip_id}/skipped):** Same structure as stops but represents removed waypoints; an empty list means nothing was skipped.
- **Auth errors:** OAuth2 token expiry returns 401; re-authenticate before retrying.

## Anomaly Flags

- **Empty trip list:** User may not have any trips created in Furkot -- suggest creating one first.
- **404 on trip_id:** The trip ID may be invalid or deleted; surface this clearly rather than showing a generic error.
- **Skipped list much larger than stops list:** Unusual -- the user may have significantly altered their itinerary; worth flagging.
- **OAuth2 token expiration:** Proactively warn when approaching token expiry before making batch calls across multiple trips.
- **Unexpected 5xx responses:** Furkot service may be temporarily unavailable; suggest retry with backoff.

## Playbook

### 1. View Full Trip Itinerary

1. Call `GET /trip` to retrieve all trips.
2. Identify the desired trip by name or metadata; note its `trip_id`.
3. Call `GET /trip/{trip_id}/stop` to get the ordered list of stops.
4. Present stops in sequence with location details.

### 2. Audit Skipped Stops

1. Call `GET /trip` to list available trips.
2. For the target trip, call `GET /trip/{trip_id}/skipped`.
3. Compare with `GET /trip/{trip_id}/stop` to understand what was kept vs removed.
4. Summarize the ratio of active stops to skipped stops.

### 3. Multi-Trip Overview

1. Call `GET /trip` to get all trips.
2. For each trip in the list, call `GET /trip/{trip_id}/stop` to get stop counts.
3. Present a summary table: trip name, number of stops, number of skipped stops.
4. Highlight any trips with zero stops or unusually high skip rates.

### 4. Trip Validation Check

1. Call `GET /trip` and select the trip to validate.
2. Call `GET /trip/{trip_id}/stop` to verify stops exist and are properly ordered.
3. Call `GET /trip/{trip_id}/skipped` to check for unintentionally skipped waypoints.
4. Flag any trip with stops but no clear route progression (potential planning issue).


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
