---
name: college-football-data-api
description: "College Football Data API skill. Use when working with College Football Data for wepa, teams, roster. Covers 60 endpoints."
version: 1.0.0
generator: lapsh
---

# College Football Data API
API version: 5.13.2

## Auth
Bearer bearer

## Base URL
https://api.collegefootballdata.com/

## Setup
1. Set Authorization header with your Bearer token
2. GET /wepa/team/season -- verify access

## Endpoints

60 endpoints across 25 groups. See references/api-spec.lap for full details.

### wepa
| Method | Path | Description |
|--------|------|-------------|
| GET | /wepa/team/season | Retrieve opponent-adjusted team season statistics |
| GET | /wepa/players/passing | Retrieve opponent-adjusted player passing statistics |
| GET | /wepa/players/rushing | Retrieve opponent-adjusted player rushing statistics |
| GET | /wepa/players/kicking | Retrieve Points Added Above Replacement (PAAR) ratings for kickers |

### teams
| Method | Path | Description |
|--------|------|-------------|
| GET | /teams | Retrieves team information |
| GET | /teams/fbs | Retrieves information on teams playing in the highest division of CFB |
| GET | /teams/matchup | Retrieves historical matchup details for two given teams |
| GET | /teams/ats | Retrieves against-the-spread (ATS) summary by team |

### roster
| Method | Path | Description |
|--------|------|-------------|
| GET | /roster | Retrieves historical roster data |

### conferences
| Method | Path | Description |
|--------|------|-------------|
| GET | /conferences | Retrieves list of conferences |

### talent
| Method | Path | Description |
|--------|------|-------------|
| GET | /talent | Retrieve 247 Team Talent Composite for a given year |

### venues
| Method | Path | Description |
|--------|------|-------------|
| GET | /venues | Retrieve list of venues |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats/player/season | Retrieves aggregated player statistics for a given season |
| GET | /stats/season | Retrieves aggregated team season statistics |
| GET | /stats/categories | Gets team statistical categories |
| GET | /stats/season/advanced | Retrieves advanced season statistics for teams |
| GET | /stats/game/advanced | Retrieves advanced statistics aggregated by game |
| GET | /stats/game/havoc | Retrieves havoc statistics aggregated by game |

### recruiting
| Method | Path | Description |
|--------|------|-------------|
| GET | /recruiting/players | Retrieves player recruiting rankings |
| GET | /recruiting/teams | Retrieves team recruiting rankings |
| GET | /recruiting/groups | Retrieves aggregated recruiting statistics by team and position grouping |

### ratings
| Method | Path | Description |
|--------|------|-------------|
| GET | /ratings/sp | Retrieves SP+ ratings for a given year or school |
| GET | /ratings/sp/conferences | Retrieves aggregated historical conference SP+ data |
| GET | /ratings/srs | Retrieves historical SRS for a year or team |
| GET | /ratings/elo | Retrieves historical Elo ratings |
| GET | /ratings/fpi | Retrieves historical Football Power Index (FPI) ratings |

### rankings
| Method | Path | Description |
|--------|------|-------------|
| GET | /rankings | Retrieves historical poll data |

### plays
| Method | Path | Description |
|--------|------|-------------|
| GET | /plays | Retrieves historical play data |
| GET | /plays/types | Retrieves available play types |
| GET | /plays/stats | Retrieve player-play associations (limit 2000) |
| GET | /plays/stats/types | Retrieves available play stat types |

### player
| Method | Path | Description |
|--------|------|-------------|
| GET | /player/search | Search for players (lists top 100 results) |
| GET | /player/usage | Retrieves player usage data for a given season |
| GET | /player/returning | Retrieves returning production data. Either a year or team filter must be specified. |
| GET | /player/portal | Retrieves transfer portal data for a given year |

### ppa
| Method | Path | Description |
|--------|------|-------------|
| GET | /ppa/predicted | Query Predicted Points values by down and distance |
| GET | /ppa/teams | Retrieves historical team PPA metrics by season |
| GET | /ppa/games | Retrieves historical team PPA metrics by game |
| GET | /ppa/players/games | Queries player PPA statistics by game |
| GET | /ppa/players/season | Queries player PPA statistics by season |

### metrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics/wp | Query play win probabilities by game |
| GET | /metrics/wp/pregame | Queries pregame win probabilities |
| GET | /metrics/fg/ep | Queries field goal expected points values |

### live
| Method | Path | Description |
|--------|------|-------------|
| GET | /live/plays | Queries live play-by-play data and advanced stats |

### lines
| Method | Path | Description |
|--------|------|-------------|
| GET | /lines | Retrieves historical betting data |

### info
| Method | Path | Description |
|--------|------|-------------|
| GET | /info | Retrieves information about the user, including their Patreon level and remaining API calls. |

### games
| Method | Path | Description |
|--------|------|-------------|
| GET | /games | Retrieves historical game data |
| GET | /games/teams | Retrieves team box score statistics |
| GET | /games/players | Retrieves player box score statistics |
| GET | /games/media | Retrieves media information for games |
| GET | /games/weather | Retrieve historical and future weather data (Patreon only) |

### records
| Method | Path | Description |
|--------|------|-------------|
| GET | /records | Retrieves historical team records |

### calendar
| Method | Path | Description |
|--------|------|-------------|
| GET | /calendar | Retrieves calendar information |

### scoreboard
| Method | Path | Description |
|--------|------|-------------|
| GET | /scoreboard | Retrieves live scoreboard data |

### drives
| Method | Path | Description |
|--------|------|-------------|
| GET | /drives | Retrieves historical drive data |

### draft
| Method | Path | Description |
|--------|------|-------------|
| GET | /draft/teams | Retrieves list of NFL teams |
| GET | /draft/positions | Retrieves list of player position categories for the NFL Draft |
| GET | /draft/picks | Retrieve historical NFL draft data |

### coaches
| Method | Path | Description |
|--------|------|-------------|
| GET | /coaches | Retrieves historical head coach information and records |

### game
| Method | Path | Description |
|--------|------|-------------|
| GET | /game/box/advanced | Retrieves an advanced box score for a game |

## Enhanced Skill Content
## Question Mapping

- "What's the all-time record between Alabama and Auburn?" -> GET /teams/matchup
- "Show me the current scoreboard for today's games" -> GET /scoreboard
- "Who are the top recruiting prospects from Texas?" -> GET /recruiting/players
- "What are the SP+ ratings for Ohio State this year?" -> GET /ratings/sp
- "Find me a player named Travis Hunter" -> GET /player/search
- "What was the win probability during game 401520101?" -> GET /metrics/wp
- "Show me live play-by-play for the current game" -> GET /live/plays
- "What are the betting lines for Week 5?" -> GET /lines
- "How did Clemson perform in advanced stats last season?" -> GET /stats/season/advanced
- "Who entered the transfer portal this year?" -> GET /player/portal
- "What's the expected points value on 3rd and 7?" -> GET /ppa/predicted
- "Show me the AP rankings for Week 8" -> GET /rankings
- "What NFL draft picks came from the SEC?" -> GET /draft/picks
- "What's the weather forecast for Saturday's games?" -> GET /games/weather
- "Show me all drives from the Michigan vs Ohio State game" -> GET /drives

## Response Tips

- **Teams/Conferences/Venues**: Flat arrays of objects; no pagination. Cache these reference lists locally since they rarely change.
- **Stats/Ratings/Rankings**: Nested category objects are common. Stats endpoints group by `category` field; always check `statType` or `category` to find the metric you need.
- **Games/Plays/Drives**: Large result sets filtered by required `year` + `week`. If responses are empty, verify `seasonType` (defaults to "regular" -- use "postseason" for bowl games).
- **Recruiting**: Results vary by `classification` (HighSchool, JUCO, PrepSchool). Omitting it returns all types mixed together.
- **Player endpoints**: `player/search` returns basic info only; cross-reference with `stats/player/season` or `player/usage` for performance data using the returned player ID.
- **Live/Scoreboard**: Responses include nullable fields (`period`, `down`, `distance`) when games are in intermission or haven't started. Check `status` before reading play state.
- **Matchup**: The `games` array inside the response contains per-game detail; `team1Wins`/`team2Wins`/`ties` are the rollup totals.
- **Advanced box score** (`game/box/advanced`): Deeply nested -- `teams` contains keyed arrays (ppa, rushing, successRates, etc.) and `players` has separate ppa and usage sub-arrays.

