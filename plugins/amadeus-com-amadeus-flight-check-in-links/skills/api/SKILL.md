---
name: flight-check-in-links
description: "Flight Check-in Links API skill. Use when working with Flight Check-in Links for reference-data. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Flight Check-in Links
API version: 2.1.3

## Auth
No authentication required.

## Base URL
https://test.api.amadeus.com/v2

## Setup
1. No auth setup needed
2. GET /reference-data/urls/checkin-links -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### reference-data
| Method | Path | Description |
|--------|------|-------------|
| GET | /reference-data/urls/checkin-links | Lists Check-in URLs. |

## Enhanced Skill Content
## Question Mapping

- "Where can I check in online for my flight?" -> GET /reference-data/urls/checkin-links
- "What is the check-in URL for Delta Airlines?" -> GET /reference-data/urls/checkin-links
- "How do I find the web check-in link for airline code AA?" -> GET /reference-data/urls/checkin-links
- "Can I get check-in links in Spanish?" -> GET /reference-data/urls/checkin-links
- "What airlines have online check-in available?" -> GET /reference-data/urls/checkin-links
- "Get the mobile check-in page for British Airways" -> GET /reference-data/urls/checkin-links
- "Find check-in links for IATA code LH in German" -> GET /reference-data/urls/checkin-links
- "What URL should I send passengers to for online check-in?" -> GET /reference-data/urls/checkin-links
- "Does airline code QF have a check-in page?" -> GET /reference-data/urls/checkin-links
- "Retrieve localized check-in links for a specific carrier" -> GET /reference-data/urls/checkin-links
- "Compare check-in URLs across different languages for the same airline" -> GET /reference-data/urls/checkin-links (multiple calls varying `language`)
- "Validate that an airline's check-in link is still active" -> GET /reference-data/urls/checkin-links, then follow the returned URL

## Response Tips

- **Check-in links (200):** Response contains an array of link objects with channel type (web, mobile) and the URL. Always check for multiple entries per airline -- carriers often have separate desktop and mobile check-in flows. The `language` parameter filters results but may fall back to English if the requested locale is unavailable.
- **Errors (400):** Bad request errors typically mean the `airlineCode` is missing, malformed, or not a valid IATA/ICAO code. Inspect the `errors` array in the response body for a `detail` field describing what went wrong.

## Anomaly Flags

- **Missing airlineCode parameter:** The only required field -- surface a clear error immediately if the user omits it rather than sending a guaranteed-400 request.
- **Empty results for valid airline codes:** Some carriers do not publish check-in links through Amadeus. Flag this to the user so they know the absence is data-driven, not an error.
- **Language fallback:** If the user requests a specific language but the response returns English (or fewer results than expected), note that localized links may not be available for that carrier.
- **Unexpected 400 errors:** If the airline code looks valid (2-3 characters) but still returns 400, surface the possibility that the code is ICAO vs IATA and suggest trying the alternate format.
- **OAuth token expiry:** This API sits behind Amadeus OAuth (`test.api.amadeus.com`). If requests suddenly return 401, proactively remind the user to refresh their access token before retrying.

## Playbook

### 1. Get a Check-in Link for a Known Airline

1. Identify the airline's IATA code (e.g., `AA` for American Airlines).
2. Call `GET /reference-data/urls/checkin-links?airlineCode=AA`.
3. Parse the response array for entries matching the desired channel (web or mobile).
4. Present the URL to the user.

### 2. Retrieve Localized Check-in Links

1. Determine the target language as a two-letter ISO code (e.g., `es` for Spanish).
2. Call `GET /reference-data/urls/checkin-links?airlineCode=LH&language=es`.
3. If the response returns English links despite the language parameter, inform the user that localized links are not available for this carrier.
4. Return the best-available link.

### 3. Build a Multi-Airline Check-in Directory

1. Compile a list of IATA airline codes to look up.
2. For each code, call `GET /reference-data/urls/checkin-links?airlineCode={code}`.
3. Collect all successful responses into a unified list.
4. Flag any airlines that returned empty results or 400 errors as unsupported.
5. Present the directory grouped by airline with web and mobile links separated.

### 4. Validate and Monitor Check-in Link Availability

1. Call `GET /reference-data/urls/checkin-links?airlineCode={code}` for the target airline.
2. Extract all returned URLs.
3. Perform a HEAD request against each URL to verify it resolves (2xx or 3xx).
4. Flag any URLs returning 4xx/5xx as potentially broken.
5. Report the results, distinguishing between Amadeus data issues (no links returned) and broken destination URLs.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
