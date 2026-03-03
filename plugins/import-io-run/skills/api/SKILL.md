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

## Enhanced Skill Content
## Question Mapping

- "How do I start an extraction job?" -> POST /extractor/{extractorId}/start
- "How do I run an extractor?" -> POST /extractor/{extractorId}/start
- "How do I trigger a crawl for my extractor?" -> POST /extractor/{extractorId}/start
- "How do I cancel a running extraction?" -> POST /extractor/{extractorId}/cancel
- "How do I stop an extractor that's currently running?" -> POST /extractor/{extractorId}/cancel
- "How do I abort an extraction job?" -> POST /extractor/{extractorId}/cancel
- "How do I kick off a data extraction and then cancel it if it takes too long?" -> POST /extractor/{extractorId}/start, then POST /extractor/{extractorId}/cancel
- "What happens if I start an extractor with an invalid ID?" -> POST /extractor/{extractorId}/start (expect 404)
- "How do I cancel an extraction that doesn't exist?" -> POST /extractor/{extractorId}/cancel (expect 404)
- "Can I restart an extractor by cancelling and re-starting it?" -> POST /extractor/{extractorId}/cancel, then POST /extractor/{extractorId}/start
- "What do I need to authenticate before running an extractor?" -> Both endpoints require auth (expect 401 without credentials)
- "How do I batch-run multiple extractors?" -> POST /extractor/{extractorId}/start called per extractor ID

## Response Tips

- **Start/Cancel endpoints**: 200 indicates the action was accepted. A 404 means the extractorId does not exist. A 401 means missing or invalid authentication. A 400 means the request is malformed or the extractor is in a state that does not allow the action (e.g., cancelling an already-finished job).

## Anomaly Flags

- **401 responses**: Surface immediately -- likely an expired or missing API key. Prompt the user to check their import.io credentials.
- **404 on a previously valid extractorId**: The extractor may have been deleted. Confirm the ID is still valid in the import.io dashboard.
- **400 on cancel**: The extraction may have already completed or was never started. Surface the current job state to the user.
- **Repeated 400 on start**: The extractor configuration may be broken or the account may have hit a plan limit.
- **Timeouts or network errors**: The import.io service may be experiencing downtime. Suggest checking status.import.io or retrying after a short delay.

## Playbook

### 1. Run a Single Extraction

1. Obtain the `extractorId` from the import.io dashboard.
2. Call `POST /extractor/{extractorId}/start`.
3. Confirm a 200 response indicating the job was queued.
4. Monitor job completion through the import.io dashboard or polling mechanism.

### 2. Cancel a Long-Running Extraction

1. Identify the `extractorId` of the running job.
2. Call `POST /extractor/{extractorId}/cancel`.
3. Confirm a 200 response indicating cancellation was accepted.
4. If you receive a 400, the job may have already finished -- no action needed.

### 3. Restart a Failed or Stale Extraction

1. Call `POST /extractor/{extractorId}/cancel` to ensure any stuck job is cleared.
2. Handle a 400 gracefully (job may not have been running).
3. Call `POST /extractor/{extractorId}/start` to re-trigger the extraction.
4. Confirm a 200 response on the start call.

### 4. Batch-Run Multiple Extractors

1. Collect all target `extractorId` values.
2. For each ID, call `POST /extractor/{extractorId}/start`.
3. Track which IDs returned 200 (success) vs 400/404 (failure).
4. Report any failures to the user with the specific error code and extractor ID.
5. Optionally retry failed starts after a short delay.

### 5. Authenticate and Validate Setup

1. Pick any known `extractorId`.
2. Call `POST /extractor/{extractorId}/start`.
3. If you get 401, credentials are missing or invalid -- set the API key and retry.
4. If you get 404, the extractor ID is wrong -- verify in the dashboard.
5. A 200 confirms both authentication and the extractor ID are valid.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
