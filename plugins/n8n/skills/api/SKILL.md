---
name: n8n-public-api
description: "n8n Public API skill. Use when working with n8n Public for audit, credentials, executions. Covers 59 endpoints."
version: 1.0.0
generator: lapsh
---

# n8n Public API
API version: 1.1.1

## Auth
ApiKey X-N8N-API-KEY in header

## Base URL
/api/v1

## Setup
1. Set your API key in the appropriate header
2. GET /credentials -- verify access
3. POST /audit -- create first audit

## Endpoints

59 endpoints across 10 groups. See references/api-spec.lap for full details.

### audit
| Method | Path | Description |
|--------|------|-------------|
| POST | /audit | Generate an audit |

### credentials
| Method | Path | Description |
|--------|------|-------------|
| GET | /credentials | List credentials |
| POST | /credentials | Create a credential |
| PATCH | /credentials/{id} | Update credential by ID |
| DELETE | /credentials/{id} | Delete credential by ID |
| GET | /credentials/schema/{credentialTypeName} | Show credential data schema |
| PUT | /credentials/{id}/transfer | Transfer a credential to another project. |

### executions
| Method | Path | Description |
|--------|------|-------------|
| GET | /executions | Retrieve all executions |
| GET | /executions/{id} | Retrieve an execution |
| DELETE | /executions/{id} | Delete an execution |
| POST | /executions/{id}/retry | Retry an execution |
| POST | /executions/{id}/stop | Stop an execution |
| POST | /executions/stop | Stop multiple executions |
| GET | /executions/{id}/tags | Get execution tags |
| PUT | /executions/{id}/tags | Update tags of an execution |

### tags
| Method | Path | Description |
|--------|------|-------------|
| POST | /tags | Create a tag |
| GET | /tags | Retrieve all tags |
| GET | /tags/{id} | Retrieves a tag |
| DELETE | /tags/{id} | Delete a tag |
| PUT | /tags/{id} | Update a tag |

### workflows
| Method | Path | Description |
|--------|------|-------------|
| POST | /workflows | Create a workflow |
| GET | /workflows | Retrieve all workflows |
| GET | /workflows/{id} | Retrieve a workflow |
| DELETE | /workflows/{id} | Delete a workflow |
| PUT | /workflows/{id} | Update a workflow |
| GET | /workflows/{id}/{versionId} | Retrieves a specific version of a workflow |
| POST | /workflows/{id}/activate | Publish a workflow |
| POST | /workflows/{id}/deactivate | Deactivate a workflow |
| PUT | /workflows/{id}/transfer | Transfer a workflow to another project |
| GET | /workflows/{id}/tags | Get workflow tags |
| PUT | /workflows/{id}/tags | Update tags of a workflow |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | Retrieve all users |
| POST | /users | Create multiple users |
| GET | /users/{id} | Get user by ID/Email |
| DELETE | /users/{id} | Delete a user |
| PATCH | /users/{id}/role | Change a user's global role |

### source-control
| Method | Path | Description |
|--------|------|-------------|
| POST | /source-control/pull | Pull changes from the remote repository |

### variables
| Method | Path | Description |
|--------|------|-------------|
| POST | /variables | Create a variable |
| GET | /variables | Retrieve variables |
| DELETE | /variables/{id} | Delete a variable |
| PUT | /variables/{id} | Update a variable |

### data-tables
| Method | Path | Description |
|--------|------|-------------|
| GET | /data-tables | List all data tables |
| POST | /data-tables | Create a new data table |
| GET | /data-tables/{dataTableId} | Get a data table |
| PATCH | /data-tables/{dataTableId} | Update a data table |
| DELETE | /data-tables/{dataTableId} | Delete a data table |
| GET | /data-tables/{dataTableId}/rows | Retrieve rows from a data table |
| POST | /data-tables/{dataTableId}/rows | Insert rows into a data table |
| PATCH | /data-tables/{dataTableId}/rows/update | Update rows in a data table |
| POST | /data-tables/{dataTableId}/rows/upsert | Upsert a row in a data table |
| DELETE | /data-tables/{dataTableId}/rows/delete | Delete rows from a data table |

### projects
| Method | Path | Description |
|--------|------|-------------|
| POST | /projects | Create a project |
| GET | /projects | Retrieve projects |
| DELETE | /projects/{projectId} | Delete a project |
| PUT | /projects/{projectId} | Update a project |
| GET | /projects/{projectId}/users | List project members |
| POST | /projects/{projectId}/users | Add one or more users to a project |
| DELETE | /projects/{projectId}/users/{userId} | Delete a user from a project |
| PATCH | /projects/{projectId}/users/{userId} | Change a user's role in a project |

## Enhanced Skill Content
## Question Mapping

- "How do I run a security audit on my n8n instance?" -> POST /audit
- "List all my workflows" -> GET /workflows
- "Show me failed executions for a specific workflow" -> GET /executions (with status=error and workflowId)
- "How do I create a new credential?" -> POST /credentials
- "Can I retry a failed execution?" -> POST /executions/{id}/retry
- "How do I activate a workflow?" -> POST /workflows/{id}/activate
- "What tags are on this workflow?" -> GET /workflows/{id}/tags
- "How do I transfer a workflow to another project?" -> PUT /workflows/{id}/transfer
- "Show me all environment variables" -> GET /variables
- "How do I create a data table and add rows to it?" -> POST /data-tables then POST /data-tables/{dataTableId}/rows
- "Who are the members of a project?" -> GET /projects/{projectId}/users
- "How do I stop all running executions?" -> POST /executions/stop (with status filter)
- "What credential types are available and what fields do they need?" -> GET /credentials/schema/{credentialTypeName}
- "How do I pull the latest changes from source control?" -> POST /source-control/pull
- "How do I bulk update rows in a data table by condition?" -> PATCH /data-tables/{dataTableId}/rows/update

