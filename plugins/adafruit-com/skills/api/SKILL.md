---
name: adafruit-io-rest-api
description: "Adafruit IO REST API skill. Use when working with Adafruit IO REST for user, {username}, webhooks. Covers 71 endpoints."
version: 1.0.0
generator: lapsh
---

# Adafruit IO REST API
API version: 2.0.0

## Auth
ApiKey X-AIO-Key in header | ApiKey X-AIO-Key in query | ApiKey X-AIO-Signature in header

## Base URL
https://io.adafruit.com/api/v2

## Setup
1. Set your API key in the appropriate header
2. GET /user -- verify access
3. POST /{username}/feeds -- create first feeds

## Endpoints

71 endpoints across 3 groups. See references/api-spec.lap for full details.

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user | Get information about the current user |

### {username}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{username}/throttle | Get the user's data rate limit and current activity level. |
| GET | /{username}/activities | All activities for current user |
| DELETE | /{username}/activities | All activities for current user |
| GET | /{username}/activities/{type} | Get activities by type for current user |
| GET | /{username}/feeds | All feeds for current user |
| POST | /{username}/feeds | Create a new Feed |
| GET | /{username}/feeds/{feed_key} | Get feed by feed key |
| PUT | /{username}/feeds/{feed_key} | Replace an existing Feed |
| PATCH | /{username}/feeds/{feed_key} | Update properties of an existing Feed |
| DELETE | /{username}/feeds/{feed_key} | Delete an existing Feed |
| GET | /{username}/feeds/{feed_key}/details | Get detailed feed by feed key |
| GET | /{username}/feeds/{feed_key}/data | Get all data for the given feed |
| POST | /{username}/feeds/{feed_key}/data | Create new Data |
| GET | /{username}/feeds/{feed_key}/data/chart | Chart data for current feed |
| POST | /{username}/feeds/{feed_key}/data/batch | Create multiple new Data records |
| GET | /{username}/feeds/{feed_key}/data/previous | Previous Data in Queue |
| GET | /{username}/feeds/{feed_key}/data/next | Next Data in Queue |
| GET | /{username}/feeds/{feed_key}/data/last | Last Data in Queue |
| GET | /{username}/feeds/{feed_key}/data/first | First Data in Queue |
| GET | /{username}/feeds/{feed_key}/data/retain | Last Data in MQTT CSV format |
| GET | /{username}/feeds/{feed_key}/data/{id} | Returns data based on feed key |
| PUT | /{username}/feeds/{feed_key}/data/{id} | Replace existing Data |
| PATCH | /{username}/feeds/{feed_key}/data/{id} | Update properties of existing Data |
| DELETE | /{username}/feeds/{feed_key}/data/{id} | Delete existing Data |
| GET | /{username}/groups | All groups for current user |
| POST | /{username}/groups | Create a new Group |
| GET | /{username}/groups/{group_key} | Returns Group based on ID |
| PUT | /{username}/groups/{group_key} | Replace an existing Group |
| PATCH | /{username}/groups/{group_key} | Update properties of an existing Group |
| DELETE | /{username}/groups/{group_key} | Delete an existing Group |
| POST | /{username}/groups/{group_key}/add | Add an existing Feed to a Group |
| POST | /{username}/groups/{group_key}/remove | Remove a Feed from a Group |
| GET | /{username}/groups/{group_key}/feeds | All feeds for current user in a given group |
| POST | /{username}/groups/{group_key}/feeds | Create a new Feed in a Group |
| POST | /{username}/groups/{group_key}/data | Create new data for multiple feeds in a group |
| GET | /{username}/groups/{group_key}/feeds/{feed_key}/data | All data for current feed in a specific group |
| POST | /{username}/groups/{group_key}/feeds/{feed_key}/data | Create new Data in a feed belonging to a particular group |
| POST | /{username}/groups/{group_key}/feeds/{feed_key}/data/batch | Create multiple new Data records in a feed belonging to a particular group |
| GET | /{username}/dashboards | All dashboards for current user |
| POST | /{username}/dashboards | Create a new Dashboard |
| GET | /{username}/dashboards/{id} | Returns Dashboard based on ID |
| PUT | /{username}/dashboards/{id} | Replace an existing Dashboard |
| PATCH | /{username}/dashboards/{id} | Update properties of an existing Dashboard |
| DELETE | /{username}/dashboards/{id} | Delete an existing Dashboard |
| GET | /{username}/dashboards/{dashboard_id}/blocks | All blocks for current user |
| POST | /{username}/dashboards/{dashboard_id}/blocks | Create a new Block |
| GET | /{username}/dashboards/{dashboard_id}/blocks/{id} | Returns Block based on ID |
| PUT | /{username}/dashboards/{dashboard_id}/blocks/{id} | Replace an existing Block |
| PATCH | /{username}/dashboards/{dashboard_id}/blocks/{id} | Update properties of an existing Block |
| DELETE | /{username}/dashboards/{dashboard_id}/blocks/{id} | Delete an existing Block |
| GET | /{username}/tokens | All tokens for current user |
| POST | /{username}/tokens | Create a new Token |
| GET | /{username}/tokens/{id} | Returns Token based on ID |
| PUT | /{username}/tokens/{id} | Replace an existing Token |
| PATCH | /{username}/tokens/{id} | Update properties of an existing Token |
| DELETE | /{username}/tokens/{id} | Delete an existing Token |
| GET | /{username}/triggers | All triggers for current user |
| POST | /{username}/triggers | Create a new Trigger |
| GET | /{username}/triggers/{id} | Returns Trigger based on ID |
| PUT | /{username}/triggers/{id} | Replace an existing Trigger |
| PATCH | /{username}/triggers/{id} | Update properties of an existing Trigger |
| DELETE | /{username}/triggers/{id} | Delete an existing Trigger |
| GET | /{username}/{type}/{type_id}/acl | All permissions for current user and type |
| POST | /{username}/{type}/{type_id}/acl | Create a new Permission |
| GET | /{username}/{type}/{type_id}/acl/{id} | Returns Permission based on ID |
| PUT | /{username}/{type}/{type_id}/acl/{id} | Replace an existing Permission |
| PATCH | /{username}/{type}/{type_id}/acl/{id} | Update properties of an existing Permission |
| DELETE | /{username}/{type}/{type_id}/acl/{id} | Delete an existing Permission |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| POST | /webhooks/feed/:token | Send data to a feed via webhook URL. |
| POST | /webhooks/feed/:token/raw | Send arbitrary data to a feed via webhook URL. |

