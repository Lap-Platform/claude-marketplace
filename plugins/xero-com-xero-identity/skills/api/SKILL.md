---
name: xero-oauth-2-identity-service-api
description: "Xero OAuth 2 Identity Service API skill. Use when working with Xero OAuth 2 Identity Service for Connections. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Xero OAuth 2 Identity Service API
API version: 11.1.0

## Auth
Bearer basic | OAuth2

## Base URL
https://api.xero.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /Connections -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### Connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /Connections | Retrieves the connections for this user |
| DELETE | /Connections/{id} | Deletes a connection for this user (i.e. disconnect a tenant) |

## Enhanced Skill Content
## Question Mapping

- "What Xero organizations am I connected to?" -> GET /Connections
- "List all my Xero tenant connections" -> GET /Connections
- "Which tenants are linked to my OAuth token?" -> GET /Connections
- "Show connections filtered by a specific auth event" -> GET /Connections (with authEventId)
- "What happened after a user authorized my app?" -> GET /Connections (with authEventId from callback)
- "How do I disconnect a Xero organization?" -> DELETE /Connections/{id}
- "Remove a specific tenant connection" -> DELETE /Connections/{id}
- "Revoke access to one of my connected orgs" -> DELETE /Connections/{id}
- "How many Xero orgs does this token have access to?" -> GET /Connections (count results)
- "Get the tenant ID for a specific organization" -> GET /Connections (find by org name in response)
- "Which connection ID corresponds to my company?" -> GET /Connections (match tenantName)
- "Disconnect all organizations except one" -> GET /Connections then DELETE /Connections/{id} for each unwanted
- "Verify my OAuth token still has active connections" -> GET /Connections (check for non-empty response)
- "Clean up stale tenant connections after reauthorization" -> GET /Connections (with authEventId) then DELETE /Connections/{id}

## Response Tips

- **GET /Connections**: Returns a flat array of connection objects -- each contains `id`, `tenantId`, `tenantType`, `tenantName`, and `createdDateUtc`. No pagination; all connections return in a single response. Use `tenantId` as the `Xero-Tenant-Id` header for all subsequent Xero API calls.
- **DELETE /Connections/{id}**: Returns 204 No Content on success with an empty body -- do not attempt to parse a response. A 404 means the connection ID does not exist or was already removed.

## Anomaly Flags

- **Empty connections array**: Token may be expired, revoked, or the user never completed authorization -- surface this immediately and suggest re-initiating the OAuth flow.
- **404 on DELETE**: The connection was already removed or the ID is malformed -- flag as a possible stale reference and recommend refreshing the connections list.
- **Unexpected tenant count change**: If a previously seen tenant disappears from GET /Connections without an explicit DELETE, the user may have revoked access from the Xero side -- alert the user.
- **Missing tenantId in downstream calls**: If the agent is about to call another Xero API without setting `Xero-Tenant-Id`, proactively warn that multi-tenant tokens require this header.
- **OAuth token expiry**: If GET /Connections returns a 401, surface that the access token needs refreshing via the OAuth 2.0 refresh flow before retrying.

## Playbook

### 1. Initial Setup: Discover Available Tenants After OAuth

1. Complete the OAuth 2.0 authorization flow and obtain an access token.
2. Call GET /Connections to retrieve all authorized tenant connections.
3. Store each connection's `id`, `tenantId`, and `tenantName` for later use.
4. Use the `tenantId` value as the `Xero-Tenant-Id` header in all subsequent Xero API calls.

### 2. Disconnect a Specific Organization

1. Call GET /Connections to list all current connections.
2. Identify the target connection by matching `tenantName` or `tenantId`.
3. Call DELETE /Connections/{id} using the connection's `id` (not `tenantId`).
4. Confirm success by checking for a 204 response.
5. Optionally call GET /Connections again to verify the connection was removed.

### 3. Handle Reauthorization and Clean Up Duplicates

1. After a user reauthorizes, capture the `authEventId` from the OAuth callback.
2. Call GET /Connections with the `authEventId` filter to see only newly created connections.
3. Call GET /Connections without filters to see all connections, including any prior ones.
4. Compare the two lists -- if duplicate tenants exist, DELETE the older connection IDs.
5. Update your local tenant mapping with the fresh connection IDs.

### 4. Multi-Tenant Routing for API Calls

1. Call GET /Connections to retrieve all available tenants.
2. Present the list of `tenantName` values to the user for selection.
3. Map the user's choice to the corresponding `tenantId`.
4. Set the `Xero-Tenant-Id` header to that `tenantId` for all subsequent API requests.
5. If a downstream call returns 403, re-check connections -- the tenant may have been disconnected.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
