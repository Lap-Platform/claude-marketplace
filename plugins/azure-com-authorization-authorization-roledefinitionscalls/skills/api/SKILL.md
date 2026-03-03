---
name: authorizationmanagementclient
description: "AuthorizationManagementClient API skill. Use when working with AuthorizationManagementClient for subscriptions, {scope}. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# AuthorizationManagementClient
API version: 2018-01-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Authorization/permissions -- verify access

## Endpoints

6 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Authorization/permissions | Gets all permissions the caller has for a resource group. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/permissions | Gets all permissions the caller has for a resource. |

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId} | Deletes a role definition. |
| GET | /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId} | Get role definition by name (GUID). |
| PUT | /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId} | Creates or updates a role definition. |
| GET | /{scope}/providers/Microsoft.Authorization/roleDefinitions | Get all role definitions that are applicable at scope and above. |

## Enhanced Skill Content
## Question Mapping

- "What permissions exist for a resource group?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Authorization/permissions
- "List permissions on a specific resource?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/permissions
- "What can a principal do in this resource group?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Authorization/permissions
- "Get a role definition by ID?" -> GET /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}
- "List all role definitions at a scope?" -> GET /{scope}/providers/Microsoft.Authorization/roleDefinitions
- "Create a custom role definition?" -> PUT /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}
- "Update an existing role definition?" -> PUT /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}
- "Delete a custom role definition?" -> DELETE /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}
- "Filter role definitions by name?" -> GET /{scope}/providers/Microsoft.Authorization/roleDefinitions (use $filter)
- "What built-in roles are available at subscription scope?" -> GET /{scope}/providers/Microsoft.Authorization/roleDefinitions (scope = /subscriptions/{id}, filter by type eq 'BuiltInRole')
- "Does a specific role definition exist?" -> GET /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId} (check for 200 vs error)
- "What actions does a role allow on a resource?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/permissions
- "Remove a role I no longer need?" -> DELETE /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}
- "Clone a built-in role into a custom one?" -> GET /{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId} then PUT /{scope}/providers/Microsoft.Authorization/roleDefinitions/{newId}

## Response Tips

- **Permissions endpoints**: Return `value` array of `{actions[], notActions[], dataActions[], notDataActions[]}` objects; check both action and data-action fields for complete picture. Paginated via `nextLink`.
- **Role definitions (GET single)**: Returns a single `roleDefinition` object with `properties.roleName`, `properties.type` (BuiltInRole or CustomRole), and `properties.permissions[]` array.
- **Role definitions (GET list)**: Returns `value` array; supports OData `$filter` (e.g., `roleName eq 'Contributor'` or `type eq 'CustomRole'`). Paginated via `nextLink` -- follow it until absent.
- **Role definitions (PUT)**: Returns 201 on create; request body must include `properties.roleName`, `properties.permissions`, and `properties.assignableScopes`.
- **Role definitions (DELETE)**: Returns 200 with the deleted definition body, or 204 if already absent -- both are success states; do not treat 204 as failure.
- **Errors**: All endpoints return `ErrorResponse` with `error.code` and `error.message`; watch for `AuthorizationFailed` (403-equivalent) and `RoleDefinitionDoesNotExist`.

## Anomaly Flags

- **204 on DELETE**: The role definition was already gone. Surface this so the user knows idempotent cleanup occurred rather than an actual deletion.
- **$filter ignored silently**: If the filter expression is malformed, Azure may return unfiltered results instead of an error. Flag when result count is unexpectedly large after a filtered request.
- **BuiltInRole modification attempt**: PUT against a built-in role definition ID will fail. Detect `type: BuiltInRole` in prior GET responses and warn before attempting update or delete.
- **Scope mismatch in assignableScopes**: A custom role's `assignableScopes` must include the scope where it is created. Surface a warning if the PUT body's `assignableScopes` does not contain the target scope.
- **nextLink pagination**: If a list response contains `nextLink`, surface a note that results are partial -- agents should auto-follow or inform the user.
- **Stale role definitions**: If a GET returns a role with `properties.type: CustomRole` and empty `permissions[]`, flag it as potentially misconfigured.

## Playbook

### 1. Audit Effective Permissions on a Resource Group

1. GET `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Authorization/permissions` with `api-version=2018-01-01-preview`
2. Collect all pages by following `nextLink` until absent
3. For each permission object, combine `actions` minus `notActions` for control-plane access
4. Combine `dataActions` minus `notDataActions` for data-plane access
5. Present a consolidated list of allowed and denied operations

### 2. Create a Custom Role Definition

1. GET `/subscriptions/{subscriptionId}/providers/Microsoft.Authorization/roleDefinitions` with `$filter=roleName eq 'Reader'` to use as a template
2. Copy the `properties.permissions` structure and modify `actions[]` to your needs
3. Generate a new GUID for the role definition ID
4. PUT `/{scope}/providers/Microsoft.Authorization/roleDefinitions/{newGuid}` with body containing `properties.roleName`, `properties.description`, `properties.permissions`, and `properties.assignableScopes`
5. Verify the 201 response and confirm `properties.type` is `CustomRole`

### 3. Delete a Custom Role Definition Safely

1. GET `/{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}` to confirm it exists and is `CustomRole` (not `BuiltInRole`)
2. Verify there are no active role assignments using the Authorization role assignments API (outside this spec)
3. DELETE `/{scope}/providers/Microsoft.Authorization/roleDefinitions/{roleDefinitionId}`
4. If 200: deletion confirmed, inspect returned body for audit logging
5. If 204: role was already absent, no action needed

### 4. Compare Permissions Across Resource Group and Specific Resource

1. GET permissions at resource group level: `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/Microsoft.Authorization/permissions`
2. GET permissions at resource level: `/subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{namespace}/{parentPath}/{type}/{name}/providers/Microsoft.Authorization/permissions`
3. Diff the two `actions[]` and `notActions[]` arrays to identify scope narrowing
4. Surface any permissions present at the resource group level but absent at the resource level

### 5. List and Filter Role Definitions by Type

1. GET `/{scope}/providers/Microsoft.Authorization/roleDefinitions` with `$filter=type eq 'CustomRole'` to find all custom roles
2. Follow `nextLink` pagination until complete
3. For each role, inspect `properties.permissions[].actions` to understand granted access
4. Repeat with `$filter=type eq 'BuiltInRole'` if a full inventory is needed
5. Cross-reference with assigned roles to identify unused custom definitions for cleanup


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
