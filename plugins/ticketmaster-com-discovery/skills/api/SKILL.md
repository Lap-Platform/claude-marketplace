---
name: discovery-api
description: "Discovery API skill. Use when working with Discovery for discovery. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# Discovery API
API version: v2

## Auth
No authentication required.

## Base URL
https://www.ticketmaster.com/discovery/v2

## Setup
1. No auth setup needed
2. GET /discovery/v2/attractions -- verify access

## Endpoints

13 endpoints across 1 groups. See references/api-spec.lap for full details.

### discovery
| Method | Path | Description |
|--------|------|-------------|
| GET | /discovery/v2/attractions | Attraction Search |
| GET | /discovery/v2/attractions/{id} | Get Attraction Details |
| GET | /discovery/v2/classifications | Classification Search |
| GET | /discovery/v2/classifications/genres/{id} | Get Genre Details |
| GET | /discovery/v2/classifications/segments/{id} | Get Segment Details |
| GET | /discovery/v2/classifications/subgenres/{id} | Get Sub-Genre Details |
| GET | /discovery/v2/classifications/{id} | Get Classification Details |
| GET | /discovery/v2/events | Event Search |
| GET | /discovery/v2/events/{id} | Get Event Details |
| GET | /discovery/v2/events/{id}/images | Get Event Images |
| GET | /discovery/v2/suggest | Find Suggest |
| GET | /discovery/v2/venues | Venue Search |
| GET | /discovery/v2/venues/{id} | Get Venue Details |

## Enhanced Skill Content
## Question Mapping

- "What events are happening in New York this weekend?" -> GET /discovery/v2/events
- "Find concerts near me" -> GET /discovery/v2/events (with latlong, radius, segmentName)
- "Get details for a specific event" -> GET /discovery/v2/events/{id}
- "What images are available for this event?" -> GET /discovery/v2/events/{id}/images
- "Search for Taylor Swift events" -> GET /discovery/v2/events (with keyword or attractionId)
- "Look up an attraction by name" -> GET /discovery/v2/attractions (with keyword)
- "What venues are in Los Angeles?" -> GET /discovery/v2/venues (with keyword or stateCode/latlong)
- "Get venue details and address" -> GET /discovery/v2/venues/{id}
- "What genres and segments exist?" -> GET /discovery/v2/classifications
- "Look up a specific genre" -> GET /discovery/v2/classifications/genres/{id}
- "Find all sports events in a market" -> GET /discovery/v2/events (with segmentName, marketId)
- "What events go on sale soon?" -> GET /discovery/v2/events (with onsaleStartDateTime/onsaleEndDateTime)
- "Autocomplete an event or venue search" -> GET /discovery/v2/suggest
- "List attractions in a classification" -> GET /discovery/v2/attractions (with classificationName or classificationId)
- "What subgenres belong to a genre?" -> GET /discovery/v2/classifications/subgenres/{id}

## Response Tips

- **Events/Attractions/Venues lists**: Results are in `_embedded` under a keyed array (e.g., `_embedded.events`). Always check `page.totalElements` and `page.totalPages` for pagination; use `page` and `size` params to navigate.
- **Single resource (by ID)**: Returns the object directly, no `_embedded` wrapper. Missing IDs return 404 with a `fault` or `errors` array.
- **Classifications**: Hierarchical -- segments contain genres, genres contain subgenres. Traverse nested arrays accordingly.
- **Suggest**: Returns grouped suggestions across events, attractions, and venues in separate arrays. Results are lighter-weight than full search.
- **Images**: Returns a flat array of image objects with varying aspect ratios and sizes. Filter by `ratio` and `width` to pick the best fit.

## Anomaly Flags

- **Rate limit (429)**: The Discovery API enforces strict per-key rate limits (typically 5 req/sec, 5000/day). Surface 429 responses immediately and suggest backing off or caching.
- **Empty `_embedded`**: When a list query returns 200 but no `_embedded` key, the result set is empty. Flag this explicitly rather than silently returning nothing.
- **TBA/TBD events**: Events with `dates.status.code` of "TBA" or "TBD" lack confirmed dates/times. Warn users when results include unconfirmed events, especially if `includeTBA`/`includeTBD` was set.
- **`includeTest: yes`**: If set, test events pollute results. Flag when test data is present and suggest filtering it out for production use.
- **Pagination ceiling**: The API caps results at page * size <= 1000. If `page.totalElements` exceeds this, warn that not all results are retrievable via pagination alone -- suggest narrowing filters.
- **Deprecated/moved attractions**: Attractions may have a `type` of "redirect". Surface these so users follow the canonical ID.

## Playbook

### 1. Find upcoming events for an artist in a city

1. Search attractions: `GET /discovery/v2/attractions?keyword=<artist_name>`
2. Extract the `attractionId` from the best match in `_embedded.attractions`
3. Search events: `GET /discovery/v2/events?attractionId=<id>&city=<city>&startDateTime=<now_iso>&sort=date,asc`
4. Page through results using `page` param if `page.totalPages > 1`
5. For each event, use `GET /discovery/v2/events/{id}` for full details (pricing, seat maps)

### 2. Browse events by genre near a location

1. List classifications: `GET /discovery/v2/classifications` to find the segment and genre IDs
2. Optionally drill into a genre: `GET /discovery/v2/classifications/genres/{id}`
3. Search events: `GET /discovery/v2/events?classificationId=<genre_id>&latlong=<lat,long>&radius=50&unit=miles&sort=date,asc`
4. Present results grouped by date from `dates.start.localDate`

### 3. Get venue info and its upcoming events

1. Search venues: `GET /discovery/v2/venues?keyword=<venue_name>&stateCode=<state>`
2. Pick the matching venue and note its `id`
3. Get full venue details: `GET /discovery/v2/venues/{id}` (address, parking, accessibility)
4. Find events at that venue: `GET /discovery/v2/events?venueId=<id>&sort=date,asc`

### 4. Build an autocomplete search experience

1. As user types, call `GET /discovery/v2/suggest?keyword=<partial>&size=5&countryCode=US`
2. Display grouped results from the response (events, attractions, venues)
3. When user selects a suggestion, fetch the full resource by ID using the appropriate detail endpoint
4. Use `includeFuzzy=yes` to improve results for misspelled queries

### 5. Monitor on-sale windows for events

1. Search for upcoming on-sale events: `GET /discovery/v2/events?onsaleOnAfterStartDate=<today>&sort=onSaleStartDate,asc`
2. Filter results where `sales.public.startDateTime` is in the future
3. For each event of interest, fetch images: `GET /discovery/v2/events/{id}/images`
4. Set up periodic polling with `onsaleStartDateTime` and `onsaleEndDateTime` to catch new on-sale windows
5. Flag events where `sales.public.startTBD` is true -- these need rechecking


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