## Enhanced Skill Content
## Question Mapping

- "What feeds do I have?" -> GET /{username}/feeds
- "Send a sensor reading to my temperature feed" -> POST /{username}/feeds/{feed_key}/data
- "What was the last value sent to my feed?" -> GET /{username}/feeds/{feed_key}/data/last
- "How close am I to my rate limit?" -> GET /{username}/throttle
- "Show me my feed data as a chart" -> GET /{username}/feeds/{feed_key}/data/chart
- "Upload multiple data points at once" -> POST /{username}/feeds/{feed_key}/data/batch
- "Create a new feed inside a group" -> POST /{username}/groups/{group_key}/feeds
- "Send data to all feeds in a group at once" -> POST /{username}/groups/{group_key}/data
- "List all my dashboards" -> GET /{username}/dashboards
- "Add a block to my dashboard" -> POST /{username}/dashboards/{dashboard_id}/blocks
- "Who has access to my feed?" -> GET /{username}/{type}/{type_id}/acl
- "Get my account info and plan details" -> GET /user
- "Delete all my activity logs" -> DELETE /{username}/activities
- "Set up a trigger on a feed value" -> POST /{username}/triggers
- "Push data into Adafruit IO from an external webhook" -> POST /webhooks/feed/:token

## Response Tips

- **Feeds & Data**: Feed objects include `last_value`, `created_at`, and `updated_at`; data points have `value`, `feed_id`, `created_at`, and optional `lat`/`lon`/`ele` for location. The `include` param controls which related fields are expanded.
- **Throttle**: Returns current rate limit usage vs. allowed maximum; compare `active_data_rate` to `data_rate_limit` to gauge headroom.
- **Activities**: Returns a flat list filtered by `start_time`/`end_time`; use `limit` to paginate since there is no cursor -- fetch sequential time windows instead.
- **Chart data**: Returns pre-aggregated points bucketed by `resolution` (e.g., 1, 5, 10 minutes); the `hours` param controls the lookback window.
- **Groups**: Group responses nest an array of member feeds; use `/groups/{key}/feeds` for the full feed list when the summary is insufficient.
- **Dashboards & Blocks**: Dashboard objects contain a `blocks` array summary; fetch `/blocks` sub-resource for full block configs including `visual_type` and `properties`.
- **ACL/Permissions**: Responses describe per-user access grants on a typed resource; the `type` path param is one of `feeds`, `groups`, `dashboards`.
- **Errors**: All endpoints share the same error shape (401 unauthorized, 403 forbidden, 404 not found, 500 server error); 401 almost always means a missing or invalid `X-AIO-Key`.
- **Webhooks**: Return minimal acknowledgment; errors on the webhook token path typically mean the token is expired or revoked.

