---
name: globalwinescore-api-documentation
description: "GlobalWineScore API Documentation API skill. Use when working with GlobalWineScore API Documentation for globalwinescores. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# GlobalWineScore API Documentation
API version: 8234aab51481d37a30757d925b7f4221a659427e

## Auth
ApiKey Authorization in header

## Base URL
https://api.globalwinescore.com

## Setup
1. Set your API key in the appropriate header
2. GET /globalwinescores/latest/ -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### globalwinescores
| Method | Path | Description |
|--------|------|-------------|
| GET | /globalwinescores/latest/ | List all latest GWS |
| GET | /globalwinescores/ | List all historical GWS |

## Enhanced Skill Content
## Question Mapping

- "What are the latest wine scores?" -> GET /globalwinescores/latest/
- "Show me scores for a specific wine by ID" -> GET /globalwinescores/latest/?wine_id={id}
- "What wines from 2018 are rated?" -> GET /globalwinescores/latest/?vintage=2018
- "List all red wine scores" -> GET /globalwinescores/latest/?color=red
- "Are there any primeurs/futures scores available?" -> GET /globalwinescores/latest/?is_primeurs=true
- "Look up a wine by its LWIN code" -> GET /globalwinescores/latest/?lwin={code}
- "Find scores using an 11-digit LWIN" -> GET /globalwinescores/latest/?lwin_11={code}
- "Show me historical scores for a wine across all vintages" -> GET /globalwinescores/?wine_id={id}
- "Get the full scoring history for red wines" -> GET /globalwinescores/?color=red
- "What are the top-rated wines right now?" -> GET /globalwinescores/latest/?ordering=-score
- "Show the lowest-scored wines from 2015" -> GET /globalwinescores/latest/?vintage=2015&ordering=score
- "How many wine scores are in the database?" -> GET /globalwinescores/?limit=1 (check total count in response)
- "Get the next page of results" -> GET /globalwinescores/latest/?limit=50&offset=50
- "Compare latest vs historical scores for a wine" -> GET /globalwinescores/latest/?wine_id={id} then GET /globalwinescores/?wine_id={id}

## Response Tips

- **Score listings** (`/globalwinescores/` and `/latest/`): Paginated responses -- check `count` for total results and `next`/`previous` for navigation URLs. Default page size is limited; use `limit` and `offset` to control pagination.
- **Authentication errors**: Missing or invalid `Authorization` header returns 401/403. Ensure the API key is passed as a header value, not a query parameter.
- **Empty results**: A valid query with no matches returns 200 with an empty results array and `count: 0` -- this is not an error.
- **Ordering**: Use `-` prefix for descending order (e.g., `ordering=-score`). Invalid field names may be silently ignored.

## Anomaly Flags

- **Rate limiting**: Surface any 429 responses immediately; recommend backing off and retrying with exponential delay.
- **Empty result sets**: Flag when a query by `wine_id` or `lwin` returns zero results -- the identifier may be incorrect or the wine may not be scored.
- **Pagination exhaustion**: Warn when `next` is null but `count` exceeds the number of results retrieved, indicating a possible offset/limit mismatch.
- **Deprecation headers**: Watch for `Deprecation` or `Sunset` headers in responses and alert the user proactively.
- **Score anomalies**: Flag if a wine's latest score differs significantly from its historical average (retrieved via `/globalwinescores/`).
- **Auth misconfiguration**: If multiple 401s occur, suggest verifying the API key format and header name.

## Playbook

### 1. Look Up Scores for a Specific Wine

1. Call `GET /globalwinescores/latest/?wine_id={id}` with your API key in the `Authorization` header.
2. If results are empty, try searching by `lwin` or `lwin_11` instead.
3. Review the score, confidence interval, and journalist source data in the response.

### 2. Browse Top-Rated Wines by Vintage

1. Call `GET /globalwinescores/latest/?vintage=2018&ordering=-score&limit=25`.
2. Note the `count` field for total matching wines.
3. Page through results using `offset` increments matching your `limit`.
4. Optionally filter further by `color=red` or `color=white`.

### 3. Compare Latest Score vs Historical Scores

1. Call `GET /globalwinescores/latest/?wine_id={id}` to get the current consensus score.
2. Call `GET /globalwinescores/?wine_id={id}&ordering=-vintage` to get all historical scores.
3. Compare the latest score against the historical trend to identify improving or declining wines.

### 4. Explore Primeurs (Futures) Ratings

1. Call `GET /globalwinescores/latest/?is_primeurs=true&ordering=-score&limit=50`.
2. Review which wines have early scores before bottling.
3. Cross-reference with `vintage` to confirm the en-primeur campaign year.
4. Use `lwin` to match against trade databases for purchasing decisions.

### 5. Paginate Through the Full Database

1. Start with `GET /globalwinescores/?limit=100&offset=0`.
2. Record the `count` value from the first response to know the total.
3. Loop: increment `offset` by 100 each call until `next` is null.
4. Respect rate limits between requests -- pause if a 429 is returned.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
