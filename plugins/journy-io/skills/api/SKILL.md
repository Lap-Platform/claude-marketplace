---
name: developer-documentation
description: "Developer documentation API skill. Use when working with Developer documentation for link, events, users. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# Developer documentation
API version: 1.0.0

## Auth
ApiKey (inferred from docs)

## Base URL
https://api.journy.io

## Setup
1. Set your API key in the appropriate header
2. GET /events -- verify access
3. POST /link -- create first link

## Endpoints

16 endpoints across 9 groups. See references/api-spec.lap for full details.

### link
| Method | Path | Description |
|--------|------|-------------|
| POST | /link | Link web activity to user |

### events
| Method | Path | Description |
|--------|------|-------------|
| POST | /events | Track event |
| GET | /events | Get events |

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /users/upsert | Create or update user |
| DELETE | /users | Delete user |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| POST | /accounts/upsert | Create or update account |
| POST | /accounts/users/add | Add users to an account |
| POST | /accounts/users/remove | Remove user from account |
| DELETE | /accounts | Delete account |

### properties
| Method | Path | Description |
|--------|------|-------------|
| GET | /properties/users | Get user properties |
| GET | /properties/accounts | Get account properties |

### validate
| Method | Path | Description |
|--------|------|-------------|
| GET | /validate | Validate API key |

### tracking
| Method | Path | Description |
|--------|------|-------------|
| GET | /tracking/snippet | Get snippet for a website |

### track
| Method | Path | Description |
|--------|------|-------------|
| POST | /track | Track event |

### segments
| Method | Path | Description |
|--------|------|-------------|
| GET | /segments/users | Get user segments |
| GET | /segments/accounts | Get account segments |

## Enhanced Skill Content
## Question Mapping

- "How do I link a device to a user?" -> POST /link
- "How do I track a custom event for a user or account?" -> POST /events
- "What events are available in my workspace?" -> GET /events
- "How do I create or update a user profile?" -> POST /users/upsert
- "How do I delete a user?" -> DELETE /users
- "How do I create or update an account?" -> POST /accounts/upsert
- "How do I add users to an account?" -> POST /accounts/users/add
- "How do I remove users from an account?" -> POST /accounts/users/remove
- "How do I delete an account?" -> DELETE /accounts
- "What custom properties are defined for users?" -> GET /properties/users
- "What custom properties are defined for accounts?" -> GET /properties/accounts
- "How do I check if my API key is valid?" -> GET /validate
- "How do I get the tracking snippet for my website?" -> GET /tracking/snippet
- "How do I log a behavioral event with metadata?" -> POST /track
- "What user segments exist in my workspace?" -> GET /segments/users
- "What account segments exist in my workspace?" -> GET /segments/accounts

## Response Tips

- **Link/Events/Upsert (201):** Success means the resource was created or accepted; response body may be minimal -- rely on the status code, not a returned object.
- **Delete endpoints (202/204):** Deletion is accepted asynchronously (202) or completed with no content (204); do not expect a response body.
- **GET list endpoints (events, properties, segments):** Responses return arrays; check for empty lists rather than null when no data exists.
- **Validate (200):** A 200 confirms the API key is active; any non-200 means the key is invalid or expired.
- **Tracking snippet (200):** Returns embeddable code; a 404 means the domain is not registered in journy.io.
- **All endpoints:** Errors follow a consistent set (400/401/403/429/500); parse the response body for a message field with details.

## Anomaly Flags

- **429 Too Many Requests:** All 16 endpoints can return 429. Surface rate-limit headers (`Retry-After`, `X-RateLimit-Remaining`) proactively and back off before hitting the ceiling.
- **401 vs 403 distinction:** A 401 means the API key is missing or malformed; a 403 means the key is valid but lacks permission for that operation. Flag 403 errors explicitly since they indicate a plan or scope issue, not a typo.
- **202 Accepted on deletes:** Deletion is not immediate. If a caller tries to re-create a resource right after deleting, warn them the delete may still be processing.
- **Dual event endpoints:** Both `POST /events` and `POST /track` accept nearly identical payloads. Flag if a caller uses both for the same event, as this likely causes duplicate tracking.
- **Missing optional metadata:** When `POST /events` or `POST /track` is called without `metadata` or `triggeredAt`, surface a note that the event will lack context and default to server time.
- **500 Internal Server Error:** Present on every endpoint. If seen more than once in a session, recommend checking the journy.io status page.

## Playbook

### 1. Onboard a New Account with Users

1. Call `POST /accounts/upsert` with the account's `domain` or `accountId` and any known properties.
2. Call `POST /users/upsert` for each user, passing `email` and/or `userId` plus profile properties.
3. Call `POST /accounts/users/add` to associate the users with the account in a single batch request.
4. Verify the setup by calling `GET /properties/accounts` and `GET /properties/users` to confirm properties were stored.

### 2. Track a User Event with Full Context

1. Call `GET /validate` to confirm your API key is active.
2. Call `POST /users/upsert` to ensure the user profile exists and is up to date.
3. Call `POST /events` (or `POST /track`) with the user and account identification, event `name`, optional `metadata` object, and `triggeredAt` timestamp.
4. Call `GET /events` to confirm the event type appears in the available events list.

### 3. Remove a User from an Account and Delete Them

1. Call `POST /accounts/users/remove` with the account identification and the user's identification in the `users` array.
2. Wait briefly for the async dissociation to process (202 response).
3. Call `DELETE /users` with the user's identification to remove their profile entirely.
4. Expect a 202; the deletion is asynchronous.

### 4. Set Up Website Tracking

1. Call `GET /validate` to verify the API key.
2. Call `GET /tracking/snippet?domain=example.com` to retrieve the JavaScript snippet for the target domain.
3. If a 404 is returned, the domain must first be registered in the journy.io dashboard.
4. Embed the returned snippet in the site's `<head>` tag.
5. Call `POST /link` with the visitor's `deviceId` and their `email` or `userId` to connect anonymous browsing to a known identity.

### 5. Audit Available Segments and Properties

1. Call `GET /segments/users` to list all user segments defined in the workspace.
2. Call `GET /segments/accounts` to list all account segments.
3. Call `GET /properties/users` to review custom user property definitions.
4. Call `GET /properties/accounts` to review custom account property definitions.
5. Cross-reference segments with properties to verify that segmentation rules reference properties that still exist.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
