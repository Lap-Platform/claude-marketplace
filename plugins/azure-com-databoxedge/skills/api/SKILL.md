---
name: databoxedgemanagementclient
description: "DataBoxEdgeManagementClient API skill. Use when working with DataBoxEdgeManagementClient for providers, subscriptions. Covers 49 endpoints."
version: 1.0.0
generator: lapsh
---

# DataBoxEdgeManagementClient
API version: 2019-07-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.DataBoxEdge/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/downloadUpdates -- create first downloadUpdates

## Endpoints

49 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.DataBoxEdge/operations | List all the supported operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices | Gets all the Data Box Edge/Data Box Gateway devices in a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices | Gets all the Data Box Edge/Data Box Gateway devices in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName} | Gets the properties of the Data Box Edge/Data Box Gateway device. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName} | Creates or updates a Data Box Edge/Data Box Gateway resource. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName} | Deletes the Data Box Edge/Data Box Gateway device. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName} | Modifies a Data Box Edge/Data Box Gateway resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/alerts | Gets all the alerts for a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/alerts/{name} | Gets an alert by name. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/bandwidthSchedules | Gets all the bandwidth schedules for a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/bandwidthSchedules/{name} | Gets the properties of the specified bandwidth schedule. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/bandwidthSchedules/{name} | Creates or updates a bandwidth schedule. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/bandwidthSchedules/{name} | Deletes the specified bandwidth schedule. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/downloadUpdates | Downloads the updates on a Data Box Edge/Data Box Gateway device. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/getExtendedInformation | Gets additional information for the specified Data Box Edge/Data Box Gateway device. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/installUpdates | Installs the updates on the Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/jobs/{name} | Gets the details of a specified job on a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/networkSettings/default | Gets the network settings of the specified Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/nodes | Gets all the nodes currently configured under this Data Box Edge device |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/operationsStatus/{name} | Gets the details of a specified job on a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/orders | Lists all the orders related to a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/orders/default | Gets a specific order by name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/orders/default | Creates or updates an order. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/orders/default | Deletes the order related to the device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/roles | Lists all the roles configured in a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/roles/{name} | Gets a specific role by name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/roles/{name} | Create or update a role. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/roles/{name} | Deletes the role on the device. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/scanForUpdates | Scans for updates on a Data Box Edge/Data Box Gateway device. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/securitySettings/default/update | Updates the security settings on a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/shares | Lists all the shares in a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/shares/{name} | Gets a share by name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/shares/{name} | Creates a new share or updates an existing share on the device. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/shares/{name} | Deletes the share on the Data Box Edge/Data Box Gateway device. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/shares/{name}/refresh | Refreshes the share metadata with the data from the cloud. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/storageAccountCredentials | Gets all the storage account credentials in a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/storageAccountCredentials/{name} | Gets the properties of the specified storage account credential. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/storageAccountCredentials/{name} | Creates or updates the storage account credential. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/storageAccountCredentials/{name} | Deletes the storage account credential. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/triggers | Lists all the triggers configured in the device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/triggers/{name} | Get a specific trigger by name. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/triggers/{name} | Creates or updates a trigger. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/triggers/{name} | Deletes the trigger on the gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/updateSummary/default | Gets information about the availability of updates based on the last scan of the device. It also gets information about any ongoing download or install jobs on the device. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/uploadCertificate | Uploads registration certificate for the device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/users | Gets all the users registered on a Data Box Edge/Data Box Gateway device. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/users/{name} | Gets the properties of the specified user. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/users/{name} | Creates a new user or updates an existing user's information on a Data Box Edge/Data Box Gateway device. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/users/{name} | Deletes the user on a databox edge/gateway device. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for Data Box Edge?" -> GET /providers/Microsoft.DataBoxEdge/operations
- "List all Data Box Edge devices in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices
- "Show devices in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices
- "Get details of a specific device?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}
- "Create or register a new Data Box Edge device?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}
- "Are there any alerts on my device?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/alerts
- "What is the update status of my device?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/updateSummary/default
- "How do I trigger a firmware update on my device?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/installUpdates
- "What shares are configured on my device?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/shares
- "How do I check the network settings of a device?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/networkSettings/default
- "What bandwidth schedules are set on my device?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/bandwidthSchedules
- "How do I add a storage account credential to a device?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/storageAccountCredentials/{name}
- "What is the status of a long-running job on my device?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/jobs/{name}
- "How do I update the device admin password?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/securitySettings/default/update
- "What roles are assigned on my device?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBoxEdge/dataBoxEdgeDevices/{deviceName}/roles

## Response Tips

