---
name: docker-hub-api
description: "Docker HUB API skill. Use when working with Docker HUB for users, auth, access-tokens. Covers 54 endpoints."
version: 1.0.0
generator: lapsh
---

# Docker HUB API
API version: 2-beta

## Auth
Bearer bearer | Bearer bearer

## Base URL
https://hub.docker.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/access-tokens -- verify access
3. POST /v2/users/login -- create first login

## Endpoints

54 endpoints across 9 groups. See references/api-spec.lap for full details.

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/users/login | Create an authentication token |
| POST | /v2/users/2fa-login | Second factor authentication |

### auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/auth/token | Create access token |

### access-tokens
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/access-tokens | Create personal access token |
| GET | /v2/access-tokens | List personal access tokens |
| PATCH | /v2/access-tokens/{uuid} | Update personal access token |
| GET | /v2/access-tokens/{uuid} | Get personal access token |
| DELETE | /v2/access-tokens/{uuid} | Delete personal access token |

### auditlogs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/auditlogs/{account}/actions | List audit log actions |
| GET | /v2/auditlogs/{account} | List audit log events |

### orgs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/orgs/{name}/settings | Get organization settings |
| PUT | /v2/orgs/{name}/settings | Update organization settings |
| POST | /v2/orgs/{name}/access-tokens | Create access token |
| GET | /v2/orgs/{name}/access-tokens | List access tokens |
| GET | /v2/orgs/{org_name}/access-tokens/{access_token_id} | Get access token |
| PATCH | /v2/orgs/{org_name}/access-tokens/{access_token_id} | Update access token |
| DELETE | /v2/orgs/{org_name}/access-tokens/{access_token_id} | Delete access token |
| GET | /v2/orgs/{org_name}/members | List org members |
| GET | /v2/orgs/{org_name}/members/export | Export org members CSV |
| PUT | /v2/orgs/{org_name}/members/{username} | Update org member (role) |
| DELETE | /v2/orgs/{org_name}/members/{username} | Remove member from org |
| GET | /v2/orgs/{org_name}/invites | List org invites |
| GET | /v2/orgs/{org_name}/groups | Get groups of an organization |
| POST | /v2/orgs/{org_name}/groups | Create a new group |
| GET | /v2/orgs/{org_name}/groups/{group_name} | Get a group of an organization |
| PUT | /v2/orgs/{org_name}/groups/{group_name} | Update the details for an organization group |
| PATCH | /v2/orgs/{org_name}/groups/{group_name} | Update some details for an organization group |
| DELETE | /v2/orgs/{org_name}/groups/{group_name} | Delete an organization group |
| GET | /v2/orgs/{org_name}/groups/{group_name}/members | List members of a group |
| POST | /v2/orgs/{org_name}/groups/{group_name}/members | Add a member to a group |
| DELETE | /v2/orgs/{org_name}/groups/{group_name}/members/{username} | Remove a user from a group |

### namespaces
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/namespaces/{namespace}/repositories/{repository}/tags | List repository tags |
| HEAD | /v2/namespaces/{namespace}/repositories/{repository}/tags | Check repository tags |
| GET | /v2/namespaces/{namespace}/repositories/{repository}/tags/{tag} | Read repository tag |
| HEAD | /v2/namespaces/{namespace}/repositories/{repository}/tags/{tag} | Check repository tag |
| PATCH | /v2/namespaces/{namespace}/repositories/{repository}/immutabletags | Update repository immutable tags |
| POST | /v2/namespaces/{namespace}/repositories/{repository}/immutabletags/verify | Verify repository immutable tags |
| GET | /v2/namespaces/{namespace}/repositories | List repositories in a namespace |
| POST | /v2/namespaces/{namespace}/repositories | Create a new repository |
| GET | /v2/namespaces/{namespace}/repositories/{repository} | Get repository in a namespace |
| HEAD | /v2/namespaces/{namespace}/repositories/{repository} | Check repository in a namespace |

