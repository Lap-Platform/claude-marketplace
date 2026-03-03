---
name: zeit-api
description: "ZEIT API skill. Use when working with ZEIT for integrations, domains. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# ZEIT API
API version: v2019-01-07

## Auth
Bearer bearer | OAuth2

## Base URL
https://api.zeit.co

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/integrations/webhooks -- verify access
3. POST /v1/integrations/webhooks -- create first webhooks

## Endpoints

5 endpoints across 2 groups. See references/api-spec.lap for full details.

### integrations
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/integrations/webhooks | Get a list of existent webhooks |
| POST | /v1/integrations/webhooks | Create a new webhook |
| DELETE | /v1/integrations/webhooks/:id | Remove a webhook by id |

### domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /v4/domains | Gets a list of domains registered for the authenticating user. |
| GET | /v4/domains/{name} | Get a domain for the authenticated user by name |

## Enhanced Skill Content
## Question Mapping

- "What webhooks do I have set up?" -> GET /v1/integrations/webhooks
- "Show me all my integration webhooks for a specific team" -> GET /v1/integrations/webhooks (with teamId)
- "Create a new webhook for my integration" -> POST /v1/integrations/webhooks
- "Register a webhook that posts to my Slack URL" -> POST /v1/integrations/webhooks
- "Delete a webhook I no longer need" -> DELETE /v1/integrations/webhooks/:id
- "Remove the webhook with ID abc123" -> DELETE /v1/integrations/webhooks/:id
- "List all my domains" -> GET /v4/domains
- "What domains does my team own?" -> GET /v4/domains (with teamId)
- "Get details about example.com" -> GET /v4/domains/{name}
- "Is my domain verified?" -> GET /v4/domains/{name} (check `verified` field)
- "When does my domain expire?" -> GET /v4/domains/{name} (check `expiresAt` field)
- "What nameservers should I point my domain to?" -> GET /v4/domains/{name} (check `intendedNameservers`)
- "Set up a webhook, then confirm it was created by listing all webhooks" -> POST /v1/integrations/webhooks + GET /v1/integrations/webhooks
- "Who registered this domain?" -> GET /v4/domains/{name} (check `creator` nested object)

## Response Tips

- **Webhooks (POST):** Returns the full webhook object on 201 including server-assigned `id`, `configurationId`, and `createdAt` timestamp. Save the `id` for later deletion.
- **Webhooks (DELETE):** Returns 204 with no body. Absence of an error means success.
- **Webhooks (GET):** Response structure is undocumented beyond 200 status. Expect an array or wrapper object containing webhook records.
- **Domains (list):** Returns `{ domains: [map] }`. Iterate the array; each entry is a domain summary object.
- **Domains (detail):** Returns `{ domain: map }` with deeply nested objects (`creator`, `aliases`, `certs`). Nullable timestamp fields (`boughtAt`, `expiresAt`, `orderedAt`, `transferredAt`) return `null` when not applicable.
- **Errors:** Domain detail returns 404 when the domain name is not found or not owned by the authenticated user. Other endpoints return standard HTTP error codes.

## Anomaly Flags

- **Domain not verified:** If `GET /v4/domains/{name}` returns `verified: false`, surface this immediately -- the domain may not be serving traffic correctly. Check `intendedNameservers` vs `nameservers` for mismatches.
- **Domain expiration approaching:** If `expiresAt` is within 30 days of the current date, warn the user proactively.
- **Null timestamps on domains:** If `boughtAt`, `transferredAt`, and `orderedAt` are all null, the domain may be in an unusual state (externally managed or pending setup).
- **CDN disabled:** If `cdnEnabled` is false, flag it as a potential performance concern.
- **Webhook creation returning unexpected events:** If the `events` array in the POST response is empty or contains event types the user did not expect, surface this for review.
- **404 on domain lookup:** Could mean a typo, domain was deleted, or the user lacks team-level access. Suggest checking the `teamId` parameter.
- **DNS verification incomplete:** If `nsVerifiedAt` or `txtVerifiedAt` is null while the domain exists, DNS propagation may still be in progress.

## Playbook

### 1. Set Up a New Integration Webhook

1. Call `POST /v1/integrations/webhooks` with `name` and target `url` (add `teamId` if team-scoped)
2. Save the returned `id` from the 201 response
3. Verify creation by calling `GET /v1/integrations/webhooks` and confirming the new webhook appears
4. Test the webhook by triggering a relevant event in your Vercel project

### 2. Audit and Clean Up Webhooks

1. Call `GET /v1/integrations/webhooks` to list all active webhooks
2. Review each webhook's `url` and `name` for relevance
3. For each stale or broken webhook, call `DELETE /v1/integrations/webhooks/:id`
4. Re-list with `GET /v1/integrations/webhooks` to confirm cleanup

### 3. Verify Domain DNS Configuration

1. Call `GET /v4/domains/{name}` with the domain in question
2. Compare `nameservers` (current) against `intendedNameservers` (expected)
3. Check `verified` field -- if false, DNS changes have not propagated yet
4. Check `nsVerifiedAt` and `txtVerifiedAt` for last successful verification timestamps
5. If mismatched, update DNS records at your registrar and re-check after propagation (typically 10-60 minutes)

### 4. Inventory All Domains and Their Status

1. Call `GET /v4/domains` to retrieve the full domain list (add `teamId` for team scope)
2. For each domain in the response array, note `name`, `verified`, and `expiresAt`
3. For any domain with `verified: false` or `expiresAt` approaching, call `GET /v4/domains/{name}` for full details
4. Flag domains with `cdnEnabled: false` or null verification timestamps for follow-up

### 5. Transfer Webhook to a New Endpoint URL

1. Call `GET /v1/integrations/webhooks` and locate the webhook by `name` or `id`
2. Call `DELETE /v1/integrations/webhooks/:id` to remove the old webhook
3. Call `POST /v1/integrations/webhooks` with the same `name` but the new `url`
4. Confirm the new webhook appears in `GET /v1/integrations/webhooks`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
