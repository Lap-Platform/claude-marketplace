---
name: zoom-api
description: "Zoom API skill. Use when working with Zoom for accounts, groups, h323. Covers 155 endpoints."
version: 1.0.0
generator: lapsh
---

# Zoom API
API version: 2.0.0

## Auth
ApiKey access_token in query

## Base URL
https://api.zoom.us/v2

## Setup
1. Set your API key in the appropriate header
2. GET /accounts -- verify access
3. POST /accounts -- create first accounts

## Endpoints

155 endpoints across 14 groups. See references/api-spec.lap for full details.

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | List sub accounts |
| POST | /accounts | Create a sub account |
| GET | /accounts/{accountId} | Retrieve a sub account |
| DELETE | /accounts/{accountId} | Disassociate an account |
| PATCH | /accounts/{accountId}/options | Update a sub account's options |
| GET | /accounts/{accountId}/settings | Retrieve a sub account's settings |
| PATCH | /accounts/{accountId}/settings | Update a sub account's settings |
| GET | /accounts/{accountId}/managed_domains | Retrieve a sub account's managed domains |
| GET | /accounts/{accountId}/billing | Retrieve billing information for a sub account |
| PATCH | /accounts/{accountId}/billing | Update billing information for a sub account |
| GET | /accounts/{accountId}/plans | Retrieve plan information for a sub account |
| POST | /accounts/{accountId}/plans | Subscribe plans for a sub account |
| PUT | /accounts/{accountId}/plans/base | Update a base plan for a sub account |
| POST | /accounts/{accountId}/plans/addons | Add an additional plan for sub account |
| PUT | /accounts/{accountId}/plans/addons | Update an additional plan for sub account |

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups | List groups |
| POST | /groups | Create a group |
| GET | /groups/{groupId} | Retrieve a group |
| PATCH | /groups/{groupId} | Update a group |
| DELETE | /groups/{groupId} | Delete a group |
| GET | /groups/{groupId}/members | List a group's members |
| POST | /groups/{groupId}/members | Add group members |
| DELETE | /groups/{groupId}/members/{memberId} | Delete a group member |

### h323
| Method | Path | Description |
|--------|------|-------------|
| GET | /h323/devices | List H.323/SIP Devices. |
| POST | /h323/devices | Create a H.323/SIP Device |
| PATCH | /h323/devices/{deviceId} | Update a H.323/SIP Device |
| DELETE | /h323/devices/{deviceId} | Delete a H.323/SIP Device |

### tracking_fields
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/tracking_fields | List Tracking Fields. |
| POST | /v2/tracking_fields | Create a Tracking Field |
| GET | /v2/tracking_fields/{fieldId} | Retrieve a tracking field |
| PATCH | /v2/tracking_fields/{fieldId} | Update a Tracking Field |
| DELETE | /v2/tracking_fields/{fieldId} | Delete a Tracking Field |

### im
| Method | Path | Description |
|--------|------|-------------|
| GET | /im/groups | List IM Groups |
| POST | /im/groups | Create an IM Group |
| GET | /im/groups/{groupId} | Retrieve an IM Group |
| PATCH | /im/groups/{groupId} | Update an IM Group |
| DELETE | /im/groups/{groupId} | Delete an IM Group |
| GET | /im/groups/{groupId}/members | List an IM Group's members |
| POST | /im/groups/{groupId}/members | Add IM Group members |
| DELETE | /im/groups/{groupId}/members/{memberId} | Delete an IM Group member |
| GET | /im/chat/sessions | Retrieve IM Chat sessions |
| GET | /im/chat/sessions/{sessionId} | Retrieve IM Chat messages |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/{userId}/meetings | List meetings |
| POST | /users/{userId}/meetings | Create a meeting |
| GET | /users/{userId}/recordings | List all the recordings |
| GET | /users | List Users |
| POST | /users | Create a user |
| GET | /users/{userId} | Retrieve a user |
| PATCH | /users/{userId} | Update a user |
| DELETE | /users/{userId} | Delete a user |
| GET | /users/{userId}/assistants | List a user's assistants |
| POST | /users/{userId}/assistants | Add assistants |
| DELETE | /users/{userId}/assistants | Delete a user's assistants |
| DELETE | /users/{userId}/assistants/{assistantId} | Delete a user's assistant |
| GET | /users/{userId}/schedulers | List a user's schedulers |
| DELETE | /users/{userId}/schedulers | Delete a user's schedulers |
| DELETE | /users/{userId}/schedulers/{schedulerId} | Delete a user's scheduler |
| POST | /users/{userId}/picture | Upload a user's picture |
| GET | /users/{userId}/settings | Retrieve a user's settings |
| PATCH | /users/{userId}/settings | Update a user's settings |
| PUT | /users/{userId}/status | Update a user's status |
| PUT | /users/{userId}/password | Update a user's password |
| GET | /users/{userId}/permissions | Retrieve a user's permissions |
| GET | /users/{userId}/pac | List user's PAC accounts |
| GET | /users/{userId}/tsp | List user's TSP accounts |
| POST | /users/{userId}/tsp | Add a user's TSP account |
| GET | /users/{userId}/tsp/{tspId} | Retrieve a user's TSP account |
| PATCH | /users/{userId}/tsp/{tspId} | Update a TSP account |
| DELETE | /users/{userId}/tsp/{tspId} | Delete a user's TSP account |
| GET | /users/{userId}/token | Retrieve a user's token |
| DELETE | /users/{userId}/token | Revoke a user's SSO token |
| PUT | /users/{userId}/email | Update a user's email |
| GET | /users/zpk | Verify a user's zpk (Deprecated |
| GET | /users/email | Check a user's email |
| GET | /users/vanity_name | Check a user's personal meeting room name |
| GET | /users/{userId}/webinars | List webinars |
| POST | /users/{userId}/webinars | Create a webinar |

