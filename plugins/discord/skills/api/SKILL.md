---
name: discord-http-api-preview
description: "Discord HTTP API (Preview) API skill. Use when working with Discord HTTP API (Preview) for applications, channels, gateway. Covers 229 endpoints."
version: 1.0.0
generator: lapsh
---

# Discord HTTP API (Preview)
API version: 10

## Auth
ApiKey Authorization in header | OAuth2

## Base URL
https://discord.com/api/v10

## Setup
1. Set your API key in the appropriate header
2. GET /applications/@me -- verify access
3. POST /applications/{application_id}/attachment -- create first attachment

## Endpoints

229 endpoints across 16 groups. See references/api-spec.lap for full details.

### applications
| Method | Path | Description |
|--------|------|-------------|
| GET | /applications/@me |  |
| PATCH | /applications/@me |  |
| GET | /applications/{application_id} |  |
| PATCH | /applications/{application_id} |  |
| GET | /applications/{application_id}/activity-instances/{instance_id} |  |
| POST | /applications/{application_id}/attachment |  |
| GET | /applications/{application_id}/commands |  |
| PUT | /applications/{application_id}/commands |  |
| POST | /applications/{application_id}/commands |  |
| GET | /applications/{application_id}/commands/{command_id} |  |
| DELETE | /applications/{application_id}/commands/{command_id} |  |
| PATCH | /applications/{application_id}/commands/{command_id} |  |
| GET | /applications/{application_id}/emojis |  |
| POST | /applications/{application_id}/emojis |  |
| GET | /applications/{application_id}/emojis/{emoji_id} |  |
| DELETE | /applications/{application_id}/emojis/{emoji_id} |  |
| PATCH | /applications/{application_id}/emojis/{emoji_id} |  |
| GET | /applications/{application_id}/entitlements |  |
| POST | /applications/{application_id}/entitlements |  |
| GET | /applications/{application_id}/entitlements/{entitlement_id} |  |
| DELETE | /applications/{application_id}/entitlements/{entitlement_id} |  |
| POST | /applications/{application_id}/entitlements/{entitlement_id}/consume |  |
| GET | /applications/{application_id}/guilds/{guild_id}/commands |  |
| PUT | /applications/{application_id}/guilds/{guild_id}/commands |  |
| POST | /applications/{application_id}/guilds/{guild_id}/commands |  |
| GET | /applications/{application_id}/guilds/{guild_id}/commands/permissions |  |
| GET | /applications/{application_id}/guilds/{guild_id}/commands/{command_id} |  |
| DELETE | /applications/{application_id}/guilds/{guild_id}/commands/{command_id} |  |
| PATCH | /applications/{application_id}/guilds/{guild_id}/commands/{command_id} |  |
| GET | /applications/{application_id}/guilds/{guild_id}/commands/{command_id}/permissions |  |
| PUT | /applications/{application_id}/guilds/{guild_id}/commands/{command_id}/permissions |  |
| GET | /applications/{application_id}/role-connections/metadata |  |
| PUT | /applications/{application_id}/role-connections/metadata |  |

