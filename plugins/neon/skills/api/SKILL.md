---
name: neon-api
description: "Neon API skill. Use when working with Neon for projects, api_keys, consumption_history. Covers 138 endpoints."
version: 1.0.0
generator: lapsh
---

# Neon API
API version: v2

## Auth
Bearer bearer | ApiKey zenith in cookie | ApiKey keycloak_token in cookie

## Base URL
https://console.neon.tech/api/v2

## Setup
1. Set Authorization header with your Bearer token
2. GET /api_keys -- verify access
3. POST /api_keys -- create first api_keys

## Endpoints

138 endpoints across 7 groups. See references/api-spec.lap for full details.

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{project_id}/advisors | Get advisor issues |
| GET | /projects/{project_id}/operations/{operation_id} | Retrieve operation details |
| GET | /projects | List projects |
| POST | /projects | Create project |
| GET | /projects/shared | List shared projects |
| GET | /projects/{project_id} | Retrieve project details |
| PATCH | /projects/{project_id} | Update project |
| DELETE | /projects/{project_id} | Delete project |
| POST | /projects/{project_id}/restore | Restore a deleted project |
| POST | /projects/{project_id}/recover | Recover a deleted project |
| GET | /projects/{project_id}/operations | List operations |
| GET | /projects/{project_id}/permissions | List project access |
| POST | /projects/{project_id}/permissions | Grant project access |
| DELETE | /projects/{project_id}/permissions/{permission_id} | Revoke project access |
| GET | /projects/{project_id}/available_preload_libraries | Return available shared preload libraries |
| POST | /projects/{project_id}/transfer_requests | Create a project transfer request |
| PUT | /projects/{project_id}/transfer_requests/{request_id} | Accept a project transfer request |
| GET | /projects/{project_id}/jwks | List JWKS URLs |
| POST | /projects/{project_id}/jwks | Add JWKS URL |
| DELETE | /projects/{project_id}/jwks/{jwks_id} | Delete JWKS URL |
| POST | /projects/{project_id}/branches/{branch_id}/data-api/{database_name} | Create Neon Data API |
| PATCH | /projects/{project_id}/branches/{branch_id}/data-api/{database_name} | Update Neon Data API |
| DELETE | /projects/{project_id}/branches/{branch_id}/data-api/{database_name} | Delete Neon Data API |
| GET | /projects/{project_id}/branches/{branch_id}/data-api/{database_name} | Get Neon Data API |
| POST | /projects/auth/create | Create Neon Auth integration |
| GET | /projects/{project_id}/branches/{branch_id}/auth | Get details of Neon Auth for the branch |
| POST | /projects/{project_id}/branches/{branch_id}/auth | Enable Neon Auth for the branch |
| DELETE | /projects/{project_id}/branches/{branch_id}/auth | Disables Neon Auth for the branch |
| GET | /projects/{project_id}/auth/domains | List domains in redirect_uri whitelist |
| POST | /projects/{project_id}/auth/domains | Add domain to redirect_uri whitelist |
| DELETE | /projects/{project_id}/auth/domains | Delete domain from redirect_uri whitelist |
| GET | /projects/{project_id}/branches/{branch_id}/auth/domains | List domains in redirect_uri whitelist |
| POST | /projects/{project_id}/branches/{branch_id}/auth/domains | Add domain to redirect_uri whitelist |
| DELETE | /projects/{project_id}/branches/{branch_id}/auth/domains | Delete domain from redirect_uri whitelist |
| POST | /projects/auth/keys | Create Auth Provider SDK keys |
| POST | /projects/auth/user | Create new auth user |
| POST | /projects/{project_id}/branches/{branch_id}/auth/users | Create new auth user |
| DELETE | /projects/{project_id}/branches/{branch_id}/auth/users/{auth_user_id} | Delete auth user |
| PUT | /projects/{project_id}/branches/{branch_id}/auth/users/{auth_user_id}/role | Update auth user role |
| DELETE | /projects/{project_id}/auth/users/{auth_user_id} | Delete auth user |
| POST | /projects/auth/transfer_ownership | Transfer Neon-managed auth project to your own account |
| GET | /projects/{project_id}/auth/integrations | Lists active integrations with auth providers |
| GET | /projects/{project_id}/auth/oauth_providers | List OAuth providers |
| POST | /projects/{project_id}/auth/oauth_providers | Add a OAuth provider |
| GET | /projects/{project_id}/branches/{branch_id}/auth/oauth_providers | List OAuth providers for neon auth for a branch |
| POST | /projects/{project_id}/branches/{branch_id}/auth/oauth_providers | Add a OAuth provider |
| PATCH | /projects/{project_id}/auth/oauth_providers/{oauth_provider_id} | Update OAuth provider |
| DELETE | /projects/{project_id}/auth/oauth_providers/{oauth_provider_id} | Delete OAuth provider |
| PATCH | /projects/{project_id}/branches/{branch_id}/auth/oauth_providers/{oauth_provider_id} | Update OAuth provider |
| DELETE | /projects/{project_id}/branches/{branch_id}/auth/oauth_providers/{oauth_provider_id} | Delete OAuth provider |
| GET | /projects/{project_id}/auth/email_server | Get email server configuration |
| PATCH | /projects/{project_id}/auth/email_server | Update email server configuration |
| POST | /projects/{project_id}/branches/{branch_id}/auth/send_test_email | Send test email |
| GET | /projects/{project_id}/branches/{branch_id}/auth/email_and_password | Get email and password configuration |
| PATCH | /projects/{project_id}/branches/{branch_id}/auth/email_and_password | Update email and password configuration |
| GET | /projects/{project_id}/branches/{branch_id}/auth/email_provider | Get email provider configuration |
| PATCH | /projects/{project_id}/branches/{branch_id}/auth/email_provider | Update email provider configuration |
| DELETE | /projects/{project_id}/auth/integration/{auth_provider} | Delete integration with auth provider |
| GET | /projects/{project_id}/connection_uri | Retrieve connection URI |
| GET | /projects/{project_id}/branches/{branch_id}/auth/allow_localhost | Get allow localhost |
| PATCH | /projects/{project_id}/branches/{branch_id}/auth/allow_localhost | Update allow localhost |
| GET | /projects/{project_id}/branches/{branch_id}/auth/plugins | Get all plugin configurations |
| PATCH | /projects/{project_id}/branches/{branch_id}/auth/plugins/organization | Update organization plugin configuration |
| GET | /projects/{project_id}/branches/{branch_id}/auth/webhooks | Get webhook configuration for Neon Auth |
| PUT | /projects/{project_id}/branches/{branch_id}/auth/webhooks | Update webhook configuration for Neon Auth |
| POST | /projects/{project_id}/branches | Create branch |
| GET | /projects/{project_id}/branches | List branches |
| POST | /projects/{project_id}/branch_anonymized | Create anonymized branch |
| GET | /projects/{project_id}/branches/count | Retrieve number of branches |
| GET | /projects/{project_id}/branches/{branch_id} | Retrieve branch details |
| DELETE | /projects/{project_id}/branches/{branch_id} | Delete branch |
| PATCH | /projects/{project_id}/branches/{branch_id} | Update branch |
| POST | /projects/{project_id}/branches/{branch_id}/restore | Restore branch |
| GET | /projects/{project_id}/branches/{branch_id}/schema | Retrieve database schema |
| GET | /projects/{project_id}/branches/{branch_id}/compare_schema | Compare database schema |
| GET | /projects/{project_id}/branches/{branch_id}/masking_rules | Get masking rules |
| PATCH | /projects/{project_id}/branches/{branch_id}/masking_rules | Update masking rules |
| GET | /projects/{project_id}/branches/{branch_id}/anonymized_status | Get anonymized branch status |
| POST | /projects/{project_id}/branches/{branch_id}/anonymize | Start anonymization |
| POST | /projects/{project_id}/branches/{branch_id}/set_as_default | Set branch as default |
| POST | /projects/{project_id}/branches/{branch_id}/finalize_restore | Finalize restore |
| GET | /projects/{project_id}/branches/{branch_id}/endpoints | List branch endpoints |
| GET | /projects/{project_id}/branches/{branch_id}/databases | List databases |
| POST | /projects/{project_id}/branches/{branch_id}/databases | Create database |
| GET | /projects/{project_id}/branches/{branch_id}/databases/{database_name} | Retrieve database details |
| PATCH | /projects/{project_id}/branches/{branch_id}/databases/{database_name} | Update database |
| DELETE | /projects/{project_id}/branches/{branch_id}/databases/{database_name} | Delete database |
| GET | /projects/{project_id}/branches/{branch_id}/roles | List roles |
| POST | /projects/{project_id}/branches/{branch_id}/roles | Create role |
| GET | /projects/{project_id}/branches/{branch_id}/roles/{role_name} | Retrieve role details |
| DELETE | /projects/{project_id}/branches/{branch_id}/roles/{role_name} | Delete role |
| GET | /projects/{project_id}/branches/{branch_id}/roles/{role_name}/reveal_password | Retrieve role password |
| POST | /projects/{project_id}/branches/{branch_id}/roles/{role_name}/reset_password | Reset role password |
| GET | /projects/{project_id}/vpc_endpoints | List VPC endpoint restrictions |
| POST | /projects/{project_id}/vpc_endpoints/{vpc_endpoint_id} | Set VPC endpoint restriction |
| DELETE | /projects/{project_id}/vpc_endpoints/{vpc_endpoint_id} | Delete VPC endpoint restriction |
| POST | /projects/{project_id}/endpoints | Create compute endpoint |
| GET | /projects/{project_id}/endpoints | List compute endpoints |
| GET | /projects/{project_id}/endpoints/{endpoint_id} | Retrieve compute endpoint details |
| DELETE | /projects/{project_id}/endpoints/{endpoint_id} | Delete compute endpoint |
| PATCH | /projects/{project_id}/endpoints/{endpoint_id} | Update compute endpoint |
| POST | /projects/{project_id}/endpoints/{endpoint_id}/start | Start compute endpoint |
| POST | /projects/{project_id}/endpoints/{endpoint_id}/suspend | Suspend compute endpoint |
| POST | /projects/{project_id}/endpoints/{endpoint_id}/restart | Restart compute endpoint |
| POST | /projects/{project_id}/branches/{branch_id}/snapshot | Create snapshot |
| GET | /projects/{project_id}/snapshots | List project snapshots |
| DELETE | /projects/{project_id}/snapshots/{snapshot_id} | Delete snapshot |
| PATCH | /projects/{project_id}/snapshots/{snapshot_id} | Update snapshot |
| POST | /projects/{project_id}/snapshots/{snapshot_id}/restore | Restore snapshot |
| GET | /projects/{project_id}/branches/{branch_id}/backup_schedule | View backup schedule |
| PUT | /projects/{project_id}/branches/{branch_id}/backup_schedule | Update backup schedule |

