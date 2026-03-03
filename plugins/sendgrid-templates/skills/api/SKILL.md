---
name: twilio-sendgrid-templates-api
description: "Twilio SendGrid Templates API skill. Use when working with Twilio SendGrid Templates for templates. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# Twilio SendGrid Templates API
API version: 1.0.0

## Auth
Bearer bearer

## Base URL
https://api.sendgrid.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v3/templates -- verify access
3. POST /v3/templates -- create first templates

## Endpoints

11 endpoints across 1 groups. See references/api-spec.lap for full details.

### templates
| Method | Path | Description |
|--------|------|-------------|
| POST | /v3/templates | Create a transactional template. |
| GET | /v3/templates | Retrieve paged transactional templates. |
| POST | /v3/templates/{template_id} | Duplicate a transactional template. |
| GET | /v3/templates/{template_id} | Retrieve a single transactional template. |
| PATCH | /v3/templates/{template_id} | Edit a transactional template. |
| DELETE | /v3/templates/{template_id} | Delete a template. |
| POST | /v3/templates/{template_id}/versions | Create a new transactional template version. |
| GET | /v3/templates/{template_id}/versions/{version_id} | Retrieve a specific transactional template version. |
| PATCH | /v3/templates/{template_id}/versions/{version_id} | Edit a transactional template version. |
| DELETE | /v3/templates/{template_id}/versions/{version_id} | Delete a transactional template version. |
| POST | /v3/templates/{template_id}/versions/{version_id}/activate | Activate a transactional template version. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new email template?" -> POST /v3/templates
- "List all my SendGrid templates" -> GET /v3/templates
- "How do I find a specific template by ID?" -> GET /v3/templates/{template_id}
- "How do I rename a template?" -> PATCH /v3/templates/{template_id}
- "How do I delete a template?" -> DELETE /v3/templates/{template_id}
- "How do I add a new version to a template?" -> POST /v3/templates/{template_id}/versions
- "How do I update the HTML content of a template version?" -> PATCH /v3/templates/{template_id}/versions/{version_id}
- "How do I activate a specific template version?" -> POST /v3/templates/{template_id}/versions/{version_id}/activate
- "How do I get the content of a template version?" -> GET /v3/templates/{template_id}/versions/{version_id}
- "How do I delete a template version?" -> DELETE /v3/templates/{template_id}/versions/{version_id}
- "How do I create a dynamic template instead of a legacy one?" -> POST /v3/templates (with `generation: "dynamic"`)
- "How do I paginate through all my templates?" -> GET /v3/templates (using `page_token` from `_metadata.next`)
- "How do I duplicate a template?" -> GET /v3/templates/{template_id} then POST /v3/templates + POST /v3/templates/{new_id}/versions
- "How do I act on behalf of a subuser?" -> Any endpoint with the `on-behalf-of` header

## Response Tips

- **Template CRUD** (POST/GET/PATCH /v3/templates/...): Returns a `versions` array nested inside the template object; each version has its own `id` separate from the template `id`. Check the `warning` map for deprecation or validation notices.
- **Template listing** (GET /v3/templates): Paginated via `_metadata` -- use `_metadata.next` URI as the `page_token` for the next page. `page_size` is required. `_metadata.count` gives total results.
- **Version endpoints**: Return flat objects with both `id` (version ID) and `template_id` (parent). `active` is an integer (0 or 1), not a boolean. `plain_content` auto-generates from `html_content` when `generate_plain_content` is true.
- **DELETE endpoints**: Return 204 with no body -- treat any 2xx as success.
- **Errors**: 400 on listing indicates invalid query parameters (bad `page_size` or `generations` value).

## Anomaly Flags

- **Warning fields present**: Both template and version responses include `warning`/`warnings` maps -- surface these immediately as they may indicate deprecated features or content issues.
- **Legacy vs dynamic generation**: Flag if a user creates a template with `generation: "legacy"` since SendGrid recommends dynamic templates for new work.
- **Inactive version edits**: Alert when a user edits a version where `active: 0` without following up with an activate call -- the changes won't take effect in sends.
- **Missing HTML content**: Flag if a version is created/updated without `html_content`, as this may result in empty emails.
- **Pagination exhaustion**: Warn when `_metadata.next` is null (no more pages) to prevent unnecessary follow-up requests.
- **On-behalf-of misuse**: Surface a notice when the `on-behalf-of` header is set, confirming the action is being performed as a subuser.

## Playbook

### 1. Create a dynamic template with an initial version

1. POST /v3/templates with `{ "name": "Welcome Email", "generation": "dynamic" }`
2. Capture the returned `id` as `template_id`
3. POST /v3/templates/{template_id}/versions with `{ "name": "v1", "subject": "Welcome!", "html_content": "<html>...</html>", "editor": "code" }`
4. The version is created inactive by default (`active: 0`)
5. POST /v3/templates/{template_id}/versions/{version_id}/activate to make it live

### 2. Update a live template safely

1. GET /v3/templates/{template_id} to see all versions and identify the active one
2. POST /v3/templates/{template_id}/versions to create a new version with updated content (keeps the old active version as a rollback)
3. GET /v3/templates/{template_id}/versions/{new_version_id} to verify content looks correct
4. POST /v3/templates/{template_id}/versions/{new_version_id}/activate to switch traffic to the new version

### 3. List and export all templates

1. GET /v3/templates with `page_size=50&generations=dynamic` (or `legacy,dynamic` for all)
2. Read `_metadata.next` from the response
3. Loop: GET /v3/templates with `page_token={next}` until `_metadata.next` is null
4. For each template, GET /v3/templates/{template_id} to retrieve full version details including HTML content

### 4. Clean up unused templates

1. GET /v3/templates with `page_size=50&generations=dynamic,legacy` and iterate all pages
2. For each template, check `versions` array -- if empty or all versions have `active: 0`, flag as candidate
3. GET /v3/templates/{template_id} for the full version list to confirm
4. DELETE /v3/templates/{template_id}/versions/{version_id} for each version first
5. DELETE /v3/templates/{template_id} to remove the template itself

### 5. Roll back to a previous template version

1. GET /v3/templates/{template_id} to list all versions
2. Identify the desired previous version by `updated_at` timestamp or `name`
3. POST /v3/templates/{template_id}/versions/{old_version_id}/activate to reactivate it
4. Verify `active: 1` in the response to confirm the rollback succeeded


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
