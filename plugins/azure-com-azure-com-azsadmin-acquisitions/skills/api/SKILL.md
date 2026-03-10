---
name: storagemanagementclient
description: "StorageManagementClient API skill. Use when working with StorageManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# StorageManagementClient
API version: 2019-08-08-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions | Returns a list of BLOB acquisitions. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all acquisitions?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Storage.Admin/locations/{location}/acquisitions
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
