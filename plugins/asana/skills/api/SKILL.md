---
name: asana
description: "Asana API skill. Use when working with Asana for access_requests, allocations, attachments. Covers 222 endpoints."
version: 1.0.0
generator: lapsh
---

# Asana
API version: 1.0

## Auth
Bearer bearer | OAuth2

## Base URL
https://app.asana.com/api/1.0

## Setup
1. Set Authorization header with your Bearer token
2. GET /access_requests -- verify access
3. POST /access_requests -- create first access_requests

## Endpoints

222 endpoints across 41 groups. See references/api-spec.lap for full details.

### access_requests
| Method | Path | Description |
|--------|------|-------------|
| GET | /access_requests | Get access requests |
| POST | /access_requests | Create an access request |
| POST | /access_requests/{access_request_gid}/approve | Approve an access request |
| POST | /access_requests/{access_request_gid}/reject | Reject an access request |

### allocations
| Method | Path | Description |
|--------|------|-------------|
| GET | /allocations/{allocation_gid} | Get an allocation |
| PUT | /allocations/{allocation_gid} | Update an allocation |
| DELETE | /allocations/{allocation_gid} | Delete an allocation |
| GET | /allocations | Get multiple allocations |
| POST | /allocations | Create an allocation |

### attachments
| Method | Path | Description |
|--------|------|-------------|
| GET | /attachments/{attachment_gid} | Get an attachment |
| DELETE | /attachments/{attachment_gid} | Delete an attachment |
| GET | /attachments | Get attachments from an object |
| POST | /attachments | Upload an attachment |

### workspaces
| Method | Path | Description |
|--------|------|-------------|
| GET | /workspaces/{workspace_gid}/audit_log_events | Get audit log events |
| GET | /workspaces/{workspace_gid}/custom_fields | Get a workspace's custom fields |
| GET | /workspaces/{workspace_gid}/projects | Get all projects in a workspace |
| POST | /workspaces/{workspace_gid}/projects | Create a project in a workspace |
| GET | /workspaces/{workspace_gid}/tags | Get tags in a workspace |
| POST | /workspaces/{workspace_gid}/tags | Create a tag in a workspace |
| GET | /workspaces/{workspace_gid}/tasks/custom_id/{custom_id} | Get a task for a given custom ID |
| GET | /workspaces/{workspace_gid}/tasks/search | Search tasks in a workspace |
| GET | /workspaces/{workspace_gid}/teams | Get teams in a workspace |
| GET | /workspaces/{workspace_gid}/typeahead | Get objects via typeahead |
| GET | /workspaces/{workspace_gid}/users | Get users in a workspace or organization |
| GET | /workspaces/{workspace_gid}/users/{user_gid} | Get a user in a workspace or organization |
| PUT | /workspaces/{workspace_gid}/users/{user_gid} | Update a user in a workspace or organization |
| GET | /workspaces/{workspace_gid}/workspace_memberships | Get the workspace memberships for a workspace |
| GET | /workspaces | Get multiple workspaces |
| GET | /workspaces/{workspace_gid} | Get a workspace |
| PUT | /workspaces/{workspace_gid} | Update a workspace |
| POST | /workspaces/{workspace_gid}/addUser | Add a user to a workspace or organization |
| POST | /workspaces/{workspace_gid}/removeUser | Remove a user from a workspace or organization |
| GET | /workspaces/{workspace_gid}/events | Get workspace events |

### batch
| Method | Path | Description |
|--------|------|-------------|
| POST | /batch | Submit parallel requests |

