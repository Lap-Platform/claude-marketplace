---
name: apicurio-registry-api-v2
description: "Apicurio Registry API [v2] API skill. Use when working with Apicurio Registry API [v2] for ids, admin, system. Covers 65 endpoints."
version: 1.0.0
generator: lapsh
---

# Apicurio Registry API [v2]
API version: 2.6.x

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /admin/artifactTypes -- verify access
3. POST /admin/rules -- create first rules

## Endpoints

65 endpoints across 6 groups. See references/api-spec.lap for full details.

### ids
| Method | Path | Description |
|--------|------|-------------|
| GET | /ids/globalIds/{globalId} | Get artifact by global ID |
| GET | /ids/contentHashes/{contentHash}/references | List artifact references by hash |
| GET | /ids/contentIds/{contentId}/references | List artifact references by content ID |
| GET | /ids/globalIds/{globalId}/references | List artifact references by global ID |
| GET | /ids/contentIds/{contentId} | Get artifact content by ID |
| GET | /ids/contentHashes/{contentHash} | Get artifact content by SHA-256 hash |

### admin
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin/artifactTypes | List artifact types |
| GET | /admin/rules | List global rules |
| POST | /admin/rules | Create global rule |
| DELETE | /admin/rules | Delete all global rules |
| GET | /admin/rules/{rule} | Get global rule configuration |
| PUT | /admin/rules/{rule} | Update global rule configuration |
| DELETE | /admin/rules/{rule} | Delete global rule |
| GET | /admin/export | Export registry data |
| POST | /admin/import | Import registry data |
| GET | /admin/roleMappings/{principalId} | Return a single role mapping |
| PUT | /admin/roleMappings/{principalId} | Update a role mapping |
| DELETE | /admin/roleMappings/{principalId} | Delete a role mapping |
| GET | /admin/roleMappings | List all role mappings |
| POST | /admin/roleMappings | Create a new role mapping |
| GET | /admin/config/properties | List all configuration properties |
| GET | /admin/config/properties/{propertyName} | Get configuration property value |
| PUT | /admin/config/properties/{propertyName} | Update a configuration property |
| DELETE | /admin/config/properties/{propertyName} | Reset a configuration property |

### system
| Method | Path | Description |
|--------|------|-------------|
| GET | /system/info | Get system information |
| GET | /system/limits | Get resource limits information |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/artifacts | Search for artifacts |
| POST | /search/artifacts | Search for artifacts by content |

### groups
| Method | Path | Description |
|--------|------|-------------|
| PUT | /groups/{groupId}/artifacts/{artifactId}/state | Update artifact state |
| GET | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/meta | Get artifact version metadata |
| PUT | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/meta | Update artifact version metadata |
| DELETE | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/meta | Delete artifact version metadata |
| GET | /groups/{groupId}/artifacts/{artifactId}/versions/{version} | Get artifact version |
| DELETE | /groups/{groupId}/artifacts/{artifactId}/versions/{version} | Delete artifact version |
| PUT | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/state | Update artifact version state |
| GET | /groups/{groupId}/artifacts/{artifactId}/rules | List artifact rules |
| POST | /groups/{groupId}/artifacts/{artifactId}/rules | Create artifact rule |
| DELETE | /groups/{groupId}/artifacts/{artifactId}/rules | Delete artifact rules |
| GET | /groups/{groupId}/artifacts/{artifactId}/rules/{rule} | Get artifact rule configuration |
| PUT | /groups/{groupId}/artifacts/{artifactId}/rules/{rule} | Update artifact rule configuration |
| DELETE | /groups/{groupId}/artifacts/{artifactId}/rules/{rule} | Delete artifact rule |
| GET | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/references | Get artifact version references |
| GET | /groups/{groupId}/artifacts/{artifactId} | Get latest artifact |
| PUT | /groups/{groupId}/artifacts/{artifactId} | Update artifact |
| DELETE | /groups/{groupId}/artifacts/{artifactId} | Delete artifact |
| GET | /groups/{groupId}/artifacts | List artifacts in group |
| POST | /groups/{groupId}/artifacts | Create artifact |
| DELETE | /groups/{groupId}/artifacts | Delete artifacts in group |
| PUT | /groups/{groupId}/artifacts/{artifactId}/test | Test update artifact |
| GET | /groups/{groupId}/artifacts/{artifactId}/versions | List artifact versions |
| POST | /groups/{groupId}/artifacts/{artifactId}/versions | Create artifact version |
| GET | /groups/{groupId}/artifacts/{artifactId}/owner | Get artifact owner |
| PUT | /groups/{groupId}/artifacts/{artifactId}/owner | Update artifact owner |
| GET | /groups/{groupId} | Get a group by the specified ID. |
| DELETE | /groups/{groupId} | Delete a group by the specified ID. |
| GET | /groups | List groups |
| POST | /groups | Create a new group |
| GET | /groups/{groupId}/artifacts/{artifactId}/meta | Get artifact metadata |
| PUT | /groups/{groupId}/artifacts/{artifactId}/meta | Update artifact metadata |
| POST | /groups/{groupId}/artifacts/{artifactId}/meta | Get artifact version metadata by content |
| GET | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/comments | Get artifact version comments |
| POST | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/comments | Add new comment |
| PUT | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/comments/{commentId} | Update a comment |
| DELETE | /groups/{groupId}/artifacts/{artifactId}/versions/{version}/comments/{commentId} | Delete a single comment |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/me | Get current user |

