---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2015-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations | Gets a list of web test locations available to this Application Insights component. |

## Enhanced Skill Content
## Question Mapping

- "What synthetic monitor locations are available for my Application Insights resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "Where can I run availability tests from?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "List all web test locations for a specific Application Insights component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "Which geographic regions support synthetic monitoring?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "How do I find the location ID to configure an availability test?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "What ping test locations does Azure provide for my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "Can I see monitor locations scoped to a specific subscription?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "What test agents are available for my Application Insights instance?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "I need to pick locations for a multi-step web test - what's available?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "Which locations should I select for global coverage in availability monitoring?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations

## Response Tips

- **Synthetic monitor locations**: Response is a flat list of location objects; each contains a display name and an ID string (e.g., `us-il-ch1-azr`) used when configuring web tests. Expect `value` as the top-level array key per Azure ARM conventions. A 404 means the Application Insights component name or resource group is wrong. A 401/403 indicates the OAuth token lacks `Microsoft.Insights/components/read` permission.

## Anomaly Flags

- **API version staleness**: This spec targets `2015-05-01`, which is a legacy version. Surface a warning if Azure returns `x-ms-deprecation` headers or if newer API versions are available.
- **Empty location list**: If the response returns zero locations, flag it -- this may indicate the Application Insights resource is in a restricted region or misconfigured.
- **Subscription quota errors**: Watch for 429 (throttling) responses with `Retry-After` headers; Azure ARM has per-subscription rate limits (typically 12000 reads/hour).
- **Authorization scope mismatch**: If a 403 is returned despite a valid token, flag that the token may be scoped to the wrong tenant or lack the Reader role on the resource group.
- **Resource not found pattern**: A 404 with error code `ResourceNotFound` vs `ResourceGroupNotFound` -- surface which path segment is wrong to speed up debugging.

## Playbook

### 1. List Available Synthetic Monitor Locations

1. Authenticate via OAuth2 to obtain a Bearer token with scope `https://management.azure.com/.default`
2. Identify your `subscriptionId`, `resourceGroupName`, and Application Insights `resourceName`
3. Call `GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations`
4. Parse the `value` array from the response to get location IDs and display names
5. Use the location IDs when creating or updating availability web tests

### 2. Validate Resource Access Before Configuring Tests

1. Call the synthetic monitor locations endpoint for your target resource
2. If 200: resource exists and you have read access -- proceed with test configuration
3. If 404: verify the resource name and resource group are correct using `az resource list`
4. If 403: check your role assignment on the resource group (need at least Reader)
5. If 401: re-authenticate, ensuring the correct tenant ID is used

### 3. Select Optimal Locations for Global Availability Coverage

1. Fetch all available synthetic monitor locations via the endpoint
2. Filter the returned locations by geographic diversity (pick one per major region: US, Europe, Asia-Pacific)
3. For each selected location, note the location ID string (e.g., `emea-gb-db3-azr`)
4. Use these IDs in your web test configuration to ensure balanced global coverage
5. Re-check available locations periodically as Azure may add or retire test agents


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
