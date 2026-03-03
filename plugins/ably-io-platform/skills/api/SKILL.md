---
name: platform-api
description: "Platform API skill. Use when working with Platform for channels, push, keys. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# Platform API
API version: 1.1.1

## Auth
Bearer basic | Bearer bearer

## Base URL
https://rest.ably.io

## Setup
1. Set Authorization header with your Bearer token
2. GET /channels -- verify access
3. POST /channels/{channel_id}/messages -- create first messages

## Endpoints

22 endpoints across 5 groups. See references/api-spec.lap for full details.

### channels
| Method | Path | Description |
|--------|------|-------------|
| GET | /channels/{channel_id}/messages | Get message history for a channel |
| POST | /channels/{channel_id}/messages | Publish a message to a channel |
| GET | /channels/{channel_id}/presence | Get presence of a channel |
| GET | /channels/{channel_id}/presence/history | Get presence history of a channel |
| GET | /channels/{channel_id} | Get metadata of a channel |
| GET | /channels | Enumerate all active channels of the application |

### push
| Method | Path | Description |
|--------|------|-------------|
| GET | /push/deviceRegistrations | List devices registered for receiving push notifications |
| POST | /push/deviceRegistrations | Register a device for receiving push notifications |
| DELETE | /push/deviceRegistrations | Unregister matching devices for push notifications |
| GET | /push/deviceRegistrations/{device_id} | Get a device registration |
| PUT | /push/deviceRegistrations/{device_id} | Update a device registration |
| PATCH | /push/deviceRegistrations/{device_id} | Update a device registration |
| DELETE | /push/deviceRegistrations/{device_id} | Unregister a single device for push notifications |
| GET | /push/deviceRegistrations/{device_id}/resetUpdateToken | Reset a registered device's update token |
| GET | /push/channelSubscriptions | List channel subscriptions |
| POST | /push/channelSubscriptions | Subscribe a device to a channel |
| DELETE | /push/channelSubscriptions | Delete a registered device's update token |
| GET | /push/channels | List all channels with at least one subscribed device |
| POST | /push/publish | Publish a push notification to device(s) |

### keys
| Method | Path | Description |
|--------|------|-------------|
| POST | /keys/{keyName}/requestToken | Request an access token |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats | Retrieve usage statistics for an application |

### time
| Method | Path | Description |
|--------|------|-------------|
| GET | /time | Get the service time |

## Enhanced Skill Content
## Question Mapping

- "How do I publish a message to a channel?" -> POST /channels/{channel_id}/messages
- "What messages were sent on a channel recently?" -> GET /channels/{channel_id}/messages
- "Who is currently present on a channel?" -> GET /channels/{channel_id}/presence
- "Show me the presence history for a channel" -> GET /channels/{channel_id}/presence/history
- "How many subscribers does a channel have?" -> GET /channels/{channel_id}
- "List all active channels" -> GET /channels
- "List channels that start with a specific prefix" -> GET /channels
- "How do I register a device for push notifications?" -> POST /push/deviceRegistrations
- "Send a push notification to a specific device" -> POST /push/publish
- "What devices are registered for push for a given client?" -> GET /push/deviceRegistrations
- "How do I subscribe a device to push on a channel?" -> POST /push/channelSubscriptions
- "Remove a device's push registration" -> DELETE /push/deviceRegistrations/{device_id}
- "Generate a temporary auth token for a key?" -> POST /keys/{keyName}/requestToken
- "What is the current server time?" -> GET /time
- "Show me usage stats for the past hour" -> GET /stats

## Response Tips

- **Channels (list/messages/presence):** Responses are arrays; use `limit` (max 100) and `direction` for pagination. Pass the timestamp of the last item as `start` or `end` to page through results.
- **Channel metadata (GET /channels/{id}):** Returns a nested `status.occupancy` object with separate counts for publishers, subscribers, presenceMembers, presenceConnections, and presenceSubscribers -- do not conflate these.
- **Push device registrations:** Responses nest recipient config under `push.recipient` (dot-notation key, not a nested object path). The `push.state` field is one of Active/Failing/Failed -- check this to determine delivery health.
- **Push publish:** Returns 2XX with no body on success. Any non-2XX means the notification was not delivered.
- **Token requests:** The response includes `issued` and `expires` as Unix timestamps (int64). Compute `expires - issued` to know the token TTL.
- **Stats:** Returns an array of stat objects bucketed by `unit` (minute/hour/day/month). Empty buckets may be omitted rather than returned as zeros.
- **Time:** Returns a single-element array containing the server time as a Unix timestamp in milliseconds.

## Anomaly Flags

- **push.state = "Failing" or "Failed"**: Surface immediately when reading device registrations -- the device is not receiving push notifications and may need re-registration.
- **Token expiry approaching**: When a requested token's `expires` timestamp is within 5 minutes of current time, warn that re-authentication will be needed soon.
- **Empty channel list with prefix filter**: If GET /channels with a `prefix` returns zero results, flag that the prefix may be misspelled or no matching channels are active.
- **Presence count mismatch**: If `presenceMembers` differs significantly from `presenceConnections` on a channel, flag it -- this may indicate stale presence entries or connection issues.
- **Limit capping**: When a response returns exactly `limit` items (default 100), warn that results are likely truncated and pagination is needed for complete data.
- **Device registration without deviceSecret**: If a POST/PUT to device registrations omits `deviceSecret`, flag that the device may not be able to authenticate future updates.

## Playbook

### 1. Send a Push Notification to All Devices for a Client

1. GET /push/deviceRegistrations with `clientId` to list all registered devices for the client.
2. Verify each device has `push.state` = "Active". Flag any in Failing/Failed state.
3. POST /push/publish with `recipient.clientId` set to the target client ID, along with the `push.notification` payload (title, body, sound).
4. Confirm 2XX response. If non-2XX, check error body for details.

### 2. Monitor Channel Activity and Presence

1. GET /channels with optional `prefix` to discover active channels.
2. For each channel of interest, GET /channels/{channel_id} to check `status.isActive` and `status.occupancy` counts.
3. GET /channels/{channel_id}/presence to see who is currently connected.
4. GET /channels/{channel_id}/presence/history with `start`/`end` to review presence changes over a time window.

### 3. Register a Mobile Device for Push and Subscribe to a Channel

1. POST /push/deviceRegistrations with `platform` (ios/android), `formFactor`, and `push.recipient` containing the device token or registration token.
2. Capture the returned `id` (device ID) and `deviceSecret` from the response.
3. POST /push/channelSubscriptions with the `deviceId` and target `channel` name.
4. Verify with GET /push/channelSubscriptions using `deviceId` to confirm the subscription is active.

### 4. Retrieve and Page Through Message History

1. GET /channels/{channel_id}/messages with `direction=backwards` and `limit=100` to get the most recent messages.
2. If 100 results are returned, extract the timestamp of the oldest message.
3. Repeat the request with `end` set to that timestamp to fetch the next page.
4. Continue until fewer than `limit` results are returned, indicating the end of history.

### 5. Generate a Temporary Token for Client-Side Use

1. POST /keys/{keyName}/requestToken with the key name (format: `appId.keyId`).
2. Extract the `token`, `issued`, and `expires` fields from the response.
3. Compute remaining TTL: `expires - issued`. Default is typically 60 minutes.
4. Pass the `token` value to the client application for use as a Bearer token.
5. Schedule token refresh before `expires` to avoid authentication interruptions.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
