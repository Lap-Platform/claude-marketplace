---
name: figma-api
description: "Figma API skill. Use when working with Figma for files, images, teams. Covers 46 endpoints."
version: 1.0.0
generator: lapsh
---

# Figma API
API version: 0.36.0

## Auth
ApiKey X-Figma-Token in header | OAuth2 | OAuth2

## Base URL
https://api.figma.com

## Setup
1. Set your API key in the appropriate header
2. GET /v1/me -- verify access
3. POST /v1/files/{file_key}/comments -- create first comments

## Endpoints

46 endpoints across 13 groups. See references/api-spec.lap for full details.

### files
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/files/{file_key} | Get file JSON |
| GET | /v1/files/{file_key}/nodes | Get file JSON for specific nodes |
| GET | /v1/files/{file_key}/images | Get image fills |
| GET | /v1/files/{file_key}/meta | Get file metadata |
| GET | /v1/files/{file_key}/versions | Get versions of a file |
| GET | /v1/files/{file_key}/comments | Get comments in a file |
| POST | /v1/files/{file_key}/comments | Add a comment to a file |
| DELETE | /v1/files/{file_key}/comments/{comment_id} | Delete a comment |
| GET | /v1/files/{file_key}/comments/{comment_id}/reactions | Get reactions for a comment |
| POST | /v1/files/{file_key}/comments/{comment_id}/reactions | Add a reaction to a comment |
| DELETE | /v1/files/{file_key}/comments/{comment_id}/reactions | Delete a reaction |
| GET | /v1/files/{file_key}/components | Get file components |
| GET | /v1/files/{file_key}/component_sets | Get file component sets |
| GET | /v1/files/{file_key}/styles | Get file styles |
| GET | /v1/files/{file_key}/variables/local | Get local variables |
| GET | /v1/files/{file_key}/variables/published | Get published variables |
| POST | /v1/files/{file_key}/variables | Create/modify/delete variables |
| GET | /v1/files/{file_key}/dev_resources | Get dev resources |
| DELETE | /v1/files/{file_key}/dev_resources/{dev_resource_id} | Delete dev resource |

### images
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/images/{file_key} | Render images of file nodes |

### teams
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/teams/{team_id}/projects | Get projects in a team |
| GET | /v1/teams/{team_id}/components | Get team components |
| GET | /v1/teams/{team_id}/component_sets | Get team component sets |
| GET | /v1/teams/{team_id}/styles | Get team styles |
| GET | /v2/teams/{team_id}/webhooks | [Deprecated] Get team webhooks |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/projects/{project_id}/files | Get files in a project |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/me | Get current user |

### components
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/components/{key} | Get component |

### component_sets
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/component_sets/{key} | Get component set |

### styles
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/styles/{key} | Get style |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/webhooks | Get webhooks by context or plan |
| POST | /v2/webhooks | Create a webhook |
| GET | /v2/webhooks/{webhook_id} | Get a webhook |
| PUT | /v2/webhooks/{webhook_id} | Update a webhook |
| DELETE | /v2/webhooks/{webhook_id} | Delete a webhook |
| GET | /v2/webhooks/{webhook_id}/requests | Get webhook requests |

### activity_logs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/activity_logs | Get activity logs |

### payments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/payments | Get payments |

### dev_resources
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/dev_resources | Create dev resources |
| PUT | /v1/dev_resources | Update dev resources |

### analytics
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/analytics/libraries/{file_key}/component/actions | Get library analytics component action data. |
| GET | /v1/analytics/libraries/{file_key}/component/usages | Get library analytics component usage data. |
| GET | /v1/analytics/libraries/{file_key}/style/actions | Get library analytics style action data. |
| GET | /v1/analytics/libraries/{file_key}/style/usages | Get library analytics style usage data. |
| GET | /v1/analytics/libraries/{file_key}/variable/actions | Get library analytics variable action data. |
| GET | /v1/analytics/libraries/{file_key}/variable/usages | Get library analytics variable usage data. |

## Enhanced Skill Content
## Question Mapping

- "Get the contents of a Figma file" -> GET /v1/files/{file_key}
- "What nodes are in this Figma file?" -> GET /v1/files/{file_key}/nodes
- "Export a frame or layer as PNG/SVG/PDF" -> GET /v1/images/{file_key}
- "List all images uploaded to a file" -> GET /v1/files/{file_key}/images
- "Get metadata about a file without downloading the full document tree" -> GET /v1/files/{file_key}/meta
- "What projects does this team have?" -> GET /v1/teams/{team_id}/projects
- "List all files in a project" -> GET /v1/projects/{project_id}/files
- "Show the version history of a file" -> GET /v1/files/{file_key}/versions
- "Post a comment on a Figma file" -> POST /v1/files/{file_key}/comments
- "Who am I authenticated as?" -> GET /v1/me
- "List all components in a team library" -> GET /v1/teams/{team_id}/components
- "Get details about a specific component by key" -> GET /v1/components/{key}
- "Set up a webhook to notify me when a file changes" -> POST /v2/webhooks
- "Check what design variables are defined in this file" -> GET /v1/files/{file_key}/variables/local
- "How often is a library component being inserted or detached?" -> GET /v1/analytics/libraries/{file_key}/component/actions

