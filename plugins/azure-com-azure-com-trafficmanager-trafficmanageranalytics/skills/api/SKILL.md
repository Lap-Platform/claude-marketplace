---
name: trafficmanagermanagementclient
description: "TrafficManagerManagementClient API skill. Use when working with TrafficManagerManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# TrafficManagerManagementClient
API version: 2017-09-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType} | Gets latest heatmap for Traffic Manager profile. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys | Get the subscription-level key used for Real User Metrics collection. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys | Create or update a subscription-level key used for Real User Metrics collection. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys | Delete a subscription-level key used for Real User Metrics collection. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get heatMap details?" -> GET /subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Network/trafficmanagerprofiles/{profileName}/heatMaps/{heatMapType}
- "List all trafficManagerUserMetricsKeys?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network/trafficManagerUserMetricsKeys
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
