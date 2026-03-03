---
name: stream-api
description: "Stream API skill. Use when working with Stream for app, blocklists, campaigns. Covers 167 endpoints."
version: 1.0.0
generator: lapsh
---

# Stream API
API version: v223.6.0

## Auth
ApiKey Authorization in header | ApiKey api_key in query | ApiKey Stream-Auth-Type in header

## Base URL
https://chat.stream-io-api.com

## Setup
1. Set your API key in the appropriate header
2. GET /app -- verify access
3. POST /blocklists -- create first blocklists

## Endpoints

167 endpoints across 41 groups. See references/api-spec.lap for full details.

### app
| Method | Path | Description |
|--------|------|-------------|
| GET | /app | Get App Settings |
| PATCH | /app | Update App Settings |

### blocklists
| Method | Path | Description |
|--------|------|-------------|
| GET | /blocklists | List block lists |
| POST | /blocklists | Create block list |
| DELETE | /blocklists/{name} | Delete block list |
| GET | /blocklists/{name} | Get block list |
| PUT | /blocklists/{name} | Update block list |

### campaigns
| Method | Path | Description |
|--------|------|-------------|
| GET | /campaigns/{id} | Get campaign |
| POST | /campaigns/{id}/start | Start/schedule campaign |
| POST | /campaigns/{id}/stop | Stop campaign |
| POST | /campaigns/query | Query campaigns |

### channels
| Method | Path | Description |
|--------|------|-------------|
| POST | /channels | Query channels |
| DELETE | /channels/{type}/{id} | Delete channel |
| PATCH | /channels/{type}/{id} | Partially update channel |
| POST | /channels/{type}/{id} | Update channel |
| DELETE | /channels/{type}/{id}/draft | Delete draft |
| GET | /channels/{type}/{id}/draft | Get draft |
| POST | /channels/{type}/{id}/event | Send event |
| DELETE | /channels/{type}/{id}/file | Delete file |
| POST | /channels/{type}/{id}/file | Upload file |
| POST | /channels/{type}/{id}/hide | Hide channel |
| DELETE | /channels/{type}/{id}/image | Delete image |
| POST | /channels/{type}/{id}/image | Upload image |
| PATCH | /channels/{type}/{id}/member | Partially channel member update |
| POST | /channels/{type}/{id}/message | Send new message |
| GET | /channels/{type}/{id}/messages | Get many messages |
| POST | /channels/{type}/{id}/query | Get or create channel |
| POST | /channels/{type}/{id}/read | Mark read |
| POST | /channels/{type}/{id}/show | Show channel |
| POST | /channels/{type}/{id}/truncate | Truncate channel |
| POST | /channels/{type}/{id}/unread | Mark unread |
| POST | /channels/{type}/query | Get or create channel |
| PUT | /channels/batch | Update channels in batch |
| POST | /channels/delete | Deletes channels asynchronously |
| POST | /channels/delivered | Mark channel message delivery status |
| POST | /channels/read | Mark channels as read |

### channeltypes
| Method | Path | Description |
|--------|------|-------------|
| GET | /channeltypes | List channel types |
| POST | /channeltypes | Create channel type |
| DELETE | /channeltypes/{name} | Delete channel type |
| GET | /channeltypes/{name} | Get channel type |
| PUT | /channeltypes/{name} | Update channel type |

### check_push
| Method | Path | Description |
|--------|------|-------------|
| POST | /check_push | Check push |

### check_sns
| Method | Path | Description |
|--------|------|-------------|
| POST | /check_sns | Check SNS |

### check_sqs
| Method | Path | Description |
|--------|------|-------------|
| POST | /check_sqs | Check SQS |

### commands
| Method | Path | Description |
|--------|------|-------------|
| GET | /commands | List commands |
| POST | /commands | Create command |
| DELETE | /commands/{name} | Delete command |
| GET | /commands/{name} | Get command |
| PUT | /commands/{name} | Update command |

### devices
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /devices | Delete device |
| GET | /devices | List devices |
| POST | /devices | Create device |

### drafts
| Method | Path | Description |
|--------|------|-------------|
| POST | /drafts/query | Query draft messages |

### export
| Method | Path | Description |
|--------|------|-------------|
| POST | /export/users | Export users |

### export_channels
| Method | Path | Description |
|--------|------|-------------|
| POST | /export_channels | Export channels |

