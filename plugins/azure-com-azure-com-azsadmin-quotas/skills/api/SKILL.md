---
name: compute-admin-client
description: "Compute Admin Client API skill. Use when working with Compute Admin Client for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Compute Admin Client
API version: 2018-02-09

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName} | Returns the requested Compute quota. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName} | Creates or Updates a Compute Quota. |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName} | Deletes specified Compute quota |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas | Lists all Compute quotas. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get quota details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Update a quota?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "Delete a quota?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas/{quotaName}
- "List all quotas?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Compute.Admin/locations/{location}/quotas
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