### repositories
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/repositories/{namespace}/{repository}/groups | Assign a group (Team) to a repository for access |

### invites
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /v2/invites/{id} | Cancel an invite |
| PATCH | /v2/invites/{id}/resend | Resend an invite |
| POST | /v2/invites/bulk | Bulk create invites |

### scim
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/scim/2.0/ServiceProviderConfig | Get service provider config |
| GET | /v2/scim/2.0/ResourceTypes | List resource types |
| GET | /v2/scim/2.0/ResourceTypes/{name} | Get a resource type |
| GET | /v2/scim/2.0/Schemas | List schemas |
| GET | /v2/scim/2.0/Schemas/{id} | Get a schema |
| GET | /v2/scim/2.0/Users | List users |
| POST | /v2/scim/2.0/Users | Create user |
| GET | /v2/scim/2.0/Users/{id} | Get a user |
| PUT | /v2/scim/2.0/Users/{id} | Update a user |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with Docker Hub?" -> POST /v2/users/login
- "How do I complete two-factor authentication?" -> POST /v2/users/2fa-login
- "How do I create a personal access token?" -> POST /v2/access-tokens
- "How do I list all my access tokens?" -> GET /v2/access-tokens
- "How do I revoke or delete an access token?" -> DELETE /v2/access-tokens/{uuid}
- "How do I disable a token without deleting it?" -> PATCH /v2/access-tokens/{uuid} (set is_active: false)
- "What repositories exist in a namespace?" -> GET /v2/namespaces/{namespace}/repositories
- "What tags are available for a specific image?" -> GET /v2/namespaces/{namespace}/repositories/{repository}/tags
- "How do I get details about a specific tag including architecture and digest?" -> GET /v2/namespaces/{namespace}/repositories/{repository}/tags/{tag}
- "How do I create a new repository?" -> POST /v2/namespaces/{namespace}/repositories
- "How do I invite users to my organization in bulk?" -> POST /v2/invites/bulk
- "How do I view audit logs for my organization?" -> GET /v2/auditlogs/{account}
- "How do I manage team membership within an org group?" -> POST /v2/orgs/{org_name}/groups/{group_name}/members
- "How do I enable immutable tags on a repository?" -> PATCH /v2/namespaces/{namespace}/repositories/{repository}/immutabletags
- "How do I provision users via SCIM for SSO?" -> POST /v2/scim/2.0/Users

## Response Tips

- **Auth endpoints** (`/users/login`, `/users/2fa-login`, `/auth/token`): Response contains a single token string -- store it immediately as `Bearer` header for all subsequent calls. A 401 means credentials are wrong, not expired.
- **Access tokens** (`/access-tokens`): List responses use cursor pagination (`count`, `next`, `previous`). The `results` array contains token objects. The `active_count` field only appears on the list endpoint, not individual GETs. The `token` secret value is only returned on creation (POST) -- it cannot be retrieved later.
- **Repositories & tags**: Paginated with `page`/`page_size` params. Tag detail responses nest `images` as a map keyed by architecture with deep layer info. `full_size` is the compressed size in bytes. `pull_count` is cumulative and never resets.
- **Org management**: Member/group list endpoints return `count`/`next`/`previous` pagination. Invite list returns `data` array (different key). Export endpoint returns CSV, not JSON.
- **Audit logs**: Returns `logs` array of maps. The actions endpoint returns a flat `actions` map of available action types for filtering. Watch for 429 (rate limit) and 500 (server errors) -- no 401/403 on these endpoints.
- **SCIM**: Follows SCIM 2.0 spec conventions (`startIndex`/`count` pagination, not `page`/`page_size`). Filter parameter uses SCIM filter syntax, not query strings. Returns 409 on duplicate user provisioning.

## Anomaly Flags

