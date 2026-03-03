---
name: batchservice
description: "BatchService API skill. Use when working with BatchService for applications, poolusagemetrics, nodeagentskus. Covers 77 endpoints."
version: 1.0.0
generator: lapsh
---

# BatchService
API version: 2018-08-01.7.0

## Auth
No authentication required.

## Base URL
https://batch.core.windows.net

## Setup
1. No auth setup needed
2. GET /applications -- verify access
3. POST /certificates -- create first certificates

## Endpoints

77 endpoints across 11 groups. See references/api-spec.lap for full details.

### applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /applications | Lists all of the applications available in the specified account. |
| GET | /applications/{applicationId} | Gets information about the specified application. |

### poolusagemetrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /poolusagemetrics | Lists the usage metrics, aggregated by pool across individual time intervals, for the specified account. |

### nodeagentskus
| Method | Path | Description |
|--------|------|-------------|
| GET | /nodeagentskus | Lists all node agent SKUs supported by the Azure Batch service. |

### nodecounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /nodecounts | Gets the number of nodes in each state, grouped by pool. |

### lifetimepoolstats
| Method | Path | Description |
|--------|------|-------------|
| GET | /lifetimepoolstats | Gets lifetime summary statistics for all of the pools in the specified account. |

### lifetimejobstats
| Method | Path | Description |
|--------|------|-------------|
| GET | /lifetimejobstats | Gets lifetime summary statistics for all of the jobs in the specified account. |

### certificates
| Method | Path | Description |
|--------|------|-------------|
| POST | /certificates | Adds a certificate to the specified account. |
| GET | /certificates | Lists all of the certificates that have been added to the specified account. |

### certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint})
| Method | Path | Description |
|--------|------|-------------|
| POST | /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint})/canceldelete | Cancels a failed deletion of a certificate from the specified account. |
| DELETE | /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint}) | Deletes a certificate from the specified account. |
| GET | /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint}) | Gets information about the specified certificate. |

### jobs
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /jobs/{jobId}/tasks/{taskId}/files/{filePath} | Deletes the specified task file from the compute node where the task ran. |
| GET | /jobs/{jobId}/tasks/{taskId}/files/{filePath} | Returns the content of the specified task file. |
| HEAD | /jobs/{jobId}/tasks/{taskId}/files/{filePath} | Gets the properties of the specified task file. |
| GET | /jobs/{jobId}/tasks/{taskId}/files | Lists the files in a task's directory on its compute node. |
| DELETE | /jobs/{jobId} | Deletes a job. |
| GET | /jobs/{jobId} | Gets information about the specified job. |
| PATCH | /jobs/{jobId} | Updates the properties of the specified job. |
| PUT | /jobs/{jobId} | Updates the properties of the specified job. |
| POST | /jobs/{jobId}/disable | Disables the specified job, preventing new tasks from running. |
| POST | /jobs/{jobId}/enable | Enables the specified job, allowing new tasks to run. |
| POST | /jobs/{jobId}/terminate | Terminates the specified job, marking it as completed. |
| POST | /jobs | Adds a job to the specified account. |
| GET | /jobs | Lists all of the jobs in the specified account. |
| GET | /jobs/{jobId}/jobpreparationandreleasetaskstatus | Lists the execution status of the Job Preparation and Job Release task for the specified job across the compute nodes where the job has run. |
| GET | /jobs/{jobId}/taskcounts | Gets the task counts for the specified job. |
| POST | /jobs/{jobId}/tasks | Adds a task to the specified job. |
| GET | /jobs/{jobId}/tasks | Lists all of the tasks that are associated with the specified job. |
| POST | /jobs/{jobId}/addtaskcollection | Adds a collection of tasks to the specified job. |
| DELETE | /jobs/{jobId}/tasks/{taskId} | Deletes a task from the specified job. |
| GET | /jobs/{jobId}/tasks/{taskId} | Gets information about the specified task. |
| PUT | /jobs/{jobId}/tasks/{taskId} | Updates the properties of the specified task. |
| GET | /jobs/{jobId}/tasks/{taskId}/subtasksinfo | Lists all of the subtasks that are associated with the specified multi-instance task. |
| POST | /jobs/{jobId}/tasks/{taskId}/terminate | Terminates the specified task. |
| POST | /jobs/{jobId}/tasks/{taskId}/reactivate | Reactivates a task, allowing it to run again even if its retry count has been exhausted. |

