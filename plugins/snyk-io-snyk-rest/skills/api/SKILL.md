---
name: snyk-api
description: "Snyk API skill. Use when working with Snyk for custom_base_images, groups, learn. Covers 250 endpoints."
version: 1.0.0
generator: lapsh
---

# Snyk API
API version: REST

## Auth
ApiKey Authorization in header | Bearer bearer

## Base URL
https://api.snyk.io/rest

## Setup
1. Set Authorization header with your Bearer token
2. GET /custom_base_images -- verify access
3. POST /custom_base_images -- create first custom_base_images

## Endpoints

250 endpoints across 7 groups. See references/api-spec.lap for full details.

### custom_base_images
| Method | Path | Description |
|--------|------|-------------|
| GET | /custom_base_images | Get a custom base image collection |
| POST | /custom_base_images | Create a Custom Base Image from an existing container project |
| DELETE | /custom_base_images/{custombaseimage_id} | Delete a custom base image |
| GET | /custom_base_images/{custombaseimage_id} | Get a custom base image |
| PATCH | /custom_base_images/{custombaseimage_id} | Update a custom base image |

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups | Get all groups (Early Access) |
| GET | /groups/{group_id} | Get Group (Early Access) |
| GET | /groups/{group_id}/apps/installs | Get a list of Snyk Apps installed for a Group |
| POST | /groups/{group_id}/apps/installs | Install a Snyk App for a Group |
| DELETE | /groups/{group_id}/apps/installs/{install_id} | Revoke app authorization for a Snyk group with install ID |
| POST | /groups/{group_id}/apps/installs/{install_id}/secrets | Manage client secret for non-interactive Snyk App installations |
| POST | /groups/{group_id}/assets/search | List Assets with filters (Early Access) |
| GET | /groups/{group_id}/assets/{asset_id} | Get an Asset by its ID (Early Access) |
| PATCH | /groups/{group_id}/assets/{asset_id} | Update asset attributes (Early Access) |
| GET | /groups/{group_id}/assets/{asset_id}/relationships/assets | List related assets with pagination (Early Access) |
| GET | /groups/{group_id}/assets/{asset_id}/relationships/projects | List asset projects with pagination (Early Access) |
| GET | /groups/{group_id}/audit_logs/search | Search Group audit logs. |
| POST | /groups/{group_id}/export | Start an export |
| GET | /groups/{group_id}/export/{export_id} | Get export results |
| GET | /groups/{group_id}/inventory/assets | List or search all assets (synchronous) - Group scope (Early Access) |
| PATCH | /groups/{group_id}/inventory/assets | Bulk update asset attributes - Group scope (Early Access) |
| GET | /groups/{group_id}/inventory/assets/filters | Get available filter fields - Group scope (Early Access) |
| GET | /groups/{group_id}/inventory/assets/filters/{filter_id}/values | Get filter value suggestions (autocomplete) - Group scope (Early Access) |
| GET | /groups/{group_id}/inventory/assets/groups | Get available group fields - Group scope (Early Access) |
| GET | /groups/{group_id}/inventory/assets/groups/{group_field}/values | Get group value aggregation - Group scope (Early Access) |
| POST | /groups/{group_id}/inventory/assets/searches | Create an asset search (asynchronous) - Group scope (Early Access) |
| GET | /groups/{group_id}/inventory/assets/searches/{search_id}/results | Retrieve asset search results (asynchronous) - Group scope (Early Access) |
| GET | /groups/{group_id}/inventory/assets/{asset_id} | Get a single asset by ID - Group scope (Early Access) |
| PATCH | /groups/{group_id}/inventory/assets/{asset_id} | Update asset attributes - Group scope (Early Access) |
| GET | /groups/{group_id}/inventory/assets/{asset_id}/relationships/projects | List projects for an asset (group scope) (Early Access) |
| GET | /groups/{group_id}/inventory/assets/{asset_id}/relationships/targets | List targets for an asset (group scope) (Early Access) |
| GET | /groups/{group_id}/issues | Get issues by group ID |
| GET | /groups/{group_id}/issues/{issue_id} | Get an issue |
| GET | /groups/{group_id}/jobs/export/{export_id} | Get export status |
| GET | /groups/{group_id}/memberships | Get all memberships of the group |
| POST | /groups/{group_id}/memberships | Create a group membership for a user with role |
| DELETE | /groups/{group_id}/memberships/{membership_id} | Delete a membership from a group |
| PATCH | /groups/{group_id}/memberships/{membership_id} | Update a role from a group membership |
| GET | /groups/{group_id}/org_memberships | Get list of org memberships of a group user |
| GET | /groups/{group_id}/orgs | List all organizations in group |
| GET | /groups/{group_id}/policies | Get group level policies (Early Access) |
| POST | /groups/{group_id}/policies | Create a new group level policy (Early Access) |
| DELETE | /groups/{group_id}/policies/{policy_id} | Delete an group-level policy (Early Access) |
| PATCH | /groups/{group_id}/policies/{policy_id} | Update a group-level policy (Early Access) |
| GET | /groups/{group_id}/service_accounts | Get a list of group service accounts. |
| POST | /groups/{group_id}/service_accounts | Create a service account for a group. |
| DELETE | /groups/{group_id}/service_accounts/{serviceaccount_id} | Delete a group service account. |
| GET | /groups/{group_id}/service_accounts/{serviceaccount_id} | Get a group service account. |
| PATCH | /groups/{group_id}/service_accounts/{serviceaccount_id} | Update a group service account. |
| POST | /groups/{group_id}/service_accounts/{serviceaccount_id}/secrets | Manage a group service account's client secret. |
| GET | /groups/{group_id}/settings/iac | Get the Infrastructure as Code Settings for a group |
| PATCH | /groups/{group_id}/settings/iac | Update the Infrastructure as Code Settings for a group |
| DELETE | /groups/{group_id}/settings/pull_request_template | Delete pull request template for group |
| GET | /groups/{group_id}/settings/pull_request_template | Get pull request template for group |
| POST | /groups/{group_id}/settings/pull_request_template | Create or update pull request template for group |
| GET | /groups/{group_id}/sso_connections | Get all SSO connections for a group (Early Access) |
| GET | /groups/{group_id}/sso_connections/{sso_id}/users | Get all users using a given SSO connection (Early Access) |
| DELETE | /groups/{group_id}/sso_connections/{sso_id}/users/{user_id} | Delete a user from a Group SSO connection (Early Access) |
| PATCH | /groups/{group_id}/users/{id} | Update a user's role in a group (Early Access) |

