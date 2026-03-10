---
name: spec
description: "spec API skill. Use when working with spec for agreements. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# spec

## Auth
No authentication required.

## Base URL
https://api.ote-godaddy.com

## Setup
1. No auth setup needed
2. GET /v1/agreements -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### agreements
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/agreements | Retrieve Legal Agreements for provided agreements keys |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all agreements?" -> GET /v1/agreements

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