### pools
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /pools/{poolId}/nodes/{nodeId}/files/{filePath} | Deletes the specified file from the compute node. |
| GET | /pools/{poolId}/nodes/{nodeId}/files/{filePath} | Returns the content of the specified compute node file. |
| HEAD | /pools/{poolId}/nodes/{nodeId}/files/{filePath} | Gets the properties of the specified compute node file. |
| GET | /pools/{poolId}/nodes/{nodeId}/files | Lists all of the files in task directories on the specified compute node. |
| POST | /pools | Adds a pool to the specified account. |
| GET | /pools | Lists all of the pools in the specified account. |
| DELETE | /pools/{poolId} | Deletes a pool from the specified account. |
| HEAD | /pools/{poolId} | Gets basic properties of a pool. |
| GET | /pools/{poolId} | Gets information about the specified pool. |
| PATCH | /pools/{poolId} | Updates the properties of the specified pool. |
| POST | /pools/{poolId}/disableautoscale | Disables automatic scaling for a pool. |
| POST | /pools/{poolId}/enableautoscale | Enables automatic scaling for a pool. |
| POST | /pools/{poolId}/evaluateautoscale | Gets the result of evaluating an automatic scaling formula on the pool. |
| POST | /pools/{poolId}/resize | Changes the number of compute nodes that are assigned to a pool. |
| POST | /pools/{poolId}/stopresize | Stops an ongoing resize operation on the pool. |
| POST | /pools/{poolId}/updateproperties | Updates the properties of the specified pool. |
| POST | /pools/{poolId}/upgradeos | Upgrades the operating system of the specified pool. |
| POST | /pools/{poolId}/removenodes | Removes compute nodes from the specified pool. |
| POST | /pools/{poolId}/nodes/{nodeId}/users | Adds a user account to the specified compute node. |
| DELETE | /pools/{poolId}/nodes/{nodeId}/users/{userName} | Deletes a user account from the specified compute node. |
| PUT | /pools/{poolId}/nodes/{nodeId}/users/{userName} | Updates the password and expiration time of a user account on the specified compute node. |
| GET | /pools/{poolId}/nodes/{nodeId} | Gets information about the specified compute node. |
| POST | /pools/{poolId}/nodes/{nodeId}/reboot | Restarts the specified compute node. |
| POST | /pools/{poolId}/nodes/{nodeId}/reimage | Reinstalls the operating system on the specified compute node. |
| POST | /pools/{poolId}/nodes/{nodeId}/disablescheduling | Disables task scheduling on the specified compute node. |
| POST | /pools/{poolId}/nodes/{nodeId}/enablescheduling | Enables task scheduling on the specified compute node. |
| GET | /pools/{poolId}/nodes/{nodeId}/remoteloginsettings | Gets the settings required for remote login to a compute node. |
| GET | /pools/{poolId}/nodes/{nodeId}/rdp | Gets the Remote Desktop Protocol file for the specified compute node. |
| POST | /pools/{poolId}/nodes/{nodeId}/uploadbatchservicelogs | Upload Azure Batch service log files from the specified compute node to Azure Blob Storage. |
| GET | /pools/{poolId}/nodes | Lists the compute nodes in the specified pool. |

