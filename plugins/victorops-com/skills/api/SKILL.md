---
name: victorops-api
description: "VictorOps API skill. Use when working with VictorOps for api-public, api-reporting. Covers 96 endpoints."
version: 1.0.0
generator: lapsh
---

# VictorOps API
API version: 0.0.3

## Auth
ApiKey X-VO-Api-Key in header

## Base URL
https://api.victorops.com/

## Setup
1. Set your API key in the appropriate header
2. GET /api-public/v1/user -- verify access
3. POST /api-public/v1/user -- create first user

## Endpoints

96 endpoints across 2 groups. See references/api-spec.lap for full details.

### api-public
| Method | Path | Description |
|--------|------|-------------|
| POST | /api-public/v1/user | Add a user |
| GET | /api-public/v1/user | List users |
| GET | /api-public/v2/user | List users |
| POST | /api-public/v1/user/batch | Add multiple users |
| GET | /api-public/v1/user/{user} | Retrieve information for a user |
| PUT | /api-public/v1/user/{user} | Update a user |
| DELETE | /api-public/v1/user/{user} | Remove a user |
| GET | /api-public/v1/user/{user}/teams | Retrieve the user's team membership |
| GET | /api-public/v1/policies/types/notifications | Get the available notification types |
| GET | /api-public/v1/policies/types/contacts | Get the available contact types |
| GET | /api-public/v1/policies/types/timeouts | Get the available timeout values |
| GET | /api-public/v1/profile/{username}/policies | Get the user's primary paging policy |
| POST | /api-public/v1/profile/{username}/policies | Create a paging policy step |
| GET | /api-public/v1/profile/{username}/policies/{step} | Get a paging policy step |
| PUT | /api-public/v1/profile/{username}/policies/{step} | Update a paging policy step |
| POST | /api-public/v1/profile/{username}/policies/{step} | Create a rule for a paging policy step |
| GET | /api-public/v1/profile/{username}/policies/{step}/{rule} | Get a rule from a paging policy step |
| PUT | /api-public/v1/profile/{username}/policies/{step}/{rule} | Update a rule for a paging policy step |
| DELETE | /api-public/v1/profile/{username}/policies/{step}/{rule} | Delete a rule from a paging policy step |
| GET | /api-public/v2/profile/{username}/policies | Get the user's paging policies |
| GET | /api-public/v1/user/{user}/contact-methods | Get a list of all contact methods for a user |
| GET | /api-public/v1/user/{user}/contact-methods/devices | Get a list of all contact devices for a user |
| GET | /api-public/v1/user/{user}/contact-methods/devices/{contactId} | Get the indicated contact device for a user |
| PUT | /api-public/v1/user/{user}/contact-methods/devices/{contactId} | Update a contact device for a user |
| DELETE | /api-public/v1/user/{user}/contact-methods/devices/{contactId} | Delete a contact device for a user |
| GET | /api-public/v1/user/{user}/contact-methods/emails | Get a list of all contact emails for a user |
| POST | /api-public/v1/user/{user}/contact-methods/emails | Create a contact emails for a user |
| GET | /api-public/v1/user/{user}/contact-methods/emails/{contactId} | Get the indicated contact email for a user |
| DELETE | /api-public/v1/user/{user}/contact-methods/emails/{contactId} | Delete a contact email for a user |
| GET | /api-public/v1/user/{user}/contact-methods/phones | Get a list of all contact phones for a user |
| POST | /api-public/v1/user/{user}/contact-methods/phones | Create a contact phones for a user |
| GET | /api-public/v1/user/{user}/contact-methods/phones/{contactId} | Get the indicated contact phone for a user |
| DELETE | /api-public/v1/user/{user}/contact-methods/phones/{contactId} | Delete a contact phone for a user |
| GET | /api-public/v1/user/{user}/policies | Get a list of paging policies for a user |
| GET | /api-public/v1/user/{user}/oncall/schedule | Get a user's on-call schedule |
| GET | /api-public/v2/user/{user}/oncall/schedule | Get a user's on-call schedule |
| GET | /api-public/v1/team/{team}/oncall/schedule | Get a team's on-call schedule |
| GET | /api-public/v2/team/{team}/oncall/schedule | Get a team's on-call schedule |
| GET | /api-public/v1/oncall/current | Get an organization's on-call users |
| PATCH | /api-public/v1/team/{team}/oncall/user | Create an on-call override (take on-call) |
| PATCH | /api-public/v1/policies/{policy}/oncall/user | Create an on-call override (take on-call) |
| GET | /api-public/v1/incidents/{incidentNumber} | Get a single incident |
| GET | /api-public/v1/incidents | Get current incident information |
| POST | /api-public/v1/incidents | Create a new incident |
| PATCH | /api-public/v1/incidents/ack | Acknowledge an incident or list of incidents |
| POST | /api-public/v1/incidents/reroute | Reroute one or more incidents to one or more new routable destinations. |
| PATCH | /api-public/v1/incidents/resolve | Resolve an incident or list of incidents |
| PATCH | /api-public/v1/incidents/byUser/ack | Acknowledge all incidents for which a user was paged. |
| PATCH | /api-public/v1/incidents/byUser/resolve | Resolve all incidents for which a user was paged. |
| GET | /api-public/v1/incidents/{incidentNumber}/notes | Get the notes associated with an incident |
| POST | /api-public/v1/incidents/{incidentNumber}/notes | Create a new Note |
| PUT | /api-public/v1/incidents/{incidentNumber}/notes/{noteName} | Update a Note |
| DELETE | /api-public/v1/incidents/{incidentNumber}/notes/{noteName} | Delete a Note |
| GET | /api-public/v1/alerts/{uuid} | Retrieve alert details. |
| GET | /api-public/v1/org/routing-keys | List routing keys with associated teams |
| POST | /api-public/v1/org/routing-keys | Create a new routing key |
| GET | /api-public/v1/overrides | List the scheduled overrides |
| POST | /api-public/v1/overrides | Creates a new scheduled override |
| GET | /api-public/v1/overrides/{publicId} | Get the specified scheduled override |
| DELETE | /api-public/v1/overrides/{publicId} | Deletes a scheduled override |
| GET | /api-public/v1/overrides/{publicId}/assignments | Get the specified scheduled override |
| GET | /api-public/v1/overrides/{publicId}/assignments/{policySlug} | Get the specified scheduled override assignment |
| PUT | /api-public/v1/overrides/{publicId}/assignments/{policySlug} | Update the scheduled override assignment |
| DELETE | /api-public/v1/overrides/{publicId}/assignments/{policySlug} | Delete the scheduled override assignment |
| GET | /api-public/v1/teams/{team}/rotations | Get all rotation groups for a team |
| POST | /api-public/v1/teams/{team}/rotations | Create a rotation group |
| DELETE | /api-public/v1/teams/{team}/rotations/{groupId} | Delete a rotation group |
| GET | /api-public/v1/teams/{team}/rotations/{groupId}/{shiftId}/scheduled | Get the scheduled user for a shift |
| PUT | /api-public/v1/teams/{team}/rotations/{groupId}/{shiftId}/scheduled | Set the scheduled user for a shift |
| GET | /api-public/v2/team/{team}/rotations | Get all rotations and some rotation details for a team |
| GET | /api-public/v1/webhooks | Get all of your organization's webhooks |
| GET | /api-public/v1/policies | Get a list of escalation policy info |
| POST | /api-public/v1/policies | Create an escalation policy |
| GET | /api-public/v1/policies/{policy} | Get a specific escalation policy |
| DELETE | /api-public/v1/policies/{policy} | Delete a specified escalation policy |
| POST | /api-public/v1/team | Add a team |
| GET | /api-public/v1/team | List teams |
| GET | /api-public/v1/team/{team} | Retrieve information for a team |
| PUT | /api-public/v1/team/{team} | Update a team |
| DELETE | /api-public/v1/team/{team} | Remove a team |
| GET | /api-public/v1/team/{team}/policies | Retrieve a list of escalation policies for a team |
| GET | /api-public/v1/team/{team}/admins | Retrieve a list of team admins for a team |
| GET | /api-public/v1/team/{team}/members | Retrieve a list of members for a team |
| POST | /api-public/v1/team/{team}/members | Add a team member |
| DELETE | /api-public/v1/team/{team}/members/{user} | Remove a team member |
| GET | /api-public/v1/maintenancemode | Get an organization's current maintenance mode state |
| POST | /api-public/v1/maintenancemode/start | Start maintenance mode for routing keys |
| PUT | /api-public/v1/maintenancemode/{maintenancemodeid}/end | End maintenance mode for routing keys |
| POST | /api-public/v1/chat | Send a chat message into VictorOps |
| POST | /api-public/v1/stakeholders/sendMessage | Sends a stakeholder message to the recipients. Recipients can either be User/team or both. |
| GET | /api-public/v1/alertRules | Get all alert rules |
| POST | /api-public/v1/alertRules | Create alert rule |
| PUT | /api-public/v1/alertRules/{ruleId} | Update alert rule |
| DELETE | /api-public/v1/alertRules/{ruleId} | Delete alert rule |

