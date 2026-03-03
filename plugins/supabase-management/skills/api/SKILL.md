---
name: supabase-api-v1
description: "Supabase API (v1) API skill. Use when working with Supabase API (v1) for branches, projects, organizations. Covers 158 endpoints."
version: 1.0.0
generator: lapsh
---

# Supabase API (v1)
API version: 1.0.0

## Auth
Bearer bearer

## Base URL
Not specified.

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/projects -- verify access
3. POST /v1/branches/{branch_id_or_ref}/push -- create first push

## Endpoints

158 endpoints across 5 groups. See references/api-spec.lap for full details.

### branches
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/branches/{branch_id_or_ref} | Get database branch config |
| PATCH | /v1/branches/{branch_id_or_ref} | Update database branch config |
| DELETE | /v1/branches/{branch_id_or_ref} | Delete a database branch |
| POST | /v1/branches/{branch_id_or_ref}/push | Pushes a database branch |
| POST | /v1/branches/{branch_id_or_ref}/merge | Merges a database branch |
| POST | /v1/branches/{branch_id_or_ref}/reset | Resets a database branch |
| POST | /v1/branches/{branch_id_or_ref}/restore | Restore a scheduled branch deletion |
| GET | /v1/branches/{branch_id_or_ref}/diff | [Beta] Diffs a database branch |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/projects | List all projects |
| POST | /v1/projects | Create a project |
| GET | /v1/projects/available-regions | [Beta] Gets the list of available regions that can be used for a new project |
| GET | /v1/projects/{ref}/actions | List all action runs |
| HEAD | /v1/projects/{ref}/actions | Count the number of action runs |
| GET | /v1/projects/{ref}/actions/{run_id} | Get the status of an action run |
| PATCH | /v1/projects/{ref}/actions/{run_id}/status | Update the status of an action run |
| GET | /v1/projects/{ref}/actions/{run_id}/logs | Get the logs of an action run |
| GET | /v1/projects/{ref}/api-keys | Get project api keys |
| POST | /v1/projects/{ref}/api-keys | Creates a new API key for the project |
| GET | /v1/projects/{ref}/api-keys/legacy | Check whether JWT based legacy (anon, service_role) API keys are enabled. This API endpoint will be removed in the future, check for HTTP 404 Not Found. |
| PUT | /v1/projects/{ref}/api-keys/legacy | Disable or re-enable JWT based legacy (anon, service_role) API keys. This API endpoint will be removed in the future, check for HTTP 404 Not Found. |
| PATCH | /v1/projects/{ref}/api-keys/{id} | Updates an API key for the project |
| GET | /v1/projects/{ref}/api-keys/{id} | Get API key |
| DELETE | /v1/projects/{ref}/api-keys/{id} | Deletes an API key for the project |
| GET | /v1/projects/{ref}/branches | List all database branches |
| POST | /v1/projects/{ref}/branches | Create a database branch |
| DELETE | /v1/projects/{ref}/branches | Disables preview branching |
| GET | /v1/projects/{ref}/branches/{name} | Get a database branch |
| GET | /v1/projects/{ref}/custom-hostname | [Beta] Gets project's custom hostname config |
| DELETE | /v1/projects/{ref}/custom-hostname | [Beta] Deletes a project's custom hostname configuration |
| POST | /v1/projects/{ref}/custom-hostname/initialize | [Beta] Updates project's custom hostname configuration |
| POST | /v1/projects/{ref}/custom-hostname/reverify | [Beta] Attempts to verify the DNS configuration for project's custom hostname configuration |
| POST | /v1/projects/{ref}/custom-hostname/activate | [Beta] Activates a custom hostname for a project. |
| GET | /v1/projects/{ref}/jit-access | [Beta] Get project's just-in-time access configuration. |
| PUT | /v1/projects/{ref}/jit-access | [Beta] Update project's just-in-time access configuration. |
| POST | /v1/projects/{ref}/network-bans/retrieve | [Beta] Gets project's network bans |
| POST | /v1/projects/{ref}/network-bans/retrieve/enriched | [Beta] Gets project's network bans with additional information about which databases they affect |
| DELETE | /v1/projects/{ref}/network-bans | [Beta] Remove network bans. |
| GET | /v1/projects/{ref}/network-restrictions | [Beta] Gets project's network restrictions |
| PATCH | /v1/projects/{ref}/network-restrictions | [Alpha] Updates project's network restrictions by adding or removing CIDRs |
| POST | /v1/projects/{ref}/network-restrictions/apply | [Beta] Updates project's network restrictions |
| GET | /v1/projects/{ref}/pgsodium | [Beta] Gets project's pgsodium config |
| PUT | /v1/projects/{ref}/pgsodium | [Beta] Updates project's pgsodium config. Updating the root_key can cause all data encrypted with the older key to become inaccessible. |
| GET | /v1/projects/{ref}/postgrest | Gets project's postgrest config |
| PATCH | /v1/projects/{ref}/postgrest | Updates project's postgrest config |
| GET | /v1/projects/{ref} | Gets a specific project that belongs to the authenticated user |
| DELETE | /v1/projects/{ref} | Deletes the given project |
| PATCH | /v1/projects/{ref} | Updates the given project |
| GET | /v1/projects/{ref}/secrets | List all secrets |
| POST | /v1/projects/{ref}/secrets | Bulk create secrets |
| DELETE | /v1/projects/{ref}/secrets | Bulk delete secrets |
| GET | /v1/projects/{ref}/ssl-enforcement | [Beta] Get project's SSL enforcement configuration. |
| PUT | /v1/projects/{ref}/ssl-enforcement | [Beta] Update project's SSL enforcement configuration. |
| GET | /v1/projects/{ref}/types/typescript | Generate TypeScript types |
| GET | /v1/projects/{ref}/vanity-subdomain | [Beta] Gets current vanity subdomain config |
| DELETE | /v1/projects/{ref}/vanity-subdomain | [Beta] Deletes a project's vanity subdomain configuration |
| POST | /v1/projects/{ref}/vanity-subdomain/check-availability | [Beta] Checks vanity subdomain availability |
| POST | /v1/projects/{ref}/vanity-subdomain/activate | [Beta] Activates a vanity subdomain for a project. |
| POST | /v1/projects/{ref}/upgrade | [Beta] Upgrades the project's Postgres version |
| GET | /v1/projects/{ref}/upgrade/eligibility | [Beta] Returns the project's eligibility for upgrades |
| GET | /v1/projects/{ref}/upgrade/status | [Beta] Gets the latest status of the project's upgrade |
| GET | /v1/projects/{ref}/readonly | Returns project's readonly mode status |
| POST | /v1/projects/{ref}/readonly/temporary-disable | Disables project's readonly mode for the next 15 minutes |
| POST | /v1/projects/{ref}/read-replicas/setup | [Beta] Set up a read replica |
| POST | /v1/projects/{ref}/read-replicas/remove | [Beta] Remove a read replica |
| GET | /v1/projects/{ref}/health | Gets project's service health status |
| POST | /v1/projects/{ref}/config/auth/signing-keys/legacy | Set up the project's existing JWT secret as an in_use JWT signing key. This endpoint will be removed in the future always check for HTTP 404 Not Found. |
| GET | /v1/projects/{ref}/config/auth/signing-keys/legacy | Get the signing key information for the JWT secret imported as signing key for this project. This endpoint will be removed in the future, check for HTTP 404 Not Found. |
| POST | /v1/projects/{ref}/config/auth/signing-keys | Create a new signing key for the project in standby status |
| GET | /v1/projects/{ref}/config/auth/signing-keys | List all signing keys for the project |
| GET | /v1/projects/{ref}/config/auth/signing-keys/{id} | Get information about a signing key |
| DELETE | /v1/projects/{ref}/config/auth/signing-keys/{id} | Remove a signing key from a project. Only possible if the key has been in revoked status for a while. |
| PATCH | /v1/projects/{ref}/config/auth/signing-keys/{id} | Update a signing key, mainly its status |
| GET | /v1/projects/{ref}/config/auth | Gets project's auth config |
| PATCH | /v1/projects/{ref}/config/auth | Updates a project's auth config |
| POST | /v1/projects/{ref}/config/auth/third-party-auth | Creates a new third-party auth integration |
| GET | /v1/projects/{ref}/config/auth/third-party-auth | Lists all third-party auth integrations |
| DELETE | /v1/projects/{ref}/config/auth/third-party-auth/{tpa_id} | Removes a third-party auth integration |
| GET | /v1/projects/{ref}/config/auth/third-party-auth/{tpa_id} | Get a third-party integration |
| POST | /v1/projects/{ref}/pause | Pauses the given project |
| GET | /v1/projects/{ref}/restore | Lists available restore versions for the given project |
| POST | /v1/projects/{ref}/restore | Restores the given project |
| POST | /v1/projects/{ref}/restore/cancel | Cancels the given project restoration |
| GET | /v1/projects/{ref}/billing/addons | List billing addons and compute instance selections |
| PATCH | /v1/projects/{ref}/billing/addons | Apply or update billing addons, including compute instance size |
| DELETE | /v1/projects/{ref}/billing/addons/{addon_variant} | Remove billing addons or revert compute instance sizing |
| GET | /v1/projects/{ref}/claim-token | Gets project claim token |
| POST | /v1/projects/{ref}/claim-token | Creates project claim token |
| DELETE | /v1/projects/{ref}/claim-token | Revokes project claim token |
| GET | /v1/projects/{ref}/advisors/performance | Gets project performance advisors. |
| GET | /v1/projects/{ref}/advisors/security | Gets project security advisors. |
| GET | /v1/projects/{ref}/analytics/endpoints/logs.all | Gets project's logs |
| GET | /v1/projects/{ref}/analytics/endpoints/usage.api-counts | Gets project's usage api counts |
| GET | /v1/projects/{ref}/analytics/endpoints/usage.api-requests-count | Gets project's usage api requests count |
| GET | /v1/projects/{ref}/analytics/endpoints/functions.combined-stats | Gets a project's function combined statistics |
| POST | /v1/projects/{ref}/cli/login-role | [Beta] Create a login role for CLI with temporary password |
| DELETE | /v1/projects/{ref}/cli/login-role | [Beta] Delete existing login roles used by CLI |
| GET | /v1/projects/{ref}/database/migrations | [Beta] List applied migration versions |
| POST | /v1/projects/{ref}/database/migrations | [Beta] Apply a database migration |
| PUT | /v1/projects/{ref}/database/migrations | [Beta] Upsert a database migration without applying |
| DELETE | /v1/projects/{ref}/database/migrations | [Beta] Rollback database migrations and remove them from history table |
| GET | /v1/projects/{ref}/database/migrations/{version} | [Beta] Fetch an existing entry from migration history |
| PATCH | /v1/projects/{ref}/database/migrations/{version} | [Beta] Patch an existing entry in migration history |
| POST | /v1/projects/{ref}/database/query | [Beta] Run sql query |
| POST | /v1/projects/{ref}/database/query/read-only | [Beta] Run a sql query as supabase_read_only_user |
| POST | /v1/projects/{ref}/database/webhooks/enable | [Beta] Enables Database Webhooks on the project |
| GET | /v1/projects/{ref}/database/context | Gets database metadata for the given project. |
| PATCH | /v1/projects/{ref}/database/password | Updates the database password |
| GET | /v1/projects/{ref}/database/jit | Get user-id to role mappings for JIT access |
| POST | /v1/projects/{ref}/database/jit | Authorize user-id to role mappings for JIT access |
| PUT | /v1/projects/{ref}/database/jit | Updates a user mapping for JIT access |
| GET | /v1/projects/{ref}/database/jit/list | List all user-id to role mappings for JIT access |
| DELETE | /v1/projects/{ref}/database/jit/{user_id} | Delete JIT access by user-id |
| GET | /v1/projects/{ref}/functions | List all functions |
| POST | /v1/projects/{ref}/functions | Create a function |
| PUT | /v1/projects/{ref}/functions | Bulk update functions |
| POST | /v1/projects/{ref}/functions/deploy | Deploy a function |
| GET | /v1/projects/{ref}/functions/{function_slug} | Retrieve a function |
| PATCH | /v1/projects/{ref}/functions/{function_slug} | Update a function |
| DELETE | /v1/projects/{ref}/functions/{function_slug} | Delete a function |
| GET | /v1/projects/{ref}/functions/{function_slug}/body | Retrieve a function body |
| GET | /v1/projects/{ref}/storage/buckets | Lists all buckets |
| GET | /v1/projects/{ref}/config/disk | Get database disk attributes |
| POST | /v1/projects/{ref}/config/disk | Modify database disk |
| GET | /v1/projects/{ref}/config/disk/util | Get disk utilization |
| GET | /v1/projects/{ref}/config/disk/autoscale | Gets project disk autoscale config |
| GET | /v1/projects/{ref}/config/storage | Gets project's storage config |
| PATCH | /v1/projects/{ref}/config/storage | Updates project's storage config |
| GET | /v1/projects/{ref}/config/database/pgbouncer | Get project's pgbouncer config |
| GET | /v1/projects/{ref}/config/database/pooler | Gets project's supavisor config |
| PATCH | /v1/projects/{ref}/config/database/pooler | Updates project's supavisor config |
| GET | /v1/projects/{ref}/config/database/postgres | Gets project's Postgres config |
| PUT | /v1/projects/{ref}/config/database/postgres | Updates project's Postgres config |
| GET | /v1/projects/{ref}/config/realtime | Gets realtime configuration |
| PATCH | /v1/projects/{ref}/config/realtime | Updates realtime configuration |
| POST | /v1/projects/{ref}/config/realtime/shutdown | Shutdowns realtime connections for a project |
| POST | /v1/projects/{ref}/config/auth/sso/providers | Creates a new SSO provider |
| GET | /v1/projects/{ref}/config/auth/sso/providers | Lists all SSO providers |
| GET | /v1/projects/{ref}/config/auth/sso/providers/{provider_id} | Gets a SSO provider by its UUID |
| PUT | /v1/projects/{ref}/config/auth/sso/providers/{provider_id} | Updates a SSO provider by its UUID |
| DELETE | /v1/projects/{ref}/config/auth/sso/providers/{provider_id} | Removes a SSO provider by its UUID |
| GET | /v1/projects/{ref}/database/backups | Lists all backups |
| POST | /v1/projects/{ref}/database/backups/restore-pitr | Restores a PITR backup for a database |
| POST | /v1/projects/{ref}/database/backups/restore-point | Initiates a creation of a restore point for a database |
| GET | /v1/projects/{ref}/database/backups/restore-point | Get restore points for project |
| POST | /v1/projects/{ref}/database/backups/undo | Initiates an undo to a given restore point |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/organizations | List all organizations |
| POST | /v1/organizations | Create an organization |
| GET | /v1/organizations/{slug}/members | List members of an organization |
| GET | /v1/organizations/{slug} | Gets information about the organization |
| GET | /v1/organizations/{slug}/project-claim/{token} | Gets project details for the specified organization and claim token |
| POST | /v1/organizations/{slug}/project-claim/{token} | Claims project for the specified organization |
| GET | /v1/organizations/{slug}/projects | Gets all projects for the given organization |

