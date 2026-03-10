---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Defender for Cloud
API version: 2015-06-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/allowedConnections -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/allowedConnections | Gets the list of all possible traffic between resources for the subscription |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/locations/{ascLocation}/allowedConnections | Gets the list of all possible traffic between resources for the subscription and location. |
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/locations/{ascLocation}/allowedConnections/{connectionType} | Gets the list of all possible traffic between resources for the subscription and location, based on connection type. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all allowedConnections?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/allowedConnections
- "List all allowedConnections?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/locations/{ascLocation}/allowedConnections
- "Get allowedConnection details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Security/locations/{ascLocation}/allowedConnections/{connectionType}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
