---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for subscriptions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Defender for Cloud
API version: 2017-08-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts -- verify access

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts | Security contact configurations for the subscription |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts/{securityContactName} | Security contact configurations for the subscription |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts/{securityContactName} | Security contact configurations for the subscription |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts/{securityContactName} | Security contact configurations for the subscription |
| PATCH | /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts/{securityContactName} | Security contact configurations for the subscription |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all securityContacts?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts
- "Get securityContact details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts/{securityContactName}
- "Update a securityContact?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts/{securityContactName}
- "Delete a securityContact?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts/{securityContactName}
- "Partially update a securityContact?" -> PATCH /subscriptions/{subscriptionId}/providers/Microsoft.Security/securityContacts/{securityContactName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