### budgets
| Method | Path | Description |
|--------|------|-------------|
| GET | /budgets | Get all budgets |
| POST | /budgets | Create a budget |
| GET | /budgets/{budget_gid} | Get a budget |
| PUT | /budgets/{budget_gid} | Update a budget |
| DELETE | /budgets/{budget_gid} | Delete a budget |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{project_gid}/custom_field_settings | Get a project's custom fields |
| POST | /projects/{project_gid}/project_briefs | Create a project brief |
| GET | /projects/{project_gid}/project_memberships | Get memberships from a project |
| GET | /projects/{project_gid}/project_statuses | Get statuses from a project |
| POST | /projects/{project_gid}/project_statuses | Create a project status |
| GET | /projects | Get multiple projects |
| POST | /projects | Create a project |
| GET | /projects/{project_gid} | Get a project |
| PUT | /projects/{project_gid} | Update a project |
| DELETE | /projects/{project_gid} | Delete a project |
| POST | /projects/{project_gid}/duplicate | Duplicate a project |
| POST | /projects/{project_gid}/addCustomFieldSetting | Add a custom field to a project |
| POST | /projects/{project_gid}/removeCustomFieldSetting | Remove a custom field from a project |
| GET | /projects/{project_gid}/task_counts | Get task count of a project |
| POST | /projects/{project_gid}/addMembers | Add users to a project |
| POST | /projects/{project_gid}/removeMembers | Remove users from a project |
| POST | /projects/{project_gid}/addFollowers | Add followers to a project |
| POST | /projects/{project_gid}/removeFollowers | Remove followers from a project |
| POST | /projects/{project_gid}/saveAsTemplate | Create a project template from a project |
| GET | /projects/{project_gid}/sections | Get sections in a project |
| POST | /projects/{project_gid}/sections | Create a section in a project |
| POST | /projects/{project_gid}/sections/insert | Move or Insert sections |
| GET | /projects/{project_gid}/tasks | Get tasks from a project |

### portfolios
| Method | Path | Description |
|--------|------|-------------|
| GET | /portfolios/{portfolio_gid}/custom_field_settings | Get a portfolio's custom fields |
| GET | /portfolios/{portfolio_gid}/portfolio_memberships | Get memberships from a portfolio |
| GET | /portfolios | Get multiple portfolios |
| POST | /portfolios | Create a portfolio |
| GET | /portfolios/{portfolio_gid} | Get a portfolio |
| PUT | /portfolios/{portfolio_gid} | Update a portfolio |
| DELETE | /portfolios/{portfolio_gid} | Delete a portfolio |
| GET | /portfolios/{portfolio_gid}/items | Get portfolio items |
| POST | /portfolios/{portfolio_gid}/addItem | Add a portfolio item |
| POST | /portfolios/{portfolio_gid}/removeItem | Remove a portfolio item |
| POST | /portfolios/{portfolio_gid}/addCustomFieldSetting | Add a custom field to a portfolio |
| POST | /portfolios/{portfolio_gid}/removeCustomFieldSetting | Remove a custom field from a portfolio |
| POST | /portfolios/{portfolio_gid}/addMembers | Add users to a portfolio |
| POST | /portfolios/{portfolio_gid}/removeMembers | Remove users from a portfolio |

### goals
| Method | Path | Description |
|--------|------|-------------|
| GET | /goals/{goal_gid}/custom_field_settings | Get a goal's custom fields |
| POST | /goals/{goal_gid}/addSupportingRelationship | Add a supporting goal relationship |
| POST | /goals/{goal_gid}/removeSupportingRelationship | Removes a supporting goal relationship |
| GET | /goals/{goal_gid} | Get a goal |
| PUT | /goals/{goal_gid} | Update a goal |
| DELETE | /goals/{goal_gid} | Delete a goal |
| GET | /goals | Get goals |
| POST | /goals | Create a goal |
| POST | /goals/{goal_gid}/setMetric | Create a goal metric |
| POST | /goals/{goal_gid}/setMetricCurrentValue | Update a goal metric |
| POST | /goals/{goal_gid}/addFollowers | Add a collaborator to a goal |
| POST | /goals/{goal_gid}/removeFollowers | Remove a collaborator from a goal |
| GET | /goals/{goal_gid}/parentGoals | Get parent goals from a goal |
| POST | /goals/{goal_gid}/addCustomFieldSetting | Add a custom field to a goal |
| POST | /goals/{goal_gid}/removeCustomFieldSetting | Remove a custom field from a goal |