### meetings
| Method | Path | Description |
|--------|------|-------------|
| GET | /meetings/{meetingId} | Retrieve a meeting |
| PATCH | /meetings/{meetingId} | Update a meeting |
| DELETE | /meetings/{meetingId} | Delete a meeting |
| PUT | /meetings/{meetingId}/status | Update a meeting's status |
| GET | /meetings/{meetingId}/invitation | Retrieve meeting invitation |
| GET | /meetings/{meetingId}/registrants | List a meeting's registrants |
| POST | /meetings/{meetingId}/registrants | Add a meeting registrant |
| PUT | /meetings/{meetingId}/registrants/status | Update a meeting registrant's status |
| PATCH | /meetings/{meetingId}/livestream | Update a meeting live stream |
| PATCH | /meetings/{meetingId}/livestream/status | Update a meeting live stream status |
| GET | /meetings/{meetingId}/polls | List a meeting's polls |
| POST | /meetings/{meetingId}/polls | Create a meeting's poll |
| GET | /meetings/{meetingId}/polls/{pollId} | Retrieve a meeting's poll |
| PUT | /meetings/{meetingId}/polls/{pollId} | Update a meeting's poll |
| DELETE | /meetings/{meetingId}/polls/{pollId} | Delete a meeting's Poll |
| GET | /meetings/{meetingId}/recordings | Retrieve a meeting’s all recordings |
| DELETE | /meetings/{meetingId}/recordings | Delete a meeting's recordings |
| DELETE | /meetings/{meetingId}/recordings/{recordingId} | Delete one meeting recording file |
| PUT | /meetings/{meetingId}/recordings/status | Recover a meeting's recordings |
| PUT | /meetings/{meetingId}/recordings/{recordingId}/status | Recover a single recording |
| GET | /meetings/{meetingId}/recordings/settings | Retrieve a meeting recording's settings |
| PATCH | /meetings/{meetingId}/recordings/settings | Update a meeting recording's settings |

### past_meetings
| Method | Path | Description |
|--------|------|-------------|
| GET | /past_meetings/{meetingUUID} | Retrieve past meeting details |
| GET | /past_meetings/{meetingUUID}/participants | Retrieve past meeting participants |
| GET | /past_meetings/{meetingId}/instances | List of ended meeting instances |

### metrics
| Method | Path | Description |
|--------|------|-------------|
| GET | /metrics/meetings | List meetings |
| GET | /metrics/meetings/{meetingId} | Retrieve meeting detail |
| GET | /metrics/meetings/{meetingId}/participants | Retrieve meeting participants |
| GET | /metrics/meetings/{meetingId}/participants/{participantId}/qos | Retrieve meeting participant QOS |
| GET | /metrics/meetings/{meetingId}/participants/qos | List meeting participants QOS |
| GET | /metrics/meetings/{meetingId}/participants/sharing | Retrieve sharing/recording details of meeting participant |
| GET | /metrics/webinars | List webinars |
| GET | /metrics/webinars/{webinarId} | Retrieve webinar detail |
| GET | /metrics/webinars/{webinarId}/participants | Retrieve webinar participants |
| GET | /metrics/webinars/{webinarId}/participants/{participantId}/qos | Retrieve webinar participant QOS |
| GET | /metrics/webinars/{webinarId}/participants/qos | List webinar participant QOS |
| GET | /metrics/webinars/{webinarId}/participants/sharing | Retrieve sharing/recording details of webinar participant |
| GET | /metrics/zoomrooms | List Zoom Rooms |
| GET | /metrics/zoomrooms/{zoomroomId} | Retrieve Zoom Room |
| GET | /metrics/crc | Retrieve CRC Port Usage |
| GET | /metrics/im | Retrieve IM |

