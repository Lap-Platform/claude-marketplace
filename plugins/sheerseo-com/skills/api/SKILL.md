---
name: sheerseo-api
description: "SheerSEO API skill. Use when working with SheerSEO for serp-submit, serp-collect, rank-submit. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# SheerSEO API
API version: 0.0.1

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
3. POST /serp-submit -- create first serp-submit

## Endpoints

4 endpoints across 4 groups. See references/api-spec.lap for full details.

### serp-submit
| Method | Path | Description |
|--------|------|-------------|
| POST | /serp-submit | Submit serp jobs |

### serp-collect
| Method | Path | Description |
|--------|------|-------------|
| POST | /serp-collect | Submit serp jobs |

### rank-submit
| Method | Path | Description |
|--------|------|-------------|
| POST | /rank-submit | Submit rank jobs |

### rank-collect
| Method | Path | Description |
|--------|------|-------------|
| POST | /rank-collect | Submit serp jobs |

## Enhanced Skill Content
## Question Mapping

- "How do I check my keyword rankings?" -> POST /rank-submit then POST /rank-collect
- "What are the SERP results for a keyword?" -> POST /serp-submit then POST /serp-collect
- "How do I submit keywords for rank tracking?" -> POST /rank-submit
- "How do I retrieve rank tracking results?" -> POST /rank-collect
- "Can I check Google search results for multiple keywords at once?" -> POST /serp-submit
- "How do I get SERP data I previously requested?" -> POST /serp-collect
- "What position does my site rank for a keyword?" -> POST /rank-submit then POST /rank-collect
- "How do I monitor competitor rankings?" -> POST /rank-submit
- "Are my SERP results ready yet?" -> POST /serp-collect
- "How do I bulk-submit keywords for SERP analysis?" -> POST /serp-submit
- "Why am I getting a 503 error on submit?" -> Check rate limits / service availability on POST /serp-submit or POST /rank-submit
- "How do I track ranking changes over time?" -> POST /rank-submit (repeated) then POST /rank-collect

## Response Tips

- **Submit endpoints** (`/serp-submit`, `/rank-submit`): Returns a job reference or acknowledgment. Store any returned ID for the collect step. A 200 means the job was accepted, not completed.
- **Collect endpoints** (`/serp-collect`, `/rank-collect`): Results may not be ready immediately after submit. A 200 with empty or partial data means results are still processing. Re-poll after a delay.
- **Error responses**: 400 indicates malformed body (check required fields). 404 means the requested job or resource was not found. 503 signals the service is temporarily overloaded - back off and retry.

## Anomaly Flags

- **503 responses on submit**: Service is overloaded. Surface immediately and suggest exponential backoff before retrying.
- **Repeated empty collect responses**: Results may be stuck in processing. Flag if collect returns no data after multiple attempts.
- **400 errors**: Likely a schema mismatch in the request body. Surface the error details and suggest validating the payload structure.
- **404 on collect**: The submitted job ID may have expired or been invalid. Alert the user to re-submit.
- **High latency between submit and collect**: If results take significantly longer than expected, flag potential service degradation.

## Playbook

### 1. Check SERP Results for Keywords

1. Call `POST /serp-submit` with your target keywords in the request body
2. Note the job reference or ID returned in the response
3. Wait a reasonable interval (start with 10-30 seconds)
4. Call `POST /serp-collect` with the job reference to retrieve results
5. If results are not yet ready, wait and retry step 4

### 2. Track Keyword Rankings for Your Site

1. Call `POST /rank-submit` with your domain and target keywords
2. Store the returned job reference
3. Wait for processing (may take longer than SERP queries)
4. Call `POST /rank-collect` to retrieve ranking positions
5. Compare results against previous collect calls to identify ranking changes

### 3. Monitor Competitor Rankings

1. Call `POST /rank-submit` with the competitor domain and shared keywords
2. Call `POST /rank-submit` with your own domain and the same keywords
3. Collect both result sets via `POST /rank-collect`
4. Compare ranking positions side by side

### 4. Handle Service Unavailability

1. If any endpoint returns 503, stop sending new requests immediately
2. Wait 30 seconds, then retry with a single request
3. If 503 persists, double the wait interval (exponential backoff, cap at 5 minutes)
4. Once a 200 is returned, resume normal request flow
5. If 503 continues beyond 15 minutes, flag the issue as a potential outage


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
