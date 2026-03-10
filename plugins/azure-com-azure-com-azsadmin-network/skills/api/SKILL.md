---
name: networkadminmanagementclient
description: "NetworkAdminManagementClient API skill. Use when working with NetworkAdminManagementClient for subscriptions, providers. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# NetworkAdminManagementClient
API version: 2015-06-15

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Network.Admin/operations -- verify access

## Endpoints

5 endpoints across 2 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminOverview | Get an overview of the state of the network resource provider. |

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Network.Admin/operations | Returns the list of support REST operations. |
| GET | /providers/Microsoft.Network.Admin/locations | Returns the list of supported locations |
| GET | /providers/Microsoft.Network.Admin/locations/{location}/operationResults | Returns the list of operation results for a location |
| GET | /providers/Microsoft.Network.Admin/locations/{location}/operations | Returns the list of support REST operations. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all adminOverview?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Network.Admin/adminOverview
- "List all operations?" -> GET /providers/Microsoft.Network.Admin/operations
- "List all locations?" -> GET /providers/Microsoft.Network.Admin/locations
- "List all operationResults?" -> GET /providers/Microsoft.Network.Admin/locations/{location}/operationResults
- "List all operations?" -> GET /providers/Microsoft.Network.Admin/locations/{location}/operations
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
