---
name: gitlab-api
description: "GitLab API skill. Use when working with GitLab for groups, projects, admin. Covers 73 endpoints."
version: 1.0.0
generator: lapsh
---

# GitLab API
API version: v4

## Auth
ApiKey Private-Token in header

## Base URL
https://www.gitlab.com/api/v4

## Setup
1. Set your API key in the appropriate header
2. GET /admin/batched_background_migrations -- verify access
3. POST /groups/{id}/badges -- create first badges

## Endpoints

73 endpoints across 10 groups. See references/api-spec.lap for full details.

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups/{id}/badges/{badge_id} | Gets a badge of a group. |
| PUT | /groups/{id}/badges/{badge_id} | Updates a badge of a group. |
| DELETE | /groups/{id}/badges/{badge_id} | Removes a badge from the group. |
| GET | /groups/{id}/badges | Gets a list of group badges viewable by the authenticated user. |
| POST | /groups/{id}/badges | Adds a badge to a group. |
| GET | /groups/{id}/badges/render | Preview a badge from a group. |
| DELETE | /groups/{id}/access_requests/{user_id} | Denies an access request for the given user. |
| PUT | /groups/{id}/access_requests/{user_id}/approve | Approves an access request for the given user. |
| GET | /groups/{id}/access_requests | Gets a list of access requests for a group. |
| POST | /groups/{id}/access_requests | Requests access for the authenticated user to a group. |

### projects
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /projects/{id}/repository/merged_branches | Delete all merged branches |
| GET | /projects/{id}/repository/branches/{branch} | Get a single repository branch |
| DELETE | /projects/{id}/repository/branches/{branch} | Delete a branch |
| HEAD | /projects/{id}/repository/branches/{branch} | Check if a branch exists |
| GET | /projects/{id}/repository/branches | Get a project repository branches |
| POST | /projects/{id}/repository/branches | Create branch |
| PUT | /projects/{id}/repository/branches/{branch}/unprotect | Unprotect a single branch |
| PUT | /projects/{id}/repository/branches/{branch}/protect | Protect a single branch |
| GET | /projects/{id}/badges/{badge_id} | Gets a badge of a project. |
| PUT | /projects/{id}/badges/{badge_id} | Updates a badge of a project. |
| DELETE | /projects/{id}/badges/{badge_id} | Removes a badge from the project. |
| GET | /projects/{id}/badges | Gets a list of project badges viewable by the authenticated user. |
| POST | /projects/{id}/badges | Adds a badge to a project. |
| GET | /projects/{id}/badges/render | Preview a badge from a project. |
| DELETE | /projects/{id}/access_requests/{user_id} | Denies an access request for the given user. |
| PUT | /projects/{id}/access_requests/{user_id}/approve | Approves an access request for the given user. |
| GET | /projects/{id}/access_requests | Gets a list of access requests for a project. |
| POST | /projects/{id}/access_requests | Requests access for the authenticated user to a project. |
| PUT | /projects/{id}/alert_management_alerts/{alert_iid}/metric_images/{metric_image_id} | Update a metric image for an alert |
| DELETE | /projects/{id}/alert_management_alerts/{alert_iid}/metric_images/{metric_image_id} | Remove a metric image for an alert |
| GET | /projects/{id}/alert_management_alerts/{alert_iid}/metric_images | Metric Images for alert |
| POST | /projects/{id}/alert_management_alerts/{alert_iid}/metric_images | Upload a metric image for an alert |
| POST | /projects/{id}/alert_management_alerts/{alert_iid}/metric_images/authorize | Workhorse authorize metric image file upload |
| GET | /projects/{id}/jobs | List jobs for a project |
| GET | /projects/{id}/jobs/{job_id} | Get a single job by ID |
| POST | /projects/{id}/jobs/{job_id}/play | Run a manual job |

