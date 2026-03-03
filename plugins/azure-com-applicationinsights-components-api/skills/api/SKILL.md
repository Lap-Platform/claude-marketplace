---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 8 endpoints."
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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Insights/components -- verify access
3. POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/purge -- create first purge

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Insights/components | Gets a list of all Application Insights components within a subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components | Gets a list of Application Insights components within a resource group. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName} | Deletes an Application Insights component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName} | Returns an Application Insights component. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName} | Creates (or updates) an Application Insights component. Note: You cannot specify a different value for InstrumentationKey nor AppId in the Put operation. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName} | Updates an existing component's tags. To update other fields use the CreateOrUpdate method. |
| POST | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/purge | Purges data in an Application Insights component by a set of user-defined filters. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/operations/{purgeId} | Get status for an ongoing purge operation. |

## Enhanced Skill Content
## Question Mapping

- "List all Application Insights components in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Insights/components
- "What Application Insights resources exist in a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components
- "Get details for a specific Application Insights component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}
- "How do I create a new Application Insights resource?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}
- "How do I update the properties of an existing Application Insights component?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}
- "How do I add or update tags on an Application Insights component without replacing the whole resource?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}
- "Delete an Application Insights component?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}
- "How do I purge data from an Application Insights component for GDPR compliance?" -> POST /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/purge
- "Check the status of a data purge operation?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/operations/{purgeId}
- "How do I move an Application Insights resource between resource groups?" -> DELETE then PUT (recreate in target resource group)
- "How do I find the instrumentation key for my Application Insights resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}
- "How do I tag multiple Application Insights resources for cost tracking?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName} (repeat per resource)
- "Was my Application Insights component successfully deleted?" -> DELETE returns 200 (deleted) or 204 (already gone)

## Response Tips

- **List endpoints (GET .../components):** Response contains a `value` array of component objects. Check for a `nextLink` property for pagination -- follow it until absent to retrieve all results.
- **Single resource (GET/PUT/PATCH .../components/{resourceName}):** Returns the full component object. The `properties` nested object holds `InstrumentationKey`, `AppId`, `ApplicationType`, `FlowType`, and provisioning state.
- **Delete (DELETE .../components/{resourceName}):** 200 means successfully deleted; 204 means the resource did not exist. Both are success -- do not treat 204 as an error.
- **Purge (POST .../purge):** Returns 202 Accepted with an operation ID in the response headers (`x-ms-status-location`). This is async -- you must poll for completion.
- **Purge status (GET .../operations/{purgeId}):** Returns a status field. Expect `pending`, `completed`, or `failed`. Purges can take hours to finish.

## Anomaly Flags

- **202 on purge without polling:** Agent should proactively remind the user that purge is async and offer to poll the status endpoint until completion.
- **204 on delete:** Surface that the resource was already absent -- the caller may have the wrong resource name or it was already cleaned up.
- **Provisioning state not "Succeeded":** When reading a component, flag if `properties.provisioningState` is anything other than `Succeeded` (e.g., `Failed`, `Creating`) as the resource may not be ready.
- **Missing InstrumentationKey:** After a PUT/create, if the response lacks an `InstrumentationKey`, flag this as the SDK integration will not work without it.
- **Throttling (429 responses):** Azure ARM APIs enforce rate limits. If 429 is returned, surface the `Retry-After` header value and pause before retrying.
- **API version drift:** This spec targets `2015-05-01`. If Azure returns errors about unsupported API versions, flag that a newer `api-version` query parameter may be required.
- **Large subscription scans:** When listing components across an entire subscription (no resource group filter), warn that this may be slow and paginated for subscriptions with many resources.

## Playbook

### 1. Provision a New Application Insights Component

1. Choose a resource group and resource name for the new component.
2. PUT to `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}` with `InsightProperties` in the body (include `Application_Type`, `location`, and optional `tags`).
3. Confirm the response is 200 and `provisioningState` is `Succeeded`.
4. Extract the `InstrumentationKey` from the response to configure your application SDK.

### 2. GDPR Data Purge and Verification

1. POST to `.../components/{resourceName}/purge` with a body specifying the table and filter predicates for the data to remove.
2. Capture the `purgeId` from the 202 response (check `x-ms-status-location` header).
3. Poll GET `.../components/{resourceName}/operations/{purgeId}` periodically (start at 1-minute intervals).
4. Continue polling until status is `completed` or `failed`.
5. If `failed`, inspect the error details and retry with corrected filters.

### 3. Audit and Tag All Components in a Resource Group

1. GET `.../resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components` to list all components.
2. Follow `nextLink` pagination until all components are retrieved.
3. For each component missing the desired tags, PATCH `.../components/{resourceName}` with the `ComponentTags` body containing the new tag key-value pairs.
4. Verify each PATCH returns 200 with the updated tags in the response.

### 4. Decommission an Application Insights Resource

1. GET the component to confirm it exists and note its current configuration for records.
2. Export or archive any critical data (via Application Insights query API or Azure portal) before deletion.
3. DELETE `.../components/{resourceName}`.
4. If 200 is returned, the resource is removed. If 204, it was already gone.
5. Verify removal by attempting a GET on the same resource -- expect a 404.

### 5. Inventory All Application Insights Across a Subscription

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Insights/components` to list all components subscription-wide.
2. Follow `nextLink` for pagination until all results are collected.
3. Group results by `resourceGroup` from each component's `id` field.
4. For each component, extract `name`, `location`, `InstrumentationKey`, and `tags` for the inventory report.
5. Flag any components with `provisioningState` other than `Succeeded` for investigation.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
