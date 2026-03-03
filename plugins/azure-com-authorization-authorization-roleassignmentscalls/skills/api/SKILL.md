---
name: authorizationmanagementclient
description: "AuthorizationManagementClient API skill. Use when working with AuthorizationManagementClient for subscriptions, {scope}, {roleId}. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# AuthorizationManagementClient
API version: 2018-09-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/roleAssignments -- verify access

## Endpoints

10 endpoints across 3 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/roleAssignments | Gets role assignments for a resource. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/roleAssignments | Gets role assignments for a resource group. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/roleAssignments | Gets all role assignments for the subscription. |

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName} | Deletes a role assignment. |
| PUT | /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName} | Creates a role assignment. |
| GET | /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName} | Get the specified role assignment. |
| GET | /{scope}/providers/Microsoft.Authorization/roleAssignments | Gets role assignments for a scope. |

### {roleId}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{roleId} | Deletes a role assignment. |
| PUT | /{roleId} | Creates a role assignment by ID. |
| GET | /{roleId} | Gets a role assignment by ID. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all role assignments in a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/roleAssignments
- "What role assignments exist for a specific resource?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/roleAssignments
- "How do I assign a role to a user or service principal?" -> PUT /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName}
- "How do I remove a role assignment?" -> DELETE /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName}
- "How do I get details of a specific role assignment by name?" -> GET /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName}
- "How do I list all role assignments across an entire subscription?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/roleAssignments
- "How do I list role assignments at a custom scope?" -> GET /{scope}/providers/Microsoft.Authorization/roleAssignments
- "How do I filter role assignments by principal?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/roleAssignments with $filter
- "How do I look up a role assignment by its full role ID?" -> GET /{roleId}
- "How do I update an existing role assignment?" -> PUT /{roleId}
- "How do I delete a role assignment using its role ID?" -> DELETE /{roleId}
- "How do I check what permissions a user has on a resource group?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/roleAssignments with $filter=principalId
- "How do I grant Contributor access at subscription scope?" -> PUT /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName} with scope set to /subscriptions/{id}

## Response Tips

- **List endpoints (all GET collections):** Returns a `value` array of role assignment objects; use `$filter` (OData syntax like `principalId eq '{id}'` or `atScope()`) to narrow results. Check for `nextLink` for pagination.
- **Single GET:** Returns one role assignment object with `id`, `name`, `type`, and `properties` (containing `roleDefinitionId`, `principalId`, `scope`).
- **PUT (create/assign):** Returns 201 on success with the created role assignment. A 409 means a duplicate assignment already exists at that scope.
- **DELETE:** Returns 200 if the assignment was removed, 204 if it did not exist (idempotent). Do not treat 204 as an error.
- **Errors:** All endpoints return `ErrorResponse` with `code` and `message` nested under `error`. Common codes: `AuthorizationFailed` (403), `RoleAssignmentNotFound` (404), `RoleAssignmentExists` (409).

## Anomaly Flags

- **204 on DELETE**: The role assignment was already absent. Surface this so the caller knows the state was already clean rather than assuming a deletion occurred.
- **409 Conflict on PUT**: A role assignment with the same principal, role definition, and scope already exists. Surface the existing assignment ID from the error body.
- **AuthorizationFailed errors**: The calling principal lacks `Microsoft.Authorization/roleAssignments/write` or `/delete` permission. Flag this with a suggestion to check the caller's own role assignments.
- **$filter ignored silently**: If the filter syntax is invalid, the API may return unfiltered results instead of an error. Flag when a list response is unexpectedly large after applying a filter.
- **Scope mismatch**: If a GET by roleAssignmentName returns a role assignment whose `properties.scope` differs from the requested `{scope}`, the assignment was inherited from a parent scope. Surface this inheritance.
- **Deprecated API version**: This spec uses `2018-09-01-preview`. Flag if Azure returns `x-ms-deprecation` headers indicating a newer stable version is available.

## Playbook

### 1. Grant a User Contributor Access to a Resource Group

1. Identify the user's `principalId` (object ID from Entra ID).
2. Look up the Contributor role definition ID (typically `b24988ac-6180-42a0-ab88-20f7382dd24c`).
3. Generate a new GUID for the `roleAssignmentName`.
4. PUT `/{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName}` where scope is `/subscriptions/{subId}/resourceGroups/{rgName}` and body contains `roleDefinitionId` and `principalId`.
5. Confirm 201 response and verify the returned `properties.scope` matches the intended resource group.

### 2. Audit All Role Assignments for a Subscription

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Authorization/roleAssignments` to list all assignments.
2. If `nextLink` is present, follow it to retrieve additional pages.
3. For each assignment, extract `properties.principalId`, `properties.roleDefinitionId`, and `properties.scope`.
4. Cross-reference `roleDefinitionId` values with the Role Definitions API to resolve human-readable role names.
5. Flag any assignments scoped to the subscription level (broad access) or with Owner/User Access Administrator roles.

### 3. Remove a Specific User's Access from a Resource

1. GET the role assignments at the target resource scope using `$filter=principalId eq '{targetPrincipalId}'`.
2. From the results, identify the role assignment(s) to remove by matching `roleDefinitionId`.
3. DELETE `/{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName}` for each matching assignment.
4. Verify 200 response (assignment removed) vs 204 (already absent).

### 4. Check and Replace a Role Assignment (Least Privilege Migration)

1. GET `/{scope}/providers/Microsoft.Authorization/roleAssignments` with `$filter=principalId eq '{principalId}'` to find current assignments.
2. Identify any over-privileged roles (e.g., Owner when Contributor suffices).
3. PUT a new role assignment at the same scope with the narrower `roleDefinitionId` and a new GUID name.
4. Confirm 201 response for the new assignment.
5. DELETE the original over-privileged role assignment by its `roleAssignmentName`.
6. Verify the user retains expected access by listing their assignments again.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
