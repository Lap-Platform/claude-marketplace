---
name: monitormanagementclient
description: "MonitorManagementClient API skill. Use when working with MonitorManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# MonitorManagementClient
API version: 2017-05-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings/{name} | Gets the active subscription diagnostic settings for the specified resource. |
| PUT | /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings/{name} | Creates or updates subscription diagnostic settings for the specified resource. |
| DELETE | /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings/{name} | Deletes existing subscription diagnostic settings for the specified resource. |
| GET | /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings | Gets the active subscription diagnostic settings list for the specified subscriptionId. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get diagnosticSetting details?" -> GET /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings/{name}
- "Update a diagnosticSetting?" -> PUT /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings/{name}
- "Delete a diagnosticSetting?" -> DELETE /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings/{name}
- "List all diagnosticSettings?" -> GET /subscriptions/{subscriptionId}/providers/microsoft.insights/diagnosticSettings
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
