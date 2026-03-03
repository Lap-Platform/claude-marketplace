---
name: 1password-connect
description: "1Password Connect API skill. Use when working with 1Password Connect for activity, vaults, heartbeat. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# 1Password Connect
API version: 1.5.7

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
- "Get a specific item's full details including fields and sections" -> GET /vaults/{vaultUuid}/items/{itemUuid}
- "Create a new login item in a vault" -> POST /vaults/{vaultUuid}/items
- "Update an existing item completely" -> PUT /vaults/{vaultUuid}/items/{itemUuid}
- "Change just one field on an item without replacing everything" -> PATCH /vaults/{vaultUuid}/items/{itemUuid}
- "Delete an item from a vault" -> DELETE /vaults/{vaultUuid}/items/{itemUuid}
- "List files attached to an item" -> GET /vaults/{vaultUuid}/items/{itemUuid}/files
- "Download a specific file's content" -> GET /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid}/content
- "Is the Connect server running?" -> GET /heartbeat
- "Check the health and dependency status of the server" -> GET /health
- "Show recent activity and audit events" -> GET /activity

## Response Tips

- **Vaults/Items listing**: Responses are arrays; use `filter` param (SCIM-style, e.g. `title eq "MyLogin"`) to narrow results server-side rather than fetching all and filtering client-side.
- **Single vault/item**: Returns full object with nested `sections`, `fields`, and `urls` arrays; credentials live inside `fields` -- look for `purpose` or `label` to identify username/password.
- **Files**: Set `inline_files=true` to get base64-encoded `content` inline; without it you get metadata only and must call the `/content` endpoint separately. Watch for 413 errors on large files.
- **DELETE**: Returns 204 with no body on success -- do not attempt to parse a response.
- **Health**: The `dependencies` array contains objects with `service` and `status` fields indicating backend connectivity (e.g., to the 1Password service).
- **Activity**: Supports `limit`/`offset` pagination; default limit is 50. Iterate by incrementing offset until fewer results than limit are returned.

## Anomaly Flags

- **401 on any endpoint**: Bearer token is missing, expired, or invalid -- surface immediately and suggest checking the `OP_CONNECT_TOKEN` environment variable.
- **403 Forbidden**: The token lacks permission for the target vault -- flag that the Connect server's token-vault access scope needs updating in 1Password.
- **413 Payload Too Large**: Returned on file endpoints when content exceeds size limits -- alert the user and suggest using the `/content` streaming endpoint instead of `inline_files`.
- **Health dependency degradation**: If `GET /health` returns dependencies with non-healthy status, proactively warn that the Connect server cannot reach the 1Password backend.
- **Heartbeat failure**: If `GET /heartbeat` returns non-200 or times out, surface that the Connect server may be down before attempting any other operations.
- **Empty vault list**: If `GET /vaults` returns an empty array, flag that the Connect token may not have any vaults assigned to it.
- **404 on item operations**: Could indicate the item was deleted externally or the UUID is stale -- suggest re-listing items to confirm existence.

## Playbook

### 1. Retrieve a Password from a Known Vault

1. `GET /vaults` to list available vaults and find the target vault's `id`.
2. `GET /vaults/{vaultUuid}/items?filter=title eq "ServiceName"` to find the item by title.
3. `GET /vaults/{vaultUuid}/items/{itemUuid}` to get full item details including credential fields.
4. Parse the `fields` array: look for entries with `purpose: "USERNAME"` and `purpose: "PASSWORD"`.

### 2. Create a New Login Item

1. `GET /vaults` to identify the destination vault UUID.
2. `POST /vaults/{vaultUuid}/items` with a body containing `category: "LOGIN"`, a `title`, and a `fields` array with username and password field objects.
3. Confirm success by checking for a 200 response with the created item's `id`.
4. Optionally `GET /vaults/{vaultUuid}/items/{itemUuid}` to verify the item was stored correctly.

### 3. Rotate a Secret

1. `GET /vaults/{vaultUuid}/items?filter=title eq "TargetItem"` to find the item.
2. `GET /vaults/{vaultUuid}/items/{itemUuid}` to retrieve the current item structure.
3. `PATCH /vaults/{vaultUuid}/items/{itemUuid}` with an update operation targeting the password field's `value` to set the new secret.
4. Verify with `GET /vaults/{vaultUuid}/items/{itemUuid}` that the field was updated.

### 4. Download a File Attachment

1. `GET /vaults/{vaultUuid}/items/{itemUuid}/files` to list all attached files and get their UUIDs and names.
2. `GET /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid}?inline_files=true` to get metadata with base64 content inline, OR
3. `GET /vaults/{vaultUuid}/items/{itemUuid}/files/{fileUuid}/content` to stream the raw file content directly.

### 5. Health Check and Diagnostics

1. `GET /heartbeat` to confirm the Connect server process is responding.
2. `GET /health` to check server version and dependency connectivity status.
3. `GET /metrics` to pull Prometheus-format metrics for monitoring integration.
4. If any check fails, inspect Connect server logs and verify network connectivity to the 1Password service.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
