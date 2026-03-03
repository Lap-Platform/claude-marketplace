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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults/{operation} | Returns the status of a storage operation. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults | Returns a list of all storage operation results at a location. |

## Enhanced Skill Content
## Question Mapping

- "What is the status of my storage operation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults/{operation}
- "Did my storage operation complete successfully?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults/{operation}
- "List all storage operation results in a fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults
- "Show me pending storage operations" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults
- "Has my fabric storage migration finished?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults/{operation}
- "Why did my storage operation fail?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults/{operation}
- "Are there any failed storage operations in my location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults
- "Get the result of operation {operationId}" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults/{operation}
- "How many storage operations have run in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults
- "Check if a specific storage operation exists" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults/{operation}
- "What storage operations were triggered recently?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults
- "Poll for storage operation completion" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/storageOperationResults/{operation}

## Response Tips

- **Single operation result (GET .../{operation})**: Response contains the operation status object with provisioning state. A 404 means the operation ID is invalid or has expired -- operation results are not retained indefinitely.
- **Operation results list (GET .../storageOperationResults)**: Returns an array of operation result objects. Watch for `nextLink` pagination on large result sets; follow it until absent. Empty array means no operations have been recorded for that location.

## Anomaly Flags

- **404 on a known operation ID**: The operation result may have been purged after its retention window. Surface this to the user rather than silently failing.
- **Stuck operations**: When polling a single operation, flag if the status remains non-terminal (e.g., "InProgress") across multiple checks spanning several minutes.
- **Empty result sets**: If the list endpoint returns zero results for a location that should have activity, flag a possible misconfigured location name or resource group.
- **API version mismatch**: This spec uses `2016-05-01`. If Azure returns errors about unsupported API versions, surface that the api-version query parameter may need updating.
- **OAuth2 token expiry**: Surface 401 responses proactively -- the bearer token likely needs refresh before retrying.

## Playbook

### 1. Poll a Storage Operation to Completion

1. Trigger the storage operation via the relevant Azure Fabric API (outside this spec) and capture the operation ID from the response headers or body.
2. Call `GET .../storageOperationResults/{operation}` with the operation ID.
3. Inspect the provisioning state in the response (e.g., "Succeeded", "Failed", "InProgress").
4. If still in progress, wait 10-30 seconds and repeat step 2.
5. On success, proceed with your workflow. On failure, inspect the error details in the response body.

### 2. Audit All Storage Operations in a Location

1. Call `GET .../storageOperationResults` to retrieve the full list.
2. If the response includes a `nextLink`, follow it to fetch subsequent pages until no `nextLink` is returned.
3. Filter results by status to identify failed or stuck operations.
4. For each failed operation, call `GET .../storageOperationResults/{operation}` to get detailed error information.

### 3. Diagnose a Failed Storage Operation

1. Obtain the operation ID from your deployment logs or from the list endpoint.
2. Call `GET .../storageOperationResults/{operation}`.
3. If 404 is returned, the result has expired -- check Azure Activity Log instead.
4. If 200 is returned, read the error code and message from the response body.
5. Cross-reference the error code with Azure Fabric Admin documentation for remediation steps.

### 4. Verify Fabric Location Connectivity

1. Call `GET .../storageOperationResults` for the target location with a known-good subscription and resource group.
2. A 200 response (even with an empty array) confirms the location path is valid and accessible.
3. A 404 indicates the fabric location name, resource group, or subscription is incorrect.
4. Correct the path parameters and retry until a 200 is returned.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
