---
name: api
description: " API skill. Use when working with  for extractor. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# 
API version: 1.0

## Auth
No authentication required.

## Base URL
https://schedule.import.io/

## Setup
1. No auth setup needed
2. GET /extractor -- verify access
3. POST /extractor -- create first extractor

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### extractor
| Method | Path | Description |
|--------|------|-------------|
| POST | /extractor | Schedule and extractor to run at a specific time |
| GET | /extractor | Get the list of schedules for all your extractors |
| DELETE | /extractor/{extractorId}/ | Delete an existing schedule |
| GET | /extractor/{extractorId}/ | Get the schedule of a particular extractor |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a extractor?" -> POST /extractor
- "List all extractor?" -> GET /extractor
- "Delete a extractor?" -> DELETE /extractor/{extractorId}/
- "Get extractor details?" -> GET /extractor/{extractorId}/

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
