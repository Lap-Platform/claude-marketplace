---
name: lexicon-schemas-api
description: "Lexicon Schemas API skill. Use when working with Lexicon Schemas for projects. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Lexicon Schemas API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /projects/{projectId}/schemas -- verify access
3. POST /projects/{projectId}/schemas -- create first schemas

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{projectId}/schemas | List Schemas |
| POST | /projects/{projectId}/schemas | Create/Replace Multiple |
| DELETE | /projects/{projectId}/schemas | Delete all Schemas |
| GET | /projects/{projectId}/schemas/{entityType} | List for Entity |
| DELETE | /projects/{projectId}/schemas/{entityType} | Delete for Entity |
| GET | /projects/{projectId}/schemas/{entityType}/{name} | List for Entity and Name |
| DELETE | /projects/{projectId}/schemas/{entityType}/{name} | Delete for Entity and Name |
| POST | /projects/{projectId}/schemas/{entityType}/{name} | Create/Replace One |

## Enhanced Skill Content
## Question Mapping

- "What schemas exist in my project?" -> GET /projects/{projectId}/schemas
- "List all event schemas for this project" -> GET /projects/{projectId}/schemas/{entityType}
- "Show me the schema definition for a specific event" -> GET /projects/{projectId}/schemas/{entityType}/{name}
- "How do I add new schemas to my project?" -> POST /projects/{projectId}/schemas
- "Can I replace all schemas at once?" -> POST /projects/{projectId}/schemas (with `truncate: true`)
- "How do I update a schema's description or properties?" -> POST /projects/{projectId}/schemas/{entityType}/{name}
- "Delete all schemas in my project" -> DELETE /projects/{projectId}/schemas
- "Remove all schemas of a specific entity type" -> DELETE /projects/{projectId}/schemas/{entityType}
- "Delete a single named schema" -> DELETE /projects/{projectId}/schemas/{entityType}/{name}
- "How many schemas were added or removed after a bulk update?" -> POST /projects/{projectId}/schemas (check `results.added` and `results.deleted`)
- "What tags and contacts are set on a schema?" -> GET /projects/{projectId}/schemas/{entityType}/{name} (inspect `metadata.com.mixpanel`)
- "How do I hide a schema from the UI?" -> POST /projects/{projectId}/schemas/{entityType}/{name} (set `metadata.com.mixpanel.hidden: true`)
- "How do I mark a schema as dropped?" -> POST /projects/{projectId}/schemas/{entityType}/{name} (set `metadata.com.mixpanel.dropped: true`)

## Response Tips

- **List endpoints** (GET /schemas, GET /schemas/{entityType}): Results are returned as flat arrays in `results`; no pagination -- expect the full set in one response.
- **Detail endpoint** (GET /schemas/{entityType}/{name}): Returns the schema body directly (description, properties, metadata) without a wrapper object.
- **Bulk create** (POST /schemas): Returns `results.added` and `results.deleted` counts; when `truncate: true`, `deleted` reflects schemas removed before insertion.
- **Delete endpoints**: All return `results.delete_count` indicating how many schemas were removed; a `0` count is valid (nothing matched).
- **Update endpoint** (POST /schemas/{entityType}/{name}): Returns only `{status: str}` with no echo of the updated schema; re-fetch to confirm changes.
- **Errors**: 401 means missing or invalid auth; 403 means the token lacks permission for this project. The single-schema POST also returns 400 for malformed payloads.

## Anomaly Flags

- **403 on previously accessible project**: The API key's project permissions may have changed -- surface immediately and suggest verifying project access.
- **Bulk POST with high `deleted` count**: If `truncate: true` was used and `results.deleted` is large, warn the user that existing schemas were purged before insertion.
- **Delete returning `delete_count: 0`**: The target schema or entity type may not exist or was already removed -- flag as a no-op to avoid silent failures.
- **400 on single-schema POST**: Only this endpoint returns 400; likely indicates malformed `properties`, `metadata`, or an invalid schema structure -- surface the response body for debugging.
- **`dropped: true` or `hidden: true` in metadata**: When reading schemas, proactively note any that are marked dropped or hidden, as these are suppressed in Mixpanel's UI and may indicate deprecated data.
- **Missing `metadata.com.mixpanel` block**: If a schema lacks the Mixpanel metadata namespace, it may be an externally created or incomplete schema -- flag for review.

## Playbook

### 1. Audit all schemas in a project

1. GET /projects/{projectId}/schemas to retrieve every schema across all entity types.
2. Group results by `entityType` to understand coverage.
3. For each schema of interest, GET /projects/{projectId}/schemas/{entityType}/{name} to inspect full metadata including tags, contacts, and hidden/dropped status.
4. Flag any schemas where `dropped: true` or `hidden: true` for cleanup consideration.

### 2. Bulk replace schemas (full sync)

1. Prepare an `entries` array with all desired schemas, each containing `entityType`, `name`, and `schemaJson` (with description, properties, metadata).
2. POST /projects/{projectId}/schemas with `truncate: true` to remove all existing schemas and replace with the new set.
3. Check `results.added` and `results.deleted` to confirm the expected counts.
4. GET /projects/{projectId}/schemas to verify the final state.

### 3. Update metadata on a single schema

1. GET /projects/{projectId}/schemas/{entityType}/{name} to fetch the current schema definition.
2. Modify the desired fields (e.g., set `metadata.com.mixpanel.tags`, update `description`, toggle `hidden`).
3. POST /projects/{projectId}/schemas/{entityType}/{name} with only the changed fields.
4. GET the same schema again to confirm the update took effect (the POST response only returns status).

### 4. Clean up a specific entity type

1. GET /projects/{projectId}/schemas/{entityType} to list all schemas under that entity type.
2. Review each schema name and decide which to keep.
3. To remove all at once: DELETE /projects/{projectId}/schemas/{entityType} and verify `delete_count`.
4. To selectively remove: DELETE /projects/{projectId}/schemas/{entityType}/{name} for each unwanted schema.
5. GET /projects/{projectId}/schemas/{entityType} to confirm only desired schemas remain.

### 5. Incrementally add schemas without disrupting existing ones

1. GET /projects/{projectId}/schemas to snapshot current state and note existing entity types and names.
2. Build an `entries` array containing only the new schemas to add.
3. POST /projects/{projectId}/schemas with `truncate` omitted or set to `false` (default).
4. Verify `results.added` matches the number of entries submitted and `results.deleted` is `0`.
5. GET /projects/{projectId}/schemas to confirm old schemas are intact alongside the new additions.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
