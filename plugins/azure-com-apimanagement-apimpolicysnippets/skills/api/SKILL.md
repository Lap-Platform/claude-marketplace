---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# ApiManagementClient
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets | Lists all policy snippets. |

## Enhanced Skill Content
## Question Mapping

- "What policy snippets are available for my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets
- "Show me policy snippets scoped to a specific level" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets?scope={scope}
- "List all built-in policy templates I can use" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets
- "What policy snippets apply at the API scope?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets?scope=Api
- "Which policy snippets are available at the product level?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets?scope=Product
- "Get policy snippet examples for my APIM instance in resource group X" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets
- "What policies can I apply at the operation scope?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets?scope=Operation
- "Show me tenant-level policy snippets" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets?scope=Tenant
- "What XML snippets are available for rate limiting policies?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets
- "List policy templates I can insert into my API configuration" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets
- "Are there any policy snippets for authentication policies in my APIM service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets

## Response Tips

- **Policy Snippets (GET):** Response contains a `value` array of snippet objects, each with `name`, `content` (XML fragment), and `toolTip`. The `scope` filter narrows results but the response shape stays the same. No pagination -- all matching snippets return in a single response. Check for an empty `value` array rather than a 404 when no snippets match the requested scope.

## Anomaly Flags

- **Missing or empty `value` array:** If the response returns an empty list, the scope filter may be too restrictive or the APIM service tier may not support certain policies. Surface this to the user.
- **401/403 errors:** OAuth2 token may lack the `Microsoft.ApiManagement/service/read` permission or the subscription/resource group path is incorrect. Prompt the user to verify RBAC assignments.
- **404 on service name:** The APIM instance does not exist in the specified resource group. Suggest verifying the service name and resource group spelling.
- **api-version mismatch warnings:** If Azure returns a version-negotiation error, the `2019-01-01` API version may be deprecated for the target region. Surface the suggested version from the error body.
- **Throttling (429):** Azure ARM has per-subscription rate limits (typically 12,000 reads/hour). If approaching the limit, flag the `x-ms-ratelimit-remaining-subscription-reads` response header proactively.

## Playbook

### 1. Retrieve All Available Policy Snippets

1. Authenticate and obtain an OAuth2 bearer token with ARM read permissions.
2. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/policySnippets` with no scope filter.
3. Parse the `value` array from the response.
4. Each entry's `content` field contains an XML snippet ready to paste into a policy document.

### 2. Get Scope-Filtered Snippets for Policy Authoring

1. Determine the target scope: `Tenant`, `Product`, `Api`, or `Operation`.
2. Call the policy snippets endpoint with `?scope={targetScope}`.
3. Review returned snippets -- only those applicable at the chosen scope appear.
4. Copy the `content` XML into the appropriate `<inbound>`, `<outbound>`, `<backend>`, or `<on-error>` section of your policy document.

### 3. Audit Policy Capabilities Across Scopes

1. Call the endpoint four times, once per scope: `Tenant`, `Product`, `Api`, `Operation`.
2. Compare the `value` arrays to identify which snippets are available at each level.
3. Note any snippets exclusive to a single scope -- these indicate scope-restricted policies.
4. Document the differences to inform your API governance strategy.

### 4. Bootstrap a New API Policy from Snippets

1. Retrieve all snippets at the `Api` scope using the scope filter.
2. Identify snippets for your required policies (e.g., rate-limit, validate-jwt, cors).
3. Assemble the XML fragments into a complete policy document, placing each in the correct section.
4. Apply the assembled policy via the separate APIM policy PUT endpoint.
5. Test the API to verify the policy behaves as expected.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