### oauth
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/oauth/authorize | [Beta] Authorize user through oauth |
| POST | /v1/oauth/token | [Beta] Exchange auth code for user's access and refresh token |
| POST | /v1/oauth/revoke | [Beta] Revoke oauth app authorization and it's corresponding tokens |
| GET | /v1/oauth/authorize/project-claim | Authorize user through oauth and claim a project |

### snippets
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/snippets | Lists SQL snippets for the logged in user |
| GET | /v1/snippets/{id} | Gets a specific SQL snippet |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my Supabase projects?" -> GET /v1/projects
- "How do I create a new Supabase project?" -> POST /v1/projects
- "What regions are available for my organization?" -> GET /v1/projects/available-regions
- "How do I check if my project database upgrade is eligible?" -> GET /v1/projects/{ref}/upgrade/eligibility
- "How do I enable Google OAuth for my project?" -> PATCH /v1/projects/{ref}/config/auth
- "How do I create a database branch for preview environments?" -> POST /v1/projects/{ref}/branches
- "How do I deploy an Edge Function?" -> POST /v1/projects/{ref}/functions
- "How do I run a SQL query against my project database?" -> POST /v1/projects/{ref}/database/query
- "How do I set up a custom domain for my project?" -> POST /v1/projects/{ref}/custom-hostname/initialize
- "How do I check my project's health status?" -> GET /v1/projects/{ref}/health
- "How do I rotate my project's API keys?" -> POST /v1/projects/{ref}/api-keys + DELETE /v1/projects/{ref}/api-keys/{id}
- "How do I restore my database from a point-in-time backup?" -> POST /v1/projects/{ref}/database/backups/restore-pitr
- "How do I merge a database branch back into production?" -> POST /v1/branches/{branch_id_or_ref}/merge
- "How do I configure network restrictions to allow only specific IPs?" -> POST /v1/projects/{ref}/network-restrictions/apply
- "How do I generate TypeScript types from my database schema?" -> GET /v1/projects/{ref}/types/typescript

