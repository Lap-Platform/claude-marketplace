---
name: batchservice
description: "BatchService API skill. Use when working with BatchService for applications, poolusagemetrics, supportedimages. Covers 76 endpoints."
version: 1.0.0
generator: lapsh
---

# BatchService
API version: 2019-08-01.10.0

## Auth
OAuth2 | ApiKey Authorization in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /applications -- verify access
3. POST /certificates -- create first certificates

## Endpoints

76 endpoints across 11 groups. See references/api-spec.lap for full details.

### applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /applications | Lists all of the applications available in the specified Account. |
| GET | /applications/{applicationId} | Gets information about the specified Application. |

### poolusagemetrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /poolusagemetrics | Lists the usage metrics, aggregated by Pool across individual time intervals, for the specified Account. |

### supportedimages
| Method | Path | Description |
|--------|------|-------------|
| GET | /supportedimages | Lists all Virtual Machine Images supported by the Azure Batch service. |

### nodecounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /nodecounts | Gets the number of Compute Nodes in each state, grouped by Pool. |

### lifetimepoolstats
| Method | Path | Description |
|--------|------|-------------|
| GET | /lifetimepoolstats | Gets lifetime summary statistics for all of the Pools in the specified Account. |

### lifetimejobstats
| Method | Path | Description |
|--------|------|-------------|
| GET | /lifetimejobstats | Gets lifetime summary statistics for all of the Jobs in the specified Account. |

### certificates
| Method | Path | Description |
|--------|------|-------------|
| POST | /certificates | Adds a Certificate to the specified Account. |
| GET | /certificates | Lists all of the Certificates that have been added to the specified Account. |

### certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint})
| Method | Path | Description |
|--------|------|-------------|
| POST | /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint})/canceldelete | Cancels a failed deletion of a Certificate from the specified Account. |
| DELETE | /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint}) | Deletes a Certificate from the specified Account. |
| GET | /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint}) | Gets information about the specified Certificate. |

### jobs
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /jobs/{jobId}/tasks/{taskId}/files/{filePath} | Deletes the specified Task file from the Compute Node where the Task ran. |
| GET | /jobs/{jobId}/tasks/{taskId}/files/{filePath} | Returns the content of the specified Task file. |
| HEAD | /jobs/{jobId}/tasks/{taskId}/files/{filePath} | Gets the properties of the specified Task file. |
| GET | /jobs/{jobId}/tasks/{taskId}/files | Lists the files in a Task's directory on its Compute Node. |
| DELETE | /jobs/{jobId} | Deletes a Job. |
| GET | /jobs/{jobId} | Gets information about the specified Job. |
| PATCH | /jobs/{jobId} | Updates the properties of the specified Job. |
| PUT | /jobs/{jobId} | Updates the properties of the specified Job. |
| POST | /jobs/{jobId}/disable | Disables the specified Job, preventing new Tasks from running. |
| POST | /jobs/{jobId}/enable | Enables the specified Job, allowing new Tasks to run. |
| POST | /jobs/{jobId}/terminate | Terminates the specified Job, marking it as completed. |
| POST | /jobs | Adds a Job to the specified Account. |
| GET | /jobs | Lists all of the Jobs in the specified Account. |
| GET | /jobs/{jobId}/jobpreparationandreleasetaskstatus | Lists the execution status of the Job Preparation and Job Release Task for the specified Job across the Compute Nodes where the Job has run. |
| GET | /jobs/{jobId}/taskcounts | Gets the Task counts for the specified Job. |
| POST | /jobs/{jobId}/tasks | Adds a Task to the specified Job. |
| GET | /jobs/{jobId}/tasks | Lists all of the Tasks that are associated with the specified Job. |
| POST | /jobs/{jobId}/addtaskcollection | Adds a collection of Tasks to the specified Job. |
| DELETE | /jobs/{jobId}/tasks/{taskId} | Deletes a Task from the specified Job. |
| GET | /jobs/{jobId}/tasks/{taskId} | Gets information about the specified Task. |
| PUT | /jobs/{jobId}/tasks/{taskId} | Updates the properties of the specified Task. |
| GET | /jobs/{jobId}/tasks/{taskId}/subtasksinfo | Lists all of the subtasks that are associated with the specified multi-instance Task. |
| POST | /jobs/{jobId}/tasks/{taskId}/terminate | Terminates the specified Task. |
| POST | /jobs/{jobId}/tasks/{taskId}/reactivate | Reactivates a Task, allowing it to run again even if its retry count has been exhausted. |

