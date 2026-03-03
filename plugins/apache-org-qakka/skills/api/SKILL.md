---
name: qakka
description: "Qakka API skill. Use when working with Qakka for queues, status. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# Qakka
API version: v1

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /queues -- verify access
3. POST /queues -- create first queues

## Endpoints

10 endpoints across 2 groups. See references/api-spec.lap for full details.

### queues
| Method | Path | Description |
|--------|------|-------------|
| GET | /queues | Get list of all Queues. |
| POST | /queues | Create new queue. |
| DELETE | /queues/{queueName} | Delete Queue. |
| GET | /queues/{queueName}/config | Get Queue config. |
| PUT | /queues/{queueName}/config | Update Queue configuration. |
| GET | /queues/{queueName}/data/{queueMessageId} | Get data associated with a Queue Message. |
| GET | /queues/{queueName}/messages | Get next Queue Messages from a Queue |
| POST | /queues/{queueName}/messages | Send Queue Message with a binary data (blob) payload. |
| DELETE | /queues/{queueName}/messages/{queueMessageId} | Acknowledge that Queue Message has been processed. |

### status
| Method | Path | Description |
|--------|------|-------------|
| GET | /status | Status of webapp. |

## Enhanced Skill Content
## Question Mapping

- "What queues exist?" -> GET /queues
- "Create a new queue" -> POST /queues
- "Delete a queue called orders" -> DELETE /queues/{queueName}
- "Show me the config for the notifications queue" -> GET /queues/{queueName}/config
- "Update the configuration of my events queue" -> PUT /queues/{queueName}/config
- "Get a specific message from a queue by ID" -> GET /queues/{queueName}/data/{queueMessageId}
- "List messages in the tasks queue" -> GET /queues/{queueName}/messages
- "How many messages are in the jobs queue?" -> GET /queues/{queueName}/messages
- "Send a message to the alerts queue" -> POST /queues/{queueName}/messages
- "Send a delayed message to a queue" -> POST /queues/{queueName}/messages (use `delay` param)
- "Post a message that expires after 60 seconds" -> POST /queues/{queueName}/messages (use `expiration` param)
- "Remove a specific message from a queue" -> DELETE /queues/{queueName}/messages/{queueMessageId}
- "Is the Qakka service running?" -> GET /status
- "Delete a queue but skip confirmation" -> DELETE /queues/{queueName} (use `confirm` param)
- "Send a message to a specific region" -> POST /queues/{queueName}/messages (use `regions` param)

## Response Tips

- **Queues (list/create/delete):** All return 200 on success. DELETE may require the `confirm` parameter. Watch for 400 on invalid queue names or malformed create payloads.
- **Queue config (get/put):** 400 typically means the queue name is invalid or the config payload is malformed. Responses likely contain key-value settings -- inspect for retention, visibility, and size limits.
- **Messages (list/send/delete):** GET accepts `count` to limit results -- default may return all pending messages. POST requires `contentType` and a base64-encoded `body`. 404 on data fetch means the message was already consumed or expired.
- **Status:** Simple health check. 200 means the service is operational. Any other code indicates degraded state.

## Anomaly Flags

- **404 on message data fetch:** The message was consumed, expired, or never existed -- surface this to the user since it may indicate a race condition with competing consumers.
- **400 on queue deletion without confirm:** The API may require explicit confirmation before deleting a non-empty queue. Prompt the user to retry with `confirm` set.
- **Message expiration overlap:** If `delay` exceeds `expiration` when sending a message, the message may expire before delivery. Flag this mismatch proactively.
- **Empty queue list:** If GET /queues returns no results, confirm whether this is expected or if the service was recently reset.
- **Repeated 400 errors on POST /queues/messages:** Likely a `contentType` mismatch or improperly encoded `body` (must be base64). Surface encoding guidance.

## Playbook

### 1. Create a Queue and Send a Message

1. POST /queues to create the queue (note the queue name from the response)
2. GET /queues to verify the queue appears in the list
3. POST /queues/{queueName}/messages with `contentType`, base64-encoded `body`
4. GET /queues/{queueName}/messages to confirm the message was enqueued

### 2. Consume and Acknowledge a Message

1. GET /queues/{queueName}/messages with `count=1` to fetch one message
2. Extract the `queueMessageId` from the response
3. GET /queues/{queueName}/data/{queueMessageId} to retrieve full message content
4. Process the message in your application
5. DELETE /queues/{queueName}/messages/{queueMessageId} to acknowledge and remove it

### 3. Inspect and Update Queue Configuration

1. GET /queues/{queueName}/config to view current settings
2. Modify the desired fields in the config object
3. PUT /queues/{queueName}/config with the updated payload
4. GET /queues/{queueName}/config again to verify changes took effect

### 4. Safely Delete a Queue

1. GET /queues/{queueName}/messages to check for remaining messages
2. Process or drain any pending messages
3. DELETE /queues/{queueName} with `confirm` set to proceed
4. GET /queues to verify the queue no longer appears

### 5. Health Check and Service Diagnostics

1. GET /status to verify the service is running
2. GET /queues to list all active queues
3. For each queue, GET /queues/{queueName}/messages to check queue depths
4. Flag any queues with unexpectedly high message counts for investigation


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