### channels
| Method | Path | Description |
|--------|------|-------------|
| GET | /channels/{channel_id} |  |
| DELETE | /channels/{channel_id} |  |
| PATCH | /channels/{channel_id} |  |
| POST | /channels/{channel_id}/followers |  |
| GET | /channels/{channel_id}/invites |  |
| POST | /channels/{channel_id}/invites |  |
| GET | /channels/{channel_id}/messages |  |
| POST | /channels/{channel_id}/messages |  |
| POST | /channels/{channel_id}/messages/bulk-delete |  |
| GET | /channels/{channel_id}/messages/pins |  |
| PUT | /channels/{channel_id}/messages/pins/{message_id} |  |
| DELETE | /channels/{channel_id}/messages/pins/{message_id} |  |
| GET | /channels/{channel_id}/messages/{message_id} |  |
| DELETE | /channels/{channel_id}/messages/{message_id} |  |
| PATCH | /channels/{channel_id}/messages/{message_id} |  |
| POST | /channels/{channel_id}/messages/{message_id}/crosspost |  |
| DELETE | /channels/{channel_id}/messages/{message_id}/reactions |  |
| GET | /channels/{channel_id}/messages/{message_id}/reactions/{emoji_name} |  |
| DELETE | /channels/{channel_id}/messages/{message_id}/reactions/{emoji_name} |  |
| PUT | /channels/{channel_id}/messages/{message_id}/reactions/{emoji_name}/@me |  |
| DELETE | /channels/{channel_id}/messages/{message_id}/reactions/{emoji_name}/@me |  |
| DELETE | /channels/{channel_id}/messages/{message_id}/reactions/{emoji_name}/{user_id} |  |
| POST | /channels/{channel_id}/messages/{message_id}/threads |  |
| PUT | /channels/{channel_id}/permissions/{overwrite_id} |  |
| DELETE | /channels/{channel_id}/permissions/{overwrite_id} |  |
| GET | /channels/{channel_id}/pins |  |
| PUT | /channels/{channel_id}/pins/{message_id} |  |
| DELETE | /channels/{channel_id}/pins/{message_id} |  |
| GET | /channels/{channel_id}/polls/{message_id}/answers/{answer_id} |  |
| POST | /channels/{channel_id}/polls/{message_id}/expire |  |
| PUT | /channels/{channel_id}/recipients/{user_id} |  |
| DELETE | /channels/{channel_id}/recipients/{user_id} |  |
| POST | /channels/{channel_id}/send-soundboard-sound |  |
| GET | /channels/{channel_id}/thread-members |  |
| PUT | /channels/{channel_id}/thread-members/@me |  |
| DELETE | /channels/{channel_id}/thread-members/@me |  |
| GET | /channels/{channel_id}/thread-members/{user_id} |  |
| PUT | /channels/{channel_id}/thread-members/{user_id} |  |
| DELETE | /channels/{channel_id}/thread-members/{user_id} |  |
| POST | /channels/{channel_id}/threads |  |
| GET | /channels/{channel_id}/threads/archived/private |  |
| GET | /channels/{channel_id}/threads/archived/public |  |
| GET | /channels/{channel_id}/threads/search |  |
| POST | /channels/{channel_id}/typing |  |
| GET | /channels/{channel_id}/users/@me/threads/archived/private |  |
| GET | /channels/{channel_id}/webhooks |  |
| POST | /channels/{channel_id}/webhooks |  |

### gateway
| Method | Path | Description |
|--------|------|-------------|
| GET | /gateway |  |
| GET | /gateway/bot |  |