- **429 on audit log endpoints**: Rate limit hit -- back off and retry. Surface the retry-after header if present.
- **401 across multiple endpoints in sequence**: Token likely expired or revoked. Prompt re-authentication before continuing.
- **`is_active: false` on access tokens**: Token is disabled. Surface this when a user asks why API calls are failing with a specific token.
- **`last_used: null` on access tokens**: Token has never been used -- may indicate orphaned credentials worth cleaning up.
- **`pull_count: 0` on repositories**: Repository exists but has never been pulled -- could be a placeholder or misconfigured image.
- **`tag_last_pulled: null` with high `full_size`**: Large image tag that nobody is pulling -- potential storage waste.
- **`immutable_tags_settings.enabled: false`**: Repository allows tag overwrites -- flag as a supply chain security risk for production images.
- **SCIM 409 Conflict**: Attempting to provision an already-existing user. Surface the existing user info rather than retrying.
- **`status` field on repository not matching expected values**: Unusual repository state -- surface for investigation.
- **Expired `expires_at` on access tokens**: Token past its expiration date but still listed -- may still be active if the system doesn't auto-revoke.

## Playbook

### 1. Authenticate and Set Up Token-Based Access

1. Call `POST /v2/users/login` with username and password
2. If the response is a 401 with a 2FA challenge, take the `login_2fa_token` from the error response
3. Call `POST /v2/users/2fa-login` with the `login_2fa_token` and the user's TOTP code
4. Store the returned `token` and use it as `Bearer {token}` in the Authorization header for all subsequent requests
5. For long-lived automation, create a personal access token via `POST /v2/access-tokens` with appropriate scopes and an `expires_at` date

### 2. Inventory All Repositories and Their Tags

1. Authenticate (see Playbook 1)
2. Call `GET /v2/namespaces/{namespace}/repositories?page=1&page_size=100` to list repositories
3. Follow `next` pagination links until all repositories are collected
4. For each repository, call `GET /v2/namespaces/{namespace}/repositories/{repository}/tags?page=1&page_size=100`
5. For tags needing architecture details, call `GET /v2/namespaces/{namespace}/repositories/{repository}/tags/{tag}` to get the full manifest with image digests and layer info

### 3. Set Up Organization Team Permissions

1. Authenticate as an org owner
2. Create a group via `POST /v2/orgs/{org_name}/groups` with a descriptive name
3. Add members to the group via `POST /v2/orgs/{org_name}/groups/{group_name}/members` for each user
4. Grant the group access to specific repositories via `POST /v2/repositories/{namespace}/{repository}/groups` with the `group_id` and desired `permission` level (read/write/admin)
5. Verify membership with `GET /v2/orgs/{org_name}/groups/{group_name}/members`

### 4. Bulk Invite and Onboard New Org Members

1. Authenticate as an org owner
2. Optionally do a dry run: `POST /v2/invites/bulk` with `dry_run: true` to validate email addresses
3. Send actual invitations: `POST /v2/invites/bulk` with `org`, `invitees` list, optional `role` and `team`
4. Monitor pending invitations via `GET /v2/orgs/{org_name}/invites`
5. Resend failed or stale invitations with `PATCH /v2/invites/{id}/resend`
6. Remove cancelled invitations with `DELETE /v2/invites/{id}`

### 5. Audit and Rotate Access Tokens

1. List all personal access tokens: `GET /v2/access-tokens?page_size=100`
2. For org tokens, also check: `GET /v2/orgs/{name}/access-tokens?page_size=100`
3. Identify tokens with `last_used: null` or tokens past their `expires_at` -- flag for review
4. Deactivate suspicious tokens: `PATCH /v2/access-tokens/{uuid}` with `is_active: false`
5. Delete confirmed-stale tokens: `DELETE /v2/access-tokens/{uuid}`
6. Create replacement tokens with narrower scopes via `POST /v2/access-tokens`
7. Review the audit log for token usage: `GET /v2/auditlogs/{account}?action=token` to confirm no unauthorized access occurred


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