### external_storage
| Method | Path | Description |
|--------|------|-------------|
| GET | /external_storage | List external storage |
| POST | /external_storage | Create external storage |
| DELETE | /external_storage/{name} | Delete external storage |
| PUT | /external_storage/{name} | Update External Storage |
| GET | /external_storage/{name}/check | Check External Storage |

### guest
| Method | Path | Description |
|--------|------|-------------|
| POST | /guest | Create Guest |

### import_urls
| Method | Path | Description |
|--------|------|-------------|
| POST | /import_urls | Create import URL |

### imports
| Method | Path | Description |
|--------|------|-------------|
| GET | /imports | Get import |
| POST | /imports | Create import |
| GET | /imports/{id} | Get import |
| GET | /imports/v2 | List import v2 tasks |
| POST | /imports/v2 | Create import v2 task |
| DELETE | /imports/v2/{id} | Delete import v2 task |
| GET | /imports/v2/{id} | Get import v2 task |

### members
| Method | Path | Description |
|--------|------|-------------|
| GET | /members | Query members |

### messages
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /messages/{id} | Delete message |
| GET | /messages/{id} | Get message |
| POST | /messages/{id} | Update message |
| PUT | /messages/{id} | Partially message update |
| POST | /messages/{id}/action | Run message command action |
| POST | /messages/{id}/commit | Commit message |
| PATCH | /messages/{id}/ephemeral | Ephemeral message update |
| POST | /messages/{id}/reaction | Send reaction |
| DELETE | /messages/{id}/reaction/{type} | Delete reaction |
| GET | /messages/{id}/reactions | Get reactions |
| POST | /messages/{id}/reactions | Get reactions on a message |
| POST | /messages/{id}/translate | Translate message |
| POST | /messages/{id}/undelete | Undelete message |
| POST | /messages/{message_id}/polls/{poll_id}/vote | Cast vote |
| DELETE | /messages/{message_id}/polls/{poll_id}/vote/{vote_id} | Delete vote |
| DELETE | /messages/{message_id}/reminders | Delete reminder |
| PATCH | /messages/{message_id}/reminders | Updates Reminder |
| POST | /messages/{message_id}/reminders | Create reminder |
| GET | /messages/{parent_id}/replies | Get replies |
| POST | /messages/history | Query message history |

### moderation
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /moderation/ban | Unban user |
| POST | /moderation/ban | Ban user |
| POST | /moderation/flag | Flag |
| GET | /moderation/flags/message | Query Message Flags |
| POST | /moderation/mute | Mute user |
| POST | /moderation/mute/channel | Mute channel |
| POST | /moderation/unmute | Unmute user |
| POST | /moderation/unmute/channel | Unmute channel |

### og
| Method | Path | Description |
|--------|------|-------------|
| GET | /og | Get OG |

### permissions
| Method | Path | Description |
|--------|------|-------------|
| GET | /permissions | List permissions |
| GET | /permissions/{id} | Get permission |

### polls
| Method | Path | Description |
|--------|------|-------------|
| POST | /polls | Create poll |
| PUT | /polls | Update poll |
| DELETE | /polls/{poll_id} | Delete poll |
| GET | /polls/{poll_id} | Get poll |
| PATCH | /polls/{poll_id} | Partial update poll |
| POST | /polls/{poll_id}/options | Create poll option |
| PUT | /polls/{poll_id}/options | Update poll option |
| DELETE | /polls/{poll_id}/options/{option_id} | Delete poll option |
| GET | /polls/{poll_id}/options/{option_id} | Get poll option |
| POST | /polls/{poll_id}/votes | Query votes |
| POST | /polls/query | Query polls |

### push_preferences
| Method | Path | Description |
|--------|------|-------------|
| POST | /push_preferences | Push notification preferences |

### push_providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /push_providers | List push providers |
| POST | /push_providers | Upsert a push provider |
| DELETE | /push_providers/{type}/{name} | Delete a push provider |

### push_templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /push_templates | Get push notification templates |
| POST | /push_templates | Upsert a push notification template |

### query_banned_users
| Method | Path | Description |
|--------|------|-------------|
| GET | /query_banned_users | Query Banned Users |

### query_future_channel_bans
| Method | Path | Description |
|--------|------|-------------|
| GET | /query_future_channel_bans | Query Future Channel Bans |

### rate_limits
| Method | Path | Description |
|--------|------|-------------|
| GET | /rate_limits | Get rate limits |

