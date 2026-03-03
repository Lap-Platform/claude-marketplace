---
name: updateadminclient
description: "UpdateAdminClient API skill. Use when working with UpdateAdminClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# UpdateAdminClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updates/{updateName}/updateRuns -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updates/{updateName}/updateRuns/{runName}/rerun -- create first rerun

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updates/{updateName}/updateRuns | Get the list of update runs. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updates/{updateName}/updateRuns/{runName} | Get an instance of update run using the ID. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updateRuns | Get the list of update runs. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updateRuns/{runName} | Get an instance of update run using the ID. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updates/{updateName}/updateRuns/{runName}/rerun | Resume a failed update. |

## Enhanced Skill Content
## Question Mapping

- "What update runs exist for a specific update?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updates/{updateName}/updateRuns
- "Show me the details of a particular update run" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updates/{updateName}/updateRuns/{runName}
- "List all update runs in my update location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updateRuns
- "Get a specific update run by name from an update location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updateRuns/{runName}
- "Retry a failed update run" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}/updates/{updateName}/updateRuns/{runName}/rerun
- "Did update X complete successfully?" -> GET .../updates/{updateName}/updateRuns then inspect run status fields
- "How many update runs have been triggered for my environment?" -> GET .../updateLocations/{updateLocation}/updateRuns
- "Which update runs failed and need rerunning?" -> GET .../updateRuns then filter by failure status, followed by POST .../rerun for each
- "What is the current status of run Y under update X?" -> GET .../updates/{updateName}/updateRuns/{runName}
- "Rerun a specific failed update and confirm it started" -> POST .../rerun then GET .../updateRuns/{runName} to verify new status
- "Compare update runs across different updates in the same location" -> GET .../updateLocations/{updateLocation}/updateRuns (location-wide listing)
- "Is a specific update run still in progress?" -> GET .../updateRuns/{runName} and check status/duration fields

## Response Tips

- **List endpoints (updateRuns collections):** Responses may include a `nextLink` or `value` array; always check for pagination tokens and iterate until exhausted.
- **Detail endpoints (single updateRun):** Expect nested `properties` object containing status, duration, timestamps, and progress details -- unpack `properties` before presenting to the user.
- **Rerun endpoint (POST):** A 200 response confirms the rerun was accepted; the response body may mirror the update run object with a reset status -- does not mean completion, only initiation.
- **Error responses:** Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure; surface both code and message to the user.

## Anomaly Flags

- **Failed update runs detected:** When listing runs, proactively flag any with a failed or cancelled status and suggest the rerun endpoint.
- **Repeated rerun attempts:** If a rerun is requested for a run that has already been rerun multiple times, warn the user about potential recurring failures that may need root-cause investigation.
- **Long-running updates:** Flag update runs whose duration or timestamps suggest they have been in progress unusually long -- possible stalled execution.
- **Missing required parameters:** Surface immediately if `runName`, `updateName`, or `updateLocation` are missing before making a call, since all paths are deeply nested.
- **HTTP 404 on run lookup:** May indicate the run name is misspelled or the update/location context is wrong -- suggest listing runs first to discover valid names.
- **Throttling (429) or 5xx responses:** Azure ARM applies rate limits per subscription; if encountered, surface retry-after headers and recommend backoff.

## Playbook

### 1. Investigate Update Run Status for a Specific Update

1. Call GET `.../updates/{updateName}/updateRuns` to list all runs for the target update.
2. Scan the response `value` array for the run of interest by name or timestamp.
3. If a specific run is identified, call GET `.../updates/{updateName}/updateRuns/{runName}` for full details.
4. Inspect `properties.status` and `properties.progress` to determine current state.
5. Report status, duration, and any errors back to the user.

### 2. Retry a Failed Update Run

1. Call GET `.../updates/{updateName}/updateRuns` to list runs and identify the failed one.
2. Confirm the run's status is failed or cancelled (do not rerun a successful or in-progress run).
3. Call POST `.../updates/{updateName}/updateRuns/{runName}/rerun` to trigger a retry.
4. Verify the response returns 200 and the run object shows a reset status.
5. Optionally poll GET `.../updateRuns/{runName}` to monitor progress until completion.

### 3. Audit All Update Runs Across an Update Location

1. Call GET `.../updateLocations/{updateLocation}/updateRuns` to get the full list of runs across all updates.
2. Page through results if `nextLink` is present.
3. Group runs by update name and status for a summary view.
4. Flag any failed or long-running entries for the user's attention.
5. For any flagged run, retrieve details via GET `.../updateRuns/{runName}` and present error information.

### 4. Confirm a Rerun Completed Successfully

1. After triggering POST `.../rerun`, note the `runName` from the response.
2. Wait a reasonable interval, then call GET `.../updateRuns/{runName}`.
3. Check `properties.status` -- if still in progress, report estimated progress.
4. Repeat step 2-3 until status is terminal (succeeded or failed).
5. If failed again, surface the error details and suggest investigating the underlying update or infrastructure issue.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
