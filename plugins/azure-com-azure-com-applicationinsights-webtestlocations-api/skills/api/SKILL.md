---
name: applicationinsightsmanagementclient
description: "ApplicationInsightsManagementClient API skill. Use when working with ApplicationInsightsManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# ApplicationInsightsManagementClient
API version: 2015-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations | Gets a list of web test locations available to this Application Insights component. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all syntheticmonitorlocations?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Insights/components/{resourceName}/syntheticmonitorlocations
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