### teams
| Method | Path | Description |
|--------|------|-------------|
| GET | /teams/{team_gid}/custom_field_settings | Get a team's custom fields |
| GET | /teams/{team_gid}/project_templates | Get a team's project templates |
| GET | /teams/{team_gid}/projects | Get a team's projects |
| POST | /teams/{team_gid}/projects | Create a project in a team |
| GET | /teams/{team_gid}/team_memberships | Get memberships from a team |
| POST | /teams | Create a team |
| GET | /teams/{team_gid} | Get a team |
| PUT | /teams/{team_gid} | Update a team |
| POST | /teams/{team_gid}/addUser | Add a user to a team |
| POST | /teams/{team_gid}/removeUser | Remove a user from a team |
| GET | /teams/{team_gid}/users | Get users in a team |

### custom_fields
| Method | Path | Description |
|--------|------|-------------|
| POST | /custom_fields | Create a custom field |
| GET | /custom_fields/{custom_field_gid} | Get a custom field |
| PUT | /custom_fields/{custom_field_gid} | Update a custom field |
| DELETE | /custom_fields/{custom_field_gid} | Delete a custom field |
| POST | /custom_fields/{custom_field_gid}/enum_options | Create an enum option |
| POST | /custom_fields/{custom_field_gid}/enum_options/insert | Reorder a custom field's enum |

### enum_options
| Method | Path | Description |
|--------|------|-------------|
| PUT | /enum_options/{enum_option_gid} | Update an enum option |

### custom_types
| Method | Path | Description |
|--------|------|-------------|
| GET | /custom_types | Get all custom types associated with an object |
| GET | /custom_types/{custom_type_gid} | Get a custom type |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Get events on a resource |

### exports
| Method | Path | Description |
|--------|------|-------------|
| POST | /exports/graph | Initiate a graph export |
| POST | /exports/resource | Initiate a resource export |

### goal_relationships
| Method | Path | Description |
|--------|------|-------------|
| GET | /goal_relationships/{goal_relationship_gid} | Get a goal relationship |
| PUT | /goal_relationships/{goal_relationship_gid} | Update a goal relationship |
| GET | /goal_relationships | Get goal relationships |

### jobs
| Method | Path | Description |
|--------|------|-------------|
| GET | /jobs/{job_gid} | Get a job by id |

### memberships
| Method | Path | Description |
|--------|------|-------------|
| GET | /memberships | Get multiple memberships |
| POST | /memberships | Create a membership |
| GET | /memberships/{membership_gid} | Get a membership |
| PUT | /memberships/{membership_gid} | Update a membership |
| DELETE | /memberships/{membership_gid} | Delete a membership |

### organization_exports
| Method | Path | Description |
|--------|------|-------------|
| POST | /organization_exports | Create an organization export request |
| GET | /organization_exports/{organization_export_gid} | Get details on an org export request |

### portfolio_memberships
| Method | Path | Description |
|--------|------|-------------|
| GET | /portfolio_memberships | Get multiple portfolio memberships |
| GET | /portfolio_memberships/{portfolio_membership_gid} | Get a portfolio membership |

### project_briefs
| Method | Path | Description |
|--------|------|-------------|
| GET | /project_briefs/{project_brief_gid} | Get a project brief |
| PUT | /project_briefs/{project_brief_gid} | Update a project brief |
| DELETE | /project_briefs/{project_brief_gid} | Delete a project brief |

### project_memberships
| Method | Path | Description |
|--------|------|-------------|
| GET | /project_memberships/{project_membership_gid} | Get a project membership |

### project_statuses
| Method | Path | Description |
|--------|------|-------------|
| GET | /project_statuses/{project_status_gid} | Get a project status |
| DELETE | /project_statuses/{project_status_gid} | Delete a project status |

### project_templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /project_templates/{project_template_gid} | Get a project template |
| DELETE | /project_templates/{project_template_gid} | Delete a project template |
| GET | /project_templates | Get multiple project templates |
| POST | /project_templates/{project_template_gid}/instantiateProject | Instantiate a project from a project template |

