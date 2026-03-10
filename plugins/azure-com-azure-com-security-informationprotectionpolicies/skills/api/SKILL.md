---
name: security-center
description: "Security Center API skill. Use when working with Security Center for {scope}. Covers 3 endpoints."
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
2. GET /{scope}/providers/Microsoft.Security/informationProtectionPolicies -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{scope}/providers/Microsoft.Security/informationProtectionPolicies/{informationProtectionPolicyName} | Details of the information protection policy. |
| PUT | /{scope}/providers/Microsoft.Security/informationProtectionPolicies/{informationProtectionPolicyName} | Details of the information protection policy. |
| GET | /{scope}/providers/Microsoft.Security/informationProtectionPolicies | Information protection policies of a specific management group. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get informationProtectionPolicy details?" -> GET /{scope}/providers/Microsoft.Security/informationProtectionPolicies/{informationProtectionPolicyName}
- "Update a informationProtectionPolicy?" -> PUT /{scope}/providers/Microsoft.Security/informationProtectionPolicies/{informationProtectionPolicyName}
- "List all informationProtectionPolicies?" -> GET /{scope}/providers/Microsoft.Security/informationProtectionPolicies
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
