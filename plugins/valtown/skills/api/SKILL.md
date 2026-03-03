---
name: val-town-api
description: "Val Town API skill. Use when working with Val Town for alias, me, blob. Covers 36 endpoints."
version: 1.0.0
generator: lapsh
---

# Val Town API
API version: 1

## Auth
Bearer bearer

## Base URL
https://api.val.town

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/me -- verify access
3. POST /v1/blob/{key} -- create first blob

## Endpoints

36 endpoints across 11 groups. See references/api-spec.lap for full details.

### alias
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/alias/{username} | Get basic details about a user, given their username |
| GET | /v2/alias/vals/{username}/{val_name} | Get a val |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/me | Get profile information for the current user |
| GET | /v2/me/vals | [BETA] List all of a user's vals for authenticated users |

### blob
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/blob | List blobs in your account |
| GET | /v1/blob/{key} | Get a blob’s contents. |
| POST | /v1/blob/{key} | Store data in blob storage |
| DELETE | /v1/blob/{key} | Delete a blob |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/users/{user_id} | Get basic information about a user |

### sqlite
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/sqlite/execute | Execute a single SQLite statement and return results |
| POST | /v1/sqlite/batch | Execute a batch of SQLite statements and return results for all of them |

### email
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/email | Send emails |

### telemetry
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/telemetry/traces | Get OpenTelemetry traces within a specified time window with flexible pagination options: Pass in only the end time to paginate backwards from there. Pass in a start time to paginate backwards from now until the start time. Pass in both to get resources within the time window. Choose to return in end_time order instead to view traces that completed in a window or since a time. Filter additionally by branch_ids or file_id. |
| GET | /v1/telemetry/logs | Get OpenTelemetry logs within a specified time window with flexible pagination options: Pass in only the end time to paginate backwards from there. Pass in a start time to paginate backwards from now until the start time. Pass in both to get resources within the time window. Filter additionally by branch_ids or file_id. |

### vals
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/vals/{val_id} | Get a val by id |
| DELETE | /v2/vals/{val_id} | Delete a project |
| GET | /v2/vals | Lists all vals including all public vals and your unlisted and private vals |
| POST | /v2/vals | Create a new val |
| GET | /v2/vals/{val_id}/branches/{branch_id} | Get a branch by id |
| DELETE | /v2/vals/{val_id}/branches/{branch_id} | Delete a branch |
| GET | /v2/vals/{val_id}/branches | List all branches for a val |
| POST | /v2/vals/{val_id}/branches | Create a new branch |
| GET | /v2/vals/{val_id}/files | Get metadata for files and directories in a val. If path is an empty string, returns files at the root directory. |
| POST | /v2/vals/{val_id}/files | Create a new file, project val or directory |
| DELETE | /v2/vals/{val_id}/files | Deletes a file or a directory. To delete a directory and all of its children, use the recursive flag. To delete all files, pass in an empty path and the recursive flag. |
| PUT | /v2/vals/{val_id}/files | Update a file's content |
| GET | /v2/vals/{val_id}/environment_variables | List environment variables defined in this project. This only includes names, not values. |
| POST | /v2/vals/{val_id}/environment_variables | Create a new environment variable scoped to this project. |
| PUT | /v2/vals/{val_id}/environment_variables/{key} | Update a environment variable scoped to this project. |
| DELETE | /v2/vals/{val_id}/environment_variables/{key} | Delete a environment variable scoped to this project. |
| GET | /v2/vals/{val_id}/files/content | Download file content |

### files
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/files/{file_id} | Get file metadata by file ID |

### orgs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/orgs | Get all orgs you are a member of |
| GET | /v2/orgs/{org_id}/memberships | List all memberships of an org |

### connections
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/connections/slack/token | Get a valid Slack access token for a connected workspace. Automatically refreshes the token if expired. |
| POST | /v3/connections/google-docs/token | Get a valid Google access token for a connected Google account. Automatically refreshes the token if expired. |

## Enhanced Skill Content
## Question Mapping

- "Who am I logged in as?" -> GET /v1/me
- "Look up a user by username" -> GET /v1/alias/{username}
- "Get user details by ID" -> GET /v1/users/{user_id}
- "List all my vals" -> GET /v2/me/vals
- "Find a val by username and name" -> GET /v2/alias/vals/{username}/{val_name}
- "Create a new private val" -> POST /v2/vals
- "Delete a val" -> DELETE /v2/vals/{val_id}
- "Run a SQL query against my SQLite database" -> POST /v1/sqlite/execute
- "Run multiple SQL statements in a transaction" -> POST /v1/sqlite/batch
- "Send an email from my val" -> POST /v1/email
- "Store a value in blob storage" -> POST /v1/blob/{key}
- "List all blobs with a given prefix" -> GET /v1/blob
- "Read the source code of a file in a val" -> GET /v2/vals/{val_id}/files/content
- "Set an environment variable on a val" -> POST /v2/vals/{val_id}/environment_variables
- "Check recent execution logs for a val" -> GET /v1/telemetry/logs

