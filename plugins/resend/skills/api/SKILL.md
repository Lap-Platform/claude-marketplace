---
name: resend
description: "Resend API skill. Use when working with Resend for emails, domains, api-keys. Covers 67 endpoints."
version: 1.0.0
generator: lapsh
---

# Resend
API version: 1.5.0

## Auth
Bearer bearer

## Base URL
https://api.resend.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /emails -- verify access
3. POST /emails -- create first emails

## Endpoints

67 endpoints across 11 groups. See references/api-spec.lap for full details.

### emails
| Method | Path | Description |
|--------|------|-------------|
| POST | /emails | Send an email |
| GET | /emails | Retrieve a list of emails |
| GET | /emails/{email_id} | Retrieve a single email |
| PATCH | /emails/{email_id} | Update a single email |
| POST | /emails/{email_id}/cancel | Cancel the schedule of the e-mail. |
| POST | /emails/batch | Trigger up to 100 batch emails at once. |
| GET | /emails/{email_id}/attachments | Retrieve a list of attachments for a sent email |
| GET | /emails/{email_id}/attachments/{attachment_id} | Retrieve a single attachment for a sent email |
| GET | /emails/receiving | Retrieve a list of received emails |
| GET | /emails/receiving/{email_id} | Retrieve a single received email |
| GET | /emails/receiving/{email_id}/attachments | Retrieve a list of attachments for a received email |
| GET | /emails/receiving/{email_id}/attachments/{attachment_id} | Retrieve a single attachment for a received email |

### domains
| Method | Path | Description |
|--------|------|-------------|
| POST | /domains | Create a new domain |
| GET | /domains | Retrieve a list of domains |
| GET | /domains/{domain_id} | Retrieve a single domain |
| PATCH | /domains/{domain_id} | Update an existing domain |
| DELETE | /domains/{domain_id} | Remove an existing domain |
| POST | /domains/{domain_id}/verify | Verify an existing domain |

### api-keys
| Method | Path | Description |
|--------|------|-------------|
| POST | /api-keys | Create a new API key |
| GET | /api-keys | Retrieve a list of API keys |
| DELETE | /api-keys/{api_key_id} | Remove an existing API key |

### templates
| Method | Path | Description |
|--------|------|-------------|
| POST | /templates | Create a template |
| GET | /templates | Retrieve a list of templates |
| GET | /templates/{id} | Retrieve a single template |
| PATCH | /templates/{id} | Update an existing template |
| DELETE | /templates/{id} | Remove an existing template |
| POST | /templates/{id}/publish | Publish a template |
| POST | /templates/{id}/duplicate | Duplicate a template |

### audiences
| Method | Path | Description |
|--------|------|-------------|
| POST | /audiences | Create a list of contacts |
| GET | /audiences | Retrieve a list of audiences |
| DELETE | /audiences/{id} | Remove an existing audience |
| GET | /audiences/{id} | Retrieve a single audience |

### contacts
| Method | Path | Description |
|--------|------|-------------|
| POST | /contacts | Create a new contact |
| GET | /contacts | Retrieve a list of contacts |
| GET | /contacts/{id} | Retrieve a single contact by ID or email |
| PATCH | /contacts/{id} | Update a single contact by ID or email |
| DELETE | /contacts/{id} | Remove an existing contact by ID or email |
| GET | /contacts/{contact_id}/segments | Retrieve a list of segments for a contact |
| POST | /contacts/{contact_id}/segments/{segment_id} | Add a contact to a segment |
| DELETE | /contacts/{contact_id}/segments/{segment_id} | Remove a contact from a segment |
| GET | /contacts/{contact_id}/topics | Retrieve topics for a contact |
| PATCH | /contacts/{contact_id}/topics | Update topics for a contact |

### broadcasts
| Method | Path | Description |
|--------|------|-------------|
| POST | /broadcasts | Create a broadcast |
| GET | /broadcasts | Retrieve a list of broadcasts |
| DELETE | /broadcasts/{id} | Remove an existing broadcast that is in the draft status |
| GET | /broadcasts/{id} | Retrieve a single broadcast |
| PATCH | /broadcasts/{id} | Update an existing broadcast |
| POST | /broadcasts/{id}/send | Send or schedule a broadcast |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| POST | /webhooks | Create a new webhook |
| GET | /webhooks | Retrieve a list of webhooks |
| GET | /webhooks/{webhook_id} | Retrieve a single webhook |
| PATCH | /webhooks/{webhook_id} | Update an existing webhook |
| DELETE | /webhooks/{webhook_id} | Remove an existing webhook |