## Response Tips

- **Projects**: `GET /v1/projects` returns a flat array; individual project responses nest database info under `database.host`, `database.version`. Deletion returns minimal `{id, ref, name}` -- not the full object.
- **Branches**: Branch status flows through `CREATING_PROJECT` -> `RUNNING_MIGRATIONS` -> `MIGRATIONS_PASSED` -> `FUNCTIONS_DEPLOYED`. Async operations (push/merge/reset) return a `workflow_run_id` -- poll via `GET /v1/projects/{ref}/actions/{run_id}` for completion.
- **Auth config**: The `GET /config/auth` response is an extremely large flat object (100+ fields). Filter client-side by prefix (`external_github_*`, `sms_*`, `hook_*`) to extract relevant provider or feature config.
- **Organizations**: `GET /v1/organizations/{slug}/projects` is the only paginated endpoint -- uses `offset`/`limit` with a `pagination` envelope containing `count`. All other list endpoints return bare arrays.
- **Snippets**: Uses cursor-based pagination with `cursor` and `limit` params; response includes `data` array and next `cursor` value.
- **Edge Functions**: Timestamps (`created_at`, `updated_at`) are Unix int64, not ISO strings -- unlike every other resource which uses ISO date-time.
- **Errors**: All project-scoped endpoints share a consistent error pattern: 401 (bad token), 403 (insufficient permissions), 429 (rate limited), 500 (server error). Branch-only endpoints skip 401/403/429 and only return 500.
- **OAuth**: Token endpoint returns `expires_in` as seconds; revoke returns 204 with no body.

