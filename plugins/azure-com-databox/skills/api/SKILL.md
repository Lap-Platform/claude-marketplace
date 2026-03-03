---
name: databoxmanagementclient
description: "DataBoxManagementClient API skill. Use when working with DataBoxManagementClient for providers, subscriptions. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# DataBoxManagementClient
API version: 2019-09-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.DataBox/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/availableSkus -- create first availableSkus

## Endpoints

16 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.DataBox/operations | This method gets all the operations. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/jobs | Lists all the jobs available under the subscription. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/availableSkus | This method provides the list of available skus for the given subscription and location. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/locations/{location}/availableSkus | This method provides the list of available skus for the given subscription, resource group and location. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/validateAddress | [DEPRECATED NOTICE: This operation will soon be removed] This method validates the customer shipping address and provide alternate addresses if any. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/locations/{location}/validateInputs | This method does all necessary pre-job creation validation under resource group. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/validateInputs | This method does all necessary pre-job creation validation under subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs | Lists all the jobs available under the given resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName} | Gets information about the specified job. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName} | Creates a new job with the specified parameters. Existing job cannot be updated with this API and should instead be updated with the Update job API. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName} | Deletes a job. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName} | Updates the properties of an existing job. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}/bookShipmentPickUp | Book shipment pick up. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}/cancel | CancelJob. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}/listCredentials | This method gets the unencrypted secrets related to the job. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/regionConfiguration | This API provides configuration details specific to given region/location. |

## Enhanced Skill Content
## Question Mapping

- "What operations are available for the DataBox provider?" -> GET /providers/Microsoft.DataBox/operations
- "List all DataBox jobs in my subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/jobs
- "List DataBox jobs in a specific resource group" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs
- "Get details of a specific DataBox job" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}
- "What DataBox SKUs are available in a region?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/availableSkus
- "Which SKUs are available for my resource group's location?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/locations/{location}/availableSkus
- "Create a new DataBox order" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}
- "Update an existing DataBox job" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}
- "Cancel a DataBox order" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}/cancel
- "Delete a DataBox job" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}
- "Schedule a shipment pickup for my DataBox" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}/bookShipmentPickUp
- "Get credentials for a DataBox job" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.DataBox/jobs/{jobName}/listCredentials
- "Validate a shipping address before placing an order" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/validateAddress
- "Validate all inputs before creating a job" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/validateInputs
- "Get region configuration for DataBox in a location" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/locations/{location}/regionConfiguration

## Response Tips

- **Job listings** (GET .../jobs): Paginated via `$skipToken`; when `nextLink` is present in the response, pass its token to fetch the next page. An empty list means no jobs exist in that scope.
- **Job details** (GET .../jobs/{jobName}): Use `$expand=details` to include copy progress, shipping info, and error details in the response. Without it, you get summary-level fields only.
- **Job create/update** (PUT, PATCH): 200 means completed synchronously; 202 means the operation is async -- check the `Location` or `Azure-AsyncOperation` header to poll for completion.
- **Job delete/cancel** (DELETE, POST .../cancel): 202 means deletion is in progress; 204 means the resource was already gone or cancellation succeeded with no content returned.
- **Validation endpoints** (validateAddress, validateInputs): Return structured validation results with per-field error details. A 200 does not mean valid -- inspect the `status` field inside the response body.
- **SKU and region config** (availableSkus, regionConfiguration): Returns arrays of available options filtered by location. Empty results mean the service is not available in that region.

## Anomaly Flags

- **202 responses on PUT/PATCH/DELETE**: The operation is long-running. Surface the async operation URL and remind the user to poll for completion status.
- **Empty SKU results**: No DataBox SKUs available in the requested region -- flag this before the user attempts to create a job that will fail.
- **Address validation failures**: If `validateAddress` returns alternate suggestions, surface them proactively so the user can correct before placing an order.
- **`$skipToken` present in response**: More pages of results exist. Alert the user that the listing is incomplete and offer to fetch remaining pages.
- **`If-Match` header on PATCH**: If omitted, the update may overwrite concurrent changes. Flag when the user updates a job without providing an ETag for optimistic concurrency.
- **Job stuck in transitional state**: If a GET on a job shows a status like `Dispatched` or `InProgress` for an unusual duration, surface it as potentially stuck.
- **api-version mismatch**: All calls require `api-version=2019-09-01`. Flag if a different version is used, as it may produce unexpected schema differences.

## Playbook

### 1. Place a New DataBox Order

1. Call `POST .../locations/{location}/availableSkus` to check which device types are available in your target region
2. Call `POST .../locations/{location}/validateAddress` with the destination shipping address to confirm it is valid
3. Call `POST .../locations/{location}/validateInputs` with the full job parameters to catch errors before submission
4. Call `PUT .../jobs/{jobName}` with the complete `jobResource` body to create the order
5. If you receive 202, poll the async operation URL until the job reaches a terminal state

### 2. Monitor and Manage an Active Order

1. Call `GET .../jobs/{jobName}?$expand=details` to retrieve full job status including copy progress and shipping tracking
2. If the device has arrived and data copy is complete, call `POST .../jobs/{jobName}/bookShipmentPickUp` with pickup date/time details
3. If the order is no longer needed, call `POST .../jobs/{jobName}/cancel` with a `cancellationReason` body

### 3. Retrieve Device Credentials

1. Call `GET .../jobs/{jobName}` to confirm the job exists and is in a state where credentials are available (e.g., `Delivered`)
2. Call `POST .../jobs/{jobName}/listCredentials` to retrieve unlock passwords and share credentials for the device
3. Store credentials securely -- they grant direct access to the DataBox device

### 4. Audit All Jobs Across a Subscription

1. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.DataBox/jobs` to list all jobs at the subscription level
2. If the response includes a `nextLink`, extract the `$skipToken` and repeat the call to fetch subsequent pages
3. For each job requiring detailed inspection, call `GET .../jobs/{jobName}?$expand=details`
4. Aggregate statuses to identify jobs that are stuck, cancelled, or errored

### 5. Update a Job Before Shipment

1. Call `GET .../jobs/{jobName}` to retrieve the current job state and its `ETag` header
2. Confirm the job is still in a modifiable state (e.g., `DeviceOrdered`, not yet `Dispatched`)
3. Call `PATCH .../jobs/{jobName}` with the `jobResourceUpdateParameter` body and set `If-Match` to the ETag value
4. If you receive 202, poll the async operation URL until the update completes
5. Call `GET .../jobs/{jobName}` again to verify the changes took effect


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
