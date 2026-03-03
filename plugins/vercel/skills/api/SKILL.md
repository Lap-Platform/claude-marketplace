---
name: vercel-api
description: "Vercel API skill. Use when working with Vercel for access-groups, artifacts, billing. Covers 281 endpoints."
version: 1.0.0
generator: lapsh
---

# Vercel API
API version: 0.0.1

## Auth
Bearer bearer | OAuth2

## Base URL
https://api.vercel.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/access-groups -- verify access
3. POST /v1/access-groups/{idOrName} -- create first access-groups

## Endpoints

281 endpoints across 26 groups. See references/api-spec.lap for full details.

### access-groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/access-groups/{idOrName} | Reads an access group |
| POST | /v1/access-groups/{idOrName} | Update an access group |
| DELETE | /v1/access-groups/{idOrName} | Deletes an access group |
| GET | /v1/access-groups/{idOrName}/members | List members of an access group |
| GET | /v1/access-groups | List access groups for a team, project or member |
| POST | /v1/access-groups | Creates an access group |
| GET | /v1/access-groups/{idOrName}/projects | List projects of an access group |
| POST | /v1/access-groups/{accessGroupIdOrName}/projects | Create an access group project |
| GET | /v1/access-groups/{accessGroupIdOrName}/projects/{projectId} | Reads an access group project |
| PATCH | /v1/access-groups/{accessGroupIdOrName}/projects/{projectId} | Update an access group project |
| DELETE | /v1/access-groups/{accessGroupIdOrName}/projects/{projectId} | Delete an access group project |

### artifacts
| Method | Path | Description |
|--------|------|-------------|
| POST | /v8/artifacts/events | Record an artifacts cache usage event |
| GET | /v8/artifacts/status | Get status of Remote Caching for this principal |
| PUT | /v8/artifacts/{hash} | Upload a cache artifact |
| GET | /v8/artifacts/{hash} | Download a cache artifact |
| HEAD | /v8/artifacts/{hash} | Check if a cache artifact exists |
| POST | /v8/artifacts | Query information about an artifact |

### billing
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/billing/charges | List FOCUS billing charges |
| GET | /v1/billing/contract-commitments | List FOCUS contract commitments |