### guilds
| Method | Path | Description |
|--------|------|-------------|
| GET | /guilds/templates/{code} |  |
| GET | /guilds/{guild_id} |  |
| PATCH | /guilds/{guild_id} |  |
| GET | /guilds/{guild_id}/audit-logs |  |
| GET | /guilds/{guild_id}/auto-moderation/rules |  |
| POST | /guilds/{guild_id}/auto-moderation/rules |  |
| GET | /guilds/{guild_id}/auto-moderation/rules/{rule_id} |  |
| DELETE | /guilds/{guild_id}/auto-moderation/rules/{rule_id} |  |
| PATCH | /guilds/{guild_id}/auto-moderation/rules/{rule_id} |  |
| GET | /guilds/{guild_id}/bans |  |
| GET | /guilds/{guild_id}/bans/{user_id} |  |
| PUT | /guilds/{guild_id}/bans/{user_id} |  |
| DELETE | /guilds/{guild_id}/bans/{user_id} |  |
| POST | /guilds/{guild_id}/bulk-ban |  |
| GET | /guilds/{guild_id}/channels |  |
| POST | /guilds/{guild_id}/channels |  |
| PATCH | /guilds/{guild_id}/channels |  |
| GET | /guilds/{guild_id}/emojis |  |
| POST | /guilds/{guild_id}/emojis |  |
| GET | /guilds/{guild_id}/emojis/{emoji_id} |  |
| DELETE | /guilds/{guild_id}/emojis/{emoji_id} |  |
| PATCH | /guilds/{guild_id}/emojis/{emoji_id} |  |
| GET | /guilds/{guild_id}/integrations |  |
| DELETE | /guilds/{guild_id}/integrations/{integration_id} |  |
| GET | /guilds/{guild_id}/invites |  |
| GET | /guilds/{guild_id}/members |  |
| PATCH | /guilds/{guild_id}/members/@me |  |
| GET | /guilds/{guild_id}/members/search |  |
| GET | /guilds/{guild_id}/members/{user_id} |  |
| PUT | /guilds/{guild_id}/members/{user_id} |  |
| DELETE | /guilds/{guild_id}/members/{user_id} |  |
| PATCH | /guilds/{guild_id}/members/{user_id} |  |
| PUT | /guilds/{guild_id}/members/{user_id}/roles/{role_id} |  |
| DELETE | /guilds/{guild_id}/members/{user_id}/roles/{role_id} |  |
| GET | /guilds/{guild_id}/new-member-welcome |  |
| GET | /guilds/{guild_id}/onboarding |  |
| PUT | /guilds/{guild_id}/onboarding |  |
| GET | /guilds/{guild_id}/preview |  |
| GET | /guilds/{guild_id}/prune |  |
| POST | /guilds/{guild_id}/prune |  |
| GET | /guilds/{guild_id}/regions |  |
| GET | /guilds/{guild_id}/roles |  |
| POST | /guilds/{guild_id}/roles |  |
| PATCH | /guilds/{guild_id}/roles |  |
| GET | /guilds/{guild_id}/roles/member-counts |  |
| GET | /guilds/{guild_id}/roles/{role_id} |  |
| DELETE | /guilds/{guild_id}/roles/{role_id} |  |
| PATCH | /guilds/{guild_id}/roles/{role_id} |  |
| GET | /guilds/{guild_id}/scheduled-events |  |
| POST | /guilds/{guild_id}/scheduled-events |  |
| GET | /guilds/{guild_id}/scheduled-events/{guild_scheduled_event_id} |  |
| DELETE | /guilds/{guild_id}/scheduled-events/{guild_scheduled_event_id} |  |
| PATCH | /guilds/{guild_id}/scheduled-events/{guild_scheduled_event_id} |  |
| GET | /guilds/{guild_id}/scheduled-events/{guild_scheduled_event_id}/users |  |
| GET | /guilds/{guild_id}/soundboard-sounds |  |
| POST | /guilds/{guild_id}/soundboard-sounds |  |
| GET | /guilds/{guild_id}/soundboard-sounds/{sound_id} |  |
| DELETE | /guilds/{guild_id}/soundboard-sounds/{sound_id} |  |
| PATCH | /guilds/{guild_id}/soundboard-sounds/{sound_id} |  |
| GET | /guilds/{guild_id}/stickers |  |
| POST | /guilds/{guild_id}/stickers |  |
| GET | /guilds/{guild_id}/stickers/{sticker_id} |  |
| DELETE | /guilds/{guild_id}/stickers/{sticker_id} |  |
| PATCH | /guilds/{guild_id}/stickers/{sticker_id} |  |
| GET | /guilds/{guild_id}/templates |  |
| POST | /guilds/{guild_id}/templates |  |
| PUT | /guilds/{guild_id}/templates/{code} |  |
| DELETE | /guilds/{guild_id}/templates/{code} |  |
| PATCH | /guilds/{guild_id}/templates/{code} |  |
| GET | /guilds/{guild_id}/threads/active |  |
| GET | /guilds/{guild_id}/vanity-url |  |
| GET | /guilds/{guild_id}/voice-states/@me |  |
| PATCH | /guilds/{guild_id}/voice-states/@me |  |
| GET | /guilds/{guild_id}/voice-states/{user_id} |  |
| PATCH | /guilds/{guild_id}/voice-states/{user_id} |  |
| GET | /guilds/{guild_id}/webhooks |  |
| GET | /guilds/{guild_id}/welcome-screen |  |
| PATCH | /guilds/{guild_id}/welcome-screen |  |
| GET | /guilds/{guild_id}/widget |  |
| PATCH | /guilds/{guild_id}/widget |  |
| GET | /guilds/{guild_id}/widget.json |  |
| GET | /guilds/{guild_id}/widget.png |  |

