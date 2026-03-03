---
name: twilio-conversations
description: "Twilio - Conversations API skill. Use when working with Twilio - Conversations for Configuration, Conversations, ConversationWithParticipants. Covers 103 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio - Conversations
API version: 1.0.0

## Auth
Bearer basic

## Base URL
https://conversations.twilio.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/Configuration -- verify access
3. POST /v1/Configuration -- create first Configuration

## Endpoints

103 endpoints across 8 groups. See references/api-spec.lap for full details.

### Configuration
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/Configuration | Fetch the global configuration of conversations on your account |
| POST | /v1/Configuration | Update the global configuration of conversations on your account |
| GET | /v1/Configuration/Addresses | Retrieve a list of address configurations for an account |
| POST | /v1/Configuration/Addresses | Create a new address configuration |
| GET | /v1/Configuration/Addresses/{Sid} | Fetch an address configuration |
| POST | /v1/Configuration/Addresses/{Sid} | Update an existing address configuration |
| DELETE | /v1/Configuration/Addresses/{Sid} | Remove an existing address configuration |
| GET | /v1/Configuration/Webhooks |  |
| POST | /v1/Configuration/Webhooks |  |

### Conversations
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/Conversations | Create a new conversation in your account's default service |
| GET | /v1/Conversations | Retrieve a list of conversations in your account's default service |
| POST | /v1/Conversations/{Sid} | Update an existing conversation in your account's default service |
| DELETE | /v1/Conversations/{Sid} | Remove a conversation from your account's default service |
| GET | /v1/Conversations/{Sid} | Fetch a conversation from your account's default service |
| POST | /v1/Conversations/{ConversationSid}/Messages | Add a new message to the conversation |
| GET | /v1/Conversations/{ConversationSid}/Messages | Retrieve a list of all messages in the conversation |
| POST | /v1/Conversations/{ConversationSid}/Messages/{Sid} | Update an existing message in the conversation |
| DELETE | /v1/Conversations/{ConversationSid}/Messages/{Sid} | Remove a message from the conversation |
| GET | /v1/Conversations/{ConversationSid}/Messages/{Sid} | Fetch a message from the conversation |
| GET | /v1/Conversations/{ConversationSid}/Messages/{MessageSid}/Receipts/{Sid} | Fetch the delivery and read receipts of the conversation message |
| GET | /v1/Conversations/{ConversationSid}/Messages/{MessageSid}/Receipts | Retrieve a list of all delivery and read receipts of the conversation message |
| POST | /v1/Conversations/{ConversationSid}/Participants | Add a new participant to the conversation |
| GET | /v1/Conversations/{ConversationSid}/Participants | Retrieve a list of all participants of the conversation |
| POST | /v1/Conversations/{ConversationSid}/Participants/{Sid} | Update an existing participant in the conversation |
| DELETE | /v1/Conversations/{ConversationSid}/Participants/{Sid} | Remove a participant from the conversation |
| GET | /v1/Conversations/{ConversationSid}/Participants/{Sid} | Fetch a participant of the conversation |
| GET | /v1/Conversations/{ConversationSid}/Webhooks | Retrieve a list of all webhooks scoped to the conversation |
| POST | /v1/Conversations/{ConversationSid}/Webhooks | Create a new webhook scoped to the conversation |
| GET | /v1/Conversations/{ConversationSid}/Webhooks/{Sid} | Fetch the configuration of a conversation-scoped webhook |
| POST | /v1/Conversations/{ConversationSid}/Webhooks/{Sid} | Update an existing conversation-scoped webhook |
| DELETE | /v1/Conversations/{ConversationSid}/Webhooks/{Sid} | Remove an existing webhook scoped to the conversation |

### ConversationWithParticipants
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/ConversationWithParticipants | Create a new conversation with the list of participants in your account's default service |

### Credentials
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/Credentials | Add a new push notification credential to your account |
| GET | /v1/Credentials | Retrieve a list of all push notification credentials on your account |
| POST | /v1/Credentials/{Sid} | Update an existing push notification credential on your account |
| DELETE | /v1/Credentials/{Sid} | Remove a push notification credential from your account |
| GET | /v1/Credentials/{Sid} | Fetch a push notification credential from your account |

### ParticipantConversations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/ParticipantConversations | Retrieve a list of all Conversations that this Participant belongs to by identity or by address. Only one parameter should be specified. |

