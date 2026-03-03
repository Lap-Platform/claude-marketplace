---
name: planetscale-api
description: "PlanetScale API skill. Use when working with PlanetScale for organizations, regions, user. Covers 148 endpoints."
version: 1.0.0
generator: lapsh
---

# PlanetScale API
API version: v1

## Auth
OAuth2

## Base URL
https://api.planetscale.com/v1

## Setup
1. Configure auth: OAuth2
2. GET /organizations -- verify access
3. POST /organizations/{organization}/databases -- create first databases

## Endpoints

148 endpoints across 3 groups. See references/api-spec.lap for full details.

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations | List organizations |
| GET | /organizations/{organization} | Get an organization |
| PATCH | /organizations/{organization} | Update an organization |
| GET | /organizations/{organization}/audit-log | List audit logs |
| GET | /organizations/{organization}/cluster-size-skus | List available cluster sizes |
| GET | /organizations/{organization}/databases | List databases |
| POST | /organizations/{organization}/databases | Create a database |
| GET | /organizations/{organization}/databases/{database} | Get a database |
| PATCH | /organizations/{organization}/databases/{database} | Update database settings |
| DELETE | /organizations/{organization}/databases/{database} | Delete a database |
| GET | /organizations/{organization}/databases/{database}/branches | List branches |
| POST | /organizations/{organization}/databases/{database}/branches | Create a branch |
| GET | /organizations/{organization}/databases/{database}/branches/{branch} | Get a branch |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch} | Update a branch |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch} | Delete a branch |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/backups | List backups |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/backups | Create a backup |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/backups/{id} | Get a backup |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch}/backups/{id} | Update a backup |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/backups/{id} | Delete a backup |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/bouncer-resizes | Get bouncer resize requests |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/bouncers | List bouncers |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/bouncers | Create a bouncer |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/bouncers/{bouncer} | Get a bouncer |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/bouncers/{bouncer} | Delete a bouncer |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/bouncers/{bouncer}/resizes | Get bouncer resize requests |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch}/bouncers/{bouncer}/resizes | Upsert a bouncer resize request |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/bouncers/{bouncer}/resizes | Cancel a resize request |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/changes | Get branch change requests |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch}/changes | Upsert a change request |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/changes/{id} | Get a branch change request |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch}/cluster | Change a branch cluster configuration |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/demote | Demote a branch |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/extensions | List cluster extensions |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/keyspaces | Get keyspaces |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/keyspaces | Create a keyspace |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/keyspaces/{keyspace} | Get a keyspace |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch}/keyspaces/{keyspace} | Configure keyspace settings |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/keyspaces/{keyspace} | Delete a keyspace |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/keyspaces/{keyspace}/rollout-status | Get keyspace rollout status |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/keyspaces/{keyspace}/vschema | Get the VSchema for the keyspace |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch}/keyspaces/{keyspace}/vschema | Update the VSchema for the keyspace |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/parameters | List cluster parameters |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/passwords | List passwords |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/passwords | Create a password |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/passwords/{id} | Get a password |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch}/passwords/{id} | Update a password |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/passwords/{id} | Delete a password |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/passwords/{id}/renew | Renew a password |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/promote | Promote a branch |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/query-patterns | List generated query patterns reports |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/query-patterns | Create a new query patterns report |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/query-patterns/{id} | Show the status of a query patterns report |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/query-patterns/{id} | Delete a query patterns report |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/query-patterns/{id}/download | Download a finished query patterns report |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/resizes | Cancel a change request |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/roles | List roles |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/roles | Create role credentials |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/roles/default | Get the default postgres role |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/roles/reset-default | Reset default credentials |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/roles/{id} | Get a role |
| PATCH | /organizations/{organization}/databases/{database}/branches/{branch}/roles/{id} | Update role name |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/roles/{id} | Delete role credentials |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/roles/{id}/reassign | Reassign objects owned by one role to another role |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/roles/{id}/renew | Renew role expiration |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/roles/{id}/reset | Reset a role's password |
| POST | /organizations/{organization}/databases/{database}/branches/{branch}/safe-migrations | Enable safe migrations for a branch |
| DELETE | /organizations/{organization}/databases/{database}/branches/{branch}/safe-migrations | Disable safe migrations for a branch |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/schema | Get a branch schema |
| GET | /organizations/{organization}/databases/{database}/branches/{branch}/schema/lint | Lint a branch schema |
| GET | /organizations/{organization}/databases/{database}/cidrs | List IP restriction entries |
| POST | /organizations/{organization}/databases/{database}/cidrs | Create an IP restriction entry |
| GET | /organizations/{organization}/databases/{database}/cidrs/{id} | Get an IP restriction entry |
| PUT | /organizations/{organization}/databases/{database}/cidrs/{id} | Update an IP restriction entry |
| DELETE | /organizations/{organization}/databases/{database}/cidrs/{id} | Delete an IP restriction entry |
| GET | /organizations/{organization}/databases/{database}/deploy-queue | Get the deploy queue |
| GET | /organizations/{organization}/databases/{database}/deploy-requests | List deploy requests |
| POST | /organizations/{organization}/databases/{database}/deploy-requests | Create a deploy request |
| GET | /organizations/{organization}/databases/{database}/deploy-requests/{number} | Get a deploy request |
| PATCH | /organizations/{organization}/databases/{database}/deploy-requests/{number} | Close a deploy request |
| POST | /organizations/{organization}/databases/{database}/deploy-requests/{number}/apply-deploy | Complete a gated deploy request |
| PUT | /organizations/{organization}/databases/{database}/deploy-requests/{number}/auto-apply | Update auto-apply for deploy request |
| PUT | /organizations/{organization}/databases/{database}/deploy-requests/{number}/auto-delete-branch | Update auto-delete branch for deploy request |
| POST | /organizations/{organization}/databases/{database}/deploy-requests/{number}/cancel | Cancel a queued deploy request |
| POST | /organizations/{organization}/databases/{database}/deploy-requests/{number}/complete-deploy | Complete an errored deploy |
| POST | /organizations/{organization}/databases/{database}/deploy-requests/{number}/deploy | Queue a deploy request |
| GET | /organizations/{organization}/databases/{database}/deploy-requests/{number}/deployment | Get a deployment |
| GET | /organizations/{organization}/databases/{database}/deploy-requests/{number}/operations | List deploy operations |
| POST | /organizations/{organization}/databases/{database}/deploy-requests/{number}/revert | Complete a revert |
| GET | /organizations/{organization}/databases/{database}/deploy-requests/{number}/reviews | List deploy request reviews |
| POST | /organizations/{organization}/databases/{database}/deploy-requests/{number}/reviews | Review a deploy request |
| POST | /organizations/{organization}/databases/{database}/deploy-requests/{number}/skip-revert | Skip revert period |
| GET | /organizations/{organization}/databases/{database}/deploy-requests/{number}/throttler | Get deploy request throttler configurations |
| PATCH | /organizations/{organization}/databases/{database}/deploy-requests/{number}/throttler | Update deploy request throttler configurations |
| GET | /organizations/{organization}/databases/{database}/read-only-regions | List read-only regions |
| GET | /organizations/{organization}/databases/{database}/regions | List database regions |
| GET | /organizations/{organization}/databases/{database}/schema-recommendations | List schema recommendations |
| GET | /organizations/{organization}/databases/{database}/schema-recommendations/{number} | Get a schema recommendation |
| POST | /organizations/{organization}/databases/{database}/schema-recommendations/{number}/dismiss | Dismiss a schema recommendation |
| GET | /organizations/{organization}/databases/{database}/throttler | Get database throttler configurations |
| PATCH | /organizations/{organization}/databases/{database}/throttler | Update database throttler configurations |
| GET | /organizations/{organization}/databases/{database}/webhooks | List webhooks |
| POST | /organizations/{organization}/databases/{database}/webhooks | Create a webhook |
| GET | /organizations/{organization}/databases/{database}/webhooks/{id} | Get a webhook |
| PATCH | /organizations/{organization}/databases/{database}/webhooks/{id} | Update a webhook |
| DELETE | /organizations/{organization}/databases/{database}/webhooks/{id} | Delete a webhook |
| POST | /organizations/{organization}/databases/{database}/webhooks/{id}/test | Test a webhook |
| GET | /organizations/{organization}/databases/{database}/workflows | List workflows |
| POST | /organizations/{organization}/databases/{database}/workflows | Create a workflow |
| GET | /organizations/{organization}/databases/{database}/workflows/{number} | Get a workflow |
| DELETE | /organizations/{organization}/databases/{database}/workflows/{number} | Cancel a workflow |
| PATCH | /organizations/{organization}/databases/{database}/workflows/{number}/complete | Complete a workflow |
| PATCH | /organizations/{organization}/databases/{database}/workflows/{number}/cutover | Cutover traffic |
| PATCH | /organizations/{organization}/databases/{database}/workflows/{number}/retry | Retry a failed workflow |
| PATCH | /organizations/{organization}/databases/{database}/workflows/{number}/reverse-cutover | Reverse traffic cutover |
| PATCH | /organizations/{organization}/databases/{database}/workflows/{number}/reverse-traffic | Reverse traffic |
| PATCH | /organizations/{organization}/databases/{database}/workflows/{number}/switch-primaries | Switch primary traffic |
| PATCH | /organizations/{organization}/databases/{database}/workflows/{number}/switch-replicas | Switch replica traffic |
| PATCH | /organizations/{organization}/databases/{database}/workflows/{number}/verify-data | Verify workflow data |
| GET | /organizations/{organization}/invoices | Get invoices |
| GET | /organizations/{organization}/invoices/{id} | Get an invoice |
| GET | /organizations/{organization}/invoices/{id}/line-items | Get invoice line items |
| GET | /organizations/{organization}/members | List organization members |
| GET | /organizations/{organization}/members/{id} | Get an organization member |
| PATCH | /organizations/{organization}/members/{id} | Update organization member role |
| DELETE | /organizations/{organization}/members/{id} | Remove a member from an organization |
| GET | /organizations/{organization}/oauth-applications | List OAuth applications |
| GET | /organizations/{organization}/oauth-applications/{application_id} | Get an OAuth application |
| GET | /organizations/{organization}/oauth-applications/{application_id}/tokens | List OAuth tokens |
| GET | /organizations/{organization}/oauth-applications/{application_id}/tokens/{token_id} | Get an OAuth token |
| DELETE | /organizations/{organization}/oauth-applications/{application_id}/tokens/{token_id} | Delete an OAuth token |
| POST | /organizations/{organization}/oauth-applications/{id}/token | Create or renew an OAuth token |
| GET | /organizations/{organization}/regions | List regions for an organization |
| GET | /organizations/{organization}/service-tokens | List service tokens |
| POST | /organizations/{organization}/service-tokens | Create a service token |
| GET | /organizations/{organization}/service-tokens/{id} | Get a service token |
| DELETE | /organizations/{organization}/service-tokens/{id} | Delete a service token |
| GET | /organizations/{organization}/teams | List teams in an organization |
| POST | /organizations/{organization}/teams | Create an organization team |
| GET | /organizations/{organization}/teams/{team} | Get an organization team |
| PATCH | /organizations/{organization}/teams/{team} | Update an organization team |
| DELETE | /organizations/{organization}/teams/{team} | Delete an organization team |
| GET | /organizations/{organization}/teams/{team}/members | List team members |
| POST | /organizations/{organization}/teams/{team}/members | Add a member to a team |
| GET | /organizations/{organization}/teams/{team}/members/{id} | Get a team member |
| DELETE | /organizations/{organization}/teams/{team}/members/{id} | Remove a member from a team |

