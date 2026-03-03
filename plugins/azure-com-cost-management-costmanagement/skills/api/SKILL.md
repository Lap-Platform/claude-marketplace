---
name: costmanagementclient
description: "CostManagementClient API skill. Use when working with CostManagementClient for providers, {scope}. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# CostManagementClient
API version: 2019-04-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.CostManagement/views -- verify access

## Endpoints

13 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.CostManagement/views | Lists all views by tenant and object. |
| GET | /providers/Microsoft.CostManagement/views/{viewName} | Gets the view by view name. |
| PUT | /providers/Microsoft.CostManagement/views/{viewName} | The operation to create or update a view. Update operation requires latest eTag to be set in the request. You may obtain the latest eTag by performing a get operation. Create operation does not require eTag. |
| DELETE | /providers/Microsoft.CostManagement/views/{viewName} | The operation to delete a view. |
| GET | /providers/Microsoft.CostManagement/operations | Lists all of the available consumption REST API operations. |

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{scope}/providers/Microsoft.CostManagement/views | Lists all views at the given scope. |
| GET | /{scope}/providers/Microsoft.CostManagement/views/{viewName} | Gets the view for the defined scope by view name. |
| PUT | /{scope}/providers/Microsoft.CostManagement/views/{viewName} | The operation to create or update a view. Update operation requires latest eTag to be set in the request. You may obtain the latest eTag by performing a get operation. Create operation does not require eTag. |
| DELETE | /{scope}/providers/Microsoft.CostManagement/views/{viewName} | The operation to delete a view. |
| GET | /{scope}/providers/Microsoft.CostManagement/budgets | Lists all budgets for the defined scope. |
| GET | /{scope}/providers/Microsoft.CostManagement/budgets/{budgetName} | Gets the budget for the scope by budget name. |
| PUT | /{scope}/providers/Microsoft.CostManagement/budgets/{budgetName} | The operation to create or update a budget. Update operation requires latest eTag to be set in the request mandatorily. You may obtain the latest eTag by performing a get operation. Create operation does not require eTag. |
| DELETE | /{scope}/providers/Microsoft.CostManagement/budgets/{budgetName} | The operation to delete a budget. |

## Enhanced Skill Content
## Question Mapping

- "What cost management views exist across my tenant?" -> GET /providers/Microsoft.CostManagement/views
- "List all views for a specific subscription or resource group?" -> GET /{scope}/providers/Microsoft.CostManagement/views
- "Get the details of a specific global view?" -> GET /providers/Microsoft.CostManagement/views/{viewName}
- "Get a view scoped to a particular subscription?" -> GET /{scope}/providers/Microsoft.CostManagement/views/{viewName}
- "Create or update a global cost view?" -> PUT /providers/Microsoft.CostManagement/views/{viewName}
- "Create or update a scoped cost view for a resource group?" -> PUT /{scope}/providers/Microsoft.CostManagement/views/{viewName}
- "Delete a global cost view?" -> DELETE /providers/Microsoft.CostManagement/views/{viewName}
- "Remove a scoped cost view?" -> DELETE /{scope}/providers/Microsoft.CostManagement/views/{viewName}
- "List all budgets for a subscription?" -> GET /{scope}/providers/Microsoft.CostManagement/budgets
- "Get details of a specific budget?" -> GET /{scope}/providers/Microsoft.CostManagement/budgets/{budgetName}
- "Create or update a budget with spending limits and alerts?" -> PUT /{scope}/providers/Microsoft.CostManagement/budgets/{budgetName}
- "Delete a budget I no longer need?" -> DELETE /{scope}/providers/Microsoft.CostManagement/budgets/{budgetName}
- "What operations are available in the Cost Management API?" -> GET /providers/Microsoft.CostManagement/operations
- "How do I move a global view to be subscription-scoped?" -> GET /providers/Microsoft.CostManagement/views/{viewName} then PUT /{scope}/providers/Microsoft.CostManagement/views/{viewName}

## Response Tips

