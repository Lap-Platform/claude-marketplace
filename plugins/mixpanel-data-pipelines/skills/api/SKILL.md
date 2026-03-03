---
name: data-pipelines-api
description: "Data Pipelines API skill. Use when working with Data Pipelines for nessie. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Data Pipelines API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /nessie/pipeline/jobs -- verify access
3. POST /nessie/pipeline/create -- create first create

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### nessie
| Method | Path | Description |
|--------|------|-------------|
| GET | /nessie/pipeline/jobs | List Pipelines |
| POST | /nessie/pipeline/create | Create Pipeline |
| POST | /nessie/pipeline/edit | Edit Pipeline |
| POST | /nessie/pipeline/cancel | Delete Pipeline |
| POST | /nessie/pipeline/pause | Pause Pipeline |
| POST | /nessie/pipeline/resume | Resume Pipeline |
| GET | /nessie/pipeline/status | Get Pipeline |
| GET | /nessie/pipeline/timeline | List Pipeline Logs |

## Enhanced Skill Content
## Question Mapping

- "What pipelines are running right now?" -> GET /nessie/pipeline/jobs
- "Show me all pipeline jobs" -> GET /nessie/pipeline/jobs
- "Create a new data pipeline" -> POST /nessie/pipeline/create
- "Set up a pipeline to process this data" -> POST /nessie/pipeline/create
- "Update an existing pipeline configuration" -> POST /nessie/pipeline/edit
- "Change the settings on my pipeline" -> POST /nessie/pipeline/edit
- "Stop a running pipeline" -> POST /nessie/pipeline/cancel
- "Cancel the current pipeline execution" -> POST /nessie/pipeline/cancel
- "Pause a pipeline temporarily" -> POST /nessie/pipeline/pause
- "Resume a paused pipeline" -> POST /nessie/pipeline/resume
- "What is the status of my pipeline?" -> GET /nessie/pipeline/status
- "Show me which jobs succeeded or failed" -> GET /nessie/pipeline/status
- "How many jobs were canceled or retried?" -> GET /nessie/pipeline/status
- "Show me the pipeline execution timeline" -> GET /nessie/pipeline/timeline
- "When did my pipeline jobs run over the past week?" -> GET /nessie/pipeline/timeline

## Response Tips

- **Jobs & listing** (`GET /jobs`): Returns a list of pipeline job objects. Expect an array at the top level; filter client-side if no query params are supported.
- **Mutations** (`POST /create`, `/edit`, `/cancel`, `/pause`, `/resume`): Return 200 on success. Check for 404 on pause/resume -- the pipeline may not exist or may already be in the target state.
- **Status** (`GET /status`): Response contains three arrays -- `canceled`, `retried`, `succeeded` -- each holding map objects. Use the `status` filter param (accepts a list) to narrow results. The `name` param is required.
- **Timeline** (`GET /timeline`): Optional `name` filter. Without it, returns timeline data across all pipelines.
- **Errors**: 401 means missing or invalid auth. 403 means authenticated but insufficient permissions. 404 (only on pause/resume) means the pipeline was not found.

## Anomaly Flags

- **Repeated 403 errors**: User may lack the required role or scope. Surface permission requirements proactively.
- **404 on pause/resume**: Pipeline may have been deleted or never existed. Confirm the pipeline name with a status check before retrying.
- **High canceled/retried counts**: When `GET /status` returns many entries in `canceled` or `retried` arrays, flag potential pipeline instability to the user.
- **Missing auth (401)**: Surface immediately -- all endpoints require authentication. Prompt the user to provide or refresh credentials.
- **Silent 200 on mutations**: Create, edit, cancel, pause, and resume return 200 with minimal detail. If the user expects confirmation, follow up with `GET /status` to verify the change took effect.

## Playbook

### 1. Create and Monitor a New Pipeline

1. `POST /nessie/pipeline/create` with the pipeline configuration
2. `GET /nessie/pipeline/status` with the pipeline `name` to confirm it is running
3. `GET /nessie/pipeline/timeline` with `name` to watch execution progress
4. Check `succeeded`, `canceled`, and `retried` arrays in the status response to assess health

### 2. Pause, Modify, and Resume a Pipeline

1. `POST /nessie/pipeline/pause` to pause the target pipeline
2. Confirm pause with `GET /nessie/pipeline/status` (expect no new entries in `succeeded`)
3. `POST /nessie/pipeline/edit` to apply configuration changes
4. `POST /nessie/pipeline/resume` to restart execution
5. `GET /nessie/pipeline/status` to verify jobs are processing again

### 3. Investigate a Failing Pipeline

1. `GET /nessie/pipeline/status` with `name` and `status` filter to isolate `canceled` or `retried` jobs
2. Review the `retried` array for recurring failure patterns
3. `GET /nessie/pipeline/timeline` with `name` to identify when failures started
4. If unstable, `POST /nessie/pipeline/cancel` to stop the pipeline, then `POST /nessie/pipeline/edit` to fix the config before restarting

### 4. Audit All Pipeline Activity

1. `GET /nessie/pipeline/jobs` to list all known pipelines
2. For each pipeline, `GET /nessie/pipeline/status` with its `name` to collect job outcomes
3. `GET /nessie/pipeline/timeline` (no name filter) for a cross-pipeline view of execution history
4. Aggregate `succeeded`, `canceled`, and `retried` counts to build a health summary


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