### pools
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /pools/{poolId}/nodes/{nodeId}/files/{filePath} | Deletes the specified file from the Compute Node. |
| GET | /pools/{poolId}/nodes/{nodeId}/files/{filePath} | Returns the content of the specified Compute Node file. |
| HEAD | /pools/{poolId}/nodes/{nodeId}/files/{filePath} | Gets the properties of the specified Compute Node file. |
| GET | /pools/{poolId}/nodes/{nodeId}/files | Lists all of the files in Task directories on the specified Compute Node. |
| POST | /pools | Adds a Pool to the specified Account. |
| GET | /pools | Lists all of the Pools in the specified Account. |
| DELETE | /pools/{poolId} | Deletes a Pool from the specified Account. |
| HEAD | /pools/{poolId} | Gets basic properties of a Pool. |
| GET | /pools/{poolId} | Gets information about the specified Pool. |
| PATCH | /pools/{poolId} | Updates the properties of the specified Pool. |
| POST | /pools/{poolId}/disableautoscale | Disables automatic scaling for a Pool. |
| POST | /pools/{poolId}/enableautoscale | Enables automatic scaling for a Pool. |
| POST | /pools/{poolId}/evaluateautoscale | Gets the result of evaluating an automatic scaling formula on the Pool. |
| POST | /pools/{poolId}/resize | Changes the number of Compute Nodes that are assigned to a Pool. |
| POST | /pools/{poolId}/stopresize | Stops an ongoing resize operation on the Pool. |
| POST | /pools/{poolId}/updateproperties | Updates the properties of the specified Pool. |
| POST | /pools/{poolId}/removenodes | Removes Compute Nodes from the specified Pool. |
| POST | /pools/{poolId}/nodes/{nodeId}/users | Adds a user Account to the specified Compute Node. |
| DELETE | /pools/{poolId}/nodes/{nodeId}/users/{userName} | Deletes a user Account from the specified Compute Node. |
| PUT | /pools/{poolId}/nodes/{nodeId}/users/{userName} | Updates the password and expiration time of a user Account on the specified Compute Node. |
| GET | /pools/{poolId}/nodes/{nodeId} | Gets information about the specified Compute Node. |
| POST | /pools/{poolId}/nodes/{nodeId}/reboot | Restarts the specified Compute Node. |
| POST | /pools/{poolId}/nodes/{nodeId}/reimage | Reinstalls the operating system on the specified Compute Node. |
| POST | /pools/{poolId}/nodes/{nodeId}/disablescheduling | Disables Task scheduling on the specified Compute Node. |
| POST | /pools/{poolId}/nodes/{nodeId}/enablescheduling | Enables Task scheduling on the specified Compute Node. |
| GET | /pools/{poolId}/nodes/{nodeId}/remoteloginsettings | Gets the settings required for remote login to a Compute Node. |
| GET | /pools/{poolId}/nodes/{nodeId}/rdp | Gets the Remote Desktop Protocol file for the specified Compute Node. |
| POST | /pools/{poolId}/nodes/{nodeId}/uploadbatchservicelogs | Upload Azure Batch service log files from the specified Compute Node to Azure Blob Storage. |
| GET | /pools/{poolId}/nodes | Lists the Compute Nodes in the specified Pool. |

### jobschedules
| Method | Path | Description |
|--------|------|-------------|
| HEAD | /jobschedules/{jobScheduleId} | Checks the specified Job Schedule exists. |
| DELETE | /jobschedules/{jobScheduleId} | Deletes a Job Schedule from the specified Account. |
| GET | /jobschedules/{jobScheduleId} | Gets information about the specified Job Schedule. |
| PATCH | /jobschedules/{jobScheduleId} | Updates the properties of the specified Job Schedule. |
| PUT | /jobschedules/{jobScheduleId} | Updates the properties of the specified Job Schedule. |
| POST | /jobschedules/{jobScheduleId}/disable | Disables a Job Schedule. |
| POST | /jobschedules/{jobScheduleId}/enable | Enables a Job Schedule. |
| POST | /jobschedules/{jobScheduleId}/terminate | Terminates a Job Schedule. |
| POST | /jobschedules | Adds a Job Schedule to the specified Account. |
| GET | /jobschedules | Lists all of the Job Schedules in the specified Account. |
| GET | /jobschedules/{jobScheduleId}/jobs | Lists the Jobs that have been created under the specified Job Schedule. |

## Enhanced Skill Content
## Question Mapping

- "What applications are available in my Batch account?" -> GET /applications
- "Get details about a specific application" -> GET /applications/{applicationId}
- "How do I create a new Batch job?" -> POST /jobs
- "List all jobs in my Batch account" -> GET /jobs
- "How do I submit a task to a job?" -> POST /jobs/{jobId}/tasks
- "Add multiple tasks to a job at once" -> POST /jobs/{jobId}/addtaskcollection
- "What's the task count breakdown for my job?" -> GET /jobs/{jobId}/taskcounts
- "How do I create a compute pool?" -> POST /pools
- "Resize an existing pool" -> POST /pools/{poolId}/resize
- "How do I set up autoscaling on a pool?" -> POST /pools/{poolId}/enableautoscale
- "Download a file from a task's output" -> GET /jobs/{jobId}/tasks/{taskId}/files/{filePath}
- "List files produced by a task" -> GET /jobs/{jobId}/tasks/{taskId}/files
- "How do I create a recurring job schedule?" -> POST /jobschedules
- "Reboot a compute node that's stuck" -> POST /pools/{poolId}/nodes/{nodeId}/reboot
- "Get RDP connection info for a node" -> GET /pools/{poolId}/nodes/{nodeId}/rdp