### learn
| Method | Path | Description |
|--------|------|-------------|
| GET | /learn/catalog | List Snyk Learn's resources (Early Access) |

### openapi
| Method | Path | Description |
|--------|------|-------------|
| GET | /openapi | List available versions of OpenAPI specification |
| GET | /openapi/{version} | Get OpenAPI specification effective at version. |

### orgs
| Method | Path | Description |
|--------|------|-------------|
| GET | /orgs | List accessible organizations |
| GET | /orgs/{org_id} | Get organization |
| PATCH | /orgs/{org_id} | Update organization |
| GET | /orgs/{org_id}/ai_bom_jobs/{job_id} | Get an AI-BOM job status (Early Access) |
| POST | /orgs/{org_id}/ai_boms | Create a new AI-BOM (Early Access) |
| POST | /orgs/{org_id}/ai_boms/upload | Create and upload an AI-BOM (Early Access) |
| GET | /orgs/{org_id}/ai_boms/{ai_bom_id} | Get an AI-BOM. (Early Access) |
| GET | /orgs/{org_id}/app_bots | Get a list of app bots authorized to an organization. |
| DELETE | /orgs/{org_id}/app_bots/{bot_id} | Revoke app bot authorization |
| GET | /orgs/{org_id}/apps | Get a list of Snyk Apps created by an Organization |
| POST | /orgs/{org_id}/apps | Create a new app for an organization. |
| GET | /orgs/{org_id}/apps/creations | Get a list of Snyk Apps created by an Organization |
| POST | /orgs/{org_id}/apps/creations | Create a new Snyk App for an organization |
| DELETE | /orgs/{org_id}/apps/creations/{app_id} | Delete a Snyk App by app ID |
| GET | /orgs/{org_id}/apps/creations/{app_id} | Get a Snyk App by app ID |
| PATCH | /orgs/{org_id}/apps/creations/{app_id} | Update app creation attributes such as name, redirect URIs, and access token time to live using the App ID |
| POST | /orgs/{org_id}/apps/creations/{app_id}/secrets | Manage client secret for a Snyk App |
| GET | /orgs/{org_id}/apps/installs | Get a list of Snyk Apps installed for an Organization |
| POST | /orgs/{org_id}/apps/installs | Install a Snyk App for an Organization |
| DELETE | /orgs/{org_id}/apps/installs/{install_id} | Revoke app authorization for a Snyk organization with install ID |
| POST | /orgs/{org_id}/apps/installs/{install_id}/secrets | Manage client secret for non-interactive Snyk App installations |
| DELETE | /orgs/{org_id}/apps/{client_id} | Delete an app |
| GET | /orgs/{org_id}/apps/{client_id} | Get an app by client id |
| PATCH | /orgs/{org_id}/apps/{client_id} | Update app attributes that are name, redirect URIs, and access token time to live |
| POST | /orgs/{org_id}/apps/{client_id}/secrets | Manage client secrets for an app. |
| GET | /orgs/{org_id}/audit_logs/search | Search Organization audit logs. |
| GET | /orgs/{org_id}/brokers/connections | List Broker connections for a given organization |
| GET | /orgs/{org_id}/cloud/environments | List Environments (Early Access) |
| POST | /orgs/{org_id}/cloud/environments | Create New Environment (Early Access) |
| DELETE | /orgs/{org_id}/cloud/environments/{environment_id} | Delete Environment (Early Access) |
| PATCH | /orgs/{org_id}/cloud/environments/{environment_id} | Update Environment (Early Access) |
| POST | /orgs/{org_id}/cloud/permissions | Generate Cloud Provider Permissions (Early Access) |
| GET | /orgs/{org_id}/cloud/resources | List Resources (Early Access) |
| GET | /orgs/{org_id}/cloud/scans | List Scans (Early Access) |
| POST | /orgs/{org_id}/cloud/scans | Create Scan (Early Access) |
| GET | /orgs/{org_id}/cloud/scans/{scan_id} | Get scan (Early Access) |
| GET | /orgs/{org_id}/collections | Get collections |
| POST | /orgs/{org_id}/collections | Create a collection |
| DELETE | /orgs/{org_id}/collections/{collection_id} | Delete a collection |
| GET | /orgs/{org_id}/collections/{collection_id} | Get a collection |
| PATCH | /orgs/{org_id}/collections/{collection_id} | Edit a collection |
| DELETE | /orgs/{org_id}/collections/{collection_id}/relationships/projects | Remove projects from a collection |
| GET | /orgs/{org_id}/collections/{collection_id}/relationships/projects | Get projects from the specified collection |
| POST | /orgs/{org_id}/collections/{collection_id}/relationships/projects | Add projects to a collection |
| GET | /orgs/{org_id}/container_images | List instances of container image |
| GET | /orgs/{org_id}/container_images/{image_id} | Get instance of container image |
| GET | /orgs/{org_id}/container_images/{image_id}/relationships/image_target_refs | List instances of image target references for a container image |
| POST | /orgs/{org_id}/container_import/{integration_id}/policy/dry_run | Create a dry run job for a container registry import policy (Early Access) |
| GET | /orgs/{org_id}/container_import/{integration_id}/policy/dry_run/{job_id} | Get a dry run job (Early Access) |
| GET | /orgs/{org_id}/ecosystems/{ecosystem}/packages/{package_name} | Get a package (Early Access) |
| GET | /orgs/{org_id}/ecosystems/{ecosystem}/packages/{package_name}/versions/{package_version} | Get a package version (Early Access) |
| POST | /orgs/{org_id}/export | Start an export |
| GET | /orgs/{org_id}/export/{export_id} | Get export results |
| GET | /orgs/{org_id}/inventory/assets | List or search all assets (synchronous) - Org scope (Early Access) |
| PATCH | /orgs/{org_id}/inventory/assets | Bulk update asset attributes - Org scope (Early Access) |
| GET | /orgs/{org_id}/inventory/assets/filters | Get available filter fields - Org scope (Early Access) |
| GET | /orgs/{org_id}/inventory/assets/filters/{filter_id}/values | Get filter value suggestions (autocomplete) - Org scope (Early Access) |
| GET | /orgs/{org_id}/inventory/assets/groups | Get available group fields - Org scope (Early Access) |
| GET | /orgs/{org_id}/inventory/assets/groups/{group_field}/values | Get group value aggregation - Org scope (Early Access) |
| POST | /orgs/{org_id}/inventory/assets/searches | Create an asset search (asynchronous) - Org scope (Early Access) |
| GET | /orgs/{org_id}/inventory/assets/searches/{search_id}/results | Retrieve asset search results (asynchronous) - Org scope (Early Access) |
| GET | /orgs/{org_id}/inventory/assets/{asset_id} | Get a single asset by ID - Org scope (Early Access) |
| PATCH | /orgs/{org_id}/inventory/assets/{asset_id} | Update asset attributes - Org scope (Early Access) |
| GET | /orgs/{org_id}/inventory/assets/{asset_id}/relationships/projects | List projects for an asset (org scope) (Early Access) |
| GET | /orgs/{org_id}/inventory/assets/{asset_id}/relationships/targets | List targets for an asset (org scope) (Early Access) |
| GET | /orgs/{org_id}/invites | List pending user invitations to an organization. |
| POST | /orgs/{org_id}/invites | Invite a user to an organization |
| DELETE | /orgs/{org_id}/invites/{invite_id} | Cancel a pending user invitations to an organization. |
| GET | /orgs/{org_id}/issues | Get issues by org ID |
| GET | /orgs/{org_id}/issues/{issue_id} | Get an issue |
| GET | /orgs/{org_id}/jobs/export/{export_id} | Get export status |
| DELETE | /orgs/{org_id}/learn/assignments | Bulk deletion of assignments in an organization (Early Access) |
| GET | /orgs/{org_id}/learn/assignments | Retrieve a list of assignments for an organization (Early Access) |
| PATCH | /orgs/{org_id}/learn/assignments | Update due date for assignments in an organization. (Early Access) |
| POST | /orgs/{org_id}/learn/assignments | Bulk creation of assignments for users in an organization. (Early Access) |
| POST | /orgs/{org_id}/learn/assignments/bulk_delete | Bulk deletion of assignments in an organization (Early Access) |
| GET | /orgs/{org_id}/learn/progress/catalog | Get collective learning progress (Early Access) |
| GET | /orgs/{org_id}/learn/progress/users | Get individual user learning progress (Early Access) |
| GET | /orgs/{org_id}/memberships | Get all memberships of the org |
| POST | /orgs/{org_id}/memberships | Create a org membership for a user with role |
| DELETE | /orgs/{org_id}/memberships/{membership_id} | Remove user's org membership |
| PATCH | /orgs/{org_id}/memberships/{membership_id} | Update a org membership for a user with role |
| POST | /orgs/{org_id}/packages/issues | List issues for a given set of packages  (Currently not available to all customers) |
| GET | /orgs/{org_id}/packages/{purl}/issues | List issues for a package |
| GET | /orgs/{org_id}/policies | Get org-level policies |
| POST | /orgs/{org_id}/policies | Create a new org-level policy |
| DELETE | /orgs/{org_id}/policies/{policy_id} | Delete an org-level policy |
| GET | /orgs/{org_id}/policies/{policy_id} | Get an org-level policy |
| PATCH | /orgs/{org_id}/policies/{policy_id} | Update an org-level policy |
| GET | /orgs/{org_id}/policies/{policy_id}/events | List org policy events (Early Access) |
| GET | /orgs/{org_id}/projects | List all Projects for an Org with the given Org ID. |
| DELETE | /orgs/{org_id}/projects/{project_id} | Delete project by project ID. |
| GET | /orgs/{org_id}/projects/{project_id} | Get project by project ID. |
| PATCH | /orgs/{org_id}/projects/{project_id} | Updates project by project ID. |
| GET | /orgs/{org_id}/projects/{project_id}/sbom | Get a project’s SBOM document |
| POST | /orgs/{org_id}/sbom_tests | Create an SBOM test run (Early Access) |
| GET | /orgs/{org_id}/sbom_tests/{job_id} | Gets an SBOM test run status (Early Access) |
| GET | /orgs/{org_id}/sbom_tests/{job_id}/results | Gets an SBOM test run result (Early Access) |
| GET | /orgs/{org_id}/service_accounts | Get a list of organization service accounts. |
| POST | /orgs/{org_id}/service_accounts | Create a service account for an organization. |
| DELETE | /orgs/{org_id}/service_accounts/{serviceaccount_id} | Delete a service account in an organization. |
| GET | /orgs/{org_id}/service_accounts/{serviceaccount_id} | Get an organization service account. |
| PATCH | /orgs/{org_id}/service_accounts/{serviceaccount_id} | Update an organization service account. |
| POST | /orgs/{org_id}/service_accounts/{serviceaccount_id}/secrets | Manage an organization service account's client secret. |
| GET | /orgs/{org_id}/settings/iac | Get the Infrastructure as Code Settings for an org. |
| PATCH | /orgs/{org_id}/settings/iac | Update the Infrastructure as Code Settings for an org |
| GET | /orgs/{org_id}/settings/opensource | Get the Open Source Settings for an Org. (Early Access) |
| GET | /orgs/{org_id}/settings/sast | Retrieves the SAST settings for an org |
| PATCH | /orgs/{org_id}/settings/sast | Enable/Disable the Snyk Code settings for an org |
| DELETE | /orgs/{org_id}/slack_app/{bot_id} | Remove the given Slack App integration |
| GET | /orgs/{org_id}/slack_app/{bot_id} | Get Slack integration default notification settings. |
| POST | /orgs/{org_id}/slack_app/{bot_id} | Create new Slack notification default settings. |
| GET | /orgs/{org_id}/slack_app/{bot_id}/projects | Slack notification settings overrides for projects |
| DELETE | /orgs/{org_id}/slack_app/{bot_id}/projects/{project_id} | Remove Slack settings override for a project. |
| PATCH | /orgs/{org_id}/slack_app/{bot_id}/projects/{project_id} | Update Slack notification settings for a project. |
| POST | /orgs/{org_id}/slack_app/{bot_id}/projects/{project_id} | Create a new Slack settings override for a given project. |
| GET | /orgs/{org_id}/slack_app/{tenant_id}/channels | Get a list of Slack channels |
| GET | /orgs/{org_id}/slack_app/{tenant_id}/channels/{channel_id} | Get Slack Channel name by Slack Channel ID. |
| GET | /orgs/{org_id}/targets | Get targets by org ID |
| DELETE | /orgs/{org_id}/targets/{target_id} | Delete target by target ID |
| GET | /orgs/{org_id}/targets/{target_id} | Get target by target ID |
| GET | /orgs/{org_id}/test_jobs/{job_id} | Get a test job. (Early Access) |
| POST | /orgs/{org_id}/tests | Create a new test. (Early Access) |
| GET | /orgs/{org_id}/tests/{test_id} | Get a test. (Early Access) |
| GET | /orgs/{org_id}/tests/{test_id}/findings | List findings for a test. (Early Access) |
| GET | /orgs/{org_id}/users/{id} | Get user by ID (Early Access) |

