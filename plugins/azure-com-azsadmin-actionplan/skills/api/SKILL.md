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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans | Gets the list of action plans |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId} | Gets the specified action plan |

## Enhanced Skill Content
## Question Mapping

- "What action plans exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans
- "List all deployment action plans" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans
- "Show me the status of a specific action plan" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}
- "Get details for action plan X" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}
- "Are there any failed deployment plans?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans (then filter by status)
- "How many action plans are running right now?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans (then count by status)
- "What is the progress of plan {planId}?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}
- "Which action plans completed successfully?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans (then filter)
- "Show me all plans and their current state" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans
- "Is action plan {planId} still in progress?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}
- "Give me a summary of deployment activity" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans
- "What went wrong with plan {planId}?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans/{planId}

## Response Tips

- **Action plan lists**: Response is a JSON object with a `value` array. Check for `nextLink` property for pagination -- if present, follow it with another GET to retrieve the next page.
- **Single action plan**: Returns a flat resource object with `id`, `name`, `type`, and `properties`. Status and error details are nested under `properties`.
- **Errors**: Azure Resource Manager errors return `{ "error": { "code": "...", "message": "..." } }`. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403), `SubscriptionNotFound` (404).

## Anomaly Flags

- **Failed action plans**: Proactively surface any action plans where `properties.status` indicates failure or error, including the error message.
- **Stale plans**: Flag action plans that have been in a running or pending state for an unusually long time (no progress).
- **Throttling (429)**: Azure ARM applies rate limits per subscription. Surface `Retry-After` header value and warn the user before making additional calls.
- **API version mismatch**: This spec uses `2019-01-01`. If the response includes a `x-ms-api-version` header with a different value, flag the discrepancy.
- **Empty results**: If the list endpoint returns zero action plans, note this explicitly rather than silently returning nothing.
- **Deprecated resource provider**: If a 404 is returned on the provider path itself, flag that Microsoft.Deployment.Admin may not be registered on the subscription.

## Playbook

### 1. Check overall deployment health

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans` to list all plans.
2. Follow any `nextLink` values to retrieve the complete list.
3. Group plans by `properties.status` (e.g., succeeded, failed, running).
4. Report counts per status and highlight any failures.

### 2. Investigate a failed action plan

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans` and filter for plans with a failed status.
2. For each failed plan, call GET `.../actionPlans/{planId}` to retrieve full details.
3. Extract error information from `properties.error` or `properties.statusMessage`.
4. Present the plan ID, failure time, and error message to the user.

### 3. Monitor an in-progress deployment

1. Call GET `.../actionPlans/{planId}` to get current status.
2. Check `properties.status` and any progress indicators in the response.
3. If still running, wait an appropriate interval and poll again.
4. Surface completion or failure as soon as the status changes.

### 4. Verify the Deployment Admin provider is available

1. Call GET `/subscriptions/{subscriptionId}/providers/Microsoft.Deployment.Admin/locations/global/actionPlans`.
2. If a 404 with `ResourceNotFound` is returned, the provider may not be registered.
3. Advise the user to register the provider via `az provider register --namespace Microsoft.Deployment.Admin`.
4. Retry the list call after registration propagates.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