### regions
| Method | Path | Description |
|--------|------|-------------|
| GET | /regions | List public regions |

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user | Get current user |

## Enhanced Skill Content
## Question Mapping

- "What organizations do I belong to?" -> GET /organizations
- "Show me details about my organization" -> GET /organizations/{organization}
- "List all databases in my org" -> GET /organizations/{organization}/databases
- "Create a new database" -> POST /organizations/{organization}/databases
- "What branches exist on my database?" -> GET /organizations/{organization}/databases/{database}/branches
- "Create a development branch from main" -> POST /organizations/{organization}/databases/{database}/branches
- "How do I deploy schema changes?" -> POST /organizations/{organization}/databases/{database}/deploy-requests
- "What's the status of my deploy request?" -> GET /organizations/{organization}/databases/{database}/deploy-requests/{number}
- "Generate a connection password for a branch" -> POST /organizations/{organization}/databases/{database}/branches/{branch}/passwords
- "Who are the members of my organization?" -> GET /organizations/{organization}/members
- "Show my recent invoices" -> GET /organizations/{organization}/invoices
- "What regions are available?" -> GET /regions
- "Who am I authenticated as?" -> GET /user
- "List backups for my production branch" -> GET /organizations/{organization}/databases/{database}/branches/{branch}/backups
- "What schema recommendations exist for my database?" -> GET /organizations/{organization}/databases/{database}/schema-recommendations

