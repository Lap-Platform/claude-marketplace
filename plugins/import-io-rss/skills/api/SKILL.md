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
https://rss.import.io/

## Setup
1. No auth setup needed
2. GET /extractor/{extractorId}/runs -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### extractor
| Method | Path | Description |
|--------|------|-------------|
| GET | /extractor/{extractorId}/runs | Get a feed of the runs performed on an extractor |

## Enhanced Skill Content
## Question Mapping

- "How do I get runs for an extractor?" -> GET /extractor/{extractorId}/runs
- "What extraction runs have completed?" -> GET /extractor/{extractorId}/runs
- "Show me the run history for this extractor" -> GET /extractor/{extractorId}/runs
- "Has my extractor run recently?" -> GET /extractor/{extractorId}/runs
- "List all runs for extractor abc123" -> GET /extractor/{extractorId}/runs
- "Did my last extraction succeed?" -> GET /extractor/{extractorId}/runs
- "How many times has this extractor run?" -> GET /extractor/{extractorId}/runs
- "Check the status of my extractor runs" -> GET /extractor/{extractorId}/runs
- "Why is my extractor returning 404?" -> GET /extractor/{extractorId}/runs (invalid extractorId)
- "I'm getting unauthorized errors on my extractor" -> GET /extractor/{extractorId}/runs (auth issue, 401)
- "Get the most recent extraction results" -> GET /extractor/{extractorId}/runs
- "Monitor my RSS extractor progress" -> GET /extractor/{extractorId}/runs (poll periodically)

## Response Tips

- **Runs listing (200):** Response contains an array of run objects. Each run typically includes a status, timestamp, and row count. Check the most recent entry for current state.
- **Not Found (404):** The extractorId does not exist or has been deleted. Verify the ID is correct and the extractor has not been removed from your import.io account.
- **Unauthorized (401):** Authentication is missing or invalid. Ensure your API key or session credentials are included in the request headers.

## Anomaly Flags

- **401 on a previously working extractor:** Credentials may have expired or been revoked. Surface immediately and suggest re-authenticating.
- **404 for a known extractorId:** The extractor may have been deleted upstream. Flag this as a potential data pipeline break.
- **Empty runs array on 200:** The extractor exists but has never run or runs have been purged. Prompt the user to trigger a manual run.
- **Repeated failed run statuses:** If multiple consecutive runs show failure, surface a warning about possible source-site changes or broken selectors.
- **Unusually long gap between runs:** If the most recent run timestamp is significantly older than expected, flag a possible scheduling issue.

## Playbook

### 1. Check if an Extractor is Healthy

1. Call `GET /extractor/{extractorId}/runs` with your extractor ID
2. Inspect the most recent run entry in the response
3. Verify the status is successful and the row count is non-zero
4. If the status indicates failure, check the error details and review the extractor configuration in import.io

### 2. Diagnose a Failing Extractor

1. Call `GET /extractor/{extractorId}/runs` to retrieve run history
2. Identify when runs started failing by scanning status fields chronologically
3. If you get a 404, confirm the extractorId is valid in your import.io dashboard
4. If you get a 401, regenerate or refresh your API credentials
5. If runs return 200 but show errors, the target site may have changed structure

### 3. Monitor an Extractor Over Time

1. Call `GET /extractor/{extractorId}/runs` on a schedule (e.g., hourly or daily)
2. Compare the latest run timestamp against the previous check
3. If no new runs appear within the expected interval, flag a scheduling issue
4. Track row counts across runs to detect data volume anomalies (sudden drops or spikes)

### 4. Validate Extractor Setup After Creation

1. Create or configure your extractor in the import.io dashboard
2. Trigger an initial run manually from the dashboard
3. Call `GET /extractor/{extractorId}/runs` to confirm the run appears
4. Verify the response includes a successful status and expected row count
5. If the runs list is empty, wait a moment and retry -- the run may still be processing


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
