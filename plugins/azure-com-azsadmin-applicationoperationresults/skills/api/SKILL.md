---
name: fabricadminclient
description: "FabricAdminClient API skill. Use when working with FabricAdminClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# FabricAdminClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation} | Returns the status of an application operation. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults | Returns a list of all application operation results at a location. |

## Enhanced Skill Content
## Question Mapping

- "What is the status of my fabric operation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation}
- "Did my fabric provisioning complete?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation}
- "List all application operation results for a fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults
- "Show me recent fabric operations in East US" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults
- "Check if operation {id} failed or succeeded" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation}
- "Why did my fabric operation return 404?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation}
- "Are there any pending fabric operations in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults
- "Poll for completion of a long-running fabric admin operation" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation}
- "Get all operation results across a specific fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults
- "Has my fabric infrastructure change finished deploying?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation}
- "Audit which fabric admin operations ran recently" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults
- "Retrieve the result of a specific async fabric operation by ID" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation}

## Response Tips

- **Single operation result (by {operation}):** Returns 200 with the operation status object; 404 means the operation ID does not exist or has expired -- do not retry, verify the operation ID is correct.
- **Operation results list:** Returns 200 with an array (potentially wrapped in a `value` property following Azure ARM conventions); check for a `nextLink` field to handle pagination across large result sets.
- **General Azure ARM patterns:** All responses include standard Azure envelope fields (`id`, `name`, `type`). Error responses follow the `{ "error": { "code", "message" } }` structure. Always check `provisioningState` or equivalent status fields for terminal vs. in-progress states.

## Anomaly Flags

- **404 on operation lookup:** The operation ID may have expired or been cleaned up -- surface this clearly rather than silently retrying.
- **Long-running operation still in progress:** If polling a specific operation and the status has not reached a terminal state (`Succeeded`, `Failed`, `Canceled`), flag that the operation is still running and suggest a polling interval (typically 15-30 seconds for Azure async operations).
- **API version 2016-05-01 is legacy:** This API version is from 2016. Surface a note that newer API versions may be available and recommend checking Azure documentation for updated endpoints or features.
- **Throttling (429 responses):** Azure ARM APIs enforce rate limits per subscription. If a 429 is returned, surface the `Retry-After` header value and pause before retrying.
- **Empty operation results list:** If the list endpoint returns an empty array, flag that either no operations have been triggered in the specified location or results may have been purged.

## Playbook

### 1. Poll an Async Operation to Completion

1. Capture the operation ID from the `Location` or `Azure-AsyncOperation` header of the original request that triggered the operation.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults/{operation}` with the captured operation ID.
3. Inspect the response status field (`provisioningState` or operation status).
4. If the status is `InProgress` or equivalent, wait 15-30 seconds and repeat step 2.
5. If the status is `Succeeded`, the operation is complete -- proceed with downstream logic.
6. If the status is `Failed` or `Canceled`, extract the error details and surface them.

### 2. Audit Recent Operations in a Fabric Location

1. Identify the target subscription ID, resource group, and fabric location.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/applicationOperationResults` to list all results.
3. If the response contains a `nextLink`, follow it to retrieve additional pages.
4. Filter or sort the results by timestamp or status to identify failures or unexpected operations.
5. For any operation of interest, call the single-operation endpoint with its ID to get full details.

### 3. Diagnose a Failed Operation

1. Call the list endpoint to find operations with a `Failed` status in the target fabric location.
2. Note the operation ID of the failed operation.
3. Call `GET .../applicationOperationResults/{operation}` with that ID.
4. Extract the error code and message from the response body.
5. Cross-reference the error code with Azure Fabric Admin documentation for remediation steps.

### 4. Verify Fabric Location Connectivity

1. Call the list endpoint for a known fabric location with valid subscription and resource group.
2. A 200 response (even with an empty list) confirms the location is reachable and credentials are valid.
3. A 404 or 403 indicates the location name is wrong, the resource group does not exist, or OAuth credentials lack sufficient permissions.
4. Use this as a health check before initiating new fabric operations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
