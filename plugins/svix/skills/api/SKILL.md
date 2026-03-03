---
name: svix-api
description: "Svix API skill. Use when working with Svix for api, ingest. Covers 128 endpoints."
version: 1.0.0
generator: lapsh
---

# Svix API
API version: 1.84.0

## Auth
Bearer bearer

## Base URL
https://api.eu.svix.com/

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/v1/app -- verify access
3. POST /api/v1/app -- create first app

## Endpoints

128 endpoints across 2 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1/app | List Applications |
| POST | /api/v1/app | Create Application |
| GET | /api/v1/app/{app_id} | Get Application |
| PUT | /api/v1/app/{app_id} | Update Application |
| DELETE | /api/v1/app/{app_id} | Delete Application |
| PATCH | /api/v1/app/{app_id} | Patch Application |
| GET | /api/v1/app/{app_id}/attempt/endpoint/{endpoint_id} | List Attempts By Endpoint |
| GET | /api/v1/app/{app_id}/attempt/msg/{msg_id} | List Attempts By Msg |
| GET | /api/v1/app/{app_id}/endpoint | List Endpoints |
| POST | /api/v1/app/{app_id}/endpoint | Create Endpoint |
| GET | /api/v1/app/{app_id}/endpoint/{endpoint_id} | Get Endpoint |
| PUT | /api/v1/app/{app_id}/endpoint/{endpoint_id} | Update Endpoint |
| DELETE | /api/v1/app/{app_id}/endpoint/{endpoint_id} | Delete Endpoint |
| PATCH | /api/v1/app/{app_id}/endpoint/{endpoint_id} | Patch Endpoint |
| POST | /api/v1/app/{app_id}/endpoint/{endpoint_id}/bulk-replay | Bulk Replay Messages |
| GET | /api/v1/app/{app_id}/endpoint/{endpoint_id}/headers | Get Endpoint Headers |
| PUT | /api/v1/app/{app_id}/endpoint/{endpoint_id}/headers | Update Endpoint Headers |
| PATCH | /api/v1/app/{app_id}/endpoint/{endpoint_id}/headers | Patch Endpoint Headers |
| GET | /api/v1/app/{app_id}/endpoint/{endpoint_id}/msg | List Attempted Messages |
| POST | /api/v1/app/{app_id}/endpoint/{endpoint_id}/recover | Recover Failed Webhooks |
| POST | /api/v1/app/{app_id}/endpoint/{endpoint_id}/replay-missing | Replay Missing Webhooks |
| GET | /api/v1/app/{app_id}/endpoint/{endpoint_id}/secret | Get Endpoint Secret |
| POST | /api/v1/app/{app_id}/endpoint/{endpoint_id}/secret/rotate | Rotate Endpoint Secret |
| POST | /api/v1/app/{app_id}/endpoint/{endpoint_id}/send-example | Send Event Type Example Message |
| GET | /api/v1/app/{app_id}/endpoint/{endpoint_id}/stats | Endpoint Stats |
| GET | /api/v1/app/{app_id}/endpoint/{endpoint_id}/transformation | Get Endpoint Transformation |
| PATCH | /api/v1/app/{app_id}/endpoint/{endpoint_id}/transformation | Patch Endpoint Transformation |
| GET | /api/v1/app/{app_id}/integration | List Integrations |
| POST | /api/v1/app/{app_id}/integration | Create Integration |
| GET | /api/v1/app/{app_id}/integration/{integ_id} | Get Integration |
| PUT | /api/v1/app/{app_id}/integration/{integ_id} | Update Integration |
| DELETE | /api/v1/app/{app_id}/integration/{integ_id} | Delete Integration |
| GET | /api/v1/app/{app_id}/integration/{integ_id}/key | Get Integration Key |
| POST | /api/v1/app/{app_id}/integration/{integ_id}/key/rotate | Rotate Integration Key |
| GET | /api/v1/app/{app_id}/msg | List Messages |
| POST | /api/v1/app/{app_id}/msg | Create Message |
| POST | /api/v1/app/{app_id}/msg/expunge-all-contents | Expunge all message contents |
| POST | /api/v1/app/{app_id}/msg/precheck/active | Create Message Precheck |
| GET | /api/v1/app/{app_id}/msg/{msg_id} | Get Message |
| GET | /api/v1/app/{app_id}/msg/{msg_id}/attempt/{attempt_id} | Get Attempt |
| DELETE | /api/v1/app/{app_id}/msg/{msg_id}/attempt/{attempt_id}/content | Delete attempt response body |
| DELETE | /api/v1/app/{app_id}/msg/{msg_id}/content | Delete message payload |
| GET | /api/v1/app/{app_id}/msg/{msg_id}/endpoint | List Attempted Destinations |
| POST | /api/v1/app/{app_id}/msg/{msg_id}/endpoint/{endpoint_id}/resend | Resend Webhook |
| GET | /api/v1/app/{app_id}/poller/{sink_id} | Poller Poll |
| GET | /api/v1/app/{app_id}/poller/{sink_id}/consumer/{consumer_id} | Poller Consumer Poll |
| POST | /api/v1/app/{app_id}/poller/{sink_id}/consumer/{consumer_id}/seek | Poller Consumer Seek |
| POST | /api/v1/auth/app-portal-access/{app_id} | Get Consumer App Portal Access |
| POST | /api/v1/auth/app/{app_id}/expire-all | Expire All |
| POST | /api/v1/auth/logout | Logout |
| POST | /api/v1/auth/stream-logout | Stream Logout |
| POST | /api/v1/auth/stream-portal-access/{stream_id} | Get Stream Portal Access |
| POST | /api/v1/auth/stream/{stream_id}/expire-all | Stream Expire All |
| GET | /api/v1/auth/stream/{stream_id}/sink/{sink_id}/poller/token | Get Poller Token |
| POST | /api/v1/auth/stream/{stream_id}/sink/{sink_id}/poller/token/rotate | Rotate Poller Token |
| GET | /api/v1/background-task | List Background Tasks |
| GET | /api/v1/background-task/{task_id} | Get Background Task |
| GET | /api/v1/connector | List Connectors |
| POST | /api/v1/connector | Create Connector |
| GET | /api/v1/connector/{connector_id} | Get Connector |
| PUT | /api/v1/connector/{connector_id} | Update Connector |
| DELETE | /api/v1/connector/{connector_id} | Delete Connector |
| PATCH | /api/v1/connector/{connector_id} | Patch Connector |
| POST | /api/v1/environment/export | Export Environment Configuration |
| POST | /api/v1/environment/import | Import Environment Configuration |
| GET | /api/v1/event-type | List Event Types |
| POST | /api/v1/event-type | Create Event Type |
| POST | /api/v1/event-type/import/openapi | Event Type Import From Openapi |
| GET | /api/v1/event-type/{event_type_name} | Get Event Type |
| PUT | /api/v1/event-type/{event_type_name} | Update Event Type |
| DELETE | /api/v1/event-type/{event_type_name} | Delete Event Type |
| PATCH | /api/v1/event-type/{event_type_name} | Patch Event Type |
| GET | /api/v1/health | Health |
| GET | /api/v1/operational-webhook/endpoint | List Operational Webhook Endpoints |
| POST | /api/v1/operational-webhook/endpoint | Create Operational Webhook Endpoint |
| GET | /api/v1/operational-webhook/endpoint/{endpoint_id} | Get Operational Webhook Endpoint |
| PUT | /api/v1/operational-webhook/endpoint/{endpoint_id} | Update Operational Webhook Endpoint |
| DELETE | /api/v1/operational-webhook/endpoint/{endpoint_id} | Delete Operational Webhook Endpoint |
| GET | /api/v1/operational-webhook/endpoint/{endpoint_id}/headers | Get Operational Webhook Endpoint Headers |
| PUT | /api/v1/operational-webhook/endpoint/{endpoint_id}/headers | Update Operational Webhook Endpoint Headers |
| GET | /api/v1/operational-webhook/endpoint/{endpoint_id}/secret | Get Operational Webhook Endpoint Secret |
| POST | /api/v1/operational-webhook/endpoint/{endpoint_id}/secret/rotate | Rotate Operational Webhook Endpoint Secret |
| POST | /api/v1/stats/usage/app | Aggregate App Stats |
| PUT | /api/v1/stats/usage/event-types | Aggregate Event Types |
| GET | /api/v1/stream | List Streams |
| POST | /api/v1/stream | Create Stream |
| GET | /api/v1/stream/event-type | List Stream Event Types |
| POST | /api/v1/stream/event-type | Create Stream Event Type |
| GET | /api/v1/stream/event-type/{name} | Get Stream Event Type |
| PUT | /api/v1/stream/event-type/{name} | Update Stream Event Type |
| DELETE | /api/v1/stream/event-type/{name} | Delete Stream Event Type |
| PATCH | /api/v1/stream/event-type/{name} | Patch Stream Event Type |
| GET | /api/v1/stream/{stream_id} | Get Stream |
| PUT | /api/v1/stream/{stream_id} | Update Stream |
| DELETE | /api/v1/stream/{stream_id} | Delete Stream |
| PATCH | /api/v1/stream/{stream_id} | Patch Stream |
| POST | /api/v1/stream/{stream_id}/events | Create Events |
| GET | /api/v1/stream/{stream_id}/sink | List Sinks |
| POST | /api/v1/stream/{stream_id}/sink | Create Sink |
| GET | /api/v1/stream/{stream_id}/sink/{sink_id} | Get Sink |
| PUT | /api/v1/stream/{stream_id}/sink/{sink_id} | Update Sink |
| DELETE | /api/v1/stream/{stream_id}/sink/{sink_id} | Delete Sink |
| PATCH | /api/v1/stream/{stream_id}/sink/{sink_id} | Patch Sink |
| GET | /api/v1/stream/{stream_id}/sink/{sink_id}/events | Poller Sink Stream Events |
| GET | /api/v1/stream/{stream_id}/sink/{sink_id}/headers | Get Sink Headers |
| PATCH | /api/v1/stream/{stream_id}/sink/{sink_id}/headers | Patch Sink Headers |
| GET | /api/v1/stream/{stream_id}/sink/{sink_id}/secret | Get Sink Secret |
| POST | /api/v1/stream/{stream_id}/sink/{sink_id}/secret/rotate | Rotate Sink Secret |
| GET | /api/v1/stream/{stream_id}/sink/{sink_id}/transformation | Get Sink Transformation |
| PATCH | /api/v1/stream/{stream_id}/sink/{sink_id}/transformation | Set Sink Transformation |

