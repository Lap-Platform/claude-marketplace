---
name: fitbit-plus-api
description: "Fitbit Plus API skill. Use when working with Fitbit Plus for oauth, organization, group. Covers 62 endpoints."
version: 1.0.0
generator: lapsh
---

# Fitbit Plus API
API version: v7.78.1

## Auth
OAuth2

## Base URL
https://api.twinehealth.com/pub

## Setup
1. Configure auth: OAuth2
2. GET /group -- verify access
3. POST /oauth/token -- create first token

## Endpoints

62 endpoints across 22 groups. See references/api-spec.lap for full details.

### oauth
| Method | Path | Description |
|--------|------|-------------|
| POST | /oauth/token | Create an oauth token |
| GET | /oauth/token/{id}/groups | Get the groups for a token |
| GET | /oauth/token/{id}/organization | Get the organization for a token |

### organization
| Method | Path | Description |
|--------|------|-------------|
| GET | /organization/{id} | Get an organization |

### group
| Method | Path | Description |
|--------|------|-------------|
| POST | /group | Create a group |
| GET | /group | List groups |
| GET | /group/{id} | Get a group |

### coach
| Method | Path | Description |
|--------|------|-------------|
| GET | /coach | List coaches |
| GET | /coach/{id} | Get a coach |

### reward_program
| Method | Path | Description |
|--------|------|-------------|
| POST | /reward_program | Create a reward program |
| GET | /reward_program | List reward programs |
| GET | /reward_program/{id} | Get a reward program |
| GET | /reward_program/{id}/group | Get group for a reward program |

### action
| Method | Path | Description |
|--------|------|-------------|
| POST | /action | Create action |
| GET | /action/{id} | Get an action |
| PATCH | /action/{id} | Update an action |

### bundle
| Method | Path | Description |
|--------|------|-------------|
| POST | /bundle | Create bundle |
| GET | /bundle/{id} | Get a bundle |
| PATCH | /bundle/{id} | Update a bundle |

### calendar_event
| Method | Path | Description |
|--------|------|-------------|
| POST | /calendar_event | Create calendar event |
| GET | /calendar_event | List calendar events |
| GET | /calendar_event/{id} | Get a calendar event |
| PATCH | /calendar_event/{id} | Update a calendar event |
| DELETE | /calendar_event/{id} | Delete a calendar event |

### calendar_event_response
| Method | Path | Description |
|--------|------|-------------|
| POST | /calendar_event_response | Create calendar event response |

### email_history
| Method | Path | Description |
|--------|------|-------------|
| GET | /email_history | List email histories |
| GET | /email_history/{id} | Get an email history |

### health_profile
| Method | Path | Description |
|--------|------|-------------|
| GET | /health_profile | List health profiles |
| GET | /health_profile/{id} | Get a health profile |

### health_profile_question
| Method | Path | Description |
|--------|------|-------------|
| GET | /health_profile_question | List health profile questions |
| GET | /health_profile_question/{id} | Get a health profile question |

### health_profile_answer
| Method | Path | Description |
|--------|------|-------------|
| GET | /health_profile_answer | List health profile answers |
| GET | /health_profile_answer/{id} | Get a health profile answer |

### health_question_definition
| Method | Path | Description |
|--------|------|-------------|
| GET | /health_question_definition | List health question definitions |
| GET | /health_question_definition/{id} | Get a health question definition |

### patient_health_metric
| Method | Path | Description |
|--------|------|-------------|
| POST | /patient_health_metric | Create patient health metrics |
| GET | /patient_health_metric | List patient health metrics |
| GET | /patient_health_metric/{id} | Get a patient health metric |

### patient
| Method | Path | Description |
|--------|------|-------------|
| POST | /patient | Create a patient |
| GET | /patient | List patients |
| PUT | /patient | Upsert patient |
| GET | /patient/{id} | Get a patient |
| PATCH | /patient/{id} | Update a patient |
| GET | /patient/{id}/groups | List groups for a patient |
| GET | /patient/{id}/coaches | List coaches for a patient |

### patient_plan_summary
| Method | Path | Description |
|--------|------|-------------|
| GET | /patient_plan_summary | List patient plan summaries |
| GET | /patient_plan_summary/{id} | Get the plan summary for a patient |
| PATCH | /patient_plan_summary/{id} | Update a plan summary |

### result
| Method | Path | Description |
|--------|------|-------------|
| GET | /result | List patient health results |
| GET | /result/{id} | Get a patient health result |

### reward
| Method | Path | Description |
|--------|------|-------------|
| POST | /reward | Create a reward |
| GET | /reward | List rewards |
| GET | /reward/{id} | Get a reward |

### reward_earning
| Method | Path | Description |
|--------|------|-------------|
| POST | /reward_earning | Create a reward earning |
| GET | /reward_earning | List reward earnings |
| GET | /reward_earning/{id} | Get a reward earning |

### reward_earning_fulfillment
| Method | Path | Description |
|--------|------|-------------|
| POST | /reward_earning_fulfillment | Create a reward earning fulfillment |
| GET | /reward_earning_fulfillment | List reward earning fulfillments |
| GET | /reward_earning_fulfillment/{id} | Get a reward earning fulfillment |

