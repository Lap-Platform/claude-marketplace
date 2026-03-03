---
name: the-blue-alliance-api-v3
description: "The Blue Alliance API v3 API skill. Use when working with The Blue Alliance API v3 for district, districts, event. Covers 80 endpoints."
version: 1.0.0
generator: lapsh
---

# The Blue Alliance API v3
API version: 3.12.0

## Auth
ApiKey X-TBA-Auth-Key in header

## Base URL
https://www.thebluealliance.com/api/v3

## Setup
1. Set your API key in the appropriate header
2. GET /search_index -- verify access

## Endpoints

80 endpoints across 11 groups. See references/api-spec.lap for full details.

### district
| Method | Path | Description |
|--------|------|-------------|
| GET | /district/{district_abbreviation}/dcmp_history | Gets a list of DCMP events and awards for the given district abbreviation. |
| GET | /district/{district_abbreviation}/history | Gets a list of District objects with the given district abbreviation. This accounts for district abbreviation changes, such as MAR to FMA. |
| GET | /district/{district_abbreviation}/insights | Gets insights for a given district. |
| GET | /district/{district_key}/advancement | Gets a list of advancement information per team in a district. |
| GET | /district/{district_key}/awards | Gets a list of awards in the given district. |
| GET | /district/{district_key}/events | Gets a list of events in the given district. |
| GET | /district/{district_key}/events/keys | Gets a list of event keys for events in the given district. |
| GET | /district/{district_key}/events/simple | Gets a short-form list of events in the given district. |
| GET | /district/{district_key}/rankings | Gets a list of team district rankings for the given district. |
| GET | /district/{district_key}/teams | Gets a list of `Team` objects that competed in events in the given district. |
| GET | /district/{district_key}/teams/keys | Gets a list of `Team` objects that competed in events in the given district. |
| GET | /district/{district_key}/teams/simple | Gets a short-form list of `Team` objects that competed in events in the given district. |

### districts
| Method | Path | Description |
|--------|------|-------------|
| GET | /districts/{year} | Gets a list of districts and their corresponding district key, for the given year. |

### event
| Method | Path | Description |
|--------|------|-------------|
| GET | /event/{event_key} | Gets an Event. |
| GET | /event/{event_key}/advancement_points | Depending on the type of event (district/regional), this will return either district points or regional CMP points |
| GET | /event/{event_key}/alliances | Gets a list of Elimination Alliances for the given Event. |
| GET | /event/{event_key}/awards | Gets a list of awards from the given event. |
| GET | /event/{event_key}/coprs | Gets a set of Event Component OPRs for the given Event. |
| GET | /event/{event_key}/district_points | Gets a list of district points for the Event. These are always calculated, regardless of event type, and may/may not be actually useful. |
| GET | /event/{event_key}/insights | Gets a set of Event-specific insights for the given Event. |
| GET | /event/{event_key}/matches | Gets a list of matches for the given event. |
| GET | /event/{event_key}/matches/keys | Gets a list of match keys for the given event. |
| GET | /event/{event_key}/matches/simple | Gets a short-form list of matches for the given event. |
| GET | /event/{event_key}/matches/timeseries | Gets an array of Match Keys for the given event key that have timeseries data. Returns an empty array if no matches have timeseries data. |
| GET | /event/{event_key}/oprs | Gets a set of Event OPRs (including OPR, DPR, and CCWM) for the given Event. |
| GET | /event/{event_key}/predictions | Gets information on TBA-generated predictions for the given Event. Contains year-specific information. *WARNING* This endpoint is currently under development and may change at any time. |
| GET | /event/{event_key}/rankings | Gets a list of team rankings for the Event. |
| GET | /event/{event_key}/regional_champs_pool_points | For 2025+ Regional events, this will return points towards the Championship qualification pool. |
| GET | /event/{event_key}/simple | Gets a short-form Event. |
| GET | /event/{event_key}/team_media | Gets a list of media objects that correspond to teams at this event. |
| GET | /event/{event_key}/teams | Gets a list of `Team` objects that competed in the given event. |
| GET | /event/{event_key}/teams/keys | Gets a list of `Team` keys that competed in the given event. |
| GET | /event/{event_key}/teams/simple | Gets a short-form list of `Team` objects that competed in the given event. |
| GET | /event/{event_key}/teams/statuses | Gets a key-value list of the event statuses for teams competing at the given event. |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events/{year} | Gets a list of events in the given year. |
| GET | /events/{year}/keys | Gets a list of event keys in the given year. |
| GET | /events/{year}/simple | Gets a short-form list of events in the given year. |

