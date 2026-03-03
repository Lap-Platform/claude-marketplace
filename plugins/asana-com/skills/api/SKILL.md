---
name: asana
description: "Asana API skill. Use when working with Asana for attachments, workspaces, batch. Covers 167 endpoints."
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
2. GET /attachments -- verify access
3. POST /attachments -- create first attachments

## Endpoints

167 endpoints across 29 groups. See references/api-spec.lap for full details.

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
| GET | /workspaces/{workspace_gid}/tasks/search | Search tasks in a workspace |
| GET | /workspaces/{workspace_gid}/teams | Get teams in a workspace |
| GET | /workspaces/{workspace_gid}/typeahead | Get objects via typeahead |
| GET | /workspaces/{workspace_gid}/users | Get users in a workspace or organization |
| GET | /workspaces/{workspace_gid}/workspace_memberships | Get the workspace memberships for a workspace |
| GET | /workspaces | Get multiple workspaces |
| GET | /workspaces/{workspace_gid} | Get a workspace |
| PUT | /workspaces/{workspace_gid} | Update a workspace |
| POST | /workspaces/{workspace_gid}/addUser | Add a user to a workspace or organization |
| POST | /workspaces/{workspace_gid}/removeUser | Remove a user from a workspace or organization |

### batch
| Method | Path | Description |
|--------|------|-------------|
| POST | /batch | Submit parallel requests |

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

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Get events on a resource |

### goal_relationships
| Method | Path | Description |
|--------|------|-------------|
| GET | /goal_relationships/{goal_relationship_gid} | Get a goal relationship |
| PUT | /goal_relationships/{goal_relationship_gid} | Update a goal relationship |
| GET | /goal_relationships | Get goal relationships |

### goals
| Method | Path | Description |
|--------|------|-------------|
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

### jobs
| Method | Path | Description |
|--------|------|-------------|
| GET | /jobs/{job_gid} | Get a job by id |

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
| GET | /project_templates | Get multiple project templates |
| POST | /project_templates/{project_template_gid}/instantiateProject | Instantiate a project from a project template |

### teams
| Method | Path | Description |
|--------|------|-------------|
| GET | /teams/{team_gid}/project_templates | Get a team's project templates |
| GET | /teams/{team_gid}/projects | Get a team's projects |
| POST | /teams/{team_gid}/projects | Create a project in a team |
| GET | /teams/{team_gid}/team_memberships | Get memberships from a team |
| POST | /teams | Create a team |
| PUT | /teams | Update a team |
| GET | /teams/{team_gid} | Get a team |
| POST | /teams/{team_gid}/addUser | Add a user to a team |
| POST | /teams/{team_gid}/removeUser | Remove a user from a team |
| GET | /teams/{team_gid}/users | Get users in a team |

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
| GET | /status_updates/{status_gid} | Get a status update |
| DELETE | /status_updates/{status_gid} | Delete a status update |
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
| GET | /users/{user_gid}/favorites | Get a user's favorites |
| GET | /users/{user_gid}/workspace_memberships | Get workspace memberships for a user |

### time_periods
| Method | Path | Description |
|--------|------|-------------|
| GET | /time_periods/{time_period_gid} | Get a time period |
| GET | /time_periods | Get time periods |

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

- "What tasks are assigned to me?" -> GET /tasks?assignee=me&workspace={workspace_gid}
- "Show me the details of a specific task" -> GET /tasks/{task_gid}
- "Create a new task in a project" -> POST /tasks (with project in data)
- "What projects exist in my workspace?" -> GET /projects?workspace={workspace_gid}
- "Add a comment or story to a task" -> POST /tasks/{task_gid}/stories
- "Who are the members of a team?" -> GET /teams/{team_gid}/users
- "Search for tasks in a workspace" -> GET /workspaces/{workspace_gid}/tasks/search
- "What are the subtasks of a task?" -> GET /tasks/{task_gid}/subtasks
- "Move a task to a different section" -> POST /sections/{section_gid}/addTask
- "What goals are set for my team?" -> GET /goals?team={team_gid}
- "List all sections in a project" -> GET /projects/{project_gid}/sections
- "What portfolios do I own?" -> GET /portfolios?workspace={workspace_gid}&owner=me
- "Set up a webhook for task changes" -> POST /webhooks (with resource and target)
- "What workspaces do I have access to?" -> GET /workspaces
- "Mark a task as complete" -> PUT /tasks/{task_gid} (set completed: true)

## Response Tips

