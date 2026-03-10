---
name: policyclient
description: "PolicyClient API skill. Use when working with PolicyClient for subscriptions, providers. Covers 10 endpoints."
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
2. GET /providers/Microsoft.Authorization/policyDefinitions -- verify access

## Endpoints

10 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName} | Creates or updates a policy definition in a subscription. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName} | Deletes a policy definition in a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName} | Retrieves a policy definition in a subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions | Retrieves policy definitions in a subscription |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName} | Retrieves a built-in policy definition. |
| PUT | /providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName} | Creates or updates a policy definition in a management group. |
| DELETE | /providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName} | Deletes a policy definition in a management group. |
| GET | /providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName} | Retrieve a policy definition in a management group. |
| GET | /providers/Microsoft.Authorization/policyDefinitions | Retrieve built-in policy definitions |
| GET | /providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions | Retrieve policy definitions in a management group |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Update a policyDefinition?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName}
- "Delete a policyDefinition?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName}
- "Get policyDefinition details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName}
- "Get policyDefinition details?" -> GET /providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName}
- "Update a policyDefinition?" -> PUT /providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName}
- "Delete a policyDefinition?" -> DELETE /providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName}
- "Get policyDefinition details?" -> GET /providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions/{policyDefinitionName}
- "List all policyDefinitions?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions
- "List all policyDefinitions?" -> GET /providers/Microsoft.Authorization/policyDefinitions
- "List all policyDefinitions?" -> GET /providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