## Response Tips

- **Paginated lists** (databases, branches, members, invoices, deploy-requests): Check for `page` and `per_page` params; iterate with `page=1,2,...` until results are empty. Default page size varies by endpoint.
- **CRUD resources** (branches, passwords, roles, webhooks, CIDRs): 201 on create, 200 on read/update, 204 on delete (empty body). Always confirm 204 means success, not missing data.
- **Deploy requests**: Stateful resource -- watch the `state` field across GET calls after triggering apply/deploy/revert/cancel actions. Operations sub-endpoint gives granular step tracking.
- **Workflows** (data migrations): Multi-phase lifecycle -- use cutover, reverse-cutover, switch-primaries, switch-replicas, verify-data endpoints sequentially. Each PATCH returns the updated workflow state.
- **Errors**: All endpoints share the same error shape (401 unauthorized, 403 forbidden, 404 not found, 500 server error). Some CIDR and team endpoints also return 400/422 for validation failures.
- **OAuth tokens**: POST to `.../token` returns the raw token value only once -- store it immediately as it cannot be retrieved again.

## Anomaly Flags

- **401 on any call**: OAuth token may be expired or revoked. Surface immediately and suggest re-authentication.
- **403 after successful auth**: The authenticated user/service-token lacks permission for this org or database. Flag the specific resource and suggest checking role assignments.
- **422 on password or VSchema updates**: Input validation failure. Surface the response body which typically contains field-level error details.
- **204 from PATCH on branch changes**: This endpoint can return either 200 or 204. A 204 means no actionable diff was found -- flag this so the user knows the change was a no-op.
- **Deploy request stuck in non-terminal state**: If a deploy request remains in a non-complete/non-cancelled state across multiple checks, surface it as potentially stalled and suggest checking the operations sub-endpoint.
- **302 on query pattern download**: This is a redirect to a signed URL, not an error. Agents should follow the redirect transparently.
- **Backup state filtering**: When listing backups, if `state` filter returns zero results but unfiltered returns many, flag that no backups match the requested state (e.g., no completed backups).
- **Service token creation**: The token value is only returned on creation (POST). Flag this to the user so they save it before moving on.