## Anomaly Flags

- **Rate limit approaching**: After any write, check `GET /{username}/throttle` -- surface a warning when `active_data_rate` exceeds 80% of `data_rate_limit`.
- **401 on first call**: Likely means the `X-AIO-Key` header is missing or malformed. Prompt the user to verify their API key before retrying.
- **404 on feed/group operations**: The `feed_key` or `group_key` is case-sensitive and uses the slug form (e.g., `temperature-sensor`, not `Temperature Sensor`). Flag key mismatch as the probable cause.
- **Batch upload partial failures**: `POST .../data/batch` may silently drop malformed entries. If the returned count is less than submitted, surface the discrepancy.
- **Stale last_value**: If `GET .../data/last` returns a timestamp older than expected, alert that the device may be offline or the feed is inactive.
- **500 errors**: Adafruit IO occasionally returns 500 during maintenance windows. If a 500 is encountered, suggest a retry after 30 seconds before escalating.
- **Deprecated token patterns**: If `GET /{username}/tokens` returns tokens with no recent `last_used_at`, flag them as candidates for rotation or deletion.

## Playbook

### 1. Set up a new IoT feed and send your first data point

1. `GET /user` to confirm authentication and retrieve your username.
2. `GET /{username}/throttle` to check you have rate limit headroom.
3. `POST /{username}/feeds` with `{"feed": {"name": "Temperature", "description": "Living room sensor"}}` to create the feed.
4. Note the returned `key` (e.g., `temperature`).
5. `POST /{username}/feeds/temperature/data` with `{"datum": {"value": "22.5"}}` to send a reading.
6. `GET /{username}/feeds/temperature/data/last` to verify the value was stored.

### 2. Organize feeds into a group and send multi-feed data

1. `POST /{username}/groups` with `{"group": {"name": "Weather Station"}}` to create a group.
2. `POST /{username}/groups/weather-station/add` with `{"feed_key": "temperature"}` to add an existing feed.
3. `POST /{username}/groups/weather-station/feeds` with `{"feed": {"name": "Humidity"}}` to create a new feed directly inside the group.
4. `POST /{username}/groups/weather-station/data` with `{"group_feed_data": {"feeds": {"temperature": "22.5", "humidity": "60"}}}` to push values to all feeds in one call.
5. `GET /{username}/groups/weather-station/feeds` to confirm both feeds and their latest values.

### 3. Build a dashboard with visualization blocks

1. `POST /{username}/dashboards` with `{"dashboard": {"name": "Home Monitor"}}` to create a dashboard.
2. Note the returned `id`.
3. `POST /{username}/dashboards/{id}/blocks` with a block definition specifying `visual_type` (e.g., line chart) and linking it to your feed key.
4. Repeat step 3 for additional blocks (gauge, toggle, map, etc.).
5. `GET /{username}/dashboards/{id}/blocks` to verify the full layout.

### 4. Set up a reactive trigger on feed data

1. `GET /{username}/feeds` to identify the feed key you want to monitor.
2. `POST /{username}/triggers` with `{"trigger": {"name": "High Temp Alert", "feed_key": "temperature", "operator": "gt", "value": "30"}}` to fire when temperature exceeds 30.
3. `GET /{username}/triggers` to confirm the trigger is active and correctly configured.
4. Send a test data point: `POST /{username}/feeds/temperature/data` with `{"datum": {"value": "31"}}`.
5. Check activity: `GET /{username}/activities?limit=5` to verify the trigger fired.

### 5. Ingest external data via webhook

1. `GET /{username}/feeds/{feed_key}/details` to find the webhook token (or create a token via `POST /{username}/tokens`).
2. Configure your external service to POST to `https://io.adafruit.com/api/v2/webhooks/feed/{token}` with `{"payload": {"value": "42"}}`.
3. For raw body ingestion (plain text sensors), POST to `/webhooks/feed/{token}/raw` with the value as the request body.
4. `GET /{username}/feeds/{feed_key}/data/last` to confirm the webhook delivered the data.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