### api_keys
| Method | Path | Description |
|--------|------|-------------|
| GET | /api_keys | List API keys |
| POST | /api_keys | Create API key |
| DELETE | /api_keys/{key_id} | Revoke API key |

### consumption_history
| Method | Path | Description |
|--------|------|-------------|
| GET | /consumption_history/account | Retrieve account consumption metrics (legacy plans) |
| GET | /consumption_history/projects | Retrieve project consumption metrics (legacy plans) |
| GET | /consumption_history/v2/projects | Retrieve project consumption metrics |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations/{org_id} | Retrieve organization details |
| GET | /organizations/{org_id}/api_keys | List organization API keys |
| POST | /organizations/{org_id}/api_keys | Create organization API key |
| DELETE | /organizations/{org_id}/api_keys/{key_id} | Revoke organization API key |
| GET | /organizations/{org_id}/members | Retrieve organization members details |
| GET | /organizations/{org_id}/members/{member_id} | Retrieve organization member details |
| PATCH | /organizations/{org_id}/members/{member_id} | Update role for organization member |
| DELETE | /organizations/{org_id}/members/{member_id} | Remove member from the organization |
| GET | /organizations/{org_id}/invitations | Retrieve organization invitation details |
| POST | /organizations/{org_id}/invitations | Create organization invitations |
| POST | /organizations/{source_org_id}/projects/transfer | Transfer projects between organizations |
| GET | /organizations/{org_id}/vpc/vpc_endpoints | List VPC endpoints across all regions |
| GET | /organizations/{org_id}/vpc/region/{region_id}/vpc_endpoints | List VPC endpoints |
| GET | /organizations/{org_id}/vpc/region/{region_id}/vpc_endpoints/{vpc_endpoint_id} | Retrieve VPC endpoint details |
| POST | /organizations/{org_id}/vpc/region/{region_id}/vpc_endpoints/{vpc_endpoint_id} | Assign or update VPC endpoint |
| DELETE | /organizations/{org_id}/vpc/region/{region_id}/vpc_endpoints/{vpc_endpoint_id} | Delete VPC endpoint |

