---
name: iqualify-management-api
description: "iQualify Management API skill. Use when working with iQualify Management for root, offerings, course-mappings. Covers 84 endpoints."
version: 1.0.0
generator: lapsh
---

# iQualify Management API
API version: v1

## Auth
ApiKey Authorization in header

## Base URL
https://api.iqualify.com/v1

## Setup
1. Set your API key in the appropriate header
2. GET / -- verify access
3. POST /offerings/{offeringId}/groups -- create first groups

## Endpoints

84 endpoints across 6 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | List supported endpoints URLs |

### offerings
| Method | Path | Description |
|--------|------|-------------|
| GET | /offerings/{offeringId}/analytics/pulses | Find all pulse IDs in the specified offering |
| GET | /offerings/{offeringId}/analytics/pulses/responses | Find pulses by offeringId |
| GET | /offerings/{offeringId}/analytics/pulses/{pulseId}/responses | Find pulses by offeringId and pulseId |
| GET | /offerings/{offeringId}/analytics/marks/assignments | Find assessment marks |
| GET | /offerings/{offeringId}/analytics/marks/quizzes | Find quiz marks |
| GET | /offerings/{offeringId}/analytics/learners-progress | Find learner progress in a specified offering |
| GET | /offerings/{offeringId}/analytics/unit-reactions | Find unit reactions |
| GET | /offerings/{offeringId}/analytics/submissions/assignments | Find submissions to assessments, including marks if any |
| GET | /offerings/{offeringId}/analytics/social-notes | Find shared social notes in an offering |
| GET | /offerings/{offeringId}/analytics/activities/responses | Find open response activity attempts |
| GET | /offerings/{offeringId}/analytics/submissions/open-response/{assessmentId} | Find submissions to a specified open response assessment, including marks if any |
| GET | /offerings/{offeringId}/analytics/submissions/{userEmail}/assignments/{assessmentId} | Find a learner's submission to a specified assessment, including marks if any |
| GET | /offerings/{offeringId}/groups | Find assessment groups |
| POST | /offerings/{offeringId}/groups | Add an assessment group |
| GET | /offerings/{offeringId}/groups/{groupId}/learners | Find learners in an assessment group |
| POST | /offerings/{offeringId}/groups/{groupId}/learners | Add a learner to an assessment group |
| DELETE | /offerings/{offeringId}/groups/{groupId}/learners/{userEmail} | Remove a learner from an assessment group |
| GET | /offerings/{offeringId}/analytics/channels/{channelId}/posts | Find posts |
| GET | /offerings/{offeringId}/analytics/channels/{channelId}/comments | Find comments |
| GET | /offerings/{offeringId}/analytics/channels/{channelId}/replies | Find replies |
| GET | /offerings/{offeringId}/channels | Find channels |
| POST | /offerings/{offeringId}/channels | Add channel |
| PATCH | /offerings/{offeringId}/channels/{channelId} | Update channel |
| POST | /offerings/{offeringId}/channels/{channelId}/learners | Add learners to a group channel |
| DELETE | /offerings/{offeringId}/channels/{channelId}/learners | Remove learners from a group channel |
| GET | /offerings/{offeringId}/channels/{channelId}/learners | Find learners in a group channel |
| GET | /offerings | Find current, past and future offerings |
| POST | /offerings | Create offering |
| GET | /offerings/summary | Offerings summary |
| GET | /offerings/current | Find active offerings |
| GET | /offerings/past | Find past offerings |
| GET | /offerings/future | Find scheduled offerings |
| GET | /offerings/info/{textPattern} | Find offerings where info field matches the specified textPattern |
| GET | /offerings/{offeringId} | Find offering by ID |
| PATCH | /offerings/{offeringId} | Update offering |
| GET | /offerings/{offeringId}/badges | Find offering badges |
| PUT | /offerings/{offeringId}/metadata/tags | Update offering tags metadata |
| PUT | /offerings/{offeringId}/metadata/category | Update offering category metadata |
| PUT | /offerings/{offeringId}/metadata/topic | Update offering topic metadata |
| PUT | /offerings/{offeringId}/metadata/level | Update offering level metadata |
| GET | /offerings/{offeringId}/assessments | Find offering's assessments |
| PATCH | /offerings/{offeringId}/assessments/{assessmentId} | Update assessment details |
| PATCH | /offerings/{offeringId}/assessments/{assessmentId}/{userEmail} | Update the due dates for a learner's quiz attempt |
| DELETE | /offerings/{offeringId}/assessments/{assessmentId}/documents/{documentId} | Remove assessment document |
| GET | /offerings/{offeringId}/learners/pending-submission | Find learners with assessments pending x days before due date within the specified offeringId |
| GET | /offerings/{offeringId}/activities/openresponse | Find offering's activities |
| GET | /offerings/{offeringId}/users | Find offering's users |
| POST | /offerings/{offeringId}/users | Adds user to the offering |
| DELETE | /offerings/{offeringId}/users/{userEmail} | Removes user from the offering |
| GET | /offerings/{offeringId}/users/{markerEmail}/marks | Find Learners marked by a coach |
| POST | /offerings/{offeringId}/users/{markerEmail}/marks | Add learners to be marked by a coach |
| DELETE | /offerings/{offeringId}/users/{markerEmail}/marks | Remove learners from coach's marking list |
| POST | /offerings/{offeringId}/users/{userEmail}/badges/award | Award badge |
| GET | /offerings/{offeringId}/users/{userEmail}/submissions/open-response | Find learner's open response assessment submissions |
| DELETE | /offerings/{offeringId}/users/{userEmail}/assessments/{assessmentId} | Reset user's assessment to draft state |

