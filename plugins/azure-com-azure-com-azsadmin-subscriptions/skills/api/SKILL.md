---
name: subscriptionclient
description: "SubscriptionClient API skill. Use when working with SubscriptionClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions | Get the list of subscriptions. |
| GET | /subscriptions/{subscriptionId} | Gets details about particular subscription. |
| PUT | /subscriptions/{subscriptionId} | Create or updates a subscription. |
| DELETE | /subscriptions/{subscriptionId} | Delete the specified subscription. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all subscriptions?" -> GET /subscriptions
- "Get subscription details?" -> GET /subscriptions/{subscriptionId}
- "Update a subscription?" -> PUT /subscriptions/{subscriptionId}
- "Delete a subscription?" -> DELETE /subscriptions/{subscriptionId}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
