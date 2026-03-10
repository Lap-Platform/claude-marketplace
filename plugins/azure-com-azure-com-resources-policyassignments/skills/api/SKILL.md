---
name: policyclient
description: "PolicyClient API skill. Use when working with PolicyClient for {scope}, subscriptions, {policyAssignmentId}. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# PolicyClient
API version: 2019-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/policyAssignments -- verify access

## Endpoints

9 endpoints across 3 groups. See references/api-spec.lap for full details.

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{scope}/providers/Microsoft.Authorization/policyAssignments/{policyAssignmentName} | Deletes a policy assignment. |
| PUT | /{scope}/providers/Microsoft.Authorization/policyAssignments/{policyAssignmentName} | Creates or updates a policy assignment. |
| GET | /{scope}/providers/Microsoft.Authorization/policyAssignments/{policyAssignmentName} | Retrieves a policy assignment. |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/policyAssignments | Retrieves all policy assignments that apply to a resource group. |
| GET | /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/policyAssignments | Retrieves all policy assignments that apply to a resource. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyAssignments | Retrieves all policy assignments that apply to a subscription. |

### {policyAssignmentId}
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /{policyAssignmentId} | Deletes a policy assignment. |
| PUT | /{policyAssignmentId} | Creates or updates a policy assignment. |
| GET | /{policyAssignmentId} | Retrieves the policy assignment with the given ID. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Delete a policyAssignment?" -> DELETE /{scope}/providers/Microsoft.Authorization/policyAssignments/{policyAssignmentName}
- "Update a policyAssignment?" -> PUT /{scope}/providers/Microsoft.Authorization/policyAssignments/{policyAssignmentName}
- "Get policyAssignment details?" -> GET /{scope}/providers/Microsoft.Authorization/policyAssignments/{policyAssignmentName}
- "List all policyAssignments?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Authorization/policyAssignments
- "List all policyAssignments?" -> GET /subscriptions/{subscriptionId}/resourcegroups/{resourceGroupName}/providers/{resourceProviderNamespace}/{parentResourcePath}/{resourceType}/{resourceName}/providers/Microsoft.Authorization/policyAssignments
- "List all policyAssignments?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyAssignments
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