## Enhanced Skill Content
## Question Mapping

- "What artifacts exist in the registry?" -> GET /search/artifacts
- "Show me the content of a specific artifact" -> GET /groups/{groupId}/artifacts/{artifactId}
- "How do I register a new schema or API definition?" -> POST /groups/{groupId}/artifacts
- "What versions does this artifact have?" -> GET /groups/{groupId}/artifacts/{artifactId}/versions
- "What global rules are configured?" -> GET /admin/rules
- "Who am I logged in as and what permissions do I have?" -> GET /users/me
- "How do I deprecate an artifact version?" -> PUT /groups/{groupId}/artifacts/{artifactId}/versions/{version}/state
- "What are the system limits for schema size and count?" -> GET /system/limits
- "How do I export the entire registry for backup?" -> GET /admin/export
- "How do I assign a role to a new team member?" -> POST /admin/roleMappings
- "What groups are defined in the registry?" -> GET /groups
- "How do I look up an artifact by its global ID?" -> GET /ids/globalIds/{globalId}
- "What comments exist on a specific version?" -> GET /groups/{groupId}/artifacts/{artifactId}/versions/{version}/comments
- "How do I set a compatibility rule on a single artifact?" -> POST /groups/{groupId}/artifacts/{artifactId}/rules
- "What artifact types does this registry support?" -> GET /admin/artifactTypes

## Response Tips

- **Search endpoints** (`/search/artifacts`): Responses include `count` (total matches) and `artifacts` array; use `offset`/`limit` for pagination (default 0/20). Always check `count` against array length to know if more pages exist.
- **Artifact CRUD** (`/groups/{groupId}/artifacts/*`): Successful creates/updates return full metadata including `globalId`, `contentId`, `state`, and `references` array. 409 means a conflict (duplicate ID or rule violation).
- **Rules endpoints** (`/admin/rules`, artifact rules): GET returns an array of rule type strings, not full objects. Fetch individual rules by type to get `config` and `type` detail.
- **State changes** (artifact/version state): Returns 204 with no body on success. Valid states are ENABLED, DISABLED, DEPRECATED only.
- **Role mappings**: GET individual returns `{principalId, role, principalName}`. Roles are READ_ONLY, DEVELOPER, or ADMIN.
- **System info/limits**: Flat objects with no nesting. Limit values are int64; treat -1 or 0 as "unlimited" depending on server config.
- **ID lookups** (`/ids/*`): Return raw artifact content (not JSON metadata). Use the `dereference` param on globalId to resolve `$ref` pointers inline.
- **Export/Import** (`/admin/export`, `/admin/import`): Export returns a download link object; import accepts binary ZIP body with optional header flags to preserve IDs.

## Anomaly Flags