### report
| Method | Path | Description |
|--------|------|-------------|
| GET | /report/daily | Retrieve daily report |
| GET | /report/users | Retrieve hosts report |
| GET | /report/users/{userId}/meetings | Retrieve meetings report |
| GET | /report/meetings/{meetingId} | Retrieve meeting details report |
| GET | /report/meetings/{meetingId}/participants | Retrieve meeting participants report |
| GET | /report/meetings/{meetingId}/polls | Retrieve meeting polls report |
| GET | /report/webinars/{webinarId} | Retrieve webinar details report |
| GET | /report/webinars/{webinarId}/participants | Retrieve webinar participants report |
| GET | /report/webinars/{webinarId}/polls | Retrieve webinar polls report |
| GET | /report/webinars/{webinarId}/qa | Retrieve webinar Q&A report |
| GET | /report/telephone | Retrieve telephone report |
| GET | /report/cloud_recording | Retrieve cloud recording usage report |

### tsp
| Method | Path | Description |
|--------|------|-------------|
| GET | /tsp | Retrieve account's TSP information |
| PATCH | /tsp | Update account's TSP information |

### webinars
| Method | Path | Description |
|--------|------|-------------|
| GET | /webinars/{webinarId} | Retrieve a webinar |
| PATCH | /webinars/{webinarId} | Update a webinar |
| DELETE | /webinars/{webinarId} | Delete a webinar |
| PUT | /webinars/{webinarId}/status | Update a webinar's status |
| GET | /webinars/{webinarId}/panelists | List a webinar's panelists |
| POST | /webinars/{webinarId}/panelists | Add a webinar panelist |
| DELETE | /webinars/{webinarId}/panelists | Remove a webinar's panelists |
| DELETE | /webinars/{webinarId}/panelists/{panelistId} | Remove a webinar panelist |
| GET | /webinars/{webinarId}/registrants | List a webinar's registrants |
| POST | /webinars/{webinarId}/registrants | Add a webinar registrant |
| PUT | /webinars/{webinarId}/registrants/status | Update a webinar registrant's status |
| GET | /webinars/{webinarId}/polls | List a webinar's polls |
| POST | /webinars/{webinarId}/polls | Create a webinar's poll |
| GET | /webinars/{webinarId}/polls/{pollId} | Retrieve a webinar's poll |
| PUT | /webinars/{webinarId}/polls/{pollId} | Update a webinar's poll |
| DELETE | /webinars/{webinarId}/polls/{pollId} | Delete a webinar's Poll |

### past_webinars
| Method | Path | Description |
|--------|------|-------------|
| GET | /past_webinars/{webinarId}/instances | List of ended webinar instances |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| PATCH | /webhooks/options | Switch webhook version |
| GET | /webhooks | List webhooks |
| POST | /webhooks | Create a webhook |
| GET | /webhooks/{webhookId} | Retrieve a webhook |
| PATCH | /webhooks/{webhookId} | Update a webhook |
| DELETE | /webhooks/{webhookId} | Delete a webhook |

## Enhanced Skill Content
## Question Mapping

- "How do I list all users in my Zoom account?" -> GET /users
- "How do I create a new meeting for a user?" -> POST /users/{userId}/meetings
- "How do I get details about a specific meeting?" -> GET /meetings/{meetingId}
- "How do I delete a recording from a meeting?" -> DELETE /meetings/{meetingId}/recordings/{recordingId}
- "How do I list all recordings for a user in a date range?" -> GET /users/{userId}/recordings
- "Who attended a past meeting?" -> GET /past_meetings/{meetingUUID}/participants
- "How do I register someone for a webinar?" -> POST /webinars/{webinarId}/registrants
- "How do I check meeting quality metrics for a participant?" -> GET /metrics/meetings/{meetingId}/participants/{participantId}/qos
- "How do I update a user's settings?" -> PATCH /users/{userId}/settings
- "How do I add members to a group?" -> POST /groups/{groupId}/members
- "How do I get the daily usage report?" -> GET /report/daily
- "How do I set up a webhook for event notifications?" -> POST /webhooks
- "How do I approve or deny meeting registrants?" -> PUT /meetings/{meetingId}/registrants/status
- "How do I configure livestreaming for a meeting?" -> PATCH /meetings/{meetingId}/livestream
- "How do I look up a user by email address?" -> GET /users/email

