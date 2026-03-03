---
name: storageimportexport
description: "StorageImportExport API skill. Use when working with StorageImportExport for providers, subscriptions. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# StorageImportExport
API version: 2016-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.ImportExport/locations -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName}/listBitLockerKeys -- create first listBitLockerKeys

## Endpoints

10 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.ImportExport/locations | Returns a list of locations to which you can ship the disks associated with an import or export job. A location is a Microsoft data center region. |
| GET | /providers/Microsoft.ImportExport/locations/{locationName} | Returns the details about a location to which you can ship the disks associated with an import or export job. A location is an Azure region. |
| GET | /providers/Microsoft.ImportExport/operations | Returns the list of operations supported by the import/export resource provider. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.ImportExport/jobs | Returns all active and completed jobs in a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs | Returns all active and completed jobs in a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName} | Gets information about an existing job. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName} | Updates specific properties of a job. You can call this operation to notify the Import/Export service that the hard drives comprising the import or export job have been shipped to the Microsoft data center. It can also be used to cancel an existing job. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName} | Creates a new job or updates an existing job in the specified subscription. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName} | Deletes an existing job. Only jobs in the Creating or Completed states can be deleted. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName}/listBitLockerKeys | Returns the BitLocker Keys for all drives in the specified job. |

## Enhanced Skill Content
## Question Mapping

- "What locations are available for import/export jobs?" -> GET /providers/Microsoft.ImportExport/locations
- "Get details about a specific import/export location" -> GET /providers/Microsoft.ImportExport/locations/{locationName}
- "List all import/export jobs in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ImportExport/jobs
- "What import/export jobs exist in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs
- "Get the status of a specific import/export job" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName}
- "Create a new import or export job" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName}
- "Update an existing import/export job" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName}
- "Delete an import/export job" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName}
- "Get the BitLocker keys for a job's drives" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName}/listBitLockerKeys
- "What operations does the Import/Export resource provider support?" -> GET /providers/Microsoft.ImportExport/operations
- "Filter jobs by status or creation date" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs (with $filter)
- "List the first N jobs in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.ImportExport/jobs (with $top)
- "Change the shipping info or return address on a job" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName}
- "Create a job specifying a client tenant ID" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName} (with x-ms-client-tenant-id)

## Response Tips

- **Locations**: Responses return location objects with supported capabilities; check for region-specific restrictions before creating jobs.
- **Job listings**: Use `$top` to limit results and `$filter` for OData filtering; paginated results include a `nextLink` property to follow.
- **Job details**: The `properties` nested object holds job state, drive list, and shipping info; always check `properties.state` for current status.
- **Job create (PUT)**: Returns 200 for updates to existing jobs and 201 for newly created ones; inspect the response code to confirm which occurred.
- **Job update (PATCH)**: Only fields included in the body are modified; the response returns the full updated job object.
- **BitLocker keys**: Returns an array of key-drive pairs; each entry maps a drive ID to its encryption key.
- **Errors**: Azure returns `ErrorResponse` with `error.code` and `error.message`; common codes include `InvalidParameter`, `ResourceNotFound`, and `SubscriptionNotRegistered`.

## Anomaly Flags

- **Job stuck in unexpected state**: Surface if a job's `properties.state` remains in `Transferring` or `Packaging` for an unusually long period after creation.
- **Subscription not registered**: If calls return `SubscriptionNotRegistered`, proactively suggest running `az provider register --namespace Microsoft.ImportExport`.
- **Missing BitLocker keys**: Flag if `listBitLockerKeys` returns an empty array, as this may indicate drives have not been processed yet.
- **Deprecated API version**: Alert if `api-version=2016-11-01` triggers deprecation warnings in response headers (`x-ms-deprecation` or `Sunset` headers).
- **Throttling (429)**: Surface rate-limit headers (`Retry-After`, `x-ms-ratelimit-remaining-subscription-reads`) when approaching limits, and pause before retrying.
- **201 on PUT when 200 expected**: If a PUT intended as an update returns 201, flag that a new job was created rather than updating the existing one -- likely a name mismatch.

## Playbook

### 1. Create a New Import Job

1. Call GET /providers/Microsoft.ImportExport/locations to list available locations.
2. Select the location nearest to your storage account or shipping origin.
3. Call PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ImportExport/jobs/{jobName} with a body containing job type (`Import`), storage account details, drive list, return address, and shipping info.
4. Confirm the response is 201 (created). Save the job name for tracking.
5. Call GET .../jobs/{jobName} periodically to monitor `properties.state` until it reaches `Completed`.

### 2. Retrieve BitLocker Keys for Drive Preparation

1. Call GET .../jobs/{jobName} to verify the job exists and has drives assigned.
2. Call POST .../jobs/{jobName}/listBitLockerKeys to retrieve encryption keys.
3. Map each returned key to its corresponding drive ID.
4. Use the keys with the Azure Import/Export tool (WAImportExport) to encrypt or unlock drives.

### 3. Update Shipping Information on an Active Job

1. Call GET .../jobs/{jobName} to retrieve the current job state and verify it accepts updates.
2. Call PATCH .../jobs/{jobName} with a body containing only the updated fields (e.g., `properties.deliveryPackage` with the new tracking number and carrier).
3. Confirm the 200 response and verify the updated fields in the returned job object.

### 4. List and Filter Jobs Across a Subscription

1. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.ImportExport/jobs with `$filter=properties/state eq 'Active'` to find active jobs.
2. Use `$top=10` to page through results if the subscription has many jobs.
3. If the response includes a `nextLink`, follow it to retrieve the next page.
4. For deeper inspection, call GET .../jobs/{jobName} on individual results to get full details including drive status.

### 5. Clean Up Completed Jobs

1. Call GET .../jobs in the target resource group with `$filter=properties/state eq 'Completed'`.
2. For each completed job, call POST .../jobs/{jobName}/listBitLockerKeys and archive the keys if needed.
3. Call DELETE .../jobs/{jobName} to remove each completed job.
4. Verify each DELETE returns 200. If a job returns an error, check whether it is still in a transitional state.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