## Response Tips

- **Paginated lists** (credentials, executions, tags, workflows, users, variables, data-tables, projects): All return `{data: [...], nextCursor: str?}`. When `nextCursor` is present, pass it as `cursor` on the next request. Default page size is 100.
- **Executions**: Response includes `status` (canceled/error/running/success/waiting), `finished` boolean, and nullable `stoppedAt`/`waitTill`/`retryOf` fields -- check all three to determine true state.
- **Workflows**: Nodes, connections, and settings are deeply nested maps. The optional `activeVersion` object is null when no version is pinned. Tags and shared arrays may be empty but are always present.
- **Audit**: Returns five separate risk report maps (Credentials, Database, Filesystem, Nodes, Instance) -- each is independent and may have different severity structures.
- **Data tables**: Row operations (update, upsert, delete) support `dryRun: true` to preview changes without applying them. Use `returnData: true` to get affected rows in the response.
- **Deletions**: User delete returns 204 (no body), while credential/tag/workflow deletes return 200 with the deleted object. Variable and data-table deletes return 204.

## Anomaly Flags

- **401 on any endpoint**: API key is missing, invalid, or revoked -- surface immediately and suggest checking the `X-N8N-API-KEY` header.
- **409 on execution retry**: The execution is already running or queued -- warn the user before they retry again.
- **409 on tag/data-table create or update**: Name conflict detected -- surface the existing resource name and suggest renaming.
- **403 on user/project/variable operations**: Current API key lacks admin or owner permissions -- flag the permission gap and suggest using a higher-privilege key.
- **Execution status "waiting"**: Workflow is paused at a Wait node -- proactively inform the user this is not an error and the execution will resume on trigger.
- **Large nextCursor chains**: If pagination exceeds 5 pages, alert the user to consider filtering (by workflowId, status, projectId, tags) to narrow results.
- **Source control pull conflict (409)**: Unresolved merge conflict -- surface immediately and advise manual resolution before retrying.
- **Bulk stop returning stopped: 0**: No executions matched the filter -- warn the user their status/date filters may be too narrow.

## Playbook

### 1. Create and activate a new workflow

1. `POST /credentials` to create any credentials the workflow needs (e.g., HTTP header auth, OAuth2). Note the returned `id`.
2. `POST /tags` to create organizational tags if they do not already exist.
3. `POST /workflows` with the workflow name, nodes array (referencing credential IDs), connections map, and settings. Optionally attach tags.
4. `POST /workflows/{id}/activate` to turn the workflow on.
5. `GET /workflows/{id}` to confirm `active: true` in the response.

### 2. Investigate and retry failed executions

1. `GET /executions?status=error&workflowId={id}` to list all failed executions for a workflow.
2. `GET /executions/{id}?includeData=true` on each failure to inspect the full execution data and identify the failing node.
3. Fix the root cause (update credentials via `PATCH /credentials/{id}`, or update the workflow via `PUT /workflows/{id}`).
4. `POST /executions/{id}/retry` to re-run the failed execution. If the workflow definition changed, pass `loadWorkflow: true` to use the updated version.
5. `GET /executions/{id}` to verify the retry succeeded (`status: "success"`).

### 3. Set up a project with team members

1. `POST /projects` with a project name to create the workspace.
2. `GET /users` to find user IDs for team members you want to add.
3. `POST /projects/{projectId}/users` with a `relations` array mapping each userId to a role (e.g., `"editor"`, `"viewer"`).
4. `PUT /workflows/{id}/transfer` and/or `PUT /credentials/{id}/transfer` to move existing resources into the project using `destinationProjectId`.
5. `GET /projects/{projectId}/users` to confirm membership and roles.

### 4. Build and query a data table

1. `POST /data-tables` with a name and column definitions (each column needs `name` and `type`).
2. `POST /data-tables/{dataTableId}/rows` with a `data` array of row objects matching the column schema. Use `returnType: "all"` to get inserted rows back.
3. `GET /data-tables/{dataTableId}/rows?search=term` or pass a `filter` JSON string to query rows.
4. `PATCH /data-tables/{dataTableId}/rows/update` with a filter and data map to bulk-update matching rows. Use `dryRun: true` first to preview.
5. `DELETE /data-tables/{dataTableId}/rows/delete` with a filter to remove rows. Again, `dryRun: true` is recommended before committing.

### 5. Audit instance security and remediate

1. `POST /audit` with no body to run a full audit, or pass `additionalOptions.categories` to scope it (e.g., `["credentials", "nodes"]`).
2. Review each of the five returned risk reports: Credentials, Database, Filesystem, Nodes, Instance.
3. For credential risks, `GET /credentials` to list affected credentials, then `PATCH /credentials/{id}` to rotate secrets or update configurations.
4. For workflow/node risks, `GET /workflows/{id}` to inspect flagged workflows, then `PUT /workflows/{id}` to fix risky node configurations.
5. Re-run `POST /audit` to confirm the risk scores have improved.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