### segments
| Method | Path | Description |
|--------|------|-------------|
| POST | /segments | Create a new segment |
| GET | /segments | Retrieve a list of segments |
| GET | /segments/{id} | Retrieve a single segment |
| DELETE | /segments/{id} | Remove an existing segment |

### topics
| Method | Path | Description |
|--------|------|-------------|
| POST | /topics | Create a new topic |
| GET | /topics | Retrieve a list of topics |
| GET | /topics/{id} | Retrieve a single topic |
| PATCH | /topics/{id} | Update an existing topic |
| DELETE | /topics/{id} | Remove an existing topic |

### contact-properties
| Method | Path | Description |
|--------|------|-------------|
| POST | /contact-properties | Create a new contact property |
| GET | /contact-properties | Retrieve a list of contact properties |
| GET | /contact-properties/{id} | Retrieve a single contact property |
| PATCH | /contact-properties/{id} | Update an existing contact property |
| DELETE | /contact-properties/{id} | Remove an existing contact property |

## Enhanced Skill Content
## Question Mapping

- "How do I send an email?" -> POST /emails
- "How do I send a batch of emails at once?" -> POST /emails/batch
- "Can I cancel a scheduled email?" -> POST /emails/{email_id}/cancel
- "How do I check the status of an email I sent?" -> GET /emails/{email_id}
- "How do I reschedule a scheduled email?" -> PATCH /emails/{email_id}
- "How do I add and verify a sending domain?" -> POST /domains + POST /domains/{domain_id}/verify
- "How do I create a reusable email template?" -> POST /templates
- "How do I send a broadcast to a segment of contacts?" -> POST /broadcasts + POST /broadcasts/{id}/send
- "How do I add a contact and subscribe them to a topic?" -> POST /contacts (with topics array)
- "How do I list all contacts in a specific segment?" -> GET /contacts?segment_id={id}
- "How do I manage a contact's topic subscriptions?" -> PATCH /contacts/{contact_id}/topics
- "How do I set up a webhook for email delivery events?" -> POST /webhooks
- "How do I create an API key with restricted permissions?" -> POST /api-keys (with permission: sending_access and domain_id)
- "How do I download an attachment from a received email?" -> GET /emails/receiving/{email_id}/attachments/{attachment_id} (use download_url from response)
- "How do I define custom properties on contacts?" -> POST /contact-properties + PATCH /contacts/{id} (set properties map)

## Response Tips

- **Emails / Domains / Contacts / Templates / Broadcasts / Webhooks / Segments / Topics / Contact Properties (list endpoints):** All paginated lists return `{object, has_more, data}`. Use `after` (cursor from last item ID) to page forward, `before` to page backward, and `limit` to control page size. Always check `has_more` before requesting the next page.
- **Emails (send):** POST /emails returns only `{id}` on success. Poll GET /emails/{id} and inspect `last_event` for delivery status (`delivered`, `bounced`, `complained`, etc.).
- **Domains:** POST /domains returns a `records` array with DNS entries (MX, TXT, CNAME) you must configure before calling /verify. The `status` field tracks verification progress.
- **Templates:** GET /templates/{id} includes `has_unpublished_versions` and `status` -- a template must be published (POST /templates/{id}/publish) before it can be used in emails.
- **Broadcasts:** The `status` field tracks lifecycle (`draft`, `queued`, `sending`, `sent`). Creating a broadcast does not send it unless `send: true` is passed; otherwise call POST /broadcasts/{id}/send separately.
- **API Keys:** POST /api-keys returns the plaintext `token` exactly once. It cannot be retrieved again after creation.
- **Webhooks:** POST /webhooks returns `signing_secret` -- store it immediately for signature verification. It is also available via GET /webhooks/{id}.
- **Errors:** All endpoints return standard HTTP error codes. 422 indicates validation failures (check the response body for field-level details). 429 indicates rate limiting.

## Anomaly Flags

