---
name: authorizationmanagementclient
description: "AuthorizationManagementClient API skill. Use when working with AuthorizationManagementClient for subscriptions, {scope}, {denyAssignmentId}. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# AuthorizationManagementClient
API version: 2018-07-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/denyAssignments -- verify access

## Endpoints

6 endpoints across 3 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/denyAssignments | Gets deny assignments for a resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/denyAssignments | Gets deny assignments for a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/denyAssignments | Gets all deny assignments for the subscription. |

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{scope}/providers/Microsoft.Authorization/denyAssignments/{denyAssignmentId} | Get the specified deny assignment. |
| GET | /{scope}/providers/Microsoft.Authorization/denyAssignments | Gets deny assignments for a scope. |

### {denyAssignmentId}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{denyAssignmentId} | Gets a deny assignment by ID. |

## Enhanced Skill Content
## Question Mapping

- "What deny assignments exist in my subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/denyAssignments
- "List deny assignments for a specific resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/denyAssignments
- "What deny assignments apply to a particular resource?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/denyAssignments
- "Get details of a specific deny assignment by its ID?" -> GET /{denyAssignmentId}
- "Look up a deny assignment within a given scope?" -> GET /{scope}/providers/Microsoft.Authorization/denyAssignments/{denyAssignmentId}
- "List all deny assignments at a custom scope?" -> GET /{scope}/providers/Microsoft.Authorization/denyAssignments
- "Are there deny assignments blocking actions on my storage account?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/denyAssignments
- "Filter deny assignments by principal ID in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/denyAssignments (with $filter)
- "Which deny assignments apply at management group scope?" -> GET /{scope}/providers/Microsoft.Authorization/denyAssignments
- "Does a specific deny assignment still exist?" -> GET /{denyAssignmentId}
- "What deny assignments affect a child resource path?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/denyAssignments
- "How do I check inherited deny assignments on a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/denyAssignments (with $filter for atScope() or inherited)

## Response Tips

- **List endpoints** (subscription, resource group, resource, scope): Returns a `value` array of deny assignment objects; check for `nextLink` to handle pagination across large result sets.
- **Get-by-ID endpoints** (direct ID or scoped): Returns a single deny assignment object; a 404 means the assignment was deleted or the ID is wrong -- verify the fully qualified resource ID format.
- **All endpoints**: The `$filter` parameter supports OData expressions like `atScope()`, `denyAssignmentNameEq('{name}')`, and `principalId eq '{id}'` -- combine these to narrow results.
- **Deny assignment objects**: Key nested fields are `properties.permissions` (array of actions/notActions/dataActions/notDataActions) and `properties.principals` (array with `id` and `type`) -- always inspect both to understand the full restriction.
- **Error responses**: Azure returns `ErrorResponse` with `error.code` and `error.message` -- common codes are `AuthorizationFailed` (missing Reader or higher role) and `InvalidFilterClauseValue`.

## Anomaly Flags

- **Deny assignment with empty principals array**: May indicate a system-managed deny assignment (e.g., Azure Blueprints) -- surface this since it affects all users and cannot be removed manually.
- **Large result sets with nextLink present**: Pagination required; warn the user if results are truncated and offer to fetch remaining pages.
- **Deny assignments blocking wildcard actions (`*`)**: Flag any deny assignment where `permissions[].actions` contains `*` as this blocks nearly all control plane operations on the scope.
- **Deny assignments with `excludePrincipals` set**: Important to surface since some principals bypass the deny -- the user may mistakenly believe the deny is universal.
- **`doNotApplyToChildScopes` flag**: When `true`, the deny assignment only applies at the exact scope and not below -- flag this to avoid confusion about inheritance behavior.
- **HTTP 403 vs 404 ambiguity**: A 403 on a get-by-ID may mean the deny assignment exists but the caller lacks read permissions -- surface this distinction rather than assuming it does not exist.

## Playbook

### 1. Audit All Deny Assignments Across a Subscription

1. Call GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/denyAssignments to list all deny assignments.
2. Check the response for a `nextLink` property; if present, follow it to retrieve additional pages.
3. For each deny assignment, inspect `properties.principals` to identify who is blocked and `properties.permissions` to see which actions are denied.
4. Note any entries where `properties.isSystemProtected` is `true` -- these are managed by Azure services and cannot be modified.
5. Export results for review, flagging any assignments with wildcard (`*`) denied actions.

### 2. Diagnose Why a User Cannot Perform an Action

1. Identify the target resource's full scope (subscription, resource group, or resource path).
2. Call the appropriate list endpoint for that scope to retrieve all deny assignments.
3. Add `$filter=principalId eq '{userId}'` to narrow results to the affected user.
4. Review returned deny assignments: check `properties.permissions` for the specific action being blocked.
5. Check `properties.excludePrincipals` to see if a bypass exists, and verify `doNotApplyToChildScopes` to confirm inheritance behavior.

### 3. Inspect a Specific Deny Assignment

1. If you have the fully qualified deny assignment ID, call GET /{denyAssignmentId} directly.
2. If you only have the short name and scope, call GET /{scope}/providers/Microsoft.Authorization/denyAssignments/{denyAssignmentId} with both parameters.
3. Review `properties.description` for context on why the deny was created.
4. Check `properties.createdBy` and `properties.createdOn` to determine origin and age.
5. If `isSystemProtected` is `true`, document that removal requires deleting the parent Azure resource (e.g., Blueprint assignment).

### 4. Compare Deny Assignments Between Two Resource Groups

1. Call GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName1}/providers/Microsoft.Authorization/denyAssignments for the first resource group.
2. Call GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName2}/providers/Microsoft.Authorization/denyAssignments for the second resource group.
3. Collect deny assignment names and scopes from both responses.
4. Diff the two lists: identify assignments unique to each group and shared assignments inherited from the subscription level.
5. For any discrepancies, check whether the deny assignment uses `doNotApplyToChildScopes` which would explain scope-limited behavior.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
