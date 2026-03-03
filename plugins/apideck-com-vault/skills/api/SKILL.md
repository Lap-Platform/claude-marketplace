---
name: vault-api
description: "Vault API skill. Use when working with Vault for vault. Covers 33 endpoints."
version: 1.0.0
generator: lapsh
---

# Vault API
API version: 10.24.0

## Auth
ApiKey Authorization in header | ApiKey x-apideck-app-id in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /vault/consumers -- verify access
3. POST /vault/consumers -- create first consumers

## Endpoints

33 endpoints across 1 groups. See references/api-spec.lap for full details.

### vault
| Method | Path | Description |
|--------|------|-------------|
| POST | /vault/consumers | Create consumer |
| GET | /vault/consumers | Get all consumers |
| GET | /vault/consumers/{consumer_id} | Get consumer |
| PATCH | /vault/consumers/{consumer_id} | Update consumer |
| DELETE | /vault/consumers/{consumer_id} | Delete consumer |
| GET | /vault/consumers/{consumer_id}/stats | Consumer request counts |
| GET | /vault/connections | Get all connections |
| GET | /vault/connections/{unified_api}/{service_id} | Get connection |
| POST | /vault/connections/{unified_api}/{service_id} | Create connection |
| PATCH | /vault/connections/{unified_api}/{service_id} | Update connection |
| DELETE | /vault/connections/{unified_api}/{service_id} | Deletes a connection |
| POST | /vault/connections/{unified_api}/{service_id}/import | Import connection |
| POST | /vault/connections/{unified_api}/{service_id}/token | Authorize Access Token |
| POST | /vault/connections/{unified_api}/{service_id}/validate | Validate Connection State |
| GET | /vault/connections/{unified_api}/{service_id}/consent | Get consent records |
| PATCH | /vault/connections/{unified_api}/{service_id}/consent | Update consent state |
| POST | /vault/connections/{unified_api}/{service_id}/callback-state | Create Callback State |
| GET | /vault/connections/{unified_api}/{service_id}/{resource}/config | Get resource settings |
| PATCH | /vault/connections/{unified_api}/{service_id}/{resource}/config | Update settings |
| GET | /vault/connections/{unified_api}/{service_id}/{resource}/schema | Get resource schema |
| GET | /vault/connections/{unified_api}/{service_id}/{resource}/example | Get resource example |
| GET | /vault/connections/{unified_api}/{service_id}/{resource}/custom-fields | Get resource custom fields |
| GET | /vault/connections/{unified_api}/{service_id}/{resource}/custom-mappings | List connection custom mappings |
| GET | /vault/authorize/{service_id}/{application_id} | Authorize |
| GET | /vault/revoke/{service_id}/{application_id} | Revoke connection |
| GET | /vault/custom-mappings/{unified_api}/{service_id}/{target_field_id} | Get custom mapping |
| POST | /vault/custom-mappings/{unified_api}/{service_id}/{target_field_id} | Create custom mapping |
| PATCH | /vault/custom-mappings/{unified_api}/{service_id}/{target_field_id} | Update custom mapping |
| DELETE | /vault/custom-mappings/{unified_api}/{service_id}/{target_field_id} | Deletes a custom mapping |
| GET | /vault/custom-mappings/{unified_api}/{service_id} | List custom mappings |
| GET | /vault/callback | Callback |
| POST | /vault/sessions | Create Session |
| GET | /vault/logs | Get all consumer request logs |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new consumer?" -> POST /vault/consumers
- "List all consumers in my application" -> GET /vault/consumers
- "Get details for a specific consumer" -> GET /vault/consumers/{consumer_id}
- "How do I update a consumer's metadata?" -> PATCH /vault/consumers/{consumer_id}
- "Delete a consumer and all their data" -> DELETE /vault/consumers/{consumer_id}
- "Show API usage stats for a consumer over a date range" -> GET /vault/consumers/{consumer_id}/stats
- "What integrations does a consumer have connected?" -> GET /vault/connections
- "Check the health status of a specific connection" -> GET /vault/connections/{unified_api}/{service_id}
- "How do I import existing OAuth credentials into a connection?" -> POST /vault/connections/{unified_api}/{service_id}/import
- "Validate whether a connection's credentials still work" -> POST /vault/connections/{unified_api}/{service_id}/validate
- "Create a Vault session so a user can manage integrations in the UI" -> POST /vault/sessions
- "How do I start the OAuth flow for a service?" -> GET /vault/authorize/{service_id}/{application_id}
- "Map a custom field from a downstream service to a unified field" -> POST /vault/custom-mappings/{unified_api}/{service_id}/{target_field_id}
- "View all custom field mappings for a connection" -> GET /vault/custom-mappings/{unified_api}/{service_id}
- "Get the schema for a specific resource on a connection" -> GET /vault/connections/{unified_api}/{service_id}/{resource}/schema

