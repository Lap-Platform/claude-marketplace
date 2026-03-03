---
name: data-api
description: "Data API skill. Use when working with Data for contacts, district_admins, districts. Covers 44 endpoints."
version: 1.0.0
generator: lapsh
---

# Data API
API version: 1.2.0

## Auth
OAuth2

## Base URL
https://api.clever.com/v1.2

## Setup
1. Configure auth: OAuth2
2. GET /contacts -- verify access

## Endpoints

44 endpoints across 8 groups. See references/api-spec.lap for full details.

### contacts
| Method | Path | Description |
|--------|------|-------------|
| GET | /contacts | Returns a list of student contacts |
| GET | /contacts/{id} | Returns a specific student contact |
| GET | /contacts/{id}/district | Returns the district for a student contact |
| GET | /contacts/{id}/student | Returns the student for a student contact |

### district_admins
| Method | Path | Description |
|--------|------|-------------|
| GET | /district_admins | Returns a list of district admins |
| GET | /district_admins/{id} | Returns a specific district admin |

### districts
| Method | Path | Description |
|--------|------|-------------|
| GET | /districts | Returns a list of districts. In practice this will only return the one district associated with the bearer token |
| GET | /districts/{id} | Returns a specific district |
| GET | /districts/{id}/admins | Returns the admins for a district |
| GET | /districts/{id}/schools | Returns the schools for a district |
| GET | /districts/{id}/sections | Returns the sections for a district |
| GET | /districts/{id}/status | Returns the status of the district |
| GET | /districts/{id}/students | Returns the students for a district |
| GET | /districts/{id}/teachers | Returns the teachers for a district |

### school_admins
| Method | Path | Description |
|--------|------|-------------|
| GET | /school_admins | Returns a list of school admins |
| GET | /school_admins/{id} | Returns a specific school admin |
| GET | /school_admins/{id}/schools | Returns the schools for a school admin |

### schools
| Method | Path | Description |
|--------|------|-------------|
| GET | /schools | Returns a list of schools |
| GET | /schools/{id} | Returns a specific school |
| GET | /schools/{id}/district | Returns the district for a school |
| GET | /schools/{id}/sections | Returns the sections for a school |
| GET | /schools/{id}/students | Returns the students for a school |
| GET | /schools/{id}/teachers | Returns the teachers for a school |

### sections
| Method | Path | Description |
|--------|------|-------------|
| GET | /sections | Returns a list of sections |
| GET | /sections/{id} | Returns a specific section |
| GET | /sections/{id}/district | Returns the district for a section |
| GET | /sections/{id}/school | Returns the school for a section |
| GET | /sections/{id}/students | Returns the students for a section |
| GET | /sections/{id}/teacher | Returns the primary teacher for a section |
| GET | /sections/{id}/teachers | Returns the teachers for a section |

### students
| Method | Path | Description |
|--------|------|-------------|
| GET | /students | Returns a list of students |
| GET | /students/{id} | Returns a specific student |
| GET | /students/{id}/contacts | Returns the contacts for a student |
| GET | /students/{id}/district | Returns the district for a student |
| GET | /students/{id}/school | Returns the primary school for a student |
| GET | /students/{id}/sections | Returns the sections for a student |
| GET | /students/{id}/teachers | Returns the teachers for a student |

### teachers
| Method | Path | Description |
|--------|------|-------------|
| GET | /teachers | Returns a list of teachers |
| GET | /teachers/{id} | Returns a specific teacher |
| GET | /teachers/{id}/district | Returns the district for a teacher |
| GET | /teachers/{id}/grade_levels | Returns the grade levels for sections a teacher teaches |
| GET | /teachers/{id}/school | Retrieves school info for a teacher. |
| GET | /teachers/{id}/sections | Returns the sections for a teacher |
| GET | /teachers/{id}/students | Returns the students for a teacher |

## Enhanced Skill Content
## Question Mapping

