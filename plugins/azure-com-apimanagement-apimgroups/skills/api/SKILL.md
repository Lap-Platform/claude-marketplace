---
name: apimanagementclient
description: "ApiManagementClient API skill. Use when working with ApiManagementClient for subscriptions. Covers 10 endpoints."
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
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups -- verify access

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups | Lists a collection of groups defined within a service instance. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId} | Gets the entity state (Etag) version of the group specified by its identifier. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId} | Gets the details of the group specified by its identifier. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId} | Creates or Updates a group. |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId} | Updates the details of the group specified by its identifier. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId} | Deletes specific group of the API Management service instance. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}/users | Lists a collection of user entities associated with the group. |
| HEAD | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}/users/{userId} | Checks that user entity specified by identifier is associated with the group entity. |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}/users/{userId} | Add existing user to existing group |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}/users/{userId} | Remove existing user from existing group. |

## Enhanced Skill Content
## Question Mapping

- "What groups exist in my API Management service?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups
- "List groups filtered by display name?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups (use $filter)
- "Does a specific group exist?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}
- "Get details of a specific group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}
- "How do I create a new group?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}
- "Update a group's properties without replacing it?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}
- "Remove a group from my API Management service?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}
- "Who belongs to a specific group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}/users
- "Is a particular user a member of a group?" -> HEAD /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}/users/{userId}
- "Add a user to a group?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}/users/{userId}
- "Remove a user from a group?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}/users/{userId}
- "How do I replace a group's configuration entirely?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups/{groupId}
- "List only external groups from an identity provider?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.ApiManagement/service/{serviceName}/groups (use $filter on type)

## Response Tips

- **Group listings (GET .../groups, GET .../users):** Responses are paged; check `nextLink` for continuation URLs and loop until absent. Use `$filter` (OData syntax) to narrow results server-side.
- **Group existence checks (HEAD .../groups/{groupId}):** Success returns 200 with no body; use status code alone to confirm existence.
- **User membership checks (HEAD .../users/{userId}):** Returns 204 if the user is in the group, 404 if not -- treat 404 as a valid "not a member" signal, not an error.
- **Create/Add operations (PUT):** 201 means a new resource was created; 200 means an existing resource was returned or updated. Branch logic on status code when idempotency matters.
- **Patch operations (PATCH .../groups/{groupId}):** Returns 204 No Content on success -- do not attempt to parse a body.
- **Delete operations (DELETE):** Returns 200 or 204; both indicate success. 200 may include the deleted resource representation, 204 will not.

## Anomaly Flags

- **404 on HEAD user-membership check:** Expected behavior (user not in group), but flag if it appears during a bulk-add workflow -- it may indicate a typo in userId.
- **Unexpected 200 on PUT (create):** If you expected to create a new group but got 200 instead of 201, the group already existed and was returned as-is. Surface this so the caller knows no creation occurred.
- **Missing nextLink on large listings:** If a group list returns many results but no `nextLink`, the service may have returned everything in one page or pagination may be misconfigured -- flag if result count seems unusually high.
- **$filter silently ignored:** If a filtered request returns the same count as an unfiltered one, the filter expression may be malformed. Azure ARM often returns unfiltered results rather than erroring on bad OData.
- **Built-in group modification attempts:** Azure APIM has immutable built-in groups (Administrators, Developers, Guests). PUT/PATCH/DELETE against these will fail -- proactively warn before attempting mutations on groupIds matching built-in names.
- **ETag / If-Match conflicts on PATCH/DELETE:** If the service returns 412 Precondition Failed, the resource was modified since last read. Surface the conflict and suggest re-fetching before retrying.

## Playbook

### 1. Create a Group and Add Users

1. PUT `.../groups/{groupId}` with `parameters` containing the group display name, description, and type.
2. Confirm 201 (created) or 200 (already exists).
3. For each user to add, PUT `.../groups/{groupId}/users/{userId}`.
4. Confirm 201 (added) or 200 (already a member) for each.
5. Verify with GET `.../groups/{groupId}/users` to list all members.

### 2. Audit Group Membership

1. GET `.../groups` to retrieve all groups (follow `nextLink` for pagination).
2. For each group, GET `.../groups/{groupId}/users` to list members.
3. Compile a map of groupId to user list.
4. Flag any groups with zero members or unexpectedly large membership counts.

### 3. Check and Remove a User from a Group

1. HEAD `.../groups/{groupId}/users/{userId}` to confirm membership (expect 204).
2. If 404, the user is not in the group -- no action needed.
3. If 204, DELETE `.../groups/{groupId}/users/{userId}`.
4. Confirm 200 or 204 (both mean success).
5. Optionally HEAD again to verify removal (expect 404).

### 4. Rename or Update a Group

1. GET `.../groups/{groupId}` to fetch current properties and the ETag header.
2. PATCH `.../groups/{groupId}` with only the fields to change (e.g., display name, description). Include `If-Match` header with the ETag.
3. Confirm 204 No Content.
4. GET `.../groups/{groupId}` again to verify the update took effect.

### 5. Clean Up Unused Groups

1. GET `.../groups` to list all groups.
2. For each group, GET `.../groups/{groupId}/users` to check membership count.
3. Identify groups with zero users (skip built-in groups: Administrators, Developers, Guests).
4. For each candidate, DELETE `.../groups/{groupId}`.
5. Confirm 200 or 204 for each deletion.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