### Roles
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/Roles | Create a new user role in your account's default service |
| GET | /v1/Roles | Retrieve a list of all user roles in your account's default service |
| POST | /v1/Roles/{Sid} | Update an existing user role in your account's default service |
| DELETE | /v1/Roles/{Sid} | Remove a user role from your account's default service |
| GET | /v1/Roles/{Sid} | Fetch a user role from your account's default service |

### Services
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/Services | Create a new conversation service on your account |
| GET | /v1/Services | Retrieve a list of all conversation services on your account |
| DELETE | /v1/Services/{Sid} | Remove a conversation service with all its nested resources from your account |
| GET | /v1/Services/{Sid} | Fetch a conversation service from your account |
| DELETE | /v1/Services/{ChatServiceSid}/Bindings/{Sid} | Remove a push notification binding from the conversation service |
| GET | /v1/Services/{ChatServiceSid}/Bindings/{Sid} | Fetch a push notification binding from the conversation service |
| GET | /v1/Services/{ChatServiceSid}/Bindings | Retrieve a list of all push notification bindings in the conversation service |
| GET | /v1/Services/{ChatServiceSid}/Configuration | Fetch the configuration of a conversation service |
| POST | /v1/Services/{ChatServiceSid}/Configuration | Update configuration settings of a conversation service |
| POST | /v1/Services/{ChatServiceSid}/Conversations | Create a new conversation in your service |
| GET | /v1/Services/{ChatServiceSid}/Conversations | Retrieve a list of conversations in your service |
| POST | /v1/Services/{ChatServiceSid}/Conversations/{Sid} | Update an existing conversation in your service |
| DELETE | /v1/Services/{ChatServiceSid}/Conversations/{Sid} | Remove a conversation from your service |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{Sid} | Fetch a conversation from your service |
| POST | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Messages | Add a new message to the conversation in a specific service |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Messages | Retrieve a list of all messages in the conversation |
| POST | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Messages/{Sid} | Update an existing message in the conversation |
| DELETE | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Messages/{Sid} | Remove a message from the conversation |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Messages/{Sid} | Fetch a message from the conversation |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Messages/{MessageSid}/Receipts/{Sid} | Fetch the delivery and read receipts of the conversation message |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Messages/{MessageSid}/Receipts | Retrieve a list of all delivery and read receipts of the conversation message |
| POST | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Participants | Add a new participant to the conversation in a specific service |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Participants | Retrieve a list of all participants of the conversation |
| POST | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Participants/{Sid} | Update an existing participant in the conversation |
| DELETE | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Participants/{Sid} | Remove a participant from the conversation |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Participants/{Sid} | Fetch a participant of the conversation |
| POST | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Webhooks | Create a new webhook scoped to the conversation in a specific service |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Webhooks | Retrieve a list of all webhooks scoped to the conversation |
| POST | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Webhooks/{Sid} | Update an existing conversation-scoped webhook |
| DELETE | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Webhooks/{Sid} | Remove an existing webhook scoped to the conversation |
| GET | /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Webhooks/{Sid} | Fetch the configuration of a conversation-scoped webhook |
| POST | /v1/Services/{ChatServiceSid}/ConversationWithParticipants | Create a new conversation with the list of participants in your account's default service |
| POST | /v1/Services/{ChatServiceSid}/Configuration/Notifications | Update push notification service settings |
| GET | /v1/Services/{ChatServiceSid}/Configuration/Notifications | Fetch push notification service settings |
| GET | /v1/Services/{ChatServiceSid}/ParticipantConversations | Retrieve a list of all Conversations that this Participant belongs to by identity or by address. Only one parameter should be specified. |
| POST | /v1/Services/{ChatServiceSid}/Roles | Create a new user role in your service |
| GET | /v1/Services/{ChatServiceSid}/Roles | Retrieve a list of all user roles in your service |
| POST | /v1/Services/{ChatServiceSid}/Roles/{Sid} | Update an existing user role in your service |
| DELETE | /v1/Services/{ChatServiceSid}/Roles/{Sid} | Remove a user role from your service |
| GET | /v1/Services/{ChatServiceSid}/Roles/{Sid} | Fetch a user role from your service |
| POST | /v1/Services/{ChatServiceSid}/Users | Add a new conversation user to your service |
| GET | /v1/Services/{ChatServiceSid}/Users | Retrieve a list of all conversation users in your service |
| POST | /v1/Services/{ChatServiceSid}/Users/{Sid} | Update an existing conversation user in your service |
| DELETE | /v1/Services/{ChatServiceSid}/Users/{Sid} | Remove a conversation user from your service |
| GET | /v1/Services/{ChatServiceSid}/Users/{Sid} | Fetch a conversation user from your service |
| POST | /v1/Services/{ChatServiceSid}/Users/{UserSid}/Conversations/{ConversationSid} | Update a specific User Conversation. |
| DELETE | /v1/Services/{ChatServiceSid}/Users/{UserSid}/Conversations/{ConversationSid} | Delete a specific User Conversation. |
| GET | /v1/Services/{ChatServiceSid}/Users/{UserSid}/Conversations/{ConversationSid} | Fetch a specific User Conversation. |
| GET | /v1/Services/{ChatServiceSid}/Users/{UserSid}/Conversations | Retrieve a list of all User Conversations for the User. |
| POST | /v1/Services/{ChatServiceSid}/Configuration/Webhooks | Update a specific Webhook. |
| GET | /v1/Services/{ChatServiceSid}/Configuration/Webhooks | Fetch a specific service webhook configuration. |

