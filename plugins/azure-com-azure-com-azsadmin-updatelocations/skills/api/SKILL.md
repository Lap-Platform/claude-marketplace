---
name: updateadminclient
description: "UpdateAdminClient API skill. Use when working with UpdateAdminClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# UpdateAdminClient
API version: 2016-05-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/ -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/ | Get the list of update locations. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation} | Get an update location based on name. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all updateLocations?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/
- "Get updateLocation details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Update.Admin/updateLocations/{updateLocation}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
