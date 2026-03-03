---
name: batchmanagement
description: "BatchManagement API skill. Use when working with BatchManagement for subscriptions, providers. Covers 35 endpoints."
version: 1.0.0
generator: lapsh
---

# BatchManagement
API version: 2019-08-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Batch/operations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/syncAutoStorageKeys -- create first syncAutoStorageKeys

## Endpoints

35 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName} | Creates a new Batch account with the specified parameters. Existing accounts cannot be updated with this API and should instead be updated with the Update Batch Account API. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName} | Updates the properties of an existing Batch account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName} | Deletes the specified Batch account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName} | Gets information about the specified Batch account. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Batch/batchAccounts | Gets information about the Batch accounts associated with the subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts | Gets information about the Batch accounts associated with the specified resource group. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/syncAutoStorageKeys | Synchronizes access keys for the auto-storage account configured for the specified Batch account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/regenerateKeys | Regenerates the specified account key for the Batch account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/listKeys | Gets the account keys for the specified Batch account. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName}/versions/{versionName}/activate | Activates the specified application package. This should be done after the `ApplicationPackage` was created and uploaded. This needs to be done before an `ApplicationPackage` can be used on Pools or Tasks |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName} | Adds an application to the specified Batch account. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName} | Deletes an application. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName} | Gets information about the specified application. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName} | Updates settings for the specified application. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName}/versions/{versionName} | Creates an application package record. The record contains the SAS where the package should be uploaded to.  Once it is uploaded the `ApplicationPackage` needs to be activated using `ApplicationPackageActive` before it can be used. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName}/versions/{versionName} | Deletes an application package record and its associated binary file. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName}/versions/{versionName} | Gets information about the specified application package. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications | Lists all of the applications in the specified account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/applications/{applicationName}/versions | Lists all of the application packages in the specified application. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Batch/locations/{locationName}/quotas | Gets the Batch service quotas for the specified subscription at the given location. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Batch/locations/{locationName}/checkNameAvailability | Checks whether the Batch account name is available in the specified region. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/certificates | Lists all of the certificates in the specified account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/certificates/{certificateName} | Creates a new certificate inside the specified account. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/certificates/{certificateName} | Updates the properties of an existing certificate. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/certificates/{certificateName} | Deletes the specified certificate. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/certificates/{certificateName} | Gets information about the specified certificate. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/certificates/{certificateName}/cancelDelete | Cancels a failed deletion of a certificate from the specified account. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools | Lists all of the pools in the specified account. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName} | Creates a new pool inside the specified account. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName} | Updates the properties of an existing pool. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName} | Deletes the specified pool. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName} | Gets information about the specified pool. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName}/disableAutoScale | Disables automatic scaling for a pool. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName}/stopResize | Stops an ongoing resize operation on the pool. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Batch/operations | Lists available operations for the Microsoft.Batch provider |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new Batch account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}
- "How do I update an existing Batch account's settings?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}
- "How do I delete a Batch account?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}
- "What Batch accounts exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Batch/batchAccounts
- "Is this Batch account name available in my region?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Batch/locations/{locationName}/checkNameAvailability
- "How do I get the access keys for my Batch account?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/listKeys
- "How do I rotate a Batch account key?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/regenerateKeys
- "How do I create a compute pool in my Batch account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName}
- "How do I stop a pool from resizing?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName}/stopResize
- "How do I turn off autoscale on a pool?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/pools/{poolName}/disableAutoScale
- "How do I upload an application package version and activate it?" -> PUT .../applications/{applicationName}/versions/{versionName} then POST .../versions/{versionName}/activate
- "How do I add a certificate to my Batch account?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/certificates/{certificateName}
- "A certificate delete failed -- how do I cancel it?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Batch/batchAccounts/{accountName}/certificates/{certificateName}/cancelDelete
- "What are my Batch quotas in a given region?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Batch/locations/{locationName}/quotas
- "What management operations does the Batch resource provider support?" -> GET /providers/Microsoft.Batch/operations

## Response Tips

