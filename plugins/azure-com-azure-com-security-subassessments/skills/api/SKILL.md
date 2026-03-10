---
name: microsoft-defender-for-cloud
description: "Microsoft Defender for Cloud API skill. Use when working with Microsoft Defender for Cloud for {scope}. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Microsoft Defender for Cloud
API version: 2019-01-01-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /{scope}/providers/Microsoft.Security/subAssessments -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### {scope}
| Method | Path | Description |
|--------|------|-------------|
| GET | /{scope}/providers/Microsoft.Security/subAssessments | Get security sub-assessments on all your scanned resources inside a subscription scope |
| GET | /{scope}/providers/Microsoft.Security/assessments/{assessmentName}/subAssessments | Get security sub-assessments on all your scanned resources inside a scope |
| GET | /{scope}/providers/Microsoft.Security/assessments/{assessmentName}/subAssessments/{subAssessmentName} | Get a security sub-assessment on your scanned resource |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all subAssessments?" -> GET /{scope}/providers/Microsoft.Security/subAssessments
- "List all subAssessments?" -> GET /{scope}/providers/Microsoft.Security/assessments/{assessmentName}/subAssessments
- "Get subAssessment details?" -> GET /{scope}/providers/Microsoft.Security/assessments/{assessmentName}/subAssessments/{subAssessmentName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