- **All endpoints**: Responses wrap payload in a `data` key; always access `response.data` not the root object.
- **List endpoints** (tasks, projects, sections, tags): Return `{data: [any]}` arrays; use `limit` and `offset` query params for pagination -- look for `next_page` in the response to determine if more results exist.
- **Mutation endpoints** (addTask, addProject, addMembers, removeTag): Return `{data: map}` (an empty map) on success, not the modified resource; re-fetch if you need the updated object.
- **Events**: Returns `{data, sync, has_more}` -- persist the `sync` token for incremental polling and loop while `has_more` is true.
- **Delete endpoints**: Return `{data: map}` (empty) on 200; a non-error response means the resource is gone.
- **Status codes**: 402 appears only on goals, goal relationships, and attachments (payment-required feature gating); 424/501/503/504 appear only on attachments and project briefs (upstream dependency failures).

## Anomaly Flags

- **402 Payment Required**: Surface immediately -- the user's Asana plan does not support this feature (goals, advanced attachments). Recommend checking plan tier before retrying.
- **424 Failed Dependency**: Attachment or project brief operations depend on external storage; flag as a transient upstream issue and suggest retry after a delay.
- **Batch endpoint misuse**: POST /batch accepts an `actions` array -- flag if a user is making many sequential calls that could be batched (up to Asana's batch limit).
- **Missing pagination**: If a list response returns exactly `limit` items, warn that results may be truncated and offer to fetch the next page via `offset`.
- **Stale sync tokens**: GET /events will return a 412 if the `sync` token is too old; surface this and advise the caller to do a full resync.
- **Empty opt_fields**: Many endpoints support `opt_fields` to reduce payload size; flag when full objects are being fetched repeatedly without field filtering.
- **503/504 on attachments**: Upstream storage timeouts; flag as transient and recommend exponential backoff.

## Playbook

### 1. Create a Task with Subtasks in a Project

1. GET /workspaces to find the target `workspace_gid`
2. GET /projects?workspace={workspace_gid} to find the target `project_gid`
3. GET /projects/{project_gid}/sections to find the target `section_gid`
4. POST /tasks with `{data: {name, projects: [project_gid], workspace: workspace_gid, ...}}`
5. Note the returned `task_gid` from `response.data.gid`
6. POST /tasks/{task_gid}/subtasks with `{data: {name: "Subtask 1"}}` for each subtask
7. Optionally POST /sections/{section_gid}/addTask with `{data: {task: task_gid}}` to place in a specific section

### 2. Set Up Event-Driven Monitoring via Webhooks

1. GET /workspaces to identify the `workspace_gid`
2. GET /projects?workspace={workspace_gid} to find the `resource` GID to monitor
3. POST /webhooks with `{data: {resource: project_gid, target: "https://your-endpoint.com/hook", filters: [{resource_type: "task", action: "changed"}]}}`
4. Respond to the initial handshake request Asana sends to your target URL with the `X-Hook-Secret` header
5. GET /webhooks?workspace={workspace_gid} to verify the webhook is active
6. To stop: DELETE /webhooks/{webhook_gid}

### 3. Track Goal Progress with Metrics

1. GET /goals?workspace={workspace_gid} or GET /goals?team={team_gid} to list goals
2. GET /goals/{goal_gid} to inspect current metric values and status
3. POST /goals/{goal_gid}/setMetric to define or update the goal metric (type, target value, unit)
4. POST /goals/{goal_gid}/setMetricCurrentValue to report progress
5. GET /goals/{goal_gid}/parentGoals to see how this goal rolls up
6. POST /goals/{goal_gid}/addSupportingRelationship to link a project or sub-goal as a contributor

### 4. Organize a Portfolio and Add Projects

1. GET /workspaces to get `workspace_gid`
2. POST /portfolios with `{data: {name: "Q1 Initiatives", workspace: workspace_gid, ...}}`
3. Note the returned `portfolio_gid`
4. GET /projects?workspace={workspace_gid} to find projects to include
5. POST /portfolios/{portfolio_gid}/addItem with `{data: {item: project_gid}}` for each project
6. POST /portfolios/{portfolio_gid}/addCustomFieldSetting to attach tracking fields
7. POST /portfolios/{portfolio_gid}/addMembers with `{data: {members: user_gid}}` to share access

### 5. Bulk Operations Using the Batch Endpoint

1. Identify 2+ independent API calls you need to make (e.g., update multiple tasks)
2. POST /batch with `{data: {actions: [{method: "PUT", relative_path: "/tasks/{gid1}", data: {...}}, {method: "PUT", relative_path: "/tasks/{gid2}", data: {...}}]}}`
3. Parse the response `data` array -- each entry corresponds to one action in order, with its own `status_code` and `body`
4. Check each action's `status_code` individually; partial failures are possible
5. Retry any failed actions individually or in a subsequent batch


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
