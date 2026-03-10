---
name: spec
description: "spec API skill. Use when working with spec for orders. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# spec

## Auth
No authentication required.

## Base URL
https://api.ote-godaddy.com

## Setup
1. No auth setup needed
2. GET /v1/orders -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/orders | Retrieve a list of orders for the authenticated shopper. Only one filter may be used at a time |
| GET | /v1/orders/{orderId} | Retrieve details for specified order |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all orders?" -> GET /v1/orders
- "Get order details?" -> GET /v1/orders/{orderId}

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
