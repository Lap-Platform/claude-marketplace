---
name: gateway-rest-api
description: "Gateway REST API skill. Use when working with Gateway REST for tyk. Covers 18 endpoints."
version: 1.0.0
generator: lapsh
---

# Gateway REST API
API version: 1.9

## Auth
ApiKey keyId in path

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /tyk/keys/ -- verify access
3. POST /tyk/keys/create -- create first create

## Endpoints

18 endpoints across 1 groups. See references/api-spec.lap for full details.

### tyk
| Method | Path | Description |
|--------|------|-------------|
| GET | /tyk/keys/ | Gets a list of *key* IDs (will only work with non-hashed installations) |
| POST | /tyk/keys/create | Create a new *API token* with the *session object* defined in the body |
| PUT | /tyk/keys/{keyId} | Update an *API token* with the *session object* defined in the body, this operatin overwrites the existing object |
| POST | /tyk/keys/{keyId} | Add a pre-specified *API token* with the *session object* defined in the body, this operatin creates a custom token that dsoes not use the gateway naming convention for tokens |
| DELETE | /tyk/keys/{keyId} | Remove this *API token* from the gateway, this will completely destroy the token and metadata associated with the token and instantly stop access from being granted |
| GET | /tyk/apis/ | Gets a list of *API Definition* objects that are currently live on the gateway |
| POST | /tyk/apis/ | Create an *API Definition* object |
| GET | /tyk/apis/{apiID} | Gets an *API Definition* object, if it exists |
| DELETE | /tyk/apis/{apiID} | Deletes an *API Definition* object, if it exists |
| PUT | /tyk/apis/{apiID} | Updates an *API Definition* object, if it exists |
| GET | /tyk/health/ | Gets the health check values for an API if it is being recorded |
| GET | /tyk/reload/ | Will reload the targetted gateway |
| GET | /tyk/reload/group | Will reload the cluster via the targeted gateway |
| POST | /tyk/oauth/clients/create | Create a new OAuth client |
| DELETE | /tyk/oauth/clients/{apiId}/{clientId} | Delete the OAuth client |
| GET | /tyk/oauth/clients/{apiId} | Get a list of OAuth clients bound to this back end |
| POST | /tyk/oauth/authorize-client/ | The final request from an authorising party for a redirect URI during the Tyk OAuth flow |
| DELETE | /tyk/oauth/refresh/{keyId} | Invalidate a refresh token |

## Enhanced Skill Content
## Question Mapping

- "How do I list all API keys?" -> GET /tyk/keys/
- "How do I create a new API key?" -> POST /tyk/keys/create
- "How do I update an existing key's session data?" -> PUT /tyk/keys/{keyId}
- "How do I delete an API key?" -> DELETE /tyk/keys/{keyId}
- "What APIs are configured on the gateway?" -> GET /tyk/apis/
- "How do I register a new API definition?" -> POST /tyk/apis/
- "How do I get details for a specific API?" -> GET /tyk/apis/{apiID}
- "How do I remove an API from the gateway?" -> DELETE /tyk/apis/{apiID}
- "How do I update an existing API definition?" -> PUT /tyk/apis/{apiID}
- "How do I check the health of an API?" -> GET /tyk/health/
- "How do I reload the gateway configuration?" -> GET /tyk/reload/
- "How do I reload all gateways in a cluster?" -> GET /tyk/reload/group
- "How do I create an OAuth client for an API?" -> POST /tyk/oauth/clients/create
- "How do I list OAuth clients for an API?" -> GET /tyk/oauth/clients/{apiId}
- "How do I revoke an OAuth client's refresh token?" -> DELETE /tyk/oauth/refresh/{keyId}

## Response Tips

- **Keys endpoints**: All return 200; create/update responses include the key identifier and session object. List requires `api_id` to scope results.
- **APIs endpoints**: Responses contain full `api_definition` maps. List returns an array; single-fetch returns one definition object.
- **Health endpoint**: Returns upstream latency and request-count metrics scoped to the given `api_id`.
- **Reload endpoints**: Return a status message confirming reload. `/reload/group` fans out to all nodes; expect slightly longer response times.
- **OAuth endpoints**: Client create returns client credentials (id + secret). Authorize-client returns a redirect payload with the authorization code or token.

## Anomaly Flags

- **Missing `x-tyk-authorization` header**: Nearly every endpoint requires it. Surface immediately if the caller omits it or receives 401/403.
- **Reload not called after changes**: API or key mutations do not take effect until `/tyk/reload/` is called. Flag when create/update/delete is performed without a follow-up reload.
- **`suppress_reset` usage**: When set on key create/update, quota counters are not reset. Flag if a user sets this unintentionally, as it can cause stale rate-limit state.
- **OAuth client deletion without token revocation**: Deleting an OAuth client does not automatically revoke issued tokens. Surface when `/oauth/clients/{apiId}/{clientId}` DELETE is called without prior refresh-token cleanup.
- **Health endpoint scoped to single API**: `/tyk/health/` requires `api_id`. If the user wants cluster-wide health, they need to iterate over all APIs -- flag this gap.

## Playbook

### 1. Register a New API and Make It Live

1. POST /tyk/apis/ with the `api_definition` map (name, target URL, auth config, version settings)
2. Note the `apiID` from the response
3. GET /tyk/reload/ to apply the new configuration
4. GET /tyk/apis/{apiID} to verify the API is registered and active
5. GET /tyk/health/ with the new `api_id` to confirm upstream connectivity

### 2. Create and Manage API Keys

1. POST /tyk/keys/create with a `session_object` defining access rights, rate limits, and quota
2. Store the returned key securely
3. GET /tyk/keys/ with `api_id` to list all keys and confirm creation
4. PUT /tyk/keys/{keyId} to update session data (e.g., change rate limits)
5. GET /tyk/reload/ to ensure changes propagate

### 3. Set Up OAuth for an API

1. GET /tyk/apis/{apiID} to confirm the API exists and has OAuth enabled in its definition
2. POST /tyk/oauth/clients/create with the `oauth_client` map (redirect URIs, policy ID)
3. Store the returned `client_id` and `client_secret`
4. POST /tyk/oauth/authorize-client/ with `response_type`, `client_id`, `redirect_uri`, and `key_rules` to generate an authorization code or token
5. To revoke access later: DELETE /tyk/oauth/refresh/{keyId} then DELETE /tyk/oauth/clients/{apiId}/{clientId}

### 4. Safely Remove an API

1. GET /tyk/keys/ with `api_id` to list all keys tied to the API
2. DELETE /tyk/keys/{keyId} for each key (with `api_id` parameter)
3. GET /tyk/oauth/clients/{apiId} to list OAuth clients
4. DELETE /tyk/oauth/clients/{apiId}/{clientId} for each client
5. DELETE /tyk/apis/{apiID} to remove the API definition
6. GET /tyk/reload/ to apply the removal across the gateway

### 5. Rolling Cluster Reload After Bulk Changes

1. Make all required changes (create/update/delete APIs and keys)
2. GET /tyk/reload/group to trigger a reload across all gateway nodes simultaneously
3. GET /tyk/apis/ to verify all API definitions reflect the expected state
4. GET /tyk/health/ for critical APIs to confirm upstream health post-reload


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
