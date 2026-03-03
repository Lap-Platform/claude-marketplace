---
name: twilio-sendgrid-mail-api
description: "Twilio SendGrid Mail API skill. Use when working with Twilio SendGrid Mail for mail. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio SendGrid Mail API
API version: 1.0.0

## Auth
Bearer bearer

## Base URL
https://api.sendgrid.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v3/mail/batch/{batch_id} -- verify access
3. POST /v3/mail/batch -- create first batch

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### mail
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/mail/batch | Create a batch ID. |
| GET | /v3/mail/batch/{batch_id} | Validate a batch ID. |
| POST | /v3/mail/send | Send Email with Twilio SendGrid. |

## Enhanced Skill Content
## Question Mapping

- "How do I send an email with SendGrid?" -> POST /v3/mail/send
- "How do I send an email with attachments?" -> POST /v3/mail/send
- "How do I send a templated email using dynamic data?" -> POST /v3/mail/send (use `template_id` + `dynamic_template_data`)
- "How do I schedule an email to send later?" -> POST /v3/mail/send (use `send_at` field)
- "How do I send a batch of emails?" -> POST /v3/mail/batch then POST /v3/mail/send with `batch_id`
- "How do I create a batch ID for scheduled sends?" -> POST /v3/mail/batch
- "How do I look up an existing batch?" -> GET /v3/mail/batch/{batch_id}
- "How do I cancel a scheduled batch of emails?" -> GET /v3/mail/batch/{batch_id} (retrieve first, then use SendGrid cancel API)
- "How do I send email on behalf of a subuser?" -> POST /v3/mail/send with `on-behalf-of` header
- "How do I add CC and BCC recipients?" -> POST /v3/mail/send (use `cc` and `bcc` in `personalizations`)
- "How do I enable click and open tracking?" -> POST /v3/mail/send (use `tracking_settings`)
- "How do I test an email without actually sending it?" -> POST /v3/mail/send with `mail_settings.sandbox_mode.enable: true`
- "How do I add UTM tracking parameters to links?" -> POST /v3/mail/send (use `tracking_settings.ganalytics`)
- "How do I send to multiple recipients with different substitutions?" -> POST /v3/mail/send (use multiple entries in `personalizations` array)

## Response Tips

- **Mail Send (POST /v3/mail/send):** Returns 202 with an empty body on success -- no confirmation payload. A 202 means accepted for processing, not delivered. Check Activity Feed or Event Webhook for delivery status.
- **Batch Create (POST /v3/mail/batch):** Returns 201 with `{ batch_id }`. Store this ID; you need it to manage or cancel scheduled sends.
- **Batch Retrieve (GET /v3/mail/batch/{batch_id}):** Returns 200 with `{ batch_id }`. Use this to verify a batch ID exists before referencing it in send calls.
- **Errors (all endpoints):** 400 means malformed request (check field validation). 413 on send means payload too large (attachments or too many personalizations). 403 typically means the authenticated user lacks permission or the feature is not enabled on the account.

## Anomaly Flags

- **413 on send:** Payload exceeds size limit. Surface immediately -- agent should suggest reducing attachment size or splitting into multiple sends.
- **403 errors:** May indicate the account plan does not support the feature (e.g., dedicated IP pools, subuser delegation). Flag and recommend checking account tier.
- **Empty 202 response:** Expected behavior, but agent should proactively note that "accepted" does not mean "delivered" and suggest setting up Event Webhooks for delivery confirmation.
- **`send_at` in the past:** SendGrid may reject or send immediately. Agent should validate timestamps are in the future and within the 72-hour scheduling window.
- **Large `personalizations` array:** Each send supports up to 1,000 personalizations. Agent should warn when approaching this limit and suggest batching.
- **Missing `subject`:** Required either at the top level or within each personalization. Agent should flag if absent from both locations.
- **`sandbox_mode` enabled:** Agent should proactively warn that no email will actually be sent -- easy to forget during testing.

## Playbook

### 1. Send a Simple Email

1. Call `POST /v3/mail/send` with `from`, `personalizations[0].to`, `subject`, and `content` (type `text/plain` or `text/html`).
2. Confirm a 202 response (empty body).
3. Note: delivery is asynchronous. Use Event Webhook or Activity Feed for status.

### 2. Send a Templated Email with Dynamic Data

1. Create a Dynamic Template in the SendGrid dashboard and note the `template_id` (starts with `d-`).
2. Call `POST /v3/mail/send` with `template_id` set and `dynamic_template_data` inside each personalization containing the merge variables.
3. Omit `content` -- the template provides it. Include `subject` only if you want to override the template subject.
4. Confirm a 202 response.

### 3. Schedule a Batch of Emails

1. Call `POST /v3/mail/batch` to get a `batch_id`.
2. For each send, call `POST /v3/mail/send` with the `batch_id` and `send_at` set to a future Unix timestamp (within 72 hours).
3. To verify the batch exists, call `GET /v3/mail/batch/{batch_id}`.
4. To cancel or pause, use the batch cancel/pause endpoints (outside this spec) referencing the same `batch_id`.

### 4. Send on Behalf of a Subuser

1. Obtain the subuser's username.
2. Call `POST /v3/mail/send` (or batch endpoints) with the `on-behalf-of` header set to the subuser's username.
3. The `from` address should match a verified sender identity on the subuser's account.
4. Confirm a 202 response.

### 5. Test an Email in Sandbox Mode

1. Build the full send payload as you would for production.
2. Add `mail_settings: { sandbox_mode: { enable: true } }` to the request body.
3. Call `POST /v3/mail/send` and confirm a 202 response.
4. No email is sent -- this validates the request structure only. Remove `sandbox_mode` when ready to send for real.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
