---
name: winsms
description: "WINSMS API skill. Use when working with WINSMS for credits, sms, shortcode. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# WINSMS
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://api.winsms.co.za/api/rest/v1

## Setup
1. No auth setup needed
2. GET /credits/balance -- verify access
3. POST /credits/transfer -- create first transfer

## Endpoints

11 endpoints across 4 groups. See references/api-spec.lap for full details.

### credits
| Method | Path | Description |
|--------|------|-------------|
| GET | /credits/balance | Get your current WinSMS credit balance |
| POST | /credits/transfer | Transfer credits between main and sub accounts. |

### sms
| Method | Path | Description |
|--------|------|-------------|
| POST | /sms/outgoing/send | Send SMS messages |
| POST | /sms/outgoing/sendmulti | Send multiple different SMS messages |
| POST | /sms/outgoing/status | Get SMS delivery statuses |
| GET | /sms/scheduled | Get a list of scheduled SMS messages |
| POST | /sms/scheduled/delete | Delete scheduled SMS messages and refund credits |
| GET | /sms/incoming | Get a list of incoming SMS messages |
| GET | /sms/incoming/optout | Get a list of incoming opt-out SMS messages |

### shortcode
| Method | Path | Description |
|--------|------|-------------|
| GET | /shortcode/incoming | Get a list of incoming short/long code messages |

### subaccounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /subaccounts | Get a list of all Sub Accounts. |

## Enhanced Skill Content


## Question Mapping

- "How many SMS credits do I have left?" -> GET /credits/balance
- "Transfer credits to a sub-account" -> POST /credits/transfer
- "Send an SMS to a single number" -> POST /sms/outgoing/send
- "Send different messages to multiple recipients" -> POST /sms/outgoing/sendmulti
- "Did my message get delivered?" -> POST /sms/outgoing/status
- "What messages are scheduled to go out?" -> GET /sms/scheduled
- "Cancel a scheduled SMS" -> POST /sms/scheduled/delete
- "Show me replies I've received" -> GET /sms/incoming
- "Which numbers have opted out?" -> GET /sms/incoming/optout
- "List messages received on my shortcode" -> GET /shortcode/incoming
- "Show all my sub-accounts" -> GET /subaccounts
- "Send a bulk campaign and then check delivery status" -> POST /sms/outgoing/sendmulti + POST /sms/outgoing/status
- "How many credits remain after a transfer?" -> POST /credits/transfer + GET /credits/balance
- "Page through my incoming messages" -> GET /sms/incoming (with offset & limit)

## Response Tips

- **Credits**: Balance is a simple numeric value; transfer responses confirm the moved amount -- check for 422 if the transfer exceeds available credits.
- **Outgoing SMS**: Send endpoints return per-recipient status arrays -- iterate each entry to catch partial failures even on a 200.
- **Message Status**: Pass an array of message IDs; response maps each ID to its delivery state -- missing IDs may indicate expired or invalid references.
- **Scheduled/Incoming SMS**: Support `offset` and `limit` for pagination -- absence of these params returns the default page; keep paging until results come back empty.
- **Shortcode/Subaccounts**: Flat list responses; shortcode incoming supports pagination, subaccounts does not.

## Anomaly Flags

- **Low credit balance**: Surface a warning when credits drop below a configurable threshold after any send or transfer operation.
- **Partial send failures**: Flag when a 200 response contains individual recipient errors within the results array.
- **422 Unprocessable Entity**: Indicates validation failure (bad phone format, insufficient credits, empty message) -- surface the specific rejection reason.
- **413 Payload Too Large**: Recipient list or message body exceeds limits -- alert and suggest splitting the batch.
- **401 Unauthorized**: Auth credentials invalid or expired -- prompt for re-authentication immediately rather than retrying.
- **Opt-out list growth**: Note when the opt-out list has grown since last check, as sending to opted-out numbers wastes credits and risks compliance issues.
- **Rate limiting (repeated 500s)**: Consecutive server errors may signal throttling -- back off and surface the pattern.

## Playbook

### 1. Send a Single SMS and Confirm Delivery

1. Check credits with `GET /credits/balance` to ensure sufficient funds.
2. Send the message via `POST /sms/outgoing/send` with recipient number and message text.
3. Extract the message ID from the response.
4. Wait a reasonable interval (30-60 seconds).
5. Check delivery status with `POST /sms/outgoing/status` using the message ID.

### 2. Run a Bulk Campaign with Different Messages

1. Verify credit balance with `GET /credits/balance` -- ensure it covers all recipients.
2. Check `GET /sms/incoming/optout` and remove opted-out numbers from your list.
3. Send via `POST /sms/outgoing/sendmulti` with per-recipient message details.
4. Inspect the response array for any per-recipient failures.
5. Collect all message IDs and batch-check delivery via `POST /sms/outgoing/status`.

### 3. Manage Scheduled Messages

1. List pending scheduled messages with `GET /sms/scheduled` (paginate with offset/limit).
2. Identify messages to cancel by their IDs.
3. Delete them via `POST /sms/scheduled/delete` with the array of IDs.
4. Re-fetch `GET /sms/scheduled` to confirm deletion.

### 4. Monitor Incoming Messages and Replies

1. Poll `GET /sms/incoming` with offset/limit to page through new replies.
2. For shortcode traffic, also check `GET /shortcode/incoming` with pagination.
3. Periodically review `GET /sms/incoming/optout` to maintain a clean suppression list.
4. Update your contact records to exclude opted-out numbers from future sends.

### 5. Transfer Credits Between Accounts

1. List sub-accounts with `GET /subaccounts` to get the target account identifier.
2. Check source balance via `GET /credits/balance`.
3. Execute `POST /credits/transfer` with the target account and amount.
4. Verify the new balance with `GET /credits/balance` to confirm the deduction.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