### ingest
| Method | Path | Description |
|--------|------|-------------|
| GET | /ingest/api/v1/source | List Ingest Sources |
| POST | /ingest/api/v1/source | Create Ingest Source |
| GET | /ingest/api/v1/source/{source_id} | Get Ingest Source |
| PUT | /ingest/api/v1/source/{source_id} | Update Source |
| DELETE | /ingest/api/v1/source/{source_id} | Delete Ingest Source |
| POST | /ingest/api/v1/source/{source_id}/dashboard | Ingest Source Consumer Portal |
| GET | /ingest/api/v1/source/{source_id}/endpoint | List Ingest Endpoints |
| POST | /ingest/api/v1/source/{source_id}/endpoint | Create Ingest Endpoint |
| GET | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id} | Get Ingest Endpoint |
| PUT | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id} | Update Ingest Endpoint |
| DELETE | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id} | Delete Ingest Endpoint |
| GET | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/headers | Get Ingest Endpoint Headers |
| PUT | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/headers | Update Ingest Endpoint Headers |
| GET | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/secret | Get Ingest Endpoint Secret |
| POST | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/secret/rotate | Rotate Ingest Endpoint Secret |
| GET | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/transformation | Get Ingest Endpoint Transformation |
| PATCH | /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/transformation | Patch Ingest Endpoint Transformation |
| POST | /ingest/api/v1/source/{source_id}/token/rotate | Rotate Ingest Token |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my applications?" -> GET /api/v1/app
- "How do I send a webhook message to an app?" -> POST /api/v1/app/{app_id}/msg
- "How do I check if any endpoint is listening for a specific event type?" -> POST /api/v1/app/{app_id}/msg/precheck/active
- "How do I see failed delivery attempts for an endpoint?" -> GET /api/v1/app/{app_id}/attempt/endpoint/{endpoint_id}
- "How do I retry a failed message to a specific endpoint?" -> POST /api/v1/app/{app_id}/msg/{msg_id}/endpoint/{endpoint_id}/resend
- "How do I replay all failed messages from a date range?" -> POST /api/v1/app/{app_id}/endpoint/{endpoint_id}/bulk-replay
- "How do I rotate an endpoint's signing secret?" -> POST /api/v1/app/{app_id}/endpoint/{endpoint_id}/secret/rotate
- "How do I create an app portal session for my customer?" -> POST /api/v1/auth/app-portal-access/{app_id}
- "How do I set up an ingest source to receive external webhooks?" -> POST /ingest/api/v1/source
- "How do I define a new event type with a JSON schema?" -> POST /api/v1/event-type
- "How do I add a transformation to an endpoint?" -> PATCH /api/v1/app/{app_id}/endpoint/{endpoint_id}/transformation
- "How do I check the delivery stats for an endpoint?" -> GET /api/v1/app/{app_id}/endpoint/{endpoint_id}/stats
- "How do I export my environment config (event types, connectors)?" -> POST /api/v1/environment/export
- "How do I poll for events from a stream sink?" -> GET /api/v1/app/{app_id}/poller/{sink_id}
- "How do I monitor background tasks like bulk replays?" -> GET /api/v1/background-task/{task_id}

