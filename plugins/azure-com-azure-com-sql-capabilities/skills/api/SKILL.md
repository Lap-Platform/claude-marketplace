---
name: sqlmanagementclient
description: "SqlManagementClient API skill. Use when working with SqlManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# SqlManagementClient
API version: 2017-10-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Sql/locations/{locationName}/capabilities -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Sql/locations/{locationName}/capabilities | Gets the subscription capabilities available for the specified location. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all capabilities?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Sql/locations/{locationName}/capabilities
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