### bulk-redirects
| Method | Path | Description |
|--------|------|-------------|
| PUT | /v1/bulk-redirects | Stages new redirects for a project. |
| GET | /v1/bulk-redirects | Gets project-level redirects. |
| DELETE | /v1/bulk-redirects | Delete project-level redirects. |
| PATCH | /v1/bulk-redirects | Edit a project-level redirect. |
| POST | /v1/bulk-redirects/restore | Restore staged project-level redirects to their production version. |
| GET | /v1/bulk-redirects/versions | Get the version history for a project's redirects. |
| POST | /v1/bulk-redirects/versions | Promote a staging version to production or restore a previous production version. |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/projects/{projectIdOrName}/checks | List all checks for a project |
| POST | /v2/projects/{projectIdOrName}/checks | Create a check |
| GET | /v2/projects/{projectIdOrName}/checks/{checkId} | Get a check |
| PATCH | /v2/projects/{projectIdOrName}/checks/{checkId} | Update a check |
| DELETE | /v2/projects/{projectIdOrName}/checks/{checkId} | Delete a check |
| GET | /v2/projects/{projectIdOrName}/checks/{checkId}/runs | List runs for a check |
| GET | /v1/projects/{projectIdOrName}/feature-flags/flags | List flags |
| PUT | /v1/projects/{projectIdOrName}/feature-flags/flags | Create a flag |
| GET | /v1/projects/{projectIdOrName}/feature-flags/flags/{flagIdOrSlug} | Get a flag |
| PATCH | /v1/projects/{projectIdOrName}/feature-flags/flags/{flagIdOrSlug} | Update a flag |
| DELETE | /v1/projects/{projectIdOrName}/feature-flags/flags/{flagIdOrSlug} | Delete a flag |
| GET | /v1/projects/{projectIdOrName}/feature-flags/flags/{flagIdOrSlug}/versions | List flag versions |
| GET | /v1/projects/{projectIdOrName}/feature-flags/settings | Get project flag settings |
| PATCH | /v1/projects/{projectIdOrName}/feature-flags/settings | Update project flag settings |
| PUT | /v1/projects/{projectIdOrName}/feature-flags/segments | Create a segment |
| GET | /v1/projects/{projectIdOrName}/feature-flags/segments | List segments |
| GET | /v1/projects/{projectIdOrName}/feature-flags/segments/{segmentIdOrSlug} | Get a segment |
| DELETE | /v1/projects/{projectIdOrName}/feature-flags/segments/{segmentIdOrSlug} | Delete a segment |
| PATCH | /v1/projects/{projectIdOrName}/feature-flags/segments/{segmentIdOrSlug} | Update a segment |
| GET | /v1/projects/{projectIdOrName}/feature-flags/sdk-keys | Get all SDK keys |
| PUT | /v1/projects/{projectIdOrName}/feature-flags/sdk-keys | Create an SDK key |
| DELETE | /v1/projects/{projectIdOrName}/feature-flags/sdk-keys/{hashKey} | Delete an SDK key |
| GET | /v1/projects/{projectId}/deployments/{deploymentId}/runtime-logs | Get logs for a deployment |
| GET | /v1/projects/{idOrName}/members | List project members |
| POST | /v1/projects/{idOrName}/members | Adds a new member to a project. |
| DELETE | /v1/projects/{idOrName}/members/{uid} | Remove a Project Member |
| GET | /v10/projects | Retrieve a list of projects |
| POST | /v11/projects | Create a new project |
| GET | /v9/projects/{idOrName} | Find a project by id or name |
| PATCH | /v9/projects/{idOrName} | Update an existing project |
| DELETE | /v9/projects/{idOrName} | Delete a Project |
| PATCH | /v1/projects/{idOrName}/shared-connect-links | Configures Static IPs for a project |
| POST | /v9/projects/{idOrName}/custom-environments | Create a custom environment for the current project. |
| GET | /v9/projects/{idOrName}/custom-environments | Retrieve custom environments |
| GET | /v9/projects/{idOrName}/custom-environments/{environmentSlugOrId} | Retrieve a custom environment |
| PATCH | /v9/projects/{idOrName}/custom-environments/{environmentSlugOrId} | Update a custom environment |
| DELETE | /v9/projects/{idOrName}/custom-environments/{environmentSlugOrId} | Remove a custom environment |
| GET | /v9/projects/{idOrName}/domains | Retrieve project domains by project by id or name |
| GET | /v9/projects/{idOrName}/domains/{domain} | Get a project domain |
| PATCH | /v9/projects/{idOrName}/domains/{domain} | Update a project domain |
| DELETE | /v9/projects/{idOrName}/domains/{domain} | Remove a domain from a project |
| POST | /v10/projects/{idOrName}/domains | Add a domain to a project |
| POST | /v1/projects/{idOrName}/domains/{domain}/move | Move a project domain |
| POST | /v9/projects/{idOrName}/domains/{domain}/verify | Verify project domain |
| GET | /v10/projects/{idOrName}/env | Retrieve the environment variables of a project by id or name |
| POST | /v10/projects/{idOrName}/env | Create one or more environment variables |
| GET | /v1/projects/{idOrName}/env/{id} | Retrieve the decrypted value of an environment variable of a project by id |
| DELETE | /v9/projects/{idOrName}/env/{id} | Remove an environment variable |
| PATCH | /v9/projects/{idOrName}/env/{id} | Edit an environment variable |
| DELETE | /v1/projects/{idOrName}/env | Batch remove environment variables |
| GET | /v1/projects/{idOrName}/rolling-release/billing | Get rolling release billing status |
| GET | /v1/projects/{idOrName}/rolling-release/config | Get rolling release configuration |
| DELETE | /v1/projects/{idOrName}/rolling-release/config | Delete rolling release configuration |
| PATCH | /v1/projects/{idOrName}/rolling-release/config | Update the rolling release settings for the project |
| GET | /v1/projects/{idOrName}/rolling-release | Get the active rolling release information for a project |
| POST | /v1/projects/{idOrName}/rolling-release/approve-stage | Update the active rolling release to the next stage for a project |
| POST | /v1/projects/{idOrName}/rolling-release/complete | Complete the rolling release for the project |
| POST | /projects/{idOrName}/transfer-request | Create project transfer request |
| PUT | /projects/transfer-request/{code} | Accept project transfer request |
| PATCH | /v1/projects/{idOrName}/protection-bypass | Update Protection Bypass for Automation |
| POST | /v1/projects/{projectId}/rollback/{deploymentId} | Points all production domains for a project to the given deploy |
| PATCH | /v1/projects/{projectId}/rollback/{deploymentId}/update-description | Updates the description for a rollback |
| POST | /v10/projects/{projectId}/promote/{deploymentId} | Points all production domains for a project to the given deploy |
| GET | /v1/projects/{projectId}/promote/aliases | Gets a list of aliases with status for the current promote |
| POST | /v1/projects/{projectId}/pause | Pause a project |
| POST | /v1/projects/{projectId}/unpause | Unpause a project |