### reminders
| Method | Path | Description |
|--------|------|-------------|
| POST | /reminders/query | Query reminders |

### roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /roles | List roles |
| POST | /roles | Create role |
| DELETE | /roles/{name} | Delete role |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search | Search messages |

### segments
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /segments/{id} | Delete segment |
| GET | /segments/{id} | Get segment |
| POST | /segments/{id}/deletetargets | Delete targets from a segment |
| GET | /segments/{id}/target/{target_id} | Check whether a target exists in a segment |
| POST | /segments/{id}/targets/query | Query segment targets |
| POST | /segments/query | Query segments |

### stats
| Method | Path | Description |
|--------|------|-------------|
| POST | /stats/team_usage | Query Team Usage Statistics |

### tasks
| Method | Path | Description |
|--------|------|-------------|
| GET | /tasks/{id} | Get status of a task |

### threads
| Method | Path | Description |
|--------|------|-------------|
| POST | /threads | Query Threads |
| GET | /threads/{message_id} | Get Thread |
| PATCH | /threads/{message_id} | Partially update thread |

### unread
| Method | Path | Description |
|--------|------|-------------|
| GET | /unread | Unread counts |

### unread_batch
| Method | Path | Description |
|--------|------|-------------|
| POST | /unread_batch | Batch unread counts |

### uploads
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /uploads/file | Delete file |
| POST | /uploads/file | Upload file |
| DELETE | /uploads/image | Delete image |
| POST | /uploads/image | Upload image |

### usergroups
| Method | Path | Description |
|--------|------|-------------|
| GET | /usergroups | List user groups |
| POST | /usergroups | Create user group |
| DELETE | /usergroups/{id} | Delete user group |
| GET | /usergroups/{id} | Get user group |
| PUT | /usergroups/{id} | Update user group |
| DELETE | /usergroups/{id}/members | Remove user group members |
| POST | /usergroups/{id}/members | Add user group members |
| GET | /usergroups/search | Search user groups |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | Query users |
| PATCH | /users | Partially update user |
| POST | /users | Upsert users |
| POST | /users/{user_id}/deactivate | Deactivate user |
| POST | /users/{user_id}/event | Send user event |
| GET | /users/{user_id}/export | Export user |
| POST | /users/{user_id}/reactivate | Reactivate user |
| GET | /users/block | Get list of blocked Users |
| POST | /users/block | Block user |
| POST | /users/deactivate | Deactivate users |
| POST | /users/delete | Delete Users |
| GET | /users/live_locations | Get user live locations |
| PUT | /users/live_locations | Update live location |
| POST | /users/reactivate | Reactivate users |
| POST | /users/restore | Restore users |
| POST | /users/unblock | Unblock user |

## Enhanced Skill Content
## Question Mapping

- "How do I get my app settings?" -> GET /app
- "How do I send a message to a channel?" -> POST /channels/{type}/{id}/message
- "How do I create or join a channel?" -> POST /channels/{type}/{id}
- "How do I search for messages?" -> GET /search
- "How do I list all channels matching a filter?" -> POST /channels
- "How do I ban a user from a channel?" -> POST /moderation/ban
- "How do I add a reaction to a message?" -> POST /messages/{id}/reaction
- "How do I create a poll in a channel?" -> POST /polls
- "How do I upload a file to a channel?" -> POST /channels/{type}/{id}/file
- "How do I mark a channel as read?" -> POST /channels/{type}/{id}/read
- "How do I get unread counts for a user?" -> GET /unread
- "How do I delete a message?" -> DELETE /messages/{id}
- "How do I query threads the user participates in?" -> POST /threads
- "How do I create a blocklist for content moderation?" -> POST /blocklists
- "How do I start a campaign to message a segment of users?" -> POST /campaigns/{id}/start

## Response Tips