## Anomaly Flags

- **429 Rate Limit**: Nearly all project endpoints can return 429. Surface rate limit responses immediately and suggest backing off before retrying.
- **Branch migration failures**: If branch status is `MIGRATIONS_FAILED` or `FUNCTIONS_FAILED`, alert the user -- the branch is in a broken state and needs manual intervention or reset.
- **Upgrade eligibility warnings**: When `GET /upgrade/eligibility` returns `eligible: false`, surface `unsupported_extensions`, `objects_to_be_dropped`, and `legacy_auth_custom_roles` -- these are blocking issues the user must resolve.
- **SSL not enforced**: If `GET /ssl-enforcement` returns `database: false`, flag this as a security concern.
- **Security advisor lints**: If `GET /advisors/security` returns non-empty `lints`, proactively summarize the findings.
- **Disk utilization**: If `GET /config/disk/util` shows `fs_used_bytes` approaching `fs_size_bytes` (>85%), alert about impending storage pressure.
- **Readonly mode active**: If `GET /readonly` returns `enabled: true`, warn that writes are blocked and surface `override_active_until` if a temporary disable is in effect.
- **Network bans**: If `POST /network-bans/retrieve` returns a non-empty `banned_ipv4_addresses` list, surface this -- legitimate clients may be getting blocked.
- **Custom hostname verification errors**: If `GET /custom-hostname` response includes non-empty `verification_errors` or SSL `validation_errors`, flag that the domain is not yet active.
- **Branch scheduled for deletion**: If a branch response includes a non-null `deletion_scheduled_at`, alert the user with the deadline.