### admin
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin/batched_background_migrations/{id} | Retrieve a batched background migration |
| GET | /admin/batched_background_migrations | Get the list of batched background migrations |
| PUT | /admin/batched_background_migrations/{id}/resume | Resume a batched background migration |
| PUT | /admin/batched_background_migrations/{id}/pause | Pause a batched background migration |
| GET | /admin/ci/variables/{key} | Get the details of a specific instance-level variable |
| PUT | /admin/ci/variables/{key} | Update an instance-level variable |
| DELETE | /admin/ci/variables/{key} | Delete an existing instance-level variable |
| GET | /admin/ci/variables | List all instance-level variables |
| POST | /admin/ci/variables | Create a new instance-level variable |
| GET | /admin/databases/{database_name}/dictionary/tables/{table_name} | Retrieve dictionary details |
| GET | /admin/clusters/{cluster_id} | Get a single instance cluster |
| PUT | /admin/clusters/{cluster_id} | Edit instance cluster |
| DELETE | /admin/clusters/{cluster_id} | Delete instance cluster |
| POST | /admin/clusters/add | Add existing instance cluster |
| GET | /admin/clusters | List instance clusters |
| POST | /admin/migrations/{timestamp}/mark | Mark the migration as successfully executed |

### applications
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /applications/{id} | Delete an application |
| GET | /applications | Get applications |
| POST | /applications | Create a new application |

### avatar
| Method | Path | Description |
|--------|------|-------------|
| GET | /avatar | Return avatar url for a user |

### broadcast_messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /broadcast_messages/{id} | Get a specific broadcast message |
| PUT | /broadcast_messages/{id} | Update a broadcast message |
| DELETE | /broadcast_messages/{id} | Delete a broadcast message |
| GET | /broadcast_messages | Get all broadcast messages |
| POST | /broadcast_messages | Create a broadcast message |

### bulk_imports
| Method | Path | Description |
|--------|------|-------------|
| GET | /bulk_imports/{import_id}/entities/{entity_id} | Get GitLab Migration entity details |
| GET | /bulk_imports/{import_id}/entities | List GitLab Migration entities |
| GET | /bulk_imports/{import_id} | Get GitLab Migration details |
| GET | /bulk_imports/entities | List all GitLab Migrations' entities |
| GET | /bulk_imports | List all GitLab Migrations |
| POST | /bulk_imports | Start a new GitLab Migration |

### application
| Method | Path | Description |
|--------|------|-------------|
| GET | /application/appearance | Get the current appearance |
| PUT | /application/appearance | Modify appearance |
| GET | /application/plan_limits | Get current plan limits |
| PUT | /application/plan_limits | Change plan limits |

### metadata
| Method | Path | Description |
|--------|------|-------------|
| GET | /metadata | Retrieve metadata information for this GitLab instance |

### version
| Method | Path | Description |
|--------|------|-------------|
| GET | /version | Retrieves version information for the GitLab instance |

## Enhanced Skill Content
## Question Mapping

- "What badges does this group have?" -> GET /groups/{id}/badges
- "How do I add a badge to my project?" -> POST /projects/{id}/badges
- "Who has requested access to my group?" -> GET /groups/{id}/access_requests
- "How do I approve someone's access request for a project?" -> PUT /projects/{id}/access_requests/{user_id}/approve
- "What branches exist in my project?" -> GET /projects/{id}/repository/branches
- "How do I create a new branch from main?" -> POST /projects/{id}/repository/branches
- "How do I protect a branch?" -> PUT /projects/{id}/repository/branches/{branch}/protect
- "Delete all merged branches from a project" -> DELETE /projects/{id}/repository/merged_branches
- "What version of GitLab is running?" -> GET /version
- "Show me all CI/CD variables set at the admin level" -> GET /admin/ci/variables
- "What are the plan limits for the free tier?" -> GET /application/plan_limits
- "How do I create a new OAuth application?" -> POST /applications
- "What's the status of a bulk import?" -> GET /bulk_imports/{import_id}
- "Get the avatar URL for a user's email" -> GET /avatar
- "List all active broadcast messages" -> GET /broadcast_messages

## Response Tips

