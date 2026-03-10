---
name: keyvaultmanagementclient
description: "KeyVaultManagementClient API skill. Use when working with KeyVaultManagementClient for providers. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# KeyVaultManagementClient
API version: 2017-02-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.KeyVault.Admin/operations -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.KeyVault.Admin/operations | Get the list of support rest operations. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all operations?" -> GET /providers/Microsoft.KeyVault.Admin/operations
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
