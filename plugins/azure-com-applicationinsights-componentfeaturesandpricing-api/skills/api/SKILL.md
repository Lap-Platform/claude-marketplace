---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2017-10-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current | Returns the current pricing plan setting for an Application Insights component. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current | Replace current pricing plan for an Application Insights component. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current | Update current pricing plan for an Application Insights component. |

## Enhanced Skill Content
## Question Mapping

- "What pricing plan is my Application Insights resource using?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current
- "How do I check the current billing tier for an App Insights component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current
- "How do I set the pricing plan for Application Insights?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current
- "How do I switch my App Insights resource to a different pricing tier?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current
- "How do I update just the daily cap on my pricing plan without replacing the whole config?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current
- "How do I modify the data retention setting on my current plan?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current
- "What is the difference between PUT and PATCH for pricing plans?" -> PUT replaces the entire plan; PATCH updates specific fields only
- "How do I verify a pricing plan change took effect?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current (call after PUT/PATCH)
- "How do I reset my Application Insights pricing plan to defaults?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/pricingPlans/current (with default PricingPlanProperties)
- "Can I check pricing plans across multiple resource groups?" -> Loop GET over each resourceGroup/resourceName combination (no bulk endpoint exists)
- "What fields go into PricingPlanProperties?" -> Required map for PUT and PATCH; includes plan tier, daily cap, and retention settings
- "How do I audit who changed the pricing plan?" -> Not available in this API; use Azure Activity Log or Monitor APIs instead

## Response Tips

- **GET (read plan):** Returns 200 with a PricingPlanProperties object. Key fields include the plan name/tier, daily data volume cap, and stop-on-cap behavior. A missing or null field means the default applies.
- **PUT (replace plan):** Returns 200 with the full updated plan. Compare the response body against your request to confirm all fields were accepted. Omitted fields reset to defaults.
- **PATCH (partial update):** Returns 200 with the merged plan. Only fields you sent are changed; others remain untouched. Verify the response includes your changes alongside the preserved values.
- **Errors:** 404 means the component resourceName or resource group does not exist. 401/403 indicates an OAuth2 token issue or insufficient RBAC permissions. 409 may occur if a concurrent update conflicts.

## Anomaly Flags

- **404 on a known resource:** The Application Insights component may have been deleted or moved to a different resource group. Surface this immediately.
- **Unexpected plan tier in GET response:** If the returned plan does not match what was last set via PUT/PATCH, flag a possible external change (portal, CLI, or policy).
- **Daily cap near limit:** If the pricing plan response includes daily volume cap data and current ingestion is approaching it, warn that data collection may stop.
- **PUT silently resetting fields:** When a PUT response shows fields at default values that were previously customized, alert that the full-replace semantics may have wiped intentional settings.
- **Deprecated API version:** This spec uses `2017-10-01`. If Azure returns `x-ms-deprecation` headers or the response includes newer field names, flag that a migration to a newer API version may be needed.
- **OAuth2 token expiry:** If repeated 401s occur mid-workflow, surface that the bearer token has likely expired and needs refresh.

## Playbook

### 1. Check and Update a Pricing Plan

1. Call GET on `/pricingPlans/current` with the target subscriptionId, resourceGroupName, and resourceName.
2. Inspect the returned PricingPlanProperties for current tier, daily cap, and retention settings.
3. Decide whether to use PUT (full replacement) or PATCH (partial update) based on scope of change.
4. Send the PUT or PATCH request with the desired PricingPlanProperties map.
5. Call GET again to confirm the change persisted as expected.

### 2. Audit Pricing Plans Across All Resources in a Resource Group

1. Use the Azure Resource Management API (outside this spec) to list all `microsoft.insights/components` in the target resource group.
2. For each component name returned, call GET on `/pricingPlans/current`.
3. Collect and compare the PricingPlanProperties across components.
4. Flag any resources on unexpected or inconsistent tiers.

### 3. Safely Modify Daily Data Cap Without Affecting Other Settings

1. Call GET on `/pricingPlans/current` to retrieve the full current configuration.
2. Note the current daily cap and stop-on-cap values.
3. Send a PATCH request with only the daily cap field updated in PricingPlanProperties.
4. Verify the GET response shows the new cap while all other fields remain unchanged.

### 4. Restore Default Pricing Plan

1. Call GET to document the current non-default settings (for rollback reference).
2. Send a PUT request with a minimal PricingPlanProperties map containing only the default tier.
3. Confirm via GET that all fields have returned to their default values.
4. Save the previously documented settings in case a rollback is needed.

### 5. Rotate or Refresh OAuth2 Credentials Mid-Session

1. If any call returns 401, do not retry immediately.
2. Request a new OAuth2 token from your Azure AD tenant using the appropriate grant flow.
3. Retry the failed request with the refreshed bearer token.
4. If 403 persists after token refresh, verify that the service principal has the `Application Insights Component Contributor` role on the target resource.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