## Playbook

### 1. Create a Database and Connect to It

1. GET /organizations to find your organization name
2. POST /organizations/{organization}/databases with `{"name": "my-app-db", "cluster_size": "..."}` -- note the database name from the 201 response
3. GET /organizations/{organization}/databases/{database}/branches to confirm the default `main` branch exists
4. POST /organizations/{organization}/databases/{database}/branches/main/passwords to generate connection credentials
5. Store the returned password immediately (it will not be shown again)
6. Use the host, username, and password from the response to connect via your MySQL client

### 2. Branch-Based Schema Change Workflow

1. POST /organizations/{organization}/databases/{database}/branches to create a dev branch (e.g., `{"name": "add-users-table", "parent_branch": "main"}`)
2. Connect to the new branch and apply your DDL changes directly
3. POST /organizations/{organization}/databases/{database}/deploy-requests with `{"branch": "add-users-table", "into_branch": "main"}`
4. GET /organizations/{organization}/databases/{database}/deploy-requests/{number} to review the schema diff
5. POST /organizations/{organization}/databases/{database}/deploy-requests/{number}/deploy to begin deployment
6. Poll GET /organizations/{organization}/databases/{database}/deploy-requests/{number} until state is `complete`
7. DELETE /organizations/{organization}/databases/{database}/branches/add-users-table to clean up the dev branch

### 3. Rotate a Branch Password

1. GET /organizations/{organization}/databases/{database}/branches/{branch}/passwords to list current passwords
2. POST /organizations/{organization}/databases/{database}/branches/{branch}/passwords to create a new password -- save the returned credentials immediately
3. Update your application configuration to use the new credentials
4. Verify connectivity with the new password
5. DELETE /organizations/{organization}/databases/{database}/branches/{branch}/passwords/{id} using the old password's ID to revoke it

### 4. Set Up a Deploy Webhook for Notifications

1. POST /organizations/{organization}/databases/{database}/webhooks with your endpoint URL and desired events in the body
2. GET /organizations/{organization}/databases/{database}/webhooks/{id} to confirm it was created
3. POST /organizations/{organization}/databases/{database}/webhooks/{id}/test to send a test payload and verify your receiver works
4. If the test fails, PATCH /organizations/{organization}/databases/{database}/webhooks/{id} to update the URL or config, then re-test

### 5. Manage Organization Teams and Access

1. POST /organizations/{organization}/teams with `{"name": "backend-team"}` to create a team
2. GET /organizations/{organization}/members to find member IDs you want to add
3. POST /organizations/{organization}/teams/{team}/members with the member ID to add them to the team
4. PATCH /organizations/{organization}/members/{id} to adjust individual member roles if needed
5. To revoke access: DELETE /organizations/{organization}/teams/{team}/members/{id} to remove from team, or DELETE /organizations/{organization}/members/{id} to remove from the org entirely


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