### api-reporting
| Method | Path | Description |
|--------|------|-------------|
| GET | /api-reporting/v1/team/{team}/oncall/log | A list of shift changes for a team |
| GET | /api-reporting/v2/incidents | Get/search incident history |

## Enhanced Skill Content
## Question Mapping

- "Who is currently on call?" -> GET /api-public/v1/oncall/current
- "What is a user's on-call schedule?" -> GET /api-public/v2/user/{user}/oncall/schedule
- "List all open incidents" -> GET /api-public/v1/incidents
- "Get details for incident #1234" -> GET /api-public/v1/incidents/{incidentNumber}
- "Acknowledge one or more incidents" -> PATCH /api-public/v1/incidents/ack
- "Resolve incidents assigned to me" -> PATCH /api-public/v1/incidents/byUser/resolve
- "Create a new user account" -> POST /api-public/v1/user
- "What teams does a user belong to?" -> GET /api-public/v1/user/{user}/teams
- "Add an email contact method for a user" -> POST /api-public/v1/user/{user}/contact-methods/emails
- "Put the system into maintenance mode" -> POST /api-public/v1/maintenancemode/start
- "Search incident history with filters" -> GET /api-reporting/v2/incidents
- "Create a new escalation policy" -> POST /api-public/v1/policies
- "Override who is on call for a policy" -> PUT /api-public/v1/overrides/{publicId}/assignments/{policySlug}
- "Take someone on or off call immediately" -> PATCH /api-public/v1/team/{team}/oncall/user
- "Send a stakeholder notification" -> POST /api-public/v1/stakeholders/sendMessage

