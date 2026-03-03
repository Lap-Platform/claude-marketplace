---
name: aggregators-api-service
description: "Aggregators API Service API skill. Use when working with Aggregators API Service for api, stats, partners. Covers 28 endpoints."
version: 1.0.0
generator: lapsh
---

# Aggregators API Service
API version: 0.73-26f7c03

## Auth
ApiKey x-zeno-api-key in header | Bearer basic

## Base URL
https://api.zeno.fm

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/v2/stations/list -- verify access
3. POST /stats/mounts/{mount}/auth-cache/reload -- create first reload

## Endpoints

28 endpoints across 3 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v2/podcasts/{podcastKey} | Get podcast |
| PUT | /api/v2/podcasts/{podcastKey} | Update podcast |
| DELETE | /api/v2/podcasts/{podcastKey} | Delete podcast |
| GET | /api/v2/podcasts/{podcastKey}/episodes/{episodeKey} | Get podcast episode |
| PUT | /api/v2/podcasts/{podcastKey}/episodes/{episodeKey} | Update podcast episode |
| DELETE | /api/v2/podcasts/{podcastKey}/episodes/{episodeKey} | Delete podcast episode |
| POST | /api/v2/stations/search | Search stations |
| POST | /api/v2/stations/listener/location | Get top stations by listener location |
| POST | /api/v2/podcasts/{podcastKey}/episodes/create | Create podcast episode |
| POST | /api/v2/podcasts/search | Search podcasts |
| POST | /api/v2/podcasts/create | Create podcast |
| GET | /api/v2/stations/{stationKey} | Get station |
| GET | /api/v2/stations/list | List stations |
| GET | /api/v2/stations/languages | Get the list of Languages that can be used to filter stations in the search stations request |
| GET | /api/v2/stations/genres | Get the list of Genres that can be used to filter stations in the search stations request |
| GET | /api/v2/stations/countries | Get the list of Countries that can be used to filter stations in the search stations request |
| GET | /api/v2/stations/browse | Browse all stations |
| GET | /api/v2/podcasts/{podcastKey}/episodes | Get podcast episodes |
| GET | /api/v2/podcasts/languages | Get the list of Languages that can be used to filter podcasts in the search podcasts request |
| GET | /api/v2/podcasts/countries | Get the list of Countries that can be used to filter podcasts in the search podcasts request |
| GET | /api/v2/podcasts/categories | Get the list of Categories that can be used to filter podcasts in the search podcasts request |

### stats
| Method | Path | Description |
|--------|------|-------------|
| POST | /stats/mounts/{mount}/auth-cache/reload | Retrieve total numer of live stats for a specific mount |
| POST | /stats/mounts/{mount}/auth-cache/reload/all | Retrieve total numer of live stats for a specific mount |
| GET | /stats/mounts/{mount}/live/total | Retrieve total numer of live stats for a specific mount |

### partners
| Method | Path | Description |
|--------|------|-------------|
| POST | /partners/streams | Get the partner information for a list of streams. |
| GET | /partners/{partnerId}/ads/stats | Retrieve partner stats |
| GET | /partners/streams/{streamId} | Get the stream partner information. |
| GET | /partners/streams/{streamId}/tracks | Get the stream partner information. |

## Enhanced Skill Content
## Question Mapping

- "How do I search for radio stations by genre or country?" -> POST /api/v2/stations/search
- "What genres are available on Zeno?" -> GET /api/v2/stations/genres
- "Show me all available station languages" -> GET /api/v2/stations/languages
- "List stations with pagination" -> GET /api/v2/stations/list
- "Browse all stations with an offset" -> GET /api/v2/stations/browse
- "Get details for a specific station" -> GET /api/v2/stations/{stationKey}
- "Search for podcasts by category or language" -> POST /api/v2/podcasts/search
- "List episodes of a podcast" -> GET /api/v2/podcasts/{podcastKey}/episodes
- "Create a new podcast and add an episode to it" -> POST /api/v2/podcasts/create then POST /api/v2/podcasts/{podcastKey}/episodes/create
- "Delete a specific episode from a podcast" -> DELETE /api/v2/podcasts/{podcastKey}/episodes/{episodeKey}
- "How many listeners does my station have right now?" -> GET /stats/mounts/{mount}/live/total
- "Get ad performance stats for a partner over a date range" -> GET /partners/{partnerId}/ads/stats
- "What track is currently playing on a partner stream?" -> GET /partners/streams/{streamId} (with currentTrack=True)
- "View track history for a partner stream" -> GET /partners/streams/{streamId}/tracks
- "Force reload the auth cache for a mount point" -> POST /stats/mounts/{mount}/auth-cache/reload