### self
| Method | Path | Description |
|--------|------|-------------|
| GET | /self | My User Details |
| GET | /self/access_requests | Get access requests (Early Access) |
| GET | /self/apps | Get a list of Snyk Apps that can act on your behalf |
| GET | /self/apps/installs | Get a list of Snyk Apps installed for a user |
| DELETE | /self/apps/installs/{install_id} | Revoke a Snyk App by install ID |
| DELETE | /self/apps/{app_id} | Revoke a Snyk App by app ID |
| GET | /self/apps/{app_id}/sessions | Get a list of active OAuth sessions by app ID |
| DELETE | /self/apps/{app_id}/sessions/{session_id} | Revoke the Snyk App session of an active user |
| GET | /self/personal_access_tokens | List personal access tokens |
| DELETE | /self/personal_access_tokens/{personal_access_token_id} | Deletes a personal access token |

### tenants
| Method | Path | Description |
|--------|------|-------------|
| GET | /tenants | Get a list of all accessible Tenants |
| GET | /tenants/{tenant_id} | Get a single Tenant by ID |
| PATCH | /tenants/{tenant_id} | Update tenant |
| GET | /tenants/{tenant_id}/brokers/connections/{connection_id}/integrations | Get Integrations using the current Broker connection |
| POST | /tenants/{tenant_id}/brokers/connections/{connection_id}/orgs/{org_id}/integration | Creates Broker connection Integration Configuration |
| DELETE | /tenants/{tenant_id}/brokers/connections/{connection_id}/orgs/{org_id}/integrations/{integration_id} | Deletes an Integration for a Broker connection |
| GET | /tenants/{tenant_id}/brokers/deployments | List Broker deployments for tenant |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/connections/{connection_id}/contexts | List Connection contexts |
| DELETE | /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id} | Deletes broker context |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id} | List Connection context |
| PATCH | /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id} | Updates Broker Context |
| PATCH | /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id}/integration | Updates an integration to be associated with a Broker context |
| DELETE | /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id}/integrations/{integration_id} | Deletes the Broker context association with an Integration |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments | List Broker deployments |
| POST | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments | Creates Broker Deployment |
| DELETE | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id} | Deletes Broker deployment |
| PATCH | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id} | Updates Broker deployment |
| DELETE | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections | Deletes Broker connections |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections | List Broker connections |
| POST | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections | Creates Broker connection |
| DELETE | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id} | Deletes Broker connection |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id} | Get Broker connection |
| PATCH | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id} | Updates Broker connection |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id}/bulk_migration | List organizations for bulk migration |
| POST | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id}/bulk_migration | Performs bulk migration integrations to universal broker |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/contexts | List Deployment contexts |
| POST | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/contexts | Create broker Context |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials | List Deployment credentials |
| POST | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials | Create deployment credential |
| DELETE | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials/{credential_id} | Deletes Deployment credential |
| GET | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials/{credential_id} | Get Deployment credential |
| PATCH | /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials/{credential_id} | Updates Deployment credential |
| GET | /tenants/{tenant_id}/inventory/assets | List or search all assets (synchronous) (Early Access) |
| PATCH | /tenants/{tenant_id}/inventory/assets | Bulk update asset attributes (Early Access) |
| GET | /tenants/{tenant_id}/inventory/assets/filters | Get available filter fields (Early Access) |
| GET | /tenants/{tenant_id}/inventory/assets/filters/{filter_id}/values | Get filter value suggestions (autocomplete) (Early Access) |
| GET | /tenants/{tenant_id}/inventory/assets/groups | Get available group fields (Early Access) |
| GET | /tenants/{tenant_id}/inventory/assets/groups/{group_field}/values | Get group value aggregation (Early Access) |
| POST | /tenants/{tenant_id}/inventory/assets/searches | Create an asset search (asynchronous) (Early Access) |
| GET | /tenants/{tenant_id}/inventory/assets/searches/{search_id}/results | Retrieve asset search results (asynchronous) (Early Access) |
| GET | /tenants/{tenant_id}/inventory/assets/{asset_id} | Get a single asset by ID (Early Access) |
| PATCH | /tenants/{tenant_id}/inventory/assets/{asset_id} | Update asset attributes (Early Access) |
| GET | /tenants/{tenant_id}/inventory/assets/{asset_id}/relationships/projects | List projects for an asset (Early Access) |
| GET | /tenants/{tenant_id}/inventory/assets/{asset_id}/relationships/targets | List targets for an asset (Early Access) |
| GET | /tenants/{tenant_id}/memberships | Get all memberships of the tenant (Early Access) |
| DELETE | /tenants/{tenant_id}/memberships/{membership_id} | Delete an individual tenant membership for a single user. (Early Access) |
| PATCH | /tenants/{tenant_id}/memberships/{membership_id} | Update tenant membership (Early Access) |
| GET | /tenants/{tenant_id}/roles | List all available roles for a given tenant (Early Access) |
| POST | /tenants/{tenant_id}/roles | Create a custom tenant role for a given tenant (Early Access) |
| DELETE | /tenants/{tenant_id}/roles/{role_id} | Delete a specific tenant role by its id and its tenant id. (Early Access) |
| GET | /tenants/{tenant_id}/roles/{role_id} | Return a specific role by its id and its tenant id. (Early Access) |
| PATCH | /tenants/{tenant_id}/roles/{role_id} | Update a specific tenant role by its id and its tenant id. (Early Access) |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all custom_base_images?" -> GET /custom_base_images
- "Create a custom_base_image?" -> POST /custom_base_images
- "Delete a custom_base_image?" -> DELETE /custom_base_images/{custombaseimage_id}
- "Get custom_base_image details?" -> GET /custom_base_images/{custombaseimage_id}
- "Partially update a custom_base_image?" -> PATCH /custom_base_images/{custombaseimage_id}
- "List all groups?" -> GET /groups
- "Get group details?" -> GET /groups/{group_id}
- "List all installs?" -> GET /groups/{group_id}/apps/installs
- "Create a install?" -> POST /groups/{group_id}/apps/installs
- "Delete a install?" -> DELETE /groups/{group_id}/apps/installs/{install_id}
- "Create a secret?" -> POST /groups/{group_id}/apps/installs/{install_id}/secrets
- "Create a search?" -> POST /groups/{group_id}/assets/search
- "Get asset details?" -> GET /groups/{group_id}/assets/{asset_id}
- "Partially update a asset?" -> PATCH /groups/{group_id}/assets/{asset_id}
- "List all assets?" -> GET /groups/{group_id}/assets/{asset_id}/relationships/assets
- "List all projects?" -> GET /groups/{group_id}/assets/{asset_id}/relationships/projects
- "List all search?" -> GET /groups/{group_id}/audit_logs/search
- "Create a export?" -> POST /groups/{group_id}/export
- "Get export details?" -> GET /groups/{group_id}/export/{export_id}
- "List all assets?" -> GET /groups/{group_id}/inventory/assets
- "List all filters?" -> GET /groups/{group_id}/inventory/assets/filters
- "Search values?" -> GET /groups/{group_id}/inventory/assets/filters/{filter_id}/values
- "List all groups?" -> GET /groups/{group_id}/inventory/assets/groups
- "List all values?" -> GET /groups/{group_id}/inventory/assets/groups/{group_field}/values
- "Create a searche?" -> POST /groups/{group_id}/inventory/assets/searches
- "List all results?" -> GET /groups/{group_id}/inventory/assets/searches/{search_id}/results
- "Get asset details?" -> GET /groups/{group_id}/inventory/assets/{asset_id}
- "Partially update a asset?" -> PATCH /groups/{group_id}/inventory/assets/{asset_id}
- "List all projects?" -> GET /groups/{group_id}/inventory/assets/{asset_id}/relationships/projects
- "List all targets?" -> GET /groups/{group_id}/inventory/assets/{asset_id}/relationships/targets
- "List all issues?" -> GET /groups/{group_id}/issues
- "Get issue details?" -> GET /groups/{group_id}/issues/{issue_id}
- "Get export details?" -> GET /groups/{group_id}/jobs/export/{export_id}
- "List all memberships?" -> GET /groups/{group_id}/memberships
- "Create a membership?" -> POST /groups/{group_id}/memberships
- "Delete a membership?" -> DELETE /groups/{group_id}/memberships/{membership_id}
- "Partially update a membership?" -> PATCH /groups/{group_id}/memberships/{membership_id}
- "List all org_memberships?" -> GET /groups/{group_id}/org_memberships
- "List all orgs?" -> GET /groups/{group_id}/orgs
- "List all policies?" -> GET /groups/{group_id}/policies
- "Create a policy?" -> POST /groups/{group_id}/policies
- "Delete a policy?" -> DELETE /groups/{group_id}/policies/{policy_id}
- "Partially update a policy?" -> PATCH /groups/{group_id}/policies/{policy_id}
- "List all service_accounts?" -> GET /groups/{group_id}/service_accounts
- "Create a service_account?" -> POST /groups/{group_id}/service_accounts
- "Delete a service_account?" -> DELETE /groups/{group_id}/service_accounts/{serviceaccount_id}
- "Get service_account details?" -> GET /groups/{group_id}/service_accounts/{serviceaccount_id}
- "Partially update a service_account?" -> PATCH /groups/{group_id}/service_accounts/{serviceaccount_id}
- "Create a secret?" -> POST /groups/{group_id}/service_accounts/{serviceaccount_id}/secrets
- "List all iac?" -> GET /groups/{group_id}/settings/iac
- "List all pull_request_template?" -> GET /groups/{group_id}/settings/pull_request_template
- "Create a pull_request_template?" -> POST /groups/{group_id}/settings/pull_request_template
- "List all sso_connections?" -> GET /groups/{group_id}/sso_connections
- "List all users?" -> GET /groups/{group_id}/sso_connections/{sso_id}/users
- "Delete a user?" -> DELETE /groups/{group_id}/sso_connections/{sso_id}/users/{user_id}
- "Partially update a user?" -> PATCH /groups/{group_id}/users/{id}
- "List all catalog?" -> GET /learn/catalog
- "List all openapi?" -> GET /openapi
- "Get openapi details?" -> GET /openapi/{version}
- "List all orgs?" -> GET /orgs
- "Get org details?" -> GET /orgs/{org_id}
- "Partially update a org?" -> PATCH /orgs/{org_id}
- "Get ai_bom_job details?" -> GET /orgs/{org_id}/ai_bom_jobs/{job_id}
- "Create a ai_bom?" -> POST /orgs/{org_id}/ai_boms
- "Create a upload?" -> POST /orgs/{org_id}/ai_boms/upload
- "Get ai_bom details?" -> GET /orgs/{org_id}/ai_boms/{ai_bom_id}
- "List all app_bots?" -> GET /orgs/{org_id}/app_bots
- "Delete a app_bot?" -> DELETE /orgs/{org_id}/app_bots/{bot_id}
- "List all apps?" -> GET /orgs/{org_id}/apps
- "Create a app?" -> POST /orgs/{org_id}/apps
- "List all creations?" -> GET /orgs/{org_id}/apps/creations
- "Create a creation?" -> POST /orgs/{org_id}/apps/creations
- "Delete a creation?" -> DELETE /orgs/{org_id}/apps/creations/{app_id}
- "Get creation details?" -> GET /orgs/{org_id}/apps/creations/{app_id}
- "Partially update a creation?" -> PATCH /orgs/{org_id}/apps/creations/{app_id}
- "Create a secret?" -> POST /orgs/{org_id}/apps/creations/{app_id}/secrets
- "List all installs?" -> GET /orgs/{org_id}/apps/installs
- "Create a install?" -> POST /orgs/{org_id}/apps/installs
- "Delete a install?" -> DELETE /orgs/{org_id}/apps/installs/{install_id}
- "Create a secret?" -> POST /orgs/{org_id}/apps/installs/{install_id}/secrets
- "Delete a app?" -> DELETE /orgs/{org_id}/apps/{client_id}
- "Get app details?" -> GET /orgs/{org_id}/apps/{client_id}
- "Partially update a app?" -> PATCH /orgs/{org_id}/apps/{client_id}
- "Create a secret?" -> POST /orgs/{org_id}/apps/{client_id}/secrets
- "List all search?" -> GET /orgs/{org_id}/audit_logs/search
- "List all connections?" -> GET /orgs/{org_id}/brokers/connections
- "List all environments?" -> GET /orgs/{org_id}/cloud/environments
- "Create a environment?" -> POST /orgs/{org_id}/cloud/environments
- "Delete a environment?" -> DELETE /orgs/{org_id}/cloud/environments/{environment_id}
- "Partially update a environment?" -> PATCH /orgs/{org_id}/cloud/environments/{environment_id}
- "Create a permission?" -> POST /orgs/{org_id}/cloud/permissions
- "List all resources?" -> GET /orgs/{org_id}/cloud/resources
- "List all scans?" -> GET /orgs/{org_id}/cloud/scans
- "Create a scan?" -> POST /orgs/{org_id}/cloud/scans
- "Get scan details?" -> GET /orgs/{org_id}/cloud/scans/{scan_id}
- "List all collections?" -> GET /orgs/{org_id}/collections
- "Create a collection?" -> POST /orgs/{org_id}/collections
- "Delete a collection?" -> DELETE /orgs/{org_id}/collections/{collection_id}
- "Get collection details?" -> GET /orgs/{org_id}/collections/{collection_id}
- "Partially update a collection?" -> PATCH /orgs/{org_id}/collections/{collection_id}
- "List all projects?" -> GET /orgs/{org_id}/collections/{collection_id}/relationships/projects
- "Create a project?" -> POST /orgs/{org_id}/collections/{collection_id}/relationships/projects
- "List all container_images?" -> GET /orgs/{org_id}/container_images
- "Get container_image details?" -> GET /orgs/{org_id}/container_images/{image_id}
- "List all image_target_refs?" -> GET /orgs/{org_id}/container_images/{image_id}/relationships/image_target_refs
- "Create a dry_run?" -> POST /orgs/{org_id}/container_import/{integration_id}/policy/dry_run
- "Get dry_run details?" -> GET /orgs/{org_id}/container_import/{integration_id}/policy/dry_run/{job_id}
- "Get package details?" -> GET /orgs/{org_id}/ecosystems/{ecosystem}/packages/{package_name}
- "Get version details?" -> GET /orgs/{org_id}/ecosystems/{ecosystem}/packages/{package_name}/versions/{package_version}
- "Create a export?" -> POST /orgs/{org_id}/export
- "Get export details?" -> GET /orgs/{org_id}/export/{export_id}
- "List all assets?" -> GET /orgs/{org_id}/inventory/assets
- "List all filters?" -> GET /orgs/{org_id}/inventory/assets/filters
- "Search values?" -> GET /orgs/{org_id}/inventory/assets/filters/{filter_id}/values
- "List all groups?" -> GET /orgs/{org_id}/inventory/assets/groups
- "List all values?" -> GET /orgs/{org_id}/inventory/assets/groups/{group_field}/values
- "Create a searche?" -> POST /orgs/{org_id}/inventory/assets/searches
- "List all results?" -> GET /orgs/{org_id}/inventory/assets/searches/{search_id}/results
- "Get asset details?" -> GET /orgs/{org_id}/inventory/assets/{asset_id}
- "Partially update a asset?" -> PATCH /orgs/{org_id}/inventory/assets/{asset_id}
- "List all projects?" -> GET /orgs/{org_id}/inventory/assets/{asset_id}/relationships/projects
- "List all targets?" -> GET /orgs/{org_id}/inventory/assets/{asset_id}/relationships/targets
- "List all invites?" -> GET /orgs/{org_id}/invites
- "Create a invite?" -> POST /orgs/{org_id}/invites
- "Delete a invite?" -> DELETE /orgs/{org_id}/invites/{invite_id}
- "List all issues?" -> GET /orgs/{org_id}/issues
- "Get issue details?" -> GET /orgs/{org_id}/issues/{issue_id}
- "Get export details?" -> GET /orgs/{org_id}/jobs/export/{export_id}
- "List all assignments?" -> GET /orgs/{org_id}/learn/assignments
- "Create a assignment?" -> POST /orgs/{org_id}/learn/assignments
- "Create a bulk_delete?" -> POST /orgs/{org_id}/learn/assignments/bulk_delete
- "List all catalog?" -> GET /orgs/{org_id}/learn/progress/catalog
- "List all users?" -> GET /orgs/{org_id}/learn/progress/users
- "List all memberships?" -> GET /orgs/{org_id}/memberships
- "Create a membership?" -> POST /orgs/{org_id}/memberships
- "Delete a membership?" -> DELETE /orgs/{org_id}/memberships/{membership_id}
- "Partially update a membership?" -> PATCH /orgs/{org_id}/memberships/{membership_id}
- "Create a issue?" -> POST /orgs/{org_id}/packages/issues
- "List all issues?" -> GET /orgs/{org_id}/packages/{purl}/issues
- "Search policies?" -> GET /orgs/{org_id}/policies
- "Create a policy?" -> POST /orgs/{org_id}/policies
- "Delete a policy?" -> DELETE /orgs/{org_id}/policies/{policy_id}
- "Get policy details?" -> GET /orgs/{org_id}/policies/{policy_id}
- "Partially update a policy?" -> PATCH /orgs/{org_id}/policies/{policy_id}
- "List all events?" -> GET /orgs/{org_id}/policies/{policy_id}/events
- "List all projects?" -> GET /orgs/{org_id}/projects
- "Delete a project?" -> DELETE /orgs/{org_id}/projects/{project_id}
- "Get project details?" -> GET /orgs/{org_id}/projects/{project_id}
- "Partially update a project?" -> PATCH /orgs/{org_id}/projects/{project_id}
- "List all sbom?" -> GET /orgs/{org_id}/projects/{project_id}/sbom
- "Create a sbom_test?" -> POST /orgs/{org_id}/sbom_tests
- "Get sbom_test details?" -> GET /orgs/{org_id}/sbom_tests/{job_id}
- "List all results?" -> GET /orgs/{org_id}/sbom_tests/{job_id}/results
- "List all service_accounts?" -> GET /orgs/{org_id}/service_accounts
- "Create a service_account?" -> POST /orgs/{org_id}/service_accounts
- "Delete a service_account?" -> DELETE /orgs/{org_id}/service_accounts/{serviceaccount_id}
- "Get service_account details?" -> GET /orgs/{org_id}/service_accounts/{serviceaccount_id}
- "Partially update a service_account?" -> PATCH /orgs/{org_id}/service_accounts/{serviceaccount_id}
- "Create a secret?" -> POST /orgs/{org_id}/service_accounts/{serviceaccount_id}/secrets
- "List all iac?" -> GET /orgs/{org_id}/settings/iac
- "List all opensource?" -> GET /orgs/{org_id}/settings/opensource
- "List all sast?" -> GET /orgs/{org_id}/settings/sast
- "Delete a slack_app?" -> DELETE /orgs/{org_id}/slack_app/{bot_id}
- "Get slack_app details?" -> GET /orgs/{org_id}/slack_app/{bot_id}
- "List all projects?" -> GET /orgs/{org_id}/slack_app/{bot_id}/projects
- "Delete a project?" -> DELETE /orgs/{org_id}/slack_app/{bot_id}/projects/{project_id}
- "Partially update a project?" -> PATCH /orgs/{org_id}/slack_app/{bot_id}/projects/{project_id}
- "List all channels?" -> GET /orgs/{org_id}/slack_app/{tenant_id}/channels
- "Get channel details?" -> GET /orgs/{org_id}/slack_app/{tenant_id}/channels/{channel_id}
- "List all targets?" -> GET /orgs/{org_id}/targets
- "Delete a target?" -> DELETE /orgs/{org_id}/targets/{target_id}
- "Get target details?" -> GET /orgs/{org_id}/targets/{target_id}
- "Get test_job details?" -> GET /orgs/{org_id}/test_jobs/{job_id}
- "Create a test?" -> POST /orgs/{org_id}/tests
- "Get test details?" -> GET /orgs/{org_id}/tests/{test_id}
- "List all findings?" -> GET /orgs/{org_id}/tests/{test_id}/findings
- "Get user details?" -> GET /orgs/{org_id}/users/{id}
- "List all self?" -> GET /self
- "List all access_requests?" -> GET /self/access_requests
- "List all apps?" -> GET /self/apps
- "List all installs?" -> GET /self/apps/installs
- "Delete a install?" -> DELETE /self/apps/installs/{install_id}
- "Delete a app?" -> DELETE /self/apps/{app_id}
- "List all sessions?" -> GET /self/apps/{app_id}/sessions
- "Delete a session?" -> DELETE /self/apps/{app_id}/sessions/{session_id}
- "List all personal_access_tokens?" -> GET /self/personal_access_tokens
- "Delete a personal_access_token?" -> DELETE /self/personal_access_tokens/{personal_access_token_id}
- "List all tenants?" -> GET /tenants
- "Get tenant details?" -> GET /tenants/{tenant_id}
- "Partially update a tenant?" -> PATCH /tenants/{tenant_id}
- "List all integrations?" -> GET /tenants/{tenant_id}/brokers/connections/{connection_id}/integrations
- "Create a integration?" -> POST /tenants/{tenant_id}/brokers/connections/{connection_id}/orgs/{org_id}/integration
- "Delete a integration?" -> DELETE /tenants/{tenant_id}/brokers/connections/{connection_id}/orgs/{org_id}/integrations/{integration_id}
- "List all deployments?" -> GET /tenants/{tenant_id}/brokers/deployments
- "List all contexts?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/connections/{connection_id}/contexts
- "Delete a context?" -> DELETE /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id}
- "Get context details?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id}
- "Partially update a context?" -> PATCH /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id}
- "Delete a integration?" -> DELETE /tenants/{tenant_id}/brokers/installs/{install_id}/contexts/{context_id}/integrations/{integration_id}
- "List all deployments?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/deployments
- "Create a deployment?" -> POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments
- "Delete a deployment?" -> DELETE /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}
- "Partially update a deployment?" -> PATCH /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}
- "List all connections?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections
- "Create a connection?" -> POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections
- "Delete a connection?" -> DELETE /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id}
- "Get connection details?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id}
- "Partially update a connection?" -> PATCH /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id}
- "List all bulk_migration?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id}/bulk_migration
- "Create a bulk_migration?" -> POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections/{connection_id}/bulk_migration
- "List all contexts?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/contexts
- "Create a context?" -> POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/contexts
- "List all credentials?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials
- "Create a credential?" -> POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials
- "Delete a credential?" -> DELETE /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials/{credential_id}
- "Get credential details?" -> GET /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials/{credential_id}
- "Partially update a credential?" -> PATCH /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials/{credential_id}
- "List all assets?" -> GET /tenants/{tenant_id}/inventory/assets
- "List all filters?" -> GET /tenants/{tenant_id}/inventory/assets/filters
- "Search values?" -> GET /tenants/{tenant_id}/inventory/assets/filters/{filter_id}/values
- "List all groups?" -> GET /tenants/{tenant_id}/inventory/assets/groups
- "List all values?" -> GET /tenants/{tenant_id}/inventory/assets/groups/{group_field}/values
- "Create a searche?" -> POST /tenants/{tenant_id}/inventory/assets/searches
- "List all results?" -> GET /tenants/{tenant_id}/inventory/assets/searches/{search_id}/results
- "Get asset details?" -> GET /tenants/{tenant_id}/inventory/assets/{asset_id}
- "Partially update a asset?" -> PATCH /tenants/{tenant_id}/inventory/assets/{asset_id}
- "List all projects?" -> GET /tenants/{tenant_id}/inventory/assets/{asset_id}/relationships/projects
- "List all targets?" -> GET /tenants/{tenant_id}/inventory/assets/{asset_id}/relationships/targets
- "List all memberships?" -> GET /tenants/{tenant_id}/memberships
- "Delete a membership?" -> DELETE /tenants/{tenant_id}/memberships/{membership_id}
- "Partially update a membership?" -> PATCH /tenants/{tenant_id}/memberships/{membership_id}
- "List all roles?" -> GET /tenants/{tenant_id}/roles
- "Create a role?" -> POST /tenants/{tenant_id}/roles
- "Delete a role?" -> DELETE /tenants/{tenant_id}/roles/{role_id}
- "Get role details?" -> GET /tenants/{tenant_id}/roles/{role_id}
- "Partially update a role?" -> PATCH /tenants/{tenant_id}/roles/{role_id}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object
- Error responses use types: Conflict, Forbidden, Unauthorized

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
