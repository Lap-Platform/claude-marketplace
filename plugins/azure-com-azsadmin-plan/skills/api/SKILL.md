---
name: subscriptionsmanagementclient
description: "SubscriptionsManagementClient API skill. Use when working with SubscriptionsManagementClient for subscriptions. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionsManagementClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/plans -- verify access

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/plans | List all plans across all subscriptions. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans | Get the list of plans under a resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} | Get the specified plan. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} | Create or update the plan. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} | Delete the specified plan. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metrics | Get the metrics of the specified plan. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metricDefinitions | Get the metric definitions of the specified plan. |

## Enhanced Skill Content
## Question Mapping

- "What subscription plans exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/plans
- "List all plans in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans
- "Get details of a specific plan?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "How do I create a new subscription plan?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "Update an existing plan's configuration?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "Delete a subscription plan?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "What metrics are available for a plan?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metrics
- "What metric definitions does a plan support?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metricDefinitions
- "Does a specific plan already exist before I create it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "How is a plan performing right now?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metrics
- "What units and aggregations can I query for plan metrics?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}/metricDefinitions
- "Remove a plan that is no longer needed?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}
- "Compare plans across different resource groups?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/plans (subscription-wide list)

## Response Tips

- **Plan listings** (GET .../plans): Returns an array of plan objects; may include `nextLink` for pagination -- follow it until absent. Filter client-side if no `$filter` query param is supported.
- **Single plan** (GET .../plans/{plan}): Returns the full plan definition including properties, display name, and quota. A 404 means the plan does not exist -- use this for existence checks before PUT.
- **Create/Update** (PUT .../plans/{plan}): 201 means created, 200 means updated in place. The response body contains the final state of the plan -- always read it back rather than assuming your input was stored verbatim.
- **Delete** (DELETE .../plans/{plan}): 200 means deleted, 204 means already gone (idempotent). No response body on 204.
- **Metrics and definitions** (GET .../metrics, .../metricDefinitions): Metrics return time-series data with nested value arrays; metric definitions describe available metric names, units, and supported aggregation types.

## Anomaly Flags

- **204 on DELETE**: The plan was already absent. Surface this so the caller knows the resource was not found rather than assuming successful deletion of an existing resource.
- **Casing inconsistency**: The metrics and metricDefinitions paths use lowercase `resourcegroups` while other endpoints use `resourceGroups`. Agents must use the exact casing from the spec to avoid 404s.
- **PUT returning 200 vs 201**: If the caller intended to create a new plan but receives 200, the plan already existed and was overwritten. Flag this as a potential unintended update.
- **Missing planDefinition body on PUT**: The `planDefinition` map is required. A 400 response likely means the body was malformed or missing -- surface the error detail.
- **OAuth2 token expiry**: All endpoints require OAuth2. If any call returns 401, surface that the bearer token has likely expired and needs refresh before retrying.
- **Rate limiting (429)**: Azure ARM APIs enforce throttling. If a 429 is returned, surface the `Retry-After` header value and pause before retrying.

## Playbook

### 1. Create a New Subscription Plan

1. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} to check if the plan already exists.
2. If 404, proceed. If 200, decide whether to update or abort.
3. PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} with the `planDefinition` map in the request body.
4. Confirm the response is 201 (created). Read back the response body to verify the stored state.

### 2. Audit All Plans Across a Subscription

1. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/plans to retrieve all plans subscription-wide.
2. Follow any `nextLink` pagination until all pages are collected.
3. For each plan, GET .../plans/{plan}/metricDefinitions to understand what metrics are tracked.
4. GET .../plans/{plan}/metrics to pull current metric values.
5. Compile results into a summary comparing plan health and usage.

### 3. Safely Delete a Plan

1. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} to confirm the plan exists and inspect its current state.
2. GET .../plans/{plan}/metrics to check for active usage that might indicate the plan should not be removed.
3. If safe to proceed, DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan}.
4. Verify the response is 200 (deleted) or 204 (already absent).
5. Optionally, GET the plan again to confirm a 404 is returned.

### 4. Monitor Plan Health

1. GET .../plans/{plan}/metricDefinitions to discover available metrics and their aggregation types.
2. GET .../plans/{plan}/metrics to retrieve current values.
3. Compare metric values against expected thresholds (defined by your operations team).
4. If any metric exceeds thresholds, flag the plan name and metric for investigation.

### 5. Update a Plan Configuration

1. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Subscriptions.Admin/plans/{plan} to retrieve the current plan definition.
2. Modify the desired fields in the returned `planDefinition` map.
3. PUT the updated definition back to the same path.
4. Confirm the response is 200 (updated). Compare the response body against your intended changes to verify correctness.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