### deployments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/deployments/{deploymentId}/check-runs | List check runs for a deployment |
| POST | /v2/deployments/{deploymentId}/check-runs | Create a check run |
| GET | /v2/deployments/{deploymentId}/check-runs/{checkRunId} | Get a check run |
| PATCH | /v2/deployments/{deploymentId}/check-runs/{checkRunId} | Update a check run |
| POST | /v1/deployments/{deploymentId}/checks | Creates a new Check |
| GET | /v1/deployments/{deploymentId}/checks | Retrieve a list of all checks |
| GET | /v1/deployments/{deploymentId}/checks/{checkId} | Get a single check |
| PATCH | /v1/deployments/{deploymentId}/checks/{checkId} | Update a check |
| POST | /v1/deployments/{deploymentId}/checks/{checkId}/rerequest | Rerequest a check |
| GET | /v3/deployments/{idOrUrl}/events | Get deployment events |
| PATCH | /v1/deployments/{deploymentId}/integrations/{integrationConfigurationId}/resources/{resourceId}/actions/{action} | Update deployment integration action |
| GET | /v13/deployments/{idOrUrl} | Get a deployment by ID or URL |
| POST | /v13/deployments | Create a new deployment |
| PATCH | /v12/deployments/{id}/cancel | Cancel a deployment |
| GET | /v1/deployments/{deploymentId}/feature-flags | Retrieve the feature flags of a deployment |
| GET | /v2/deployments/{id}/aliases | List Deployment Aliases |
| POST | /v2/deployments/{id}/aliases | Assign an Alias |
| GET | /v6/deployments/{id}/files | List Deployment Files |
| GET | /v8/deployments/{id}/files/{fileId} | Get Deployment File Contents |
| GET | /v6/deployments | List deployments |
| DELETE | /v13/deployments/{id} | Delete a Deployment |

### connect
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/connect/networks | List Secure Compute networks |
| POST | /v1/connect/networks | Create a Secure Compute network |
| DELETE | /v1/connect/networks/{networkId} | Delete a Secure Compute network |
| PATCH | /v1/connect/networks/{networkId} | Update a Secure Compute network |
| GET | /v1/connect/networks/{networkId} | Read a Secure Compute network |

### domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/domains/{domain}/records | List existing DNS records |
| POST | /v2/domains/{domain}/records | Create a DNS record |
| PATCH | /v1/domains/records/{recordId} | Update an existing DNS record |
| DELETE | /v2/domains/{domain}/records/{recordId} | Delete a DNS record |
| GET | /v6/domains/{domain}/config | Get a Domain's configuration |
| GET | /v5/domains/{domain} | Get Information for a Single Domain |
| GET | /v5/domains | List all the domains |
| POST | /v7/domains | Add an existing domain to the Vercel platform |
| PATCH | /v3/domains/{domain} | Update or move apex domain |
| DELETE | /v6/domains/{domain} | Remove a domain by name |

