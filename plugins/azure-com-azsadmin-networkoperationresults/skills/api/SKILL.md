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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults/{operation} | Returns the status of a network operation. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults | Returns a list of all network operation results at a location. |

## Enhanced Skill Content
## Question Mapping

- "What is the status of a specific network operation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults/{operation}
- "Did my network operation complete successfully?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults/{operation}
- "List all network operation results in a fabric location" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults
- "Are there any failed network operations in my fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults
- "How do I poll a long-running network operation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults/{operation}
- "What network operations have run in resource group X?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults
- "Is a specific network operation still in progress?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults/{operation}
- "Show me recent fabric network operations for location eastus" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults
- "Why did my network operation return 404?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults/{operation}
- "Can I check if a network change has propagated?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults/{operation}
- "How do I confirm a fabric infrastructure change completed?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults/{operation}
- "What operations are tracked under a given fabric location?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Fabric.Admin/fabricLocations/{location}/networkOperationResults

## Response Tips

- **Single operation result (GET .../{operation}):** Returns the operation resource with provisioning state -- check the `status` or `provisioningState` field for `Succeeded`, `Failed`, or `InProgress`. A 404 means the operation ID is invalid or has expired.
- **Operation list (GET .../networkOperationResults):** Returns a `value` array of operation result objects. May include a `nextLink` property for pagination -- follow it with subsequent GET requests until `nextLink` is absent. An empty `value` array with 200 is normal (no operations recorded).
- **Error responses (404):** Azure Resource Manager wraps errors in `{"error": {"code": "...", "message": "..."}}`. The `code` field identifies the category (e.g., `ResourceNotFound`, `ResourceGroupNotFound`). Always surface the `message` to the user.

## Anomaly Flags

- **Operation stuck in progress:** If polling a single operation and the status remains `InProgress` across multiple checks over several minutes, surface a warning that the operation may be stalled.
- **404 on a previously valid operation:** The operation result may have been cleaned up or the operation ID was transient. Flag this as a potential retention expiry rather than a bug.
- **Empty operation list:** If the list endpoint returns zero results for a location that should have activity, flag that the location name or resource group may be incorrect.
- **Azure throttling headers:** Watch for `x-ms-ratelimit-remaining-subscription-reads` in response headers. Surface a warning when remaining reads drop below 50.
- **Unexpected error codes:** Any error code other than `ResourceNotFound` or `ResourceGroupNotFound` (e.g., `AuthorizationFailed`, `SubscriptionNotFound`) should be surfaced immediately as it indicates a configuration or permissions issue, not a missing resource.

## Playbook

### 1. Poll a Long-Running Network Operation to Completion

1. Obtain the operation ID from the response headers (`Location` or `Azure-AsyncOperation`) of the original network mutation request.
2. Call `GET .../networkOperationResults/{operation}` with that ID.
3. Inspect the `status` or `provisioningState` field in the response body.
4. If `InProgress`, wait 5-10 seconds and repeat from step 2.
5. If `Succeeded`, report success and extract any result details.
6. If `Failed`, extract the error message from the response and surface it.

### 2. Audit All Network Operations in a Fabric Location

1. Call `GET .../networkOperationResults` with the target subscription, resource group, and location.
2. Iterate through the `value` array, noting each operation's status and timestamp.
3. If `nextLink` is present, follow it to retrieve additional pages.
4. Filter results by status (`Failed`, `InProgress`) to identify items needing attention.
5. For any failed operation, call the single-operation endpoint to get full error details.

### 3. Verify a Network Change Propagated Successfully

1. Trigger the network change via the appropriate Azure Fabric Admin API (outside this spec).
2. Capture the operation ID from the response.
3. Call `GET .../networkOperationResults/{operation}` to check status.
4. Confirm the status is `Succeeded`.
5. If `Failed`, read the error payload and decide whether to retry the original operation.

### 4. Diagnose a Missing Operation (404)

1. Call `GET .../networkOperationResults/{operation}` and confirm the 404 response.
2. Verify the operation ID is correct and was not truncated or miscopied.
3. Check that `subscriptionId`, `resourceGroupName`, and `location` match the original request context.
4. Call `GET .../networkOperationResults` (list) to see if the operation appears under a different ID or was already cleaned up.
5. If the operation is absent from the list, it likely expired from the results store -- re-trigger the original action if needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