## Response Tips

- **Users**: List endpoints return arrays of user objects; v2 adds optional `email` filter for narrowing results.
- **Incidents**: `GET /incidents` returns all current incidents; use `GET /api-reporting/v2/incidents` with `offset`/`limit` for paginated historical queries filtered by phase, host, service, or routing key.
- **On-call schedules**: Responses are shaped by `daysForward`, `daysSkip`, and `step` params; omitting them returns defaults (typically 14 days forward).
- **Contact methods**: Three sub-resources (devices, emails, phones) each return their own list; aggregate by calling all three.
- **Policies/Overrides**: Nested step/rule structure -- policies contain steps, steps contain rules; address each level by its own path segment.
- **Errors**: 422 indicates validation failure (check required body fields); 409 signals conflict (duplicate user, maintenance mode already active); 429 means rate limit hit.

## Anomaly Flags

- **429 on schedules or stakeholder messages**: Rate limit reached -- surface immediately and suggest backing off or batching requests.
- **409 on user creation or maintenance mode**: Conflict state -- alert that the resource already exists or mode is already active before retrying.
- **422 on any write**: Validation failure -- surface the response body which typically contains field-level error details.
- **Maintenance mode active**: When `GET /maintenancemode` returns an active mode, warn that alerts may be suppressed and incidents won't trigger escalations.
- **Empty on-call response**: If `GET /oncall/current` returns no users, flag that no one is currently on call -- this is a coverage gap that needs attention.
- **Deprecated v1 vs v2 endpoints**: When a v2 exists (users, on-call schedule, rotations, policies, incidents reporting), flag if the agent is using the v1 variant and suggest upgrading.
- **420 on maintenance mode start**: Non-standard status code unique to this API -- surface as "enhancement already active or rate limited."

## Playbook

### 1. Respond to a New Incident

1. GET /api-public/v1/incidents -- list current incidents, identify the new one
2. GET /api-public/v1/incidents/{incidentNumber} -- get full details
3. GET /api-public/v1/oncall/current -- confirm who is on call
4. PATCH /api-public/v1/incidents/ack -- acknowledge the incident (pass incident names in body)
5. POST /api-public/v1/incidents/{incidentNumber}/notes -- add a timeline note with initial findings
6. PATCH /api-public/v1/incidents/resolve -- resolve once remediated

### 2. Onboard a New Team Member

1. POST /api-public/v1/user -- create the user account
2. POST /api-public/v1/user/{user}/contact-methods/emails -- add email contact
3. POST /api-public/v1/user/{user}/contact-methods/phones -- add phone contact
4. POST /api-public/v1/team/{team}/members -- add user to their team
5. POST /api-public/v1/profile/{username}/policies -- set up their personal notification policy

### 3. Set Up a Temporary On-Call Override

1. GET /api-public/v1/team/{team}/oncall/schedule -- review current schedule
2. POST /api-public/v1/overrides -- create a new override with start/end times
3. PUT /api-public/v1/overrides/{publicId}/assignments/{policySlug} -- assign the override to the target policy
4. GET /api-public/v1/overrides/{publicId} -- verify the override is active
5. DELETE /api-public/v1/overrides/{publicId} -- remove when no longer needed

### 4. Investigate Historical Incidents

1. GET /api-reporting/v2/incidents?startedAfter=...&startedBefore=... -- query by date range
2. Filter further with `currentPhase`, `routingKey`, `host`, or `service` params
3. Use `offset` and `limit` to paginate through large result sets
4. GET /api-public/v1/incidents/{incidentNumber}/notes -- pull timeline notes for specific incidents
5. GET /api-reporting/v1/team/{team}/oncall/log?start=...&end=... -- correlate with on-call log to see who responded

### 5. Enter and Exit Maintenance Mode

1. GET /api-public/v1/maintenancemode -- check if maintenance mode is already active
2. POST /api-public/v1/maintenancemode/start -- activate with routing keys and target names in body
3. POST /api-public/v1/stakeholders/sendMessage -- notify stakeholders that maintenance is underway
4. PUT /api-public/v1/maintenancemode/{maintenancemodeid}/end -- end maintenance when work is complete
5. GET /api-public/v1/incidents -- verify no incidents were suppressed that need follow-up


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
