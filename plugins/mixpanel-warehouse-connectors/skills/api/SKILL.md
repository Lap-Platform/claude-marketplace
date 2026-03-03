---
name: warehouse-connectors-api
description: "Warehouse Connectors API skill. Use when working with Warehouse Connectors for projects. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# Warehouse Connectors API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /projects/{projectId}/warehouse-sources/imports -- verify access
3. POST /projects/{projectId}/warehouse-sources/imports/event-stream -- create first event-stream

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{projectId}/warehouse-sources/imports | List all warehouse imports |
| GET | /projects/{projectId}/warehouse-sources/imports/{importId} | Get a specific warehouse import |
| PATCH | /projects/{projectId}/warehouse-sources/imports/{importId} | Update a warehouse import |
| DELETE | /projects/{projectId}/warehouse-sources/imports/{importId} | Delete a warehouse import |
| POST | /projects/{projectId}/warehouse-sources/imports/event-stream | Create an event stream import |
| POST | /projects/{projectId}/warehouse-sources/imports/people | Create a people (user profiles) import |
| POST | /projects/{projectId}/warehouse-sources/imports/groups | Create a groups import |
| POST | /projects/{projectId}/warehouse-sources/imports/lookup-table | Create a lookup table import |
| PUT | /projects/{projectId}/warehouse-sources/imports/{importId}/manual-sync | Run an import |
| GET | /projects/{projectId}/warehouse-sources/imports/{importId}/history | Get import job history |

## Enhanced Skill Content
## Question Mapping

- "What warehouse imports are configured for my project?" -> GET /projects/{projectId}/warehouse-sources/imports
- "Show me the details of a specific import job" -> GET /projects/{projectId}/warehouse-sources/imports/{importId}
- "How do I pause a warehouse import?" -> PATCH /projects/{projectId}/warehouse-sources/imports/{importId}
- "How do I change the sync frequency of an import?" -> PATCH /projects/{projectId}/warehouse-sources/imports/{importId}
- "How do I delete a warehouse import and its data?" -> DELETE /projects/{projectId}/warehouse-sources/imports/{importId}
- "How do I set up event streaming from my warehouse?" -> POST /projects/{projectId}/warehouse-sources/imports/event-stream
- "How do I import user profiles from a warehouse table?" -> POST /projects/{projectId}/warehouse-sources/imports/people
- "How do I import group data from my warehouse?" -> POST /projects/{projectId}/warehouse-sources/imports/groups
- "How do I create a lookup table import from my warehouse?" -> POST /projects/{projectId}/warehouse-sources/imports/lookup-table
- "How do I trigger a manual sync for an existing import?" -> PUT /projects/{projectId}/warehouse-sources/imports/{importId}/manual-sync
- "What is the run history for a warehouse import?" -> GET /projects/{projectId}/warehouse-sources/imports/{importId}/history
- "How do I set up a one-time full sync from my warehouse?" -> POST /projects/{projectId}/warehouse-sources/imports/event-stream (with sync_mode=one_time)
- "How do I configure Databricks cluster settings for an import?" -> PATCH /projects/{projectId}/warehouse-sources/imports/{importId}
- "How do I delete an import but keep the data already imported?" -> DELETE /projects/{projectId}/warehouse-sources/imports/{importId} (with delete_data=false)

## Response Tips

- **List/detail endpoints (GET):** Responses wrap data in `results` (array for lists, object for detail). Always check the top-level `status` field before reading `results`.
- **Create endpoints (POST):** Returns the created import config in `results`. A 400 means invalid parameters -- check `sync_mode` enum values and required fields per import type.
- **Update endpoint (PATCH):** Returns the updated import in `results`. Only `paused` and `run_every` are patchable; other fields require delete and recreate.
- **Delete endpoint (DELETE):** Returns only `status` with no `results`. The `delete_data` flag defaults to `false`, so imported data is retained unless explicitly removed.
- **History endpoint (GET):** Results are nested under `results.runs` as an array of run objects -- iterate over `runs`, not `results` directly.
- **Manual sync (PUT):** Returns only `status`. No body required. A 404 means the import ID is invalid or belongs to another project.

## Anomaly Flags

