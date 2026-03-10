---
name: spec
description: "spec API skill. Use when working with spec for shoppers. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# spec

## Auth
ApiKey secret in body

## Base URL
https://api.ote-godaddy.com

## Setup
1. Set your API key in the appropriate header
2. GET /v1/shoppers/{shopperId}/status -- verify access
3. POST /v1/shoppers/subaccount -- create first subaccount

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### shoppers
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/shoppers/subaccount | Create a Subaccount owned by the authenticated Reseller |
| GET | /v1/shoppers/{shopperId} | Get details for the specified Shopper |
| POST | /v1/shoppers/{shopperId} | Update details for the specified Shopper |
| DELETE | /v1/shoppers/{shopperId} | Request the deletion of a shopper profile |
| GET | /v1/shoppers/{shopperId}/status | Get details for the specified Shopper |
| PUT | /v1/shoppers/{shopperId}/factors/password | Set subaccount's password |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a subaccount?" -> POST /v1/shoppers/subaccount
- "Get shopper details?" -> GET /v1/shoppers/{shopperId}
- "Delete a shopper?" -> DELETE /v1/shoppers/{shopperId}
- "List all status?" -> GET /v1/shoppers/{shopperId}/status
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
