---
name: blueprintclient
description: "BlueprintClient API skill. Use when working with BlueprintClient for {resourceScope}. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# BlueprintClient
API version: 2018-11-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments -- verify access
3. POST /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/whoIsBlueprint -- create first whoIsBlueprint

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceScope}
| Method | Path | Description |
|--------|------|-------------|
| PUT | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} | Create or update a blueprint assignment. |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} | Get a blueprint assignment. |
| DELETE | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName} | Delete a blueprint assignment. |
| POST | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/whoIsBlueprint | Get Blueprints service SPN objectId |
| GET | /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments | List blueprint assignments within a subscription or a management group. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Update a blueprintAssignment?" -> PUT /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}
- "Get blueprintAssignment details?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}
- "Delete a blueprintAssignment?" -> DELETE /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}
- "Create a whoIsBlueprint?" -> POST /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments/{assignmentName}/whoIsBlueprint
- "List all blueprintAssignments?" -> GET /{resourceScope}/providers/Microsoft.Blueprint/blueprintAssignments
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