### regions
| Method | Path | Description |
|--------|------|-------------|
| GET | /regions | List supported regions |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/me | Retrieve current user details |
| GET | /users/me/organizations | Retrieve current user organizations list |
| POST | /users/me/projects/transfer | Transfer projects from personal account to organization |

### auth
| Method | Path | Description |
|--------|------|-------------|
| GET | /auth | Get request authentication details |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my projects?" -> GET /projects
- "How do I create a new Neon project?" -> POST /projects
- "What's the connection string for my database?" -> GET /projects/{project_id}/connection_uri
- "How do I create a new branch for my project?" -> POST /projects/{project_id}/branches
- "How do I check my resource consumption?" -> GET /consumption_history/account
- "What regions are available?" -> GET /regions
- "How do I get my account info and current plan?" -> GET /users/me
- "How do I share a project with someone?" -> POST /projects/{project_id}/permissions
- "How do I reveal a database role's password?" -> GET /projects/{project_id}/branches/{branch_id}/roles/{role_name}/reveal_password
- "How do I scale my compute endpoint up or down?" -> PATCH /projects/{project_id}/endpoints/{endpoint_id}
- "What organizations do I belong to?" -> GET /users/me/organizations
- "How do I set up Neon Auth on a branch?" -> POST /projects/{project_id}/branches/{branch_id}/auth
- "How do I compare schema changes between branches?" -> GET /projects/{project_id}/branches/{branch_id}/compare_schema
- "How do I check the status of a long-running operation?" -> GET /projects/{project_id}/operations/{operation_id}
- "How do I create an API key?" -> POST /api_keys

