---
name: streamanalyticsmanagementclient
description: "StreamAnalyticsManagementClient API skill. Use when working with StreamAnalyticsManagementClient for providers, subscriptions. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# StreamAnalyticsManagementClient
API version: 2016-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.StreamAnalytics/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/start -- create first start

## Endpoints

9 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.StreamAnalytics/operations | Lists all of the available Stream Analytics related operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName} | Creates a streaming job or replaces an already existing streaming job. |
| PATCH | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName} | Updates an existing streaming job. This can be used to partially update (ie. update one or two properties) a streaming job without affecting the rest the job definition. |
| DELETE | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName} | Deletes a streaming job. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName} | Gets details about the specified streaming job. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs | Lists all of the streaming jobs in the specified resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/streamingjobs | Lists all of the streaming jobs in the given subscription. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/start | Starts a streaming job. Once a job is started it will start processing input events and produce output. |
| POST | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/stop | Stops a running streaming job. This will cause a running streaming job to stop processing input events and producing output. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Stream Analytics?" -> GET /providers/Microsoft.StreamAnalytics/operations
- "How do I create a new streaming job?" -> PUT /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}
- "How do I update an existing streaming job?" -> PATCH /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}
- "How do I delete a streaming job?" -> DELETE /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}
- "Get details of a specific streaming job" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}
- "List all streaming jobs in a resource group" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs
- "List all streaming jobs in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/streamingjobs
- "How do I start a streaming job?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/start
- "How do I stop a streaming job?" -> POST /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}/stop
- "Can I create a job only if it doesn't already exist?" -> PUT .../streamingjobs/{jobName} (use `If-None-Match: *` header)
- "How do I safely update a job without overwriting concurrent changes?" -> PATCH .../streamingjobs/{jobName} (use `If-Match` header with ETag)
- "How do I expand job details to include inputs, outputs, and functions?" -> GET .../streamingjobs/{jobName} (use `$expand` query parameter)
- "What streaming jobs are running across all my resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/streamingjobs

## Response Tips

- **Operations (providers):** Returns a flat list of available provider operations; no pagination.
- **Create/PUT:** 200 means the job was updated in place; 201 means a new job was created -- check the status code to distinguish.
- **Update/PATCH:** Always returns 200; response body contains the merged job definition with server-side defaults applied.
- **Delete:** 200 means deleted immediately, 202 means deletion is in progress (async), 204 means the job did not exist -- all are success cases.
- **Get single job:** Use `$expand` to inline nested resources (inputs, outputs, transformation, functions); without it you get summary metadata only.
- **List jobs:** Returns an array in `value`; paginate via `nextLink` if present. Supports `$expand` for bulk detail retrieval.
- **Start/Stop:** 200 means the action completed synchronously; 202 means it was accepted and is running asynchronously -- poll the job status to confirm completion.

## Anomaly Flags

- **202 Accepted on start/stop/delete:** The operation is async. Surface this and recommend polling the job's `provisioningState` until it reaches a terminal state.
- **ETag mismatch (412 Precondition Failed):** If `If-Match` is used and the job was modified concurrently, surface the conflict and suggest re-fetching before retrying.
- **Job state inconsistencies:** If a job shows `provisioningState: Failed` or `jobState` does not transition after start/stop, flag for investigation.
- **204 on delete:** The job was already gone. Surface this if the caller expected the job to exist.
- **Missing `$expand` on detail requests:** If the user asks about inputs/outputs but the response lacks them, suggest re-requesting with `$expand`.
- **API version drift:** The spec uses `2016-03-01`. Flag if Azure documentation references a newer api-version with additional fields or breaking changes.
- **Rate limiting (429):** Azure ARM APIs enforce per-subscription throttling. Surface retry-after headers and recommend exponential backoff.

## Playbook

### 1. Create and Start a New Streaming Job

1. Call PUT `/subscriptions/{sub}/resourcegroups/{rg}/providers/Microsoft.StreamAnalytics/streamingjobs/{jobName}` with the full job definition in `streamingJob` body.
2. Confirm a 201 response (created) or 200 (updated existing).
3. Call POST `.../streamingjobs/{jobName}/start` with optional `startJobParameters` (e.g., custom start time).
4. If 202 is returned, poll GET `.../streamingjobs/{jobName}` until `jobState` is `Running`.

### 2. Safely Update a Running Job

1. Call GET `.../streamingjobs/{jobName}` to retrieve the current definition and its `ETag` header.
2. Modify the desired properties in the response body.
3. Call PATCH `.../streamingjobs/{jobName}` with the changes, setting `If-Match` to the retrieved ETag.
4. If 200 is returned, the update succeeded. If 412, re-fetch and retry.

### 3. Stop and Delete a Job

1. Call POST `.../streamingjobs/{jobName}/stop`.
2. If 202 is returned, poll GET `.../streamingjobs/{jobName}` until `jobState` is `Stopped`.
3. Call DELETE `.../streamingjobs/{jobName}`.
4. Confirm 200 (deleted) or 202 (deletion in progress). A 204 means it was already removed.

### 4. Inventory All Streaming Jobs Across a Subscription

1. Call GET `/subscriptions/{sub}/providers/Microsoft.StreamAnalytics/streamingjobs` with `$expand` to get full details.
2. Collect results from the `value` array.
3. If `nextLink` is present, follow it to retrieve the next page. Repeat until no `nextLink`.
4. Group results by `resourceGroup` extracted from each job's `id` field for a per-group summary.

### 5. Conditional Job Creation (Create-If-Not-Exists)

1. Call PUT `.../streamingjobs/{jobName}` with `If-None-Match: *` header and the full job definition.
2. If 201 is returned, the job was created successfully.
3. If a 412 or 200 is returned, a job with that name already exists -- decide whether to update or abort.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
