---
name: microsoft-storage-sync
description: "Microsoft Storage Sync API skill. Use when working with Microsoft Storage Sync for providers, subscriptions. Covers 37 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Storage Sync
API version: 2019-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.StorageSync/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.StorageSync/locations/{locationName}/checkNameAvailability -- create first checkNameAvailability

## Endpoints

37 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.StorageSync/operations | Lists all of the available Storage Sync Rest API operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.StorageSync/locations/{locationName}/checkNameAvailability | Check the give namespace name availability. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName} | Create a new StorageSyncService. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName} | Get a given StorageSyncService. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName} | Patch a given StorageSyncService. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName} | Delete a given StorageSyncService. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices | Get a StorageSyncService list by Resource group name. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.StorageSync/storageSyncServices | Get a StorageSyncService list by subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups | Get a SyncGroup List. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName} | Create a new SyncGroup. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName} | Get a given SyncGroup. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName} | Delete a given SyncGroup. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName} | Create a new CloudEndpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName} | Get a given CloudEndpoint. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName} | Delete a given CloudEndpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints | Get a CloudEndpoint List. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName}/prebackup | Pre Backup a given CloudEndpoint. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName}/postbackup | Post Backup a given CloudEndpoint. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName}/prerestore | Pre Restore a given CloudEndpoint. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName}/restoreheartbeat | Restore Heartbeat a given CloudEndpoint. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName}/postrestore | Post Restore a given CloudEndpoint. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName}/triggerChangeDetection | Triggers detection of changes performed on Azure File share connected to the specified Azure File Sync Cloud Endpoint. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/serverEndpoints/{serverEndpointName} | Create a new ServerEndpoint. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/serverEndpoints/{serverEndpointName} | Patch a given ServerEndpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/serverEndpoints/{serverEndpointName} | Get a ServerEndpoint. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/serverEndpoints/{serverEndpointName} | Delete a given ServerEndpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/serverEndpoints | Get a ServerEndpoint list. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/serverEndpoints/{serverEndpointName}/recallAction | Recall a server endpoint. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/registeredServers | Get a given registered server list. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/registeredServers/{serverId} | Get a given registered server. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/registeredServers/{serverId} | Add a new registered server. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/registeredServers/{serverId} | Delete the given registered server. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/registeredServers/{serverId}/triggerRollover | Triggers Server certificate rollover. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/workflows | Get a Workflow List |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/workflows/{workflowId} | Get Workflows resource |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/workflows/{workflowId}/abort | Abort the given workflow. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/locations/{locationName}/workflows/{workflowId}/operations/{operationId} | Get Operation status |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Storage Sync?" -> GET /providers/Microsoft.StorageSync/operations
- "Can I use this name for a new Storage Sync service?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.StorageSync/locations/{locationName}/checkNameAvailability
- "Create a new Storage Sync service" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}
- "List all Storage Sync services in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StorageSync/storageSyncServices
- "Show me the sync groups for a Storage Sync service" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups
- "Register a server with my Storage Sync service" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/registeredServers/{serverId}
- "Add an Azure file share as a cloud endpoint" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName}
- "Add a server endpoint to a sync group" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/serverEndpoints/{serverEndpointName}
- "What's the status of a running workflow?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/workflows/{workflowId}
- "Cancel a long-running sync operation" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/workflows/{workflowId}/abort
- "Trigger change detection on a cloud endpoint" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/cloudEndpoints/{cloudEndpointName}/triggerChangeDetection
- "Recall tiered files from a server endpoint" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/syncGroups/{syncGroupName}/serverEndpoints/{serverEndpointName}/recallAction
- "Rotate the server certificate" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/registeredServers/{serverId}/triggerRollover
- "Remove a registered server from my sync service" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.StorageSync/storageSyncServices/{storageSyncServiceName}/registeredServers/{serverId}
- "Back up my cloud endpoint before maintenance" -> POST /...cloudEndpoints/{cloudEndpointName}/prebackup then POST /...cloudEndpoints/{cloudEndpointName}/postbackup

## Response Tips

