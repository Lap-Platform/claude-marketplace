---
name: authorizationmanagementclient
description: "AuthorizationManagementClient API skill. Use when working with AuthorizationManagementClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# AuthorizationManagementClient
API version: 2015-07-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
3. POST /providers/Microsoft.Authorization/elevateAccess -- create first elevateAccess

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| POST | /providers/Microsoft.Authorization/elevateAccess | Elevates access for a Global Administrator. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a elevateAccess?" -> POST /providers/Microsoft.Authorization/elevateAccess
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
