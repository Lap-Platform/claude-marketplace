---
name: security-center
description: "Security Center API skill. Use when working with Security Center for subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Security Center
API version: 2019-08-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/iotSecuritySolutions -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/iotSecuritySolutions | Use this method to get the list of IoT Security solutions by subscription. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions | Use this method to get the list IoT Security solutions organized by resource group. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions/{solutionName} | User this method to get details of a specific IoT Security solution based on solution name |
| PUT | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions/{solutionName} | Use this method to create or update yours IoT Security solution |
| PATCH | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions/{solutionName} | Use this method to update existing IoT Security solution tags or user defined resources. To update other fields use the CreateOrUpdate method. |
| DELETE | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions/{solutionName} | Use this method to delete yours IoT Security solution |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all iotSecuritySolutions?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/iotSecuritySolutions
- "List all iotSecuritySolutions?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions
- "Get iotSecuritySolution details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions/{solutionName}
- "Update a iotSecuritySolution?" -> PUT /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions/{solutionName}
- "Partially update a iotSecuritySolution?" -> PATCH /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions/{solutionName}
- "Delete a iotSecuritySolution?" -> DELETE /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/iotSecuritySolutions/{solutionName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
