---
name: twilio-chat
description: "Twilio - Chat API skill. Use when working with Twilio - Chat for Services, Credentials. Covers 54 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Chat
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://chat.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v2/Credentials -- verify access
3. POST /v2/Services/{ServiceSid}/Channels/{Sid} -- create first Channels

## Endpoints

54 endpoints across 2 groups. See references/api-spec.lap for full details.

### Services
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/Services/{ServiceSid}/Bindings |  |
| GET | /v2/Services/{ServiceSid}/Bindings/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Bindings/{Sid} |  |
| GET | /v2/Services/{ServiceSid}/Channels/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Channels/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Channels/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Channels |  |
| GET | /v2/Services/{ServiceSid}/Channels |  |
| GET | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks |  |
| POST | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks |  |
| GET | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks/{Sid} |  |
| GET | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Invites/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Invites/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Invites |  |
| GET | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Invites |  |
| GET | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Members/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Members/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Members/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Members |  |
| GET | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Members |  |
| GET | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages |  |
| GET | /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages |  |
| GET | /v2/Services/{ServiceSid}/Roles/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Roles/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Roles/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Roles |  |
| GET | /v2/Services/{ServiceSid}/Roles |  |
| GET | /v2/Services/{Sid} |  |
| DELETE | /v2/Services/{Sid} |  |
| POST | /v2/Services/{Sid} |  |
| POST | /v2/Services |  |
| GET | /v2/Services |  |
| GET | /v2/Services/{ServiceSid}/Users/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Users/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Users/{Sid} |  |
| POST | /v2/Services/{ServiceSid}/Users |  |
| GET | /v2/Services/{ServiceSid}/Users |  |
| GET | /v2/Services/{ServiceSid}/Users/{UserSid}/Bindings |  |
| GET | /v2/Services/{ServiceSid}/Users/{UserSid}/Bindings/{Sid} |  |
| DELETE | /v2/Services/{ServiceSid}/Users/{UserSid}/Bindings/{Sid} |  |
| GET | /v2/Services/{ServiceSid}/Users/{UserSid}/Channels | List all Channels for a given User. |
| GET | /v2/Services/{ServiceSid}/Users/{UserSid}/Channels/{ChannelSid} |  |
| DELETE | /v2/Services/{ServiceSid}/Users/{UserSid}/Channels/{ChannelSid} | Removes User from selected Channel. |
| POST | /v2/Services/{ServiceSid}/Users/{UserSid}/Channels/{ChannelSid} |  |

### Credentials
| Method | Path | Description |
|--------|------|-------------|
| GET | /v2/Credentials |  |
| POST | /v2/Credentials |  |
| GET | /v2/Credentials/{Sid} |  |
| POST | /v2/Credentials/{Sid} |  |
| DELETE | /v2/Credentials/{Sid} |  |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new chat service?" -> POST /v2/Services
- "List all my chat services" -> GET /v2/Services
- "How do I create a channel in a service?" -> POST /v2/Services/{ServiceSid}/Channels
- "Show me all members in a channel" -> GET /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Members
- "How do I send a message to a channel?" -> POST /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages
- "Get the message history for a channel" -> GET /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages
- "How do I invite someone to a channel?" -> POST /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Invites
- "What push notification bindings does a user have?" -> GET /v2/Services/{ServiceSid}/Users/{UserSid}/Bindings
- "Which channels has a user joined?" -> GET /v2/Services/{ServiceSid}/Users/{UserSid}/Channels
- "How do I check a user's unread message count in a channel?" -> GET /v2/Services/{ServiceSid}/Users/{UserSid}/Channels/{ChannelSid}
- "How do I set up a channel webhook?" -> POST /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks
- "How do I delete a credential?" -> DELETE /v2/Credentials/{Sid}
- "How do I assign a role to a user?" -> POST /v2/Services/{ServiceSid}/Users/{Sid}
- "List all roles defined in a service" -> GET /v2/Services/{ServiceSid}/Roles
- "How do I update a service's webhook configuration?" -> POST /v2/Services/{Sid}

## Response Tips

