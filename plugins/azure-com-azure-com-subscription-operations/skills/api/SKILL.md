---
name: subscriptionclient
description: "SubscriptionClient API skill. Use when working with SubscriptionClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# SubscriptionClient
API version: 2018-03-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Subscription/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Subscription/operations | Lists all of the available Microsoft.Subscription API operations. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all operations?" -> GET /providers/Microsoft.Subscription/operations
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
