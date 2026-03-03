---
name: bulksms-json-rest-api
description: "BulkSMS JSON REST API skill. Use when working with BulkSMS JSON REST for webhooks, profile, messages. Covers 15 endpoints."
version: 1.0.0
generator: lapsh
---

# BulkSMS JSON REST API
API version: 1.1.0

## Auth
basic

## Base URL
https://api.bulksms.com/v1

## Setup
1. Configure auth: basic
2. GET /webhooks -- verify access
3. POST /webhooks -- create first webhooks

## Endpoints

15 endpoints across 6 groups. See references/api-spec.lap for full details.

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| POST | /webhooks | Create a webhook |
| GET | /webhooks | List webhooks |
| GET | /webhooks/{id} | Read a webhook |
| POST | /webhooks/{id} | Update a webhook |
| DELETE | /webhooks/{id} | Delete a webhook |

### profile
| Method | Path | Description |
|--------|------|-------------|
| GET | /profile | Get profile |

### messages
| Method | Path | Description |
|--------|------|-------------|
| POST | /messages | Send Messages |
| GET | /messages | Retrieve Messages |
| GET | /messages/send | Send message by simple GET or POST |
| GET | /messages/{id}/relatedReceivedMessages | List Related Messages |
| GET | /messages/{id} | Show Message |

### blocked-numbers
| Method | Path | Description |
|--------|------|-------------|
| POST | /blocked-numbers | Create a blocked number |
| GET | /blocked-numbers | List blocked numbers |

### credit
| Method | Path | Description |
|--------|------|-------------|
| POST | /credit/transfer | Transfer credits to another account |

### rmm
| Method | Path | Description |
|--------|------|-------------|
| POST | /rmm/pre-sign-attachment | Upload an attachment via a signed URL |

## Enhanced Skill Content
## Question Mapping

- "How do I send an SMS message?" -> POST /messages
- "How do I send a quick SMS without a JSON body?" -> GET /messages/send
- "How do I check my account balance or credits?" -> GET /profile
- "How do I list all sent messages?" -> GET /messages
- "How do I check the delivery status of a message?" -> GET /messages/{id}
- "Did anyone reply to my message?" -> GET /messages/{id}/relatedReceivedMessages
- "How do I set up a webhook for delivery receipts?" -> POST /webhooks
- "How do I list all my webhooks?" -> GET /webhooks
- "How do I delete a webhook?" -> DELETE /webhooks/{id}
- "How do I block a phone number?" -> POST /blocked-numbers
- "How do I see which numbers are blocked?" -> GET /blocked-numbers
- "How do I transfer credits to a sub-account?" -> POST /credit/transfer
- "How do I schedule a message for later?" -> POST /messages (use `schedule-date` optional param)
- "How do I send a bulk batch of messages?" -> POST /messages (body is an array of message objects)
- "How do I attach media to a rich message?" -> POST /rmm/pre-sign-attachment, then POST /messages

## Response Tips

- **messages**: `GET /messages` supports `limit`, `filter`, and `sortOrder` -- paginate by adjusting filter criteria on message ID. 201 on successful send (not 200). Response is always an array, even for single sends.
- **webhooks**: All CRUD returns 200. Lookup by `{id}` returns 404 when not found -- check ID validity before retrying.
- **blocked-numbers**: `GET` supports cursor-based pagination via `min-id` and `limit`. POST body is a flat string array of phone numbers, not objects.
- **credit**: 403 means insufficient permissions or balance -- surface this clearly, do not retry.
- **profile**: Single object response with account metadata and remaining credits.
- **rmm**: Pre-sign returns a temporary upload URL -- it must be used promptly before expiry.

## Anomaly Flags

- **403 on send**: Agent should surface immediately -- likely means insufficient credits or account suspended. Check `GET /profile` for balance.
- **400 on POST /messages**: Commonly malformed phone numbers or missing required fields. Surface the response body which contains field-level errors.
- **Schedule date in the past**: API will reject with 400. Agent should validate `schedule-date` is future before sending.
- **Deduplication collisions**: If `deduplication-id` is reused, the API silently deduplicates. Flag when a send returns fewer results than messages submitted.
- **Blocked number sends**: Sends to blocked numbers may silently fail. Agent should cross-check `GET /blocked-numbers` when delivery issues arise.
- **Webhook 404**: A webhook was deleted or the ID is stale. Agent should suggest re-listing webhooks via `GET /webhooks`.
- **Empty related messages**: `GET /messages/{id}/relatedReceivedMessages` returning an empty array could mean replies haven't arrived yet or the number doesn't support two-way messaging.

## Playbook

### 1. Send a Single SMS and Track Delivery

1. `POST /messages` with body `[{"to": "+1234567890", "body": "Hello"}]`
2. Note the returned message `id` from the 201 response
3. `GET /messages/{id}` to check delivery status
4. Repeat step 3 until status is terminal (delivered or failed)

### 2. Set Up Inbound Message Webhooks

1. `POST /webhooks` with body specifying the trigger type and your callback URL
2. `GET /webhooks` to confirm it was created and note the `id`
3. Send a test message to your number and verify your endpoint receives the callback
4. If needed, update with `POST /webhooks/{id}` or remove with `DELETE /webhooks/{id}`

### 3. Send a Scheduled Bulk Campaign

1. Prepare an array of message objects with distinct `to` numbers
2. `POST /messages` with the array body, include `schedule-date` (ISO 8601 future timestamp) and `schedule-description`
3. Set `deduplication-id` to prevent accidental re-sends if retrying
4. `GET /messages?filter=...` to monitor the batch status after the scheduled time

### 4. Block a Number and Verify

1. `POST /blocked-numbers` with body `["+1234567890"]`
2. `GET /blocked-numbers` to confirm the number appears in the list
3. To review the full block list, paginate using `min-id` and `limit`

### 5. Transfer Credits Between Accounts

1. `GET /profile` to check available credit balance
2. `POST /credit/transfer` with body specifying target account and amount
3. `GET /profile` again to confirm the balance was deducted
4. If 403 is returned, verify account permissions and that the balance covers the transfer amount


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