- **List endpoints** (Services, Channels, Members, Messages, etc.): All return a `meta` object with `next_page_url` and `previous_page_url` for cursor-based pagination; follow `next_page_url` until it is `null`. Use `PageSize` (max typically 1000) and `PageToken` for control.
- **Single-resource GETs**: Return the resource directly at the top level (no wrapper); all fields are nullable except `type`, counters (`members_count`, `messages_count`), and enum-like strings.
- **DELETE endpoints**: Return 204 with no body -- treat any non-204 as an error.
- **POST create vs. update**: Creates return 201, updates return 200; both return the full resource. Distinguish by status code, not response shape.
- **User channels**: The per-user channel view (`/Users/{UserSid}/Channels/{ChannelSid}`) returns `unread_messages_count` and `last_consumed_message_index` -- these are user-scoped, not the same as the channel-level counters.
- **Credentials**: Flat resources with `type` (gcm, apn, fcm) and optional `sandbox` flag; no nested objects.

## Anomaly Flags

- **Pagination truncation**: If `meta.next_page_url` is present, warn that results are incomplete and offer to fetch remaining pages.
- **Null identity on bindings or members**: A binding or member with `identity: null` may indicate an orphaned record -- surface for review.
- **`was_edited: true` on messages**: Flag edited messages when reviewing channel history so the user knows the content may have changed.
- **User offline status**: When `is_online: false` and `is_notifiable: false` on a user, flag that the user is unreachable for both real-time and push delivery.
- **Zero members/messages on a channel**: A channel with `members_count: 0` or `messages_count: 0` that is not newly created may indicate a stale or abandoned channel.
- **Missing webhook URLs on service**: If `pre_webhook_url` and `post_webhook_url` are both empty on a service, note that no event callbacks are configured.
- **High `unread_messages_count`**: On a user-channel record, a large unread count may signal a disengaged user or a noisy channel worth investigating.
- **`X-Twilio-Webhook-Enabled` header usage**: When this header is omitted on mutating calls that support it, webhooks fire by default -- flag if the caller might want to suppress them.

## Playbook

### 1. Set Up a New Chat Service with a Channel

1. POST /v2/Services with a `friendly_name` to create the service. Save the returned `sid` as `ServiceSid`.
2. POST /v2/Services/{ServiceSid}/Channels with `friendly_name`, `unique_name`, and `type` (public or private).
3. POST /v2/Services/{ServiceSid}/Roles with `friendly_name` and `permissions` to define custom roles (optional).
4. GET /v2/Services/{ServiceSid} to verify the service configuration, especially `default_service_role_sid` and `default_channel_role_sid`.

### 2. Add Users to a Channel and Send Messages

1. POST /v2/Services/{ServiceSid}/Users with `identity` to create the user. Save `sid` as `UserSid`.
2. POST /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Members with the user's `identity` to add them to the channel.
3. POST /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages with `body` and `from` (identity) to send a message.
4. GET /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages with `Order=desc` to confirm delivery and retrieve recent history.

### 3. Configure Push Notifications

1. POST /v2/Credentials with `type` (apn, gcm, or fcm) and the platform-specific certificate or API key. Save `sid` as `CredentialSid`.
2. GET /v2/Services/{ServiceSid}/Bindings to list existing push bindings and verify which users and endpoints are registered.
3. GET /v2/Services/{ServiceSid}/Users/{UserSid}/Bindings to inspect a specific user's push configuration.
4. DELETE /v2/Services/{ServiceSid}/Users/{UserSid}/Bindings/{Sid} to remove stale or duplicate bindings.

### 4. Monitor User Engagement Across Channels

1. GET /v2/Services/{ServiceSid}/Users/{UserSid}/Channels to list all channels the user belongs to.
2. For each channel, check `unread_messages_count` and `last_consumed_message_index` to gauge read status.
3. GET /v2/Services/{ServiceSid}/Users/{UserSid} to check `is_online` and `is_notifiable` for reachability.
4. If a user has high unread counts across channels, consider sending a re-engagement notification or reviewing channel noise levels.

### 5. Set Up Channel Webhooks for Event Processing

1. GET /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks to check for existing webhook configurations.
2. POST /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks with `type` (webhook, trigger, or studio) and `configuration` containing the target URL and filters.
3. POST /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Messages with `X-Twilio-Webhook-Enabled: true` to send a test message and trigger the webhook.
4. GET /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks/{Sid} to verify the webhook's `date_updated` changed, confirming it fired.
5. To disable, DELETE /v2/Services/{ServiceSid}/Channels/{ChannelSid}/Webhooks/{Sid}.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
