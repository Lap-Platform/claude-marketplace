---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for {scope}, {resourceId}. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Defender for Cloud
API version: 2017-08-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{scope}/providers/Microsoft.Security/complianceResults -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{scope}/providers/Microsoft.Security/complianceResults | Security compliance results in the subscription |

### {resourceId}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceId}/providers/Microsoft.Security/complianceResults/{complianceResultName} | Security Compliance Result |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all complianceResults?" -> GET /{scope}/providers/Microsoft.Security/complianceResults
- "Get complianceResult details?" -> GET /{resourceId}/providers/Microsoft.Security/complianceResults/{complianceResultName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