- **Rate limit proximity**: Surface `maxRequestsPerSecondCount` from `GET /system/limits` proactively when making bulk operations; warn if planned batch size may exceed it.
- **Deprecated artifacts**: When retrieving artifact or version metadata, flag `state: "DEPRECATED"` immediately so the user knows they are working with a sunset schema.
- **Schema count approaching limits**: Compare artifact count from search results (`count`) against `maxTotalSchemasCount` and `maxArtifactsCount` from `/system/limits`; warn at 80% capacity.
- **409 Conflict on publish**: Surface the conflict reason (duplicate artifact ID, rule violation, content hash mismatch) rather than silently failing; suggest `ifExists` parameter options (FAIL, UPDATE, RETURN, RETURN_OR_UPDATE).
- **405 on version delete**: Version deletion may be disabled server-side; if 405 is returned, inform the user this is a server policy, not a client error.
- **Missing global rules**: If `GET /admin/rules` returns an empty array, proactively suggest setting COMPATIBILITY or VALIDITY rules to prevent breaking changes.
- **Unusual auth errors**: A 401 on read endpoints (which are typically open) indicates the server is running in authenticated-read mode; surface this configuration difference.

## Playbook

### 1. Register a New Schema and Set Compatibility Rules

1. Create a group if needed: `POST /groups` with `{id: "my-team"}`.
2. Publish the artifact: `POST /groups/my-team/artifacts` with the schema content in the body, setting `X-Registry-ArtifactId`, `X-Registry-ArtifactType`, and `X-Registry-Version` headers.
3. Confirm creation by checking the returned metadata (note the `globalId` and `contentId`).
4. Add a compatibility rule: `POST /groups/my-team/artifacts/{artifactId}/rules` with `{type: "COMPATIBILITY", config: "BACKWARD"}`.
5. Verify rule is active: `GET /groups/my-team/artifacts/{artifactId}/rules/{COMPATIBILITY}`.

### 2. Search, Inspect, and Download an Artifact

1. Search by name: `GET /search/artifacts?name=my-schema&limit=10`.
2. Pick the artifact from results and note its `groupId` and `id`.
3. Get full metadata: `GET /groups/{groupId}/artifacts/{artifactId}/meta`.
4. Download the content: `GET /groups/{groupId}/artifacts/{artifactId}` (optionally with `?dereference=true` to inline references).
5. List all versions if needed: `GET /groups/{groupId}/artifacts/{artifactId}/versions`.

### 3. Evolve a Schema with a New Version

1. Fetch current metadata: `GET /groups/{groupId}/artifacts/{artifactId}/meta` to see current version and state.
2. Post the new version: `POST /groups/{groupId}/artifacts/{artifactId}/versions` with updated schema in the body and `X-Registry-Version` header.
3. If a 409 is returned, the compatibility rule rejected the change; review the diff and adjust the schema.
4. Once accepted, deprecate the old version: `PUT /groups/{groupId}/artifacts/{artifactId}/versions/{oldVersion}/state` with `{state: "DEPRECATED"}`.
5. Verify the version list: `GET /groups/{groupId}/artifacts/{artifactId}/versions` to confirm ordering and states.

### 4. Export Registry and Import to Another Instance

1. Check current user permissions: `GET /users/me` (must be admin).
2. Trigger export: `GET /admin/export?forBrowser=false` to get a download link.
3. Download the ZIP file from the returned `href`.
4. On the target instance, import: `POST /admin/import` with the ZIP as the request body.
5. Optionally set `X-Registry-Preserve-GlobalId: true` and `X-Registry-Preserve-ContentId: true` headers to maintain ID continuity.

### 5. Manage Team Access with Role Mappings

1. Check existing role mappings: `GET /admin/roleMappings`.
2. Add a new developer: `POST /admin/roleMappings` with `{principalId: "jane", role: "DEVELOPER", principalName: "Jane Smith"}`.
3. Promote to admin if needed: `PUT /admin/roleMappings/jane` with `{role: "ADMIN"}`.
4. Remove access: `DELETE /admin/roleMappings/jane`.
5. Have the user verify their own role: `GET /users/me` to confirm `admin`, `developer`, or `viewer` flags.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
