---
name: sms-api
description: "SMS API skill. Use when working with SMS for sms. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# SMS API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /sms/messages -- verify access
3. POST /sms/messages -- create first messages

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### sms
| Method | Path | Description |
|--------|------|-------------|
| GET | /sms/messages | List Messages |
| POST | /sms/messages | Create Message |
| GET | /sms/messages/{id} | Get Message |
| PATCH | /sms/messages/{id} | Update Message |
| DELETE | /sms/messages/{id} | Delete Message |

## Enhanced Skill Content
## Question Mapping

- "List all SMS messages" -> GET /sms/messages
- "Send a text message to a phone number" -> POST /sms/messages
- "Send an MMS with media" -> POST /sms/messages (with `type: "mms"`)
- "Get the details of a specific message" -> GET /sms/messages/{id}
- "What is the delivery status of my message?" -> GET /sms/messages/{id}
- "Update a scheduled message before it sends" -> PATCH /sms/messages/{id}
- "Change the body of a queued message" -> PATCH /sms/messages/{id}
- "Cancel or delete a message" -> DELETE /sms/messages/{id}
- "Schedule a message for later" -> POST /sms/messages (with `scheduled_at`)
- "How much did a message cost?" -> GET /sms/messages/{id} (check `data.price`)
- "Why did my message fail?" -> GET /sms/messages/{id} (check `data.error`)
- "Page through all messages in my account" -> GET /sms/messages (use `cursor` and `limit`)
- "Send a message through a specific downstream service" -> POST /sms/messages (set `x-apideck-service-id`)
- "Get the raw upstream provider response" -> GET /sms/messages/{id} (set `raw=true`, read `_raw`)

## Response Tips

- **List (GET /sms/messages):** Paginated via cursor -- use `meta.cursors.next` as the `cursor` param for the next page; `meta.items_on_page` tells you how many came back (max `limit`, default 20). Stop when `links.next` is null.
- **Create/Update/Delete (POST, PATCH, DELETE):** Returns only `data.id` -- fetch GET /sms/messages/{id} afterward if you need the full record.
- **Detail (GET /sms/messages/{id}):** Full message object lives under `data`; pricing is nested in `data.price`, errors in `data.error` -- both can be null on success.
- **Errors (400/401/402/404/422):** 401 means bad API key or missing consumer/app headers; 402 signals a billing issue on the upstream connector; 422 is validation failure -- check the response body for field-level detail.

## Anomaly Flags

- **Message failure:** Surface `data.status` values `failed` or `undelivered` immediately with the `data.error.code` and `data.error.message`.
- **402 Payment Required:** Alert the user that the upstream SMS connector may need a plan upgrade or billing update.
- **Empty cursor on first page:** If `meta.items_on_page` is 0 on the initial list call, confirm the `x-apideck-consumer-id` and `x-apideck-service-id` are correct -- the consumer may have no connected SMS service.
- **Scheduled message in the past:** If `scheduled_at` is set to a datetime that has already passed, warn the user the message may send immediately or be rejected depending on the provider.
- **Price data present:** When `data.price.total_amount` is non-null on a retrieved message, proactively show the cost so the user is aware of spend.
- **Unknown direction:** If `data.direction` returns `unknown`, flag that the upstream provider could not classify the message origin.

## Playbook

### 1. Send an SMS and confirm delivery

1. POST /sms/messages with `from`, `to`, `body` (and required headers `x-apideck-consumer-id`, `x-apideck-app-id`).
2. Capture `data.id` from the 201 response.
3. GET /sms/messages/{id} using that ID.
4. Check `data.status` -- repeat step 3 until status is `delivered`, `failed`, or `undelivered`.
5. If `failed`, read `data.error.message` and surface it to the user.

### 2. Page through all messages

1. GET /sms/messages with `limit=20` (or desired page size).
2. Read `meta.cursors.next` from the response.
3. If `next` is not null, call GET /sms/messages with `cursor` set to that value.
4. Repeat until `meta.cursors.next` is null.
5. Aggregate `data` arrays from each page for the full message list.

### 3. Schedule, review, and cancel a message

1. POST /sms/messages with `from`, `to`, `body`, and `scheduled_at` set to a future ISO 8601 datetime.
2. Capture `data.id` from the 201 response.
3. GET /sms/messages/{id} to verify `data.status` is `scheduled` and `data.scheduled_at` is correct.
4. If the user changes their mind, DELETE /sms/messages/{id} to cancel.
5. Confirm deletion succeeded by checking for a 200 response with the matching `data.id`.

### 4. Update a message before it is sent

1. GET /sms/messages/{id} to confirm `data.status` is still `scheduled` or `queued`.
2. PATCH /sms/messages/{id} with updated `from`, `to`, and `body` fields (all three are required even if only one changes).
3. GET /sms/messages/{id} again to verify the update took effect.

### 5. Retrieve raw upstream provider data

1. GET /sms/messages/{id} with `raw=true`.
2. The response includes `_raw` containing the unmodified response from the downstream SMS provider.
3. Use this for debugging provider-specific fields or behaviors not normalized by Apideck.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