- **Views (list):** 200 returns an array of view objects; check `value[]` for results and `nextLink` for pagination across large tenants.
- **Views (get/put):** 200 means existing resource returned or updated; 201 on PUT means a new view was created. The `parameters` map defines the query definition, timeframe, and dataset configuration.
- **Views (delete):** 200 confirms deletion; 204 means the view was already absent -- both are success states, do not treat 204 as an error.
- **Budgets (list):** 200 returns scoped budgets in `value[]`; always requires `{scope}` (e.g., `subscriptions/{id}` or `resourceGroups/{name}`).
- **Budgets (get/put):** Same 200/201 pattern as views. Budget objects include `amount`, `timeGrain`, `timePeriod`, and `notifications` with threshold-based alerts.
- **Budgets (delete):** 200/204 dual success -- identical semantics to view deletion.
- **Operations:** 200 returns a flat list of available API operations with display metadata; useful for capability discovery.
- **All endpoints:** Errors follow Azure standard `ErrorResponse` with `error.code` and `error.message`. Always pass `api-version=2019-04-01-preview` as a query parameter.

## Anomaly Flags

- **Scope misconfiguration:** Surface immediately if `{scope}` is missing or malformed -- common mistake is omitting the leading `subscriptions/{subscriptionId}` prefix.
- **Preview API version:** This API uses `2019-04-01-preview` -- flag that this is a preview version and behavior may change; recommend checking for GA releases.
- **Silent deletes (204):** If a DELETE returns 204 instead of 200, warn the user the resource may not have existed -- could indicate a naming mismatch or prior deletion.
- **Budget threshold breaches:** When reading budgets, proactively check if `currentSpend` is approaching or exceeding `amount` and surface a spending alert.
- **Missing notifications on budgets:** Flag any PUT budget that lacks `notifications` configuration -- budgets without alerts provide no proactive cost warnings.
- **Rate limiting (429):** Azure throttles Cost Management requests per subscription; surface `Retry-After` header values and suggest backing off or batching operations.
- **Stale views:** If a view's dataset configuration references time ranges in the past, flag it as potentially outdated.

## Playbook

### 1. Set Up a New Subscription Budget with Alerts

1. Determine the scope: `subscriptions/{subscriptionId}`
2. GET `/{scope}/providers/Microsoft.CostManagement/budgets` to check existing budgets and avoid conflicts
3. PUT `/{scope}/providers/Microsoft.CostManagement/budgets/{budgetName}` with `parameters` including `amount`, `timeGrain` (Monthly/Quarterly/Annually), `timePeriod`, and `notifications` with threshold percentages and contact emails
4. Confirm 201 (created) or 200 (updated existing)
5. GET `/{scope}/providers/Microsoft.CostManagement/budgets/{budgetName}` to verify the budget is active with correct settings

### 2. Migrate a Global View to Subscription Scope

1. GET `/providers/Microsoft.CostManagement/views/{viewName}` to retrieve the global view definition
2. Extract the `parameters` map (query definition, dataset, timeframe) from the response
3. PUT `/{scope}/providers/Microsoft.CostManagement/views/{viewName}` with the same `parameters`, adjusting scope-specific filters as needed
4. Verify with GET `/{scope}/providers/Microsoft.CostManagement/views/{viewName}` that the scoped view returns expected data
5. Optionally DELETE `/providers/Microsoft.CostManagement/views/{viewName}` to remove the global copy

### 3. Audit All Cost Views Across the Tenant

1. GET `/providers/Microsoft.CostManagement/views` to list all global (tenant-level) views
2. For each subscription in scope, GET `/{scope}/providers/Microsoft.CostManagement/views` to list scoped views
3. Compare results to identify duplicate or orphaned views
4. For each suspect view, GET the individual view by name to inspect its query parameters and last-modified metadata
5. DELETE any views that are outdated, duplicated, or no longer aligned with current cost policies

### 4. Clean Up Unused Budgets

1. GET `/{scope}/providers/Microsoft.CostManagement/budgets` for the target subscription or resource group
2. Review each budget's `timePeriod.endDate` -- flag any with expired end dates
3. Check `currentSpend` vs `amount` -- budgets consistently at 0 spend may be attached to inactive resources
4. DELETE `/{scope}/providers/Microsoft.CostManagement/budgets/{budgetName}` for each confirmed unused budget
5. Verify deletion succeeded (200) and re-list budgets to confirm cleanup is complete

### 5. Discover Available API Operations

1. GET `/providers/Microsoft.CostManagement/operations` to retrieve all supported operations
2. Review the `display` property of each operation for human-readable descriptions
3. Cross-reference against your current usage to identify capabilities you may not be leveraging (e.g., scoped views vs global views)
4. Use the operation names to build RBAC role assignments that match your team's actual Cost Management workflow


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