- **Paginated lists** (badges, branches, access requests, bulk imports, variables, broadcast messages): Check `page` and `per_page` params; defaults are page=1, per_page=20. Iterate by incrementing `page` until response array is shorter than `per_page`.
- **Branch operations**: Responses include a nested `commit` map with full commit metadata (author, committer, dates, trailers); the branch-level `protected`, `merged`, and `default` booleans indicate state.
- **Access requests**: The `access_level` field on approve defaults to 30 (Developer); valid GitLab levels are 10=Guest, 20=Reporter, 30=Developer, 40=Maintainer, 50=Owner.
- **Admin endpoints**: Expect 401/403 errors if the token lacks admin scope; batched migration responses include `progress` as a float (0.0 to 1.0).
- **Badges**: Distinguish `rendered_link_url` / `rendered_image_url` (with variable substitution applied) from the raw `link_url` / `image_url` templates.
- **Bulk imports**: Entity `status` is one of created/started/finished/timeout/failed; the `failures` array inside entities contains error details.
- **204 responses**: DELETE and HEAD calls return no body; treat any 2xx as success.
- **Jobs**: The `scope` filter on GET /projects/{id}/jobs accepts an array of statuses (created, pending, running, failed, success, canceled, skipped, manual).

## Anomaly Flags

- **202 on merged branch cleanup**: `DELETE /projects/{id}/repository/merged_branches` returns 202 (accepted, not completed) -- the operation runs asynchronously. Surface this to avoid premature follow-up calls.
- **503 on bulk imports**: All bulk import endpoints can return 503 (service unavailable), indicating the feature is disabled or the instance is under load. Retry with backoff.
- **422 on migration mark/pause/resume**: Indicates the migration is in a state that cannot be transitioned (e.g., pausing an already-paused migration). Surface the current `status` field.
- **Masked CI variables**: When `masked: true`, the `value` field is redacted in GET responses. Flag when a user tries to read a masked variable and gets a placeholder.
- **Branch protection conflicts**: If `developers_can_push` and `developers_can_merge` are both false after a protect call, flag that the branch may be inaccessible to non-maintainers.
- **Stale access requests**: If `requested_at` on an access request is older than 30 days, surface it as potentially forgotten.
- **Bulk import timeout status**: If an entity shows `status: timeout`, flag it -- the import stalled and may need manual intervention.
- **Admin cluster with no management project**: If `management_project` is null in a cluster response, flag that GitOps features will not work for that cluster.

## Playbook

### 1. Create and Protect a New Branch

1. Create the branch: `POST /projects/{id}/repository/branches` with `branch` (name) and `ref` (source branch or commit SHA)
2. Verify creation succeeded (201 response, check `name` and `default` fields)
3. Protect the branch: `PUT /projects/{id}/repository/branches/{branch}/protect` with optional `developers_can_push` and `developers_can_merge`
4. Confirm protection: check that `protected: true` in the response

### 2. Manage Group Access Requests

1. List pending requests: `GET /groups/{id}/access_requests` (paginate if needed)
2. Review each request's `username`, `state`, and `requested_at`
3. Approve: `PUT /groups/{id}/access_requests/{user_id}/approve` with desired `access_level` (default 30 = Developer)
4. Or deny: `DELETE /groups/{id}/access_requests/{user_id}`
5. Verify the user no longer appears in the pending list

### 3. Set Up Admin-Level CI/CD Variables

1. Check existing variables: `GET /admin/ci/variables` (paginate with `page`/`per_page`)
2. Create a new variable: `POST /admin/ci/variables` with `key`, `value`, and optionally `protected`, `masked`, `variable_type`
3. Verify creation (201 response, check `masked` and `protected` flags)
4. To update later: `PUT /admin/ci/variables/{key}` with new values
5. To remove: `DELETE /admin/ci/variables/{key}` (returns 204)

### 4. Monitor a Bulk Import

1. Start the import: `POST /bulk_imports` (returns import ID and initial status)
2. Poll status: `GET /bulk_imports/{import_id}` -- watch the `status` field transition from `created` to `started` to `finished`
3. List entities: `GET /bulk_imports/{import_id}/entities` to see per-project/group progress
4. For failed entities: inspect the `failures` array in `GET /bulk_imports/{import_id}/entities/{entity_id}`
5. If status is `timeout`, consider re-triggering or investigating server load (check for 503s)

### 5. Add Badges to a Project with Preview

1. Preview the badge rendering: `GET /projects/{id}/badges/render` with `link_url` and `image_url` templates
2. Inspect `rendered_link_url` and `rendered_image_url` to confirm variable substitution looks correct
3. Create the badge: `POST /projects/{id}/badges` with `link_url`, `image_url`, and optional `name`
4. List all badges: `GET /projects/{id}/badges` to verify it appears
5. Update if needed: `PUT /projects/{id}/badges/{badge_id}` to change URL or name


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
