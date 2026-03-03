---
name: blueprintclient
description: "BlueprintClient API skill. Use when working with BlueprintClient for {resourceScope}. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# BlueprintClient
API version: 2018-11-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceScope}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations | List operations for given blueprint assignment within a subscription or a management group. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations/{assignmentOperationName} | Get a blueprint assignment operation. |

## Enhanced Skill Content
## Question Mapping

- "What operations have run for a blueprint assignment?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations
- "List all assignment operations for a specific blueprint?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations
- "Show me the history of a blueprint assignment deployment?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations
- "Get details of a specific assignment operation?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations/{assignmentOperationName}
- "What happened during a particular blueprint deployment?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations/{assignmentOperationName}
- "Did my blueprint assignment succeed or fail?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations/{assignmentOperationName}
- "What is the provisioning state of a blueprint operation?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations/{assignmentOperationName}
- "How many times has this blueprint assignment been applied?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations
- "Which blueprint operations ran at subscription scope?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations (resourceScope = subscriptions/{subId})
- "Show blueprint operations scoped to a management group?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations (resourceScope = managementGroups/{mgId})
- "What resources were deployed by a blueprint operation?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations/{assignmentOperationName}
- "Check if a blueprint assignment operation is still running?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations/{assignmentOperationName}

## Response Tips

- **List operations** (GET .../assignmentOperations): Returns a `value` array of operation objects. Check for `nextLink` to handle pagination across large operation histories.
- **Single operation** (GET .../assignmentOperations/{name}): Returns a flat operation object with `properties.provisioningState` (succeeded/failed/running/cancelled) and `properties.assignmentState`. Inspect `properties.deployments` for per-resource status breakdown.
- **Errors**: Azure ARM errors return `{ "error": { "code": "...", "message": "..." } }`. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403), `InvalidApiVersionParameter`.

## Anomaly Flags

- **Operation stuck in "running"**: Surface if a single operation's `provisioningState` remains `running` -- may indicate a hung deployment requiring manual intervention.
- **Repeated failures**: When listing operations, flag if the most recent N operations all show `failed` state -- suggests a systemic issue with the assignment definition.
- **API version mismatch**: This spec uses `2018-11-01-preview`. Flag if the caller passes a different api-version, as behavior may differ or the version may be deprecated.
- **Empty operation list**: If a known assignment returns zero operations, flag it -- the assignment may not have been triggered yet or the resourceScope may be incorrect.
- **Mixed resource scopes**: Surface a warning if the caller switches between subscription-level and management-group-level scopes mid-workflow, as results are scoped and won't overlap.

## Playbook

### 1. Audit the Full Deployment History of a Blueprint Assignment

1. Determine the `resourceScope` (e.g., `subscriptions/{subscriptionId}` or `managementGroups/{mgId}`).
2. Call `GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/assignmentOperations?api-version=2018-11-01-preview`.
3. Iterate through the `value` array. Follow `nextLink` if present to retrieve all pages.
4. Sort operations by timestamp to build a chronological deployment history.
5. Summarize success/failure counts and identify any patterns.

### 2. Diagnose a Failed Blueprint Deployment

1. List all operations for the assignment (see Playbook 1).
2. Identify the most recent operation with `provisioningState: failed`.
3. Call `GET /{resourceScope}/.../assignmentOperations/{assignmentOperationName}?api-version=2018-11-01-preview` with that operation's name.
4. Inspect `properties.deployments` for individual resource deployment statuses.
5. Look for resources with `result: failed` and read their error messages to pinpoint the root cause.

### 3. Verify a Blueprint Assignment Completed Successfully

1. Call the single-operation endpoint for the most recent operation name.
2. Check `properties.provisioningState` -- confirm it reads `succeeded`.
3. Verify `properties.assignmentState` matches the expected state.
4. Optionally, review `properties.deployments` to confirm all individual resources were provisioned.

### 4. Monitor an In-Progress Blueprint Deployment

1. List operations for the assignment and identify the operation with `provisioningState: running`.
2. Poll `GET /{resourceScope}/.../assignmentOperations/{assignmentOperationName}` at a reasonable interval (30-60s).
3. Check `provisioningState` on each poll -- continue until it transitions to `succeeded`, `failed`, or `cancelled`.
4. If the operation remains `running` beyond the expected window, flag for manual review.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