- **Channels/Messages**: All responses include a `duration` field (server processing time as string). Messages are deeply nested with `quoted_message`, `poll`, `reminder`, and `shared_location` sub-objects -- traverse carefully. The `cid` field is `{type}:{id}` composite key.
- **Pagination**: Query endpoints (`POST /channels`, `POST /threads`, `POST /drafts/query`, `POST /campaigns/query`, `POST /polls/query`) use cursor-based pagination via `next`/`prev` tokens with a `limit` parameter, not page numbers. Pass the returned `next` value as `next` in the follow-up request.
- **Errors**: All endpoints return only `400` (bad request) or `429` (rate limited). There are no 404s -- missing resources come back as 400. Check the error body for details.
- **Batch/Async**: Operations like `POST /channels/delete`, `PUT /channels/batch`, `POST /users/delete`, and `POST /export/users` return a `task_id`. Poll `GET /tasks/{id}` to check completion status.
- **Moderation**: Flag and ban responses include full user objects for both the reporter and target. The `moderation` sub-object on messages contains `blocklist_matched`, `image_harms`, and `text_harms` arrays for content analysis.

## Anomaly Flags

- **429 on any endpoint**: Surface immediately -- all 167 endpoints share the same rate limit error. Check `GET /rate_limits` to see current limits by platform (server_side, android, ios, web) and adjust call frequency.
- **User `banned: true` or `shadow_banned: true`**: Flag when these appear in user objects returned from channel queries -- the user's messages may be silently hidden from others.
- **Channel `frozen: true` or `disabled: true`**: No new messages can be sent. Surface if a send attempt would target this channel.
- **Message `moderation.action` present**: Content was flagged by automod. Values like `blocklist_matched` or `platform_circumvented: true` warrant review.
- **`suspended: true` on app settings**: The entire app is suspended -- all operations will fail. Surface the `suspended_explanation` field.
- **`revoke_tokens_issued_before` set**: Tokens issued before this timestamp are invalid. Flag if authentication failures occur after a token revocation.
- **Task `status` not completing**: For async operations (exports, batch deletes), flag if `GET /tasks/{id}` shows an `error` object or stays pending for an extended period.
- **`deleted_at` present on channels or messages**: Indicates soft-deleted resources. When `show_deleted_message` is not set, these may be omitted or returned without content.

## Playbook

### 1. Set Up a New Chat Channel and Send the First Message

1. Create or query the channel: `POST /channels/{type}/{id}` with `data` containing channel config (name, members, team)
2. Optionally add more members: include `add_members` array with `user_id` entries in the same POST body
3. Send the first message: `POST /channels/{type}/{id}/message` with `message.text` set
4. Verify delivery by checking the returned `message.id` and `created_at` timestamp

### 2. Moderate a Reported User

1. Review flagged content: `GET /moderation/flags/message` to see outstanding message flags
2. Ban the user: `POST /moderation/ban` with `target_user_id`, optional `reason`, `timeout` (seconds), and `channel_cid` for channel-scoped bans
3. Optionally delete their messages: set `delete_messages: "soft"` (or `"hard"`) in the ban request
4. To shadow ban instead (user sees own messages, others don't): set `shadow: true`
5. To lift the ban later: `DELETE /moderation/ban` with `target_user_id` and `channel_cid`

### 3. Run a Poll in a Channel

1. Create the poll: `POST /polls` with `name`, `options` array (each with `text`), and optional settings like `enforce_unique_vote`, `max_votes_allowed`, or `voting_visibility: "anonymous"`
2. Attach to a message: `POST /channels/{type}/{id}/message` with `message.poll_id` set to the poll's `id`
3. Cast votes: `POST /messages/{message_id}/polls/{poll_id}/vote` with `vote.option_id`
4. Check results: `GET /polls/{poll_id}` -- inspect `vote_counts_by_option` and `vote_count`
5. Close the poll: `PATCH /polls/{poll_id}` with `set: { is_closed: true }`

### 4. Export User Data for GDPR Compliance

1. Initiate the export: `POST /export/users` with `user_ids` array
2. Note the returned `task_id`
3. Poll task status: `GET /tasks/{id}` until `status` indicates completion
4. On success, the `result` field contains download information
5. For a single user's full data (messages + reactions): `GET /users/{user_id}/export` returns everything synchronously

### 5. Send a Campaign Message to a User Segment

1. Create a segment (if not existing): query segments with `POST /segments/query` using a `filter`
2. Retrieve the campaign: `GET /campaigns/{id}` to review `message_template`, `segment_ids`, and `sender`
3. Start the campaign: `POST /campaigns/{id}/start` with optional `scheduled_for` (ISO 8601 datetime) for delayed delivery
4. Monitor progress: re-fetch with `GET /campaigns/{id}` and check `stats.progress`, `stats_messages_sent`, `stats_users_sent`
5. Stop early if needed: `POST /campaigns/{id}/stop`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