### course-mappings
| Method | Path | Description |
|--------|------|-------------|
| GET | /course-mappings | Find course mappings |
| GET | /course-mappings/externalcourse/{externalCourseId} | Find course mappings by externalCourseId |
| GET | /course-mappings/{offeringId} | Find course mappings by offeringId |
| PUT | /course-mappings/{offeringId}/{externalCourseId} | Add course mapping |
| DELETE | /course-mappings/{offeringId}/{externalCourseId} | Remove course mapping |

### courses
| Method | Path | Description |
|--------|------|-------------|
| GET | /courses | Find courses |
| GET | /courses/{contentId} | Find course by contentId |
| GET | /courses/{contentId}/activations | Find activations for a contentId |
| PUT | /courses/{contentId}/metadata/tags | Update course tags |
| PUT | /courses/{contentId}/metadata/category | Update course category |
| PUT | /courses/{contentId}/metadata/level | Update course level |
| PUT | /courses/{contentId}/metadata/topic | Update course topic |
| POST | /courses/{rootContentId}/permissions/{userEmail} | Update course access |
| GET | /courses/{contentId}/permissions | Find users who have access to the contentId provided |

### org
| Method | Path | Description |
|--------|------|-------------|
| GET | /org | Gets the current organisation |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/{userEmail} | Find user by email |
| PATCH | /users/{userEmail} | Update user |
| PUT | /users/{userEmail}/suspend | Suspend user |
| GET | /users/{userEmail}/offerings | Find user's offerings |
| POST | /users/{userEmail}/offerings | Adds the user to the specified offerings as a learner |
| GET | /users/{userEmail}/offerings/{offeringId}/progress | Find learner's progress in a specified offering |
| POST | /users/{userEmail}/permissions/{permissionName} | Add permission to user |
| GET | /users/all/progress | Find learner progress in all offerings |
| GET | /users/{userEmail}/progress | Find learner's progress in offerings |
| GET | /users/{userEmail}/badges | Find user's badges |
| PATCH | /users/{userEmail}/transfer | Transfer a user between offerings |
| POST | /users/{userEmail}/invite-email | Resend invitation email |
| POST | /users | Add new user |

## Enhanced Skill Content
## Question Mapping

- "What courses are available in my organization?" -> GET /courses
- "Show me details for a specific offering" -> GET /offerings/{offeringId}
- "How are learners progressing in this offering?" -> GET /offerings/{offeringId}/analytics/learners-progress
- "What are the quiz scores for an offering?" -> GET /offerings/{offeringId}/analytics/marks/quizzes
- "Who are the users enrolled in this offering?" -> GET /offerings/{offeringId}/users
- "Create a new offering starting next Monday" -> POST /offerings
- "Add a learner to a group in an offering" -> POST /offerings/{offeringId}/groups/{groupId}/learners
- "Remove a user from an offering" -> DELETE /offerings/{offeringId}/users/{userEmail}
- "What badges has a user earned?" -> GET /users/{userEmail}/badges
- "Transfer a learner from one offering to another" -> PATCH /users/{userEmail}/transfer
- "Get all pulse responses filtered by MCQ type" -> GET /offerings/{offeringId}/analytics/pulses/responses
- "Map an external course ID to an iQualify offering" -> PUT /course-mappings/{offeringId}/{externalCourseId}
- "Suspend a user account" -> PUT /users/{userEmail}/suspend
- "Award a badge to a specific learner" -> POST /offerings/{offeringId}/users/{userEmail}/badges/award
- "Which learners have pending assignment submissions?" -> GET /offerings/{offeringId}/learners/pending-submission

## Response Tips

