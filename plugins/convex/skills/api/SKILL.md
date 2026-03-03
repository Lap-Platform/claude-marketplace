---
name: convex-management-api
description: "Convex Management API skill. Use when working with Convex Management for teams, projects, deployments. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# Convex Management API
API version: 1.0.0

## Auth
Bearer bearer | Bearer bearer | Bearer bearer

## Base URL
https://api.convex.dev/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /token_details -- verify access
3. POST /teams/{team_id}/create_project -- create first create_project

## Endpoints

20 endpoints across 4 groups. See references/api-spec.lap for full details.

### teams
| Method | Path | Description |
|--------|------|-------------|
| POST | /teams/{team_id}/create_project | Create project |
| GET | /teams/{team_id}/list_projects | List projects |
| GET | /teams/{team_id_or_slug}/projects/{project_slug} | Get project by slug |
| GET | /teams/{team_id}/list_deployment_classes | List deployment classes |
| GET | /teams/{team_id}/list_deployment_regions | List deployment regions |
| GET | /teams/{team_id}/list_members | List team members |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{project_id}/list_deployments | List deployments |
| POST | /projects/{project_id}/delete | Delete project |
| GET | /projects/{project_id} | Get project by ID |
| POST | /projects/{project_id}/create_deployment | Create deployment |

### deployments
| Method | Path | Description |
|--------|------|-------------|
| POST | /deployments/{deployment_name}/delete | Delete deployment |
| GET | /deployments/{deployment_name} | Get deployment |
| PATCH | /deployments/{deployment_name} | Update deployment |
| POST | /deployments/{deployment_name}/create_deploy_key | Create deploy key |
| GET | /deployments/{deployment_name}/list_deploy_keys | List deploy keys |
| POST | /deployments/{deployment_name}/delete_deploy_key | Delete deploy key |
| POST | /deployments/{deployment_name}/create_custom_domain | Create custom domain |
| POST | /deployments/{deployment_name}/delete_custom_domain | Delete custom domain |
| GET | /deployments/{deployment_name}/custom_domains | List custom domains |

### token_details
| Method | Path | Description |
|--------|------|-------------|
| GET | /token_details | Get token details |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new project in my team?" -> POST /teams/{team_id}/create_project
- "What projects does my team have?" -> GET /teams/{team_id}/list_projects
- "Show me all deployments for a project" -> GET /projects/{project_id}/list_deployments
- "How do I delete a project?" -> POST /projects/{project_id}/delete
- "Get details about a specific project" -> GET /projects/{project_id}
- "Look up a project by its slug" -> GET /teams/{team_id_or_slug}/projects/{project_slug}
- "Create a new deployment for my project" -> POST /projects/{project_id}/create_deployment
- "Delete a deployment" -> POST /deployments/{deployment_name}/delete
- "Get info about a specific deployment" -> GET /deployments/{deployment_name}
- "Update a deployment's settings" -> PATCH /deployments/{deployment_name}
- "What deployment classes are available for my team?" -> GET /teams/{team_id}/list_deployment_classes
- "What regions can I deploy to?" -> GET /teams/{team_id}/list_deployment_regions
- "Generate a deploy key for CI/CD" -> POST /deployments/{deployment_name}/create_deploy_key
- "List all deploy keys for a deployment" -> GET /deployments/{deployment_name}/list_deploy_keys
- "Revoke a deploy key" -> POST /deployments/{deployment_name}/delete_deploy_key
- "Who am I authenticated as?" -> GET /token_details
- "Set up a custom domain for my deployment" -> POST /deployments/{deployment_name}/create_custom_domain
- "Remove a custom domain" -> POST /deployments/{deployment_name}/delete_custom_domain
- "What custom domains are configured?" -> GET /deployments/{deployment_name}/custom_domains
- "Who are the members of my team?" -> GET /teams/{team_id}/list_members

## Response Tips

- **Teams/Projects listings**: Results come back as arrays or objects with `items: [map]`; iterate directly -- no pagination cursor is documented, so expect full lists.
- **Project details**: Returns flat objects with `id`, `name`, `slug`, `teamId`, `teamSlug`, and `createTime` (epoch int64 in milliseconds); convert timestamps client-side.
- **Create operations**: `create_project` returns `projectId`, `deploymentName`, and `deploymentUrl` (nullable) -- check for null deployment fields when `deploymentType` is omitted.
- **Deploy keys**: `create_deploy_key` returns a `deployKey` string shown only once; store it immediately as it cannot be retrieved again.
- **Custom domains**: `custom_domains` returns `domains: [map]` where each map contains domain config and verification status; check DNS propagation state within each entry.
- **Deletions**: All delete endpoints (project, deployment, deploy key, custom domain) use POST (not DELETE); 200 with empty body signals success.
- **Errors**: Expect 401 for invalid/expired bearer tokens, 404 for nonexistent resources, and 400 for malformed parameters; error bodies typically include a message field.