## Response Tips

- **Paginated lists** (vals, branches, files, env vars, orgs, telemetry): Response includes `data` array and `links` object with `self`, `prev`, `next` URIs. Use `offset`/`limit` or `cursor` params to page through. A missing `next` link means you are on the last page.
- **User/alias lookups**: Return a flat object with `id`, `username`, `url`, and a `links.self` URI. The `bio`, `username`, and `profileImageUrl` fields are nullable (`any` type).
- **SQLite execute**: Returns `columns`, `columnTypes`, `rows` (array of arrays), `rowsAffected`, and `lastInsertRowid`. Parse `rows` positionally against `columns`.
- **Blob storage**: GET returns raw blob content (not JSON). POST returns 201 with no body. DELETE returns 204.
- **Email**: Returns 202 (accepted, not sent yet) with a `message` string. A 500 means delivery failure.
- **File operations**: PUT returns 200 for updates, 201 for creates. The response includes `links.module` (import URL), `links.endpoint` (HTTP trigger URL), and `links.email` (email trigger address).
- **Connections (Slack/Google Docs)**: Return short-lived `access_token` strings. 403 means the connection exists but is not authorized; 404 means no connection found.

## Anomaly Flags

- **409 Conflict** on val or branch creation: Name collision. Surface the conflicting resource name and suggest an alternative.
- **304 Not Modified / 412 Precondition Failed** on file content reads: Conditional request headers (`If-Match`, `If-None-Match`) did not match. Alert the user that the file version may have changed or is already cached.
- **204 with no body** on DELETE operations: Normal, but flag if the caller expects a response body.
- **500 on email send**: Val Town email delivery failed. Surface immediately and suggest checking the `to`/`from` fields and attachment sizes.
- **Nullable user fields**: `bio`, `username`, `profileImageUrl` can all be null. Flag when a user profile has no username set, as alias lookups will not work for that user.
- **SQLite batch mode parameter**: If `mode` is omitted on a batch with writes, the default may not be `write`. Surface a warning when INSERT/UPDATE/DELETE statements are sent without explicit `mode: "write"`.
- **Blob key collisions**: POST to an existing blob key overwrites silently (returns 201 either way). Flag when overwriting a key that was recently written.

## Playbook

### 1. Create a Val and Add a File

1. GET /v1/me to confirm authentication and retrieve your user ID
2. POST /v2/vals with `name` and `privacy` (e.g., `"public"`) to create the val
3. Note the `id` from the 201 response
4. PUT /v2/vals/{val_id}/files with `path` (e.g., `"main.tsx"`), `content` (source code), and `type` (e.g., `"http"`)
5. Verify using the `links.endpoint` URL from the response to confirm the val is live

### 2. Query and Modify SQLite Data

1. POST /v1/sqlite/execute with `statement: "SELECT name FROM sqlite_master WHERE type='table'"` to list all tables
2. POST /v1/sqlite/execute with your SELECT query to inspect data
3. POST /v1/sqlite/batch with `statements` array and `mode: "write"` to run INSERT/UPDATE/DELETE operations atomically
4. Verify by running a follow-up SELECT via /v1/sqlite/execute

### 3. Debug a Failing Val

1. GET /v2/vals/{val_id} to confirm the val exists and check its privacy setting
2. GET /v2/vals/{val_id}/files with `path: "/"` and `recursive: true` to list all files
3. GET /v2/vals/{val_id}/files/content with the target file's `path` to read its source
4. GET /v1/telemetry/traces with `file_id` set to the file's ID and `direction: "desc"` to see recent executions
5. GET /v1/telemetry/logs filtered by the trace ID from step 4 to read error details

### 4. Manage Environment Variables for a Val

1. GET /v2/vals/{val_id}/environment_variables to list current env vars
2. POST /v2/vals/{val_id}/environment_variables with `key`, `value`, and optional `description` to add a new variable
3. PUT /v2/vals/{val_id}/environment_variables/{key} with updated `value` to rotate a secret
4. DELETE /v2/vals/{val_id}/environment_variables/{key} to remove a variable that is no longer needed

### 5. Store and Retrieve Data with Blob Storage

1. GET /v1/blob with `prefix` to check if the target key already exists
2. POST /v1/blob/{key} with the data payload in the request body to store it
3. GET /v1/blob/{key} to retrieve and verify the stored content
4. DELETE /v1/blob/{key} when the data is no longer needed


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object
- Error responses use types: Conflict

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