## Response Tips

- **List endpoints** (jobs, pools, tasks, certificates, schedules): Paginated via `maxresults`; follow `odata.nextLink` in response body for subsequent pages.
- **Async operations** (delete, resize, terminate returning 202): The resource is not immediately gone; poll the resource GET endpoint or use `If-Match` with the ETag to confirm completion.
- **File content endpoints** (GET .../files/{filePath}): Returns raw file bytes, not JSON; use `ocp-range` header for partial downloads; HEAD returns metadata (size, modified date) without body.
- **Task collection** (POST /addtaskcollection): Returns per-task status in an array; check each entry's status individually since partial failures are possible.
- **Autoscale evaluate** (POST /evaluateautoscale): Returns the formula evaluation result without applying it; use this to dry-run formulas before enabling autoscale.

## Anomaly Flags

- **202 Accepted on deletes/terminates**: The operation is queued, not complete. Agent should note this and suggest polling for final state if the user expects immediate removal.
- **ETag / conditional header conflicts**: If a PATCH or PUT returns 412 Precondition Failed, surface that the resource was modified by another client since last read. Recommend re-fetching before retrying.
- **404 on HEAD checks** (pools, job schedules): HEAD endpoints explicitly declare 404 errors. Flag when a resource existence check returns 404 so the user knows the resource is gone or never existed.
- **Autoscale formula errors**: When `evaluateautoscale` returns error results in the evaluation, proactively warn before the user enables a broken formula.
- **Large task collections**: When `addtaskcollection` response contains mixed success/failure statuses, surface the failure count and specific error codes rather than reporting generic success.
- **Rate limiting via `client-request-id`**: If responses start returning 429 or throttling headers, flag the pattern and suggest backing off or batching requests.

## Playbook

### 1. Submit a Job with Tasks and Monitor Completion

1. POST /jobs with job configuration (pool reference, constraints, priority)
2. POST /jobs/{jobId}/addtaskcollection with your task array for bulk submission
3. GET /jobs/{jobId}/taskcounts to check active/completed/failed breakdown
4. GET /jobs/{jobId}/tasks with `$filter=state eq 'completed'` to list finished tasks
5. GET /jobs/{jobId}/tasks/{taskId}/files/{filePath} to download stdout.txt or other outputs
6. POST /jobs/{jobId}/terminate when all work is done (or DELETE /jobs/{jobId} to remove entirely)

### 2. Create and Autoscale a Pool

1. POST /pools with initial VM size, target node count, and OS configuration
2. HEAD /pools/{poolId} to confirm the pool exists (200 = ready, 404 = still provisioning or failed)
3. POST /pools/{poolId}/evaluateautoscale with your formula to dry-run it
4. POST /pools/{poolId}/enableautoscale with the validated formula and evaluation interval
5. GET /pools/{poolId} periodically to monitor allocation state and current node count
6. POST /pools/{poolId}/disableautoscale if you need to return to manual scaling

### 3. Manage a Recurring Job Schedule

1. POST /jobschedules with schedule configuration (recurrence interval, job specification)
2. GET /jobschedules/{jobScheduleId} to verify it was created correctly
3. GET /jobschedules/{jobScheduleId}/jobs to see jobs spawned by the schedule
4. POST /jobschedules/{jobScheduleId}/disable to temporarily pause the schedule
5. POST /jobschedules/{jobScheduleId}/enable to resume it
6. POST /jobschedules/{jobScheduleId}/terminate or DELETE /jobschedules/{jobScheduleId} to stop permanently

### 4. Troubleshoot a Failed Compute Node

1. GET /pools/{poolId}/nodes with `$filter` to find nodes in error or unusable state
2. GET /pools/{poolId}/nodes/{nodeId} to inspect the node's scheduling state and recent errors
3. GET /pools/{poolId}/nodes/{nodeId}/files with `recursive=true` to browse log files
4. POST /pools/{poolId}/nodes/{nodeId}/uploadbatchservicelogs to collect diagnostics
5. POST /pools/{poolId}/nodes/{nodeId}/reboot to attempt recovery, or POST /pools/{poolId}/removenodes to evict it
6. POST /pools/{poolId}/nodes/{nodeId}/reimage as an alternative to reboot for a clean slate

### 5. Manage Certificates for Secure Workloads

1. POST /certificates with the certificate data (PFX or CER format, password if PFX)
2. GET /certificates to list all certificates and confirm the new one appears
3. GET /certificates(thumbprintAlgorithm={alg},thumbprint={tp}) to retrieve a specific certificate's details
4. Reference the certificate thumbprint in pool configuration when creating or updating pools
5. DELETE /certificates(thumbprintAlgorithm={alg},thumbprint={tp}) to remove when no longer needed
6. POST /certificates(...)/canceldelete if the deletion was premature and the certificate is still in use by active nodes


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
