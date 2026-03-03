---
name: webhooks-management
description: "Webhooks Management API skill. Use when working with Webhooks Management for notifications. Covers 16 endpoints."
version: 1.0.0
generator: lapsh
---

# Webhooks Management
API version: 1.11

## Auth
OAuth2

## Base URL
https://api-m.sandbox.paypal.com

## Setup
1. Configure auth: OAuth2
2. GET /v1/notifications/webhooks -- verify access
3. POST /v1/notifications/webhooks -- create first webhooks

## Endpoints

16 endpoints across 1 groups. See references/api-spec.lap for full details.

### notifications
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/notifications/webhooks | Create webhook |
| GET | /v1/notifications/webhooks | List webhooks |
| GET | /v1/notifications/webhooks/{webhook_id} | Show webhook details |
| PATCH | /v1/notifications/webhooks/{webhook_id} | Update webhook |
| DELETE | /v1/notifications/webhooks/{webhook_id} | Delete webhook |
| GET | /v1/notifications/webhooks/{webhook_id}/event-types | List event subscriptions for webhook |
| POST | /v1/notifications/webhooks-lookup | Create webhook lookup |
| GET | /v1/notifications/webhooks-lookup | List webhook lookups |
| GET | /v1/notifications/webhooks-lookup/{webhook_lookup_id} | Show webhook lookup details |
| DELETE | /v1/notifications/webhooks-lookup/{webhook_lookup_id} | Delete webhook lookup |
| POST | /v1/notifications/verify-webhook-signature | Verify webhook signature |
| GET | /v1/notifications/webhooks-event-types | List available events |
| GET | /v1/notifications/webhooks-events | List event notifications |
| GET | /v1/notifications/webhooks-events/{event_id} | Show event notification details |
| POST | /v1/notifications/webhooks-events/{event_id}/resend | Resend event notification |
| POST | /v1/notifications/simulate-event | Simulate webhook event |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new webhook?" -> POST /v1/notifications/webhooks
- "What webhooks do I have registered?" -> GET /v1/notifications/webhooks
- "Show me the details of a specific webhook" -> GET /v1/notifications/webhooks/{webhook_id}
- "How do I update my webhook URL or event types?" -> PATCH /v1/notifications/webhooks/{webhook_id}
- "How do I delete a webhook?" -> DELETE /v1/notifications/webhooks/{webhook_id}
- "What event types is my webhook subscribed to?" -> GET /v1/notifications/webhooks/{webhook_id}/event-types
- "What event types are available to subscribe to?" -> GET /v1/notifications/webhooks-event-types
- "Show me recent webhook events" -> GET /v1/notifications/webhooks-events
- "Get details of a specific webhook event" -> GET /v1/notifications/webhooks-events/{event_id}
- "How do I resend a failed webhook event?" -> POST /v1/notifications/webhooks-events/{event_id}/resend
- "How do I verify an incoming webhook signature?" -> POST /v1/notifications/verify-webhook-signature
- "How do I test my webhook without a real transaction?" -> POST /v1/notifications/simulate-event
- "How do I look up webhooks by client ID?" -> POST /v1/notifications/webhooks-lookup
- "Show me all webhook lookups" -> GET /v1/notifications/webhooks-lookup
- "How do I filter webhook events by date range or type?" -> GET /v1/notifications/webhooks-events (use start_time, end_time, event_type params)

## Response Tips

- **Webhook CRUD (create/get/patch):** Responses include HATEOAS `links` array -- use `rel` values to discover available actions without hardcoding URLs.
- **List endpoints (webhooks, events, lookups):** Results are wrapped in a plural key (`webhooks`, `events`, `webhooks_lookups`) -- always access the array property, not the root object.
- **Event listing:** Uses `count` + `links` for pagination (look for `rel: "next"`); default `page_size` is 10, increase for bulk retrieval.
- **Delete operations:** Return 204 with no body -- a successful delete means an empty response, not an error.
- **Async operations (resend, simulate):** Return 202 Accepted -- the event is queued, not immediately delivered; poll or check your endpoint for confirmation.
- **Signature verification:** Returns `verification_status` as a string -- check for `"SUCCESS"` explicitly; any other value means the signature is invalid.

