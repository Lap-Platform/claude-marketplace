---
name: monitormanagementclient
description: "MonitorManagementClient API skill. Use when working with MonitorManagementClient for {resourceUri}. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# MonitorManagementClient
API version: 2016-09-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{resourceUri}/providers/microsoft.insights/diagnosticSettings/service -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceUri}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceUri}/providers/microsoft.insights/diagnosticSettings/service | Gets the active diagnostic settings for the specified resource. **WARNING**: This method will be deprecated in future releases. |
| PUT | /{resourceUri}/providers/microsoft.insights/diagnosticSettings/service | Create or update new diagnostic settings for the specified resource. **WARNING**: This method will be deprecated in future releases. |
| PATCH | /{resourceUri}/providers/microsoft.insights/diagnosticSettings/service | Updates an existing ServiceDiagnosticSettingsResource. To update other fields use the CreateOrUpdate method. **WARNING**: This method will be deprecated in future releases. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all service?" -> GET /{resourceUri}/providers/microsoft.insights/diagnosticSettings/service
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
