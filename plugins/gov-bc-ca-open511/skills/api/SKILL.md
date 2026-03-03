---
name: drivebcs-open511-api
description: "DriveBC's Open511 API skill. Use when working with DriveBC's Open511 for events, jurisdiction, jurisdictiongeography. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# DriveBC's Open511 API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
http://api.open511.gov.bc.ca/

## Setup
1. No auth setup needed
2. GET /events -- verify access

## Endpoints

4 endpoints across 4 groups. See references/api-spec.lap for full details.

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Lists road events |

### jurisdiction
| Method | Path | Description |
|--------|------|-------------|
| GET | /jurisdiction | Lists the jurisdictions publishing data through this Open511 API implementation |

### jurisdictiongeography
| Method | Path | Description |
|--------|------|-------------|
| GET | /jurisdictiongeography | Provides the geographical boundaries for all the jurisdictions. |

### areas
| Method | Path | Description |
|--------|------|-------------|
| GET | /areas | Lists the geographical areas (e.g. districts) that can be used to filter events. |

## Enhanced Skill Content
## Question Mapping

- "What road events are currently active in BC?" -> GET /events?status=ACTIVE
- "Are there any construction projects on Highway 1?" -> GET /events?event_type=CONSTRUCTION&road_name=Highway 1
- "Show me major incidents right now" -> GET /events?status=ACTIVE&severity=MAJOR&event_type=INCIDENT
- "What weather conditions are affecting roads in BC?" -> GET /events?event_type=WEATHER_CONDITION&status=ACTIVE
- "Were there any events updated since yesterday?" -> GET /events?updated=>{yesterday_iso8601}
- "What events are happening near Vancouver?" -> GET /events?bbox=-123.3,49.0,-122.8,49.4
- "Show me all special events affecting traffic" -> GET /events?event_type=SPECIAL_EVENT&status=ACTIVE
- "What road conditions exist on Highway 99?" -> GET /events?event_type=ROAD_CONDITION&road_name=Highway 99
- "List all areas/regions DriveBC tracks" -> GET /areas
- "What jurisdiction does this API cover?" -> GET /jurisdiction
- "Get the geographic boundary of the DriveBC jurisdiction" -> GET /jurisdictiongeography
- "What events were created after March 1st?" -> GET /events?created=>2026-03-01T00:00:00Z
- "Show me archived incidents in a specific area" -> GET /events?status=ARCHIVED&event_type=INCIDENT&area_id=drivebc.ca/{id}
- "Give me all events as XML" -> GET /events?format=xml

## Response Tips

- **Events**: Results are nested under a top-level `events` array; each event contains `geography` (GeoJSON), `roads` (array with road name and direction), and `schedule` with recurring/interval blocks. Pagination uses `Link` headers or a `pagination.next_url` field -- always check for a next page.
- **Jurisdiction**: Returns a single object (or array of one) with jurisdiction ID, name, and contact info under `jurisdictions`. No pagination.
- **Jurisdiction Geography**: Returns GeoJSON geometry representing the full coverage boundary. Can be large -- parse as spatial data, not plain text.
- **Areas**: Returns a flat list of named geographic regions under `areas`, each with an `id` (e.g., `drivebc.ca/1`) usable as the `area_id` filter on events.

## Anomaly Flags

- **Empty event list with `status=ACTIVE`**: Unusual for a major highway network -- may indicate an API outage or data feed delay rather than truly zero events. Surface this to the user.
- **Stale `updated` timestamps**: If the most recent event update is more than 24 hours old, the data feed may be lagging. Flag this proactively.
- **Large bbox returning few results**: The bounding box may be malformed (lon/lat order is west,south,east,north). Alert if results seem unexpectedly sparse relative to area size.
- **XML format fallback**: If a JSON request returns XML or unparseable content, the server may be defaulting. Flag the content-type mismatch.
- **Pagination truncation**: If the response includes a next page URL, always warn the user that results are incomplete and offer to fetch remaining pages.
- **Deprecated or unknown `event_type` values**: If the API returns event types not in the known set (CONSTRUCTION, SPECIAL_EVENT, INCIDENT, WEATHER_CONDITION, ROAD_CONDITION), surface the new type for the user's awareness.

## Playbook

### 1. Get a Full Picture of Current Road Disruptions

1. Fetch all active events: `GET /events?status=ACTIVE`
2. Group results by `event_type` (construction, incidents, weather, road conditions)
3. Summarize counts per category and list the most severe items first
4. Check for pagination -- fetch all pages before summarizing
5. If the user mentions a specific route, filter with `road_name` to narrow down

### 2. Monitor a Specific Highway Corridor

1. Identify the road name (e.g., "Highway 5") and approximate bounding box coordinates
2. Fetch events: `GET /events?status=ACTIVE&road_name=Highway 5&bbox={coords}`
3. Note the `updated` timestamp of each event for change tracking
4. On subsequent checks, use `updated=>` with the last check time to get only changes
5. Surface any new INCIDENT or WEATHER_CONDITION events immediately

### 3. Explore Available Regions and Filter by Area

1. Fetch all areas: `GET /areas`
2. Present the list of area names and IDs to the user
3. Once the user picks a region, fetch events: `GET /events?status=ACTIVE&area_id={selected_id}`
4. Summarize event types and severities for that region

### 4. Historical Event Research

1. Determine the date range the user is interested in
2. Fetch archived events: `GET /events?status=ARCHIVED&created=>{start_date}&updated=<{end_date}`
3. Filter by `event_type` or `road_name` if the user specifies
4. Page through all results to build the complete dataset
5. Summarize patterns (e.g., recurring construction zones, seasonal weather events)

### 5. Jurisdiction and Coverage Verification

1. Fetch jurisdiction info: `GET /jurisdiction` to confirm the API covers `drivebc.ca`
2. Fetch geographic boundary: `GET /jurisdictiongeography` for the exact coverage polygon
3. If a user asks about a location, check whether their coordinates fall within the jurisdiction geometry before querying events
4. If outside coverage, inform the user that this API only covers British Columbia provincial highways


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
