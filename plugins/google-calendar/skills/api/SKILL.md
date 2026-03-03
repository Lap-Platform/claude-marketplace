---
name: calendar-api
description: "Calendar API skill. Use when working with Calendar for calendars, channels, colors. Covers 37 endpoints."
version: 1.0.0
generator: lapsh
---

# Calendar API
API version: v3

## Auth
OAuth2 | OAuth2

## Base URL
https://www.googleapis.com/calendar/v3

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /colors -- verify access
3. POST /calendars -- create first calendars

## Endpoints

37 endpoints across 5 groups. See references/api-spec.lap for full details.

### calendars
| Method | Path | Description |
|--------|------|-------------|
| POST | /calendars | Creates a secondary calendar. |
| DELETE | /calendars/{calendarId} | Deletes a secondary calendar. Use calendars.clear for clearing all events on primary calendars. |
| GET | /calendars/{calendarId} | Returns metadata for a calendar. |
| PATCH | /calendars/{calendarId} | Updates metadata for a calendar. This method supports patch semantics. |
| PUT | /calendars/{calendarId} | Updates metadata for a calendar. |
| GET | /calendars/{calendarId}/acl | Returns the rules in the access control list for the calendar. |
| POST | /calendars/{calendarId}/acl | Creates an access control rule. |
| POST | /calendars/{calendarId}/acl/watch | Watch for changes to ACL resources. |
| DELETE | /calendars/{calendarId}/acl/{ruleId} | Deletes an access control rule. |
| GET | /calendars/{calendarId}/acl/{ruleId} | Returns an access control rule. |
| PATCH | /calendars/{calendarId}/acl/{ruleId} | Updates an access control rule. This method supports patch semantics. |
| PUT | /calendars/{calendarId}/acl/{ruleId} | Updates an access control rule. |
| POST | /calendars/{calendarId}/clear | Clears a primary calendar. This operation deletes all events associated with the primary calendar of an account. |
| GET | /calendars/{calendarId}/events | Returns events on the specified calendar. |
| POST | /calendars/{calendarId}/events | Creates an event. |
| POST | /calendars/{calendarId}/events/import | Imports an event. This operation is used to add a private copy of an existing event to a calendar. |
| POST | /calendars/{calendarId}/events/quickAdd | Creates an event based on a simple text string. |
| POST | /calendars/{calendarId}/events/watch | Watch for changes to Events resources. |
| DELETE | /calendars/{calendarId}/events/{eventId} | Deletes an event. |
| GET | /calendars/{calendarId}/events/{eventId} | Returns an event based on its Google Calendar ID. To retrieve an event using its iCalendar ID, call the events.list method using the iCalUID parameter. |
| PATCH | /calendars/{calendarId}/events/{eventId} | Updates an event. This method supports patch semantics. |
| PUT | /calendars/{calendarId}/events/{eventId} | Updates an event. |
| GET | /calendars/{calendarId}/events/{eventId}/instances | Returns instances of the specified recurring event. |
| POST | /calendars/{calendarId}/events/{eventId}/move | Moves an event to another calendar, i.e. changes an event's organizer. |

### channels
| Method | Path | Description |
|--------|------|-------------|
| POST | /channels/stop | Stop watching resources through this channel |

### colors
| Method | Path | Description |
|--------|------|-------------|
| GET | /colors | Returns the color definitions for calendars and events. |

### freeBusy
| Method | Path | Description |
|--------|------|-------------|
| POST | /freeBusy | Returns free/busy information for a set of calendars. |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/me/calendarList | Returns the calendars on the user's calendar list. |
| POST | /users/me/calendarList | Inserts an existing calendar into the user's calendar list. |
| POST | /users/me/calendarList/watch | Watch for changes to CalendarList resources. |
| DELETE | /users/me/calendarList/{calendarId} | Removes a calendar from the user's calendar list. |
| GET | /users/me/calendarList/{calendarId} | Returns a calendar from the user's calendar list. |
| PATCH | /users/me/calendarList/{calendarId} | Updates an existing calendar on the user's calendar list. This method supports patch semantics. |
| PUT | /users/me/calendarList/{calendarId} | Updates an existing calendar on the user's calendar list. |
| GET | /users/me/settings | Returns all user settings for the authenticated user. |
| POST | /users/me/settings/watch | Watch for changes to Settings resources. |
| GET | /users/me/settings/{setting} | Returns a single user setting. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new calendar?" -> POST /calendars
- "What events do I have this week?" -> GET /calendars/{calendarId}/events (with timeMin/timeMax)
- "Add a meeting with someone tomorrow at 3pm" -> POST /calendars/{calendarId}/events/quickAdd
- "Delete an event from my calendar" -> DELETE /calendars/{calendarId}/events/{eventId}
- "Who has access to my calendar?" -> GET /calendars/{calendarId}/acl
- "Share my calendar with a coworker" -> POST /calendars/{calendarId}/acl
- "When is someone free for a meeting?" -> POST /freeBusy
- "What calendars am I subscribed to?" -> GET /users/me/calendarList
- "Move an event to a different calendar" -> POST /calendars/{calendarId}/events/{eventId}/move
- "Get all instances of a recurring event" -> GET /calendars/{calendarId}/events/{eventId}/instances
- "Change the color of a calendar in my list" -> PATCH /users/me/calendarList/{calendarId}
- "What color options are available?" -> GET /colors
- "Remove a calendar from my list" -> DELETE /users/me/calendarList/{calendarId}
- "Get notified when events change" -> POST /calendars/{calendarId}/events/watch
- "What are my calendar settings?" -> GET /users/me/settings

