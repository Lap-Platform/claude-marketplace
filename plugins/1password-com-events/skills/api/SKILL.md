---
name: events-api
description: "Events API skill. Use when working with Events for api. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Events API
API version: 1.2.0

## Auth
Bearer bearer

## Base URL
https://events.1password.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/auth/introspect -- verify access
3. POST /api/v1/signinattempts -- create first signinattempts

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/auth/introspect | Performs introspection of the provided Bearer JWT token |
| GET | /api/v2/auth/introspect | Performs introspection of the provided Bearer JWT token |
| POST | /api/v1/signinattempts | Retrieves events for both successful and failed attempts to sign into a 1Password account |
| POST | /api/v1/itemusages | Retrieves events for each usage of an item stored in a shared vault within a 1Password account |
| POST | /api/v1/auditevents | Retrieves audit events for actions performed by team members within a 1Password account |

## Enhanced Skill Content
## Question Mapping

- "What features does my API token have access to?" -> GET /api/v2/auth/introspect
- "Is my bearer token still valid?" -> GET /api/v2/auth/introspect
- "When was my API token issued?" -> GET /api/v2/auth/introspect
- "What is the UUID of my current session?" -> GET /api/v2/auth/introspect
- "Show me recent sign-in attempts" -> POST /api/v1/signinattempts
- "Were there any failed logins recently?" -> POST /api/v1/signinattempts
- "Which items have been accessed or used?" -> POST /api/v1/itemusages
- "Who accessed a specific vault item?" -> POST /api/v1/itemusages
- "Show me the audit log" -> POST /api/v1/auditevents
- "What administrative actions happened today?" -> POST /api/v1/auditevents
- "Has anyone changed permissions recently?" -> POST /api/v1/auditevents
- "Check if my token supports item usage events" -> GET /api/v2/auth/introspect
- "Get sign-in activity for a specific user" -> POST /api/v1/signinattempts
- "What events occurred in my 1Password account this week?" -> POST /api/v1/auditevents

## Response Tips

- **Introspect (v1 vs v2):** v1 uses PascalCase fields (UUID, IssuedAt, Features); v2 uses snake_case (uuid, issued_at, features). Prefer v2 for new integrations. The `features` array indicates which event types the token can query.
- **Event endpoints (signinattempts, itemusages, auditevents):** These are POST because they accept filter/query parameters in the request body, not because they create resources. Expect cursor-based pagination in responses; check for a cursor field to retrieve the next page.
- **Errors:** All endpoints return 401 for invalid/expired tokens and 500 for server errors. There are no 403 or 404 responses -- a 401 means re-authenticate or check token scopes.

## Anomaly Flags

- **401 on introspect:** Token is expired or revoked. Surface immediately -- all subsequent calls will also fail.
- **Empty features array:** Token has no event scopes enabled. Alert the user before they attempt event queries that will fail.
- **500 errors:** 1Password Events API server issue. Recommend retry with backoff; surface if persistent across multiple calls.
- **v1 introspect usage:** Flag that v1 is the legacy endpoint with PascalCase fields. Suggest migrating to v2.
- **Large event volumes:** If event queries return unusually high counts, flag for potential security incident (brute-force sign-ins, bulk item access).
- **Missing event types:** If the user queries signinattempts, itemusages, or auditevents but their token's `features` array does not include the corresponding scope, warn before making the call.

## Playbook

### 1. Validate Token and Check Permissions

1. Call GET /api/v2/auth/introspect with your Bearer token
2. Confirm the response is 200 (not 401)
3. Read the `features` array to see which event types you can query
4. Note the `issued_at` timestamp to verify token freshness
5. Proceed to event queries only for features listed in the response

### 2. Investigate Suspicious Sign-In Activity

1. Call GET /api/v2/auth/introspect to confirm token has sign-in attempt access
2. Call POST /api/v1/signinattempts with date range and optional user filters in the body
3. Review results for failed attempts, unusual locations, or unfamiliar devices
4. If results are paginated, follow the cursor to retrieve all pages
5. Cross-reference suspicious entries with POST /api/v1/auditevents for related admin actions

### 3. Audit Sensitive Item Access

1. Call GET /api/v2/auth/introspect to confirm `itemusages` feature is enabled
2. Call POST /api/v1/itemusages with filters for the vault or item in question
3. Page through all results using the cursor
4. Identify unexpected users or access times
5. If anomalies found, call POST /api/v1/auditevents to check for permission changes around the same timeframe

### 4. Generate a Full Security Report

1. Call GET /api/v2/auth/introspect to verify all three event scopes are available
2. Call POST /api/v1/signinattempts for the reporting period
3. Call POST /api/v1/itemusages for the same period
4. Call POST /api/v1/auditevents for the same period
5. Aggregate and correlate events across all three sources to build a complete activity timeline

### 5. Handle Token Expiry During a Workflow

1. If any call returns 401, stop further event queries immediately
2. Call GET /api/v2/auth/introspect to confirm the token is expired (expect 401)
3. Generate or obtain a new Bearer token from the 1Password admin console
4. Re-run GET /api/v2/auth/introspect with the new token to validate
5. Resume the interrupted workflow from the last successful cursor position


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
