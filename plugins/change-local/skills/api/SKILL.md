---
name: api-v1
description: "API V1 API skill. Use when working with API V1 for api. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# API V1
API version: v1

## Auth
Bearer basic

## Base URL
https://api.getchange.io

## Setup
1. Set Authorization header with your Bearer token
2. GET /api/v1/donations/show -- verify access
3. POST /api/v1/donations/create -- create first create

## Endpoints

8 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| POST | /api/v1/donations/create | Create a donation |
| GET | /api/v1/donations/show | Retrieve a donation |
| GET | /api/v1/donations/index | List your donations |
| GET | /api/v1/donations/carbon_calculate | Calculate shipping carbon offset |
| GET | /api/v1/donations/crypto_calculate | Calculate crypto carbon offset |
| GET | /api/v1/donations/carbon_stats | Retrieve carbon offset stats |
| GET | /api/v1/nonprofits/show | Show a nonprofit |
| GET | /api/v1/nonprofits/list | Search a nonprofit |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a create?" -> POST /api/v1/donations/create
- "List all show?" -> GET /api/v1/donations/show
- "List all index?" -> GET /api/v1/donations/index
- "List all carbon_calculate?" -> GET /api/v1/donations/carbon_calculate
- "List all crypto_calculate?" -> GET /api/v1/donations/crypto_calculate
- "List all carbon_stats?" -> GET /api/v1/donations/carbon_stats
- "List all show?" -> GET /api/v1/nonprofits/show
- "List all list?" -> GET /api/v1/nonprofits/list
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