### insights
| Method | Path | Description |
|--------|------|-------------|
| GET | /insights/leaderboards/{year} | Gets a list of `LeaderboardInsight` objects from a specific year. Use year=0 for overall. |
| GET | /insights/notables/{year} | Gets a list of `NotablesInsight` objects from a specific year. Use year=0 for overall. |

### match
| Method | Path | Description |
|--------|------|-------------|
| GET | /match/{match_key} | Gets a `Match` object for the given match key. |
| GET | /match/{match_key}/simple | Gets a short-form `Match` object for the given match key. |
| GET | /match/{match_key}/timeseries | Gets an array of game-specific Match Timeseries objects for the given match key or an empty array if not available. |
| GET | /match/{match_key}/zebra_motionworks | Gets Zebra MotionWorks data for a Match for the given match key. |

### regional_advancement
| Method | Path | Description |
|--------|------|-------------|
| GET | /regional_advancement/{year} | Gets information about per-team advancement to the FIRST Championship. |
| GET | /regional_advancement/{year}/rankings | Gets the team rankings in the regional pool for a specific year. |

### search_index
| Method | Path | Description |
|--------|------|-------------|
| GET | /search_index | Gets a large blob of data that is used on the frontend for searching. May change without notice. |

### status
| Method | Path | Description |
|--------|------|-------------|
| GET | /status | Returns API status, and TBA status information. |

### team
| Method | Path | Description |
|--------|------|-------------|
| GET | /team/{team_key} | Gets a `Team` object for the team referenced by the given key. |
| GET | /team/{team_key}/awards | Gets a list of awards the given team has won. |
| GET | /team/{team_key}/awards/{year} | Gets a list of awards the given team has won in a given year. |
| GET | /team/{team_key}/districts | Gets an array of districts representing each year the team was in a district. Will return an empty array if the team was never in a district. |
| GET | /team/{team_key}/event/{event_key}/awards | Gets a list of awards the given team won at the given event. |
| GET | /team/{team_key}/event/{event_key}/matches | Gets a list of matches for the given team and event. |
| GET | /team/{team_key}/event/{event_key}/matches/keys | Gets a list of match keys for matches for the given team and event. |
| GET | /team/{team_key}/event/{event_key}/matches/simple | Gets a short-form list of matches for the given team and event. |
| GET | /team/{team_key}/event/{event_key}/status | Gets the competition rank and status of the team at the given event. |
| GET | /team/{team_key}/events | Gets a list of all events this team has competed at. |
| GET | /team/{team_key}/events/keys | Gets a list of the event keys for all events this team has competed at. |
| GET | /team/{team_key}/events/simple | Gets a short-form list of all events this team has competed at. |
| GET | /team/{team_key}/events/{year} | Gets a list of events this team has competed at in the given year. |
| GET | /team/{team_key}/events/{year}/keys | Gets a list of the event keys for events this team has competed at in the given year. |
| GET | /team/{team_key}/events/{year}/simple | Gets a short-form list of events this team has competed at in the given year. |
| GET | /team/{team_key}/events/{year}/statuses | Gets a key-value list of the event statuses for events this team has competed at in the given year. |
| GET | /team/{team_key}/history | Gets the history for the team referenced by the given key, including their events and awards. |
| GET | /team/{team_key}/matches/{year} | Gets a list of matches for the given team and year. |
| GET | /team/{team_key}/matches/{year}/keys | Gets a list of match keys for matches for the given team and year. |
| GET | /team/{team_key}/matches/{year}/simple | Gets a short-form list of matches for the given team and year. |
| GET | /team/{team_key}/media/tag/{media_tag} | Gets a list of Media (videos / pictures) for the given team and tag. |
| GET | /team/{team_key}/media/tag/{media_tag}/{year} | Gets a list of Media (videos / pictures) for the given team, tag and year. |
| GET | /team/{team_key}/media/{year} | Gets a list of Media (videos / pictures) for the given team and year. |
| GET | /team/{team_key}/robots | Gets a list of year and robot name pairs for each year that a robot name was provided. Will return an empty array if the team has never named a robot. |
| GET | /team/{team_key}/simple | Gets a `Team_Simple` object for the team referenced by the given key. |
| GET | /team/{team_key}/social_media | Gets a list of Media (social media) for the given team. |
| GET | /team/{team_key}/years_participated | Gets a list of years in which the team participated in at least one competition. |