## Playbook

### 1. Set Up a New Project with GitHub OAuth

1. List organizations: `GET /v1/organizations`
2. Check available regions: `GET /v1/projects/available-regions` with `organization_slug`
3. Create the project: `POST /v1/projects` with `name`, `db_pass`, `organization_slug`, `region`, and `plan`
4. Wait for project status to become active: poll `GET /v1/projects/{ref}` until `status` is ready
5. Enable GitHub OAuth: `PATCH /v1/projects/{ref}/config/auth` with `external_github_enabled: true`, `external_github_client_id`, and `external_github_secret`
6. Set the site URL and redirect allowlist: include `site_url` and `uri_allow_list` in the same PATCH call

### 2. Create and Merge a Database Branch

1. Create a branch: `POST /v1/projects/{ref}/branches` with `branch_name` and optional `git_branch`
2. Get branch connection details: `GET /v1/branches/{branch_id}` -- use `db_host`, `db_port`, `db_user`, `db_pass` to connect
3. Run migrations against the branch database using the connection details
4. Check the diff against production: `GET /v1/branches/{branch_id}/diff`
5. Merge the branch: `POST /v1/branches/{branch_id}/merge` -- capture `workflow_run_id`
6. Monitor merge progress: poll `GET /v1/projects/{ref}/actions/{workflow_run_id}` until all `run_steps` show completion
7. Clean up: `DELETE /v1/branches/{branch_id}`

