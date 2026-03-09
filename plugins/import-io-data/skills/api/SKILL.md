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
https://data.import.io/

## Setup
1. No auth setup needed
2. GET /extractor/{extractorId}/json/latest -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### extractor
| Method | Path | Description |
|--------|------|-------------|
| GET | /extractor/{extractorId}/json/latest | Get the latest crawl run results as json |
| GET | /extractor/{extractorId}/csv/latest | Get the latest crawl run results as a csv |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all latest?" -> GET /extractor/{extractorId}/json/latest
- "List all latest?" -> GET /extractor/{extractorId}/csv/latest

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