### jobschedules
| Method | Path | Description |
|--------|------|-------------|
| HEAD | /jobschedules/{jobScheduleId} | Checks the specified job schedule exists. |
| DELETE | /jobschedules/{jobScheduleId} | Deletes a job schedule from the specified account. |
| GET | /jobschedules/{jobScheduleId} | Gets information about the specified job schedule. |
| PATCH | /jobschedules/{jobScheduleId} | Updates the properties of the specified job schedule. |
| PUT | /jobschedules/{jobScheduleId} | Updates the properties of the specified job schedule. |
| POST | /jobschedules/{jobScheduleId}/disable | Disables a job schedule. |
| POST | /jobschedules/{jobScheduleId}/enable | Enables a job schedule. |
| POST | /jobschedules/{jobScheduleId}/terminate | Terminates a job schedule. |
| POST | /jobschedules | Adds a job schedule to the specified account. |
| GET | /jobschedules | Lists all of the job schedules in the specified account. |
| GET | /jobschedules/{jobScheduleId}/jobs | Lists the jobs that have been created under the specified job schedule. |

## Enhanced Skill Content
## Question Mapping

- "What applications are available in my Batch account?" -> GET /applications
- "Get details about a specific application" -> GET /applications/{applicationId}
- "How do I create a new Batch job?" -> POST /jobs
- "What is the status of my job?" -> GET /jobs/{jobId}
- "How do I add a task to a job?" -> POST /jobs/{jobId}/tasks
- "How many tasks are in each state for my job?" -> GET /jobs/{jobId}/taskcounts
- "How do I create a pool of compute nodes?" -> POST /pools
- "How do I resize an existing pool?" -> POST /pools/{poolId}/resize
- "How do I download a task's output file?" -> GET /jobs/{jobId}/tasks/{taskId}/files/{filePath}
- "What compute node agent SKUs are available?" -> GET /nodeagentskus
- "How do I set up a recurring job schedule?" -> POST /jobschedules
- "How do I stop an autoscale-enabled pool from scaling?" -> POST /pools/{poolId}/disableautoscale
- "How do I reboot a specific compute node?" -> POST /pools/{poolId}/nodes/{nodeId}/reboot
- "How do I add multiple tasks to a job at once?" -> POST /jobs/{jobId}/addtaskcollection
- "What are the lifetime statistics for all my pools?" -> GET /lifetimepoolstats

## Response Tips

- **List endpoints** (jobs, pools, tasks, certificates, schedules): Responses are paged; use `maxresults` to control page size and follow `odata.nextLink` for subsequent pages.
- **Async operations** (delete, resize, terminate returning 202): The 202 means accepted, not completed; poll the resource with GET or HEAD to confirm the operation finished.
- **Create endpoints** (returning 201): Response headers include the resource URL in the `Location` or `DataServiceId` header.
- **File content** (GET .../files/{filePath}): Returns raw file bytes, not JSON; use the `ocp-range` header for partial downloads and check `Content-Length` in HEAD responses before downloading.
- **Conditional headers** (If-Match, If-Modified-Since): Use ETag and Last-Modified values from GET/HEAD responses; a 412 Precondition Failed means the resource was modified since you last read it.
- **Node counts and usage metrics**: Aggregated data may lag a few minutes behind real-time state; treat as approximate.

## Anomaly Flags

- **202 responses lingering**: If a delete, resize, or terminate operation was accepted (202) but the resource still shows unchanged state after several minutes, surface a warning that the operation may be stuck.
- **Pool resize errors**: After POST /pools/{poolId}/resize, if a subsequent GET shows `resizeErrors` in the pool object, flag these immediately as they often indicate quota limits or image availability issues.
- **Task failures in bulk add**: POST /jobs/{jobId}/addtaskcollection returns per-task status; flag any tasks with non-success status codes as they are easy to miss in a large collection response.
- **Certificate deletion in "deletefailed" state**: If DELETE /certificates returns 202 but the certificate enters a `deletefailed` state (visible via GET), prompt the user to run POST .../canceldelete before retrying.
- **Job preparation/release task failures**: GET /jobs/{jobId}/jobpreparationandreleasetaskstatus may reveal nodes where prep tasks failed, which blocks task execution on those nodes -- surface these proactively.
- **Deprecated OS versions**: When POST /pools/{poolId}/upgradeos is used, flag if the target OS version is close to end-of-support based on the cloudServiceConfiguration.
- **Conditional update conflicts**: Any 412 Precondition Failed response should be surfaced with guidance to re-fetch the resource and retry with the updated ETag.