## Response Tips

- **Station/Podcast listing & search**: Results are paginated via `page`/`hitsPerPage` (search) or `offset`/`limit` (browse/episodes). Always check if more pages exist before stopping iteration.
- **Metadata endpoints** (genres, languages, countries, categories): Return flat reference lists. Cache these locally since they change infrequently.
- **Stats endpoints**: `live/total` requires an `Authorization` header separate from the API key. Expect numeric listener counts, not nested objects.
- **Partner endpoints**: Require `X-Auth-Token` or `x-zeno-api-key` in headers (not the standard auth). Ad stats support `DAILY`, `HOURLY`, or `BREAKDOWN` granularity via the `type` param.
- **Mutation endpoints** (PUT, DELETE, POST create): All return 200 on success. No 201/204 distinction -- treat any non-200 as a failure.

## Anomaly Flags

- **Dual auth schemes**: The API uses both `x-zeno-api-key` and `X-Auth-Token` depending on the endpoint group. Flag mismatched auth if a 401/403 is returned.
- **Zero results on search**: If a station or podcast search returns empty, surface whether filters were too restrictive (multiple filters compound).
- **Missing pagination awareness**: If `hitsPerPage` or `limit` equals the result count, warn the user that more results likely exist on subsequent pages.
- **Mount not found on stats**: If `live/total` or `auth-cache/reload` returns an error, flag that the mount identifier may be incorrect or the station may be offline.
- **Date format errors on ad stats**: The `from`/`to` params require date format strings. Surface parsing errors early if the format looks wrong.
- **Episode creation without podcast**: If a user tries to create an episode without a valid `podcastKey`, flag that the podcast must exist first.

## Playbook

### 1. Discover and Filter Radio Stations

1. Call `GET /api/v2/stations/genres` and `GET /api/v2/stations/countries` to get valid filter values.
2. Call `POST /api/v2/stations/search` with desired `filters` (genre, country, language) and `query` text.
3. Set `hitsPerPage` and `page` to paginate through results.
4. Use `minSessions` to exclude low-traffic stations.
5. For a specific result, call `GET /api/v2/stations/{stationKey}` to get full details.

### 2. Create a Podcast and Publish Episodes

1. Call `POST /api/v2/podcasts/create` to create a new podcast. Capture the returned `podcastKey`.
2. Call `POST /api/v2/podcasts/{podcastKey}/episodes/create` to add an episode.
3. Verify by calling `GET /api/v2/podcasts/{podcastKey}/episodes` to confirm the episode appears.
4. Update podcast metadata if needed via `PUT /api/v2/podcasts/{podcastKey}`.

### 3. Monitor Live Listener Stats

1. Identify the station's mount identifier.
2. Call `GET /stats/mounts/{mount}/live/total` with the `Authorization` header.
3. To ensure fresh auth data, call `POST /stats/mounts/{mount}/auth-cache/reload` beforehand if counts seem stale.
4. For bulk refresh across all mounts, use `POST /stats/mounts/{mount}/auth-cache/reload/all`.

### 4. Pull Partner Ad Performance Reports

1. Call `GET /partners/{partnerId}/ads/stats` with `from` and `to` date range and the `x-zeno-api-key` header.
2. Set `type` to `DAILY` for day-by-day breakdown, `HOURLY` for granular analysis, or `BREAKDOWN` for aggregate splits.
3. Paginate with `page` and `size` if the result set is large.
4. Cross-reference with `GET /partners/streams/{streamId}` to correlate ad stats with specific streams.

### 5. Track Current Playback on Partner Streams

1. Call `POST /partners/streams` with `X-Auth-Token` to list available streams. Set `currentTrack=True` to include now-playing info.
2. Pick a stream and call `GET /partners/streams/{streamId}` with `currentTrack=True` for real-time track details.
3. Call `GET /partners/streams/{streamId}/tracks` to retrieve the full track history for that stream.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