- **Service/group/endpoint CRUD (GET/PUT/DELETE):** 200 returns the resource object with properties nested under a `properties` key; 204 on DELETE means already gone -- treat as success.
- **Long-running operations (PUT/POST returning 202):** The response includes an `Azure-AsyncOperation` or `Location` header -- poll that URL until `status` is `Succeeded`, `Failed`, or `Canceled`.
- **List endpoints:** Responses wrap items in a `value` array; check for a `nextLink` property to paginate through large result sets.
- **Name availability check:** Returns `{ nameAvailable: bool, reason: string, message: string }` -- surface the `message` field when `nameAvailable` is false.
- **Workflow and operation status:** The `status` field uses Azure provisioning states (`Succeeded`, `Failed`, `Canceled`, `Active`) -- do not assume completion until a terminal state appears.

## Anomaly Flags

- **202 Accepted without completion:** Any PUT or POST returning 202 means the operation is still running. Surface this immediately and offer to poll the async operation URL.
- **204 on DELETE:** Indicates the resource was already absent. Flag if the caller expected it to exist, as it may signal a stale reference.
- **Workflow in non-terminal state:** When listing or reading workflows, flag any with `status` other than `Succeeded` -- these represent in-progress or failed operations needing attention.
- **Registered server health:** After fetching registered servers, surface any with unhealthy sync status, expired certificates, or servers not seen recently.
- **Backup/restore sequence violations:** If `postbackup` or `postrestore` is called without a preceding `prebackup` or `prerestore`, flag the out-of-order call -- this can leave the endpoint in an inconsistent state.
- **Rate limiting / throttling:** Azure ARM APIs return 429 with a `Retry-After` header. Surface the wait time and retry automatically when encountered.
- **API version drift:** This spec uses `2019-03-01`. If Azure returns errors suggesting a newer `api-version` is required, flag the version mismatch.

## Playbook

### 1. Set up a new sync topology from scratch

1. POST `.../checkNameAvailability` to validate the desired service name.
2. PUT `.../storageSyncServices/{name}` to create the Storage Sync Service.
3. PUT `.../syncGroups/{groupName}` to create a sync group within the service.
4. PUT `.../cloudEndpoints/{endpointName}` to connect an Azure file share (poll 202 until complete).
5. PUT `.../registeredServers/{serverId}` to register the on-prem server (poll 202 until complete).
6. PUT `.../serverEndpoints/{endpointName}` to add the server path to the sync group (poll 202 until complete).
7. GET `.../workflows` to confirm all provisioning workflows completed successfully.

### 2. Perform a backup and restore cycle

1. POST `.../cloudEndpoints/{name}/prebackup` to prepare the cloud endpoint (wait for 200 or poll 202).
2. Run your backup tool against the Azure file share.
3. POST `.../cloudEndpoints/{name}/postbackup` to finalize (wait for completion).
4. If restoring: POST `.../cloudEndpoints/{name}/prerestore` to prepare.
5. Restore files to the Azure file share.
6. POST `.../cloudEndpoints/{name}/restoreheartbeat` periodically during long restores to prevent timeout.
7. POST `.../cloudEndpoints/{name}/postrestore` to finalize the restore.

### 3. Decommission a server from sync

1. GET `.../serverEndpoints` to list all server endpoints in the sync group.
2. DELETE `.../serverEndpoints/{name}` for each endpoint on the target server (poll 202 until complete).
3. DELETE `.../registeredServers/{serverId}` to unregister the server (poll 202 until complete).
4. GET `.../registeredServers` to confirm the server no longer appears.

### 4. Troubleshoot a stuck sync workflow

1. GET `.../workflows` to list all workflows and identify any with non-terminal status.
2. GET `.../workflows/{workflowId}` to inspect the stuck workflow's details and error info.
3. GET `.../locations/{location}/workflows/{workflowId}/operations/{operationId}` to check the specific operation status.
4. If unrecoverable, POST `.../workflows/{workflowId}/abort` to cancel the workflow.
5. Re-attempt the original operation (e.g., re-create the endpoint) after confirming the abort succeeded.

### 5. Rotate a registered server's certificate

1. GET `.../registeredServers/{serverId}` to verify the server's current status and certificate info.
2. POST `.../registeredServers/{serverId}/triggerRollover` with the new certificate public key in the parameters body.
3. Poll the 202 response until the rollover completes.
4. GET `.../registeredServers/{serverId}` again to confirm the certificate has been updated.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
