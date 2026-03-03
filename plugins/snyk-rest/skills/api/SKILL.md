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

## Enhanced Skill Content
## Question Mapping

- "Who am I authenticated as?" -> GET /self
- "List all my organizations" -> GET /orgs
- "What issues does this org have?" -> GET /orgs/{org_id}/issues
- "Show me the audit log for my group" -> GET /groups/{group_id}/audit_logs/search
- "What projects are in this organization?" -> GET /orgs/{org_id}/projects
- "Get the SBOM for a project" -> GET /orgs/{org_id}/projects/{project_id}/sbom
- "What custom base images are configured?" -> GET /custom_base_images
- "List members of a group" -> GET /groups/{group_id}/memberships
- "Search inventory assets at the tenant level" -> POST /tenants/{tenant_id}/inventory/assets/searches
- "Create a service account for an org" -> POST /orgs/{org_id}/service_accounts
- "Export all org data for compliance" -> POST /orgs/{org_id}/export
- "Check the status of an export job" -> GET /orgs/{org_id}/export/{export_id}
- "What cloud environments are configured?" -> GET /orgs/{org_id}/cloud/environments
- "Look up a specific package's vulnerabilities" -> GET /orgs/{org_id}/packages/{purl}/issues
- "Run a test against an SBOM" -> POST /orgs/{org_id}/sbom_tests

## Response Tips

- **Paginated lists** (orgs, projects, issues, memberships, assets): Use cursor-based pagination via `starting_after` and `ending_before` fields; default `limit` is 10 (audit logs default to 100). Follow the next cursor until no more results.
- **Issues endpoints**: Filter by `effective_severity_level`, `status`, `ignored`, and date ranges (`created_before/after`, `updated_before/after`); note the 403 error message says "Unauthorized" not "Forbidden" -- handle both.
- **Export endpoints**: POST returns 202 (accepted); poll GET `/export/{export_id}` until the job completes. Watch for 429 rate limiting on export creation.
- **Inventory assets**: Support advanced filtering via `filter` query string, field selection via `fields` map, and `meta_count` for totals without full results (`with` or `only`).
- **SBOM responses**: Specify `format` explicitly (CycloneDX 1.4-1.6 JSON/XML, or SPDX 2.3 JSON); defaults may vary.
- **Broker endpoints** (tenants): Deeply nested paths with 4-5 UUID path params -- validate all IDs before calling to avoid ambiguous 404s.
- **Cloud scans/environments**: `status` field uses `queued|in_progress|success|error|null` -- null means not yet started.

## Anomaly Flags

- **429 on export endpoints**: Rate limit hit on `/export` -- surface immediately and suggest waiting before retry. This is the only endpoint that explicitly declares 429.
- **409 Conflict**: Returned on creates/updates across groups, orgs, tenants, and apps -- indicates duplicate or stale state. Surface the conflict details to the user.
- **Mixed 403 messages**: Some issue endpoints return `403: Unauthorized` instead of `403: Forbidden` -- flag if access-denied errors appear with inconsistent messaging.
- **202 Accepted on tests/exports/AI BOMs**: These are async jobs. Proactively remind the user to poll the corresponding GET endpoint for completion status.
- **303 See Other on test jobs and asset searches**: Redirects indicate the result is ready at another URL -- follow the redirect automatically or surface the location.
- **503 on AI BOM endpoints**: Service may be temporarily unavailable -- flag and suggest retry with backoff.
- **Deeply nested broker paths**: 5+ path parameters required -- proactively validate UUID format on all IDs before making the call to avoid opaque errors.
- **Inventory search two-step pattern**: POST to `/searches` returns 302 with a `search_id`, then GET `/searches/{search_id}/results` for actual data -- surface this flow to avoid confusion.

## Playbook

### 1. Audit an Organization's Security Posture

1. GET /self to confirm authentication and retrieve your user context
2. GET /orgs to list accessible organizations, note the target `org_id`
3. GET /orgs/{org_id}/projects to enumerate all monitored projects
4. GET /orgs/{org_id}/issues with `effective_severity_level=["critical","high"]` to find high-priority vulnerabilities
5. GET /orgs/{org_id}/issues/{issue_id} for detailed remediation guidance on each critical issue
6. GET /orgs/{org_id}/projects/{project_id}/sbom with `format=cyclonedx1.6+json` to export the dependency tree for further analysis

### 2. Export Organization Data for Compliance

1. GET /orgs/{org_id} to confirm the organization exists and you have access
2. POST /orgs/{org_id}/export to initiate the export job (returns 202 with `export_id`)
3. Poll GET /orgs/{org_id}/export/{export_id} until the job status indicates completion
4. If 429 is returned on the POST, wait and retry -- only one export can run at a time
5. Download the completed export payload from the final GET response

### 3. Manage Group Memberships and Access

1. GET /groups to list all groups you can access
2. GET /groups/{group_id}/memberships with `sort_by=role_name` to review current members and roles
3. POST /groups/{group_id}/memberships to invite a new user (provide role in request body)
4. PATCH /groups/{group_id}/memberships/{membership_id} to change a member's role
5. DELETE /groups/{group_id}/memberships/{membership_id} with `cascade=true` to remove a member and their downstream org memberships

### 4. Set Up Broker Connections for a Tenant

1. GET /tenants/{tenant_id} to verify the tenant and retrieve current config
2. GET /tenants/{tenant_id}/brokers/deployments to list existing broker deployments
3. POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments to create a new deployment
4. POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/connections to add a connection to the deployment
5. POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/credentials to configure credentials
6. POST /tenants/{tenant_id}/brokers/installs/{install_id}/deployments/{deployment_id}/contexts to set up the routing context

### 5. Investigate Inventory Assets Across Scopes

1. Decide scope: use `/orgs/{org_id}/inventory/assets`, `/groups/{group_id}/inventory/assets`, or `/tenants/{tenant_id}/inventory/assets`
2. GET `.../inventory/assets/filters` to discover available filter dimensions
3. GET `.../inventory/assets/filters/{filter_id}/values` with `q=search_term` to find specific filter values
4. POST `.../inventory/assets/searches` with your filter criteria (returns 302 with `search_id`)
5. GET `.../inventory/assets/searches/{search_id}/results` to retrieve matching assets, paginating with `starting_after`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object
- Error responses use types: Conflict, Forbidden, Unauthorized

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
