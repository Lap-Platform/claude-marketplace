---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for {scope}, {resourceId}. Covers 4 endpoints."
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
2. GET /{scope}/providers/Microsoft.Security/assessments -- verify access

## Endpoints

4 endpoints across 2 groups. See references/api-spec.lap for full details.

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{scope}/providers/Microsoft.Security/assessments | Get security assessments on all your scanned resources inside a scope |

### {resourceId}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{resourceId}/providers/Microsoft.Security/assessments/{assessmentName} | Get a security assessment on your scanned resource |
| PUT | /{resourceId}/providers/Microsoft.Security/assessments/{assessmentName} | Create a security assessment on your resource. An assessment metadata that describes this assessment must be predefined with the same name before inserting the assessment result |
| DELETE | /{resourceId}/providers/Microsoft.Security/assessments/{assessmentName} | Delete a security assessment on your resource. An assessment metadata that describes this assessment must be predefined with the same name before inserting the assessment result |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all assessments?" -> GET /{scope}/providers/Microsoft.Security/assessments
- "Get assessment details?" -> GET /{resourceId}/providers/Microsoft.Security/assessments/{assessmentName}
- "Update a assessment?" -> PUT /{resourceId}/providers/Microsoft.Security/assessments/{assessmentName}
- "Delete a assessment?" -> DELETE /{resourceId}/providers/Microsoft.Security/assessments/{assessmentName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