### teams
| Method | Path | Description |
|--------|------|-------------|
| GET | /teams/{page_num} | Gets a list of `Team` objects, paginated in groups of 500. |
| GET | /teams/{page_num}/keys | Gets a list of Team keys, paginated in groups of 500. (Note, each page will not have 500 teams, but will include the teams within that range of 500.) |
| GET | /teams/{page_num}/simple | Gets a list of short form `Team_Simple` objects, paginated in groups of 500. |
| GET | /teams/{year}/{page_num} | Gets a list of `Team` objects that competed in the given year, paginated in groups of 500. |
| GET | /teams/{year}/{page_num}/keys | Gets a list Team Keys that competed in the given year, paginated in groups of 500. |
| GET | /teams/{year}/{page_num}/simple | Gets a list of short form `Team_Simple` objects that competed in the given year, paginated in groups of 500. |

## Enhanced Skill Content
## Question Mapping

- "What team is number 254?" -> GET /team/{team_key}
- "What events are happening in 2024?" -> GET /events/{year}
- "Show me the rankings for this event" -> GET /event/{event_key}/rankings
- "Who won this match?" -> GET /match/{match_key}
- "What teams are at this event?" -> GET /event/{event_key}/teams
- "What districts exist this year?" -> GET /districts/{year}
- "What awards has this team won?" -> GET /team/{team_key}/awards
- "How did this team do at a specific event?" -> GET /team/{team_key}/event/{event_key}/status
- "What matches did this team play in 2024?" -> GET /team/{team_key}/matches/{year}
- "What are the OPRs for this event?" -> GET /event/{event_key}/oprs
- "Is the TBA datafeed working?" -> GET /status
- "What are the district rankings?" -> GET /district/{district_key}/rankings
- "Show me the alliances for this event" -> GET /event/{event_key}/alliances
- "What robot did this team build each year?" -> GET /team/{team_key}/robots
- "Find a team or event by name" -> GET /search_index

## Response Tips

- **Team/Event detail endpoints**: Full objects include nullable location fields (`city`, `state_prov`, `country`, `lat`, `lng`) -- always null-check before displaying addresses or mapping.
- **`/simple` variants**: Return stripped-down objects (no location details, no webcasts). Use these for listing/search to reduce payload; fall back to full endpoints only when detail is needed.
- **`/keys` variants**: Return flat string arrays (e.g., `["2024casj"]`), not objects. Ideal for existence checks or feeding into batch lookups.
- **Match objects**: `alliances` is always nested two levels deep (`alliances.red.team_keys`, `alliances.blue.score`). `score_breakdown` is year-specific and its schema changes every season.
- **Rankings**: Wrapped in a `rankings` array inside an object that also carries `sort_order_info` and `extra_stats_info` -- iterate `.rankings`, not the top-level response.
- **Teams pagination**: `/teams/{page_num}` is 0-indexed, 500 teams per page. Use `GET /status` -> `max_team_page` to know when to stop.
- **304 Not Modified**: All endpoints support `If-None-Match` (ETag caching). A 304 means data has not changed -- reuse your cached copy. Always send `If-None-Match` on repeated calls.
- **Error responses**: 401 means missing or invalid `X-TBA-Auth-Key`. 404 means the resource key does not exist (check key format: `frc254`, `2024casj`, `2024casj_qm1`).

