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

## Enhanced Skill Content


## Question Mapping

- "How do I create a new extraction schedule?" -> POST /extractor
- "How do I list all my scheduled extractors?" -> GET /extractor
- "How do I check what schedule is set for a specific extractor?" -> GET /extractor/{extractorId}/
- "How do I remove a schedule from an extractor?" -> DELETE /extractor/{extractorId}/
- "How do I update an existing extractor schedule?" -> POST /extractor (re-post with updated schedule body)
- "How do I see all active extraction schedules?" -> GET /extractor
- "How do I stop a recurring extraction?" -> DELETE /extractor/{extractorId}/
- "How do I verify a schedule was created successfully?" -> GET /extractor/{extractorId}/
- "What extractors are currently scheduled to run?" -> GET /extractor
- "How do I set up a periodic data extraction and later cancel it?" -> POST /extractor, then DELETE /extractor/{extractorId}/
- "How do I troubleshoot a schedule that isn't running?" -> GET /extractor/{extractorId}/ to inspect schedule state
- "How do I replace the schedule configuration for an extractor?" -> POST /extractor with the new Schedule Request Body

## Response Tips

- **POST /extractor**: Expect the created schedule object on 200. Watch for 400 (malformed body), 401 (missing auth), 403 (no permission on the extractor).
- **GET /extractor** (list): Returns an array of schedule objects. No documented pagination -- if the list seems truncated, confirm by cross-referencing with known extractor IDs.
- **GET /extractor/{extractorId}/**: Returns a single schedule object. A 404 means no schedule exists for that extractor, not necessarily that the extractor itself is invalid.
- **DELETE /extractor/{extractorId}/**: 200 confirms removal. A 404 may mean the schedule was already deleted or never existed; 403 means insufficient permissions.

## Anomaly Flags

- **401 on any request**: Authentication is missing or expired -- surface immediately and prompt for credential refresh.
- **403 on POST or DELETE**: The authenticated user lacks permission on the target extractor -- flag and suggest checking extractor ownership or team permissions.
- **404 on GET by ID**: The schedule may have been deleted externally or the extractor ID is wrong -- surface the distinction to the user.
- **Repeated 400 on POST**: Likely a malformed Schedule Request Body -- proactively show the request payload for review.
- **Empty list from GET /extractor**: Could indicate no schedules exist or a scoping/auth issue -- flag if the user expects active schedules.
- **Slow or timeout responses**: The scheduling service may be under load -- suggest retry with backoff.

## Playbook

### 1. Create and Verify a New Schedule

1. Prepare a Schedule Request Body with the desired extraction configuration.
2. Call `POST /extractor` with the body.
3. Confirm a 200 response and note the returned extractor ID.
4. Call `GET /extractor/{extractorId}/` to verify the schedule is active and correctly configured.

### 2. Audit All Active Schedules

1. Call `GET /extractor` to retrieve all scheduled extractors.
2. Review each entry for schedule timing, target URLs, and status.
3. For any entry that looks misconfigured, call `GET /extractor/{extractorId}/` for full details.
4. Delete stale or unwanted schedules with `DELETE /extractor/{extractorId}/`.

### 3. Cancel and Clean Up a Schedule

1. Identify the extractor ID of the schedule to cancel.
2. Call `GET /extractor/{extractorId}/` to confirm it exists and review its configuration.
3. Call `DELETE /extractor/{extractorId}/` to remove the schedule.
4. Call `GET /extractor/{extractorId}/` again -- expect a 404 to confirm deletion.

### 4. Replace an Existing Schedule

1. Call `GET /extractor/{extractorId}/` to retrieve the current schedule configuration.
2. Modify the Schedule Request Body with updated parameters.
3. Call `POST /extractor` with the new body.
4. Verify the update with `GET /extractor/{extractorId}/`.
5. If the old schedule persists as a duplicate, call `DELETE /extractor/{extractorId}/` on the obsolete one.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
