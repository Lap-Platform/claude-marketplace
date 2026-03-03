---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 4 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath} | Gets a list of Analytics Items defined within an Application Insights component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item | Gets a specific Analytics Items defined within an Application Insights component. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item | Adds or Updates a specific Analytics Item within an Application Insights component. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item | Deletes a specific Analytics Items defined within an Application Insights component. |

## Enhanced Skill Content
## Question Mapping

- "What analytics items exist for my Application Insights component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}
- "List all saved queries in my App Insights resource?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}
- "How do I filter analytics items by type or scope?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath} (use `scope`, `type`, `includeContent` query params)
- "Get a specific analytics item by ID?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item
- "Retrieve an analytics item by name instead of ID?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item (pass `name` instead of `id`)
- "How do I save a new query or function to Application Insights?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item
- "Update an existing analytics item?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item (include item ID in `itemProperties`)
- "Force-overwrite an analytics item another user modified?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item (set `overrideItem` to true)
- "Delete a saved query from my App Insights component?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item
- "Remove an analytics item by name?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/microsoft.insights/components/{resourceName}/{scopePath}/item (pass `name`)
- "What scope paths are valid for analytics items?" -> scopePath is typically `analyticsItems` (shared) or `myanalyticsItems` (user-private)
- "How do I list only my private analytics items, not shared ones?" -> GET .../myanalyticsItems (use `myanalyticsItems` as scopePath)
- "Can I see the content/body of analytics items in the listing?" -> GET /.../{scopePath} (set `includeContent` to true)

## Response Tips

- **List endpoint (GET .../{scopePath})**: Returns an array of analytics item objects. Each item includes `Id`, `Name`, `Type`, `Scope`, and optionally `Content` (only when `includeContent=true`). No pagination -- results return in a single response.
- **Single item endpoints (GET/PUT/DELETE .../item)**: Returns a single analytics item object on success (200). Look for `Id`, `Version`, `TimeCreated`, and `TimeModified` fields. PUT returns the saved item with a server-assigned `Id` if new.
- **Error responses**: Azure ARM errors return a JSON body with `error.code` and `error.message`. Common codes: `ResourceNotFound` (404), `InvalidInput` (400), `SystemError` (500). Always check the nested `error.innererror` for deeper diagnostics.

## Anomaly Flags

- **409 Conflict on PUT**: Another user modified the item since you last read it. Surface this immediately and suggest using `overrideItem=true` or re-fetching before retrying.
- **Scope mismatch**: If a user queries `analyticsItems` (shared) but the item was saved under `myanalyticsItems` (private), it will appear missing. Flag when a GET-by-ID returns 404 and suggest trying the alternate scope path.
- **Missing content in listings**: If a listing returns items without `Content` fields, remind the caller that `includeContent` defaults to false and must be explicitly set.
- **Subscription/resource group 404s**: If the base path returns `ResourceGroupNotFound` or `ResourceNotFound`, surface that the component name or resource group may be incorrect before retrying item-level calls.
- **OAuth token expiry**: Azure tokens typically expire after 60-90 minutes. Flag 401 responses and prompt for token refresh rather than retrying.

## Playbook

### 1. Inventory All Saved Queries for a Component

1. GET `.../{resourceName}/analyticsItems?type=query&includeContent=true` to list shared queries with full content.
2. GET `.../{resourceName}/myanalyticsItems?type=query&includeContent=true` to list your private queries.
3. Merge both lists, deduplicating by `Id`.
4. Review `TimeModified` to identify stale or outdated queries.

### 2. Create and Share a New Analytics Query

1. PUT `.../{resourceName}/analyticsItems/item` with `itemProperties` containing `Name`, `Content` (the KQL query body), `Type` set to `query`, and `Scope` set to `shared`.
2. Confirm the response returns the item with a server-assigned `Id`.
3. GET `.../{resourceName}/analyticsItems` to verify the new item appears in the shared listing.

### 3. Safely Update an Existing Item Without Data Loss

1. GET `.../{resourceName}/analyticsItems/item?id={itemId}` to fetch the current version.
2. Note the `Version` field from the response.
3. PUT `.../{resourceName}/analyticsItems/item` with updated `itemProperties` including the original `Id` and `Version`. Leave `overrideItem` unset (defaults to false).
4. If a 409 Conflict is returned, re-fetch the item, merge changes, and retry.
5. Only set `overrideItem=true` if you intentionally want to discard the other user's changes.

### 4. Migrate Private Items to Shared Scope

1. GET `.../{resourceName}/myanalyticsItems?includeContent=true` to list all private items.
2. For each item, PUT `.../{resourceName}/analyticsItems/item` with `itemProperties` containing the item's `Name`, `Content`, `Type`, and `Scope` set to `shared`.
3. Verify each item appears via GET `.../{resourceName}/analyticsItems`.
4. DELETE `.../{resourceName}/myanalyticsItems/item?id={originalId}` to remove the private copy.

### 5. Bulk Cleanup of Stale Analytics Items

1. GET `.../{resourceName}/analyticsItems?includeContent=true` to list all shared items.
2. Filter results where `TimeModified` is older than your retention threshold.
3. For each stale item, confirm with the user before proceeding.
4. DELETE `.../{resourceName}/analyticsItems/item?id={itemId}` for each confirmed item.
5. Repeat steps 1-4 for `myanalyticsItems` to clean private items.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