### interactions
| Method | Path | Description |
|--------|------|-------------|
| POST | /interactions/{interaction_id}/{interaction_token}/callback |  |

### invites
| Method | Path | Description |
|--------|------|-------------|
| GET | /invites/{code} |  |
| DELETE | /invites/{code} |  |
| GET | /invites/{code}/target-users | Get the target users for an invite. |
| PUT | /invites/{code}/target-users | Update the target users for an existing invite. |
| GET | /invites/{code}/target-users/job-status | Get the target users job status for an invite. |

### lobbies
| Method | Path | Description |
|--------|------|-------------|
| PUT | /lobbies |  |
| POST | /lobbies |  |
| GET | /lobbies/{lobby_id} |  |
| PATCH | /lobbies/{lobby_id} |  |
| PATCH | /lobbies/{lobby_id}/channel-linking |  |
| DELETE | /lobbies/{lobby_id}/members/@me |  |
| POST | /lobbies/{lobby_id}/members/@me/invites |  |
| POST | /lobbies/{lobby_id}/members/bulk |  |
| PUT | /lobbies/{lobby_id}/members/{user_id} |  |
| DELETE | /lobbies/{lobby_id}/members/{user_id} |  |
| POST | /lobbies/{lobby_id}/members/{user_id}/invites |  |
| GET | /lobbies/{lobby_id}/messages |  |
| POST | /lobbies/{lobby_id}/messages |  |
| PUT | /lobbies/{lobby_id}/messages/{message_id}/moderation-metadata | Update the external moderation metadata for a lobby message. |

### oauth2
| Method | Path | Description |
|--------|------|-------------|
| GET | /oauth2/@me |  |
| GET | /oauth2/applications/@me |  |
| GET | /oauth2/keys |  |
| GET | /oauth2/userinfo |  |

### partner-sdk
| Method | Path | Description |
|--------|------|-------------|
| PUT | /partner-sdk/dms/{user_id_1}/{user_id_2}/messages/{message_id}/moderation-metadata | Update the external moderation metadata for a user message (DM). |
| POST | /partner-sdk/provisional-accounts/unmerge |  |
| POST | /partner-sdk/provisional-accounts/unmerge/bot |  |
| POST | /partner-sdk/token |  |
| POST | /partner-sdk/token/bot |  |

### soundboard-default-sounds
| Method | Path | Description |
|--------|------|-------------|
| GET | /soundboard-default-sounds |  |

### stage-instances
| Method | Path | Description |
|--------|------|-------------|
| POST | /stage-instances |  |
| GET | /stage-instances/{channel_id} |  |
| DELETE | /stage-instances/{channel_id} |  |
| PATCH | /stage-instances/{channel_id} |  |

### sticker-packs
| Method | Path | Description |
|--------|------|-------------|
| GET | /sticker-packs |  |
| GET | /sticker-packs/{pack_id} |  |

### stickers
| Method | Path | Description |
|--------|------|-------------|
| GET | /stickers/{sticker_id} |  |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/@me |  |
| PATCH | /users/@me |  |
| GET | /users/@me/applications/{application_id}/entitlements |  |
| GET | /users/@me/applications/{application_id}/role-connection |  |
| PUT | /users/@me/applications/{application_id}/role-connection |  |
| DELETE | /users/@me/applications/{application_id}/role-connection |  |
| POST | /users/@me/channels |  |
| GET | /users/@me/connections |  |
| GET | /users/@me/guilds |  |
| DELETE | /users/@me/guilds/{guild_id} |  |
| GET | /users/@me/guilds/{guild_id}/member |  |
| GET | /users/{user_id} |  |

