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

## Enhanced Skill Content
## Question Mapping

- "How do I get the latest extraction results?" -> GET /extractor/{extractorId}/json/latest
- "Can I download extracted data as a spreadsheet?" -> GET /extractor/{extractorId}/csv/latest
- "How do I fetch JSON output from my extractor?" -> GET /extractor/{extractorId}/json/latest
- "How do I export extractor results to CSV?" -> GET /extractor/{extractorId}/csv/latest
- "Why am I getting a 404 when fetching extractor data?" -> GET /extractor/{extractorId}/json/latest (extractorId may be invalid or extractor has no runs)
- "How do I check if my extractor has finished running?" -> GET /extractor/{extractorId}/json/latest (a 404 may indicate no completed run yet)
- "Can I get the same data in both JSON and CSV?" -> GET /extractor/{extractorId}/json/latest + GET /extractor/{extractorId}/csv/latest (same data, different format)
- "Why is my request unauthorized?" -> GET /extractor/{extractorId}/json/latest (check API key or auth token)
- "How do I compare outputs from two different extractors?" -> GET /extractor/{extractorId}/json/latest (call twice with different extractorIds)
- "What format should I use for programmatic processing?" -> GET /extractor/{extractorId}/json/latest (JSON is easier to parse)
- "What format works best for importing into Excel?" -> GET /extractor/{extractorId}/csv/latest
- "How do I verify my extractor is returning data?" -> GET /extractor/{extractorId}/json/latest (check for non-empty response)

## Response Tips

- **Extractor endpoints**: Both `/json/latest` and `/csv/latest` return the most recent completed extraction only -- there is no pagination or historical access. A 404 means either the extractorId does not exist or no extraction has completed yet. A 401 indicates missing or invalid authentication. JSON responses will contain row-level extracted data as an array of objects; CSV responses return raw text with headers in the first row.

## Anomaly Flags

- **401 on previously working requests**: API key may have been rotated or revoked -- surface immediately and suggest re-authenticating.
- **404 after extractor creation**: The extractor likely has not completed its first run yet -- flag this with a "try again shortly" suggestion rather than treating it as a permanent error.
- **Empty result set in 200 response**: The extractor ran but matched zero rows -- surface this as a potential configuration issue (selectors may be broken or the target page changed).
- **Inconsistent row counts between JSON and CSV**: If the same extractorId returns different row counts across formats, flag as a potential data integrity issue.
- **Repeated 404s across multiple extractors**: May indicate an account-level issue or service disruption -- suggest checking import.io status.

## Playbook

### 1. Retrieve Latest Extraction as JSON

1. Obtain your `extractorId` from the import.io dashboard.
2. Call `GET /extractor/{extractorId}/json/latest` with your auth credentials.
3. Parse the JSON response -- each object in the array represents one extracted row.
4. If you receive a 404, confirm the extractor exists and has completed at least one run.

### 2. Export Extraction Results to CSV

1. Identify the `extractorId` for the target extractor.
2. Call `GET /extractor/{extractorId}/csv/latest`.
3. Save the response body directly as a `.csv` file.
4. Open in Excel, Google Sheets, or feed into a data pipeline.

### 3. Compare Two Extractors' Output

1. Call `GET /extractor/{extractorIdA}/json/latest` and store the result.
2. Call `GET /extractor/{extractorIdB}/json/latest` and store the result.
3. Compare field names (keys) to identify schema differences.
4. Compare row counts and values to assess data overlap or drift.

### 4. Validate a New Extractor Is Working

1. Create and run the extractor via the import.io dashboard.
2. Wait for the run to complete (check dashboard status).
3. Call `GET /extractor/{extractorId}/json/latest`.
4. If you get a 200, inspect the rows for expected fields and values.
5. If you get a 404, the run has not finished -- wait and retry.
6. If the 200 response is empty, review your extractor's CSS/XPath selectors.

### 5. Troubleshoot Authentication Failures

1. Attempt `GET /extractor/{extractorId}/json/latest` with your current credentials.
2. If you receive a 401, verify the API key or token is included in the request header.
3. Confirm the key has not been revoked in your import.io account settings.
4. Re-generate credentials if needed and retry the request.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
