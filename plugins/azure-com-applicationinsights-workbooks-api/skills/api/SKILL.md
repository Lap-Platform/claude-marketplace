---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2018-06-17-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks | Get all Workbooks defined within a specified resource group and category. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName} | Get a single workbook by its resourceName. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName} | Delete a workbook. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName} | Create a new workbook. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName} | Updates a workbook that has already been added. |

## Enhanced Skill Content
## Question Mapping

- "List all workbooks in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks
- "Get a specific workbook by name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName}
- "What workbooks exist for a given category and source?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks
- "Create a new Application Insights workbook?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName}
- "Update an existing workbook's properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName}
- "Replace a workbook entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName}
- "Delete a workbook?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName}
- "Filter workbooks by tags?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks
- "Can I fetch workbook content inline with the list?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks (set `canFetchContent=true`)
- "How do I check if a workbook exists before creating it?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName} then PUT if 404
- "Partially update a workbook's metadata without replacing the whole thing?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName}
- "How do I move a workbook to a different source?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/workbooks/{resourceName} (update `sourceId`)
- "Delete a workbook and confirm it's gone?" -> DELETE then GET to verify 404

## Response Tips

- **List (GET collection):** Returns an array of workbook objects; `category` and `sourceId` are required filters, so an empty result means no matches -- not an error. No built-in pagination in this API version; all matching workbooks return in one response.
- **Get single (GET by resourceName):** Returns the full workbook resource including properties. A 404 means the workbook does not exist in that resource group -- check the name and resource group spelling.
- **Create/Replace (PUT):** 200 means an existing workbook was replaced; 201 means a new workbook was created. Always check which status you received to confirm intent.
- **Update (PATCH):** Returns 200 with the updated workbook. `WorkbookUpdateParameters` is optional -- at minimum `sourceId` must be provided.
- **Delete (DELETE):** 201 confirms deletion was accepted; 204 means the resource was already gone or deletion completed with no content. Both are success states.

## Anomaly Flags

- **PUT returning 200 instead of 201:** Agent should warn that an existing workbook was overwritten, not created fresh -- possible unintended replacement.
- **DELETE returning 201 vs 204:** Surface when 204 is returned, as it may indicate the resource was already deleted or never existed.
- **Missing `sourceId` on list calls:** The API requires `sourceId`; omitting it produces an error. Agent should proactively prompt for it if absent.
- **OAuth2 token expiry:** Surface 401 responses immediately and suggest re-authentication, as Azure tokens typically expire after 60-90 minutes.
- **Azure throttling (429):** If rate-limited, surface the `Retry-After` header value and pause before retrying. ARM APIs enforce per-subscription limits.
- **Deprecated API version:** This spec uses `2018-06-17-preview` -- a preview version. Agent should flag this and suggest checking for GA (stable) versions.

## Playbook

### 1. Create a New Workbook

1. Choose a unique `resourceName` for the workbook.
2. Confirm the target `subscriptionId` and `resourceGroupName`.
3. Prepare `workbookProperties` (display name, serialized content, category, kind).
4. Set `sourceId` to the Application Insights component resource ID.
5. Call PUT with `resourceName`, `sourceId`, and `workbookProperties`.
6. Verify the response is 201 (created). If 200, an existing workbook was replaced.

### 2. Find and Inspect a Workbook

1. Call GET on the collection with the required `category` and `sourceId` filters.
2. Optionally add `tags` to narrow results or set `canFetchContent=true` to inline content.
3. Identify the target workbook from the returned list by name or properties.
4. Call GET with that workbook's `resourceName` to retrieve full details.

### 3. Update Workbook Metadata Without Full Replacement

1. Call GET with `resourceName` to fetch the current workbook state.
2. Identify which fields need updating (e.g., display name, tags).
3. Call PATCH with `sourceId` and a `WorkbookUpdateParameters` body containing only changed fields.
4. Verify the 200 response contains the expected updated values.

### 4. Safely Delete a Workbook

1. Call GET with `resourceName` to confirm the workbook exists and verify its identity.
2. Call DELETE with the same `resourceName`.
3. Expect 201 (deletion accepted) or 204 (already gone).
4. Optionally call GET again to confirm a 404, verifying complete removal.

### 5. Audit All Workbooks for a Source

1. Call GET on the collection with `sourceId` set to the target Application Insights resource and `category` set appropriately.
2. Set `canFetchContent=true` to retrieve full content inline.
3. Iterate through results, checking `properties.timeModified` and `properties.userId` for audit context.
4. For each workbook needing review, call GET by `resourceName` for the complete resource envelope including tags and location.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
