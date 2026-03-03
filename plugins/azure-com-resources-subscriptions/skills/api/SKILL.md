---
name: subscriptionclient
description: "SubscriptionClient API skill. Use when working with SubscriptionClient for providers, subscriptions, tenants. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionClient
API version: 2019-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Resources/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.Resources/checkZonePeers/ -- create first checkZonePeers

## Endpoints

7 endpoints across 3 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Resources/operations | Lists all of the available Microsoft.Resources REST API operations. |
| POST | /providers/Microsoft.Resources/checkResourceName | Checks resource name validity |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/locations | Gets all available geo-locations. |
| GET | /subscriptions/{subscriptionId} | Gets details about a specified subscription. |
| GET | /subscriptions | Gets all subscriptions for a tenant. |
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.Resources/checkZonePeers/ | Compares a subscriptions logical zone mapping |

### tenants
| Method | Path | Description |
|--------|------|-------------|
| GET | /tenants | Gets the tenants for your account. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all operations?" -> GET /providers/Microsoft.Resources/operations
- "List all locations?" -> GET /subscriptions/{subscriptionId}/locations
- "Get subscription details?" -> GET /subscriptions/{subscriptionId}
- "List all subscriptions?" -> GET /subscriptions
- "List all tenants?" -> GET /tenants
- "Create a checkZonePeer?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.Resources/checkZonePeers/
- "Create a checkResourceName?" -> POST /providers/Microsoft.Resources/checkResourceName
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