## Response Tips

- **List endpoints** (apps, endpoints, event-types, streams, sinks, sources): All return `{data, done, iterator, prevIterator}`. Paginate by passing the returned `iterator` value in the next request. Stop when `done: true`. Use `prevIterator` to page backwards.
- **Create/Update endpoints**: POST returns 201 (created) or 200 (already exists when `get_if_exists` is set). PUT returns 200 (updated) or 201 (created). Check the status code to know which happened.
- **Async operations** (bulk-replay, recover, replay-missing, expunge, usage stats): Return 202 with a `{id, status, task}` object. Poll GET /api/v1/background-task/{task_id} to track completion.
- **Delete endpoints**: Return 204 with no body. Any non-204 indicates failure.
- **Error responses**: All endpoints share the same error set (400/401/403/404/409/422/429). 409 signals a conflict (duplicate uid or concurrent update). 422 means valid JSON but failed business validation.
- **Attempt details**: The `msg` field in attempt responses is a fully nested message object with its own `payload`, `eventType`, and `timestamp` - not just an ID reference.

## Anomaly Flags

- **429 responses**: Rate limit hit. Surface immediately with the `Retry-After` header value. The app-level `rateLimit` and `throttleRate` fields control per-app throttling - suggest adjusting if 429s are frequent.
- **Endpoint `disabled: true`**: An endpoint has been disabled, meaning no deliveries will be made. Flag when listing endpoints so the user does not wonder why messages are not arriving.
- **Sink `status: "disabled"` or non-null `failureReason`**: A stream sink has stopped consuming. Surface the `failureReason` and `nextRetryAt` fields so the user can intervene.
- **Event type `deprecated: true` or `archived: true`**: The user is working with event types that are deprecated or archived. Warn before sending messages with these types.
- **High `fail` count in endpoint stats**: When GET .../stats returns a `fail` count significantly exceeding `success`, proactively suggest investigating delivery attempts or running a recover/replay.
- **Background task stuck**: If a polled background task stays in a non-terminal `status` for an extended period, flag it as potentially stalled.
- **Missing `uid` on apps/endpoints**: When `uid` is null, resources can only be referenced by Svix-generated IDs. Recommend setting `uid` for idempotent creates and easier external system mapping.
- **`expunge` flag on event type delete**: Deleting with `expunge=false` (default) only soft-deletes. Surface this distinction so the user understands the event type name remains reserved.