- **Offerings**: Full offering objects include deeply nested `settings`, `metadata`, `studyPlan`, and `badge.badgeExpiry` maps -- always drill into these rather than treating them as opaque.
- **Analytics**: Analytics endpoints (pulses, marks, progress, reactions) return 200 with untyped payloads -- inspect the shape on first call and cache the structure for subsequent parsing.
- **Users**: User objects embed `profile`, `metadata.tags[]`, and `invite.url` -- the invite URL is only present for users who haven't yet accepted.
- **Groups/Channels**: POST returns 201 with the created resource; DELETE returns 204 with no body -- check status code, not response body, for deletions.
- **Assessments**: PATCH on assessments returns a rich object with `themes[]`, `documents[]`, and nullable fields like `dueDate` -- absent dates mean no deadline is set.
- **Course Mappings**: All mapping endpoints return 200 uniformly for both reads and writes -- distinguish success by the HTTP method you called.
- **Bulk Users**: POST to offering users can return either 201 (all succeeded) or 207 (multi-status, partial success) -- always check for 207 and iterate individual results.
- **Summary/Progress**: Endpoints accepting `$top`, `$orderby`, `$filter` use OData-style query parameters -- default page size is 50, paginate by adjusting `$top`.

## Anomaly Flags

- **207 Multi-Status on user enrollment**: Surface immediately when POST /offerings/{offeringId}/users returns 207 -- some users failed to enroll and need individual attention.
- **Offering date conflicts**: Flag when `earlyCloseOffDate` is set but `hasEarlyCloseOff` is false, or when `end` is before `start` in offering responses.
- **Stale learner access**: Alert when `lastAccessAt` on a user in an active offering is more than 14 days old -- likely disengaged learner.
- **Empty analytics responses**: Surface when analytics endpoints return 200 but with empty data arrays -- may indicate the offering has no activity yet or the offeringId is wrong.
- **Missing invite URL**: Flag when a newly created user response lacks `invite.url` -- the invite email may not have been sent (check `sendInvite` parameter).
- **Badge award failure**: Surface when POST badge/award returns `awarded: false` -- the learner did not meet badge criteria and no badge was issued.
- **403 on analytics**: Proactively note that 403 across analytics endpoints likely means the API key lacks insights/manager permissions, not that the offering is missing.

## Playbook

### Onboard a New Learner into an Offering

1. Create the user: POST /users with `firstName`, `lastName`, `email`, and `sendInvite: true`
2. Note the `invite.url` from the response for manual follow-up if needed
3. Enroll the user: POST /offerings/{offeringId}/users with the user's email in the body
4. Check for 201 (success) vs 207 (partial failure) on the enrollment response
5. Optionally add the learner to a group: POST /offerings/{offeringId}/groups/{groupId}/learners

### Review Learner Performance for an Offering

1. Get the offering details: GET /offerings/{offeringId} to confirm the offering is active
2. Pull learner progress: GET /offerings/{offeringId}/analytics/learners-progress
3. Get assignment marks: GET /offerings/{offeringId}/analytics/marks/assignments
4. Get quiz marks: GET /offerings/{offeringId}/analytics/marks/quizzes
5. For specific learner submissions: GET /offerings/{offeringId}/analytics/submissions/{userEmail}/assignments/{assessmentId}

### Set Up a New Offering with Channels and Groups

1. Create the offering: POST /offerings with `start`, `name`, `contentId`, and desired settings
2. Create discussion channels: POST /offerings/{offeringId}/channels with `title` and optional `isBroadcastOnly`
3. Create learner groups: POST /offerings/{offeringId}/groups with `title`
4. Enroll users: POST /offerings/{offeringId}/users (batch)
5. Assign learners to channels: POST /offerings/{offeringId}/channels/{channelId}/learners
6. Assign learners to groups: POST /offerings/{offeringId}/groups/{groupId}/learners

### Transfer a Learner Between Offerings

1. Look up the user: GET /users/{userEmail} to confirm the account exists
2. Verify source enrollment: GET /users/{userEmail}/offerings to see current offerings
3. Check the user's progress: GET /users/{userEmail}/offerings/{offeringId}/progress to document current state
4. Execute the transfer: PATCH /users/{userEmail}/transfer with `fromOfferingId`, `toOfferingId`, and `sendInvite: true`
5. Verify new enrollment: GET /users/{userEmail}/offerings to confirm the transfer landed

### Map External LMS Courses to iQualify

1. List existing mappings: GET /course-mappings to see what is already linked
2. Find the iQualify offering: GET /offerings/info/{textPattern} to search by name
3. Create the mapping: PUT /course-mappings/{offeringId}/{externalCourseId}
4. Verify: GET /course-mappings/externalcourse/{externalCourseId} to confirm the link
5. To remove a stale mapping: DELETE /course-mappings/{offeringId}/{externalCourseId}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
