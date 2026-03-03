---
name: security-center
description: "Security Center API skill. Use when working with Security Center for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Security Center
API version: 2017-08-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/autoProvisioningSettings -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/autoProvisioningSettings | Exposes the auto provisioning settings of the subscriptions |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/autoProvisioningSettings/{settingName} | Details of a specific setting |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Security/autoProvisioningSettings/{settingName} | Details of a specific setting |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all autoProvisioningSettings?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/autoProvisioningSettings
- "Get autoProvisioningSetting details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/autoProvisioningSettings/{settingName}
- "Update a autoProvisioningSetting?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Security/autoProvisioningSettings/{settingName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
