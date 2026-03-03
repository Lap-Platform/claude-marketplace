---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for subscriptions. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Defender for Cloud
API version: 2015-06-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/applicationWhitelistings -- verify access

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/applicationWhitelistings | Gets a list of application control VM/server groups for the subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/locations/{ascLocation}/applicationWhitelistings/{groupName} | Gets an application control VM/server group. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Security/locations/{ascLocation}/applicationWhitelistings/{groupName} | Update an application control VM/server group |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Security/locations/{ascLocation}/applicationWhitelistings/{groupName} | Delete an application control VM/server group |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all applicationWhitelistings?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/applicationWhitelistings
- "Get applicationWhitelisting details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/locations/{ascLocation}/applicationWhitelistings/{groupName}
- "Update a applicationWhitelisting?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Security/locations/{ascLocation}/applicationWhitelistings/{groupName}
- "Delete a applicationWhitelisting?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Security/locations/{ascLocation}/applicationWhitelistings/{groupName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
