---
name: rumble-api-deprecated
description: "Rumble API (deprecated) API skill. Use when working with Rumble API (deprecated) for releases, export, org. Covers 116 endpoints."
version: 1.0.0
generator: lapsh
---

# Rumble API (deprecated)
API version: 2.15.0

## Auth
Bearer bearer

## Base URL
https://console.rumble.run/api/v1.0

## Setup
1. Set Authorization header with your Bearer token
2. GET /releases/agent/version -- verify access
3. POST /org/agents/{agent_id}/update -- create first update

## Endpoints

116 endpoints across 4 groups. See references/api-spec.lap for full details.

### releases
| Method | Path | Description |
|--------|------|-------------|
| GET | /releases/agent/version | Returns latest agent version |
| GET | /releases/scanner/version | Returns latest scanner version |
| GET | /releases/platform/version | Returns latest platform version |

### export
| Method | Path | Description |
|--------|------|-------------|
| GET | /export/org/assets.json | Exports the asset inventory |
| GET | /export/org/assets.jsonl | Asset inventory as JSON line-delimited |
| GET | /export/org/assets.csv | Asset inventory as CSV |
| GET | /export/org/assets.nmap.xml | Asset inventory as Nmap-style XML |
| GET | /export/org/services.json | Service inventory as JSON |
| GET | /export/org/services.jsonl | Service inventory as JSON line-delimited |
| GET | /export/org/services.csv | Service inventory as CSV |
| GET | /export/org/sites.json | Export all sites |
| GET | /export/org/sites.jsonl | Site list as JSON line-delimited |
| GET | /export/org/sites.csv | Site list as CSV |
| GET | /export/org/wireless.json | Wireless inventory as JSON |
| GET | /export/org/wireless.jsonl | Wireless inventory as JSON line-delimited |
| GET | /export/org/wireless.csv | Wireless inventory as CSV |
| GET | /export/org/assets/sync/created/assets.json | Exports the asset inventory in a sync-friendly manner using created_at as a checkpoint. Requires the Splunk entitlement. |
| GET | /export/org/assets/sync/updated/assets.json | Exports the asset inventory in a sync-friendly manner using updated_at as a checkpoint. Requires the Splunk entitlement. |
| GET | /export/org/assets.servicenow.csv | Export an asset inventory as CSV for ServiceNow integration |
| GET | /export/org/assets.servicenow.json | Exports the asset inventory as JSON |
| GET | /export/org/services.servicenow.csv | Export a service inventory as CSV for ServiceNow integration |
| GET | /export/org/assets.cisco.csv | Cisco serial number and model name export for Cisco Smart Net Total Care Service. |