### tasks
| Method | Path | Description |
|--------|------|-------------|
| GET | /tasks/{task_gid}/projects | Get projects a task is in |
| GET | /tasks/{task_gid}/stories | Get stories from a task |
| POST | /tasks/{task_gid}/stories | Create a story on a task |
| GET | /tasks/{task_gid}/tags | Get a task's tags |
| GET | /tasks | Get multiple tasks |
| POST | /tasks | Create a task |
| GET | /tasks/{task_gid} | Get a task |
| PUT | /tasks/{task_gid} | Update a task |
| DELETE | /tasks/{task_gid} | Delete a task |
| POST | /tasks/{task_gid}/duplicate | Duplicate a task |
| GET | /tasks/{task_gid}/subtasks | Get subtasks from a task |
| POST | /tasks/{task_gid}/subtasks | Create a subtask |
| POST | /tasks/{task_gid}/setParent | Set the parent of a task |
| GET | /tasks/{task_gid}/dependencies | Get dependencies from a task |
| POST | /tasks/{task_gid}/addDependencies | Set dependencies for a task |
| POST | /tasks/{task_gid}/removeDependencies | Unlink dependencies from a task |
| GET | /tasks/{task_gid}/dependents | Get dependents from a task |
| POST | /tasks/{task_gid}/addDependents | Set dependents for a task |
| POST | /tasks/{task_gid}/removeDependents | Unlink dependents from a task |
| POST | /tasks/{task_gid}/addProject | Add a project to a task |
| POST | /tasks/{task_gid}/removeProject | Remove a project from a task |
| POST | /tasks/{task_gid}/addTag | Add a tag to a task |
| POST | /tasks/{task_gid}/removeTag | Remove a tag from a task |
| POST | /tasks/{task_gid}/addFollowers | Add followers to a task |
| POST | /tasks/{task_gid}/removeFollowers | Remove followers from a task |
| GET | /tasks/{task_gid}/time_tracking_entries | Get time tracking entries for a task |
| POST | /tasks/{task_gid}/time_tracking_entries | Create a time tracking entry |

### rates
| Method | Path | Description |
|--------|------|-------------|
| GET | /rates | Get multiple rates |
| POST | /rates | Create a rate |
| GET | /rates/{rate_gid} | Get a rate |
| PUT | /rates/{rate_gid} | Update a rate |
| DELETE | /rates/{rate_gid} | Delete a rate |

### reactions
| Method | Path | Description |
|--------|------|-------------|
| GET | /reactions | Get reactions with an emoji base on an object. |

### roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /roles | Get multiple roles |
| POST | /roles | Create a role |
| GET | /roles/{role_gid} | Get a role |
| PUT | /roles/{role_gid} | Update a role |
| DELETE | /roles/{role_gid} | Delete a role |

### rule_triggers
| Method | Path | Description |
|--------|------|-------------|
| POST | /rule_triggers/{rule_trigger_gid}/run | Trigger a rule |

### sections
| Method | Path | Description |
|--------|------|-------------|
| GET | /sections/{section_gid} | Get a section |
| PUT | /sections/{section_gid} | Update a section |
| DELETE | /sections/{section_gid} | Delete a section |
| POST | /sections/{section_gid}/addTask | Add task to section |
| GET | /sections/{section_gid}/tasks | Get tasks from a section |

### status_updates
| Method | Path | Description |
|--------|------|-------------|
| GET | /status_updates/{status_update_gid} | Get a status update |
| DELETE | /status_updates/{status_update_gid} | Delete a status update |
| GET | /status_updates | Get status updates from an object |
| POST | /status_updates | Create a status update |

### stories
| Method | Path | Description |
|--------|------|-------------|
| GET | /stories/{story_gid} | Get a story |
| PUT | /stories/{story_gid} | Update a story |
| DELETE | /stories/{story_gid} | Delete a story |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags | Get multiple tags |
| POST | /tags | Create a tag |
| GET | /tags/{tag_gid} | Get a tag |
| PUT | /tags/{tag_gid} | Update a tag |
| DELETE | /tags/{tag_gid} | Delete a tag |
| GET | /tags/{tag_gid}/tasks | Get tasks from a tag |

### task_templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /task_templates | Get multiple task templates |
| GET | /task_templates/{task_template_gid} | Get a task template |
| DELETE | /task_templates/{task_template_gid} | Delete a task template |
| POST | /task_templates/{task_template_gid}/instantiateTask | Instantiate a task from a task template |

