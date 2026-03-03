---
name: twilio-video
description: "Twilio - Video API skill. Use when working with Twilio - Video for Compositions, CompositionHooks, CompositionSettings. Covers 39 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Video
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://video.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/Compositions -- verify access
3. POST /v1/Compositions -- create first Compositions

## Endpoints

39 endpoints across 6 groups. See references/api-spec.lap for full details.

### Compositions
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Compositions/{Sid} | Returns a single Composition resource identified by a Composition SID. |
| DELETE | /v1/Compositions/{Sid} | Delete a Recording Composition resource identified by a Composition SID. |
| GET | /v1/Compositions | List of all Recording compositions. |
| POST | /v1/Compositions |  |

### CompositionHooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/CompositionHooks/{Sid} | Returns a single CompositionHook resource identified by a CompositionHook SID. |
| DELETE | /v1/CompositionHooks/{Sid} | Delete a Recording CompositionHook resource identified by a `CompositionHook SID`. |
| POST | /v1/CompositionHooks/{Sid} |  |
| GET | /v1/CompositionHooks | List of all Recording CompositionHook resources. |
| POST | /v1/CompositionHooks |  |

### CompositionSettings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/CompositionSettings/Default |  |
| POST | /v1/CompositionSettings/Default |  |

### Recordings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Recordings/{Sid} | Returns a single Recording resource identified by a Recording SID. |
| DELETE | /v1/Recordings/{Sid} | Delete a Recording resource identified by a Recording SID. |
| GET | /v1/Recordings | List of all Track recordings. |

### RecordingSettings
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/RecordingSettings/Default |  |
| POST | /v1/RecordingSettings/Default |  |

### Rooms
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Rooms/{Sid} |  |
| POST | /v1/Rooms/{Sid} |  |
| POST | /v1/Rooms |  |
| GET | /v1/Rooms |  |
| GET | /v1/Rooms/{RoomSid}/Participants/{Sid} |  |
| POST | /v1/Rooms/{RoomSid}/Participants/{Sid} |  |
| GET | /v1/Rooms/{RoomSid}/Participants |  |
| POST | /v1/Rooms/{RoomSid}/Participants/{Sid}/Anonymize |  |
| GET | /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/PublishedTracks/{Sid} | Returns a single Track resource represented by TrackName or SID. |
| GET | /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/PublishedTracks | Returns a list of tracks associated with a given Participant. Only `currently` Published Tracks are in the list resource. |
| GET | /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/SubscribeRules | Returns a list of Subscribe Rules for the Participant. |
| POST | /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/SubscribeRules | Update the Subscribe Rules for the Participant |
| GET | /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/SubscribedTracks/{Sid} | Returns a single Track resource represented by `track_sid`.  Note: This is one resource with the Video API that requires a SID, be Track Name on the subscriber side is not guaranteed to be unique. |
| GET | /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/SubscribedTracks | Returns a list of tracks that are subscribed for the participant. |
| GET | /v1/Rooms/{RoomSid}/Recordings/{Sid} |  |
| DELETE | /v1/Rooms/{RoomSid}/Recordings/{Sid} |  |
| GET | /v1/Rooms/{RoomSid}/Recordings |  |
| GET | /v1/Rooms/{RoomSid}/RecordingRules | Returns a list of Recording Rules for the Room. |
| POST | /v1/Rooms/{RoomSid}/RecordingRules | Update the Recording Rules for the Room |
| GET | /v1/Rooms/{RoomSid}/Transcriptions/{Ttid} |  |
| POST | /v1/Rooms/{RoomSid}/Transcriptions/{Ttid} |  |
| GET | /v1/Rooms/{RoomSid}/Transcriptions |  |
| POST | /v1/Rooms/{RoomSid}/Transcriptions |  |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new video room?" -> POST /v1/Rooms
- "Show me details for a specific room" -> GET /v1/Rooms/{Sid}
- "List all active video rooms" -> GET /v1/Rooms (with Status=in-progress)
- "End a video room session" -> POST /v1/Rooms/{Sid} (set status to completed)
- "Who is currently in a room?" -> GET /v1/Rooms/{RoomSid}/Participants (with Status=connected)
- "Get all recordings for a specific room" -> GET /v1/Rooms/{RoomSid}/Recordings
- "Delete a recording" -> DELETE /v1/Recordings/{Sid}
- "Create a composition from a room's recordings" -> POST /v1/Compositions
- "What compositions are currently processing?" -> GET /v1/Compositions (with Status=enqueued)
- "Set up automatic composition after every room ends" -> POST /v1/CompositionHooks
- "Where are my recordings being stored externally?" -> GET /v1/RecordingSettings/Default
- "Anonymize a participant's data for GDPR compliance" -> POST /v1/Rooms/{RoomSid}/Participants/{Sid}/Anonymize
- "What tracks is a participant publishing?" -> GET /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/PublishedTracks
- "Start a live transcription in a room" -> POST /v1/Rooms/{RoomSid}/Transcriptions
- "Update subscribe rules for a participant" -> POST /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/SubscribeRules

## Response Tips

