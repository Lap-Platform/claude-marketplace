---
name: marketing-cloud-rest-api
description: "Marketing Cloud REST API skill. Use when working with Marketing Cloud REST for asset, hub, messaging. Covers 29 endpoints."
version: 1.0.0
generator: lapsh
---

# Marketing Cloud REST API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://www.exacttargetapis.com

## Setup
1. No auth setup needed
2. GET /messaging/v1/email/definitions/ -- verify access
3. POST /asset/v1/content/assets -- create first assets

## Endpoints

29 endpoints across 3 groups. See references/api-spec.lap for full details.

### asset
| Method | Path | Description |
|--------|------|-------------|
| GET | /asset/v1/content/assets/{id} | getAssetById |
| PATCH | /asset/v1/content/assets/{id} | partiallyUpdateAssetById |
| DELETE | /asset/v1/content/assets/{id} | deleteAssetById |
| POST | /asset/v1/content/assets | createAsset |

### hub
| Method | Path | Description |
|--------|------|-------------|
| POST | /hub/v1/campaigns | createCampaign |
| GET | /hub/v1/campaigns/{id} | getCampaignById |
| DELETE | /hub/v1/campaigns/{id} | deleteCampaignById |

### messaging
| Method | Path | Description |
|--------|------|-------------|
| POST | /messaging/v1/email/definitions/ | createEmailDefinition |
| GET | /messaging/v1/email/definitions/ | getEmailDefinitions |
| DELETE | /messaging/v1/email/definitions/{definitionKey} | deleteEmailDefinition |
| PATCH | /messaging/v1/email/definitions/{definitionKey} | partiallyUpdateEmailDefinition |
| GET | /messaging/v1/email/definitions/{definitionKey} | getEmailDefinition |
| GET | /messaging/v1/email/definitions/{definitionKey}/queue | getQueueMetricsForEmailDefinition |
| DELETE | /messaging/v1/email/definitions/{definitionKey}/queue | deleteQueuedMessagesForEmailDefinition |
| POST | /messaging/v1/email/messages/ | sendEmailToMultipleRecipients |
| GET | /messaging/v1/email/messages/ | getEmailsNotSentToRecipients |
| GET | /messaging/v1/email/messages/{messageKey} | getEmailSendStatusForRecipient |
| POST | /messaging/v1/email/messages/{messageKey} | sendEmailToSingleRecipient |
| GET | /messaging/v1/sms/definitions/{definitionKey} | getSmsDefinition |
| PATCH | /messaging/v1/sms/definitions/{definitionKey} | partiallyUpdateSmsDefinition |
| DELETE | /messaging/v1/sms/definitions/{definitionKey} | deleteSmsDefinition |
| POST | /messaging/v1/sms/definitions | createSmsDefinition |
| GET | /messaging/v1/sms/definitions | getSmsDefinitions |
| GET | /messaging/v1/sms/definitions/{definitionKey}/queue | getQueueMetricsForSmsDefinition |
| DELETE | /messaging/v1/sms/definitions/{definitionKey}/queue | deleteQueuedMessagesForSmsDefinition |
| POST | /messaging/v1/sms/messages/ | sendSmsToMultipleRecipients |
| GET | /messaging/v1/sms/messages/ | getSMSsNotSentToRecipients |
| POST | /messaging/v1/sms/messages/{messageKey} | sendSmsToSingleRecipient |
| GET | /messaging/v1/sms/messages/{messageKey} | getSmsSendStatusForRecipient |

## Enhanced Skill Content
## Question Mapping

- "How do I retrieve a content asset by ID?" -> GET /asset/v1/content/assets/{id}
- "How do I update an existing content asset?" -> PATCH /asset/v1/content/assets/{id}
- "How do I delete a content asset?" -> DELETE /asset/v1/content/assets/{id}
- "How do I create a new content asset?" -> POST /asset/v1/content/assets
- "How do I create a new marketing campaign?" -> POST /hub/v1/campaigns
- "How do I get details for a specific campaign?" -> GET /hub/v1/campaigns/{id}
- "How do I set up a new email send definition?" -> POST /messaging/v1/email/definitions/
- "How do I list all email definitions with filtering?" -> GET /messaging/v1/email/definitions/
- "How do I send a transactional email to a recipient?" -> POST /messaging/v1/email/messages/
- "How do I check the status of a sent email?" -> GET /messaging/v1/email/messages/{messageKey}
- "How do I view what's queued for an email definition?" -> GET /messaging/v1/email/definitions/{definitionKey}/queue
- "How do I clear the send queue for an SMS definition?" -> DELETE /messaging/v1/sms/definitions/{definitionKey}/queue
- "How do I create a new SMS send definition?" -> POST /messaging/v1/sms/definitions
- "How do I send an SMS message?" -> POST /messaging/v1/sms/messages/
- "How do I check delivery status of an SMS message?" -> GET /messaging/v1/sms/messages/{messageKey}

