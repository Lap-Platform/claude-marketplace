---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for providers, subscriptions. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Defender for Cloud
API version: 2020-01-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.Security/assessmentMetadata -- verify access

## Endpoints

6 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.Security/assessmentMetadata | Get metadata information on all assessment types |
| GET | /providers/Microsoft.Security/assessmentMetadata/{assessmentMetadataName} | Get metadata information on an assessment type |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/assessmentMetadata | Get metadata information on all assessment types in a specific subscription |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Security/assessmentMetadata/{assessmentMetadataName} | Get metadata information on an assessment type in a specific subscription |
| PUT | /subscriptions/{subscriptionId}/providers/Microsoft.Security/assessmentMetadata/{assessmentMetadataName} | Create metadata information on an assessment type in a specific subscription |
| DELETE | /subscriptions/{subscriptionId}/providers/Microsoft.Security/assessmentMetadata/{assessmentMetadataName} | Delete metadata information on an assessment type in a specific subscription, will cause the deletion of all the assessments of that type in that subscription |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all assessmentMetadata?" -> GET /providers/Microsoft.Security/assessmentMetadata
- "Get assessmentMetadata details?" -> GET /providers/Microsoft.Security/assessmentMetadata/{assessmentMetadataName}
- "List all assessmentMetadata?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/assessmentMetadata
- "Get assessmentMetadata details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Security/assessmentMetadata/{assessmentMetadataName}
- "Update a assessmentMetadata?" -> PUT /subscriptions/{subscriptionId}/providers/Microsoft.Security/assessmentMetadata/{assessmentMetadataName}
- "Delete a assessmentMetadata?" -> DELETE /subscriptions/{subscriptionId}/providers/Microsoft.Security/assessmentMetadata/{assessmentMetadataName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