## Anomaly Flags

- **Token identity unknown**: If `GET /token_details` returns unexpected or empty data, surface immediately -- the bearer token may be scoped incorrectly or near expiration.
- **Nullable deployment on project create**: When `POST /teams/{team_id}/create_project` returns `deploymentName: null` or `deploymentUrl: null`, warn that no default deployment was provisioned and the user should create one explicitly.
- **Delete operations are POST, not DELETE**: Flag if a caller mistakenly sends HTTP DELETE -- the API uses POST for all destructive actions and will return 404/405.
- **Deploy key single-reveal**: After `create_deploy_key`, proactively remind the user to save the `deployKey` value -- it will not be retrievable from `list_deploy_keys`.
- **Unknown deployment classes/regions**: If `list_deployment_classes` or `list_deployment_regions` returns empty `items`, surface this as a possible permissions or plan limitation.
- **Custom domain DNS verification**: After adding a custom domain, proactively suggest checking domain verification status via `GET .../custom_domains` since DNS propagation can take time.
- **`dashboardEditConfirmation` on PATCH**: If the user patches a deployment without setting `dashboardEditConfirmation: true`, warn that UI-initiated edits may be blocked or require confirmation.

## Playbook

### 1. Set Up a New Project with a Production Deployment

1. Call `GET /token_details` to confirm your identity and team access.
2. Call `GET /teams/{team_id}/list_deployment_classes` to see available compute tiers.
3. Call `GET /teams/{team_id}/list_deployment_regions` to pick a target region.
4. Call `POST /teams/{team_id}/create_project` with `projectName`, `deploymentClass`, and `deploymentRegion`.
5. Note the returned `projectId` and `deploymentName`.
6. If no default deployment was created (null fields), call `POST /projects/{project_id}/create_deployment` with `type: "prod"`.

### 2. Configure CI/CD with Deploy Keys

1. Call `GET /projects/{project_id}/list_deployments` to find the target `deployment_name`.
2. Call `POST /deployments/{deployment_name}/create_deploy_key` with a descriptive `name` (e.g., "github-actions-prod").
3. Store the returned `deployKey` in your CI secrets -- it is shown only once.
4. To audit existing keys, call `GET /deployments/{deployment_name}/list_deploy_keys`.
5. To rotate, call `POST /deployments/{deployment_name}/delete_deploy_key` with the old key's `id`, then create a new one.

### 3. Add a Custom Domain to a Deployment

1. Call `GET /deployments/{deployment_name}` to confirm the deployment exists and note its current config.
2. Call `POST /deployments/{deployment_name}/create_custom_domain` with `domain` and `requestDestination` set to `"convexCloud"` (for API) or `"convexSite"` (for hosted site).
3. Configure DNS records as indicated in the response.
4. Poll `GET /deployments/{deployment_name}/custom_domains` to verify DNS propagation and domain activation.
5. To remove later, call `POST /deployments/{deployment_name}/delete_custom_domain` with the same `domain` and `requestDestination`.

### 4. Audit Team Resources

1. Call `GET /teams/{team_id}/list_members` to review who has access.
2. Call `GET /teams/{team_id}/list_projects` to enumerate all projects.
3. For each project, call `GET /projects/{project_id}/list_deployments` to see all deployments.
4. For each deployment, call `GET /deployments/{deployment_name}/list_deploy_keys` to audit active keys.
5. Call `GET /deployments/{deployment_name}/custom_domains` to check domain configurations.

### 5. Tear Down a Project and Its Deployments

1. Call `GET /projects/{project_id}/list_deployments` to list all deployments under the project.
2. For each deployment, call `GET /deployments/{deployment_name}/custom_domains` and remove any custom domains via `POST .../delete_custom_domain`.
3. For each deployment, call `GET /deployments/{deployment_name}/list_deploy_keys` and revoke all keys via `POST .../delete_deploy_key`.
4. Delete each deployment with `POST /deployments/{deployment_name}/delete`.
5. Finally, delete the project with `POST /projects/{project_id}/delete`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
