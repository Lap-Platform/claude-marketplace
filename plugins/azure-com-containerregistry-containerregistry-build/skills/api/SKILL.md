---
name: containerregistrymanagementclient
description: "ContainerRegistryManagementClient API skill. Use when working with ContainerRegistryManagementClient for subscriptions. Covers 25 endpoints."
version: 1.0.0
generator: lapsh
---

# ContainerRegistryManagementClient
API version: 2019-06-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com/

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName}/listQueueStatus -- create first listQueueStatus

## Endpoints

25 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName} | Gets the detailed information for a given agent pool. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName} | Creates an agent pool for a container registry with the specified parameters. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName} | Deletes a specified agent pool resource. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName} | Updates an agent pool with the specified parameters. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools | Lists all the agent pools for a specified container registry. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName}/listQueueStatus | Gets the count of queued runs for a given agent pool. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scheduleRun | Schedules a new run based on the request parameters and add it to the run queue. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/listBuildSourceUploadUrl | Get the upload location for the user to be able to upload the source. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/runs | Gets all the runs for a registry. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/runs/{runId} | Gets the detailed information for a given run. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/runs/{runId} | Patch the run properties. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/runs/{runId}/listLogSasUrl | Gets a link to download the run logs. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/runs/{runId}/cancel | Cancel an existing run. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/taskRuns/{taskRunName} | Gets the detailed information for a given task run. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/taskRuns/{taskRunName} | Creates a task run for a container registry with the specified parameters. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/taskRuns/{taskRunName} | Deletes a specified task run resource. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/taskRuns/{taskRunName} | Updates a task run with the specified parameters. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/taskRuns/{taskRunName}/listDetails | Gets the detailed information for a given task run that includes all secrets. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/taskRuns | Lists all the task runs for a specified container registry. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks | Lists all the tasks for a specified container registry. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName} | Get the properties of a specified task. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName} | Creates a task for a container registry with the specified parameters. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName} | Deletes a specified task. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName} | Updates a task with the specified parameters. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName}/listDetails | Returns a task with extended information that includes all secrets. |

## Enhanced Skill Content
## Question Mapping

- "How do I get details about a specific agent pool in my container registry?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName}
- "How do I create or update an agent pool for builds?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName}
- "How do I list all agent pools in my registry?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools
- "How do I check the queue status of an agent pool?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/agentPools/{agentPoolName}/listQueueStatus
- "How do I trigger a container image build?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/scheduleRun
- "How do I get an upload URL for build source code?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/listBuildSourceUploadUrl
- "How do I list all build runs, optionally filtered?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/runs
- "How do I cancel a running build?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/runs/{runId}/cancel
- "How do I get the logs for a specific build run?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/runs/{runId}/listLogSasUrl
- "How do I create a recurring build task?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName}
- "How do I list all tasks defined on my registry?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks
- "How do I see the full details of a task including secrets?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName}/listDetails
- "How do I run a one-off task run?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/taskRuns/{taskRunName}
- "How do I delete a task I no longer need?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName}
- "How do I update the configuration of an existing task?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ContainerRegistry/registries/{registryName}/tasks/{taskName}

## Response Tips

- **Agent Pools (GET/PUT/PATCH):** Response includes provisioning state nested under `properties`; check `properties.provisioningState` for `Succeeded`, `Creating`, or `Failed` before assuming readiness.
- **Runs (GET list):** Supports OData `$filter` and `$top` for pagination; results include a `nextLink` property for cursor-based pagination -- follow it until null.
- **Runs (POST scheduleRun, cancel):** 202 means the operation was accepted but not completed; poll the run resource or use the `Azure-AsyncOperation` header URL to track progress.
- **Delete operations (agent pools, tasks, taskRuns):** 200 = deleted synchronously, 202 = deletion in progress (poll), 204 = resource already gone -- all three are success cases.
- **PUT (create/update):** 200 = updated existing resource, 201 = created new resource; both return the full resource body.
- **listLogSasUrl / listBuildSourceUploadUrl:** Returns a temporary SAS URL with expiry; extract `logLink` or `uploadUrl` and use before the token expires.
- **listDetails (tasks, taskRuns):** Returns sensitive fields (credentials, source triggers) omitted from standard GET; treat response data accordingly.