- **Device listings** (GET .../dataBoxEdgeDevices): Returns a paginated `value` array with `nextLink` for continuation; use `$expand` to inline child resource details.
- **Single resource GETs** (devices, alerts, shares, roles, users, triggers, bandwidth schedules, storage credentials): Return the resource object directly with `id`, `name`, `type`, and `properties` nested object containing all configuration.
- **PUT/create operations**: Return 200 for synchronous completion or 202 with an `Azure-AsyncOperation` header for long-running operations; poll the operation URL or use the jobs endpoint.
- **DELETE operations**: 200 means completed, 202 means accepted and still processing (check operationsStatus), 204 means the resource was already gone.
- **POST actions** (downloadUpdates, installUpdates, scanForUpdates, refresh): Return 200 for immediate completion or 202 for async; no response body on 202 -- track via jobs or operationsStatus.
- **Alerts**: Read-only collection; each alert has `properties.severity`, `properties.alertType`, and `properties.appearedAtDateTime` for triage.
- **Error responses**: Follow Azure standard `{ "error": { "code": "...", "message": "..." } }` pattern across all endpoints.

## Anomaly Flags

- **202 Accepted without completion**: Surface when PUT, DELETE, or POST returns 202 -- the operation is still running. Prompt the user to poll `operationsStatus/{name}` or `jobs/{name}` for final status.
- **Stale update summary**: If `updateSummary/default` shows `lastInstallOperationDateTime` significantly older than available updates, flag that updates may be pending or stalled.
- **Active alerts on device**: After any device GET, proactively check alerts and surface any with severity "Critical" or "Warning".
- **Delete returning 204**: Indicate the resource was already absent -- the user may have targeted the wrong device or name, or a prior delete already succeeded.
- **Security settings returning 204 instead of 202**: The update may not have been applied; verify the security settings took effect.
- **Rate limiting / throttling**: Azure ARM APIs enforce per-subscription rate limits; surface HTTP 429 responses and `Retry-After` headers immediately.
- **Deprecated API version**: If any response includes `x-ms-deprecation` headers or the 2019-07-01 version returns warnings, flag that a newer API version should be used.
- **Job stuck in running state**: If polling `jobs/{name}` returns a job with `status: Running` for an extended period, proactively alert the user.

## Playbook

### 1. Provision and Configure a New Device

1. Create the device: PUT `.../dataBoxEdgeDevices/{deviceName}` with the `DataBoxEdgeDevice` body (location, SKU, tags).
2. Upload activation certificate: POST `.../uploadCertificate` with the certificate parameters.
3. Get extended information: POST `.../getExtendedInformation` to retrieve the activation key and encryption details.
4. Configure bandwidth schedule: PUT `.../bandwidthSchedules/{name}` to set upload/download windows.
5. Add storage account credentials: PUT `.../storageAccountCredentials/{name}` with the account key.
6. Create shares: PUT `.../shares/{name}` referencing the storage credential.
7. Configure users: PUT `.../users/{name}` to set up local user accounts for share access.

### 2. Check for and Install Updates

1. Scan for available updates: POST `.../scanForUpdates` (returns 202; poll `operationsStatus` until complete).
2. Review update summary: GET `.../updateSummary/default` to see available update versions and sizes.
3. Download updates: POST `.../downloadUpdates` (returns 202; monitor via `jobs/{name}`).
4. Install updates: POST `.../installUpdates` (returns 202; monitor via `jobs/{name}`).
5. Verify completion: GET `.../updateSummary/default` again to confirm the device is on the latest version.

### 3. Investigate and Resolve Device Alerts

1. List all alerts: GET `.../alerts` to retrieve the full alert collection.
2. Inspect a specific alert: GET `.../alerts/{name}` to see detailed severity, type, and recommendations.
3. Check device status: GET `.../dataBoxEdgeDevices/{deviceName}` to see overall device health.
4. Review network settings: GET `.../networkSettings/default` if the alert is connectivity-related.
5. Take corrective action (e.g., refresh a share via POST `.../shares/{name}/refresh`, or update security settings via POST `.../securitySettings/default/update`).

### 4. Manage Shares and Storage Lifecycle

1. List existing shares: GET `.../shares` to see all configured shares and their status.
2. List storage account credentials: GET `.../storageAccountCredentials` to verify linked accounts.
3. Create or update a share: PUT `.../shares/{name}` with the share configuration (access protocol, user mappings, storage account reference).
4. Refresh share data: POST `.../shares/{name}/refresh` to force a sync with cloud storage (returns 202).
5. Remove a share: DELETE `.../shares/{name}` (returns 200/202/204).
6. Clean up unused credentials: DELETE `.../storageAccountCredentials/{name}` after removing all dependent shares.

### 5. Set Up Roles and Triggers for Edge Compute

1. List current roles: GET `.../roles` to see existing IoT and compute role assignments.
2. Create a role: PUT `.../roles/{name}` with the role configuration (e.g., IoTRole with IoT Hub connection details).
3. List triggers: GET `.../triggers` to review event-driven automation; use `$expand` for full details.
4. Create a trigger: PUT `.../triggers/{name}` linking it to a role and share (e.g., file event trigger on share upload).
5. Verify the setup: GET `.../roles/{name}` and GET `.../triggers/{name}` to confirm the configuration is active and healthy.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
