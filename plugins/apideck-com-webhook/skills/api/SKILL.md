---
name: webhook-api
description: "Webhook API skill. Use when working with Webhook for webhook. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# Webhook API
API version: 10.24.0

## Auth
ApiKey Authorization in header

## Base URL
https://unify.apideck.com

## Setup
1. Set your API key in the appropriate header
2. GET /webhook/webhooks -- verify access
3. POST /webhook/webhooks -- create first webhooks

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### webhook
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhook/webhooks | List webhook subscriptions |
| POST | /webhook/webhooks | Create webhook subscription |
| GET | /webhook/webhooks/{id} | Get webhook subscription |
| PATCH | /webhook/webhooks/{id} | Update webhook subscription |
| DELETE | /webhook/webhooks/{id} | Delete webhook subscription |
| POST | /webhook/webhooks/{id}/execute/{serviceId} | Execute a webhook |
| POST | /webhook/webhooks/{id}/x/{serviceId} | Execute a webhook |
| POST | /webhook/w/{id}/{serviceId} | Resolve and Execute a connection webhook |
| GET | /webhook/w/{id}/{serviceId} | Resolve and Execute a connection webhook |
| GET | /webhook/logs | List event logs |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my webhooks?" -> GET /webhook/webhooks
- "How do I create a new webhook for CRM events?" -> POST /webhook/webhooks
- "How do I get details for a specific webhook?" -> GET /webhook/webhooks/{id}
- "How do I update a webhook's delivery URL?" -> PATCH /webhook/webhooks/{id}
- "How do I disable a webhook without deleting it?" -> PATCH /webhook/webhooks/{id}
- "How do I delete a webhook?" -> DELETE /webhook/webhooks/{id}
- "How do I manually trigger a webhook for a specific service?" -> POST /webhook/webhooks/{id}/execute/{serviceId}
- "How do I execute a webhook with a shorter URL?" -> POST /webhook/w/{id}/{serviceId}
- "How do I check webhook execution logs?" -> GET /webhook/logs
- "How do I paginate through all my webhooks?" -> GET /webhook/webhooks (use cursor param)
- "How do I filter webhook logs for a specific time period?" -> GET /webhook/logs (use filter param)
- "How do I change which events a webhook listens to?" -> PATCH /webhook/webhooks/{id}
- "How do I validate an incoming webhook callback?" -> GET /webhook/w/{id}/{serviceId} or POST /webhook/w/{id}/{serviceId} (with validationToken)
- "How do I set up a webhook for my accounting integration?" -> POST /webhook/webhooks (unified_api: "accounting")

## Response Tips

- **List endpoints** (GET /webhooks, GET /logs): Paginated via cursor-based navigation. Check `meta.cursors.next` for more pages; follow `links.next` URL. Default page size is 20.
- **Single resource endpoints** (GET/PATCH/DELETE /webhooks/{id}): Response `data` is a single map, not an array. Always check `status` field for confirmation.
- **Create endpoint** (POST /webhooks): Returns 201, not 200. The returned `data` includes the generated `id` you need for future operations.
- **Execute endpoints** (POST /execute, POST /x, POST|GET /w): Return a flat response with `request_id` and `timestamp` instead of a `data` object. Use `request_id` to correlate with logs.
- **Errors**: All endpoints share the same error codes (400, 401, 402, 404, 422). A 402 indicates a payment/plan issue, not just auth. A 422 means the request body was syntactically valid but semantically wrong (bad enum value, missing required field).

## Anomaly Flags

- **Webhook disabled unexpectedly**: If `status` is `disabled` and `disabled_reason` is populated, surface this immediately -- the platform may have auto-disabled due to delivery failures.
- **402 Payment Required**: Flag when any call returns 402 -- this suggests a plan limit or billing issue, not a transient error.
- **Empty events array**: Warn if a webhook is created or updated with an empty `events` list, as it will receive no notifications.
- **Stale webhooks**: When listing webhooks, flag any where `updated_at` is significantly old and `status` is `enabled` -- they may be orphaned.
- **Pagination exhaustion**: If `meta.cursors.next` is null on the first page and `items_on_page` equals the limit, warn that results may be exactly at the boundary.
- **Missing x-apideck-app-id**: Most endpoints require this header. Surface a clear message if a 400/401 error likely stems from its absence.

## Playbook

### 1. Set Up a New Webhook for CRM Events

1. Call POST /webhook/webhooks with `unified_api: "crm"`, `status: "enabled"`, `delivery_url` set to your endpoint, and `events` listing the CRM events you care about (e.g., `["crm.contacts.created", "crm.deals.updated"]`).
2. Note the returned `data.id` and `data.execute_base_url`.
3. Verify the webhook was created by calling GET /webhook/webhooks/{id} with the returned ID.
4. Test delivery by calling POST /webhook/webhooks/{id}/execute/{serviceId} with your CRM service ID.
5. Check GET /webhook/logs to confirm the test event was delivered successfully.

### 2. Debug a Failing Webhook

1. Call GET /webhook/webhooks/{id} to check the webhook's `status` and `disabled_reason`.
2. If `status` is `disabled`, review `disabled_reason` for the cause (e.g., repeated delivery failures).
3. Call GET /webhook/logs with a `filter` scoped to recent entries to find failed deliveries.
4. Fix the delivery endpoint issue, then re-enable the webhook via PATCH /webhook/webhooks/{id} with `status: "enabled"`.
5. Trigger a test execution with POST /webhook/webhooks/{id}/execute/{serviceId} and verify in logs.

### 3. Rotate a Webhook Delivery URL

1. Call GET /webhook/webhooks/{id} to confirm the current `delivery_url` and `events`.
2. Call PATCH /webhook/webhooks/{id} with the new `delivery_url`.
3. Verify the update by calling GET /webhook/webhooks/{id} and confirming `delivery_url` changed.
4. Trigger a test with POST /webhook/webhooks/{id}/execute/{serviceId} to validate the new endpoint receives events.

### 4. Audit All Active Webhooks

1. Call GET /webhook/webhooks with `limit: 20`.
2. If `meta.cursors.next` is present, continue paginating with `cursor` set to that value until all pages are retrieved.
3. Filter results client-side: flag any with `status: "disabled"`, empty `events` arrays, or stale `updated_at` timestamps.
4. For each suspicious webhook, call GET /webhook/webhooks/{id} for full details.
5. Clean up orphaned webhooks with DELETE /webhook/webhooks/{id} as needed.

### 5. Handle Webhook Validation Callbacks

1. When the external service sends a validation request, it hits GET or POST /webhook/w/{id}/{serviceId}.
2. For POST validation, include the `validationToken` parameter from the incoming request.
3. The endpoint returns a 200 with `status_code`, `status`, and `timestamp` confirming the validation.
4. Verify the webhook is now fully active by calling GET /webhook/webhooks/{id} and checking `status: "enabled"`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
