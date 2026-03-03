---
name: svix-api
description: "Svix API skill. Use when working with Svix for api, ingest. Covers 127 endpoints."
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

127 endpoints across 2 groups. See references/api-spec.lap for full details.

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
- "Why is my endpoint not receiving webhooks?" -> GET /api/v1/app/{app_id}/endpoint/{endpoint_id}/stats
- "How do I retry failed webhook deliveries since yesterday?" -> POST /api/v1/app/{app_id}/endpoint/{endpoint_id}/recover
- "What delivery attempts were made for a specific message?" -> GET /api/v1/app/{app_id}/attempt/msg/{msg_id}
- "How do I create an app and register an endpoint for it?" -> POST /api/v1/app then POST /api/v1/app/{app_id}/endpoint
- "How do I rotate the signing secret for an endpoint?" -> POST /api/v1/app/{app_id}/endpoint/{endpoint_id}/secret/rotate
- "How do I set up event type filtering on an endpoint?" -> PATCH /api/v1/app/{app_id}/endpoint/{endpoint_id} (set filterTypes)
- "How do I check the status of a background task like bulk replay?" -> GET /api/v1/background-task/{task_id}
- "How do I give my customer access to the app portal?" -> POST /api/v1/auth/app-portal-access/{app_id}
- "How do I define a new event type with a JSON schema?" -> POST /api/v1/event-type
- "How do I set up an operational webhook to monitor my Svix environment?" -> POST /api/v1/operational-webhook/endpoint
- "How do I create a stream and add a sink to consume events?" -> POST /api/v1/stream then POST /api/v1/stream/{stream_id}/sink
- "How do I configure an ingest source to receive third-party webhooks?" -> POST /ingest/api/v1/source
- "How do I export my entire environment config for staging?" -> POST /api/v1/environment/export

## Response Tips

- **List endpoints** (apps, endpoints, messages, event types, streams, sinks, sources): All return `{data, done, iterator, prevIterator}`. Page forward by passing `iterator` from the response; stop when `done: true`. Use `prevIterator` to page backward.
- **Create/update endpoints**: Return the full resource object on success (201 or 200). PUT may return 200 (updated) or 201 (created) -- check the status code to distinguish upsert behavior.
- **Delete endpoints**: Return 204 with no body. A subsequent GET returning 404 confirms deletion.
- **Async operations** (recover, bulk-replay, replay-missing, expunge, usage stats): Return 202 with `{id, status, task}`. Poll `GET /api/v1/background-task/{task_id}` to track completion.
- **Auth/portal access**: Returns `{token, url}` -- the `url` is a ready-to-use portal link with the token embedded; `token` alone can be used with the Svix SDKs.
- **Headers endpoints**: Return `{headers, sensitive}` where `sensitive` is a list of header names whose values are masked.
- **Error responses**: All endpoints share the same error codes (400 validation, 401 unauthenticated, 403 forbidden, 404 not found, 409 conflict, 422 unprocessable, 429 rate limited). 413 only appears on message creation (payload too large).

## Anomaly Flags

- **429 responses**: Rate limit hit. Surface the `Retry-After` header value and recommend backing off. If recurring, suggest adjusting `rateLimit`/`throttleRate` on the app or endpoint.
- **Endpoint stats showing high fail count**: When `fail` significantly exceeds `success` in endpoint stats, flag the endpoint as potentially misconfigured or the target URL as unreachable.
- **Disabled endpoints**: When listing or fetching endpoints, flag any where `disabled: true` -- these silently drop deliveries.
- **Deprecated event types**: When `deprecated: true` appears on an event type, warn that it may be removed in a future version.
- **Sink failure state**: When a sink's `status` is not "enabled" or `failureReason` is non-null, surface it -- the sink has stopped consuming events.
- **Null signing secret**: If `GET .../secret` returns a null or empty `key`, warn that webhook signature verification is not possible.
- **Background tasks stuck**: If a background task stays in a non-terminal status for an extended period, flag it for investigation.
- **413 on message creation**: Payload exceeds size limits. Surface the payload size and recommend reducing it or adjusting `payloadRetentionPeriod`.

## Playbook