## Response Tips

- **Event lists** (`GET /events`, `/instances`): Paginated via `nextPageToken`; use `nextSyncToken` for incremental sync after the final page. Items are in the `items` array; `accessRole` indicates your permission level on that calendar.
- **ACL lists** (`GET /acl`): Paginated; each item has a `scope` object (type + value) and a `role` string. Supports `syncToken` for change tracking.
- **Calendar list** (`GET /calendarList`): Paginated; `primary: true` marks the user's main calendar. Colors come as `colorId` or direct `backgroundColor`/`foregroundColor` RGB values.
- **FreeBusy** (`POST /freeBusy`): Response nests busy intervals under `calendars.{id}.busy` array and errors under `calendars.{id}.errors`. Group expansion results appear in `groups`.
- **Watch channels** (all `/watch` endpoints): Return a channel object with `resourceId` and `expiration` -- store both for later stop via `POST /channels/stop`.
- **Mutations** (POST/PUT/PATCH events): Return the full event object on success. `conferenceData` is only populated when `conferenceDataVersion=1` is set on the request.
- **Delete endpoints**: Return empty 200 responses with no body.

## Anomaly Flags

- **Watch channel expiration approaching**: Surface when a channel's `expiration` timestamp is within 24 hours -- the agent should proactively renew it.
- **syncToken invalidation (410 Gone)**: When a sync request returns 410, the token is stale; the agent must discard it and perform a full sync.
- **Partial attendee lists**: If `attendeesOmitted: true` appears in an event response, the full attendee list was truncated -- re-fetch with a higher `maxAttendees` value.
- **conferenceData.createRequest status**: When `statusCode` is not `success` (e.g., `pending`), the Google Meet link is not yet ready -- surface this and suggest retrying.
- **Pagination loops**: If `nextPageToken` keeps returning on successive pages with no progress (same token), flag a possible API issue.
- **ACL role downgrades**: When an ACL PATCH/PUT response shows a `role` different from what was requested, surface the discrepancy -- the API may have clamped permissions.
- **Event `status: "cancelled"`**: Events with cancelled status appearing in lists (when `showDeleted: true`) should be flagged rather than silently displayed.
- **Rate limit errors (403/429)**: Surface immediately with the retry-after interval; Google Calendar enforces per-user and per-calendar quotas.

## Playbook

### 1. Schedule a Meeting with Attendees and Google Meet

1. `POST /calendars/{calendarId}/events` with `summary`, `start`, `end`, `attendees` array, and `conferenceData.createRequest` (set `conferenceDataVersion=1`)
2. Check the response's `conferenceData.createRequest.status.statusCode` -- if `pending`, wait and re-fetch with `GET /calendars/{calendarId}/events/{eventId}`
3. Extract `hangoutLink` or `conferenceData.entryPoints` for the meeting URL
4. Optionally set `sendUpdates: "all"` to notify attendees via email

### 2. Set Up Incremental Event Sync

1. `GET /calendars/{calendarId}/events` -- page through all results using `nextPageToken` until exhausted
2. Store the final `nextSyncToken` from the last page
3. On subsequent syncs, call `GET /calendars/{calendarId}/events?syncToken={token}` to get only changes
4. If the API returns 410 Gone, discard the sync token and repeat from step 1
5. For push notifications instead of polling, call `POST /calendars/{calendarId}/events/watch` and handle webhooks at your `address`

### 3. Find a Free Slot and Book It

1. `POST /freeBusy` with `items` listing all participant calendar IDs, plus `timeMin`/`timeMax` for the search window
2. Parse `calendars.{id}.busy` arrays to find overlapping free windows across all participants
3. `POST /calendars/{calendarId}/events` with the chosen slot's `start`/`end` and all participants in `attendees`
4. Set `sendUpdates: "all"` so participants receive invitations

### 4. Share a Calendar with Specific Permissions

1. `GET /calendars/{calendarId}/acl` to review current access rules
2. `POST /calendars/{calendarId}/acl` with `scope: {type: "user", value: "email@example.com"}` and `role` set to one of: `freeBusyReader`, `reader`, `writer`, `owner`
3. Set `sendNotifications: true` to email the user about the share
4. To modify later, use `PATCH /calendars/{calendarId}/acl/{ruleId}` with the updated `role`
5. To revoke, `DELETE /calendars/{calendarId}/acl/{ruleId}`

### 5. Move an Event Between Calendars

1. `GET /calendars/{sourceCalendarId}/events/{eventId}` to confirm the event exists and capture its current state
2. `POST /calendars/{sourceCalendarId}/events/{eventId}/move?destination={targetCalendarId}` to transfer it
3. The response contains the event with its new calendar context -- verify `organizer` and `htmlLink` updated correctly
4. Set `sendUpdates: "all"` if attendees should be notified of the calendar change


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
