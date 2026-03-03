---
name: agent-analytics-api
description: "Agent Analytics API skill. Use when working with Agent Analytics for track, stats, events. Covers 32 endpoints."
version: 1.0.0
generator: lapsh
---

# Agent Analytics API
API version: 1.0.0

## Auth
ApiKey X-API-Key in header | ApiKey token in query

## Base URL
https://api.agentanalytics.sh

## Setup
1. Set your API key in the appropriate header
2. GET /stats -- verify access
3. POST /track -- create first track

## Endpoints

32 endpoints across 19 groups. See references/api-spec.lap for full details.

### track
| Method | Path | Description |
|--------|------|-------------|
| POST | /track | Track a single event |
| POST | /track/batch | Track multiple events |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats | Aggregated stats overview |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Raw event log |

### query
| Method | Path | Description |
|--------|------|-------------|
| POST | /query | Flexible analytics query |

### properties
| Method | Path | Description |
|--------|------|-------------|
| GET | /properties | Discover event names and property keys |
| GET | /properties/received | Property keys by event name |

### sessions
| Method | Path | Description |
|--------|------|-------------|
| GET | /sessions | List sessions |
| GET | /sessions/distribution | Session duration histogram |

### breakdown
| Method | Path | Description |
|--------|------|-------------|
| GET | /breakdown | Top property values |

### insights
| Method | Path | Description |
|--------|------|-------------|
| GET | /insights | Period-over-period comparison |

### pages
| Method | Path | Description |
|--------|------|-------------|
| GET | /pages | Entry/exit page stats |

### heatmap
| Method | Path | Description |
|--------|------|-------------|
| GET | /heatmap | Day-of-week x hour traffic grid |

### funnel
| Method | Path | Description |
|--------|------|-------------|
| POST | /funnel | Funnel analysis |

### retention
| Method | Path | Description |
|--------|------|-------------|
| GET | /retention | Cohort retention analysis |

### stream
| Method | Path | Description |
|--------|------|-------------|
| GET | /stream | Live event stream (SSE) |

### live
| Method | Path | Description |
|--------|------|-------------|
| GET | /live | Live snapshot (real-time) |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects | List all projects |
| POST | /projects | Create a new project |
| GET | /projects/{id} | Get project details |
| PATCH | /projects/{id} | Update a project |
| DELETE | /projects/{id} | Delete a project |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account | Get account info |
| POST | /account/revoke-key | Revoke and regenerate API key |

### experiments
| Method | Path | Description |
|--------|------|-------------|
| GET | /experiments/config | Get experiment config for tracker.js |
| POST | /experiments | Create an A/B experiment |
| GET | /experiments | List experiments |
| GET | /experiments/{id} | Get experiment with live results |
| PATCH | /experiments/{id} | Update experiment status |
| DELETE | /experiments/{id} | Delete an experiment |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Health check |

### tracker.js
| Method | Path | Description |
|--------|------|-------------|
| GET | /tracker.js | JavaScript tracker script |

## Enhanced Skill Content
## Question Mapping

- "How do I track a custom event?" -> POST /track
- "Can I send multiple events at once?" -> POST /track/batch
- "What are my overall traffic stats for the last week?" -> GET /stats
- "Show me all events for a specific session" -> GET /events
- "Which pages do users land on most?" -> GET /pages
- "What is my bounce rate trend compared to last month?" -> GET /insights
- "How many users are on my site right now?" -> GET /live
- "Break down signups by country" -> GET /breakdown
- "What percentage of users complete my checkout funnel?" -> POST /funnel
- "Are users coming back after their first visit?" -> GET /retention
- "What custom properties have been tracked?" -> GET /properties/received
- "How do I create a new project and get the tracking snippet?" -> POST /projects
- "Which experiment variant is winning?" -> GET /experiments/{id}
- "How do I run an A/B test on my signup flow?" -> POST /experiments
- "What are my account limits and current usage?" -> GET /account

## Response Tips