### 1. Set Up a New Webhook Consumer

1. Create an application: `POST /api/v1/app` with `{name: "My Customer"}`. Note the returned `id`.
2. Register an endpoint: `POST /api/v1/app/{app_id}/endpoint` with `{url: "https://customer.com/webhook"}`. Optionally set `filterTypes` to limit which event types are delivered.
3. Retrieve the signing secret: `GET /api/v1/app/{app_id}/endpoint/{endpoint_id}/secret`. Share the `key` with the consumer for signature verification.
4. Send a test event: `POST /api/v1/app/{app_id}/endpoint/{endpoint_id}/send-example` with `{eventType: "invoice.paid"}`.
5. Verify delivery: `GET /api/v1/app/{app_id}/attempt/endpoint/{endpoint_id}` to confirm a successful attempt (status 200).

### 2. Diagnose and Recover Failed Deliveries

1. Check endpoint health: `GET /api/v1/app/{app_id}/endpoint/{endpoint_id}/stats` to see fail/success/pending counts.
2. List failed attempts: `GET /api/v1/app/{app_id}/attempt/endpoint/{endpoint_id}` with `status_code_class=400` or `status_code_class=500`.
3. Inspect a specific attempt: `GET /api/v1/app/{app_id}/msg/{msg_id}/attempt/{attempt_id}` to see the response body and duration.
4. Fix the endpoint URL or target server issue.
5. Recover missed messages: `POST /api/v1/app/{app_id}/endpoint/{endpoint_id}/recover` with `{since: "2026-03-01T00:00:00Z"}` to replay all failed messages since that timestamp.
6. Monitor the background task: `GET /api/v1/background-task/{task_id}` until `status` shows completion.

### 3. Configure Event Types and Connectors

1. Define event types: `POST /api/v1/event-type` with `{name: "order.created", description: "Fired when a new order is placed"}`. Include `schemas` for payload validation.
2. Optionally import from OpenAPI: `POST /api/v1/event-type/import/openapi` with `{specRaw: "...", dryRun: true}` to preview changes, then repeat with `dryRun: false`.
3. Create a connector: `POST /api/v1/connector` with `{name: "Slack Notifier", transformation: "...", kind: "Slack"}`. The transformation code maps your event payloads to the connector format.
4. Export the full config: `POST /api/v1/environment/export` to capture event types, connectors, and settings for environment replication.
5. Import into another environment: `POST /api/v1/environment/import` with the exported payload.

### 4. Set Up Streaming with Polling Consumers

1. Create a stream: `POST /api/v1/stream` with `{name: "event-stream"}`.
2. Create a sink on the stream: `POST /api/v1/stream/{stream_id}/sink` with `{batchSize: 50, eventTypes: ["order.*"]}`.
3. Get a poller token: `GET /api/v1/auth/stream/{stream_id}/sink/{sink_id}/poller/token`.
4. Poll for events: `GET /api/v1/app/{app_id}/poller/{sink_id}` (or use a consumer ID for competing consumers via `GET .../poller/{sink_id}/consumer/{consumer_id}`). Pass the `iterator` from each response to get the next batch.
5. Seek to a point in time if needed: `POST .../consumer/{consumer_id}/seek` with `{after: "2026-03-01T00:00:00Z"}`.

### 5. Set Up Ingest for Receiving Third-Party Webhooks

1. Create an ingest source: `POST /ingest/api/v1/source` with `{name: "Stripe Ingest"}`. Note the returned `ingestUrl` -- this is the URL you give to the third-party provider.
2. Add a destination endpoint: `POST /ingest/api/v1/source/{source_id}/endpoint` with `{url: "https://your-app.com/handler"}`.
3. Optionally add a transformation: `PATCH /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/transformation` with `{code: "function handler(input) { ... }", enabled: true}`.
4. Configure custom headers if needed: `PUT /ingest/api/v1/source/{source_id}/endpoint/{endpoint_id}/headers` with `{headers: {"X-Custom": "value"}}`.
5. Rotate the ingest token periodically: `POST /ingest/api/v1/source/{source_id}/token/rotate` to get a fresh `ingestUrl`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