### 3. Deploy and Update an Edge Function

1. List existing functions: `GET /v1/projects/{ref}/functions`
2. Deploy a new function: `POST /v1/projects/{ref}/functions` with `slug`, `name`, and `body` (the bundled source)
3. Verify deployment: `GET /v1/projects/{ref}/functions/{function_slug}` -- confirm `status` is active
4. To update: `PATCH /v1/projects/{ref}/functions/{function_slug}` with new `body`; optionally toggle `verify_jwt`
5. To roll back or remove: `DELETE /v1/projects/{ref}/functions/{function_slug}`

### 4. Point-in-Time Database Recovery

1. Check backup availability: `GET /v1/projects/{ref}/database/backups` -- note `pitr_enabled` and `earliest_physical_backup_date_unix`/`latest_physical_backup_date_unix`
2. If PITR is not enabled, enable it via addon: `PATCH /v1/projects/{ref}/billing/addons` with `addon_type: "pitr"`
3. Initiate recovery: `POST /v1/projects/{ref}/database/backups/restore-pitr` with `recovery_time_target_unix` (must be within the backup window)
4. Monitor project status: poll `GET /v1/projects/{ref}` until status returns to active
5. If recovery was wrong, undo: `POST /v1/projects/{ref}/database/backups/undo` with the restore point name

### 5. Secure a Project (Network + Auth Hardening)

1. Run security advisor: `GET /v1/projects/{ref}/advisors/security` -- review all lints
2. Enforce SSL: `PUT /v1/projects/{ref}/ssl-enforcement` with `requestedConfig: { database: true }`
3. Restrict database access by IP: `POST /v1/projects/{ref}/network-restrictions/apply` with `dbAllowedCidrs` containing your trusted CIDRs
4. Check for network bans: `POST /v1/projects/{ref}/network-bans/retrieve` and unban any legitimate IPs with `DELETE /v1/projects/{ref}/network-bans`
5. Harden auth settings: `PATCH /v1/projects/{ref}/config/auth` -- set `disable_signup: true` (if invite-only), enable `security_captcha_enabled` with provider and secret, set `password_min_length` to 10+, and enable `password_hibp_enabled`
6. Rotate API keys: create a new key with `POST /v1/projects/{ref}/api-keys`, update your application config, then delete the old key with `DELETE /v1/projects/{ref}/api-keys/{id}`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
