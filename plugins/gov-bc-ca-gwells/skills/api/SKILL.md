---
name: groundwater-wells-aquifers-and-registry-api
description: "Groundwater Wells, Aquifers and Registry API skill. Use when working with Groundwater Wells, Aquifers and Registry for aquifer-codes, aquifers, cities. Covers 24 endpoints."
version: 1.0.0
generator: lapsh
---

# Groundwater Wells, Aquifers and Registry API
API version: v1

## Auth
ApiKey JWT in header

## Base URL
https://apps.nrs.gov.bc.ca/gwells/api/v1/

## Setup
1. Set your API key in the appropriate header
2. GET /aquifer-codes/demand/ -- verify access

## Endpoints

24 endpoints across 9 groups. See references/api-spec.lap for full details.

### aquifer-codes
| Method | Path | Description |
|--------|------|-------------|
| GET | /aquifer-codes/demand/ | return a list of aquifer demand codes |
| GET | /aquifer-codes/materials/ | return a list of aquifer material codes |
| GET | /aquifer-codes/productivity/ | return a list of aquifer productivity codes |
| GET | /aquifer-codes/quality-concerns/ | return a list of quality concern codes |
| GET | /aquifer-codes/subtypes/ | return a list of aquifer subtype codes |
| GET | /aquifer-codes/vulnerability/ | return a list of aquifer vulnerability codes |
| GET | /aquifer-codes/water-use/ | return a list of water use codes |

### aquifers
| Method | Path | Description |
|--------|------|-------------|
| GET | /aquifers/ | return a list of aquifers |
| GET | /aquifers/names/ | List all aquifers in a simplified format |
| GET | /aquifers/{aquifer_id}/ | return details of aquifers |
| GET | /aquifers/{aquifer_id}/files | list files found for the aquifer identified in the uri |

### cities
| Method | Path | Description |
|--------|------|-------------|
| GET | /cities/drillers/ | returns a list of cities with a qualified, registered operator (driller or installer) |
| GET | /cities/installers/ | returns a list of cities with a qualified, registered operator (driller or installer) |

### config
| Method | Path | Description |
|--------|------|-------------|
| GET | /config | serves general configuration |

### drillers
| Method | Path | Description |
|--------|------|-------------|
| GET | /drillers/ | Returns a list of all person records |
| GET | /drillers/names/ | Search for a person in the Register |
| GET | /drillers/{person_guid}/files/ | list files found for the aquifer identified in the uri |

### keycloak
| Method | Path | Description |
|--------|------|-------------|
| GET | /keycloak | serves keycloak config |

### submissions
| Method | Path | Description |
|--------|------|-------------|
| GET | /submissions/options/ | Options required for submitting activity report forms |

### surveys
| Method | Path | Description |
|--------|------|-------------|
| GET | /surveys/ | returns a list of active surveys |

### wells
| Method | Path | Description |
|--------|------|-------------|
| GET | /wells/ | returns a list of wells |
| GET | /wells/tags/ | seach for wells by tag or owner |
| GET | /wells/{tag}/files | list files found for the well identified in the uri |
| GET | /wells/{well_tag_number} | Return well detail. |

## Enhanced Skill Content
## Question Mapping

- "What aquifers are in this area?" -> GET /aquifers/
- "Show me details for aquifer 123" -> GET /aquifers/{aquifer_id}/
- "Search for an aquifer by name" -> GET /aquifers/names/
- "What files are attached to aquifer 456?" -> GET /aquifers/{aquifer_id}/files
- "List all groundwater wells" -> GET /wells/
- "Get full details for well tag 12345" -> GET /wells/{well_tag_number}
- "What documents are associated with well 98765?" -> GET /wells/{tag}/files
- "Search for wells by tag number" -> GET /wells/tags/
- "Find a driller by name" -> GET /drillers/
- "What cities have registered drillers?" -> GET /cities/drillers/
- "What aquifer material types exist?" -> GET /aquifer-codes/materials/
- "What vulnerability classifications are available?" -> GET /aquifer-codes/vulnerability/
- "What water use codes does the system support?" -> GET /aquifer-codes/water-use/
- "What submission options are available for well reports?" -> GET /submissions/options/
- "What is the current API configuration?" -> GET /config

## Response Tips

