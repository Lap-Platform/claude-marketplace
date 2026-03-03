---
name: ticketmaster-publish-api
description: "ticketmaster publish API skill. Use when working with ticketmaster publish for publish. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# ticketmaster publish api
API version: v2

## Auth
No authentication required.

## Base URL
https://www.ticketmaster.com/publish/v2

## Setup
1. No auth setup needed
3. POST /publish/v2/attractions -- create first attractions

## Endpoints

10 endpoints across 1 groups. See references/api-spec.lap for full details.

### publish
| Method | Path | Description |
|--------|------|-------------|
| POST | /publish/v2/attractions | Publish an attractions |
| PATCH | /publish/v2/attractions/{id} | Publish a patch on an attraction |
| POST | /publish/v2/attractions/{id}/videos | Publish a video on an attraction |
| POST | /publish/v2/entitlements | Publish entitlements on an entity |
| POST | /publish/v2/events | Publish an event |
| PATCH | /publish/v2/events/{id} | Publish a patch on an event |
| POST | /publish/v2/events/{id}/videos | Publish a video on an event |
| POST | /publish/v2/extensions | Publish extension on an entity |
| POST | /publish/v2/venues | Publish a venue |
| PATCH | /publish/v2/venues/{id} | Publish a patch on a venue |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new attraction?" -> POST /publish/v2/attractions
- "How do I update an existing attraction?" -> PATCH /publish/v2/attractions/{id}
- "How do I add a video to an attraction?" -> POST /publish/v2/attractions/{id}/videos
- "How do I publish a new event?" -> POST /publish/v2/events
- "How do I update event details?" -> PATCH /publish/v2/events/{id}
- "How do I attach a video to an event?" -> POST /publish/v2/events/{id}/videos
- "How do I register a new venue?" -> POST /publish/v2/venues
- "How do I update venue information?" -> PATCH /publish/v2/venues/{id}
- "How do I create an entitlement?" -> POST /publish/v2/entitlements
- "How do I add extensions to enrich entity data?" -> POST /publish/v2/extensions
- "How do I set up a full event with a new venue and attraction?" -> POST /publish/v2/venues, then POST /publish/v2/attractions, then POST /publish/v2/events
- "How do I change the name or details of a venue after creation?" -> PATCH /publish/v2/venues/{id}
- "How do I add promotional videos to both an event and its headlining attraction?" -> POST /publish/v2/attractions/{id}/videos + POST /publish/v2/events/{id}/videos

## Response Tips

- **All endpoints** return 200 on success; non-200 likely indicates validation failure or auth error -- check the response body for error details.
- **Create endpoints (POST)** return a `data` map containing the created entity with its assigned `id` -- capture this for subsequent PATCH or video calls.
- **Update endpoints (PATCH)** return the merged entity in `data` -- compare against your request to confirm which fields were accepted.
- **Video endpoints** return confirmation in `data` -- verify the video reference was attached by checking the response payload.
- **Correlation tracking**: Every response includes `TMPS-Correlation-Id` -- log this value for debugging and support escalations.

## Anomaly Flags

- **Missing `TMPS-Correlation-Id`** in a response: indicates a proxy or gateway issue upstream -- surface immediately as it breaks traceability.
- **Non-200 on any endpoint**: since every endpoint is documented as returning 200, any other status (401, 403, 422, 429, 5xx) is noteworthy -- surface the status code, correlation ID, and response body.
- **PATCH returning unchanged data**: if the response `data` matches the pre-update state, warn that the update may not have been applied (possible read-only or locked entity).
- **Empty `data` map in response**: flag as unexpected -- all create/update operations should return the resulting entity.
- **Rate limiting signals**: watch for 429 status or `Retry-After` headers and surface the wait time before retrying.
- **Video endpoints failing after entity creation succeeds**: may indicate the entity is in a pending/draft state that does not yet accept media attachments.

## Playbook

### 1. Publish a Complete Event (Venue + Attraction + Event)

1. POST /publish/v2/venues with venue details (name, address, capacity) -- capture the returned venue `id`
2. POST /publish/v2/attractions with attraction details (artist/team name, genre) -- capture the returned attraction `id`
3. POST /publish/v2/events with event details, referencing the venue `id` and attraction `id`
4. Confirm the event `id` in the response and log the `TMPS-Correlation-Id` for each call

### 2. Update an Existing Event and Add Promo Video

1. PATCH /publish/v2/events/{id} with the fields to change (e.g., date, description, pricing)
2. Verify the response `data` reflects the updates
3. POST /publish/v2/events/{id}/videos with the video payload (URL, title, type)
4. Confirm the video attachment in the response

### 3. Enrich an Attraction with Videos and Extensions

1. POST /publish/v2/attractions/{id}/videos to attach one or more videos to the attraction
2. POST /publish/v2/extensions to add supplementary data (custom attributes, metadata) linked to the attraction
3. Verify both responses return 200 with populated `data`

### 4. Bulk Venue Onboarding

1. For each venue: POST /publish/v2/venues with venue details
2. Capture the returned `id` from each response into a mapping (venue name -> id)
3. If any venue needs corrections: PATCH /publish/v2/venues/{id} with the fixes
4. Log all `TMPS-Correlation-Id` values for audit trail

### 5. Entitlement Setup for Access Control

1. POST /publish/v2/entitlements with the entitlement rules (entity references, access scope)
2. Confirm the response returns the created entitlement with its `id`
3. Reference the entitlement `id` when creating or updating events that require gated access


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
