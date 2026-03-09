---
name: authorizationmanagementclient
description: "AuthorizationManagementClient API skill. Use when working with AuthorizationManagementClient for providers. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# AuthorizationManagementClient
API version: 2018-01-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Authorization/providerOperations -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Authorization/providerOperations/{resourceProviderNamespace} | Gets provider operations metadata for the specified resource provider. |
| GET | /providers/Microsoft.Authorization/providerOperations | Gets provider operations metadata for all resource providers. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get providerOperation details?" -> GET /providers/Microsoft.Authorization/providerOperations/{resourceProviderNamespace}
- "List all providerOperations?" -> GET /providers/Microsoft.Authorization/providerOperations
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
