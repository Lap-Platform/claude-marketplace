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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all denyAssignments?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/denyAssignments
- "List all denyAssignments?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/denyAssignments
- "List all denyAssignments?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/denyAssignments
- "Get denyAssignment details?" -> GET /{scope}/providers/Microsoft.Authorization/denyAssignments/{denyAssignmentId}
- "List all denyAssignments?" -> GET /{scope}/providers/Microsoft.Authorization/denyAssignments
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