## Response Tips

- **Consumers (list):** Cursor-paginated via `meta.cursors.next`; pass it as `cursor` param. Default page size is 20. Check `meta.items_on_page` to detect the last page.
- **Connections:** Not paginated -- returns all connections in a flat `data` array. Filter server-side with `api` and `configured` query params rather than client-side.
- **Connection detail:** Deeply nested object. Key fields: `data.state` (lifecycle), `data.health` (credential status), `data.integration_state` (config readiness). `form_fields` contains the dynamic settings UI schema.
- **Sessions:** Returns `session_uri` (redirect URL for hosted Vault UI) and `session_token`. Both are short-lived -- generate on demand, do not cache.
- **Logs:** Cursor-paginated like consumers. Use `filter` map for server-side narrowing before pagination.
- **All endpoints:** Wrap responses in `{status_code, status, data}`. The optional `_raw` field contains the unmodified downstream response when raw mode is enabled. Errors share codes 400/401/402/404/422 across all endpoints -- distinguish by reading `status` and `detail` in the error body.

## Anomaly Flags

- **Connection health degraded:** Surface immediately when `data.health` is `revoked`, `missing_settings`, `needs_consent`, `needs_auth`, or `pending_refresh` -- these mean the integration is broken or about to break.
- **Credentials expiring soon:** Flag when `credentials_expire_at` is within 24 hours of the current time. Suggest triggering a token refresh via POST .../token.
- **Last refresh failed:** If `last_refresh_failed_at` is non-zero, the automatic token refresh is failing. Alert the user to re-authorize.
- **Consent state requires action:** When `consent_state` is `pending`, `denied`, `revoked`, or `requires_reconsent`, the connection cannot fully operate. Prompt for consent update via PATCH .../consent.
- **402 Payment Required:** This error across all endpoints indicates a plan limit. Surface the specific resource that triggered it so the user can upgrade or reduce usage.
- **Deprecated form fields:** When iterating `form_fields`, flag any entry where `deprecated: true` -- the user should migrate to the replacement field before it is removed.
- **High request counts:** When `aggregated_request_count` in consumer stats spikes significantly versus prior periods, alert to potential runaway integrations.

## Playbook

### 1. Onboard a New Consumer and Connect Their First Integration

1. POST /vault/consumers with `consumer_id` and optional `metadata` (account name, email).
2. POST /vault/sessions with the new `consumer_id` to generate a hosted Vault session.
3. Redirect the user to `session_uri` so they can browse and authorize integrations in the Vault UI.
4. GET /vault/connections with `x-apideck-consumer-id` to confirm the connection was added.
5. POST /vault/connections/{unified_api}/{service_id}/validate to verify credentials are working.

### 2. Import Existing OAuth Credentials for a Connection

1. GET /vault/connections/{unified_api}/{service_id} to check current connection state.
2. POST /vault/connections/{unified_api}/{service_id}/import with `credentials` (access_token, refresh_token, expires_in) and any required `settings`.
3. POST /vault/connections/{unified_api}/{service_id}/validate to confirm the imported credentials are valid.
4. GET /vault/connections/{unified_api}/{service_id} again and verify `health` is `ok` and `state` is `callable`.

### 3. Set Up Custom Field Mappings for a Resource

1. GET /vault/connections/{unified_api}/{service_id}/{resource}/custom-fields to discover available downstream fields.
2. GET /vault/connections/{unified_api}/{service_id}/{resource}/schema to understand the unified schema and identify target field IDs.
3. POST /vault/custom-mappings/{unified_api}/{service_id}/{target_field_id} with `value` set to the downstream field path.
4. GET /vault/custom-mappings/{unified_api}/{service_id} to verify all mappings are in place.
5. GET /vault/connections/{unified_api}/{service_id}/{resource}/example to confirm the mapping produces expected data.

### 4. Monitor Consumer Usage and Connection Health

1. GET /vault/consumers to list all active consumers (paginate with `cursor` if needed).
2. For each consumer, GET /vault/consumers/{consumer_id}/stats with `start_datetime` and `end_datetime` to pull usage metrics.
3. GET /vault/connections with `x-apideck-consumer-id` for each consumer to enumerate their integrations.
4. Check each connection's `health` field -- flag any that are not `ok`.
5. GET /vault/logs with appropriate `filter` to investigate any connections showing errors.

### 5. Handle Consent Management for a Connection

1. GET /vault/connections/{unified_api}/{service_id} and check `consent_state`.
2. If state is `pending`, `requires_reconsent`, or `denied`, GET .../consent to see current consent details and required resources.
3. PATCH /vault/connections/{unified_api}/{service_id}/consent with `granted: true` and the `resources` list the consumer agrees to.
4. GET /vault/connections/{unified_api}/{service_id} to confirm `consent_state` is now `granted` and `health` is `ok`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
