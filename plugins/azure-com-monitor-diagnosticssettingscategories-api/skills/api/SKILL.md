---
name: monitormanagementclient
description: "MonitorManagementClient API skill. Use when working with MonitorManagementClient for {resourceUri}. Covers 2 endpoints."
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
2. GET /{resourceUri}/providers/Microsoft.Insights/diagnosticSettingsCategories -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceUri}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceUri}/providers/Microsoft.Insights/diagnosticSettingsCategories/{name} | Gets the diagnostic settings category for the specified resource. |
| GET | /{resourceUri}/providers/Microsoft.Insights/diagnosticSettingsCategories | Lists the diagnostic settings categories for the specified resource. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get diagnosticSettingsCategory details?" -> GET /{resourceUri}/providers/Microsoft.Insights/diagnosticSettingsCategories/{name}
- "List all diagnosticSettingsCategories?" -> GET /{resourceUri}/providers/Microsoft.Insights/diagnosticSettingsCategories
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
