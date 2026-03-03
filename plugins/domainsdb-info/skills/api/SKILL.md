---
name: domains-index-api
description: "Domains-Index API skill. Use when working with Domains-Index for domains, info. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# Domains-Index API
API version: 1.0

## Auth
ApiKey api_key in query

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /domains/search -- verify access

## Endpoints

14 endpoints across 2 groups. See references/api-spec.lap for full details.

### domains
| Method | Path | Description |
|--------|------|-------------|
| GET | /domains/search | Domains Database Search |
| GET | /domains/tld/{zone_id} | Get TLD records |
| GET | /domains/tld/{zone_id}/download | Download Whole Dataset for TLD |
| GET | /domains/tld/{zone_id}/search | Domains Search for TLD |
| GET | /domains/updates/added | Get added domains, latest if date not specified |
| GET | /domains/updates/added/download | Download added domains, latest if date not specified |
| GET | /domains/updates/deleted | Get deleted domains, latest if date not specified |
| GET | /domains/updates/deleted/download | Download deleted domains, latest if date not specified |
| GET | /domains/updates/list | List of updates |

### info
| Method | Path | Description |
|--------|------|-------------|
| GET | /info/api |  |
| GET | /info/stat/ | Returns overall stagtistics |
| GET | /info/stat/{zone} | Returns statistics for specific zone |
| GET | /info/tld/ | Returns overall Tld info |
| GET | /info/tld/{zone} | Returns statistics for specific zone |

## Enhanced Skill Content
## Question Mapping

- "Search for domains matching a keyword?" -> GET /domains/search
- "List all domains under a specific TLD like .com?" -> GET /domains/tld/{zone_id}
- "Download the full zone file for a TLD?" -> GET /domains/tld/{zone_id}/download
- "Search within a specific TLD for domains with certain DNS records?" -> GET /domains/tld/{zone_id}/search
- "What new domains were registered recently?" -> GET /domains/updates/added
- "Download a bulk list of newly added domains?" -> GET /domains/updates/added/download
- "Which domains were deleted or dropped recently?" -> GET /domains/updates/deleted
- "Download all recently deleted domains in bulk?" -> GET /domains/updates/deleted/download
- "What dates have domain update snapshots available?" -> GET /domains/updates/list
- "Check my API key status and usage info?" -> GET /info/api
- "Get overall statistics for the domain index?" -> GET /info/stat/
- "How many domains are registered under .io?" -> GET /info/stat/{zone}
- "List all supported TLDs?" -> GET /info/tld/
- "Get detailed info about a specific TLD zone?" -> GET /info/tld/{zone}
- "Find dead domains in a specific country under .com?" -> GET /domains/tld/{zone_id}/search (with isDead and country params)

## Response Tips

- **Domain listing endpoints** (`/domains/search`, `/domains/tld/*`, `/domains/updates/*`): Results are paginated via `page` and `limit` params. Always check if more pages exist by comparing returned count against `limit`.
- **Download endpoints** (`*/download`): Return bulk data (likely CSV or zone file format), not JSON. No pagination -- the full dataset for the given date is returned. Expect large payloads.
- **Info endpoints** (`/info/*`): Return metadata objects. `/info/stat/` and `/info/tld/` support pagination for long lists; individual zone lookups (`/info/stat/{zone}`, `/info/tld/{zone}`) return a single record or 404.
- **Error 403**: API key is missing, invalid, or rate-limited. Check `api_key` query parameter.
- **Error 404**: The requested zone, date snapshot, or resource does not exist. Verify zone IDs against `/info/tld/`.

## Anomaly Flags

- **403 on previously working requests**: API key may have been revoked or quota exhausted. Surface immediately and suggest checking `/info/api`.
- **Empty result sets on broad searches**: The `date` parameter may reference a snapshot that doesn't exist. Suggest calling `/domains/updates/list` to verify available dates.
- **Unexpected isDead values**: If filtering for live domains still returns dead ones (or vice versa), flag potential data staleness tied to the snapshot date.
- **Large page counts without limit**: If `limit` is omitted, default page size may be small. Flag when total results likely exceed thousands and suggest bulk download endpoints instead.
- **404 on TLD zone endpoints**: The zone_id may not match the registry's naming. Proactively suggest `/info/tld/` to list valid zone identifiers.

## Playbook

### 1. Find Available Expired Domains in a TLD

1. Call `GET /info/tld/` to list all supported TLDs and pick your target zone.
2. Call `GET /domains/updates/deleted?date={recent_date}&limit=100` to see recently dropped domains.
3. Filter results by zone or use `GET /domains/tld/{zone_id}/search?isDead=true&date={date}` for TLD-specific dead domains.
4. Cross-reference with DNS records (A, NS params) to confirm the domain is truly unresolvable.

### 2. Monitor New Domain Registrations Daily

1. Call `GET /domains/updates/list` to get the list of available snapshot dates.
2. Pick the most recent date and call `GET /domains/updates/added?date={date}&page=1&limit=100`.
3. Page through results incrementing `page` until fewer than `limit` results return.
4. For bulk ingestion, use `GET /domains/updates/added/download?date={date}` instead.

### 3. Audit DNS Records for a TLD

1. Call `GET /info/tld/{zone}` to confirm the zone exists and get metadata.
2. Call `GET /domains/tld/{zone_id}/search?A={ip_address}` to find domains pointing to a specific IP.
3. Narrow with `MX`, `NS`, `CNAME`, or `TXT` params to audit specific record types.
4. Use `country` param to scope results geographically if needed.

### 4. Export Full Zone Data for Analysis

1. Call `GET /domains/updates/list` to find available snapshot dates.
2. Call `GET /domains/tld/{zone_id}/download?date={date}` to download the complete zone file.
3. If the download fails with 404, verify the zone_id via `GET /info/tld/` and try an earlier date.
4. Compare two date snapshots to compute domain additions and deletions yourself.

### 5. Get a Statistical Overview of the Domain Landscape

1. Call `GET /info/stat/` with pagination to retrieve per-TLD domain counts.
2. For a specific TLD breakdown, call `GET /info/stat/{zone}`.
3. Call `GET /info/tld/` to get the full list of tracked zones and their metadata.
4. Combine with `GET /info/api` to check your remaining API quota before running heavy queries.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
