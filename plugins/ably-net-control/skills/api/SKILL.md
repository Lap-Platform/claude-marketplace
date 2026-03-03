---
name: control-api-v1
description: "Control API v1 API skill. Use when working with Control API v1 for accounts, apps, me. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# Control API v1
API version: 1.0.32

## Auth
Bearer bearer

## Base URL
https://control.ably.net/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /me -- verify access
3. POST /accounts/{account_id}/apps -- create first apps

## Endpoints

22 endpoints across 3 groups. See references/api-spec.lap for full details.

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts/{account_id}/apps | Lists account apps |
| POST | /accounts/{account_id}/apps | Creates an app |

### apps
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /apps/{id} | Updates an app |
| DELETE | /apps/{id} | Deletes an app |
| POST | /apps/{id}/pkcs12 | Updates app's APNs info from a `.p12` file |
| GET | /apps/{app_id}/keys | Lists app keys |
| POST | /apps/{app_id}/keys | Creates a key |
| PATCH | /apps/{app_id}/keys/{key_id} | Updates a key |
| POST | /apps/{app_id}/keys/{key_id}/revoke | Revokes a key |
| GET | /apps/{app_id}/namespaces | Lists namespaces |
| POST | /apps/{app_id}/namespaces | Creates a namespace |
| PATCH | /apps/{app_id}/namespaces/{namespace_id} | Updates a namespace |
| DELETE | /apps/{app_id}/namespaces/{namespace_id} | Deletes a namespace |
| GET | /apps/{app_id}/queues | Lists queues |
| POST | /apps/{app_id}/queues | Creates a queue |
| DELETE | /apps/{app_id}/queues/{queue_id} | Deletes a queue |
| GET | /apps/{app_id}/rules | Lists rules |
| POST | /apps/{app_id}/rules | Creates a rule |
| GET | /apps/{app_id}/rules/{rule_id} | Gets a rule using a rule ID |
| PATCH | /apps/{app_id}/rules/{rule_id} | Updates a Rule |
| DELETE | /apps/{app_id}/rules/{rule_id} | Deletes a rule |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /me | Get token details |

## Enhanced Skill Content
## Question Mapping

- "What apps exist in my account?" -> GET /accounts/{account_id}/apps
- "Create a new Ably app" -> POST /accounts/{account_id}/apps
- "How do I rename or disable an app?" -> PATCH /apps/{id}
- "Delete an app I no longer need" -> DELETE /apps/{id}
- "List all API keys for an app" -> GET /apps/{app_id}/keys
- "Create a new API key with specific capabilities" -> POST /apps/{app_id}/keys
- "Update permissions on an existing key" -> PATCH /apps/{app_id}/keys/{key_id}
- "Revoke a compromised API key" -> POST /apps/{app_id}/keys/{key_id}/revoke
- "What namespaces are configured for my app?" -> GET /apps/{app_id}/namespaces
- "Set up a persisted namespace with push notifications" -> POST /apps/{app_id}/namespaces
- "List message queues for an app" -> GET /apps/{app_id}/queues
- "Create an AMQP/STOMP queue in a specific region" -> POST /apps/{app_id}/queues
- "What integration rules are active on my app?" -> GET /apps/{app_id}/rules
- "Who am I authenticated as and what can I do?" -> GET /me
- "Upload a PKCS12 certificate for APNs push" -> POST /apps/{id}/pkcs12

## Response Tips

