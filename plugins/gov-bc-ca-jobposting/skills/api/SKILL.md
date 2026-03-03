---
name: workbc-job-posting-api
description: "WorkBC Job Posting API skill. Use when working with WorkBC Job Posting for majorProjects, jobTypes, regions. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# WorkBC Job Posting API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://workbcjobs.api.gov.bc.ca/v1

## Setup
1. No auth setup needed
2. GET /majorProjects -- verify access
3. POST /jobs -- create first jobs

## Endpoints

5 endpoints across 5 groups. See references/api-spec.lap for full details.

### majorProjects
| Method | Path | Description |
|--------|------|-------------|
| GET | /majorProjects | Major Projects |

### jobTypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /jobTypes | Job Types |

### regions
| Method | Path | Description |
|--------|------|-------------|
| GET | /regions | Regions |

### Industries
| Method | Path | Description |
|--------|------|-------------|
| GET | /Industries | Industries |

### jobs
| Method | Path | Description |
|--------|------|-------------|
| POST | /jobs | Job Feed |

## Enhanced Skill Content
## Question Mapping

- "What major projects are available in BC?" -> GET /majorProjects
- "What job types can I filter by?" -> GET /jobTypes
- "What regions are available for job search?" -> GET /regions
- "What industries are listed?" -> GET /Industries
- "Show me jobs in Victoria" -> POST /jobs (city=Victoria)
- "Find Vancouver jobs posted since last week" -> POST /jobs (city=Vancouver, lastRequestDate=<date>)
- "What major project jobs are available?" -> POST /jobs (majorProjects=True)
- "List all full-time jobs in region 2" -> POST /jobs (region=2, jobTypes=[1])
- "Are there any new job postings since yesterday?" -> POST /jobs (lastRequestDate=<yesterday>)
- "What job type IDs should I use when searching?" -> GET /jobTypes, then POST /jobs
- "Find jobs across all regions and types" -> POST /jobs (no filters)
- "How do I narrow results to a specific industry?" -> GET /Industries for IDs, then POST /jobs
- "Show me jobs related to major projects in Vancouver" -> POST /jobs (majorProjects=True, city=Vancouver)

## Response Tips

- **Reference endpoints** (GET /majorProjects, /jobTypes, /regions, /Industries): Return flat lists of lookup values -- use these IDs as filter parameters in POST /jobs.
- **Job search** (POST /jobs): Returns `{Jobs: [map]}` -- iterate the Jobs array; each entry is a map of job fields. No pagination documented, so expect full result sets.
- **Errors**: No explicit error schemas in the spec -- watch for non-200 status codes and surface the raw response body.

## Anomaly Flags

- **Empty Jobs array**: If POST /jobs returns `{Jobs: []}`, surface this explicitly -- the filters may be too narrow or the lastRequestDate too recent.
- **Unknown region/jobType IDs**: If the user passes an ID not found in GET /regions or GET /jobTypes, warn before sending the request.
- **Stale lastRequestDate**: If the user sets lastRequestDate far in the past, warn that the result set may be very large.
- **POST with no body**: All parameters on POST /jobs are optional -- if called with zero filters, flag that this returns unfiltered results.
- **Non-200 responses**: The spec only documents 200 -- any other status code (403, 429, 500) should be surfaced immediately with the full response.
- **Base URL availability**: The gov.bc.ca endpoint may have maintenance windows -- flag connection timeouts or 503 responses.

## Playbook

### 1. Browse all available jobs (no filters)

1. Call `POST /jobs` with an empty body or no parameters.
2. Read the `Jobs` array from the response.
3. Present results to the user, noting total count.

### 2. Search jobs by location and type

1. Call `GET /regions` to get valid region IDs.
2. Call `GET /jobTypes` to get valid job type IDs.
3. Call `POST /jobs` with `region`, `city`, and `jobTypes` set to the desired values.
4. Return the filtered `Jobs` array.

### 3. Get new postings since a specific date

1. Determine the target date (e.g., yesterday, last Monday).
2. Call `POST /jobs` with `lastRequestDate` set to that date in `YYYY-MM-DD` format.
3. If the result is empty, suggest broadening the date range.

### 4. Explore major project opportunities in a city

1. Call `GET /majorProjects` to confirm major projects exist.
2. Call `POST /jobs` with `majorProjects=True` and `city` set to the target city.
3. Present results, noting these are tied to major infrastructure/development projects.

### 5. Build a complete filter reference

1. Call `GET /regions`, `GET /jobTypes`, `GET /Industries`, and `GET /majorProjects` in parallel.
2. Compile the results into a lookup table of valid IDs and labels.
3. Use this reference to validate user inputs before calling `POST /jobs`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
