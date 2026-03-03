---
name: canada-holidays-api
description: "Canada Holidays API skill. Use when working with Canada Holidays for api. Covers 6 endpoints."
version: 1.0.0
generator: lapsh
---

# Canada Holidays API
API version: 1.8.0

## Auth
No authentication required.

## Base URL
https://canada-holidays.ca

## Setup
1. No auth setup needed
2. GET /api/v1 -- verify access

## Endpoints

6 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v1 | root |
| GET | /api/v1/holidays | Get all holidays |
| GET | /api/v1/provinces | Get all provinces |
| GET | /api/v1/provinces/{provinceId} | Get a province or territory by abbreviation |
| GET | /api/v1/holidays/{holidayId} | Get a holiday by id |
| GET | /api/v1/spec | Get JSON schema |

## Enhanced Skill Content
## Question Mapping

- "What holidays are coming up in Canada?" -> GET /api/v1/holidays
- "Which holidays are federal holidays?" -> GET /api/v1/holidays?federal=1
- "What are the optional holidays this year?" -> GET /api/v1/holidays?optional=true
- "What holidays does Ontario have?" -> GET /api/v1/provinces/ON
- "When is the next holiday in Quebec?" -> GET /api/v1/provinces/QC
- "List all Canadian provinces and territories" -> GET /api/v1/provinces
- "What provinces observe Canada Day?" -> GET /api/v1/holidays/1
- "What holidays are in 2026?" -> GET /api/v1/holidays?year=2026
- "Is Boxing Day a federal holiday?" -> GET /api/v1/holidays/{holidayId}
- "What's the difference between date and observedDate for a holiday?" -> GET /api/v1/holidays/{holidayId}
- "What are the optional holidays in Alberta for 2025?" -> GET /api/v1/provinces/AB?year=2025&optional=true
- "Show me the API root and available endpoints" -> GET /api/v1
- "Get the OpenAPI spec for this API" -> GET /api/v1/spec
- "What holidays do all provinces share?" -> GET /api/v1/holidays?federal=1

## Response Tips

- **Root (`/api/v1`)**: Returns `_links` with HATEOAS-style hrefs -- use these to discover endpoints dynamically rather than hardcoding paths.
- **Holidays**: Response wraps results in a `holidays` array of maps; each entry includes both `date` (legislated) and `observedDate` (actual day off) -- always prefer `observedDate` for scheduling.
- **Provinces**: Response wraps results in a `provinces` array; single-province lookup nests `nextHoliday` inside the `province` object for quick access.
- **Single holiday/province**: Returns a singular key (`holiday` or `province`), not an array -- no unwrapping needed.
- **Errors**: 400 status on invalid `provinceId` or `holidayId` -- check that province IDs are two-letter codes (e.g., ON, QC, BC) and holiday IDs are integers.
- **Boolean fields**: `federal` and `optional` are returned as `int(binary)` (0 or 1), not true/false -- compare numerically.

## Anomaly Flags

- **Year out of range**: If `year` is set far in the past or future, results may be empty or speculative -- surface a note when year differs significantly from the current year.
- **observedDate differs from date**: Flag when a holiday's `observedDate` does not match `date`, as this means the day off shifts (typically to a Monday).
- **Optional holidays**: When `optional=false` (default), optional holidays are hidden -- flag if a user asks about a holiday that only appears with `optional=true`.
- **Empty provinces array on a holiday**: If a holiday has no provinces listed, it may indicate a data gap -- surface this to the user.
- **400 errors on lookup**: Province IDs must be uppercase two-letter codes; holiday IDs must be numeric -- flag malformed IDs before making the request.
- **French vs English names**: Both `nameEn` and `nameFr` are always present -- surface the French name when the user context suggests bilingual or Quebec-specific queries.

## Playbook

### Find the next upcoming holiday for a specific province

1. Call `GET /api/v1/provinces/{provinceId}?year={currentYear}` with the two-letter province code (e.g., ON, BC, QC).
2. Read `province.nextHoliday` from the response -- this gives the nearest future holiday with its `observedDate`.
3. Present the holiday name (`nameEn`/`nameFr`), `observedDate`, and whether it is `federal` or `optional`.

### List all holidays a province observes in a given year (including optional)

1. Call `GET /api/v1/provinces/{provinceId}?year={year}&optional=true`.
2. Iterate through the `province.provinces` array (this contains the holidays for that province).
3. Group results by `federal` (1 = federal, 0 = provincial) and flag any where `optional` is 1.

### Check if a specific holiday is observed in a given province

1. Call `GET /api/v1/holidays/{holidayId}?year={year}&optional=true`.
2. Inspect the `holiday.provinces` array for an entry matching the target province ID.
3. If the province is not listed, the holiday is not observed there. If `optional` is 1, note that observance may vary by employer.

### Compare holidays across two provinces

1. Call `GET /api/v1/provinces/{provinceA}?year={year}&optional=true`.
2. Call `GET /api/v1/provinces/{provinceB}?year={year}&optional=true`.
3. Collect holiday IDs from each response and compute the intersection (shared), A-only, and B-only sets.
4. Present a comparison table with holiday names, dates, and which province(s) observe each.

### Get a full calendar of Canadian holidays for planning

1. Call `GET /api/v1/holidays?year={year}&optional=true` to get all holidays including optional ones.
2. Sort the `holidays` array by `observedDate`.
3. For each holiday, note `federal` status and list the provinces from the `provinces` array.
4. Flag any holidays where `observedDate` differs from `date` as shifted long weekends.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
