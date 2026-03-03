---
name: enterobase-api
description: "Enterobase-API API skill. Use when working with Enterobase-API for api. Covers 30 endpoints."
version: 1.0.0
generator: lapsh
---

# Enterobase-API
API version: v2.0

## Auth
basic

## Base URL
Not specified.

## Setup
1. Configure auth: basic
2. GET /api/v2.0 -- verify access
3. POST /api/v2.0/lookup/{barcode} -- create first lookup

## Endpoints

30 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| GET | /api/v2.0 | Top level information about EnteroBase databases |
| GET | /api/v2.0/login | Login endpoint, refresh your API token |
| GET | /api/v2.0/lookup | Generic endpoint for lookup list of barcodes |
| GET | /api/v2.0/lookup/{barcode} | Generic endpoint for lookup of barcodes |
| POST | /api/v2.0/lookup/{barcode} | Generic endpoint for lookup of barcodes |
| GET | /api/v2.0/{database}/AMRdata | AMR data |
| GET | /api/v2.0/{database}/AMRdata/{barcode} | AMR data |
| POST | /api/v2.0/{database}/AMRdata/{barcode} | AMR data |
| PUT | /api/v2.0/{database}/AMRdata/{barcode} | AMR data |
| GET | /api/v2.0/{database}/assemblies | Genome assemblies |
| GET | /api/v2.0/{database}/assemblies/{barcode} | Genome assemblies |
| POST | /api/v2.0/{database}/assemblies/{barcode} | Genome assemblies |
| PUT | /api/v2.0/{database}/assemblies/{barcode} | Genome assemblies |
| GET | /api/v2.0/{database}/schemes | Genotyping schemes |
| GET | /api/v2.0/{database}/schemes/{barcode} | Genotyping schemes |
| POST | /api/v2.0/{database}/schemes/{barcode} | Genotyping schemes |
| PUT | /api/v2.0/{database}/schemes/{barcode} | Genotyping schemes |
| GET | /api/v2.0/{database}/straindata | Strain data |
| GET | /api/v2.0/{database}/strains | Strain metadata |
| GET | /api/v2.0/{database}/strains/{barcode} | Strain metadata |
| POST | /api/v2.0/{database}/strains/{barcode} | Strain metadata |
| PUT | /api/v2.0/{database}/strains/{barcode} | Strain metadata |
| GET | /api/v2.0/{database}/strainsversion | Strain previous metadata |
| GET | /api/v2.0/{database}/traces | Traces (sequence-reads) metadata |
| GET | /api/v2.0/{database}/traces/{barcode} | Traces (sequence-reads) metadata |
| POST | /api/v2.0/{database}/traces/{barcode} | Traces (sequence-reads) metadata |
| PUT | /api/v2.0/{database}/traces/{barcode} | Traces (sequence-reads) metadata |
| GET | /api/v2.0/{database}/{scheme}/alleles | Alleles  data |
| GET | /api/v2.0/{database}/{scheme}/loci | Loci |
| GET | /api/v2.0/{database}/{scheme}/sts | ST profile data |

## Enhanced Skill Content
## Question Mapping

- "What databases are available in Enterobase?" -> GET /api/v2.0
- "How do I authenticate with the Enterobase API?" -> GET /api/v2.0/login
- "Look up a sample by its barcode" -> GET /api/v2.0/lookup/{barcode}
- "List all strains in the Salmonella database from Germany" -> GET /api/v2.0/{database}/strains
- "Get antimicrobial resistance data for a specific isolate" -> GET /api/v2.0/{database}/AMRdata/{barcode}
- "Find assemblies with N50 above a threshold in a database" -> GET /api/v2.0/{database}/assemblies
- "What MLST schemes exist for this organism database?" -> GET /api/v2.0/{database}/schemes
- "Retrieve allele sequences for a specific locus in a scheme" -> GET /api/v2.0/{database}/{scheme}/alleles
- "Get the sequence type (ST) profile for a strain" -> GET /api/v2.0/{database}/{scheme}/sts
- "Update metadata for a strain I uploaded" -> PUT /api/v2.0/{database}/strains/{barcode}
- "Submit new AMR data for an isolate" -> POST /api/v2.0/{database}/AMRdata/{barcode}
- "List all trace data (raw reads) for a database" -> GET /api/v2.0/{database}/traces
- "Search strains by geographic coordinates (lat/long)" -> GET /api/v2.0/{database}/strains
- "Get strain data including custom fields for my submissions" -> GET /api/v2.0/{database}/straindata
- "Check the version history of strain records" -> GET /api/v2.0/{database}/strainsversion

## Response Tips