### registrar
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/registrar/tlds/supported | Get supported TLDs |
| GET | /v1/registrar/tlds/{tld} | Get TLD |
| GET | /v1/registrar/tlds/{tld}/price | Get TLD price data |
| GET | /v1/registrar/domains/{domain}/availability | Get availability for a domain |
| GET | /v1/registrar/domains/{domain}/price | Get price data for a domain |
| POST | /v1/registrar/domains/availability | Get availability for multiple domains |
| GET | /v1/registrar/domains/{domain}/auth-code | Get the auth code for a domain |
| POST | /v1/registrar/domains/{domain}/buy | Buy a domain |
| POST | /v1/registrar/domains/buy | Buy multiple domains |
| POST | /v1/registrar/domains/{domain}/transfer | Transfer-in a domain |
| GET | /v1/registrar/domains/{domain}/transfer | Get a domain's transfer status |
| POST | /v1/registrar/domains/{domain}/renew | Renew a domain |
| PATCH | /v1/registrar/domains/{domain}/auto-renew | Update auto-renew for a domain |
| PATCH | /v1/registrar/domains/{domain}/nameservers | Update nameservers for a domain |
| GET | /v1/registrar/domains/{domain}/contact-info/schema | Get contact info schema |
| GET | /v1/registrar/orders/{orderId} | Get a domain order |

### log-drains
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/log-drains/{id} | Retrieves a Configurable Log Drain (deprecated) |
| DELETE | /v1/log-drains/{id} | Deletes a Configurable Log Drain (deprecated) |
| GET | /v1/log-drains | Retrieves a list of all the Log Drains (deprecated) |
| POST | /v1/log-drains | Creates a Configurable Log Drain (deprecated) |

### drains
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/drains | Create a new Drain |
| GET | /v1/drains | Retrieve a list of all Drains |
| DELETE | /v1/drains/{id} | Delete a drain |
| GET | /v1/drains/{id} | Find a Drain by id |
| PATCH | /v1/drains/{id} | Update an existing Drain |
| POST | /v1/drains/test | Validate Drain delivery configuration |

### edge-cache
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/edge-cache/invalidate-by-tags | Invalidate by tag |
| POST | /v1/edge-cache/dangerously-delete-by-tags | Dangerously delete by tag |
| POST | /v1/edge-cache/invalidate-by-src-images | Invalidate by source image |
| POST | /v1/edge-cache/dangerously-delete-by-src-images | Dangerously delete by source image |

### edge-config
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/edge-config | Get Edge Configs |
| POST | /v1/edge-config | Create an Edge Config |
| GET | /v1/edge-config/{edgeConfigId} | Get an Edge Config |
| PUT | /v1/edge-config/{edgeConfigId} | Update an Edge Config |
| DELETE | /v1/edge-config/{edgeConfigId} | Delete an Edge Config |
| GET | /v1/edge-config/{edgeConfigId}/items | Get Edge Config items |
| PATCH | /v1/edge-config/{edgeConfigId}/items | Update Edge Config items in batch |
| GET | /v1/edge-config/{edgeConfigId}/schema | Get Edge Config schema |
| POST | /v1/edge-config/{edgeConfigId}/schema | Update Edge Config schema |
| DELETE | /v1/edge-config/{edgeConfigId}/schema | Delete an Edge Config's schema |
| GET | /v1/edge-config/{edgeConfigId}/item/{edgeConfigItemKey} | Get an Edge Config item |
| GET | /v1/edge-config/{edgeConfigId}/tokens | Get all tokens of an Edge Config |
| DELETE | /v1/edge-config/{edgeConfigId}/tokens | Delete one or more Edge Config tokens |
| GET | /v1/edge-config/{edgeConfigId}/token/{token} | Get Edge Config token meta data |
| POST | /v1/edge-config/{edgeConfigId}/token | Create an Edge Config token |
| GET | /v1/edge-config/{edgeConfigId}/backups/{edgeConfigBackupVersionId} | Get Edge Config backup |
| GET | /v1/edge-config/{edgeConfigId}/backups | Get Edge Config backups |

### env
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/env | Create one or more shared environment variables |
| GET | /v1/env | Lists all Shared Environment Variables for a team |
| PATCH | /v1/env | Updates one or more shared environment variables |
| DELETE | /v1/env | Delete one or more Env Var |
| GET | /v1/env/{id} | Retrieve the decrypted value of a Shared Environment Variable by id. |
| PATCH | /v1/env/{id}/unlink/{projectId} | Disconnects a shared environment variable for a given project |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /v3/events | List User Events |
| GET | /v1/events/types | List Event Types |