- **API key token shown only once:** After POST /api-keys, surface a warning that the `token` value will never be retrievable again and must be stored now.
- **Domain not verified:** If GET /domains/{id} returns `status` other than `verified`, flag that emails from this domain may fail or land in spam. Prompt the user to add DNS records and call /verify.
- **Template unpublished changes:** If `has_unpublished_versions: true` on a template, alert that the live version differs from the latest draft. Suggest calling POST /templates/{id}/publish.
- **Broadcast created but not sent:** If a broadcast has `status: draft` and no `scheduled_at`, warn that it will not be delivered until POST /broadcasts/{id}/send is called.
- **Scheduled email approaching send time:** If PATCH /emails/{id} or cancel is attempted close to `scheduled_at`, warn that the window to modify may have passed.
- **Webhook disabled:** If GET /webhooks/{id} returns `status: disabled`, flag that events are not being delivered to that endpoint.
- **Pagination truncation:** If any list response returns `has_more: true`, surface that results are truncated and offer to fetch the next page.
- **Idempotency key usage:** When sending emails or batches, note whether `Idempotency-Key` was provided. If retrying a failed send without one, warn about potential duplicate delivery.
- **TLS enforcement:** If a domain is configured with `tls: opportunistic` (default), flag that emails may be sent over unencrypted connections. Suggest `enforced` for sensitive content.

## Playbook

### 1. Send Your First Email

1. Create an API key: POST /api-keys with `{name: "my-app", permission: "full_access"}`. Save the returned `token`.
2. Add a sending domain: POST /domains with `{name: "example.com"}`.
3. Configure DNS records returned in the response (MX, TXT, CNAME) with your DNS provider.
4. Verify the domain: POST /domains/{domain_id}/verify. Repeat until status is `verified`.
5. Send an email: POST /emails with `{from: "you@example.com", to: "recipient@example.com", subject: "Hello", html: "<p>Hi there</p>"}`.
6. Check delivery: GET /emails/{id} and inspect `last_event`.

### 2. Set Up a Newsletter with Broadcasts

1. Create an audience: POST /audiences with `{name: "Newsletter Subscribers"}`.
2. Create a topic: POST /topics with `{name: "Weekly Newsletter", default_subscription: "opt_in", visibility: "public"}`.
3. Add contacts: POST /contacts with `{email: "...", audience_id: "...", topics: [{id: "<topic_id>", subscription: "subscribed"}]}`.
4. Create a segment: POST /segments with `{name: "Active Subscribers", audience_id: "...", filter: {...}}`.
5. Create a broadcast: POST /broadcasts with `{segment_id: "...", from: "news@example.com", subject: "This Week", html: "...", topic_id: "..."}`.
6. Send or schedule: POST /broadcasts/{id}/send, optionally with `{scheduled_at: "2025-01-15T09:00:00Z"}`.

### 3. Manage Contact Segments and Subscriptions

1. List a contact's current segments: GET /contacts/{contact_id}/segments.
2. Add the contact to a new segment: POST /contacts/{contact_id}/segments/{segment_id}.
3. Remove from a segment: DELETE /contacts/{contact_id}/segments/{segment_id}.
4. View topic subscriptions: GET /contacts/{contact_id}/topics.
5. Update subscriptions: PATCH /contacts/{contact_id}/topics with `{topics: [{id: "...", subscription: "unsubscribed"}]}`.

### 4. Template Workflow (Create, Edit, Publish, Use)

1. Create a template: POST /templates with `{name: "Welcome", html: "<p>Hello {{name}}</p>", variables: [{key: "name", type: "string", fallback_value: "there"}]}`.
2. Preview by fetching: GET /templates/{id} to review the HTML and variable definitions.
3. Edit if needed: PATCH /templates/{id} with updated fields.
4. Publish the template: POST /templates/{id}/publish.
5. Send an email using the template: POST /emails with `{from: "...", to: "...", subject: "...", template: {id: "<template_id>", variables: {name: "Alice"}}}`.

### 5. Webhook Setup for Event Monitoring

1. Create a webhook: POST /webhooks with `{endpoint: "https://yourapp.com/hooks/resend", events: ["email.delivered", "email.bounced", "email.complained"]}`.
2. Store the `signing_secret` from the response for verifying incoming payloads.
3. List active webhooks: GET /webhooks to confirm registration.
4. If issues arise, check a specific webhook: GET /webhooks/{webhook_id} and verify `status` is `enabled`.
5. Update events or disable: PATCH /webhooks/{webhook_id} with `{events: [...], status: "enabled"}`.
6. Remove when no longer needed: DELETE /webhooks/{webhook_id}.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