## Response Tips

- **List endpoints** (users, meetings, accounts, groups): Paginated via `page_size` and `page_number` params; response includes `total_records` and `page_count` -- always check if more pages exist.
- **Token-paginated endpoints** (recordings, past meeting participants, metrics, IM chat, reports): Use `next_page_token` from the response for cursor-based pagination; stop when token is empty string.
- **Detail endpoints** (GET by ID): Return the full object; 404 means the resource was deleted or the ID is invalid -- double-check UUID encoding for past meetings.
- **Mutating endpoints** (POST/PATCH/PUT/DELETE): 201 returns the created resource with its new ID; 204 returns no body -- confirm success by status code alone.
- **Report endpoints**: Require `from`/`to` date range params (format: YYYY-MM-DD); `cloud_recording` report may return 300 for ambiguous results.
- **Metrics endpoints**: Support `type` param to filter live vs past sessions; QoS data includes nested audio/video/screen-sharing quality objects.

## Anomaly Flags

- **Rate limiting**: Zoom enforces per-second and daily rate limits. Surface `Retry-After` headers and HTTP 429 responses immediately -- back off exponentially.
- **Past meeting UUID encoding**: UUIDs starting with `/` or containing `//` must be double-URL-encoded, or the API returns 404. Flag when a past_meetings call fails with 404.
- **409 Conflict on creation**: User or account already exists. Surface the conflicting resource details so the caller can update instead of create.
- **300 on cloud recording report**: Ambiguous response -- multiple matches found. Flag this unusual status and suggest narrowing the date range.
- **Token expiration**: The `access_token` query param auth model means tokens can leak in logs. Flag if tokens appear in error messages or redirect URLs.
- **Deprecated pagination**: Some endpoints use `page_number` (offset-based) while newer ones use `next_page_token` (cursor-based). Flag when mixing pagination styles across a workflow.
- **Empty participant lists**: If `past_meetings/{UUID}/participants` returns 200 but zero participants, the meeting data may have been purged (retained ~30 days). Surface a retention warning.

## Playbook

### 1. Schedule a Meeting and Track Registrants

1. List users to find the host: `GET /users?status=active`
2. Create the meeting: `POST /users/{userId}/meetings` with topic, type (2=scheduled), start_time, and settings (approval_type for registration)
3. Share the meeting invitation: `GET /meetings/{meetingId}/invitation`
4. Check registrants: `GET /meetings/{meetingId}/registrants` -- paginate through all pages
5. Approve or deny registrants: `PUT /meetings/{meetingId}/registrants/status` with action and registrant IDs

### 2. Pull Post-Meeting Analytics

1. Get past meeting details: `GET /past_meetings/{meetingUUID}` (double-encode UUID if it starts with `/`)
2. List all participants: `GET /past_meetings/{meetingUUID}/participants` -- use `next_page_token` to paginate
3. Get QoS for a specific participant: `GET /metrics/meetings/{meetingId}/participants/{participantId}/qos`
4. Pull the meeting report: `GET /report/meetings/{meetingId}`
5. Get poll results if applicable: `GET /report/meetings/{meetingId}/polls`

### 3. Manage Webinar with Panelists and Polls

1. Create the webinar: `POST /users/{userId}/webinars` with topic, type, start_time, duration
2. Add panelists: `POST /webinars/{webinarId}/panelists` with array of name/email pairs
3. Create a poll: `POST /webinars/{webinarId}/polls` with title and questions
4. Open registration: registrants self-register or bulk-add via `POST /webinars/{webinarId}/registrants`
5. After the event, review poll results: `GET /report/webinars/{webinarId}/polls` and Q&A: `GET /report/webinars/{webinarId}/qa`

### 4. Set Up Webhook Event Notifications

1. Check current webhook configuration: `GET /webhooks`
2. Create a new webhook: `POST /webhooks` with event types, notification URL, and auth token
3. Verify delivery by checking your endpoint for Zoom's validation request
4. Update webhook settings if needed: `PATCH /webhooks/{webhookId}`
5. Adjust global webhook options: `PATCH /webhooks/options`

### 5. Bulk User Provisioning and Group Assignment

1. Create the user: `POST /users` with action (create/autoCreate/ssoCreate) and user_info
2. Upload profile picture: `POST /users/{userId}/picture` with pic_file
3. Configure user settings: `PATCH /users/{userId}/settings` with feature toggles
4. Create or find a group: `GET /groups` then optionally `POST /groups`
5. Add the user to the group: `POST /groups/{groupId}/members` with member ID


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