### voice
| Method | Path | Description |
|--------|------|-------------|
| GET | /voice/regions |  |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks/{webhook_id} |  |
| DELETE | /webhooks/{webhook_id} |  |
| PATCH | /webhooks/{webhook_id} |  |
| GET | /webhooks/{webhook_id}/{webhook_token} |  |
| POST | /webhooks/{webhook_id}/{webhook_token} |  |
| DELETE | /webhooks/{webhook_id}/{webhook_token} |  |
| PATCH | /webhooks/{webhook_id}/{webhook_token} |  |
| POST | /webhooks/{webhook_id}/{webhook_token}/github |  |
| GET | /webhooks/{webhook_id}/{webhook_token}/messages/@original |  |
| DELETE | /webhooks/{webhook_id}/{webhook_token}/messages/@original |  |
| PATCH | /webhooks/{webhook_id}/{webhook_token}/messages/@original |  |
| GET | /webhooks/{webhook_id}/{webhook_token}/messages/{message_id} |  |
| DELETE | /webhooks/{webhook_id}/{webhook_token}/messages/{message_id} |  |
| PATCH | /webhooks/{webhook_id}/{webhook_token}/messages/{message_id} |  |
| POST | /webhooks/{webhook_id}/{webhook_token}/slack |  |

## Enhanced Skill Content
## Question Mapping

- "How do I get my bot's application info?" -> GET /applications/@me
- "How do I send a message to a channel?" -> POST /channels/{channel_id}/messages
- "How do I register a slash command globally?" -> POST /applications/{application_id}/commands
- "How do I ban a user from a guild?" -> PUT /guilds/{guild_id}/bans/{user_id}
- "How do I get a list of guild members?" -> GET /guilds/{guild_id}/members
- "How do I create a webhook for a channel?" -> POST /channels/{channel_id}/webhooks
- "How do I delete multiple messages at once?" -> POST /channels/{channel_id}/messages/bulk-delete
- "How do I check my bot's gateway connection limits?" -> GET /gateway/bot
- "How do I create a role in a guild?" -> POST /guilds/{guild_id}/roles
- "How do I add a reaction to a message?" -> PUT /channels/{channel_id}/messages/{message_id}/reactions/{emoji_name}/@me
- "How do I create a thread from a message?" -> POST /channels/{channel_id}/messages/{message_id}/threads
- "How do I search for guild members by name?" -> GET /guilds/{guild_id}/members/search
- "How do I set up guild-specific slash commands?" -> POST /applications/{application_id}/guilds/{guild_id}/commands
- "How do I execute a webhook to post a message?" -> POST /webhooks/{webhook_id}/{webhook_token}
- "How do I start a stage instance for a voice channel?" -> POST /stage-instances

## Response Tips

- **Messages**: Deeply nested objects -- `author`, `embeds`, `components`, `thread`, `poll`, `message_reference` are all maps with their own subfields. Always check `edited_timestamp` (nullable) and `flags` for suppressed/ephemeral state.
- **Channels/Guilds**: List endpoints return bare arrays (no wrapper object), so there is no built-in pagination envelope. Use `before`/`after` snowflake params and `limit` (default 50, max 100) for cursor-based paging.
- **Members**: `GET /guilds/{guild_id}/members` paginates with `after` (int, not snowflake) and `limit`. The response is a flat array; `has_more` is inferred by whether you received `limit` results.
- **Commands**: `PUT` (bulk overwrite) replaces ALL commands -- it returns an array. `POST` creates one and may return 200 (updated) or 201 (created).
- **204 responses**: DELETE, PUT (pins/bans/roles/reactions), and consume endpoints return no body. Treat 204 as success with no parsing needed.
- **Webhooks**: `POST /webhooks/{id}/{token}` returns 204 by default; pass `?wait=true` to get the created message object back.
- **Threads**: Archived thread listings wrap results in `{threads, members, has_more, first_messages}` -- check `has_more` for pagination.
- **Snowflakes**: All IDs are string-encoded snowflakes (not integers). Parse with BigInt if doing arithmetic or timestamp extraction.

