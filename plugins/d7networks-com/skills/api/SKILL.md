---
name: d7sms
description: "D7SMS API skill. Use when working with D7SMS for balance, send, sendbatch. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# D7SMS
API version: 1.0.2

## Auth
basic

## Base URL
https://rest-api.d7networks.com/secure

## Setup
1. Configure auth: basic
2. GET /balance -- verify access
3. POST /send -- create first send

## Endpoints

3 endpoints across 3 groups. See references/api-spec.lap for full details.

### balance
| Method | Path | Description |
|--------|------|-------------|
| GET | /balance | Balance |

### send
| Method | Path | Description |
|--------|------|-------------|
| POST | /send | SendSMS |

### sendbatch
| Method | Path | Description |
|--------|------|-------------|
| POST | /sendbatch | Bulk SMS |

## Enhanced Skill Content
## Question Mapping

- "What is my current SMS balance?" -> GET /balance
- "How many credits do I have left?" -> GET /balance
- "Send a text message to a phone number" -> POST /send
- "How do I send an SMS?" -> POST /send
- "Send a message to multiple recipients at once" -> POST /sendbatch
- "How do I broadcast an SMS to a list of numbers?" -> POST /sendbatch
- "Can I check if the API is reachable and my credentials work?" -> GET /balance
- "Send the same message to 50 different numbers" -> POST /sendbatch
- "What happens if I run out of credits mid-batch?" -> POST /sendbatch
- "How do I authenticate with the D7SMS API?" -> All endpoints use Basic Auth
- "Send an individual SMS and then check remaining balance" -> POST /send, then GET /balance
- "What content types does the send endpoint accept?" -> POST /send (Content-Type + Accept headers required)

## Response Tips

- **Balance** (`GET /balance`): Returns current account credit balance. A 500 error typically indicates invalid credentials or a service outage rather than a balance problem.
- **Send** (`POST /send`): Expects a JSON body map with recipient and message fields; 200 confirms acceptance for delivery, not guaranteed delivery. Watch for 500 errors indicating malformed payloads or auth failures.
- **Send Batch** (`POST /sendbatch`): Same body structure as send but with multiple recipients; no documented error codes beyond 200, so treat any non-200 as a failure and retry or escalate.

## Anomaly Flags

- **Low balance**: After each `POST /send` or `/sendbatch`, check `GET /balance` and warn if credits drop below a threshold (suggest the user define one).
- **Repeated 500 errors**: The API only documents 500 as its error code. Flag if multiple consecutive requests return 500 -- likely an auth issue, service outage, or account suspension rather than a transient error.
- **Missing error response on batch**: `POST /sendbatch` has no documented error codes. If a non-200 status is returned, surface it immediately as unexpected behavior.
- **Auth misconfiguration**: Basic Auth credentials are sent on every request. Flag if any endpoint returns 401 or 403 (undocumented but possible) -- the user likely has wrong credentials.
- **Batch size concerns**: No documented limit on batch recipients. If a user attempts a very large batch (1000+), warn that the API may silently truncate or timeout.

## Playbook

### 1. Send a Single SMS

1. Confirm Basic Auth credentials are configured (username + password).
2. `POST /send` with `Content-Type: application/json` and `Accept: application/json`.
3. Include body with recipient number and message text.
4. Verify 200 response confirming message acceptance.
5. Optionally `GET /balance` to confirm credits were deducted.

### 2. Broadcast to Multiple Recipients

1. Prepare the list of recipient phone numbers.
2. `POST /sendbatch` with the recipient list and message in the body map.
3. Check for a 200 response. Any other status means the entire batch may have failed.
4. `GET /balance` to verify credits were deducted proportionally.

### 3. Monitor Account Health

1. `GET /balance` to retrieve current credit level.
2. Compare against a user-defined minimum threshold.
3. If below threshold, alert the user to top up before sending more messages.
4. Repeat on a schedule or before each send operation.

### 4. Validate Credentials and Connectivity

1. `GET /balance` as a lightweight connectivity and auth check.
2. A 200 response confirms credentials are valid and the API is reachable.
3. A 500 response suggests invalid credentials or a service issue -- verify username/password and retry.

### 5. Send-Then-Verify Workflow

1. `GET /balance` to record the starting credit count.
2. `POST /send` (or `/sendbatch`) with the desired message.
3. `GET /balance` again to confirm credits decreased by the expected amount.
4. If the balance did not change, the message may not have been sent despite a 200 -- investigate further.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