## Anomaly Flags

- **Verification failure:** If `verify-webhook-signature` returns a status other than `"SUCCESS"`, surface immediately -- this may indicate tampered or replayed payloads.
- **Empty event subscriptions:** If a webhook's `event_types` array is empty after creation or update, warn that no events will be delivered.
- **Stale webhooks:** If listing webhooks returns entries with URLs pointing to localhost, non-HTTPS, or known-dead domains, flag for cleanup.
- **High resend volume:** Multiple calls to `/resend` for the same event suggest the receiving endpoint is failing -- recommend checking endpoint health.
- **Deprecated event types:** If `event_types` returned by a webhook include types not present in `/webhooks-event-types`, flag them as potentially deprecated or removed.
- **Pagination overflow:** If `count` in event listing is significantly higher than `page_size` and no `next` link is followed, warn that results are incomplete.
- **Sandbox vs production base URL:** The base URL is `api-m.sandbox.paypal.com` -- surface a reminder when the user appears to intend production use.

## Playbook

### 1. Set Up a New Webhook End-to-End

1. Call `GET /v1/notifications/webhooks-event-types` to list all available event types.
2. Choose the event types relevant to your use case (e.g., `PAYMENT.CAPTURE.COMPLETED`).
3. Call `POST /v1/notifications/webhooks` with your HTTPS endpoint URL and selected `event_types`.
4. Note the returned `id` -- you will need it for verification and management.
5. Call `POST /v1/notifications/simulate-event` with one of your subscribed event types to confirm delivery.

### 2. Verify an Incoming Webhook Notification

1. Extract from the incoming HTTP headers: `PAYPAL-AUTH-ALGO`, `PAYPAL-CERT-URL`, `PAYPAL-TRANSMISSION-ID`, `PAYPAL-TRANSMISSION-SIG`, `PAYPAL-TRANSMISSION-TIME`.
2. Parse the request body as the `webhook_event` object.
3. Call `POST /v1/notifications/verify-webhook-signature` with all extracted values plus your `webhook_id`.
4. Check that `verification_status` equals `"SUCCESS"` before processing the event.
5. If verification fails, log the full payload and headers for investigation -- do not process the event.

### 3. Debug Missing or Failed Webhook Deliveries

1. Call `GET /v1/notifications/webhooks-events` with `start_time` and `end_time` covering the expected window.
2. Optionally filter by `event_type` or `transaction_id` to narrow results.
3. Inspect the event details with `GET /v1/notifications/webhooks-events/{event_id}`.
4. If the event exists but was not received, call `POST /v1/notifications/webhooks-events/{event_id}/resend` to redeliver it.
5. If no events appear, verify your webhook is active with `GET /v1/notifications/webhooks/{webhook_id}` and check that the correct event types are subscribed.

### 4. Update Webhook Configuration

1. Call `GET /v1/notifications/webhooks/{webhook_id}` to review the current configuration.
2. Call `PATCH /v1/notifications/webhooks/{webhook_id}` with the fields to update (URL, event types, or both).
3. Confirm the update by inspecting the response's `url` and `event_types`.
4. Call `POST /v1/notifications/simulate-event` targeting the updated webhook to validate the new configuration.

### 5. Clean Up Unused Webhooks and Lookups

1. Call `GET /v1/notifications/webhooks` to list all registered webhooks.
2. Identify webhooks that are no longer needed (dead URLs, old integrations).
3. Call `DELETE /v1/notifications/webhooks/{webhook_id}` for each one (expect 204 No Content).
4. Call `GET /v1/notifications/webhooks-lookup` to review any webhook lookups.
5. Call `DELETE /v1/notifications/webhooks-lookup/{webhook_lookup_id}` to remove stale lookups.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