### org
| Method | Path | Description |
|--------|------|-------------|
| GET | /org/assets/top.types.csv | Top asset types as CSV |
| GET | /org/assets/top.os.csv | Top asset operating systems as CSV |
| GET | /org/assets/top.hw.csv | Top asset hardware products as CSV |
| GET | /org/assets/top.tags.csv | Top asset tags as CSV |
| GET | /org/services/top.tcp.csv | Top TCP services as CSV |
| GET | /org/services/top.udp.csv | Top UDP services as CSV |
| GET | /org/services/top.protocols.csv | Top service protocols as CSV |
| GET | /org/services/top.products.csv | Top service products as CSV |
| GET | /org/services/subnet.stats.csv | Subnet utilization statistics as as CSV |
| GET | /org | Get organization details |
| PATCH | /org | Update organization details |
| GET | /org/key | Get API key details |
| DELETE | /org/key | Remove the current API key |
| PATCH | /org/key/rotate | Rotate the API key secret and return the updated key |
| GET | /org/agents | Get all agents |
| GET | /org/agents/{agent_id} | Get details for a single agent |
| DELETE | /org/agents/{agent_id} | Remove and uninstall an agent |
| PATCH | /org/agents/{agent_id} | Update the site associated with agent |
| POST | /org/agents/{agent_id}/update | Force an agent to update and restart |
| GET | /org/sites | Get all sites |
| PUT | /org/sites | Create a new site |
| GET | /org/sites/{site_id} | Get site details |
| DELETE | /org/sites/{site_id} | Remove a site and associated assets |
| PATCH | /org/sites/{site_id} | Update a site definition |
| PUT | /org/sites/{site_id}/import | Import a scan data file into a site |
| PUT | /org/sites/{site_id}/import/nessus | Import a Nessus scan data file into a site |
| PUT | /org/sites/{site_id}/scan | Create a scan task for a given site |
| GET | /org/assets | Get all assets |
| GET | /org/assets/{asset_id} | Get asset details |
| DELETE | /org/assets/{asset_id} | Remove an asset |
| PATCH | /org/assets/{asset_id}/comments | Update asset comments |
| PATCH | /org/assets/{asset_id}/tags | Update asset tags |
| PATCH | /org/assets/bulk/tags | Update tags across multiple assets based on a search query |
| POST | /org/assets/bulk/clearTags | Clear all tags across multiple assets based on a search query |
| GET | /org/services | Get all services |
| GET | /org/services/{service_id} | Get service details |
| DELETE | /org/services/{service_id} | Remove a service |
| GET | /org/wireless | Get all wireless LANs |
| GET | /org/wireless/{wireless_id} | Get wireless LAN details |
| DELETE | /org/wireless/{wireless_id} | Remove a wireless LAN |
| GET | /org/tasks | Get all tasks (last 1000) |
| GET | /org/tasks/{task_id} | Get task details |
| PATCH | /org/tasks/{task_id} | Update task parameters |
| GET | /org/tasks/{task_id}/data | Returns a temporary task scan data url |
| GET | /org/tasks/{task_id}/changes | Returns a temporary task change report data url |
| GET | /org/tasks/{task_id}/log | Returns a temporary task log data url |
| POST | /org/tasks/{task_id}/stop | Signal that a task should be stopped or canceledThis will also remove recurring and scheduled tasks |
| POST | /org/tasks/{task_id}/hide | Signal that a completed task should be hidden |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account/orgs | Get all organization details |
| PUT | /account/orgs | Create a new organization |
| GET | /account/orgs/{org_id} | Get organization details |
| PATCH | /account/orgs/{org_id} | Update organization details |
| DELETE | /account/orgs/{org_id} | Remove this organization |
| DELETE | /account/orgs/{org_id}/exportToken | Removes the export token from the specified organization |
| PATCH | /account/orgs/{org_id}/exportToken/rotate | Rotates the organization export token and returns the updated organization |
| GET | /account/license | Get license details |
| GET | /account/sites | Get all sites details across all organizations |
| GET | /account/credentials | Get all account credentials |
| PUT | /account/credentials | Create a new credential |
| GET | /account/credentials/{credential_id} | Get credential details |
| DELETE | /account/credentials/{credential_id} | Remove this credential |
| GET | /account/keys | Get all active API keys |
| PUT | /account/keys | Create a new key |
| GET | /account/keys/{key_id} | Get key details |
| DELETE | /account/keys/{key_id} | Remove this key |
| PATCH | /account/keys/{key_id}/rotate | Rotates the key secret |
| GET | /account/events.json | System event log as JSON |
| GET | /account/events.jsonl | System event log as JSON line-delimited |
| GET | /account/tasks | Get all task details across all organizations (up to 1000) |
| GET | /account/tasks/templates | Get all scan templates across all organizations (up to 1000) |
| POST | /account/tasks/templates | Create a new scan template |
| PUT | /account/tasks/templates | Update scan template |
| GET | /account/tasks/templates/{scan_template_id} | Get scan template details |
| DELETE | /account/tasks/templates/{scan_template_id} | Remove scan template |
| GET | /account/agents | Get all agents across all organizations |
| GET | /account/users | Get all users |
| PUT | /account/users | Create a new user account |
| PUT | /account/users/invite | Create a new user account and send an email invite |
| GET | /account/users/{user_id} | Get user details |
| DELETE | /account/users/{user_id} | Remove this user |
| PATCH | /account/users/{user_id} | Update a user's details |
| PATCH | /account/users/{user_id}/resetMFA | Resets the user's MFA tokens |
| PATCH | /account/users/{user_id}/resetLockout | Resets the user's lockout status |
| PATCH | /account/users/{user_id}/resetPassword | Sends the user a password reset email |
| GET | /account/groups | Get all groups |
| POST | /account/groups | Create a new group |
| PUT | /account/groups | Update an existing group |
| GET | /account/groups/{group_id} | Get group details |
| DELETE | /account/groups/{group_id} | Remove this group |
| GET | /account/sso/groups | Get all SSO group mappings |
| POST | /account/sso/groups | Create a new SSO group mapping |
| PUT | /account/sso/groups | Update an existing SSO group mapping |
| GET | /account/sso/groups/{group_mapping_id} | Get SSO group mapping details |
| DELETE | /account/sso/groups/{group_mapping_id} | Remove this SSO group mapping |

## Enhanced Skill Content
## Question Mapping

- "What version of the scanner agent is available?" -> GET /releases/scanner/version
- "Export all discovered assets as JSON" -> GET /export/org/assets.json
- "Find all services running on my network" -> GET /org/services
- "What operating systems are most common across my assets?" -> GET /org/assets/top.os.csv
- "Show me details for a specific asset" -> GET /org/assets/{asset_id}
- "Start a scan on a site" -> PUT /org/sites/{site_id}/scan
- "List all agents deployed in my organization" -> GET /org/agents
- "Create a new site with a specific IP scope" -> PUT /org/sites
- "How do I rotate my API key?" -> PATCH /org/key/rotate
- "Tag multiple assets matching a search filter" -> PATCH /org/assets/bulk/tags
- "What wireless networks have been detected?" -> GET /org/wireless
- "Check the status of a running scan task" -> GET /org/tasks/{task_id}
- "Import a Nessus scan into a site" -> PUT /org/sites/{site_id}/import/nessus
- "Invite a new user to my account" -> PUT /account/users/invite
- "Get incremental asset changes since last sync" -> GET /export/org/assets/sync/updated/assets.json