### Users
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/Users | Add a new conversation user to your account's default service |
| GET | /v1/Users | Retrieve a list of all conversation users in your account's default service |
| POST | /v1/Users/{Sid} | Update an existing conversation user in your account's default service |
| DELETE | /v1/Users/{Sid} | Remove a conversation user from your account's default service |
| GET | /v1/Users/{Sid} | Fetch a conversation user from your account's default service |
| POST | /v1/Users/{UserSid}/Conversations/{ConversationSid} | Update a specific User Conversation. |
| DELETE | /v1/Users/{UserSid}/Conversations/{ConversationSid} | Delete a specific User Conversation. |
| GET | /v1/Users/{UserSid}/Conversations/{ConversationSid} | Fetch a specific User Conversation. |
| GET | /v1/Users/{UserSid}/Conversations | Retrieve a list of all User Conversations for the User. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new conversation?" -> POST /v1/Conversations
- "How do I send a message in a conversation?" -> POST /v1/Conversations/{ConversationSid}/Messages
- "How do I add someone to a conversation?" -> POST /v1/Conversations/{ConversationSid}/Participants
- "What conversations does a user belong to?" -> GET /v1/Users/{UserSid}/Conversations
- "How do I check if a message was delivered?" -> GET /v1/Conversations/{ConversationSid}/Messages/{MessageSid}/Receipts
- "How do I list all conversations filtered by state?" -> GET /v1/Conversations (use State param: active, inactive, closed)
- "How do I set up webhooks for conversation events?" -> POST /v1/Configuration/Webhooks
- "How do I create a conversation with participants in one call?" -> POST /v1/ConversationWithParticipants
- "How do I configure push notification credentials?" -> POST /v1/Credentials
- "How do I check a user's unread message count?" -> GET /v1/Users/{UserSid}/Conversations/{ConversationSid}
- "How do I close or archive a conversation?" -> POST /v1/Conversations/{Sid} (set state to closed/inactive)
- "How do I set up per-conversation webhooks vs global webhooks?" -> POST /v1/Conversations/{ConversationSid}/Webhooks (scoped) vs POST /v1/Configuration/Webhooks (global)
- "How do I find all conversations for a phone number?" -> GET /v1/ParticipantConversations (use Address param)
- "How do I manage conversations under a specific service instance?" -> Use /v1/Services/{ChatServiceSid}/Conversations/* endpoints
- "How do I configure notification templates for a service?" -> POST /v1/Services/{ChatServiceSid}/Configuration/Notifications

## Response Tips

- **List endpoints** (Conversations, Messages, Participants, Users, Roles, Credentials): Response array is keyed by resource name (e.g., `conversations`, `messages`); pagination lives in `meta` with `next_page_url`/`previous_page_url` -- follow these URLs directly rather than computing page numbers.
- **Single resource endpoints**: Return flat objects with `sid` as the primary identifier; `attributes` is a JSON-encoded string (parse it client-side); `links` is a map of related sub-resource URLs.
- **DELETE endpoints**: Return 204 with no body -- treat any non-204 as failure.
- **ConversationWithParticipants**: Can return either 201 (sync) or 202 (async) -- a 202 means participants are still being added in the background.
- **Delivery receipts**: The `status` field indicates delivery state and `error_code` is non-zero on failure -- always check both.
- **User resources**: `is_online` and `is_notifiable` are only meaningful when reachability is enabled on the service configuration.

## Anomaly Flags

- **202 on ConversationWithParticipants**: Participant addition is still processing -- poll the participants list to confirm all were added successfully.
- **Delivery receipt error_code != 0**: A message failed to reach a participant -- surface the error code, participant SID, and channel message SID for debugging.
- **Conversation state = "closed"**: Attempts to post messages or add participants to a closed conversation will fail -- warn before calling write endpoints.
- **is_online = false combined with is_notifiable = false**: The user is unreachable by all channels -- flag when sending time-sensitive messages.
- **next_page_url present in meta**: Results are truncated -- warn the user that additional pages exist, especially when listing messages or participants.
- **timers field on conversations**: Active inactivity or closed timers mean the conversation will auto-transition state -- surface timer values so the user is not surprised by automatic closure.
- **X-Twilio-Webhook-Enabled header on mutating calls**: If omitted, webhooks fire by default -- flag when the user may want to suppress webhook side-effects during bulk operations.
- **sandbox = "true" on credentials**: Push credentials are in sandbox mode and will not work in production -- surface this prominently.

## Playbook

### 1. Create a Group Conversation and Send the First Message

1. POST /v1/Conversations -- set `friendly_name` and optionally `unique_name` for idempotency. Note the returned `sid`.
2. POST /v1/Conversations/{Sid}/Participants -- add the first participant by `identity` (chat user) or `messaging_binding` (SMS/WhatsApp). Repeat for each participant.
3. POST /v1/Conversations/{Sid}/Messages -- set `author` and `body` to send the opening message. Note the returned message `index`.
4. Verify by GET /v1/Conversations/{Sid}/Participants to confirm all participants were added.

### 2. Set Up Webhook Monitoring for All Conversations

1. GET /v1/Configuration/Webhooks -- check current global webhook config.
2. POST /v1/Configuration/Webhooks -- set `pre_webhook_url` and/or `post_webhook_url` to your server endpoint. Set `method` to POST. Add `filters` array for specific events (e.g., `onMessageAdded`, `onConversationStateUpdated`).
3. Test by POST /v1/Conversations to create a test conversation -- verify your endpoint receives the webhook payload.
4. For per-conversation overrides, POST /v1/Conversations/{ConversationSid}/Webhooks with a scoped `configuration`.

### 3. Track Message Delivery Across Participants

1. POST /v1/Conversations/{ConversationSid}/Messages -- send the message. Note the returned `sid`.
2. GET /v1/Conversations/{ConversationSid}/Messages/{MessageSid}/Receipts -- list delivery receipts. Each receipt maps to one participant.
3. Check each receipt's `status` (sent, delivered, read, failed) and `error_code`. Non-zero error codes indicate delivery failure.
4. If paginated (check `meta.next_page_url`), follow pagination to get all receipts.
5. For failed receipts, cross-reference `participant_sid` via GET /v1/Conversations/{ConversationSid}/Participants/{Sid} to identify the failing channel.

### 4. Multi-tenant Setup Using Conversation Services

1. POST /v1/Services -- create an isolated service instance. Note the returned `sid` (this becomes `ChatServiceSid`).
2. POST /v1/Services/{ChatServiceSid}/Configuration -- set default role SIDs and enable `reachability_enabled` if needed.
3. POST /v1/Services/{ChatServiceSid}/Roles -- create custom roles with specific `permissions` arrays.
4. POST /v1/Services/{ChatServiceSid}/Users -- create users scoped to this service.
5. POST /v1/Services/{ChatServiceSid}/Conversations -- create conversations within the service boundary. All sub-resources (messages, participants, webhooks) use the service-scoped paths.

### 5. Bulk Import Users and Suppress Webhooks

1. POST /v1/Services/{ChatServiceSid}/Configuration/Webhooks -- note current config so you can restore it.
2. For each user: POST /v1/Services/{ChatServiceSid}/Users with header `X-Twilio-Webhook-Enabled: false` to suppress webhook firing during import.
3. For each conversation assignment: POST /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Participants with `X-Twilio-Webhook-Enabled: false`.
4. After import completes, verify counts via GET /v1/Services/{ChatServiceSid}/Users and GET /v1/Services/{ChatServiceSid}/Conversations/{ConversationSid}/Participants.
5. Resume normal operations -- subsequent calls without the header will trigger webhooks as configured.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
