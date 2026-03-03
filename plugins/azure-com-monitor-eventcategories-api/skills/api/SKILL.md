---
name: monitormanagementclient
description: "MonitorManagementClient API skill. Use when working with MonitorManagementClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# MonitorManagementClient
API version: 2015-04-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Insights/eventcategories -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Insights/eventcategories | Get the list of available event categories supported in the Activity Logs Service.<br>The current list includes the following: Administrative, Security, ServiceHealth, Alert, Recommendation, Policy. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all eventcategories?" -> GET /providers/Microsoft.Insights/eventcategories
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