### teams
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/teams/{teamId}/feature-flags/settings | List team project flag settings |
| GET | /v1/teams/{teamId}/feature-flags/flags | List all flags for a team |
| GET | /v3/teams/{teamId}/members | List team members |
| POST | /v2/teams/{teamId}/members | Invite a user |
| POST | /v1/teams/{teamId}/request | Request access to a team |
| GET | /v1/teams/{teamId}/request/{userId} | Get access request status |
| POST | /v1/teams/{teamId}/members/teams/join | Join a team |
| PATCH | /v1/teams/{teamId}/members/{uid} | Update a Team Member |
| DELETE | /v1/teams/{teamId}/members/{uid} | Remove a Team Member |
| GET | /v2/teams/{teamId} | Get a Team |
| PATCH | /v2/teams/{teamId} | Update a Team |
| GET | /v2/teams | List all teams |
| POST | /v1/teams | Create a Team |
| POST | /v1/teams/{teamId}/dsync-roles | Update Team Directory Sync Role Mappings |
| DELETE | /v1/teams/{teamId} | Delete a Team |
| DELETE | /v1/teams/{teamId}/invites/{inviteId} | Delete a Team invite code |

### integrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/integrations/git-namespaces | List git namespaces by provider |
| GET | /v1/integrations/search-repo | List git repositories linked to namespace by provider |
| GET | /v1/integrations/integration/{integrationIdOrSlug}/products/{productIdOrSlug}/plans | List integration billing plans |
| POST | /v1/integrations/installations/{integrationConfigurationId}/resources/{resourceId}/connections | Connect integration resource to project |
| GET | /v1/integrations/configurations | Get configurations for the authenticated user or team |
| GET | /v1/integrations/configuration/{id} | Retrieve an integration configuration |
| DELETE | /v1/integrations/configuration/{id} | Delete an integration configuration |
| GET | /v1/integrations/configuration/{id}/products | List products for integration configuration |
| POST | /v1/integrations/sso/token | SSO Token Exchange |
| GET | /v2/integrations/log-drains | Retrieves a list of Integration log drains (deprecated) |
| POST | /v2/integrations/log-drains | Creates a new Integration Log Drain (deprecated) |
| DELETE | /v1/integrations/log-drains/{id} | Deletes the Integration log drain with the provided `id` (deprecated) |

### installations
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /v1/installations/{integrationConfigurationId} | Update Installation |
| GET | /v1/installations/{integrationConfigurationId}/account | Get Account Information |
| GET | /v1/installations/{integrationConfigurationId}/member/{memberId} | Get Member Information |
| POST | /v1/installations/{integrationConfigurationId}/events | Create Event |
| GET | /v1/installations/{integrationConfigurationId}/resources | Get Integration Resources |
| GET | /v1/installations/{integrationConfigurationId}/resources/{resourceId} | Get Integration Resource |
| DELETE | /v1/installations/{integrationConfigurationId}/resources/{resourceId} | Delete Integration Resource |
| PUT | /v1/installations/{integrationConfigurationId}/resources/{resourceId} | Import Resource |
| PATCH | /v1/installations/{integrationConfigurationId}/resources/{resourceId} | Update Resource |
| POST | /v1/installations/{integrationConfigurationId}/billing | Submit Billing Data |
| POST | /v1/installations/{integrationConfigurationId}/billing/invoices | Submit Invoice |
| POST | /v1/installations/{integrationConfigurationId}/billing/finalize | Finalize Installation |
| GET | /v1/installations/{integrationConfigurationId}/billing/invoices/{invoiceId} | Get Invoice |
| POST | /v1/installations/{integrationConfigurationId}/billing/invoices/{invoiceId}/actions | Invoice Actions |
| POST | /v1/installations/{integrationConfigurationId}/billing/balance | Submit Prepayment Balances |
| PUT | /v1/installations/{integrationConfigurationId}/products/{integrationProductIdOrSlug}/resources/{resourceId}/secrets | Update Resource Secrets (Deprecated) |
| PUT | /v1/installations/{integrationConfigurationId}/resources/{resourceId}/secrets | Update Resource Secrets |
| POST | /v1/installations/{integrationConfigurationId}/resources/{resourceId}/experimentation/items | Create one or multiple experimentation items |
| PATCH | /v1/installations/{integrationConfigurationId}/resources/{resourceId}/experimentation/items/{itemId} | Patch an existing experimentation item |
| DELETE | /v1/installations/{integrationConfigurationId}/resources/{resourceId}/experimentation/items/{itemId} | Delete an existing experimentation item |
| HEAD | /v1/installations/{integrationConfigurationId}/resources/{resourceId}/experimentation/edge-config | Get the data of a user-provided Edge Config |
| GET | /v1/installations/{integrationConfigurationId}/resources/{resourceId}/experimentation/edge-config | Get the data of a user-provided Edge Config |
| PUT | /v1/installations/{integrationConfigurationId}/resources/{resourceId}/experimentation/edge-config | Push data into a user-provided Edge Config |

