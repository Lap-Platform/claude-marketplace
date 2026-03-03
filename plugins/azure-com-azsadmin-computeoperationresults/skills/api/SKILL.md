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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults/{operation} | Returns the status of a compute operation. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults | Returns a list of all compute operation results at a location. |

## Enhanced Skill Content
## Question Mapping

- "What is the status of my compute operation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults/{operation}
- "Did my fabric compute operation complete?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults/{operation}
- "List all compute operation results in my fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults
- "Show me pending compute operations for a specific region" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults
- "Has operation {id} failed or succeeded?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults/{operation}
- "Which compute operations are running in resource group X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults
- "Check if a long-running fabric operation finished" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults/{operation}
- "Why did my compute operation return 404?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults/{operation}
- "Get the result of a specific async fabric admin task" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults/{operation}
- "Are there any failed compute operations in location X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults
- "Poll for completion of operation {id}" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults/{operation}
- "What compute operations happened in my subscription recently?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/computeOperationResults

## Response Tips

- **Single operation result**: A 200 response returns the operation's current state object; a 404 means the operation ID does not exist or has expired -- always confirm the operation ID and location are correct before retrying.
- **Operation list**: The list endpoint returns a paginated array; check for `nextLink` in the response body and follow it to retrieve subsequent pages until it is absent.
- **Error bodies**: Azure ARM errors follow the standard `{ "error": { "code": "...", "message": "..." } }` structure -- surface the `code` and `message` fields directly to the user.

## Anomaly Flags

- **404 on operation lookup**: The operation ID may have expired from Azure's tracking. Surface this immediately -- the user may need to re-trigger the original action.
- **Repeated in-progress state**: If polling the same operation returns an unchanged status across multiple calls, flag potential stalling and suggest checking the resource health dashboard.
- **Throttling headers**: Watch for `Retry-After` or `x-ms-ratelimit-remaining-*` headers in responses. Surface a warning when remaining calls drop below 10% of the quota.
- **API version mismatch**: This spec uses `2016-05-01`. If Azure returns errors about unsupported API versions, flag that a newer `api-version` query parameter may be required.
- **Empty operation list**: If the list endpoint returns zero results for a location where operations were expected, flag that the location name or resource group may be incorrect.
- **Long `nextLink` chains**: If pagination exceeds 5 pages, proactively notify the user of the total volume and suggest filtering by time range or status if supported.

## Playbook

### 1. Poll a Long-Running Compute Operation to Completion

1. Capture the `operation` ID from the response headers of the original action (typically the `Azure-AsyncOperation` or `Location` header).
2. Call `GET .../computeOperationResults/{operation}` with that ID.
3. If the response status is 200 and the body indicates "InProgress" or "Running", wait the interval suggested by the `Retry-After` header (default 15 seconds).
4. Repeat step 2 until the status shows "Succeeded", "Failed", or "Canceled".
5. On "Failed", extract the error details from the response body and surface them.

### 2. Audit All Compute Operations in a Fabric Location

1. Call `GET .../computeOperationResults` for the target location to list all tracked operations.
2. Follow any `nextLink` values to retrieve all pages.
3. Group results by status (succeeded, failed, in-progress).
4. For any failed operations, call the single-operation endpoint to get full error details.
5. Summarize findings: total count, failure rate, and any operations stuck in progress.

### 3. Diagnose a Missing Operation (404 Response)

1. Call `GET .../computeOperationResults/{operation}` and confirm the 404.
2. Verify the `subscriptionId`, `resourceGroupName`, and `location` path parameters are correct.
3. Call the list endpoint to check whether the operation appears under a different ID or has already completed and been purged.
4. If not found, confirm with the user whether the original triggering action completed -- the operation may never have been created.
5. Suggest re-triggering the original action if the operation is confirmed missing.

### 4. Validate Fabric Location Connectivity

1. Call `GET .../computeOperationResults` for the target location with no filters.
2. A successful 200 (even with an empty list) confirms the location, resource group, and subscription are valid and accessible.
3. If the call fails with 404 or 403, verify the fabric location name matches an active Azure Stack region.
4. Check that the OAuth2 token has the `Microsoft.Fabric.Admin/fabricLocations/read` permission.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