## Anomaly Flags

- **`is_datafeed_down: true`** from `GET /status` -- surface immediately; all data may be stale or incomplete during outages.
- **`down_events` non-empty** from `GET /status` -- warn that specific event data may be unreliable.
- **401 on any call** -- the API key is missing, expired, or malformed. Prompt user to verify `X-TBA-Auth-Key` before retrying.
- **304 on every call in a batch** -- data has not updated since last fetch. Note this to the user rather than silently returning stale results.
- **`score_breakdown: null` on a match** -- the match has not been played yet or score data is unavailable. Flag if the user expects results.
- **`winning_alliance: ""`** on a match -- indicates a tie or unplayed match; do not assume red/blue won.
- **`playoff_type` changes across events** -- different events may use different playoff formats (bracket vs round-robin). Surface when comparing cross-event playoff data.
- **Zebra MotionWorks returning 404** -- robot tracking data is only available for select events. Flag that this is expected, not an error.
- **Teams page returning empty array** -- you have passed `max_team_page`. Stop paginating.

## Playbook

### 1. Get a Full Team Profile

1. Call `GET /team/frc{number}` (e.g., `frc254`) to get team details, location, and rookie year.
2. Call `GET /team/frc{number}/years_participated` to see active seasons.
3. Call `GET /team/frc{number}/social_media` for website and social links.
4. Call `GET /team/frc{number}/robots` for robot names and photos by year.
5. Call `GET /team/frc{number}/awards` for a lifetime awards list.

### 2. Analyze a Team's Performance at an Event

1. Call `GET /team/{team_key}/event/{event_key}/status` to get qualification ranking, alliance pick, and playoff result.
2. Call `GET /team/{team_key}/event/{event_key}/matches` to get all match details.
3. Call `GET /event/{event_key}/oprs` and look up the team key in the `oprs`, `dprs`, and `ccwms` maps for offensive/defensive power ratings.
4. Call `GET /team/{team_key}/event/{event_key}/awards` to see any awards earned at that event.

### 3. Scout All Teams at an Upcoming Event

1. Call `GET /event/{event_key}/teams/simple` to get the team list with basic info.
2. For each team, call `GET /team/{team_key}/events/{year}` to see what other events they have attended this season.
3. Call `GET /event/{event_key}/rankings` once matches begin to track live qualification rankings.
4. Call `GET /event/{event_key}/oprs` as matches accumulate for calculated stats.

### 4. Track a Live Event

1. Call `GET /status` to confirm the datafeed is up and the event is not in `down_events`.
2. Call `GET /event/{event_key}/matches/simple` to get the match schedule with predicted times.
3. Poll `GET /event/{event_key}/matches` with `If-None-Match` to detect new results (304 = no update).
4. Call `GET /event/{event_key}/rankings` after each qual round to get updated standings.
5. Call `GET /event/{event_key}/alliances` once alliance selection begins.
6. Call `GET /event/{event_key}/predictions` for model-generated win probabilities.

### 5. Explore District Season Standings

1. Call `GET /districts/{year}` to list all active districts and their keys.
2. Call `GET /district/{district_key}/rankings` to see cumulative point standings.
3. Call `GET /district/{district_key}/events` to see all events in that district.
4. Call `GET /district/{district_key}/advancement` to check which teams qualify for district championship or worlds.
5. Call `GET /district/{district_abbreviation}/insights` for aggregate district statistics.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
