---
name: api
description: " API skill. Use when working with  for extractor. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# 
API version: 1.0

## Auth
No authentication required.

## Base URL
https://run.import.io/

## Setup
1. No auth setup needed
3. POST /extractor/{extractorId}/start -- create first start

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### extractor
| Method | Path | Description |
|--------|------|-------------|
| POST | /extractor/{extractorId}/start | Launch a crawl from an extractor that a user owns. |
| POST | /extractor/{extractorId}/cancel | Cancel an existing crawl. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a start?" -> POST /extractor/{extractorId}/start
- "Create a cancel?" -> POST /extractor/{extractorId}/cancel

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