### sandboxes
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/sandboxes | List sandboxes |
| POST | /v1/sandboxes | Create a sandbox |
| GET | /v1/sandboxes/snapshots | List snapshots |
| GET | /v1/sandboxes/{sandboxId} | Get a sandbox |
| GET | /v1/sandboxes/{sandboxId}/cmd | List commands |
| POST | /v1/sandboxes/{sandboxId}/cmd | Execute a command |
| POST | /v1/sandboxes/{sandboxId}/{cmdId}/kill | Kill a command |
| POST | /v1/sandboxes/{sandboxId}/stop | Stop a sandbox |
| POST | /v1/sandboxes/{sandboxId}/extend-timeout | Extend sandbox timeout |
| POST | /v1/sandboxes/{sandboxId}/network-policy | Update network policy |
| GET | /v1/sandboxes/{sandboxId}/cmd/{cmdId} | Get a command |
| GET | /v1/sandboxes/{sandboxId}/cmd/{cmdId}/logs | Stream command logs |
| POST | /v1/sandboxes/{sandboxId}/fs/read | Read a file |
| POST | /v1/sandboxes/{sandboxId}/fs/mkdir | Create a directory |
| POST | /v1/sandboxes/{sandboxId}/fs/write | Write files |
| GET | /v1/sandboxes/snapshots/{snapshotId} | Get a snapshot |
| DELETE | /v1/sandboxes/snapshots/{snapshotId} | Delete a snapshot |
| POST | /v1/sandboxes/{sandboxId}/snapshot | Create a snapshot |

### security
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/security/attack-mode | Update Attack Challenge mode |
| PUT | /v1/security/firewall/config | Put Firewall Configuration |
| PATCH | /v1/security/firewall/config | Update Firewall Configuration |
| GET | /v1/security/firewall/config/{configVersion} | Read Firewall Configuration |
| GET | /v1/security/firewall/attack-status | Read active attack data |
| GET | /v1/security/firewall/bypass | Read System Bypass |
| POST | /v1/security/firewall/bypass | Create System Bypass Rule |
| DELETE | /v1/security/firewall/bypass | Remove System Bypass Rule |
| GET | /v1/security/firewall/events | Read Firewall Actions by Project |

### storage
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/storage/stores/integration/direct | Create integration store (free and paid plans) |

### files
| Method | Path | Description |
|--------|------|-------------|
| POST | /v2/files | Upload Deployment Files |

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /v5/user/tokens | List Auth Tokens |
| POST | /v3/user/tokens | Create an Auth Token |
| GET | /v5/user/tokens/{tokenId} | Get Auth Token Metadata |
| DELETE | /v3/user/tokens/{tokenId} | Delete an authentication token |
| GET | /v2/user | Get the User |
| DELETE | /v1/user | Delete User Account |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/webhooks | Creates a webhook |
| GET | /v1/webhooks | Get a list of webhooks |
| GET | /v1/webhooks/{id} | Get a webhook |
| DELETE | /v1/webhooks/{id} | Deletes a webhook |