## Anomaly Flags

- **Provisioning stuck:** Surface a warning if an agent pool, task, or task run stays in `Creating` or `Updating` provisioning state for more than 10 minutes after a PUT/PATCH.
- **202 without completion:** If a scheduleRun, cancel, or delete returns 202, proactively remind the caller to poll for completion and provide the async operation URL from response headers.
- **Queue saturation:** After calling listQueueStatus, flag if the queued count exceeds the agent pool's configured count, indicating builds will be delayed.
- **SAS URL expiry:** When retrieving log or upload SAS URLs, warn that these are time-limited and should be consumed immediately.
- **Empty run list with filters:** If a filtered GET /runs returns zero results, suggest verifying the OData filter syntax -- malformed filters silently return empty rather than erroring.
- **Task with no recent runs:** When viewing a task, cross-reference with runs list; flag tasks that have not executed in an unexpectedly long period (possible trigger misconfiguration).
- **Deprecated API version:** The spec uses `2019-06-01-preview` -- surface a notice that this is a preview API version and recommend checking for GA releases.

## Playbook

### 1. Build and Monitor a Container Image

1. Call POST `.../listBuildSourceUploadUrl` to get a temporary upload URL.
2. Upload your build context (source archive) to the returned URL using an HTTP PUT.
3. Call POST `.../scheduleRun` with a `runRequest` body specifying the uploaded source location, Dockerfile path, and target image tags.
4. Note the `runId` from the response (or 202 async operation).
5. Poll GET `.../runs/{runId}` until `status` reaches `Succeeded` or `Failed`.
6. Call POST `.../runs/{runId}/listLogSasUrl` to retrieve build logs and review output.

### 2. Set Up a Recurring Build Task

1. Call GET `.../tasks` to see existing tasks and avoid naming conflicts.
2. Call PUT `.../tasks/{taskName}` with `taskCreateParameters` including the source trigger (e.g., git commit), platform, Dockerfile step, and credentials.
3. Confirm the response is 201 (created) and `provisioningState` is `Succeeded`.
4. Call POST `.../tasks/{taskName}/listDetails` to verify trigger configuration and credentials are set correctly.
5. Optionally, call POST `.../scheduleRun` referencing the task to trigger an immediate test run.

### 3. Scale Agent Pools for High Build Demand

1. Call GET `.../agentPools` to list current pools and their sizes.
2. Call POST `.../agentPools/{agentPoolName}/listQueueStatus` on busy pools to check queue depth.
3. If queued builds exceed pool capacity, call PATCH `.../agentPools/{agentPoolName}` with `updateParameters` to increase the `count` value.
4. Poll GET `.../agentPools/{agentPoolName}` until `provisioningState` returns to `Succeeded`.
5. Re-check queue status to confirm builds are draining.

### 4. Cancel a Failed or Stuck Build Run

1. Call GET `.../runs` with `$filter=status eq 'Running'` and `$top=10` to find active runs.
2. Identify the target run and call POST `.../runs/{runId}/cancel`.
3. If the response is 202, poll GET `.../runs/{runId}` until `status` changes to `Canceled`.
4. Call POST `.../runs/{runId}/listLogSasUrl` to fetch partial logs for debugging.

### 5. Clean Up Unused Task Runs and Tasks

1. Call GET `.../taskRuns` to list all task runs.
2. For each completed or failed task run to remove, call DELETE `.../taskRuns/{taskRunName}`.
3. Handle 204 responses gracefully (already deleted).
4. Call GET `.../tasks` and identify tasks no longer needed.
5. Call DELETE `.../tasks/{taskName}` for each, and poll if 202 is returned until deletion completes.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