## Response Tips

- **Projects**: List endpoints use cursor-based pagination (`cursor` + `limit`); always check for a next cursor in the response. Project objects are deeply nested -- `settings.quota`, `settings.allowed_ips`, `default_endpoint_settings` each contain sub-maps.
- **Operations**: Operations have a `status` field (check for `running`, `finished`, `failed`) and a `failures_count` with optional `retry_at` timestamp. Poll using GET /projects/{project_id}/operations/{operation_id} until status is terminal.
- **Consumption**: Requires `from`, `to`, and `granularity` params. Returns `periods` array; each period contains metric values. 403/404/406/429 errors are common -- check date range validity and rate limits.
- **Branches**: DELETE may return either 200 (with body) or 204 (no content). Branch schema endpoints return either `sql` (raw DDL) or `json.tables` depending on the `format` param.
- **Endpoints (compute)**: The `current_state` and `pending_state` fields indicate transition status. After start/suspend/restart, poll the endpoint until `pending_state` is null.
- **Auth**: Auth setup returns keys (`pub_client_key`, `secret_server_key`) only on creation -- store them immediately as they cannot be retrieved later.
- **Organizations**: Member roles are limited to `admin` or `member`. Project transfer may fail with 406 (not acceptable) or 422 (validation error) -- surface the error body.

## Anomaly Flags