- **Account/Pool/Certificate lists**: Paginated via `nextLink` in the response body; follow it until absent. Use `maxresults` query param to control page size.
- **Async operations (202 responses)**: Account create, account delete, pool delete, and certificate delete return 202 with a `Location` or `Azure-AsyncOperation` header -- poll that URL until terminal state.
- **Key operations (listKeys, regenerateKeys)**: Return `primary` and `secondary` key fields directly; no pagination.
- **Quota responses**: Flat object with `accountQuota` for the region; no nested collections.
- **Error responses**: All endpoints return an `error` object with `code` and `message`; nested `details` array may contain per-field validation failures.
- **ETag support**: Certificate and pool PUT/PATCH accept `If-Match` and `If-None-Match` headers; the response `ETag` header should be captured for subsequent conditional updates.

## Anomaly Flags

- **202 Accepted without completion**: Surface when account create, account delete, pool delete, or certificate delete returns 202 -- the operation is still running and needs polling.
- **204 on delete**: A 204 means the resource was already gone; flag if the caller expected it to exist.
- **Quota limits approaching**: After fetching quotas, compare current account count against `accountQuota` and warn if utilization exceeds 80%.
- **Certificate delete stuck**: If a certificate delete returns 202 and subsequent GETs show `deleteFailed` provisioning state, proactively suggest the cancelDelete endpoint.
- **ETag mismatch (412 Precondition Failed)**: Surface when conditional updates on pools or certificates are rejected due to stale ETags -- the resource was modified concurrently.
- **Deprecated certificate endpoints**: Azure Batch certificates feature is on a deprecation path; flag usage and suggest migrating to Azure Key Vault references.
- **Pool resize errors**: After a stopResize call, check pool state for `allocationFailed` or `resizeFailed` allocation states and surface them.

## Playbook

### 1. Provision a New Batch Account

1. Check name availability: POST `.../locations/{location}/checkNameAvailability` with `{ "name": "myaccount", "type": "Microsoft.Batch/batchAccounts" }`.
2. If available, create the account: PUT `.../batchAccounts/{accountName}` with location and auto-storage configuration in the request body.
3. Poll the `Location` header URL if you receive 202 until provisioning completes (200 with `provisioningState: Succeeded`).
4. Retrieve account keys: POST `.../batchAccounts/{accountName}/listKeys`.
5. Sync auto-storage keys if using auto-storage: POST `.../batchAccounts/{accountName}/syncAutoStorageKeys`.

### 2. Deploy an Application Package

1. Create the application: PUT `.../applications/{applicationName}` with display name and default version in the body.
2. Create a version placeholder: PUT `.../applications/{applicationName}/versions/{versionName}`.
3. Upload the package binary to the `storageUrl` returned in the version response.
4. Activate the version: POST `.../versions/{versionName}/activate` with `{ "format": "zip" }`.
5. Verify: GET `.../applications/{applicationName}` and confirm `defaultVersion` and `allowUpdates` are set correctly.

### 3. Set Up and Manage a Compute Pool

1. Create the pool: PUT `.../pools/{poolName}` with VM size, scale settings, and node configuration. Include `If-None-Match: *` to prevent overwriting an existing pool.
2. Monitor provisioning: GET `.../pools/{poolName}` and check `allocationState` until it reaches `steady`.
3. To resize, PATCH `.../pools/{poolName}` with updated `scaleSettings`.
4. To stop an in-progress resize: POST `.../pools/{poolName}/stopResize`.
5. To disable autoscale: POST `.../pools/{poolName}/disableAutoScale`, then PATCH with fixed `targetDedicatedNodes`.

### 4. Manage Certificates on a Batch Account

1. List current certificates: GET `.../certificates` (use `$select` and `$filter` to narrow results).
2. Add a certificate: PUT `.../certificates/{certificateName}` with the PFX/CER data and thumbprint. Use `If-None-Match: *` for create-only semantics.
3. To update, PATCH `.../certificates/{certificateName}` with `If-Match` set to the current ETag.
4. To remove, DELETE `.../certificates/{certificateName}` -- poll if 202 is returned.
5. If delete fails, cancel it: POST `.../certificates/{certificateName}/cancelDelete`, fix the issue (e.g., remove pool references), then retry the delete.

### 5. Key Rotation

1. List current keys: POST `.../batchAccounts/{accountName}/listKeys` and note which key (`primary` or `secondary`) is active in your applications.
2. Regenerate the inactive key: POST `.../batchAccounts/{accountName}/regenerateKeys` with `{ "keyName": "Secondary" }`.
3. Update all clients to use the newly regenerated key.
4. Regenerate the old active key: POST `.../regenerateKeys` with `{ "keyName": "Primary" }`.
5. Verify connectivity with the new keys by calling GET `.../batchAccounts/{accountName}`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