## Response Tips

- **Asset endpoints**: Returns the full asset object on GET/PATCH/POST (200). Watch for 403 on permission issues -- verify your token scope covers asset operations.
- **Hub/Campaign endpoints**: Campaign GET returns a single campaign object (200). DELETE returns no body on success but may return 400/403 with error detail.
- **Email/SMS definitions**: List endpoints support OData-style pagination via `$pageSize`, `$page`, `$orderBy`, and `$filter` query params. POST returns 201 on creation; watch for 409 (conflict) indicating a duplicate definitionKey.
- **Email/SMS messages**: Send endpoints return 202 (accepted, not completed) -- delivery is async. Status polling via GET uses `type` (required) plus `$pageSize` and `lastEventId` for cursor-based pagination.
- **Queue endpoints**: Queue GET/DELETE operate on pending sends for a definition. Useful for pausing or inspecting a backlog before it processes.

## Anomaly Flags

- **409 Conflict on definition creation**: A definition with that key already exists. Surface this immediately -- the caller likely needs to PATCH instead of POST, or choose a different definitionKey.
- **401 on message endpoints**: Message status/send endpoints return 401 (unlike most other endpoints which return 403). This signals an expired or invalid OAuth token -- prompt for re-authentication.
- **202 vs 200 responses**: Email/SMS send operations return 202, meaning the message is queued, not delivered. Flag if a caller assumes synchronous delivery.
- **500 errors on messaging endpoints**: All messaging definition and message endpoints can return 500. If encountered, surface as a platform-side issue and recommend retry with backoff.
- **Missing queue items**: If a queue GET returns empty but sends are expected, flag that messages may have already processed or the definition is paused.
- **404 on definition GET/DELETE**: The definitionKey does not exist. Surface this proactively when it follows a recent creation attempt (possible typo or propagation delay).

## Playbook

### 1. Send a Transactional Email End-to-End

1. Create a content asset for the email body: POST /asset/v1/content/assets
2. Create an email send definition referencing the asset: POST /messaging/v1/email/definitions/
3. Trigger the email send with recipient data: POST /messaging/v1/email/messages/
4. Poll for delivery status using the returned messageKey: GET /messaging/v1/email/messages/{messageKey}

### 2. Set Up and Launch an SMS Campaign

1. Create a campaign in the hub: POST /hub/v1/campaigns
2. Create an SMS send definition: POST /messaging/v1/sms/definitions
3. Send the SMS message with subscriber data: POST /messaging/v1/sms/messages/
4. Check delivery status: GET /messaging/v1/sms/messages/{messageKey}
5. If issues arise, inspect the queue: GET /messaging/v1/sms/definitions/{definitionKey}/queue

### 3. Update and Republish an Email Definition

1. Retrieve the current definition: GET /messaging/v1/email/definitions/{definitionKey}
2. Clear any pending queued sends: DELETE /messaging/v1/email/definitions/{definitionKey}/queue
3. Update the definition with new settings: PATCH /messaging/v1/email/definitions/{definitionKey}
4. Verify the update took effect: GET /messaging/v1/email/definitions/{definitionKey}

### 4. Audit All Email and SMS Definitions

1. List all email definitions with pagination: GET /messaging/v1/email/definitions/?$pageSize=50&$page=1
2. Iterate through pages, incrementing `$page` until results are empty
3. Repeat for SMS definitions: GET /messaging/v1/sms/definitions?$pageSize=50&$page=1
4. For each definition, check its queue depth: GET /messaging/v1/email/definitions/{definitionKey}/queue
5. Flag any definitions with large queues or error states

### 5. Clean Up Unused Assets and Campaigns

1. Retrieve the asset to confirm it is unused: GET /asset/v1/content/assets/{id}
2. Delete the asset: DELETE /asset/v1/content/assets/{id}
3. Retrieve the campaign to verify status: GET /hub/v1/campaigns/{id}
4. Delete the campaign: DELETE /hub/v1/campaigns/{id}
5. Remove any associated email/SMS definitions: DELETE /messaging/v1/email/definitions/{definitionKey} and DELETE /messaging/v1/sms/definitions/{definitionKey}


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