- **Listing endpoints** (strains, assemblies, AMRdata, traces, schemes, alleles, loci, sts): Paginated via `offset` and `limit` params. Always check if result count equals `limit` to determine if more pages exist. Use `only_fields` to reduce payload size.
- **Single-record endpoints** (GET by barcode): Return the full record object. Nested maps may contain variable fields depending on database and scheme context.
- **Auth/login**: A 403 on any endpoint means credentials are invalid or the session expired. Re-authenticate via `/login` before retrying.
- **Lookup**: The `/lookup` endpoint may return 408 (timeout) for slow barcode resolution. Retry with backoff.
- **Write endpoints** (POST/PUT): POST creates or appends data; PUT updates existing records. PUT endpoints do not document a 200 return, so confirm success by re-fetching the record.
- **Scheme-scoped endpoints** (alleles, loci, sts): Return 400 for invalid scheme or locus names in addition to 403 for auth failures. Validate scheme names via `/schemes` first.

## Anomaly Flags

- **403 on previously working requests**: Session likely expired. Proactively suggest re-authenticating via `/api/v2.0/login`.
- **408 timeout on lookup**: The barcode resolution service is slow or overloaded. Flag this and suggest retrying after a delay.
- **400 on scheme endpoints**: The scheme name or locus is invalid for the given database. Surface available schemes before the user retries.
- **Empty result sets with offset > 0**: Pagination has overshot. Flag that the user has iterated past all available records.
- **PUT without documented 200**: PUT endpoints lack explicit success response codes. Flag that write confirmation should be verified with a follow-up GET.
- **Large strain queries without `only_fields`**: Straindata has 30+ optional filter/return fields. Proactively suggest using `only_fields` and `limit` to avoid oversized responses.
- **Geospatial queries with missing coordinates**: If `latitude`/`longitude` filters return empty results, flag that not all strain records have coordinates populated.

## Playbook

### 1. Authenticate and explore a database

1. Call `GET /api/v2.0/login` with `username` and `password` to obtain a session token.
2. Call `GET /api/v2.0` to list available databases (filter by `name` or `prefix` if needed).
3. Pick a database (e.g., `senterica`) and call `GET /api/v2.0/{database}/schemes` to see available typing schemes.
4. Call `GET /api/v2.0/{database}/strains?limit=5` to preview strain records and understand the data shape.

### 2. Search strains by geography and time

1. Authenticate via `GET /api/v2.0/login`.
2. Call `GET /api/v2.0/{database}/strains` with `country`, `region`, or `city` plus `collection_year` or `collection_date` to filter.
3. Use `only_fields` to return just the columns you need (e.g., `barcode,strain_name,country,serotype`).
4. Paginate with `offset` and `limit` (e.g., `limit=100&offset=0`, then `offset=100`) until results are exhausted.
5. For coordinate-based searches, add `latitude` and `longitude` filters instead of named geography.

### 3. Retrieve full genomic context for an isolate

1. Look up the isolate: `GET /api/v2.0/lookup/{barcode}`.
2. Fetch strain metadata: `GET /api/v2.0/{database}/strains/{barcode}`.
3. Fetch assembly details: `GET /api/v2.0/{database}/assemblies?barcode={barcode}` (check `n50`, `assembly_status`).
4. Fetch AMR profile: `GET /api/v2.0/{database}/AMRdata/{barcode}`.
5. Fetch raw trace data: `GET /api/v2.0/{database}/traces?barcode={barcode}`.

### 4. Extract MLST allele profiles and sequence types

1. List schemes: `GET /api/v2.0/{database}/schemes` to find the scheme barcode/name (e.g., cgMLST or 7-gene MLST).
2. List loci in the scheme: `GET /api/v2.0/{database}/{scheme}/loci`.
3. Query STs: `GET /api/v2.0/{database}/{scheme}/sts?show_alleles=true&limit=50` to get ST profiles with allele assignments.
4. Retrieve specific allele sequences: `GET /api/v2.0/{database}/{scheme}/alleles?locus={locus_name}&allele_id={id}`.

### 5. Update strain metadata in bulk

1. Authenticate via `GET /api/v2.0/login`.
2. Query target strains: `GET /api/v2.0/{database}/strains?my_strains=true&only_fields=barcode,strain_name` to get barcodes of your submissions.
3. For each strain barcode, call `PUT /api/v2.0/{database}/strains/{barcode}` with the updated fields in the request body.
4. Verify each update by calling `GET /api/v2.0/{database}/strains/{barcode}` and confirming the changed fields.
5. If updating AMR data alongside, repeat with `PUT /api/v2.0/{database}/AMRdata/{barcode}` for each isolate.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
