---
name: monitormanagementclient
description: "MonitorManagementClient API skill. Use when working with MonitorManagementClient for {resourceUri}. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# MonitorManagementClient
API version: 2018-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{resourceUri}/providers/Microsoft.Insights/metricDefinitions -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceUri}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceUri}/providers/Microsoft.Insights/metricDefinitions | Lists the metric definitions for the resource. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all metricDefinitions?" -> GET /{resourceUri}/providers/Microsoft.Insights/metricDefinitions
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