- **401/403 on any endpoint:** Surface immediately -- likely an expired or missing auth token, or insufficient project permissions. Distinguish between authentication failure (401) and authorization failure (403).
- **404 on import operations:** The import may have been deleted by another user or process. Suggest re-listing all imports to confirm current state.
- **`run_every` set to 0:** This means the import schedule is disabled (manual-only). Flag if the user may have intended a recurring schedule.
- **`paused: true` on an import:** Proactively mention when listing imports so users are aware data is not flowing.
- **`sync_mode: one_time` with `run_every` set:** Contradictory configuration -- a one-time sync with a recurring schedule. Warn the user.
- **`delete_data: true` on DELETE:** High-impact destructive action. Always confirm with the user before proceeding.
- **Databricks cluster config present:** Complex nested object with cloud-specific attributes (AWS/Azure/GCP). Flag if multiple cloud attribute blocks are provided simultaneously, as only one should apply.

## Playbook

### 1. Set Up a New Event Stream Import

1. Identify the `projectId` and `warehouse_source_id` for your connection.
2. Call `POST /projects/{projectId}/warehouse-sources/imports/event-stream` with required fields: `import_type`, `warehouse_source_id`, `table_params`, `time_column_name`, and `sync_mode`.
3. Set `run_every` to the desired interval (3600000000000 for hourly, 86400000000000 for daily, 604800000000000 for weekly) or 0 for manual-only.
4. Optionally map columns with `event_column_name`, `user_column_name`, and `property_mappings`.
5. Verify creation by calling `GET /projects/{projectId}/warehouse-sources/imports/{importId}` with the returned import ID.
6. Trigger the first sync immediately with `PUT /projects/{projectId}/warehouse-sources/imports/{importId}/manual-sync`.

### 2. Pause, Modify, and Resume an Import

1. List all imports with `GET /projects/{projectId}/warehouse-sources/imports` and locate the target import ID.
2. Pause the import: `PATCH /projects/{projectId}/warehouse-sources/imports/{importId}` with `{ "paused": true }`.
3. Modify the schedule: `PATCH /projects/{projectId}/warehouse-sources/imports/{importId}` with `{ "run_every": <new_interval>, "paused": false }`.
4. Confirm changes with `GET /projects/{projectId}/warehouse-sources/imports/{importId}`.

### 3. Investigate a Failing Import

1. Get import details: `GET /projects/{projectId}/warehouse-sources/imports/{importId}`.
2. Pull run history: `GET /projects/{projectId}/warehouse-sources/imports/{importId}/history`.
3. Inspect the `results.runs` array for recent failures -- look at status fields and error messages in each run entry.
4. If the issue is resolved, trigger a manual re-sync: `PUT /projects/{projectId}/warehouse-sources/imports/{importId}/manual-sync`.
5. Re-check history after the sync completes to confirm success.

### 4. Clean Up an Unused Import

1. List all imports: `GET /projects/{projectId}/warehouse-sources/imports` and identify the target.
2. Check run history: `GET /projects/{projectId}/warehouse-sources/imports/{importId}/history` to confirm it is no longer needed.
3. Decide whether to keep imported data: call `DELETE /projects/{projectId}/warehouse-sources/imports/{importId}` with `delete_data=false` to keep data, or `delete_data=true` to remove everything.
4. Verify removal by re-listing imports.

### 5. Import People, Groups, and a Lookup Table for a Full Profile Setup

1. Create a people import: `POST /projects/{projectId}/warehouse-sources/imports/people` with `user_column_name`, `table_params`, `sync_mode`, and `warehouse_source_id`.
2. Create a groups import: `POST /projects/{projectId}/warehouse-sources/imports/groups` with `group_key`, `group_id_column`, `table_params`, `sync_mode`, and `warehouse_source_id`.
3. Create a lookup table import: `POST /projects/{projectId}/warehouse-sources/imports/lookup-table` with `mixpanel_property` (containing `value` and `resourceType`), `property_key_column_name`, and `sync_mode` (only `full_sync` or `one_time`).
4. Trigger manual syncs for all three using `PUT /projects/{projectId}/warehouse-sources/imports/{importId}/manual-sync`.
5. Monitor each with `GET /projects/{projectId}/warehouse-sources/imports/{importId}/history` to confirm successful runs.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
