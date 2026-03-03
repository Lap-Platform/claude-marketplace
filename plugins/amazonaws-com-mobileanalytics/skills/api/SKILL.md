---
name: amazon-mobile-analytics
description: "Amazon Mobile Analytics API skill. Use when working with Amazon Mobile Analytics for 2014-06-05. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Amazon Mobile Analytics
API version: 2014-06-05

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /2014-06-05/events -- create first events

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### 2014-06-05
| Method | Path | Description |
|--------|------|-------------|
| POST | /2014-06-05/events | The PutEvents operation records one or more events. You can have up to 1,500 unique custom events per app, any combination of up to 40 attributes and metrics per custom event, and any number of attribute or metric values. |

## Enhanced Skill Content
## Question Mapping

- "How do I send analytics events?" -> POST /2014-06-05/events
- "How do I record a custom event in Mobile Analytics?" -> POST /2014-06-05/events
- "How do I batch multiple events in one request?" -> POST /2014-06-05/events
- "How do I send session start/stop events?" -> POST /2014-06-05/events
- "How do I report monetization events?" -> POST /2014-06-05/events
- "What client context headers are required?" -> POST /2014-06-05/events
- "How do I send compressed event payloads?" -> POST /2014-06-05/events (with x-amz-Client-Context-Encoding: gzip)
- "How do I track app usage from a mobile device?" -> POST /2014-06-05/events
- "What format does the events array expect?" -> POST /2014-06-05/events
- "How do I authenticate requests to Mobile Analytics?" -> All endpoints use AWS SigV4
- "Why is my PutEvents call returning BadRequestException?" -> POST /2014-06-05/events (check x-amz-Client-Context and events payload)
- "Can I send events without the client context header?" -> No, x-amz-Client-Context is required on POST /2014-06-05/events

## Response Tips

- **PUT Events (POST /2014-06-05/events):** Successful calls return 202 Accepted with an empty body. A 500 with BadRequestException means the `x-amz-Client-Context` header is malformed or the `events` array contains invalid Event objects. Validate that client context is valid Base64-encoded JSON and each Event has required fields (eventType, timestamp, session).

## Anomaly Flags

- **BadRequestException on 500:** This API returns client errors as HTTP 500 rather than 400 -- surface this clearly so users do not assume a server-side outage.
- **Missing Client Context:** If `x-amz-Client-Context` is omitted or not valid Base64 JSON, the call fails silently or with a confusing error. Flag when the header appears missing from a request.
- **Deprecated Service:** Amazon Mobile Analytics has been superseded by Amazon Pinpoint. Surface a notice recommending migration to Pinpoint for new projects.
- **Large Batch Sizes:** If the events array exceeds service limits (typically 100 events or 4 MB payload), the request will be rejected. Flag when batch sizes approach these thresholds.
- **Encoding Mismatch:** If `x-amz-Client-Context-Encoding` is set but the payload is not actually compressed (or vice versa), the request will fail. Flag when the header and payload do not match.

## Playbook

### 1. Send a Basic Analytics Event

1. Construct the `x-amz-Client-Context` header as Base64-encoded JSON containing `client.client_id`, `client.app_title`, `client.app_version_name`, `env.platform`, and `services.mobile_analytics.app_id`.
2. Build an Event object with `eventType`, `timestamp` (ISO 8601), and `session` (with `id`, `startTimestamp`).
3. POST to `/2014-06-05/events` with the header and `{"events": [...]}` body.
4. Sign the request with AWS SigV4 using your credentials.
5. Confirm a 202 Accepted response.

### 2. Batch Multiple Events in One Call

1. Collect events locally (up to 100 or 4 MB).
2. Build an array of Event objects, each with its own `eventType` and `timestamp`.
3. Send a single POST to `/2014-06-05/events` with all events in the array.
4. On BadRequestException, validate each event individually to isolate the malformed entry.

### 3. Send Compressed Payloads

1. Gzip the JSON request body.
2. Add header `x-amz-Client-Context-Encoding: gzip`.
3. POST to `/2014-06-05/events` with the compressed body.
4. If you receive a BadRequestException, verify the body is valid gzip and the encoding header is present.

### 4. Migrate to Amazon Pinpoint

1. Create a Pinpoint project in the AWS console.
2. Replace the Mobile Analytics `app_id` in your client context with the Pinpoint project ID.
3. Switch from `POST /2014-06-05/events` to the Pinpoint `PutEvents` API.
4. Update AWS SDK calls from `MobileAnalytics` client to `Pinpoint` client.
5. Verify events appear in the Pinpoint console analytics dashboard.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object
- Error responses use types: BadRequestException

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
