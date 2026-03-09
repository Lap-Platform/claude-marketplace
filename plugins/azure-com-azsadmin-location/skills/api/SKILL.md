---
name: subscriptionsmanagementclient
description: "SubscriptionsManagementClient API skill. Use when working with SubscriptionsManagementClient for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionsManagementClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations | Get a list of all AzureStack location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location} | Get the specified location. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location} | Updates the specified location. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/operationsStatus/{operationsStatusName} | Get the operation status. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all locations?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations
- "Get location details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}
- "Update a location?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}
- "Get operationsStatus details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/locations/{location}/operationsStatus/{operationsStatusName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