- **Accounts/Apps:** List endpoints return arrays directly (not wrapped in a data key). App objects include `_links` for HATEOAS navigation; check `status` field for enabled/disabled state.
- **Keys:** `key` field in creation response is the full API key string -- store it immediately, it may not be retrievable later. `capability` is a map of channel-resource to permission arrays. `created`/`modified` are Unix timestamps.
- **Namespaces:** Boolean-heavy responses with sensible defaults. `batchingInterval` is in milliseconds. A 204 on delete means success with no body.
- **Queues:** Deeply nested response: `amqp` and `stomp` contain connection URIs, `messages` has ready/unacknowledged/total counts, `stats` has rate metrics. Nullable fields (marked `?`) may be absent when queue is new.
- **Rules:** Creation and listing return opaque rule objects -- the spec does not constrain the shape, so inspect the response to discover rule-type-specific fields.
- **Errors:** 422 indicates validation failure (bad field values, not missing fields). 504 on key/namespace/queue/rule endpoints signals upstream timeout -- safe to retry. 503 on queues means the queue backend is temporarily unavailable.

## Anomaly Flags

- **504 Gateway Timeout** on key, namespace, queue, or rule endpoints: upstream dependency is slow; surface this to the user and suggest retry after a brief wait.
- **503 Service Unavailable** on queue endpoints: the queue subsystem is degraded; alert the user that queue operations may fail temporarily.
- **422 Unprocessable Entity** on app or key creation: usually indicates a capability map or field value the API rejects; surface the response body for specifics.
- **App status not "enabled"**: after PATCH or creation, if `status` is anything other than the expected value, flag it -- the app may be suspended or disabled.
- **Key revocation succeeded but key still listed**: after revoking a key, a subsequent GET /keys that still shows `status: 0` for the revoked key warrants a warning -- propagation may be delayed.
- **Missing `_links` in app response**: nullable field; if absent, HATEOAS navigation is unavailable for that app, which may indicate a legacy or restricted account.
- **Queue `deadletter: true` with null `deadletterId`**: a dead-letter queue is enabled but not linked -- messages that exceed TTL or maxLength will be lost.

## Playbook

### 1. Provision a New App with API Keys

1. Call GET /me to confirm your identity and retrieve your `account.id`.
2. Call POST /accounts/{account_id}/apps with `name` and optionally `tlsOnly: true`.
3. Note the returned `id` -- this is your `app_id`.
4. Call POST /apps/{app_id}/keys with a `name` and `capability` map (e.g., `{"*": ["publish", "subscribe"]}`).
5. Store the `key` value from the 201 response securely.

### 2. Set Up a Persisted Channel Namespace with Push

1. Call GET /apps/{app_id}/namespaces to see existing namespaces.
2. Call POST /apps/{app_id}/namespaces with `id` (namespace prefix), `persisted: true`, `persistLast: true`, and `pushEnabled: true`.
3. Verify the 201 response confirms all flags are set as expected.
4. If push requires APNs, call POST /apps/{id}/pkcs12 to upload the certificate bundle.

### 3. Create a Message Queue and Wire an Integration Rule

1. Call POST /apps/{app_id}/queues with `name`, `ttl`, `maxLength`, and `region`.
2. Note the returned `amqp.uri` and `stomp.uri` for consumer configuration.
3. Call POST /apps/{app_id}/rules to create an integration rule that routes messages to the queue (include rule-type-specific configuration in the body).
4. Verify with GET /apps/{app_id}/rules to confirm the rule is active.

### 4. Rotate a Compromised API Key

1. Call GET /apps/{app_id}/keys to list all keys and identify the compromised key's `key_id`.
2. Call POST /apps/{app_id}/keys/{key_id}/revoke to immediately disable the key.
3. Call POST /apps/{app_id}/keys with the same `name` and `capability` to issue a replacement.
4. Update your application configuration with the new `key` value from the 201 response.
5. Verify with GET /apps/{app_id}/keys that the old key shows revoked status and the new key is active.

### 5. Audit and Clean Up Unused Resources

1. Call GET /me to get your account ID.
2. Call GET /accounts/{account_id}/apps to list all apps.
3. For each app, call GET /apps/{app_id}/keys, GET /apps/{app_id}/rules, and GET /apps/{app_id}/queues in parallel.
4. Identify apps with no keys, no rules, and no queues -- these are candidates for removal.
5. Call DELETE /apps/{id} for each confirmed unused app (204 confirms deletion).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
