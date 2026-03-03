---
name: query-api
description: "Query API skill. Use when working with Query for insights, funnels, retention. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# Query API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://{regionAndDomain}.com/api/query

## Setup
1. No auth setup needed
2. GET /insights -- verify access
3. POST /cohorts/list -- create first list

## Endpoints

19 endpoints across 9 groups. See references/api-spec.lap for full details.

### insights
| Method | Path | Description |
|--------|------|-------------|
| GET | /insights | Query Saved Report |

### funnels
| Method | Path | Description |
|--------|------|-------------|
| GET | /funnels | Query Saved Report |
| GET | /funnels/list | List Saved Funnels |

### retention
| Method | Path | Description |
|--------|------|-------------|
| GET | /retention | Query Retention Report |
| GET | /retention/addiction | Query Frequency Report |

### segmentation
| Method | Path | Description |
|--------|------|-------------|
| GET | /segmentation | Query Segmentation Report |
| GET | /segmentation/numeric | Numerically Bucket |
| GET | /segmentation/sum | Numerically Sum |
| GET | /segmentation/average | Numerically Average |

### stream
| Method | Path | Description |
|--------|------|-------------|
| GET | /stream/query | Profile Event Activity |

### cohorts
| Method | Path | Description |
|--------|------|-------------|
| POST | /cohorts/list | List Saved Cohorts |

### engage
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage | Query Profiles |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Aggregate Event Counts |
| GET | /events/top | Today's Top Events |
| GET | /events/names | Top Events |
| GET | /events/properties | Aggregrated Event Property Values |
| GET | /events/properties/top | Top Event Properties |
| GET | /events/properties/values | Top Event Property Values |

### jql
| Method | Path | Description |
|--------|------|-------------|
| POST | /jql | Custom JQL Query |

## Enhanced Skill Content
## Question Mapping

- "How do I get results from a saved insight?" -> GET /insights
- "Show me funnel conversion data for a specific funnel" -> GET /funnels
- "What funnels are available in my project?" -> GET /funnels/list
- "How well are users retained after signup?" -> GET /retention
- "What does user addiction/habit frequency look like?" -> GET /retention/addiction
- "How is a specific event trending over time?" -> GET /segmentation
- "What's the numeric distribution of an event property?" -> GET /segmentation/numeric
- "What's the total sum of a property across events?" -> GET /segmentation/sum
- "What's the average value of a property per event?" -> GET /segmentation/average
- "Show me the raw event stream for a specific user" -> GET /stream/query
- "List all cohorts in the project" -> POST /cohorts/list
- "Query user profiles with filters" -> POST /engage
- "How many times did an event happen per day?" -> GET /events
- "What are the most common events?" -> GET /events/top
- "List all event names in the project" -> GET /events/names
- "Break down an event by a specific property over time" -> GET /events/properties
- "What are the top properties for an event?" -> GET /events/properties/top
- "What distinct values does an event property have?" -> GET /events/properties/values

## Response Tips

- **Insights/Segmentation/Events**: Data lives in nested `data.series` (time buckets) and `data.values` (keyed by segment label) -- iterate values keys to get each breakdown line.
- **Funnels**: `meta.dates` lists the date buckets; `data` is keyed by date -- missing date keys mean zero-traffic periods, not errors.
- **Retention**: Response shape changes with `retention_type` (birth vs compounded) -- always check which type was requested before parsing.
- **Stream**: Results are under `results.events` as an array of event maps -- each map contains `$properties` nested one level deep.
- **Engage**: Paginated via `page`, `page_size`, `total`, and `session_id` -- you must pass `session_id` back on subsequent page requests to maintain cursor consistency.
- **Cohorts/JQL/Lists**: Return bare arrays or unstructured results -- check HTTP status rather than relying on a `status` field.

## Anomaly Flags

- **Rate limiting**: Surface HTTP 429 responses immediately; back off exponentially and report remaining quota if headers are present.
- **Empty series data**: If `data.series` returns an empty array or `legend_size` is 0, flag that the date range or filters may be too restrictive.
- **Stale computation**: When `computed_at` timestamp is more than 24 hours old, warn that results may be cached/delayed.
- **Pagination overflow**: If `POST /engage` returns `total` significantly larger than `page_size`, proactively note how many pages remain and estimate call count.
- **Invalid enum values**: If the API rejects a `unit`, `type`, or `retention_type` value, surface the allowed enum values from the spec (e.g., `day/week/month`) rather than letting the user guess.
- **Missing workspace_id**: All endpoints require `workspace_id` -- flag immediately if omitted rather than letting an ambiguous auth error propagate.

## Playbook

### 1. Analyze funnel conversion over time

1. Call `GET /funnels/list` to discover available funnels and their IDs.
2. Pick the target `funnel_id` from the list.
3. Call `GET /funnels` with `funnel_id`, setting `unit=week` and desired `interval`.
4. Iterate `meta.dates` to extract each time bucket, then read step-by-step conversion from `data`.
5. Calculate drop-off rates between steps: `(step_n - step_n+1) / step_n`.

### 2. Deep-dive a specific event's trend and property breakdown

1. Call `GET /events/names` to confirm the exact event name string.
2. Call `GET /events` with `event`, `type=general`, and `unit=day` to get the overall trend.
3. Call `GET /events/properties/top` with `event` to find the most relevant properties.
4. Call `GET /events/properties` with `event`, the chosen property `name`, `type=general`, and `unit=day` to break down the trend by property value.
5. Optionally call `GET /events/properties/values` to enumerate all distinct values for further filtering.

### 3. User-level investigation

1. Call `POST /engage` with filters to find user profiles matching criteria; note the `session_id` and `total`.
2. Page through results by re-calling `POST /engage` with the same `session_id` and incrementing `page`.
3. Extract `distinct_id` from the target user profile.
4. Call `GET /stream/query` with `distinct_ids` set to that user's ID to pull their raw event stream.
5. Correlate stream events with segmentation or retention data for context.

### 4. Retention analysis with segmentation context

1. Call `GET /retention` with `born_event` set to the activation event and `event` set to the return action, using `unit=week`.
2. Review the retention curve; identify the week where drop-off is steepest.
3. Call `GET /segmentation` with the return `event` and a `where` clause filtering to the drop-off cohort's timeframe.
4. Call `GET /segmentation/average` on a value property (e.g., session duration) to check if retained users differ behaviorally.
5. Use `GET /retention/addiction` with `addiction_unit=day` to see if power users show higher-frequency habit loops.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
