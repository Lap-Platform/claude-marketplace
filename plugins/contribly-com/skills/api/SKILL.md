---
name: contribly
description: "Contribly API skill. Use when working with Contribly for artifact-formats, assignments, change-log. Covers 44 endpoints."
version: 1.0.0
generator: lapsh
---

# Contribly
API version: 1.0.0

## Auth
OAuth2

## Base URL
https://api.contribly.com/1

## Setup
1. Configure auth: OAuth2
2. GET /artifact-formats -- verify access
3. POST /assignments -- create first assignments

## Endpoints

44 endpoints across 22 groups. See references/api-spec.lap for full details.

### artifact-formats
| Method | Path | Description |
|--------|------|-------------|
| GET | /artifact-formats | Artifact formats |

### assignments
| Method | Path | Description |
|--------|------|-------------|
| GET | /assignments | List assignments |
| POST | /assignments | Create a new assignment |
| DELETE | /assignments/{id} | Delete this assignment and all of it's contributions |
| GET | /assignments/{id} | Get a single assigment by id |

### change-log
| Method | Path | Description |
|--------|------|-------------|
| GET | /change-log | Recent changes |

### contribution-refinements
| Method | Path | Description |
|--------|------|-------------|
| GET | /contribution-refinements | List contribution refinement options |

### contribution-refinement-types
| Method | Path | Description |
|--------|------|-------------|
| GET | /contribution-refinement-types | List valid contribution refinement types |

### export
| Method | Path | Description |
|--------|------|-------------|
| POST | /export | Export contributions. |

### export-summary
| Method | Path | Description |
|--------|------|-------------|
| POST | /export-summary | Export contributions preflight summary. |

### exports
| Method | Path | Description |
|--------|------|-------------|
| GET | /exports/{id} | Get a single export job; poll to follow export progress. |

### contributions
| Method | Path | Description |
|--------|------|-------------|
| GET | /contributions | List contributions |
| POST | /contributions | Create a new contribution |
| GET | /contributions/{id} | Get a single contribution by id |
| DELETE | /contributions/{id} | Delete this contribution |
| POST | /contributions/{id}/flag | Raise a flag against this contribution |
| POST | /contributions/{id}/like | Allows a user to mark a contribution as liked |
| GET | /contributions/{id}/likes | List users who have liked this contributions |
| POST | /contributions/{id}/moderate | Perform a moderation action on this contribution |

### credentials
| Method | Path | Description |
|--------|------|-------------|
| GET | /credentials | List the credentials associated with the authenticated user. |

### event-types
| Method | Path | Description |
|--------|------|-------------|
| GET | /event-types | Event types |

### forms
| Method | Path | Description |
|--------|------|-------------|
| GET | /forms | List forms |
| POST | /forms | Create a form |
| GET | /forms/{id} | Get a single form by id |
| DELETE | /forms/{id} | Delete this form and all of it's responses. |

### form-responses
| Method | Path | Description |
|--------|------|-------------|
| POST | /form-responses | Submit a response to a form |
| GET | /form-responses | List form responses |
| GET | /form-responses/{id} | Get a single form response by id |

### media
| Method | Path | Description |
|--------|------|-------------|
| POST | /media | Submit a new media file |

### notifications
| Method | Path | Description |
|--------|------|-------------|
| GET | /notifications/contributions/{id}/preview |  |

### scopes
| Method | Path | Description |
|--------|------|-------------|
| GET | /scopes | Scopes |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions | List subscriptions for the authorised user. |
| DELETE | /subscriptions/{id} | Delete a subscription. |

### subscription-types
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscription-types | Subscription types |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags | List tags |
| POST | /tags | Create a new tag |
| GET | /tags/{id} | Retrieve a single tag by id |

### tagsets
| Method | Path | Description |
|--------|------|-------------|
| GET | /tagsets | List tag sets |
| POST | /tagsets | Create a new tag set |
| GET | /tagsets/{id} | Retrieve a single tag set by id |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | List users |
| GET | /users/{id} | Retrieve a single user by id |
| GET | /users/{id}/linked/{type} | Retrieve a users linked profile by type |

### verify
| Method | Path | Description |
|--------|------|-------------|
| POST | /verify | Verify token and return details of the owning user |

## Enhanced Skill Content
## Question Mapping

