---
name: who-hosts-this-api
description: "Who Hosts This API skill. Use when working with Who Hosts This for Detect, Status. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Who Hosts This API
API version: 0.0.1

## Auth
ApiKey key in query

## Base URL
https://www.who-hosts-this.com/APIEndpoint

## Setup
1. Set your API key in the appropriate header
2. GET /Detect -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### Detect
| Method | Path | Description |
|--------|------|-------------|
| GET | /Detect | Discover the hosting provider for a web site |

### Status
| Method | Path | Description |
|--------|------|-------------|
| GET | /Status | View usage details for the current billing period |

## Enhanced Skill Content
## Question Mapping

- "Who hosts this website?" -> GET /Detect
- "What hosting provider does example.com use?" -> GET /Detect
- "Can you detect the host for a given URL?" -> GET /Detect
- "Where is this site hosted?" -> GET /Detect
- "Is the Who Hosts This API up?" -> GET /Status
- "Check the API health status" -> GET /Status
- "Identify the hosting company behind a domain" -> GET /Detect
- "What infrastructure runs this URL?" -> GET /Detect
- "Compare hosting providers for two sites" -> GET /Detect (x2)
- "Verify the API is reachable before running a detection" -> GET /Status, then GET /Detect
- "Batch-check hosting for a list of URLs" -> GET /Detect (repeated)
- "What server does this domain resolve to?" -> GET /Detect

## Response Tips

- **Detect**: Response likely contains hosting provider name, IP, and related metadata. Absent or null fields may indicate the host could not be determined -- surface this clearly rather than silently ignoring it.
- **Status**: Expect a simple health indicator. Treat any non-200 as the service being degraded or unavailable.
- **Auth errors**: A missing or invalid `key` query parameter will likely return 401/403. Prompt the user for their API key before retrying.

## Anomaly Flags

- Non-200 from `/Status` -- surface immediately as "API may be down, results unreliable"
- `/Detect` returns 200 but hosting provider is null/unknown -- flag as "Host could not be identified for this URL"
- 429 or rate-limit headers present -- warn user and suggest spacing out requests
- Auth failure (401/403) on `/Detect` -- prompt user to verify their API key is set and valid
- Unusually slow response times (>5s) -- note potential service degradation
- Redirect responses (3xx) -- flag possible URL normalization issues with the queried domain

## Playbook

### 1. Detect a Website's Hosting Provider

1. Call `GET /Status` to confirm the API is available
2. Call `GET /Detect?url=<target>&key=<api_key>`
3. Parse the response for provider name and IP details
4. If provider is null, inform the user the host could not be determined

### 2. Compare Hosting for Multiple Sites

1. Call `GET /Status` to confirm availability
2. For each URL in the list, call `GET /Detect?url=<url>&key=<api_key>`
3. Collect provider names from each response
4. Present a summary table: URL | Provider | IP
5. Highlight any URLs where detection failed

### 3. Monitor API Availability Before a Batch Job

1. Call `GET /Status`
2. If non-200, abort and notify the user
3. If 200, proceed with queued `/Detect` calls
4. After each call, check for rate-limit headers; back off if approaching limits

### 4. Validate API Key Setup

1. Call `GET /Status` (no auth needed) to confirm the service is reachable
2. Call `GET /Detect?url=example.com&key=<api_key>` as a test
3. If 401/403, the key is invalid -- prompt the user to check their key
4. If 200 with valid data, confirm the key is working correctly


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
