---
name: security-center
description: "Security Center API skill. Use when working with Security Center for {resourceId}. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Security Center
API version: 2019-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{resourceId}/providers/Microsoft.Security/advancedThreatProtectionSettings/{settingName} -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### {resourceId}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceId}/providers/Microsoft.Security/advancedThreatProtectionSettings/{settingName} | Gets the Advanced Threat Protection settings for the specified resource. |
| PUT | /{resourceId}/providers/Microsoft.Security/advancedThreatProtectionSettings/{settingName} | Creates or updates the Advanced Threat Protection settings on a specified resource. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get advancedThreatProtectionSetting details?" -> GET /{resourceId}/providers/Microsoft.Security/advancedThreatProtectionSettings/{settingName}
- "Update a advancedThreatProtectionSetting?" -> PUT /{resourceId}/providers/Microsoft.Security/advancedThreatProtectionSettings/{settingName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
