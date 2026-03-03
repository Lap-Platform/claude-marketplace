---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 7 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests -- verify access

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests | Get all Application Insights web tests defined within a specified resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName} | Get a specific Application Insights web test definition. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName} | Creates or updates an Application Insights web test definition. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName} | Creates or updates an Application Insights web test definition. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName} | Deletes an Application Insights web test. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Insights/webtests | Get all Application Insights web test alerts definitions within a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{componentName}/webtests | Get all Application Insights web tests defined for the specified component. |

## Enhanced Skill Content
## Question Mapping

- "What web tests exist in my resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests
- "Show me all web tests across my entire subscription" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Insights/webtests
- "Get the details of a specific web test" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName}
- "Which web tests are linked to a specific Application Insights component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{componentName}/webtests
- "Create a new availability web test" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName}
- "Update the configuration of an existing web test" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName}
- "Add or change tags on a web test without replacing the whole definition" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName}
- "Delete a web test I no longer need" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName}
- "How do I move a web test to a different resource group?" -> DELETE + PUT (delete from old, create in new resource group)
- "How many web tests are running against my app?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{componentName}/webtests
- "Does a specific web test already exist before I create one?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/webtests/{webTestName}
- "How do I rename a web test?" -> GET (old) + PUT (new name) + DELETE (old) -- web tests are keyed by name, so renaming requires recreation
- "Update just the tags on multiple web tests?" -> PATCH (loop per web test)

## Response Tips

- **List endpoints** (GET collection): Returns a `value` array of web test objects; check for `nextLink` property for pagination and follow it until absent.
- **Get/Put/Patch** (single resource): Returns the full `WebTestDefinition` object with `properties`, `location`, `tags`, and `id`; inspect `properties.provisioningState` for async operation status.
- **Delete**: Returns 200 if the resource was deleted, 204 if it did not exist (idempotent) -- both are success; no response body on 204.
- **Error responses**: Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure; common codes include `ResourceNotFound` (404) and `AuthorizationFailed` (403).

## Anomaly Flags

- **204 on DELETE**: The web test did not exist at deletion time -- surface this as a warning since it may indicate a stale reference or race condition.
- **Provisioning state not Succeeded**: After PUT/PATCH, if `properties.provisioningState` is `Failed` or `Creating`, flag that the web test is not yet active.
- **Empty value array**: When listing web tests for a component and getting zero results, proactively note that either no tests are linked or the componentName may be incorrect.
- **Throttling (429)**: Azure ARM enforces per-subscription rate limits; if `Retry-After` header appears, surface the wait time and pause before retrying.
- **Missing tags after PATCH**: If PATCH was used to set tags but the response shows tags were merged or dropped, flag the discrepancy -- `WebTestTags` replaces only the tags block, not the full resource.
- **Deprecated API version**: The spec uses `2015-05-01`; if Azure returns warnings about newer API versions, surface the recommendation to upgrade.

## Playbook

### 1. Set Up a New Availability Web Test

1. List existing web tests to avoid name conflicts: GET `.../webtests` in the target resource group
2. Build the `WebTestDefinition` body with required fields: `location`, `properties.SyntheticMonitorId`, `properties.Configuration.WebTest`, and `properties.Kind`
3. Create the web test: PUT `.../webtests/{webTestName}` with the definition body
4. Verify the response `properties.provisioningState` is `Succeeded`
5. Confirm it appears in the component's test list: GET `.../components/{componentName}/webtests`

### 2. Audit All Web Tests Across a Subscription

1. List all web tests subscription-wide: GET `/subscriptions/{subscriptionId}/providers/Microsoft.Insights/webtests`
2. Follow `nextLink` pagination until all results are collected
3. Group results by `resourceGroup` (extracted from the `id` field)
4. For each test, inspect `properties.Enabled` to identify disabled tests
5. Flag any tests with `provisioningState` other than `Succeeded`

### 3. Bulk-Tag Web Tests for Cost Tracking

1. List web tests in the target resource group: GET `.../webtests`
2. For each web test, send a PATCH with the updated `WebTestTags` object (e.g., `{ "tags": { "costCenter": "engineering", "env": "prod" } }`)
3. Verify each response contains the expected tags
4. If any PATCH returns an error, log it and continue with remaining tests

### 4. Safely Delete and Recreate a Web Test (Rename)

1. Retrieve the full definition of the existing test: GET `.../webtests/{oldWebTestName}`
2. Save the response body, then modify the `name` and `properties.Name` fields to the new name
3. Create the new web test: PUT `.../webtests/{newWebTestName}` with the modified definition
4. Confirm the new test has `provisioningState: Succeeded`
5. Delete the old test: DELETE `.../webtests/{oldWebTestName}`
6. Verify deletion returned 200 (existed and was removed)

### 5. Find Which Component a Web Test Reports To

1. List all Application Insights components in the resource group (via the Components API)
2. For each component, query its linked web tests: GET `.../components/{componentName}/webtests`
3. Match the target `webTestName` against each component's results
4. If no component claims the test, it may be orphaned -- flag for cleanup


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
