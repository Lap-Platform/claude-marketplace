---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-12-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions | Lists all policy descriptions. |

## Enhanced Skill Content
## Question Mapping

- "What policy descriptions are available for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions
- "List all policy snippets I can use in my APIM instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions
- "Which policies can I apply at the API scope?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions (with scope=Api)
- "What policies are available at the product scope?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions (with scope=Product)
- "Show me global-scope policy descriptions for my service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions (with scope=Tenant)
- "What operation-level policies can I configure?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions (with scope=Operation)
- "Can I get a list of all built-in policy snippets?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions
- "What inbound/outbound policies does Azure APIM support?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions
- "How do I find which policies apply to a specific scope in APIM?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions (with scope filter)
- "What rate-limiting or quota policies are available?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions (then filter results locally)
- "Does my APIM instance support caching policies?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions (then search results for caching)
- "List policy descriptions for service {name} in resource group {rg}?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions

## Response Tips

- **Policy Descriptions (200):** Response contains a `value` array of policy description objects. Each entry includes `name`, `id`, `type`, and `properties` with `description` and `scope` fields. No pagination -- all descriptions are returned in a single response. Check `properties.scope` to determine where each policy can be applied (All, Tenant, Product, Api, Operation).

## Anomaly Flags

- **Preview API version**: This uses `2019-12-01-preview` -- a preview version. Surface a warning that behavior may change without notice and recommend checking for GA versions.
- **Empty value array**: If the response returns `"value": []`, flag that the APIM service instance may not be properly provisioned or the scope filter may be too restrictive.
- **401/403 errors**: OAuth2 token may lack the `Microsoft.ApiManagement/service/read` permission. Surface the required RBAC role (API Management Service Reader or higher).
- **404 responses**: The subscription, resource group, or service name may be incorrect. Prompt the user to verify all three path parameters.
- **Unexpected scope values**: If the `scope` parameter is passed with a value not in {Api, Product, Tenant, Operation, All}, surface that the filter may silently return unfiltered results.

## Playbook

### 1. Discover All Available Policies for an APIM Instance

1. Authenticate with Azure using OAuth2 (ensure token has Reader access on the APIM resource).
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policyDescriptions`.
3. Parse the `value` array from the response.
4. Each item's `properties.description` explains the policy purpose and `properties.scope` shows where it can be applied.

### 2. Find Policies Available at a Specific Scope

1. Identify the target scope: `Api`, `Product`, `Operation`, or `Tenant`.
2. Call `GET .../policyDescriptions?scope={targetScope}`.
3. Review the filtered list -- only policies applicable to that scope are returned.
4. Use the policy names from the results when constructing policy XML for that scope.

### 3. Build a Policy Configuration from Descriptions

1. Call `GET .../policyDescriptions` to retrieve all available policies.
2. Identify the policies you need (e.g., rate-limit, caching, IP filtering) from the response.
3. Note each policy's supported scopes from `properties.scope`.
4. Use the policy names as references when authoring policy XML via the APIM Policy API (`PUT .../policies/{policyId}`), which is a separate endpoint not covered by this spec.

### 4. Audit Policy Availability Across Scopes

1. Call `GET .../policyDescriptions` without a scope filter to get all policies.
2. Group the results by `properties.scope` value.
3. Compare scope groups to identify policies that are scope-restricted vs. available everywhere (`All`).
4. Flag any policies marked as deprecated in their description text for removal from active configurations.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