## Anomaly Flags

- **Empty responses on valid queries**: Surface when a year/week combination returns no data -- likely the season hasn't started or the week number is wrong. Suggest checking `/calendar` for valid weeks.
- **Nullable play state fields**: When `/live/plays` returns `down: null` or `distance: null`, flag that the game may be in halftime, a timeout, or not yet started.
- **seasonType mismatch**: If a user asks about a bowl game or playoff and gets no results, proactively suggest switching `seasonType` from "regular" to "postseason".
- **Stale scoreboard data**: `/scoreboard` reflects a point-in-time snapshot. Flag if a user appears to be polling for live updates -- suggest `/live/plays` with a specific `gameId` instead.
- **Missing WEPA data**: WEPA endpoints may return empty for non-FBS teams or older seasons. Surface this when results are unexpectedly empty and suggest checking `/teams/fbs` to confirm FBS status.
- **Bearer auth failures**: All endpoints require authentication. If a 401 or 403 is returned, flag immediately and confirm the Bearer token is set before retrying other calls.
- **Large play-by-play responses**: `/plays` for a full week can return thousands of records. Flag when a broad query (no team filter) is issued and suggest narrowing by team, offense, or defense.

## Playbook

### Compare Two Rival Teams Historically

1. Call `GET /teams/matchup?team1=Alabama&team2=Auburn` to get the all-time series record, win counts, and per-game results.
2. Call `GET /ratings/sp?year=2025&team=Alabama` and `GET /ratings/sp?year=2025&team=Auburn` to compare current SP+ ratings.
3. Call `GET /stats/season/advanced?year=2025&team=Alabama` and the same for Auburn to compare advanced offensive and defensive metrics.
4. Optionally call `GET /teams/ats?year=2025&team=Alabama` and for Auburn to see against-the-spread records.
5. Summarize head-to-head record, current ratings gap, and statistical advantages.

### Scout a Recruit or Transfer Portal Player

1. Call `GET /player/search?searchTerm=<name>` to find the player and get their ID.
2. If they're a recruit, call `GET /recruiting/players?year=<year>&team=<team>` to get their recruiting rating and ranking.
3. If they're a transfer, call `GET /player/portal?year=<year>` and filter for the player to see origin/destination.
4. Call `GET /stats/player/season?year=<year>&team=<team>` to pull their on-field production stats.
5. Call `GET /player/usage?year=<year>&playerId=<id>` to see snap counts and usage rates by play type.

### Analyze a Specific Game in Depth

1. Call `GET /games?year=<year>&week=<week>&team=<team>` to find the game and get its `id`.
2. Call `GET /game/box/advanced?id=<gameId>` for the full advanced box score including PPA, success rates, havoc, and explosiveness.
3. Call `GET /drives?year=<year>&week=<week>&team=<team>` to review drive-level outcomes.
4. Call `GET /plays?year=<year>&week=<week>&team=<team>` for full play-by-play detail.
5. Call `GET /metrics/wp?gameId=<gameId>` to chart win probability swings throughout the game.

### Build a Weekly Preview with Betting Context

1. Call `GET /calendar?year=<year>` to confirm the current week number and date range.
2. Call `GET /games?year=<year>&week=<week>` to get all matchups for the week.
3. Call `GET /lines?year=<year>&week=<week>` to pull spread, over/under, and moneyline from available providers.
4. Call `GET /metrics/wp/pregame?year=<year>&week=<week>` to get model-based pregame win probabilities.
5. Call `GET /games/weather?year=<year>&week=<week>` to check for weather factors that could affect totals or game plans.

### Evaluate Team Recruiting Trajectory

1. Call `GET /recruiting/teams?year=<year>&team=<team>` for the current class ranking and point total.
2. Call `GET /recruiting/groups?team=<team>&startYear=<start>&endYear=<end>` to see multi-year recruiting trends by position group.
3. Call `GET /talent?year=<year>` to see where the team ranks in overall composite talent.
4. Call `GET /player/returning?year=<year>&team=<team>` to assess how much production is coming back.
5. Cross-reference with `GET /ratings/sp?year=<year>&team=<team>` to see if recruiting talent is translating to on-field performance.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