- **Operation failures**: Surface when `failures_count > 0` or `status` is `failed` on any operation. Include `error` message and `retry_at` if present.
- **Quota approaching**: After fetching project details, compare `consumption_period_*` values against `settings.quota` limits. Warn when usage exceeds 80% of any quota (active_time_seconds, compute_time_seconds, written_data_bytes, data_transfer_bytes, logical_size_bytes).
- **Suspended endpoints**: Flag when `current_state` is `idle` or `suspended_at` is recent, as queries will fail until the endpoint wakes.
- **Maintenance scheduled**: Surface `maintenance_scheduled_for` and `maintenance_starts_at` from project details so users can plan around downtime.
- **Branch protection**: Warn before modifying or deleting branches where `protected` is true.
- **Password reveal errors**: A 412 on reveal_password means `store_passwords` is disabled on the project -- surface this with remediation advice (enable it via PATCH /projects/{project_id}).
- **Transfer request expiration**: Transfer requests have `expires_at` -- warn if expiration is imminent.
- **Rate limiting**: 429 responses on consumption_history endpoints indicate throttling. Surface the retry-after timing.
- **HIPAA projects**: Flag when `hipaa` is enabled, as this restricts certain operations and region availability.

## Playbook

### 1. Create a Project with a Dev Branch

1. GET /regions -- pick a `region_id` close to your users
2. POST /projects -- provide `project.name`, `project.region_id`, and `project.pg_version`
3. Note the `project.id` and default branch from the response
4. POST /projects/{project_id}/branches -- create a dev branch (optionally set `name` and `parent_branch_id`)
5. GET /projects/{project_id}/connection_uri with `database_name`, `role_name`, and `branch_id` to get a connection string for the new branch
6. GET /projects/{project_id}/branches/{branch_id}/roles/{role_name}/reveal_password if you need the raw password

### 2. Monitor and Manage Resource Usage

1. GET /users/me -- check your `plan`, `compute_seconds_limit`, and `active_seconds_limit`
2. GET /consumption_history/account with `from`, `to`, `granularity` set to `hourly` or `daily`
3. Compare returned metrics against quota values from GET /projects/{project_id} (`settings.quota`)
4. If approaching limits, PATCH /projects/{project_id} to adjust `settings.quota` or scale down endpoints
5. PATCH /projects/{project_id}/endpoints/{endpoint_id} to lower `autoscaling_limit_max_cu` or set `suspend_timeout_seconds` to auto-suspend sooner

### 3. Set Up Neon Auth with OAuth Provider

1. POST /projects/{project_id}/branches/{branch_id}/auth with `auth_provider` (e.g., `stack_v2` or `better_auth`) -- save the returned `pub_client_key` and `secret_server_key`
2. POST /projects/{project_id}/branches/{branch_id}/auth/oauth_providers with `id` set to `google` or `github`, plus your `client_id` and `client_secret`
3. POST /projects/{project_id}/branches/{branch_id}/auth/domains with your production `domain` and `auth_provider`
4. PATCH /projects/{project_id}/branches/{branch_id}/auth/email_and_password to configure email sign-in settings
5. GET /projects/{project_id}/branches/{branch_id}/auth/plugins to verify the full auth configuration

### 4. Branch, Test Schema Changes, and Restore

1. GET /projects/{project_id}/branches/{branch_id}/schema with `db_name` to capture current schema
2. POST /projects/{project_id}/branches -- create a test branch from the current branch
3. Apply migrations on the test branch via your SQL client
4. GET /projects/{project_id}/branches/{test_branch_id}/compare_schema with `base_branch_id` set to the original branch to review the diff
5. If satisfied, POST /projects/{project_id}/branches/{branch_id}/restore with `source_branch_id` set to the test branch to promote changes
6. POST /projects/{project_id}/branches/{branch_id}/finalize_restore to complete the operation
7. DELETE /projects/{project_id}/branches/{test_branch_id} to clean up

### 5. Transfer a Project Between Organizations

1. GET /users/me/organizations -- identify source and destination org IDs
2. GET /projects with `org_id` for the source org to find the project
3. POST /organizations/{source_org_id}/projects/transfer with `destination_org_id` and `project_ids`
4. If transfer fails with 406, check that the destination org's plan supports the project's features (HIPAA, VPC, etc.)
5. GET /projects/{project_id} to verify the `org_id` has changed on the project


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
