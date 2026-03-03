---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for subscriptions. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Defender for Cloud
API version: 2018-06-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/pricings -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/pricings | Lists Microsoft Defender for Cloud pricing configurations in the subscription. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/pricings/{pricingName} | Gets a provided Microsoft Defender for Cloud pricing configuration in the subscription. |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Security/pricings/{pricingName} | Updates a provided Microsoft Defender for Cloud pricing configuration in the subscription. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all pricings?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/pricings
- "Get pricing details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/pricings/{pricingName}
- "Update a pricing?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Security/pricings/{pricingName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
