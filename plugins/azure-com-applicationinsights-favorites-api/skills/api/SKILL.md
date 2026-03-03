---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 5 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites | Gets a list of favorites defined within an Application Insights component. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId} | Get a single favorite by its FavoriteId, defined within an Application Insights component. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId} | Adds a new favorites to an Application Insights component. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId} | Updates a favorite that has already been added to an Application Insights component. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId} | Remove a favorite that is associated to an Application Insights component. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all favorites for an Application Insights component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites
- "How do I filter favorites by type (shared vs user)?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites (use `favoriteType` param)
- "How do I get favorites from a specific source like notebooks or retention?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites (use `sourceType` param)
- "Can I fetch the full content of favorites in the list?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites (set `canFetchContent=true`)
- "How do I filter favorites by tags?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites (use `tags` param)
- "How do I get a specific favorite by ID?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId}
- "How do I create a new favorite?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId}
- "How do I replace an existing favorite entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId}
- "How do I update just the name or tags of a favorite without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId}
- "How do I partially modify favorite properties?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId}
- "How do I delete a favorite?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId}
- "How do I move a favorite from user-scoped to shared?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId} (update `FavoriteType` in body)
- "How do I back up all favorites for a component?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites (list all with `canFetchContent=true`, then store results)
- "How do I clone a favorite to another component?" -> GET favorite by ID from source, then PUT to target component with a new favoriteId

## Response Tips

- **List (GET collection):** Returns a flat JSON array of favorite objects, not paginated. Empty array `[]` when no favorites match filters. Each object may omit `Config` content unless `canFetchContent=true`.
- **Get/Put/Patch (single item):** Returns the full favorite object with properties like `FavoriteId`, `Name`, `Config`, `Version`, `FavoriteType`, `SourceType`, `Tags`. Check `FavoriteType` for `shared` vs `user` scope.
- **Delete:** Returns 200 on success with no meaningful body. Deleting a non-existent favorite may still return 200.
- **Errors:** Azure ARM errors follow `{ "error": { "code": "...", "message": "..." } }` structure. Common codes: `ResourceNotFound` (404), `AuthorizationFailed` (403), `InvalidSubscriptionId` (400).

## Anomaly Flags

- **403 AuthorizationFailed**: The OAuth2 token may lack the `Microsoft.Insights/components/favorites/read` or `write` permission. Surface the required RBAC role (Monitoring Reader/Contributor).
- **404 ResourceNotFound on component**: The `resourceName` (Application Insights component) does not exist or is in a different resource group. Suggest verifying the resource path.
- **Shared favorite write failures**: Writing shared favorites requires elevated permissions (Contributor role). If a PUT/PATCH fails on a shared favorite but works for user favorites, flag the permission gap.
- **Empty list with filters**: When the list returns empty, surface which filters were applied (`favoriteType`, `sourceType`, `tags`) since the combination may be too restrictive.
- **Stale favoriteId on PUT**: PUT is a full replace. If an agent calls PUT with incomplete `favoriteProperties`, it will overwrite existing fields. Flag when a PUT body is missing fields that existed in the previous GET response.
- **API version mismatch**: This spec uses `2015-05-01`. If the user references newer favorite features (e.g., workbook integration), flag that a newer API version may be needed.

## Playbook

### 1. List and Inspect All Shared Favorites

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites` with `favoriteType=shared` and `canFetchContent=true`
2. Parse the returned array of favorite objects
3. For each favorite, check `SourceType` to categorize (e.g., notebook, retention, events)
4. Use `Tags` to further group or filter results as needed

### 2. Create a New Favorite

1. Generate a unique `favoriteId` (GUID format recommended)
2. Build the `favoriteProperties` body with required fields: `Name`, `Config` (the saved query/view JSON), `FavoriteType` (`shared` or `user`), and optionally `SourceType` and `Tags`
3. Call PUT `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId}` with the body
4. Verify the 200 response returns the created favorite with matching properties

### 3. Update a Favorite Without Data Loss

1. Call GET `/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/favorites/{favoriteId}` to retrieve the current state
2. Modify only the fields you want to change in the returned object
3. Call PATCH (not PUT) with the modified `favoriteProperties` to apply a partial update
4. Verify the response reflects the expected changes while preserving unmodified fields

### 4. Back Up and Restore Favorites Across Components

1. Call GET on the source component's favorites with `canFetchContent=true` to get all favorites with full content
2. Store the returned array locally (each object contains `Config`, `Name`, `Tags`, etc.)
3. For each favorite, generate a new `favoriteId` and call PUT on the target component's favorites endpoint with the saved properties
4. Verify each PUT returns 200 and compare the count of source vs. successfully restored favorites

### 5. Clean Up Unused User Favorites

1. Call GET with `favoriteType=user` to list all user-scoped favorites
2. Review each favorite's `Name`, `Tags`, and `TimeModified` to identify stale entries
3. For each favorite to remove, call DELETE with the `favoriteId`
4. Re-run the list call to confirm the favorites have been removed


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