### user_task_lists
| Method | Path | Description |
|--------|------|-------------|
| GET | /user_task_lists/{user_task_list_gid}/tasks | Get tasks from a user task list |
| GET | /user_task_lists/{user_task_list_gid} | Get a user task list |

### team_memberships
| Method | Path | Description |
|--------|------|-------------|
| GET | /team_memberships/{team_membership_gid} | Get a team membership |
| GET | /team_memberships | Get team memberships |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/{user_gid}/team_memberships | Get memberships from a user |
| GET | /users/{user_gid}/teams | Get teams for a user |
| GET | /users/{user_gid}/user_task_list | Get a user's task list |
| GET | /users | Get multiple users |
| GET | /users/{user_gid} | Get a user |
| PUT | /users/{user_gid} | Update a user |
| GET | /users/{user_gid}/favorites | Get a user's favorites |
| GET | /users/{user_gid}/workspace_memberships | Get workspace memberships for a user |

### time_periods
| Method | Path | Description |
|--------|------|-------------|
| GET | /time_periods/{time_period_gid} | Get a time period |
| GET | /time_periods | Get time periods |

### time_tracking_entries
| Method | Path | Description |
|--------|------|-------------|
| GET | /time_tracking_entries/{time_tracking_entry_gid} | Get a time tracking entry |
| PUT | /time_tracking_entries/{time_tracking_entry_gid} | Update a time tracking entry |
| DELETE | /time_tracking_entries/{time_tracking_entry_gid} | Delete a time tracking entry |
| GET | /time_tracking_entries | Get multiple time tracking entries |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks | Get multiple webhooks |
| POST | /webhooks | Establish a webhook |
| GET | /webhooks/{webhook_gid} | Get a webhook |
| PUT | /webhooks/{webhook_gid} | Update a webhook |
| DELETE | /webhooks/{webhook_gid} | Delete a webhook |

### workspace_memberships
| Method | Path | Description |
|--------|------|-------------|
| GET | /workspace_memberships/{workspace_membership_gid} | Get a workspace membership |

## Enhanced Skill Content
## Question Mapping

- "What tasks are assigned to me?" -> GET /tasks (with `assignee=me`)
- "Show me all projects in my workspace" -> GET /projects (with `workspace` param)
- "Create a new task in a project" -> POST /tasks (with `data.projects` or follow up with POST /tasks/{task_gid}/addProject)
- "What are the subtasks of this task?" -> GET /tasks/{task_gid}/subtasks
- "Who are the members of a team?" -> GET /teams/{team_gid}/users
- "How much time has been logged on this task?" -> GET /tasks/{task_gid}/time_tracking_entries
- "What sections does this project have?" -> GET /projects/{project_gid}/sections
- "Search for tasks matching a keyword in a workspace" -> GET /workspaces/{workspace_gid}/tasks/search
- "What goals are set for my team?" -> GET /goals (with `team` or `workspace` param)
- "Add a comment or story to a task" -> POST /tasks/{task_gid}/stories
- "What webhooks are active in my workspace?" -> GET /webhooks (with `workspace` param)
- "Move a task to a different section" -> POST /sections/{section_gid}/addTask
- "What are the dependencies blocking this task?" -> GET /tasks/{task_gid}/dependencies
- "List all portfolios I own" -> GET /portfolios (with `workspace` and `owner` params)
- "What custom fields are available in my workspace?" -> GET /workspaces/{workspace_gid}/custom_fields

## Response Tips

- **Lists (tasks, projects, goals, tags, sections):** All wrapped in `{data: [...]}`. Paginated via `next_page.offset` -- keep fetching while `next_page` is non-null. Some endpoints (team users, typeahead, search) omit `next_page` and return all results at once.
- **Single resources (task, project, user):** Wrapped in `{data: {...}}`. Use `opt_fields` to request specific fields; default responses are compact stubs (`gid`, `name`, `resource_type` only).
- **Mutations (create, update, delete):** Create returns 201 with the new object in `data`. Update returns 200 with the updated object. Delete returns `{data: {}}` (empty map) on success.
- **Async operations (duplicate, instantiateProject, exports):** Return a Job object with `status` field. Poll GET /jobs/{job_gid} until `status` changes from `"in_progress"` to `"succeeded"` or `"failed"`. The result appears in `new_project`, `new_task`, etc.
- **Events:** Returns `{data: [...], sync: "token", has_more: bool}`. Persist the `sync` token between polls. A 412 error means the sync token expired -- start fresh.
- **Errors:** All errors return `{errors: [{message, help, phrase}]}`. 402 means a paid feature is required. 424 on attachments signals a dependency failure.