## Response Tips

- **Releases**: Simple `{id, version}` objects; no pagination. Compare versions as semver strings.
- **Export endpoints**: Streaming bulk data; format varies by extension (.json returns array, .jsonl returns newline-delimited, .csv returns flat rows). Use `search` param to filter server-side before download. The `fields` param (JSON/JSONL only) controls which columns are returned.
- **Org resource lists** (assets, services, wireless, tasks, agents, sites): Return arrays; use the `search` query param for server-side filtering. No cursor/offset pagination documented -- expect full result sets.
- **Single resource GETs**: Return the full object. Assets and services include nested `map` fields (`tags`, `services`, `rtts`, `credentials`, `attributes`, `service_data`) that are key-value dictionaries requiring further inspection.
- **Sync endpoints**: Return `{since: int64, assets: [map]}` -- the `since` timestamp is your cursor for the next incremental pull.
- **Write operations**: PUT creates, PATCH updates, POST triggers actions. 204 means success with no body (deletes, stops). 200 returns the updated object.
- **Errors**: 401 is universal (auth required on every endpoint). 404 means the UUID was not found. 403/500 appear only on scan/import actions (permission or server failure). 422 appears on task template validation.

## Anomaly Flags

- **API is deprecated**: The spec is marked `(deprecated)`. Surface this on every interaction -- recommend users check for a successor API (runZero).
- **401 on any call**: Bearer token may be expired or revoked. Suggest rotating via `PATCH /org/key/rotate` or creating a new key via `PUT /account/keys`.
- **usage_today approaching usage_limit**: The key object includes daily usage counters. Flag when `usage_today` exceeds 80% of `usage_limit`.
- **Agent not connected**: When `GET /org/agents/{id}` returns `connected: false` or `inactive: true`, surface that the agent may be offline or deactivated.
- **Stale assets**: If `last_seen` on an asset is significantly older than `expiration_assets_stale` on the org, the asset may be about to expire.
- **Task errors**: When a task's `status` is not progressing or `error` field is non-empty, proactively surface the failure.
- **Export token exposure**: `export_token` fields appear in org responses. Flag if the token is being logged or stored insecurely.
- **Scan 403/500**: Import and scan endpoints can return 403 (insufficient permissions) or 500 (server error). Surface these distinctly -- 403 means the key lacks scan privileges, 500 means retry or contact support.

## Playbook

### 1. Full Network Asset Inventory Export

1. Call `GET /org` to confirm the active organization and note `asset_count` and `service_count`
2. Call `GET /export/org/assets.json` to download all assets (add `search` to filter if needed)
3. Call `GET /export/org/services.json` to download all services
4. For ServiceNow integration, use `GET /export/org/assets.servicenow.json` instead
5. Save results; use `fields` param to limit payload size if only specific columns are needed

### 2. Set Up and Run a Network Scan

1. Call `GET /org/agents` to find a connected agent (`connected: true`)
2. Call `PUT /org/sites` with `name`, `scope` (CIDR range), and optional `excludes` to create a scan target
3. Call `PUT /org/sites/{site_id}/scan` using the returned site ID to start the scan
4. Poll `GET /org/tasks/{task_id}` using the returned task ID until `status` indicates completion
5. Call `GET /org/assets?search=site:{site_id}` to review discovered assets

### 3. Incremental Asset Sync Pipeline

1. On first run, call `GET /export/org/assets/sync/created/assets.json` without `since` to get baseline
2. Store the returned `since` timestamp
3. On subsequent runs, call `GET /export/org/assets/sync/updated/assets.json?since={timestamp}` to get only changes
4. Process the `assets` array and update your local database
5. Store the new `since` value for the next iteration

### 4. API Key Rotation and User Management

1. Call `GET /account/keys` to list all active API keys and review `last_used_at` and `usage_today`
2. Call `PATCH /account/keys/{key_id}/rotate` to rotate a key -- save the new `token` from the response immediately
3. Update all integrations with the new token
4. Call `GET /account/users` to audit active users
5. For any user showing `login_failures` > 0 or stale `last_login_at`, call `PATCH /account/users/{user_id}/resetLockout` or `DELETE /account/users/{user_id}` as appropriate

### 5. Import Third-Party Scan Data (Nessus)

1. Call `GET /org/sites` to find the target site, or `PUT /org/sites` to create one
2. Call `PUT /org/sites/{site_id}/import/nessus` with the Nessus XML file in the request body
3. Note the returned task object and its `id`
4. Poll `GET /org/tasks/{task_id}` until `status` shows completion; check `error` field for failures
5. Review imported assets with `GET /org/assets?search=site:{site_id}` and verify `stats` on the task for import counts


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
