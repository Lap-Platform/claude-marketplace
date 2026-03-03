---
name: frc-events
description: "FRC Events API skill. Use when working with FRC Events for root, {season}. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# FRC Events

## Auth
Basic username:password

## Base URL
https://frc-api.firstinspires.org/v3.0

## Setup
1. Configure auth: Basic username:password
2. GET / -- verify access

## Endpoints

19 endpoints across 2 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | API Index |

### {season}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{season} | Season Summary |
| GET | /{season}/events | Event Listings |
| GET | /{season}/districts | District Listings |
| GET | /{season}/teams | Team Listings |
| GET | /{season}/avatars | Team Avatar Listings |
| GET | /{season}/awards/event/{eventCode} | Event Awards |
| GET | /{season}/awards/list | Awards Listings |
| GET | /{season}/awards/team/{teamNumber} | Team Awards |
| GET | /{season}/awards/eventteam/{eventCode}/{teamNumber} | Event Team Awards |
| GET | /{season}/scores/{eventCode}/{tournamentLevel} | Score Details |
| GET | /{season}/matches/{eventCode} | Event Match Results |
| GET | /{season}/rankings/district/qualPerformanceCalculation | Qual Performance Points |
| GET | /{season}/rankings/district/allianceSelectionCalculation | Alliance Selection Points |
| GET | /{season}/rankings/district/playoffAdvancementCalculation | Playoff Advancement Points |
| GET | /{season}/rankings/{eventCode} | Event Rankings |
| GET | /{season}/rankings/district | District Rankings |
| GET | /{season}/schedule/{eventCode} | Event Schedule |
| GET | /{season}/alliances/{eventCode} | Event Alliances |

## Enhanced Skill Content
## Question Mapping

- "What is the current FRC season?" -> GET /
- "How many teams are competing in 2024?" -> GET /{season}
- "List all events for the 2024 season" -> GET /{season}/events
- "What districts exist in 2024?" -> GET /{season}/districts
- "Show me all teams in the 2024 season" -> GET /{season}/teams
- "Get team avatars for 2024" -> GET /{season}/avatars
- "What awards were given at a specific event?" -> GET /{season}/awards/event/{eventCode}
- "What types of awards exist this season?" -> GET /{season}/awards/list
- "What awards has team 254 won in 2024?" -> GET /{season}/awards/team/{teamNumber}
- "Did team 1678 win any awards at a specific event?" -> GET /{season}/awards/eventteam/{eventCode}/{teamNumber}
- "What are the match scores for quals at an event?" -> GET /{season}/scores/{eventCode}/{tournamentLevel}
- "Show me the match schedule for an event" -> GET /{season}/matches/{eventCode}
- "What are the current rankings at an event?" -> GET /{season}/rankings/{eventCode}
- "Show district rankings for 2024" -> GET /{season}/rankings/district
- "What is the match schedule for an event?" -> GET /{season}/schedule/{eventCode}
- "What are the playoff alliances at an event?" -> GET /{season}/alliances/{eventCode}

## Response Tips

- **Season/root endpoints**: Top-level summary fields (`eventCount`, `teamCount`). Check `frcChampionships` array for championship locations and dates.
- **Teams and avatars**: Paginated -- use `pageCurrent`, `pageTotal`, `teamCountTotal` to iterate. Each page returns `teamCountPage` items.
- **Awards (team/eventteam)**: Returns `{code, message}` on 200 when no results found instead of an empty array -- check for the `code` field before accessing `Awards`.
- **Scores**: Multiple 200 response shapes depending on `tournamentLevel` (qual, playoff, etc.). The `MatchScores` array structure varies by game year.
- **Rankings (district)**: Paginated like teams -- check `pageTotal` and loop with page parameter. Calculation endpoints (qualPerformance, allianceSelection, playoffAdvancement) return raw formula data with no wrapper object.
- **All endpoints**: Support `If-Modified-Since` header for conditional fetching -- a 304 means no changes since your last request. All errors return 500 only (no 4xx granularity).

## Anomaly Flags

- **Pagination truncation**: If `pageCurrent < pageTotal` on teams, avatars, or district rankings, warn that results are incomplete and additional pages must be fetched.
- **Award lookup returning message instead of data**: When `/{season}/awards/team/{teamNumber}` returns `{code, message}` instead of `{Awards}`, surface that the team or season may be invalid rather than silently returning empty results.
- **304 Not Modified**: If using `If-Modified-Since` and receiving 304, inform the user that data has not changed rather than treating it as an error.
- **Score schema variability**: The `MatchScores` structure changes per season and tournament level. Flag when fields don't match expected patterns for the requested year.
- **Season bounds**: The root `/` endpoint returns `maxSeason` -- flag if the user requests a season beyond this value.
- **500 errors with no detail**: The API returns only 500 for all server errors. Recommend retrying once before reporting failure, and note the lack of error detail.

## Playbook

### 1. Get Full Team List for a Season

1. Call `GET /{season}/teams` to get the first page
2. Read `pageTotal` from the response
3. If `pageTotal > 1`, loop from page 2 to `pageTotal`, appending each page's `teams` array
4. Use `teamCountTotal` to verify you collected all teams

### 2. Build a Complete Event Summary

1. Call `GET /{season}/events` to list all events and find the target `eventCode`
2. Call `GET /{season}/schedule/{eventCode}` for the match schedule
3. Call `GET /{season}/rankings/{eventCode}` for current standings
4. Call `GET /{season}/alliances/{eventCode}` for playoff alliance selections
5. Call `GET /{season}/awards/event/{eventCode}` for awards given

### 3. Track a Specific Team Across a Season

1. Call `GET /{season}/teams` (paginate) to confirm the team exists and get their info
2. Call `GET /{season}/awards/team/{teamNumber}` for all awards won
3. For each event the team attended, call `GET /{season}/matches/{eventCode}` and filter for that team's matches
4. Call `GET /{season}/rankings/district` (if applicable) to find their district ranking

### 4. Fetch Detailed Match Scores for an Event

1. Call `GET /{season}/matches/{eventCode}` to get the match list and determine tournament levels present
2. Call `GET /{season}/scores/{eventCode}/qual` for qualification match scores
3. Call `GET /{season}/scores/{eventCode}/playoff` for elimination match scores
4. Cross-reference with `GET /{season}/rankings/{eventCode}` to correlate scores with final standings

### 5. Monitor Data Freshness with Conditional Requests

1. Make initial requests to desired endpoints, noting the response `Date` header
2. On subsequent calls, pass `If-Modified-Since` with the stored date
3. If 304 is returned, use cached data -- no changes occurred
4. If 200 is returned, update your cache and store the new date
5. This is especially useful for rankings and schedule endpoints during live events


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
