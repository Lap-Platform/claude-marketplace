---
name: policyclient
description: "PolicyClient API skill. Use when working with PolicyClient for {scope}, subscriptions, {policyAssignmentId}. Covers 13 endpoints."
version: 1.0.0
generator: lapsh
---

# PolicyClient
API version: 2016-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/policyAssignments -- verify access

## Endpoints

13 endpoints across 3 groups. See references/api-spec.lap for full details.

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{scope}/providers/Microsoft.Authorization/policyassignments/{policyAssignmentName} | Deletes a policy assignment. |
| PUT | /{scope}/providers/Microsoft.Authorization/policyassignments/{policyAssignmentName} | Creates a policy assignment. |
| GET | /{scope}/providers/Microsoft.Authorization/policyassignments/{policyAssignmentName} | Gets a policy assignment. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/policyAssignments | Gets policy assignments for the resource group. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/policyassignments | Gets policy assignments for a resource. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyassignments | Gets all the policy assignments for a subscription. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policydefinitions/{policyDefinitionName} | Creates or updates a policy definition. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policydefinitions/{policyDefinitionName} | Deletes a policy definition. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policydefinitions/{policyDefinitionName} | Gets the policy definition. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policydefinitions | Gets all the policy definitions for a subscription. |

### {policyAssignmentId}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{policyAssignmentId} | Deletes a policy assignment by ID. |
| PUT | /{policyAssignmentId} | Creates a policy assignment by ID. |
| GET | /{policyAssignmentId} | Gets a policy assignment by ID. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Delete a policyassignment?" -> DELETE /{scope}/providers/Microsoft.Authorization/policyassignments/{policyAssignmentName}
- "Update a policyassignment?" -> PUT /{scope}/providers/Microsoft.Authorization/policyassignments/{policyAssignmentName}
- "Get policyassignment details?" -> GET /{scope}/providers/Microsoft.Authorization/policyassignments/{policyAssignmentName}
- "List all policyAssignments?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/policyAssignments
- "List all policyassignments?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/policyassignments
- "List all policyassignments?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyassignments
- "Update a policydefinition?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policydefinitions/{policyDefinitionName}
- "Delete a policydefinition?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policydefinitions/{policyDefinitionName}
- "Get policydefinition details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policydefinitions/{policyDefinitionName}
- "List all policydefinitions?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policydefinitions
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