- **Track endpoints** return 202 (queued, not processed) -- do not treat as confirmation that data is queryable yet; allow a brief ingestion delay before querying.
- **Stats/Insights** nest period comparisons inside `metrics` maps with `current`, `previous`, `change`, and `change_pct` (nullable when previous is zero) -- always nil-check `change_pct`.
- **Query endpoint** returns generic `rows` arrays whose shape depends on `group_by` and `metrics` params -- inspect the echoed `metrics` and `group_by` fields to interpret row keys.
- **Funnel** returns `steps` with per-step conversion plus `overall_conversion_rate` as a decimal (0-1, not percentage) -- multiply by 100 for display.
- **Retention** returns `average_rates` as an array indexed by period offset -- index 0 is always 100% (the cohort itself), real retention starts at index 1.
- **Sessions/Events** use `limit` for pagination but have no cursor or offset -- filter with `since` timestamps to page through large datasets.
- **Projects** POST returns 200 with `existing: true` if the project already exists, 201 for new -- check status code or `existing` field to distinguish.
- **Experiments** PATCH requires explicit `status` value (`active`/`paused`/`completed`) -- setting `completed` without a `winner` is allowed but the winner stays null.

## Anomaly Flags

- **429 on /track or /track/batch**: Rate limit hit. Surface immediately with the project token involved and suggest batching events or spacing requests. Check `rate_limit_rpm` from GET /account.
- **Bounce rate spike**: When GET /insights shows `bounce_rate.change_pct` exceeding +20%, flag as potential tracking or UX regression.
- **Zero unique users with nonzero events**: In GET /stats, `unique_users: 0` alongside `total_events > 0` suggests missing `user_id` on tracked events -- warn about anonymous-only tracking.
- **Project limit approaching**: When GET /account shows `projects_count` near `projects_limit`, alert before the next POST /projects fails with 403.
- **Experiment with no goal conversions**: When GET /experiments/{id} shows all variant conversion counts at zero after 48+ hours, flag as likely misconfigured `goal_event`.
- **Retention cliff**: When GET /retention returns `average_rates[1]` below 10%, proactively surface as a critical retention problem.
- **Stale heatmap data**: When GET /heatmap returns an empty `heatmap` array or null `peak`, flag that insufficient data has been collected for the time window.
- **409 on project or experiment creation**: Name collision -- surface the conflicting resource name so the user can rename or find the existing one.

## Playbook

### 1. Set Up a New Project and Start Tracking

1. GET /account -- confirm your tier and remaining project slots.
2. POST /projects with `name` and optional `allowed_origins` -- save the returned `project_token`.
3. GET /projects/{id} -- verify the project exists and note the `usage_today` baseline.
4. POST /track with the `token` (project_token) and a test event like `"page_view"` -- confirm 202 response with `queued: true`.
5. GET /events with `project` -- after a few seconds, verify your test event appears.

### 2. Analyze a Conversion Funnel

1. GET /properties with `project` -- identify the event names available for funnel steps.
2. POST /funnel with ordered `steps` (e.g., `page_view` -> `signup_start` -> `signup_complete`) and a `conversion_window_hours` appropriate to your flow.
3. Review `steps[].conversion_rate` for each stage to find the biggest drop-off.
4. Re-run POST /funnel adding `breakdown: "referrer"` to see if drop-off varies by traffic source.
5. GET /insights with `period: "30d"` to cross-reference overall engagement trends with funnel performance.

### 3. Run an A/B Test

1. POST /experiments with `project`, `name`, `variants` (e.g., `["control", "new_cta"]`), and `goal_event` (e.g., `"signup_complete"`).
2. GET /experiments/config with `token` (project_token) -- integrate the returned variant assignment into your frontend.
3. POST /track events that include the assigned variant in `properties` so conversions tie back to the experiment.
4. GET /experiments/{id} periodically to monitor per-variant conversion counts and statistical significance.
5. PATCH /experiments/{id} with `status: "completed"` and `winner` once you have a clear result.

### 4. Diagnose a Traffic Drop

1. GET /insights with `period: "7d"` -- check `change_pct` across `total_events`, `unique_users`, and `total_sessions` to quantify the drop.
2. GET /stats with `groupBy: "hour"` and `since` covering the affected window -- pinpoint when the drop started.
3. GET /heatmap -- check if the activity pattern shifted (e.g., a geography or timezone change).
4. GET /breakdown with `property: "referrer"` -- see if a specific traffic source disappeared.
5. GET /live -- confirm whether current real-time traffic is recovering or still depressed.

### 5. Audit Account Usage and Manage Keys

1. GET /account -- review `tier`, `projects_count` vs `projects_limit`, and `tier_limits` (especially `max_events_lifetime` and `retention_days`).
2. GET /projects -- list all projects and check `has_api_key` status.
3. If a key is compromised, POST /account/revoke-key -- save the new `api_key` from the response immediately (it is shown only once).
4. PATCH /projects/{id} to tighten `allowed_origins` on any project that should be locked to specific domains.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
