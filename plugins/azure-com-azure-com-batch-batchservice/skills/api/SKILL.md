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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all applications?" -> GET /applications
- "Get application details?" -> GET /applications/{applicationId}
- "List all poolusagemetrics?" -> GET /poolusagemetrics
- "List all supportedimages?" -> GET /supportedimages
- "List all nodecounts?" -> GET /nodecounts
- "List all lifetimepoolstats?" -> GET /lifetimepoolstats
- "List all lifetimejobstats?" -> GET /lifetimejobstats
- "Create a certificate?" -> POST /certificates
- "List all certificates?" -> GET /certificates
- "Create a canceldelete?" -> POST /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint})/canceldelete
- "Delete a certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint})?" -> DELETE /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint})
- "Get certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint}) details?" -> GET /certificates(thumbprintAlgorithm={thumbprintAlgorithm},thumbprint={thumbprint})
- "Delete a file?" -> DELETE /jobs/{jobId}/tasks/{taskId}/files/{filePath}
- "Get file details?" -> GET /jobs/{jobId}/tasks/{taskId}/files/{filePath}
- "Delete a file?" -> DELETE /pools/{poolId}/nodes/{nodeId}/files/{filePath}
- "Get file details?" -> GET /pools/{poolId}/nodes/{nodeId}/files/{filePath}
- "List all files?" -> GET /jobs/{jobId}/tasks/{taskId}/files
- "List all files?" -> GET /pools/{poolId}/nodes/{nodeId}/files
- "Delete a jobschedule?" -> DELETE /jobschedules/{jobScheduleId}
- "Get jobschedule details?" -> GET /jobschedules/{jobScheduleId}
- "Partially update a jobschedule?" -> PATCH /jobschedules/{jobScheduleId}
- "Update a jobschedule?" -> PUT /jobschedules/{jobScheduleId}
- "Create a disable?" -> POST /jobschedules/{jobScheduleId}/disable
- "Create a enable?" -> POST /jobschedules/{jobScheduleId}/enable
- "Create a terminate?" -> POST /jobschedules/{jobScheduleId}/terminate
- "Create a jobschedule?" -> POST /jobschedules
- "List all jobschedules?" -> GET /jobschedules
- "Delete a job?" -> DELETE /jobs/{jobId}
- "Get job details?" -> GET /jobs/{jobId}
- "Partially update a job?" -> PATCH /jobs/{jobId}
- "Update a job?" -> PUT /jobs/{jobId}
- "Create a disable?" -> POST /jobs/{jobId}/disable
- "Create a enable?" -> POST /jobs/{jobId}/enable
- "Create a terminate?" -> POST /jobs/{jobId}/terminate
- "Create a job?" -> POST /jobs
- "List all jobs?" -> GET /jobs
- "List all jobs?" -> GET /jobschedules/{jobScheduleId}/jobs
- "List all jobpreparationandreleasetaskstatus?" -> GET /jobs/{jobId}/jobpreparationandreleasetaskstatus
- "List all taskcounts?" -> GET /jobs/{jobId}/taskcounts
- "Create a pool?" -> POST /pools
- "List all pools?" -> GET /pools
- "Delete a pool?" -> DELETE /pools/{poolId}
- "Get pool details?" -> GET /pools/{poolId}
- "Partially update a pool?" -> PATCH /pools/{poolId}
- "Create a disableautoscale?" -> POST /pools/{poolId}/disableautoscale
- "Create a enableautoscale?" -> POST /pools/{poolId}/enableautoscale
- "Create a evaluateautoscale?" -> POST /pools/{poolId}/evaluateautoscale
- "Create a resize?" -> POST /pools/{poolId}/resize
- "Create a stopresize?" -> POST /pools/{poolId}/stopresize
- "Create a updateproperty?" -> POST /pools/{poolId}/updateproperties
- "Create a removenode?" -> POST /pools/{poolId}/removenodes
- "Create a task?" -> POST /jobs/{jobId}/tasks
- "List all tasks?" -> GET /jobs/{jobId}/tasks
- "Create a addtaskcollection?" -> POST /jobs/{jobId}/addtaskcollection
- "Delete a task?" -> DELETE /jobs/{jobId}/tasks/{taskId}
- "Get task details?" -> GET /jobs/{jobId}/tasks/{taskId}
- "Update a task?" -> PUT /jobs/{jobId}/tasks/{taskId}
- "List all subtasksinfo?" -> GET /jobs/{jobId}/tasks/{taskId}/subtasksinfo
- "Create a terminate?" -> POST /jobs/{jobId}/tasks/{taskId}/terminate
- "Create a reactivate?" -> POST /jobs/{jobId}/tasks/{taskId}/reactivate
- "Create a user?" -> POST /pools/{poolId}/nodes/{nodeId}/users
- "Delete a user?" -> DELETE /pools/{poolId}/nodes/{nodeId}/users/{userName}
- "Update a user?" -> PUT /pools/{poolId}/nodes/{nodeId}/users/{userName}
- "Get node details?" -> GET /pools/{poolId}/nodes/{nodeId}
- "Create a reboot?" -> POST /pools/{poolId}/nodes/{nodeId}/reboot
- "Create a reimage?" -> POST /pools/{poolId}/nodes/{nodeId}/reimage
- "Create a disablescheduling?" -> POST /pools/{poolId}/nodes/{nodeId}/disablescheduling
- "Create a enablescheduling?" -> POST /pools/{poolId}/nodes/{nodeId}/enablescheduling
- "List all remoteloginsettings?" -> GET /pools/{poolId}/nodes/{nodeId}/remoteloginsettings
- "List all rdp?" -> GET /pools/{poolId}/nodes/{nodeId}/rdp
- "Create a uploadbatchservicelog?" -> POST /pools/{poolId}/nodes/{nodeId}/uploadbatchservicelogs
- "List all nodes?" -> GET /pools/{poolId}/nodes
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