## Playbook

### 1. Submit a Job with Tasks and Monitor to Completion

1. Create a pool if one does not exist: POST /pools with desired VM size and node count.
2. Wait for pool allocation by polling GET /pools/{poolId} until `allocationState` is `steady`.
3. Create a job targeting the pool: POST /jobs with `poolInfo.poolId` set.
4. Add tasks to the job: POST /jobs/{jobId}/addtaskcollection for bulk or POST /jobs/{jobId}/tasks for individual tasks.
5. Monitor progress: GET /jobs/{jobId}/taskcounts to check active, completed, and failed counts.
6. When all tasks complete, retrieve output: GET /jobs/{jobId}/tasks/{taskId}/files/{filePath} for each task's stdout/stderr.
7. Clean up: DELETE /jobs/{jobId} (the job and its tasks are removed; pool remains).

### 2. Set Up a Recurring Job Schedule

1. Define the schedule and job specification: POST /jobschedules with a `schedule` (recurrence interval, start/end times) and `jobSpecification` (pool, task factory, constraints).
2. Verify it was created: GET /jobschedules/{jobScheduleId} and confirm `state` is `active`.
3. List jobs spawned by the schedule: GET /jobschedules/{jobScheduleId}/jobs.
4. To pause temporarily: POST /jobschedules/{jobScheduleId}/disable.
5. To resume: POST /jobschedules/{jobScheduleId}/enable.
6. To stop permanently: POST /jobschedules/{jobScheduleId}/terminate, then DELETE /jobschedules/{jobScheduleId}.

### 3. Autoscale a Pool Based on Workload

1. Create a pool with autoscale disabled: POST /pools (set `enableAutoScale` to false initially).
2. Enable autoscale with a formula: POST /pools/{poolId}/enableautoscale with `autoScaleFormula` and `autoScaleEvaluationInterval`.
3. Test a formula before applying: POST /pools/{poolId}/evaluateautoscale with candidate formula to see projected results without changing the pool.
4. Monitor: GET /pools/{poolId} and inspect `autoScaleRun` for the last evaluation result and any formula errors.
5. To revert to manual sizing: POST /pools/{poolId}/disableautoscale, then POST /pools/{poolId}/resize with a fixed `targetDedicatedNodes` value.

### 4. Manage Certificates for Secure Task Execution

1. Add a certificate: POST /certificates with the PFX/CER data, thumbprint, and thumbprint algorithm.
2. List certificates: GET /certificates to confirm it was added and check its `state`.
3. Reference the certificate in a pool: PATCH /pools/{poolId} to add it to `certificateReferences`.
4. If deletion fails (state = `deletefailed`): POST /certificates(thumbprintAlgorithm=sha1,thumbprint={thumbprint})/canceldelete, fix the dependency (remove from pool references), then retry DELETE.

### 5. Troubleshoot a Failing Compute Node

1. List nodes in the pool: GET /pools/{poolId}/nodes and identify nodes with `state` = `unusable` or `startTaskFailed`.
2. Get node details: GET /pools/{poolId}/nodes/{nodeId} to check `errors`, `startTaskInfo`, and scheduling state.
3. Retrieve startup task logs: GET /pools/{poolId}/nodes/{nodeId}/files/startup/stdout.txt (and stderr.txt).
4. If the node is stuck, reboot it: POST /pools/{poolId}/nodes/{nodeId}/reboot.
5. If reboot does not help, reimage: POST /pools/{poolId}/nodes/{nodeId}/reimage to reset it to a clean OS state.
6. Upload Batch service logs for Microsoft support: POST /pools/{poolId}/nodes/{nodeId}/uploadbatchservicelogs with a container URL and time range.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