- **List endpoints** (Rooms, Recordings, Compositions, Participants, etc.): All return a `meta` object with `next_page_url` and `previous_page_url` for cursor-based pagination; follow `next_page_url` until it is `null`. Default `PageSize` is 50 where specified.
- **Single-resource GETs**: Return the resource directly (not wrapped in an array). Nullable fields (`str?`, `int?`) may be absent or null -- always check before accessing.
- **DELETE endpoints**: Return 204 with no body. A non-204 response indicates failure (typically 404 if already deleted).
- **POST create/update**: Room updates return 202 (accepted, async processing), while creates return 201. Composition and transcription creates also return 202. Check the `status` field to track async progress.
- **Settings endpoints** (CompositionSettings, RecordingSettings): Return a singleton object at `/Default` -- there is only one per account.
- **Error responses**: Twilio returns `{ code, message, status }` on errors. The `code` field is a Twilio-specific error code (not HTTP status) useful for debugging.

## Anomaly Flags

- **Composition stuck in processing**: If a composition's `status` remains `enqueued` or `started` well beyond the room's `duration`, surface this -- it may indicate a processing failure.
- **Room at max participants**: When `max_participants` is reached, new joins will fail. Proactively warn when participant count nears the limit.
- **Large room mode**: The `large_room` flag changes billing and behavior. Flag if a room is created with `large_room: true` to ensure the user is aware of the cost implications.
- **External storage not configured**: If `aws_storage_enabled` is `false` in RecordingSettings/CompositionSettings but the user expects external storage, surface the misconfiguration.
- **Encryption disabled**: If `encryption_enabled` is `false` in settings, flag this for security-conscious workflows.
- **Recording with zero duration**: A recording where `duration` is 0 or null likely indicates a failed or interrupted capture.
- **Participant with no published tracks**: A connected participant with an empty PublishedTracks list may indicate a client-side media issue.
- **Composition hook disabled**: If `enabled` is `false` on a CompositionHook, the hook will not fire -- surface this if the user expects automatic compositions.
- **Deprecated `enable_turn` field**: The `enable_turn` field on rooms is a legacy setting. Flag if it appears in user-supplied payloads.

## Playbook

### 1. Record a Video Call and Download the Composition

1. Create a room with recording enabled: `POST /v1/Rooms` with `record_participants_on_connect: true`
2. Wait for the room session to complete (participants join and leave, or end the room via `POST /v1/Rooms/{Sid}` with status `completed`)
3. List recordings for the room: `GET /v1/Rooms/{RoomSid}/Recordings`
4. Create a composition from those recordings: `POST /v1/Compositions` with the `room_sid` and desired `audio_sources`, `video_layout`, `resolution`, and `format`
5. Poll the composition status: `GET /v1/Compositions/{Sid}` until `status` is `completed`
6. Download the composed media from the URL in the `links` field or `media_external_location`

### 2. Set Up Automatic Compositions for All Rooms

1. Check current composition settings: `GET /v1/CompositionSettings/Default`
2. Configure external storage if needed: `POST /v1/CompositionSettings/Default` with AWS S3 credentials
3. Create a composition hook: `POST /v1/CompositionHooks` with `enabled: true`, desired `video_layout`, `resolution`, `format`, and `status_callback` URL
4. Verify the hook is active: `GET /v1/CompositionHooks/{Sid}` and confirm `enabled: true`
5. All future completed rooms will automatically trigger a composition

### 3. GDPR-Compliant Participant Data Removal

1. Identify the room: `GET /v1/Rooms` filtered by date range or unique name
2. List participants in the room: `GET /v1/Rooms/{RoomSid}/Participants`
3. Find the target participant by `identity` field
4. Anonymize the participant: `POST /v1/Rooms/{RoomSid}/Participants/{Sid}/Anonymize`
5. Delete any associated recordings: `GET /v1/Recordings` filtered by `SourceSid` matching the participant, then `DELETE /v1/Recordings/{Sid}` for each
6. Delete any compositions containing the participant: `GET /v1/Compositions` filtered by `RoomSid`, then `DELETE /v1/Compositions/{Sid}`

### 4. Monitor and Manage Live Room Participants

1. List active rooms: `GET /v1/Rooms` with `Status=in-progress`
2. For each room, list connected participants: `GET /v1/Rooms/{RoomSid}/Participants` with `Status=connected`
3. Check what each participant is publishing: `GET /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/PublishedTracks`
4. Adjust what a participant receives by updating subscribe rules: `POST /v1/Rooms/{RoomSid}/Participants/{ParticipantSid}/SubscribeRules`
5. To remove a participant, disconnect them: `POST /v1/Rooms/{RoomSid}/Participants/{Sid}` with status `disconnected`

### 5. Enable Live Transcription for a Room

1. Create a room (or use an existing active room): `POST /v1/Rooms` or `GET /v1/Rooms/{Sid}`
2. Start a transcription session: `POST /v1/Rooms/{RoomSid}/Transcriptions` with desired configuration
3. Monitor transcription status: `GET /v1/Rooms/{RoomSid}/Transcriptions/{Ttid}` -- check `status` field
4. List all transcriptions for the room: `GET /v1/Rooms/{RoomSid}/Transcriptions`
5. Stop a transcription when done: `POST /v1/Rooms/{RoomSid}/Transcriptions/{Ttid}` with status `stopped`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
