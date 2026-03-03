---
name: greenwire-public-api
description: "Greenwire Public API skill. Use when working with Greenwire Public for volunteers, groups, events. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Greenwire Public API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://greenwire.greenpeace.org/api/public

## Setup
1. No auth setup needed
2. GET /volunteers -- verify access

## Endpoints

6 endpoints across 3 groups. See references/api-spec.lap for full details.

### volunteers
| Method | Path | Description |
|--------|------|-------------|
| GET | /volunteers | Gets an array of `Volunteer` object. Mandatory query param of **domain** determines the site / country the volunteers are from. |
| GET | /volunteers/{UUID} | Get one specific `Volunteer` object by specifying its UUID in the url path. |

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups | Gets an array of `Group` object. Mandatory query param of **domain** determines the site / country the group belongs to. |
| GET | /groups/{UUID} | Get one `Group` object by specifying its UUID in the url path. |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Return the upcoming events (e.g. start date >= today). Gets an array of `Event` object. Mandatory query param of **domain** determines the site / country the event belongs to. |
| GET | /events/{UUID} | Get one `Event` object by specifying its UUID in the url path. |

## Enhanced Skill Content
## Question Mapping

- "List all volunteers for a Greenpeace domain?" -> GET /volunteers
- "Get details about a specific volunteer?" -> GET /volunteers/{UUID}
- "How many volunteers are in a domain?" -> GET /volunteers
- "Find volunteers who haven't set a profile picture?" -> GET /volunteers (use must_have_default_avatar)
- "Show me all groups in a domain?" -> GET /groups
- "Get info about a specific group by ID?" -> GET /groups/{UUID}
- "What events are happening in a domain?" -> GET /events
- "Get details for a specific event?" -> GET /events/{UUID}
- "List the first 10 volunteers in a domain?" -> GET /volunteers (use limit)
- "Show a limited number of groups?" -> GET /groups (use limit)
- "Which events are available, limited to 5 results?" -> GET /events (use limit)
- "Look up a volunteer, group, and event by their UUIDs?" -> GET /volunteers/{UUID} + GET /groups/{UUID} + GET /events/{UUID}
- "Browse all community activity for a specific Greenpeace office?" -> GET /volunteers + GET /groups + GET /events (same domain)

## Response Tips

- **List endpoints** (`/volunteers`, `/groups`, `/events`): Expect an array of items. Use `limit` to control result size; omitting it returns defaults set by the server. The `domain` parameter is always required -- omitting it will likely yield an empty or error response.
- **Detail endpoints** (`/{UUID}`): Return a single object. A 400 error means the UUID is malformed or not found -- check formatting (standard UUID v4).
- **General**: All endpoints are read-only (GET). No auth headers are documented, so this is a public-access API. Responses are JSON (200 on success).

## Anomaly Flags

- **400 on detail lookups**: Surface immediately -- likely a malformed UUID. Prompt the user to verify the identifier format.
- **Empty list responses**: If a list endpoint returns zero results, flag that the `domain` value may be incorrect or the domain has no data for that resource type.
- **Missing `domain` parameter**: All list endpoints require `domain`. If the user omits it, warn before making the request rather than letting it fail silently.
- **Unexpectedly large results**: If no `limit` is set and the response is very large, suggest adding a `limit` parameter for future calls.
- **Non-200/400 status codes**: Any 5xx or 403/404 responses are undocumented -- surface these as potential API outages or access changes.

## Playbook

### 1. Survey all activity for a Greenpeace domain

1. Pick the target domain (e.g., `greenpeace.org`).
2. `GET /volunteers?domain={domain}` to list volunteers.
3. `GET /groups?domain={domain}` to list groups.
4. `GET /events?domain={domain}` to list events.
5. Combine results to build a full picture of community activity.

### 2. Look up a specific participant and their context

1. `GET /volunteers/{UUID}` to retrieve the volunteer's profile.
2. Note any group or event references in the response.
3. `GET /groups/{UUID}` for each associated group.
4. `GET /events/{UUID}` for each associated event.

### 3. Browse volunteers with default avatars

1. `GET /volunteers?domain={domain}&must_have_default_avatar=true` to find volunteers who haven't uploaded a profile image.
2. Use `limit` to page through results in manageable batches.
3. Use individual `GET /volunteers/{UUID}` calls to inspect specific profiles.

### 4. Paginate through large result sets

1. Start with `GET /volunteers?domain={domain}&limit=10` (or `/groups`, `/events`).
2. Inspect the response for offset or cursor indicators.
3. Increment the offset or pass the cursor in the next request.
4. Repeat until the response returns fewer items than the limit.

### 5. Validate a UUID before detailed lookup

1. Confirm the identifier matches UUID format (8-4-4-4-12 hex characters).
2. Call `GET /volunteers/{UUID}` (or `/groups/{UUID}`, `/events/{UUID}`).
3. If 400 is returned, re-check the UUID source and retry.
4. On success, extract the needed fields from the detail response.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
