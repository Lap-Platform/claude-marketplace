---
name: monitormanagementclient
description: "MonitorManagementClient API skill. Use when working with MonitorManagementClient for {resourceUri}. Covers 4 endpoints."
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
2. GET /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceUri}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings/{name} | Gets the active diagnostic settings for the specified resource. |
| PUT | /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings/{name} | Creates or updates diagnostic settings for the specified resource. |
| DELETE | /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings/{name} | Deletes existing diagnostic settings for the specified resource. |
| GET | /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings | Gets the active diagnostic settings list for the specified resource. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get diagnosticSetting details?" -> GET /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings/{name}
- "Update a diagnosticSetting?" -> PUT /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings/{name}
- "Delete a diagnosticSetting?" -> DELETE /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings/{name}
- "List all diagnosticSettings?" -> GET /{resourceUri}/providers/Microsoft.Insights/diagnosticSettings
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