### aliases
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/aliases | List aliases |
| GET | /v4/aliases/{idOrAlias} | Get an Alias |
| DELETE | /v2/aliases/{aliasId} | Delete an Alias |
| PATCH | /aliases/{id}/protection-bypass | Update the protection bypass for a URL |

### certs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v8/certs/{id} | Get cert by id |
| DELETE | /v8/certs/{id} | Remove cert |
| POST | /v8/certs | Issue a new cert |
| PUT | /v8/certs | Upload a cert |

## Enhanced Skill Content
## Question Mapping

- "How do I deploy my project to Vercel?" -> POST /v13/deployments
- "What is the status of my deployment?" -> GET /v13/deployments/{idOrUrl}
- "How do I cancel a running build?" -> PATCH /v12/deployments/{id}/cancel
- "What domains are assigned to my project?" -> GET /v9/projects/{idOrName}/domains
- "How do I add a custom domain to my project?" -> POST /v10/projects/{idOrName}/domains
- "How do I set environment variables for my project?" -> POST /v10/projects/{idOrName}/env
- "Is this domain name available to purchase?" -> GET /v1/registrar/domains/{domain}/availability
- "How do I list all my projects?" -> GET /v10/projects
- "How do I create a feature flag?" -> PUT /v1/projects/{projectIdOrName}/feature-flags/flags
- "How do I rollback to a previous deployment?" -> POST /v1/projects/{projectId}/rollback/{deploymentId}
- "What are the build logs for my deployment?" -> GET /v3/deployments/{idOrUrl}/events
- "How do I add a team member?" -> POST /v2/teams/{teamId}/members
- "How do I create an edge config store?" -> POST /v1/edge-config
- "How do I set up a log drain for monitoring?" -> POST /v1/log-drains
- "How do I invalidate cached content by tag?" -> POST /v1/edge-cache/invalidate-by-tags

## Response Tips

- **Projects/Deployments**: Responses are deeply nested; key fields like `readyState`, `status`, and `alias` are top-level but build details, creator info, and git metadata are nested maps. Always check `readyState` (not `status`) for current deployment state.
- **List endpoints** (projects, domains, teams, deployments): Use `pagination.next` as the `since`/`from`/`next` param for cursor-based pagination; `pagination.count` gives total in current page, not total overall.
- **Error responses**: All endpoints share 400/401/403 patterns. A 429 means rate limit hit. 402 indicates a plan/billing limitation. 409 typically signals a conflict (duplicate domain, concurrent edit).
- **Edge Config**: Items are patched as arrays of operations, not full replacements. Check the `status` field in the response for confirmation. Schema endpoints return 412 on validation mismatch.
- **Registrar/Domains**: Price endpoints return `purchasePrice`, `renewalPrice`, and `transferPrice` as `any` type (can be number or string depending on currency context). Always pass `expectedPrice` when buying to prevent price drift.
- **Sandboxes**: The `sandbox` object is always wrapped in a `{sandbox: ...}` envelope. Check `status` field for lifecycle state. Commands return `exitCode: null` while still running.
- **Feature Flags**: Support optimistic concurrency via `ifMatch` header (ETag). A 304 means no change since your last fetch. A 412 means your version is stale.

## Anomaly Flags

- **429 on any endpoint**: Rate limit hit. Surface the `Retry-After` header and pause further calls. Registrar endpoints (domain availability, pricing) are especially rate-limited.
- **402 Payment Required**: The operation requires a plan upgrade or billing method. Surface this immediately as it blocks the workflow entirely. Common on deployments, edge config creation, domain purchases, and sandbox creation.
- **409 Conflict**: Indicates concurrent modification or duplicate resource. On domain operations, this often means the domain is already assigned elsewhere. On edge config, it means a write conflict.
- **`readyState: "ERROR"` or `errorMessage` present**: Deployment failed. Surface `errorCode`, `errorMessage`, `errorStep`, and `errorLink` together for actionable debugging.
- **`aliasWarning` is non-null**: Alias assignment had issues (e.g., domain not verified, CNAME conflict). Surface `aliasWarning.message` and `aliasWarning.action`.
- **`checksConclusion: "failed"`**: Deployment checks failed. Follow up with GET /v1/deployments/{id}/checks to identify which check and why.
- **`misconfigured: true`** on domain config: DNS is not pointing correctly. Surface `recommendedCNAME` or `recommendedIPv4` so the user can fix it.
- **`usageStatus.kind` not normal**: Project may be throttled or over quota. Surface `exceededAllowanceUntil` timestamp.
- **`leakedAt` on tokens**: A token was detected as leaked. Alert immediately and recommend rotation.
- **`firewallEnabled: false` on security config**: Firewall is off for the project. Proactively suggest enabling if security is a concern.
- **Sandbox `status: "stopped"` or `abortedAt` set**: Sandbox is no longer running. Commands will fail with 410.

