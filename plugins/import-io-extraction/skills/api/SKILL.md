---
name: api
description: " API skill. Use when working with  for extractor. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# 
API version: 1.0

## Auth
No authentication required.

## Base URL
https://extraction.import.io/

## Setup
1. No auth setup needed
2. GET /extractor/{extractorId} -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### extractor
| Method | Path | Description |
|--------|------|-------------|
| GET | /extractor/{extractorId} | Query by extractor endpoint, adhoc runs only. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Get extractor details?" -> GET /extractor/{extractorId}

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
