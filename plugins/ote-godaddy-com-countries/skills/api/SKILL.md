---
name: spec
description: "spec API skill. Use when working with spec for countries. Covers 2 endpoints."
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
2. GET /v1/countries -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### countries
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/countries | Retrieves summary country information for the provided marketId and filters |
| GET | /v1/countries/{countryKey} | Retrieves country and summary state information for provided countryKey |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all countries?" -> GET /v1/countries
- "Get country details?" -> GET /v1/countries/{countryKey}

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
