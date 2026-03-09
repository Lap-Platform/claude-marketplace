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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all roleAssignments?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/roleAssignments
- "List all roleAssignments?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/roleAssignments
- "Delete a roleAssignment?" -> DELETE /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName}
- "Update a roleAssignment?" -> PUT /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName}
- "Get roleAssignment details?" -> GET /{scope}/providers/Microsoft.Authorization/roleAssignments/{roleAssignmentName}
- "List all roleAssignments?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/roleAssignments
- "List all roleAssignments?" -> GET /{scope}/providers/Microsoft.Authorization/roleAssignments
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