## Anomaly Flags

- **402 Payment Required:** Surface immediately -- the user's Asana plan lacks the requested feature (allocations, budgets, goals, task dependencies). Recommend checking plan tier.
- **412 Precondition Failed on /events:** The sync token has expired. Alert the user that event history was lost and a full re-sync from the resource is needed.
- **424 Failed Dependency on /attachments:** An upstream service (file storage) is unavailable. Retry after a short delay; if persistent, flag as a service degradation.
- **Empty `next_page` with full `limit` count:** If exactly `limit` items return but `next_page` is null, the endpoint may not support pagination (e.g., team users, search). Note this to avoid infinite polling.
- **Job stuck in `in_progress`:** If a duplicate/instantiate job hasn't resolved after 60 seconds of polling, surface it -- Asana async jobs occasionally stall.
- **`opt_fields` silently ignored:** If a requested field is missing from the response without an error, the field name may be misspelled or unavailable for that resource type. Flag the discrepancy.
- **Rate limiting (HTTP 429):** Asana enforces per-minute rate limits. Surface the `Retry-After` header value and recommend using POST /batch to consolidate calls.

## Playbook

### 1. Create a Task with Subtasks and Assign to a Section

1. POST /tasks with `data: {name, assignee, projects: [project_gid], due_on, notes}`
2. Capture the returned `task.gid`
3. POST /tasks/{task_gid}/subtasks with `data: {name, assignee}` for each subtask
4. POST /sections/{section_gid}/addTask with `data: {task: task_gid}` to place it in the right column/section
5. Optionally POST /tasks/{task_gid}/addFollowers to notify stakeholders

### 2. Set Up a Webhook and Process Events

1. GET /workspaces to find your `workspace_gid`
2. POST /webhooks with `data: {resource: project_gid, target: "https://your-server/hook", filters: [{resource_type: "task", action: "changed"}]}`
3. Respond to the handshake: return the `X-Hook-Secret` header value in your endpoint's response header
4. On each webhook delivery, parse the `events` array for `action`, `resource.gid`, and `change.field`
5. GET /tasks/{task_gid} to fetch full details for any task that changed

### 3. Track Time Across a Project

1. GET /projects/{project_gid}/tasks to list all tasks (paginate with `offset`)
2. For each task, GET /tasks/{task_gid}/time_tracking_entries
3. Sum `duration_minutes` across entries, grouping by `entered_on` or `attributable_to` as needed
4. To log new time: POST /tasks/{task_gid}/time_tracking_entries with `data: {duration_minutes, entered_on, description}`
5. Use GET /time_tracking_entries with `portfolio` and date range filters for broader reporting

### 4. Build a Project from a Template

1. GET /project_templates with `workspace` or `team` to find available templates
2. POST /project_templates/{project_template_gid}/instantiateProject with `data: {name, team, requested_dates: [...], requested_roles: [...]}`
3. The response is a Job -- capture `job.gid`
4. Poll GET /jobs/{job_gid} until `status` is `"succeeded"`
5. Read `new_project.gid` from the completed job, then GET /projects/{project_gid} to confirm setup

### 5. Batch Multiple Operations in One Request

1. Identify 1-10 independent API calls to combine (e.g., updating several tasks)
2. POST /batch with `data: {actions: [{relative_path: "/tasks/TASK_GID", method: "PUT", data: {completed: true}}, ...]}`
3. Each action in the response array contains its own `status_code` and `body` -- check each individually
4. Use batch for read-heavy dashboards (fetch multiple tasks/projects in one round trip) to stay within rate limits


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