## Playbook

### 1. Set up a new webhook consumer end-to-end

1. Create an application: POST /api/v1/app with `name` and optional `uid`
2. Create an endpoint under that app: POST /api/v1/app/{app_id}/endpoint with the consumer's `url`
3. Optionally filter by event types: include `filterTypes` in the endpoint creation
4. Retrieve the signing secret: GET /api/v1/app/{app_id}/endpoint/{endpoint_id}/secret
5. Share the `key` with the consumer so they can verify webhook signatures
6. Send a test event: POST /api/v1/app/{app_id}/endpoint/{endpoint_id}/send-example with an `eventType`
7. Verify delivery: GET /api/v1/app/{app_id}/attempt/endpoint/{endpoint_id} and confirm a 200 status attempt

### 2. Investigate and recover failed deliveries

1. Check endpoint stats: GET /api/v1/app/{app_id}/endpoint/{endpoint_id}/stats to see fail/success counts
2. List failed attempts: GET /api/v1/app/{app_id}/attempt/endpoint/{endpoint_id} with `status_code_class=400` or `status_code_class=500`
3. Inspect a specific attempt: GET /api/v1/app/{app_id}/msg/{msg_id}/attempt/{attempt_id} to see the `response`, `responseStatusCode`, and `responseDurationMs`
4. Fix the consumer issue (URL, auth headers, server bug)
5. Recover all missed messages: POST /api/v1/app/{app_id}/endpoint/{endpoint_id}/recover with `since` set to when failures started
6. Monitor the background task: GET /api/v1/background-task/{task_id} until `status` is complete

