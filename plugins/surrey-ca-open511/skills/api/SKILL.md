---
name: city-of-surrey-open511-api
description: "City of Surrey Open511 API skill. Use when working with City of Surrey Open511 for events, jurisdiction, jurisdictiongeography. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# City of Surrey Open511 API
API version: 0.1

## Auth
No authentication required.

## Base URL
http://data.surrey.ca/open511

## Setup
1. No auth setup needed
2. GET /events -- verify access

## Endpoints

4 endpoints across 4 groups. See references/api-spec.lap for full details.

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Provides real time traffic obstruction events.  The event resource provides information about road events (constructions, special events, etc.). |

### jurisdiction
| Method | Path | Description |
|--------|------|-------------|
| GET | /jurisdiction | Lists the jurisdictions publishing data through this Open511 API implementation. |

### jurisdictiongeography
| Method | Path | Description |
|--------|------|-------------|
| GET | /jurisdictiongeography | Provides the geographical boundaries for all the jurisdictions. |

### areas
| Method | Path | Description |
|--------|------|-------------|
| GET | /areas | Provides the geographical boundaries for all the jurisdictions. |

## Enhanced Skill Content
## Question Mapping

- "What road events are currently active in Surrey?" -> GET /events
- "Are there any construction closures on King George Boulevard?" -> GET /events?road_name=King George Boulevard&event_type=CONSTRUCTION
- "What events were updated in the last 24 hours?" -> GET /events?updated=>YYYY-MM-DD
- "Show me all high-severity traffic incidents" -> GET /events?severity=MAJOR&status=ACTIVE
- "What events are happening in a specific area?" -> GET /events?area_id={area_id}
- "Find events within a geographic bounding box" -> GET /events?bbox={min_lon},{min_lat},{max_lon},{max_lat}
- "Which jurisdiction does Surrey fall under?" -> GET /jurisdiction
- "Get the geographic boundary of the jurisdiction" -> GET /jurisdictiongeography
- "What named areas are defined in Surrey's system?" -> GET /areas
- "Are there any road closures right now?" -> GET /events?event_type=CONSTRUCTION&status=ACTIVE
- "What events were created after a specific date?" -> GET /events?created=>YYYY-MM-DD
- "Get events in XML format instead of default" -> GET /events?format=xml
- "Show all events regardless of status" -> GET /events?status=ALL

## Response Tips

- **events**: Results follow Open511 schema -- each event nests `roads` (array of affected road segments with `name`, `direction`, `from`, `to`) and `geography` (GeoJSON). Pagination may use `<link rel="next">` in the response; always check for a next link before assuming all results are returned.
- **jurisdiction**: Returns a single jurisdiction object with `id`, `name`, and contact info. No pagination.
- **jurisdictiongeography**: Returns GeoJSON geometry defining the jurisdiction boundary. Can be large; parse as spatial data, not display text.
- **areas**: Returns a flat list of named sub-areas with IDs usable in the `area_id` filter on `/events`.

## Anomaly Flags

- **Empty event list with no error**: The API returns 200 with an empty collection when no events match filters -- surface this explicitly so the user knows it is not a failure.
- **Stale data**: If the most recent `updated` timestamp across all events is more than 48 hours old, flag that the feed may not be refreshing.
- **Unrecognized event_type or severity values**: Open511 has a defined set (CONSTRUCTION, INCIDENT, SPECIAL_EVENT, WEATHER_CONDITION; MINOR, MODERATE, MAJOR, UNKNOWN). Flag any value outside this set as a possible schema extension.
- **Missing geography on events**: If an event lacks a `geography` field, flag it -- mapping and bbox queries depend on this data being present.
- **Format parameter behavior**: If a non-default `format` value returns an unexpected content type or an error, surface it -- not all formats may be supported.

## Playbook

### 1. Monitor Active Road Disruptions

1. Call `GET /events?status=ACTIVE` to fetch all current events.
2. Filter results client-side by `event_type` (CONSTRUCTION vs INCIDENT) if needed.
3. Extract `roads[].name` from each event to build a list of affected streets.
4. Check for a pagination next link; fetch additional pages until exhausted.
5. Re-poll periodically using `updated=>LAST_CHECK_TIMESTAMP` to get only changes.

### 2. Map Events in a Specific Area

1. Call `GET /areas` to retrieve available area IDs and names.
2. Identify the target area's `id` from the list.
3. Call `GET /events?area_id={id}&status=ACTIVE` to get events in that area.
4. Extract the `geography` field from each event for map plotting.

### 3. Build a Jurisdiction Overview

1. Call `GET /jurisdiction` to get the jurisdiction name and metadata.
2. Call `GET /jurisdictiongeography` to get the boundary polygon.
3. Call `GET /events?status=ACTIVE` to count and summarize current disruptions.
4. Combine into a dashboard showing jurisdiction info, boundary, and active event count by severity.

### 4. Track Changes to a Specific Road

1. Call `GET /events?road_name={name}` to get all events on that road.
2. Note the most recent `updated` timestamp from the results.
3. On subsequent checks, call `GET /events?road_name={name}&updated=>{last_timestamp}`.
4. Diff new results against previous state to identify new, changed, or resolved events.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
