---
name: amazon-workmail-message-flow
description: "Amazon WorkMail Message Flow API skill. Use when working with Amazon WorkMail Message Flow for messages. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon WorkMail Message Flow
API version: 2019-05-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /messages/{messageId} -- verify access
3. POST /messages/{messageId} -- create first messages

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### messages
| Method | Path | Description |
|--------|------|-------------|
| GET | /messages/{messageId} | Retrieves the raw content of an in-transit email message, in MIME format. |
| POST | /messages/{messageId} | Updates the raw content of an in-transit email message, in MIME format. This example describes how to update in-transit email message. For more information and examples for using this API, see  Updating message content with AWS Lambda.  Updates to an in-transit message only appear when you call PutRawMessageContent from an AWS Lambda function configured with a synchronous  Run Lambda rule. If you call PutRawMessageContent on a delivered or sent message, the message remains unchanged, even though GetRawMessageContent returns an updated message. |

## Enhanced Skill Content
## Question Mapping

- "How do I get the content of an email message?" -> GET /messages/{messageId}
- "How do I retrieve a raw email by its ID?" -> GET /messages/{messageId}
- "How do I download a message for inspection or archiving?" -> GET /messages/{messageId}
- "Can I fetch an email to scan it for malware or compliance?" -> GET /messages/{messageId}
- "How do I update or replace the content of an in-transit message?" -> POST /messages/{messageId}
- "How do I modify an email before it gets delivered?" -> POST /messages/{messageId}
- "Can I rewrite message content to add a disclaimer or footer?" -> POST /messages/{messageId}
- "How do I strip attachments from a message in flight?" -> GET /messages/{messageId} then POST /messages/{messageId}
- "How do I intercept and transform emails using a Lambda flow?" -> GET /messages/{messageId} then POST /messages/{messageId}
- "Can I redact sensitive content from an outbound email?" -> GET /messages/{messageId} then POST /messages/{messageId}
- "What authentication do I need for WorkMail Message Flow?" -> Auth: AWS SigV4 (use AWS credentials, not API keys)
- "How do I read a message and then send a modified version back?" -> GET /messages/{messageId} then POST /messages/{messageId}

## Response Tips

- **GET /messages/{messageId}**: Returns raw bytes (`messageContent`), not JSON. Parse as RFC 5322 MIME content. The response is the full raw email including headers, body, and attachments. Stream large messages carefully.
- **POST /messages/{messageId}**: Expects `RawMessageContent` in the request body (MIME-formatted). A 200 response confirms the replacement succeeded. No body is guaranteed on success -- check the status code.
- **Errors**: Expect `ResourceNotFoundException` (invalid messageId), `InvalidContentLocation` (bad S3 reference in RawMessageContent), and `MessageFrozen` (message already delivered, too late to modify). All errors return JSON with `__type` and `message` fields.

## Anomaly Flags

- **MessageFrozen errors**: The message has already been delivered -- the Lambda flow rule may be misconfigured or processing is too slow. Surface immediately.
- **ResourceNotFoundException**: The messageId is invalid or expired. WorkMail message IDs are only valid during the synchronous Lambda invocation -- flag if this appears outside that context.
- **InvalidContentLocation**: The S3 object referenced in RawMessageContent is inaccessible. Check bucket permissions and region alignment.
- **Large message bodies**: Raw email content over 10 MB may hit Lambda or API payload limits. Flag when GET returns content near this threshold before attempting a POST.
- **SigV4 signing failures**: Region mismatch is the most common cause. The Message Flow endpoint region must match the WorkMail organization region.
- **Repeated POST failures on the same messageId**: Indicates a retry loop -- the message may already be frozen or the content malformed.

## Playbook

### 1. Inspect an Email in a Lambda Flow

1. Receive the `messageId` from the WorkMail Lambda event payload
2. Call `GET /messages/{messageId}` to retrieve the raw MIME content
3. Parse the MIME content to extract headers, body, and attachments
4. Perform your inspection (compliance check, malware scan, logging)
5. Return the Lambda response with the appropriate action (allow, bounce, drop)

### 2. Modify an Email Before Delivery

1. Receive the `messageId` from the WorkMail Lambda event payload
2. Call `GET /messages/{messageId}` to retrieve the original raw content
3. Parse and modify the MIME content (add disclaimer, rewrite headers, strip attachments)
4. Construct a valid `RawMessageContent` object with the updated MIME data
5. Call `POST /messages/{messageId}` with the new content
6. Return the Lambda response to allow delivery of the modified message

### 3. Add a Company Disclaimer to Outbound Email

1. Receive the `messageId` from an outbound mail flow rule Lambda trigger
2. Call `GET /messages/{messageId}` to fetch the raw message
3. Parse the MIME structure and locate the text/html and text/plain body parts
4. Append the disclaimer text to each body part, preserving MIME boundaries
5. Re-encode the full message as valid `RawMessageContent`
6. Call `POST /messages/{messageId}` to replace the original with the updated version

### 4. Archive Raw Emails to S3

1. Receive the `messageId` from the WorkMail Lambda event
2. Call `GET /messages/{messageId}` to retrieve the raw bytes
3. Upload the raw content to an S3 bucket with a key like `archive/{date}/{messageId}.eml`
4. Log the archive location for audit purposes
5. Return the Lambda response to allow normal delivery (no POST needed)


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
