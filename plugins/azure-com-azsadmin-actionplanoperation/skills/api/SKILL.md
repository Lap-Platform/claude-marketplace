---
name: deploymentadminclient
description: "DeploymentAdminClient API skill. Use when working with DeploymentAdminClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# DeploymentAdminClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations | Lists the action plan operations |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations/{operationId} | Gets the specified action plan operation |

## Enhanced Skill Content
## Question Mapping

- "What operations are in this action plan?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations
- "List all deployment operations for plan X" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations
- "Show me the steps in action plan {planId}" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations
- "What is the status of operation {operationId}?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations/{operationId}
- "Get details for a specific deployment operation" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations/{operationId}
- "Did operation {operationId} in plan {planId} succeed?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations/{operationId}
- "How many operations does action plan {planId} have?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations
- "Which operations failed in this deployment plan?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations
- "Is my deployment still running?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations/{operationId}
- "Show the progress of action plan {planId}" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations
- "What went wrong with operation {operationId}?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations/{operationId}
- "Are all operations in plan {planId} complete?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}/operations

## Response Tips

- **Operation lists**: Response is typically an Azure ARM `value` array. Check for `nextLink` to handle pagination across large action plans. Each item contains an operation ID, status, and timestamps.
- **Single operation detail**: Returns a full resource object with `properties.provisioningState` (Succeeded, Failed, Running, Canceled). Error details nest under `properties.error.message` and `properties.error.code`.
- **Common errors**: 404 means the planId or operationId does not exist in the subscription. 403 indicates missing RBAC permissions on the subscription scope. 401 means the OAuth2 token is expired or invalid.

## Anomaly Flags

- **Failed operations**: Proactively surface any operation where `provisioningState` is `Failed` -- include the error code and message without the user having to drill in.
- **Stuck operations**: Flag operations that show `Running` status with no timestamp change over an extended period, suggesting a hung deployment.
- **Partial plan failure**: When listing operations, alert if some succeeded and others failed -- the plan may be in an inconsistent state requiring manual intervention.
- **Throttling (429)**: Azure ARM enforces per-subscription read rate limits. Surface `Retry-After` header value and back off automatically.
- **Missing subscriptionId**: Since both endpoints require it as a path parameter, flag early if the caller has not configured a subscription context.
- **Deprecated API version**: The spec uses `2019-01-01`. If Azure returns a warning header about newer API versions, surface it so the user can upgrade.

## Playbook

### 1. Monitor an Action Plan to Completion

1. Call `GET .../actionPlans/{planId}/operations` to list all operations.
2. Check each operation's `provisioningState`.
3. If any operation is still `Running`, wait and poll again (respect `Retry-After` or use 30s intervals).
4. Repeat until all operations show `Succeeded`, `Failed`, or `Canceled`.
5. Report final summary: count of succeeded, failed, and canceled operations.

### 2. Diagnose a Failed Deployment

1. Call `GET .../actionPlans/{planId}/operations` to list all operations.
2. Filter for operations with `provisioningState` equal to `Failed`.
3. For each failed operation, call `GET .../operations/{operationId}` to retrieve full error details.
4. Extract `properties.error.code` and `properties.error.message` for each.
5. Present a consolidated error report with operation IDs and failure reasons.

### 3. Verify a Deployment Completed Successfully

1. Call `GET .../actionPlans/{planId}/operations` to get all operations.
2. Follow `nextLink` pagination until all operations are collected.
3. Assert every operation has `provisioningState` equal to `Succeeded`.
4. If all succeeded, confirm the deployment is healthy. If any differ, escalate with details.

### 4. Track a Specific Long-Running Operation

1. Note the `operationId` from a previous list call or deployment trigger.
2. Call `GET .../operations/{operationId}` to get current status.
3. If `provisioningState` is `Running`, record the timestamp and poll at regular intervals.
4. Once the state transitions to a terminal value (`Succeeded`, `Failed`, `Canceled`), report the outcome and duration.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
