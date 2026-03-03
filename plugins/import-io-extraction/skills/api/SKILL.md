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

## Enhanced Skill Content
## Question Mapping

- "How do I extract data from a webpage?" -> GET /extractor/{extractorId}
- "Can I scrape a specific URL using my extractor?" -> GET /extractor/{extractorId}
- "How do I run an extractor against a target page?" -> GET /extractor/{extractorId}
- "What data does my extractor pull from this site?" -> GET /extractor/{extractorId}
- "How do I test if my extractor is working?" -> GET /extractor/{extractorId}
- "Can I extract data from multiple URLs?" -> GET /extractor/{extractorId} (call once per URL)
- "Why is my extraction returning a 401?" -> GET /extractor/{extractorId} (check API key/auth)
- "What happens if I pass an invalid URL to the extractor?" -> GET /extractor/{extractorId} (expect 400)
- "How do I get structured data from a webpage?" -> GET /extractor/{extractorId}
- "Can I use a different extractor configuration on the same URL?" -> GET /extractor/{extractorId} (swap extractorId)
- "How do I verify my extractor ID is valid?" -> GET /extractor/{extractorId} (check for 400 vs 200)
- "What format does extracted data come back in?" -> GET /extractor/{extractorId}

## Response Tips

- **Extractor results (200):** Response contains extracted data shaped by the extractor's configured selectors; field names and nesting vary per extractor configuration, so inspect the response schema dynamically rather than assuming fixed keys.
- **Auth errors (401):** Missing or invalid API key; ensure the `_apikey` query parameter or auth header is present and belongs to the account that owns the extractor.
- **Bad requests (400):** Typically means `extractorId` is malformed/nonexistent or `url` is missing/unparseable; check both required parameters before retrying.

## Anomaly Flags

- **401 on previously working calls:** API key may have been rotated or revoked; surface immediately and suggest re-authentication.
- **400 with valid-looking inputs:** The extractor may have been deleted or reconfigured upstream; flag the extractorId as potentially stale.
- **Slow or empty responses on valid URLs:** Target site may be blocking the extraction service (bot protection, geo-restriction); warn the user that extraction quality depends on target site accessibility.
- **Repeated identical results across different URLs:** Possible sign the extractor selectors are misconfigured or the target pages share identical structure; flag for review.
- **Rate limiting (429 or throttled responses):** import.io enforces usage quotas; proactively warn when call frequency is high and suggest batching or spacing requests.

## Playbook

### 1. Extract Data from a Single URL

1. Obtain your `extractorId` from the import.io dashboard (or from a previous configuration step).
2. Call `GET /extractor/{extractorId}` with the `url` query parameter set to the target webpage.
3. Inspect the 200 response for extracted fields.
4. If you receive 400, verify the URL is well-formed and the extractorId exists.
5. If you receive 401, confirm your API key is valid and included in the request.

### 2. Batch Extract Across Multiple URLs

1. Prepare a list of target URLs.
2. For each URL, call `GET /extractor/{extractorId}` with the same extractorId.
3. Collect and merge results, keying by source URL.
4. Handle per-request errors individually -- a 400 on one URL should not halt the batch.
5. Respect rate limits by spacing requests or using concurrency controls.

### 3. Validate an Extractor Configuration

1. Pick a known-good URL that the extractor was designed for.
2. Call `GET /extractor/{extractorId}` with that URL.
3. Confirm the response contains expected fields with reasonable values.
4. If the response is empty or malformed, the extractor selectors likely need updating in the import.io dashboard.

### 4. Diagnose a Failing Extraction

1. Call `GET /extractor/{extractorId}` and note the exact error code (400 vs 401).
2. For 401: verify the API key is correct and the account has access to this extractor.
3. For 400: confirm `extractorId` is a valid UUID and `url` is a fully qualified URL (including scheme).
4. If 200 but data is empty: visit the target URL in a browser to check if the page loads correctly and still matches the extractor's expected structure.
5. Try a different URL with the same extractor to isolate whether the issue is URL-specific or extractor-wide.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