- **Paginated lists** (wells, aquifers, drillers, aquifer-codes): All return `{count, next, previous, results}`. Use `next`/`previous` URIs directly for paging; `count` gives total records. Pass `limit` and `offset` to control page size.
- **Aquifer detail** (`/aquifers/{id}/`): Description fields come in pairs -- a code field (e.g., `demand`) and a human-readable companion (e.g., `demand_description`). Always display the `_description` variant to users.
- **Well detail** (`/wells/{tag}`): Deeply nested with embedded objects (`person_responsible`, `company_of_person_responsible`) and multiple array sets (`casing_set`, `screen_set`, `lithologydescription_set`). Parse set arrays as ordered construction records.
- **File endpoints** (`/files`): Return `{public, private}`. Private files require authenticated access; unauthenticated callers only see the `public` array.
- **Name search endpoints** (`/aquifers/names/`, `/drillers/names/`): Lightweight autocomplete responses -- use these for typeahead, not the full list endpoints.
- **Code lookups** (`/aquifer-codes/*`): Reference data that rarely changes. Cache aggressively and refresh only on config changes.

## Anomaly Flags

- **Decommissioned wells**: Surface proactively when `decommission_start_date` or `decommission_end_date` is populated, or `well_status` indicates decommission. Users may not realize a well is no longer active.
- **Missing coordinates**: Flag wells where `latitude`/`longitude` are null or zero -- common data quality issue that breaks mapping workflows.
- **Artesian conditions**: Alert when `artesian_flow` or `artesian_pressure` has non-null values, as these wells have special regulatory and safety implications.
- **Aquifer vulnerability**: When `vulnerability` is high or `aquifer_vulnerability_index` exceeds typical thresholds, surface this as a water quality risk indicator.
- **Pagination exhaustion**: Warn when `count` exceeds 10,000 records and the user is iterating without search filters -- suggest narrowing the query.
- **Private files present**: When `/files` returns a non-empty `private` array, note that additional documents exist behind authentication.
- **Missing person responsible**: Flag wells where `person_responsible` is null -- may indicate incomplete regulatory records.
- **JWT expiry**: Since auth is ApiKey JWT, surface reminders to check token validity before batch operations that could fail mid-run.

## Playbook

### 1. Profile a specific aquifer

1. GET `/aquifers/{aquifer_id}/` to retrieve full aquifer details (material, vulnerability, productivity, water use).
2. GET `/aquifer-codes/vulnerability/` and `/aquifer-codes/quality-concerns/` to decode the classification codes into human-readable labels.
3. GET `/aquifers/{aquifer_id}/files` to check for associated maps, studies, or reports.
4. GET `/wells/?search={aquifer_id}` to find all wells drawing from this aquifer. Page through results using `next`.

### 2. Look up a well and its construction history

1. GET `/wells/tags/?search={partial_tag}` to find the exact well tag number.
2. GET `/wells/{well_tag_number}` for the full record including construction dates, casing, screen, and lithology sets.
3. Inspect `lithologydescription_set` for geological layers and `casing_set`/`screen_set` for construction specs.
4. Check `person_responsible` and `company_of_person_responsible` for the driller on record.
5. GET `/wells/{tag}/files` for any attached completion reports or photos.

### 3. Find a driller and review their work

1. GET `/drillers/names/?search={name}` for quick name matching.
2. GET `/drillers/?search={name}` for the full driller record including `person_guid`.
3. GET `/drillers/{person_guid}/files/` to review certifications or compliance documents.
4. GET `/cities/drillers/` to see which cities this driller operates in.
5. GET `/wells/?search={driller_name}` to find wells they have drilled (cross-reference via `person_responsible`).

### 4. Bulk export wells with pagination

1. GET `/wells/?limit=100&offset=0` to fetch the first page.
2. Read `count` from the response to calculate total pages (`Math.ceil(count / 100)`).
3. Follow the `next` URI for each subsequent page until `next` is null.
4. For large datasets, add search filters (e.g., city, aquifer ID) to reduce total records before paginating.

### 5. Explore aquifer classification reference data

1. GET `/aquifer-codes/materials/` for aquifer material types (sand, gravel, bedrock, etc.).
2. GET `/aquifer-codes/subtypes/` for aquifer subtype classifications.
3. GET `/aquifer-codes/demand/` and `/aquifer-codes/water-use/` for demand and usage categories.
4. GET `/aquifer-codes/productivity/` for yield/productivity ratings.
5. GET `/aquifer-codes/quality-concerns/` and `/aquifer-codes/vulnerability/` for risk assessment codes.
6. Cache all code lookups locally and use them to enrich aquifer and well detail responses with human-readable labels.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
