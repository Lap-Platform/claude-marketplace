---
name: monitormanagementclient
description: "MonitorManagementClient API skill. Use when working with MonitorManagementClient for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# MonitorManagementClient
API version: 2016-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles/{logProfileName} | Deletes the log profile. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles/{logProfileName} | Gets the log profile. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles/{logProfileName} | Create or update a log profile in Azure Monitoring REST API. |
| PATCH | /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles/{logProfileName} | Updates an existing LogProfilesResource. To update other fields use the CreateOrUpdate method. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles | List the log profiles. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Delete a logprofile?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles/{logProfileName}
- "Get logprofile details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles/{logProfileName}
- "Update a logprofile?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles/{logProfileName}
- "Partially update a logprofile?" -> PATCH /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles/{logProfileName}
- "List all logprofiles?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Insights/logprofiles
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