- "How do I list all students in a district?" -> GET /districts/{id}/students
- "Who are the contacts for a specific student?" -> GET /students/{id}/contacts
- "Which school does a student attend?" -> GET /students/{id}/school
- "What sections does a teacher teach?" -> GET /teachers/{id}/sections
- "Who are the teachers at a specific school?" -> GET /schools/{id}/teachers
- "What grade levels does a teacher cover?" -> GET /teachers/{id}/grade_levels
- "Which district does a school belong to?" -> GET /schools/{id}/district
- "How do I find all sections in a school?" -> GET /schools/{id}/sections
- "Who are the district admins?" -> GET /district_admins
- "What is the sync status of a district?" -> GET /districts/{id}/status
- "Which students are in a specific section?" -> GET /sections/{id}/students
- "Who is the primary teacher for a section?" -> GET /sections/{id}/teacher
- "What schools does a school admin manage?" -> GET /school_admins/{id}/schools
- "Which district is a contact associated with?" -> GET /contacts/{id}/district
- "How do I page through all teachers in a district?" -> GET /districts/{id}/teachers (use `starting_after` and `limit`)

## Response Tips

- **List endpoints** (`/students`, `/teachers`, `/schools`, etc.): Responses are cursor-paginated -- use `starting_after` with the last item's ID and `limit` to control page size. There is no total count; an empty page signals the end.
- **Single resource** (`/students/{id}`, `/teachers/{id}`): Returns a `data` wrapper object; the entity lives inside `data`. A 404 means the ID is invalid or the token lacks access.
- **Relationship endpoints** (`/students/{id}/school`, `/sections/{id}/teacher`): Return a single related object (not an array) when the relationship is one-to-one; return a paginated list for one-to-many.
- **Filter parameters** (`where`): Available on most list endpoints under districts, schools, sections, students, and teachers -- not on contacts or district_admins.
- **Include parameter**: Supported on `/districts/{id}`, `/school_admins/{id}`, `/students/{id}`, and `/teachers/{id}` to embed related data inline and reduce follow-up calls.

## Anomaly Flags

- **404 on relationship traversal**: Surface when a nested resource call (e.g., `/students/{id}/school`) returns 404 -- this likely means the parent record was deleted or the OAuth token's scope no longer covers that entity.
- **Empty paginated results on first page**: Flag when a list endpoint returns zero results with no `starting_after` cursor -- the district may not have synced data yet or the token's scope is misconfigured.
- **District status changes**: Proactively check `/districts/{id}/status` and alert if the sync status indicates paused, error, or pending states.
- **Pagination loops**: Detect if `starting_after` returns the same cursor repeatedly, indicating a stuck pagination cycle.
- **OAuth token scope mismatch**: If multiple endpoints return 401 or consistently empty results for a district known to have data, surface a likely token scope or permissions issue.
- **Deprecated `show_links` parameter**: The `show_links` param on `/district_admins` is a legacy toggle -- flag its usage as potentially deprecated behavior.

## Playbook

### 1. Full Student Roster Export for a District

1. Call GET /districts to find the target district ID.
2. Call GET /districts/{id}/students with `limit=100`.
3. Collect all student records, using `starting_after` set to the last student's ID to fetch subsequent pages.
4. Repeat until an empty page is returned.
5. Optionally enrich each student with GET /students/{id}?include=... for additional fields.

### 2. Build a Class Roster (Students and Teachers per Section)

1. Call GET /schools/{id}/sections to list all sections for the school.
2. For each section, call GET /sections/{id}/students to get enrolled students.
3. For each section, call GET /sections/{id}/teachers to get assigned teachers (or /sections/{id}/teacher for the primary teacher).
4. Combine results into a per-section roster keyed by section ID.

### 3. Retrieve a Student's Full Context (School, District, Contacts, Teachers)

1. Call GET /students/{id} to get the student profile.
2. In parallel, call GET /students/{id}/school, GET /students/{id}/district, GET /students/{id}/contacts, and GET /students/{id}/teachers.
3. Merge all responses into a single enriched student record.

### 4. Audit District Admin and School Admin Coverage

1. Call GET /districts/{id}/admins to list all district-level admins.
2. Call GET /districts/{id}/schools to list all schools.
3. For each school, call GET /school_admins with a `where` filter scoped to that school (or iterate GET /school_admins and match).
4. Cross-reference to identify schools with no assigned admin.

### 5. Monitor District Sync Health

1. Call GET /districts to retrieve all accessible districts.
2. For each district, call GET /districts/{id}/status.
3. Flag any district where the status is not healthy or last sync timestamp is stale.
4. Schedule periodic re-checks and alert on status transitions (e.g., healthy to error).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