## Anomaly Flags

- **429 on every endpoint**: Discord rate limits are per-route and global. Surface `Retry-After` header and `X-RateLimit-Remaining` when remaining drops below 3. Every endpoint in this spec can return 429.
- **Gateway session limits**: `GET /gateway/bot` returns `session_start_limit.remaining` -- alert when below 10% of `total`. Resets tracked via `reset_after` (ms).
- **Bulk-ban partial failures**: `POST /guilds/{guild_id}/bulk-ban` returns `{banned_users, failed_users}` -- surface `failed_users` if non-empty, as this indicates permission or hierarchy issues.
- **Missing optional fields**: Many fields are nullable (`icon?`, `banner?`, `accent_color?`). Do not treat null as an error -- it means the resource has no value set.
- **Discriminator "0"**: The migration to unique usernames means `discriminator` is often `"0"`. Do not use discriminator for display; prefer `global_name` or `username`.
- **Command version snowflake**: Each command has a `version` snowflake that changes on update. If you cache commands, compare versions to detect stale data.
- **Entitlement `deleted` flag**: Entitlements can be soft-deleted (`deleted: true`). Filter these out unless explicitly auditing.
- **`is_dirty` on templates**: Guild templates have `is_dirty` (nullable bool) -- when true, the template is out of sync with the source guild. Surface this proactively.

## Playbook

### 1. Register and deploy a global slash command

1. GET /applications/@me to confirm your application ID
2. POST /applications/{application_id}/commands with `name`, `description`, and `options` array
3. Note: if 200 returned, the command was updated (already existed); 201 means newly created
4. GET /applications/{application_id}/commands to verify the command appears in the list
5. To restrict permissions per guild: PUT /applications/{application_id}/guilds/{guild_id}/commands/{command_id}/permissions

### 2. Send a rich embed message and pin it

1. POST /channels/{channel_id}/messages with `embeds` array containing title, description, color, and fields
2. Capture the returned message `id` from the 200 response
3. PUT /channels/{channel_id}/pins/{message_id} to pin it (returns 204, no body)
4. To verify: GET /channels/{channel_id}/messages/pins and confirm the message appears in `items`

### 3. Bulk-ban users and clean up messages

1. POST /guilds/{guild_id}/bulk-ban with `user_ids` array (up to 200) and `delete_message_seconds` (max 604800 = 7 days)
2. Check response: `banned_users` for successes, `failed_users` for failures (permission/hierarchy issues)
3. For individual follow-up: GET /guilds/{guild_id}/bans/{user_id} to confirm ban status
4. To unban later: DELETE /guilds/{guild_id}/bans/{user_id}

### 4. Set up a webhook and post via it

1. POST /channels/{channel_id}/webhooks with `name` (and optional `avatar`) to create a webhook
2. Save the returned `id`, `token`, and `url` from the response
3. POST /webhooks/{webhook_id}/{webhook_token}?wait=true with message content/embeds to post
4. To edit a sent message: PATCH /webhooks/{webhook_id}/{webhook_token}/messages/{message_id}
5. To forward GitHub events: POST /webhooks/{webhook_id}/{webhook_token}/github with the GitHub payload

### 5. Create and manage threads

1. To create from an existing message: POST /channels/{channel_id}/messages/{message_id}/threads with `name` and optional `auto_archive_duration`
2. To create standalone: POST /channels/{channel_id}/threads with thread configuration
3. To add a member: PUT /channels/{channel_id}/thread-members/{user_id}
4. To list members: GET /channels/{channel_id}/thread-members with `?with_member=true` for full guild member data
5. To browse archived threads: GET /channels/{channel_id}/threads/archived/public (paginate with `before` timestamp and `limit`, check `has_more`)
6. To search threads by name: GET /channels/{channel_id}/threads/search with `name` query param


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