### reward_program_activation
| Method | Path | Description |
|--------|------|-------------|
| POST | /reward_program_activation | Create a reward program activation |
| GET | /reward_program_activation | List reward program activations |
| GET | /reward_program_activation/{id} | Get a reward program activation |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the Fitbit Plus API?" -> POST /oauth/token
- "What groups does my token have access to?" -> GET /oauth/token/{id}/groups
- "Which organization is associated with my token?" -> GET /oauth/token/{id}/organization
- "How do I list all patients in a group?" -> GET /patient?filter[groups]={groupId}
- "How do I create a new patient record?" -> POST /patient
- "What coaches are assigned to a specific patient?" -> GET /patient/{id}/coaches
- "How do I schedule a calendar event for a patient?" -> POST /calendar_event
- "How do I look up a patient's health metrics?" -> GET /patient_health_metric?filter[patient]={patientId}
- "How do I record a new health metric for a patient?" -> POST /patient_health_metric
- "What rewards has a patient earned?" -> GET /reward_earning?filter[groups]={groupId}
- "How do I fulfill a reward earning?" -> POST /reward_earning_fulfillment
- "How do I view a patient's plan summary?" -> GET /patient_plan_summary?filter[patient]={patientId}
- "How do I update a patient's action?" -> PATCH /action/{id}
- "How do I check results for a specific patient and action?" -> GET /result?filter[patient]={patientId}&filter[actions]={actionId}
- "How do I see emails sent to a patient?" -> GET /email_history?filter[receiver]={receiverId}

## Response Tips

- **OAuth/Auth**: Token responses return on 201; extract the token ID for subsequent `/groups` and `/organization` lookups.
- **List endpoints** (patient, coach, group, reward): Responses likely use JSON:API envelope (`data`, `included`, `meta`); use the `include` param to sideload related resources and reduce round-trips.
- **Filter-required endpoints** (result, reward_earning, reward_earning_fulfillment): These require at least one filter param -- omitting it will return a 401 or 409, not an unfiltered list.
- **PATCH/PUT endpoints**: 409 on conflict means a concurrent update or validation failure; re-fetch the resource and retry with current state.
- **Health profiles**: Use `include` to pull nested questions and answers in a single call instead of three separate requests.
- **Calendar events**: DELETE returns 200 (not 204); expect a confirmation body rather than empty response.

## Anomaly Flags

- **409 Conflict on writes**: Surface immediately -- indicates data contention or validation failure that requires user attention before retrying.
- **401 on previously working calls**: OAuth token may have expired; prompt re-authentication via POST /oauth/token.
- **403 on group-scoped resources**: The token lacks permission for the target group; surface which group was requested and suggest checking token scope via GET /oauth/token/{id}/groups.
- **Missing `filter` on required-filter endpoints**: If GET /result or GET /reward_earning returns an error, flag that the required filter parameter was omitted.
- **Empty `included` arrays**: When `include` param is used but response has no sideloaded data, flag potential data integrity issue (e.g., patient exists but has no health profile).
- **Deprecated API base**: The base URL uses `api.twinehealth.com` (Twine Health branding); if responses include deprecation headers or redirect notices, surface them proactively.

## Playbook

### 1. Onboard a New Patient

1. Authenticate: POST /oauth/token with credentials to get a session token.
2. Identify the organization: GET /oauth/token/{tokenId}/organization.
3. List available groups: GET /group?filter[organization]={orgId}.
4. Create the patient: POST /patient with patient details and group assignment.
5. Verify enrollment: GET /patient/{id}/groups to confirm group membership.
6. Assign a coach: confirm assignment via GET /patient/{id}/coaches.

### 2. Record and Review Health Metrics

1. Retrieve the patient's health profile: GET /health_profile?filter[patient]={patientId}&include=questions,answers.
2. Post a new metric: POST /patient_health_metric with the measurement data.
3. Verify the metric was recorded: GET /patient_health_metric/{id}.
4. Check related results: GET /result?filter[patient]={patientId} to see how the metric affects plan outcomes.
5. Update the plan summary if needed: PATCH /patient_plan_summary/{id}.

### 3. Manage Reward Program Lifecycle

1. Create a reward program: POST /reward_program with program rules.
2. Activate for a patient: POST /reward_program_activation linking patient to program.
3. Define a reward: POST /reward with reward details.
4. Monitor earnings: GET /reward_earning?filter[groups]={groupId}&filter[ready_for_fulfillment]=true.
5. Fulfill earned rewards: POST /reward_earning_fulfillment for each qualifying earning.

### 4. Schedule and Track Calendar Events

1. Create an event: POST /calendar_event with patient, time, and event type.
2. List upcoming events: GET /calendar_event?filter[patient]={patientId}.
3. Record a patient response: POST /calendar_event_response with attendance or feedback.
4. Reschedule if needed: PATCH /calendar_event/{id} with updated time.
5. Cancel if necessary: DELETE /calendar_event/{id}.

### 5. Audit Communication History

1. List emails for a patient: GET /email_history?filter[receiver]={patientId}&sort=-date.
2. Inspect a specific email: GET /email_history/{id} for full content and delivery status.
3. Cross-reference with calendar events: GET /calendar_event?filter[patient]={patientId} to correlate reminders with scheduled visits.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
