---
name: 1password-connect
description: "1Password Connect API skill. Use when working with 1Password Connect for activity, vaults, heartbeat. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# 1Password Connect
API version: 1.7.1

## Auth
Bearer bearer

## Base URL
http://localhost:8080/v1

## Setup
1. Set Authorization header with your Bearer token
2. GET /activity -- verify access
3. POST /vaults/{vaultUuid}/items -- create first items

## Endpoints

15 endpoints across 5 groups. See references/api-spec.lap for full details.

### activity
| Method | Path | Description |
|--------|------|-------------|
| GET | /activity | Retrieve a list of API Requests that have been made. |

### vaults
| Method | Path | Description |
|--------|------|-------------|
| GET | /vaults | Get all Vaults |
| GET | /vaults/{vaultUuid} | Get Vault details and metadata |
| GET | /vaults/{vaultUuid}/items | Get all items for inside a Vault |
| POST | /vaults/{vaultUuid}/items | Create a new Item |
| GET | /vaults/{vaultUuid}/items/{itemUuid} | Get the details of an Item |
| PUT | /vaults/{vaultUuid}/items/{itemUuid} | Update an Item |
| DELETE | /vaults/{vaultUuid}/items/{itemUuid} | Delete an Item |
| PATCH | /vaults/{vaultUuid}/items/{itemUuid} | Update a subset of Item attributes |
| GET | /vaults/{vaultUuid}/items/{itemUuid}/files | Get all the files inside an Item |
| GET | /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid} | Get the details of a File |
| GET | /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid}/content | Get the content of a File |

### heartbeat
| Method | Path | Description |
|--------|------|-------------|
| GET | /heartbeat | Ping the server for liveness |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Get state of the server and its dependencies. |

### metrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics | Query server for exposed Prometheus metrics |

## Enhanced Skill Content
## Question Mapping

- "What vaults do I have access to?" -> GET /vaults
- "Show me the details of a specific vault" -> GET /vaults/{vaultUuid}
- "List all items in a vault" -> GET /vaults/{vaultUuid}/items
- "Find items matching a title in a vault" -> GET /vaults/{vaultUuid}/items (with filter param)
- "Get a specific item's full details including fields" -> GET /vaults/{vaultUuid}/items/{itemUuid}
- "Create a new login item in a vault" -> POST /vaults/{vaultUuid}/items
- "Update an existing item completely" -> PUT /vaults/{vaultUuid}/items/{itemUuid}
- "Change a single field on an item without replacing the whole thing" -> PATCH /vaults/{vaultUuid}/items/{itemUuid}
- "Delete an item from a vault" -> DELETE /vaults/{vaultUuid}/items/{itemUuid}
- "List files attached to an item" -> GET /vaults/{vaultUuid}/items/{itemUuid}/files
- "Download a specific file attachment" -> GET /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid}/content
- "Get file metadata with inline content" -> GET /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid} (with inline_files=true)
- "Check if the Connect server is running" -> GET /heartbeat
- "Check server health and dependency status" -> GET /health
- "View recent activity and audit log" -> GET /activity

## Response Tips

- **Vaults**: Vault list returns flat array; vault detail includes `items` count, `attributeVersion`/`contentVersion` for change tracking, and ISO 8601 timestamps.
- **Items**: Item list supports `filter` query (e.g., `title eq "MyLogin"`); full item responses contain nested `fields`, `sections`, and `urls` arrays -- always check `fields[].value` for secrets.
- **Files**: File metadata returns `content` as base64 bytes only when `inline_files=true`; use the `/content` sub-path to stream raw file data directly. Watch for 413 errors on large files.
- **Activity**: Paginated via `limit`/`offset` (default 50); returns newest-first. No total count header -- keep fetching until results < limit.
- **Health/Heartbeat**: Health returns `dependencies` array with individual service statuses; heartbeat is a simple 200 liveness check with no body.
- **Errors**: 401 means invalid or missing Bearer token across all endpoints; 403 means valid token but insufficient vault permissions; 404 means the UUID does not exist.

## Anomaly Flags

- **401 on any call**: Bearer token is expired, missing, or misconfigured -- surface immediately and suggest checking the `OP_CONNECT_TOKEN` environment variable.
- **403 on vault/item access**: The Connect token lacks permission for that vault -- recommend creating a new token with the correct vault scope in 1Password.
- **413 on file endpoints**: File exceeds size limit -- flag the file name and size, suggest downloading via `/content` stream instead of inline.
- **Health dependency degradation**: If any entry in `dependencies` array shows unhealthy status, proactively warn that Connect server operations may fail.
- **Empty vault list**: A 200 with zero vaults likely means the token has no vault access grants -- surface this before the user tries item operations that will 404.
- **Version drift**: Compare `version` from `/health` against known latest (1.7.x) and flag if significantly outdated.
- **High item counts**: If a vault's `items` count is very large (1000+), warn that list operations may be slow and suggest using `filter` to narrow results.

## Playbook

### 1. Retrieve a Secret Value

1. GET /vaults to list available vaults; note the `id` of the target vault
2. GET /vaults/{vaultUuid}/items?filter=title eq "MySecret" to find the item by name
3. GET /vaults/{vaultUuid}/items/{itemUuid} to fetch full item with all fields
4. Extract the value from the `fields` array where `label` or `purpose` matches the desired field (e.g., `password`, `username`)

### 2. Create a New Login Item

1. GET /vaults to identify the destination vault UUID
2. POST /vaults/{vaultUuid}/items with a JSON body containing `category: "LOGIN"`, `title`, and `fields` array (include `username` and `password` fields with appropriate `purpose` values)
3. Confirm the 200 response returns the created item with a generated `id`
4. Optionally GET /vaults/{vaultUuid}/items/{itemUuid} to verify the item was stored correctly

### 3. Rotate a Password

1. GET /vaults/{vaultUuid}/items/{itemUuid} to fetch the current item
2. Note the full item structure including all existing fields and sections
3. Modify only the `password` field value in the `fields` array
4. PUT /vaults/{vaultUuid}/items/{itemUuid} with the complete updated item body
5. Alternatively, use PATCH /vaults/{vaultUuid}/items/{itemUuid} with a JSON Patch array to update only the password field without sending the full object

### 4. Download a File Attachment

1. GET /vaults/{vaultUuid}/items/{itemUuid}/files to list all attachments on the item
2. Identify the target file by `name` and note its `id` and `size`
3. GET /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid}/content to download the raw file content
4. If you need metadata alongside content in a single call, use GET /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid}?inline_files=true (base64-encoded in `content` field)

### 5. Server Health Check and Diagnostics

1. GET /heartbeat for a quick liveness check (expect bare 200)
2. If heartbeat succeeds, GET /health to inspect `name`, `version`, and `dependencies` status
3. GET /metrics for operational telemetry (Prometheus-format output)
4. If any dependency shows degraded status, GET /activity to check for recent error patterns before proceeding with vault operations


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