## Playbook

### 1. Deploy a Project and Verify It Is Live

1. Create the deployment: POST /v13/deployments with `name` (project name), `files` or `gitSource`, and optional `target` (e.g., `"production"`).
2. Note the `id` and `readyState` from the response. If `readyState` is `"BUILDING"` or `"QUEUED"`, poll.
3. Poll deployment status: GET /v13/deployments/{id} until `readyState` is `"READY"` or `"ERROR"`.
4. If `"ERROR"`, read `errorMessage`, `errorCode`, and `errorStep` to diagnose.
5. If `"READY"`, confirm the live URL from the `url` field. Check `alias` array for assigned domains.
6. Optionally verify checks passed: GET /v1/deployments/{id}/checks and confirm all conclusions are `"succeeded"`.

### 2. Add and Verify a Custom Domain

1. Add the domain to the project: POST /v10/projects/{idOrName}/domains with `name` set to the domain (e.g., `"app.example.com"`).
2. Check the response `verified` field. If `false`, read the `verification` array for required DNS records.
3. Configure DNS at your registrar using the provided CNAME or A records.
4. Trigger verification: POST /v9/projects/{idOrName}/domains/{domain}/verify.
5. Confirm `verified: true` in the response. If still false, check config: GET /v6/domains/{domain}/config and review `misconfigured` and `recommendedCNAME`.

### 3. Set Up Environment Variables Across Environments

1. List existing env vars: GET /v10/projects/{idOrName}/env to avoid duplicates.
2. Create new variables: POST /v10/projects/{idOrName}/env with a body array of `{key, value, target, type}`. Set `target` to `["production", "preview", "development"]` as needed and `type` to `"encrypted"` for secrets.
3. To update a single variable: PATCH /v9/projects/{idOrName}/env/{id} with the new `value` or `target`.
4. To bulk-manage shared env vars across projects: use POST /v1/env with `projectId` array.
5. Redeploy to pick up changes if the project doesn't auto-deploy: POST /v13/deployments.

### 4. Purchase a Domain and Connect It

1. Check availability: GET /v1/registrar/domains/{domain}/availability. Confirm `available: true`.
2. Get pricing: GET /v1/registrar/domains/{domain}/price with desired `years`.
3. Purchase: POST /v1/registrar/domains/{domain}/buy with `expectedPrice` matching the price response, `contactInformation` (full address required), `years`, and `autoRenew`.
4. Track order: GET /v1/registrar/orders/{orderId} until `status` is complete.
5. Add to project: POST /v7/domains (registers in Vercel DNS), then POST /v10/projects/{idOrName}/domains with the domain name.
6. Verification is automatic when using Vercel nameservers. Confirm via GET /v6/domains/{domain}/config.

### 5. Set Up a Rolling Release with Manual Approval

1. Configure rolling release: PATCH /v1/projects/{idOrName}/rolling-release/config with stages defining `targetPercentage`, `requireApproval: true`, and `duration` for each stage.
2. Deploy normally: POST /v13/deployments with `target: "production"`. The rolling release activates automatically.
3. Monitor progress: GET /v1/projects/{idOrName}/rolling-release to see `activeStage`, canary vs. current deployment, and state.
4. When `activeStage.requireApproval` is true and the stage is ready, approve advancement: POST /v1/projects/{idOrName}/rolling-release/approve-stage with `nextStageIndex` and `canaryDeploymentId`.
5. After all stages pass, complete the rollout: POST /v1/projects/{idOrName}/rolling-release/complete with `canaryDeploymentId`. The canary becomes the production deployment.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