- "How do I list all assignments?" -> GET /assignments
- "How do I create a new assignment?" -> POST /assignments
- "How do I delete an assignment?" -> DELETE /assignments/{id}
- "How do I search for contributions by location?" -> GET /contributions (use latLong + radius params)
- "How do I submit a new contribution?" -> POST /contributions
- "How do I moderate a contribution?" -> POST /contributions/{id}/moderate
- "How do I flag inappropriate content?" -> POST /contributions/{id}/flag
- "How do I export contributions matching certain criteria?" -> POST /export
- "How do I check the status of my export?" -> GET /exports/{id}
- "How do I upload media for a contribution?" -> POST /media
- "How do I find users who contributed to a specific assignment?" -> GET /users (use assignment param)
- "How do I like a contribution?" -> POST /contributions/{id}/like
- "How do I create a tag and organize it into a tagset?" -> POST /tagsets then POST /tags (with tagSet reference)
- "How do I preview a notification before sending it?" -> GET /notifications/contributions/{id}/preview
- "How do I verify my OAuth credentials are valid?" -> POST /verify

## Response Tips

- **Assignments/Contributions (list endpoints):** Paginated via `page` and `pageSize` params; default page size varies -- always check total count in response envelope.
- **Export:** Returns 202 Accepted (async); poll GET /exports/{id} until the export object indicates completion.
- **Contributions (single):** Nested media, location, and tag objects; always check for null location and empty media arrays.
- **Moderation/Flag:** 400 means malformed body, 403 means insufficient permissions -- inspect the error message field for details.
- **Users:** Linked profiles accessed via sub-resource /users/{id}/linked/{type}; 404 means the link type does not exist for that user.
- **Tags/Tagsets:** Tags reference tagsets by ID; always resolve the tagset first when filtering.
- **Forms/Form-responses:** Form responses link to both a form ID and optionally a contribution ID; filter accordingly.

## Anomaly Flags

- **OAuth 401 on /credentials:** Token may be expired or revoked -- prompt the user to re-authenticate before retrying other calls.
- **403 on delete/moderate:** The authenticated user lacks ownership or moderator role -- surface this clearly rather than retrying.
- **Export stuck (no completion on poll):** If GET /exports/{id} returns the same incomplete status after several checks, warn that the export may have failed server-side.
- **Empty contribution lists with filters:** When geo filters (latLong, radius, geohash) return zero results, suggest broadening the radius or removing hasLocation constraint.
- **500 on POST /assignments or POST /tags:** Server-side errors on create operations -- surface the response body and suggest retrying once; if persistent, flag as a service issue.
- **Deprecated or unknown media types:** If POST /media returns an unexpected error, flag that the byte format may be unsupported.

## Playbook

### 1. Create an Assignment and Collect Contributions

1. POST /assignments with the assignment body (title, description, constraints)
2. Note the returned assignment `id`
3. Share the assignment ID or URL with contributors
4. Poll GET /contributions?assignment={id} to monitor incoming submissions
5. Use GET /contributions/{id} to inspect individual submissions in detail

### 2. Moderate and Export Contributions

1. GET /contributions?assignment={assignmentId} to list submissions
2. Review each: GET /contributions/{id} for full details including media
3. Flag problematic content: POST /contributions/{id}/flag with reason
4. Moderate as needed: POST /contributions/{id}/moderate with action body
5. Export approved set: POST /export with assignment filter and desired format
6. Poll GET /exports/{exportId} until status shows complete, then download

### 3. Organize Content with Tags and Tagsets

1. POST /tagsets to create a category grouping (e.g., "Topics", "Regions")
2. Note the tagset `id` from the response
3. POST /tags with tagSet reference to create individual tags within the set
4. Apply tags to assignments or contributions as supported by the assignment body
5. Filter contributions by tag: GET /contributions or GET /assignments?tag={tagId}

### 4. Find and Analyze Users

1. GET /users to list all users, or filter by assignment, country, or minimum contributions
2. GET /users/{id} for a specific user profile
3. GET /users/{id}/linked/{type} to retrieve linked social profiles (e.g., Twitter, Facebook)
4. Cross-reference with GET /contributions?user={userId} to see all of a user's submissions
5. Use submittedBefore/submittedAfter on GET /users to find users active in a time window

### 5. Set Up Forms and Collect Responses

1. GET /forms?ownedBy={ownerId} to list existing forms
2. POST /forms with form definition body (fields, validation rules)
3. Note the form `id` from the response
4. Collect responses: POST /form-responses linking to the form ID
5. Review responses: GET /form-responses?form={formId} or GET /form-responses/{id} for a single response


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