### 3. Set up an ingest source for receiving external webhooks

1. Create an ingest source: POST /ingest/api/v1/source with a `name`
2. Note the `ingestUrl` from the response - this is the URL to give the external provider
3. Create an ingest endpoint to forward received events: POST /ingest/api/v1/source/{source_id}/endpoint with your internal handler `url`
4. Optionally add a transformation: PATCH /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/transformation with `code` and `enabled: true`
5. Optionally set custom headers: PUT /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/headers
6. Configure the external provider to send webhooks to the `ingestUrl`

### 4. Give customers a self-service app portal

1. Ensure the application exists: POST /api/v1/app with `get_if_exists: true` and the customer's `uid`
2. Generate a portal session: POST /api/v1/auth/app-portal-access/{app_id} with desired `expiry` and optional `readOnly` flag
3. Return the `url` from the response to your frontend - this is a pre-authenticated portal URL
4. The customer can now manage their own endpoints, view delivery attempts, and replay failed messages
5. To revoke access: POST /api/v1/auth/app/{app_id}/expire-all to invalidate all active sessions

### 5. Export environment config and import to another org

1. Export the current environment: POST /api/v1/environment/export
2. Save the response containing `eventTypes`, `connectors`, and `settings`
3. Switch authentication to the target organization's Bearer token
4. Import the config: POST /api/v1/environment/import with the exported `eventTypes`, `connectors`, and `settings` arrays
5. Verify by listing event types: GET /api/v1/event-type and connectors: GET /api/v1/connector in the target org


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