## Response Tips

- **Files/Nodes**: `document` is a deeply nested tree; use `ids` and `depth` params to limit payload size. The `components` and `styles` top-level maps are keyed by node ID.
- **Images**: `images` is a map of node ID to URL (or `null` if rendering failed). URLs are temporary and expire.
- **Versions**: Paginated via `pagination.prev_page`/`next_page` URLs; pass `before`/`after` cursor values for paging.
- **Comments/Reactions**: Paginated via `cursor` param. Comments have optional `parent_id` for threading.
- **Team resources (components, styles, component_sets)**: Cursor-based pagination using `meta.cursor.before`/`meta.cursor.after` with `page_size` (default 30).
- **Webhooks**: v2 endpoints. `status` field is either `ACTIVE` or `PAUSED`. List endpoint supports filtering by `context` and `context_id`.
- **Analytics**: All analytics endpoints return `rows`, `next_page` (bool), and `cursor` for pagination. Rows schema varies by `group_by` value.
- **Variables**: `meta.variables` and `meta.variableCollections` are maps keyed by ID, not arrays.
- **Dev resources**: Batch create/update endpoints return both `links_created`/`links_updated` and `errors` arrays -- always check both.
- **Errors**: All endpoints return standard HTTP codes. 429 = rate limited. Wrapping responses often include `status` and `error` boolean fields.

## Anomaly Flags

- **429 Too Many Requests**: Surface immediately with retry-after guidance. Figma enforces per-token rate limits.
- **`images` map contains `null` values**: Rendering failed for those node IDs. Flag which nodes failed and suggest checking node validity.
- **`error: true` in response body**: Several endpoints (components, styles, variables, payments) wrap responses with `status`/`error` fields. Flag when `error` is `true` even on HTTP 200.
- **Empty `components`/`styles` maps on file GET**: May indicate the file has no published library assets, or the token lacks library read scope.
- **Webhook status `PAUSED`**: Surface when listing webhooks -- a paused webhook silently drops events.
- **`next_page: true` on analytics**: Data is incomplete. Alert the user that additional pages exist and offer to paginate automatically.
- **File `role` is `viewer`**: Write operations (comments, variables, dev resources) will likely fail with 403. Flag before attempting writes.
- **`branches` array present**: File has branches. Edits may target the wrong branch if `branch_data` is not considered.
- **Deprecated or missing `version` param**: If a user requests a stale version string that no longer exists, the API returns 404. Surface version mismatch early.

## Playbook

### 1. Export Design Assets from a File

1. Call `GET /v1/files/{file_key}` with `depth=1` to get top-level page structure and node IDs
2. Identify target node IDs from the document tree (frames, components, groups)
3. Call `GET /v1/images/{file_key}` with `ids` set to comma-separated node IDs, desired `format` (png/svg/pdf) and `scale`
4. Check the `images` map in the response -- each key is a node ID, each value is a temporary download URL (or `null` on failure)
5. Download images from the URLs before they expire

### 2. Audit Team Design System Components

1. Call `GET /v1/teams/{team_id}/projects` to list all projects
2. Call `GET /v1/projects/{project_id}/files` for each project to find library files
3. Call `GET /v1/teams/{team_id}/components` with pagination (`page_size`, `after`) to enumerate all published components
4. For each component, call `GET /v1/components/{key}` to get description, containing frame, and last updated timestamp
5. Optionally call `GET /v1/analytics/libraries/{file_key}/component/usages` grouped by `file` to find unused components

### 3. Set Up File Change Notifications

1. Call `GET /v1/me` to verify authentication and permissions
2. Call `POST /v2/webhooks` with `event_type: "FILE_UPDATE"`, `context` and `context_id` pointing to the team/project, `endpoint` as your callback URL, and a `passcode` for verification
3. Call `GET /v2/webhooks/{webhook_id}` to confirm status is `ACTIVE`
4. Monitor delivery with `GET /v2/webhooks/{webhook_id}/requests` to check for failures
5. If issues arise, call `PUT /v2/webhooks/{webhook_id}` to update the endpoint or pause/resume

### 4. Manage Design Variables Across Modes

1. Call `GET /v1/files/{file_key}/variables/local` to get all variables and variable collections with their modes
2. Review the `meta.variableCollections` map to understand groupings and available modes
3. Call `POST /v1/files/{file_key}/variables` with `variableModeValues` array to set values per variable per mode
4. Use `tempIdToRealId` from the response to map any newly created variable/collection temp IDs to permanent IDs
5. Call `GET /v1/files/{file_key}/variables/published` to verify which variables are published to the library

### 5. Review and Respond to File Comments

1. Call `GET /v1/files/{file_key}/comments` (optionally with `as_md=true` for markdown formatting) to list all comments
2. Filter comments by `resolved_at` (null = unresolved) and `parent_id` (null = top-level) to find open threads
3. Reply to a comment by calling `POST /v1/files/{file_key}/comments` with `message` and `comment_id` set to the parent comment's ID
4. React to a comment with `POST /v1/files/{file_key}/comments/{comment_id}/reactions` and the desired `emoji`
5. Resolve finished threads by noting which comments to clean up, or delete stale comments with `DELETE /v1/files/{file_key}/comments/{comment_id}`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
