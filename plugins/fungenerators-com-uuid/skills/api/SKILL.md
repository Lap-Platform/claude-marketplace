---
name: uuid-generation-api
description: "UUID Generation API skill. Use when working with UUID Generation for uuid. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# UUID Generation API
API version: 1.5

## Auth
ApiKey X-Fungenerators-Api-Secret in header

## Base URL
https://api.fungenerators.com

## Setup
1. Set your API key in the appropriate header
2. GET /uuid -- verify access
3. POST /uuid -- create first uuid

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### uuid
| Method | Path | Description |
|--------|------|-------------|
| GET | /uuid | Generate a random UUID (v4). |
| POST | /uuid | Parse a UUID string and return its version and check whether it is valid. |
| GET | /uuid/version/{version} | Generate a random UUID (v4). |

## Enhanced Skill Content
## Question Mapping

- "Generate a UUID?" -> GET /uuid
- "Generate multiple UUIDs at once?" -> GET /uuid?limit=5
- "Is this a valid UUID?" -> POST /uuid
- "What version is this UUID?" -> POST /uuid
- "Parse a UUID string?" -> POST /uuid
- "Generate a v4 random UUID?" -> GET /uuid/version/4
- "Generate a v1 timestamp-based UUID?" -> GET /uuid/version/1
- "Generate a v5 name-based UUID from a string?" -> GET /uuid/version/5?text=myvalue
- "Generate a v3 UUID with MD5 hashing?" -> GET /uuid/version/3?text=myvalue
- "Generate 10 UUIDs of a specific version?" -> GET /uuid/version/4?limit=10
- "What UUID versions are available?" -> GET /uuid/version/1 through /5 (try each)
- "Generate a UUID and then validate it?" -> GET /uuid then POST /uuid with the result
- "Batch generate v4 UUIDs for database seeding?" -> GET /uuid/version/4?limit={count}

## Response Tips

- **UUID generation (GET)**: Response contains generated UUID(s); when `limit` > 1, expect an array. Check the `contents` or `data` wrapper object for results.
- **UUID validation (POST)**: Returns parsed UUID components (version, variant, timestamp if applicable). A 200 does not always mean valid -- check the response body for validation details.
- **Versioned generation (GET /version)**: The `type` and `text` params only apply to name-based versions (v3/v5); they are ignored for v1/v4. Omitting `text` for v3/v5 may return an error or default namespace UUID.
- **All endpoints**: 401 means missing or invalid `X-Fungenerators-Api-Secret` header. No pagination -- use `limit` to control batch size.

## Anomaly Flags

- **401 on any call**: API key is missing, expired, or malformed. Surface immediately and prompt user to check `X-Fungenerators-Api-Secret`.
- **Unexpected UUID version in response**: If the returned UUID version does not match the requested version path parameter, flag the mismatch.
- **Large limit values**: API may silently cap the `limit` parameter. If fewer results return than requested, warn the user.
- **Name-based version without text**: Calling `/uuid/version/3` or `/uuid/version/5` without the `text` parameter may produce errors or meaningless output -- flag if the user omits it.
- **Non-standard status codes**: Any response outside 200/401 (e.g., 429, 500, 503) should be surfaced as a possible rate limit or service outage.

## Playbook

### Generate and Validate a UUID

1. Call `GET /uuid` to generate a single UUID.
2. Extract the UUID string from the response.
3. Call `POST /uuid` with `uuidstr` set to the generated value.
4. Inspect the parsed response for version, variant, and timestamp fields.

### Batch Generate UUIDs for a Specific Version

1. Determine the desired UUID version (1 for timestamp, 4 for random, 3/5 for name-based).
2. Call `GET /uuid/version/{version}?limit={count}`.
3. For v3 or v5, include `text=<your-input-string>` to seed the UUID.
4. Collect the array of UUIDs from the response body.

### Validate an Externally Provided UUID

1. Receive or prompt for the UUID string from the user.
2. Call `POST /uuid` with `uuidstr` set to the provided string.
3. Check the response for version info, validity, and parsed components.
4. Report back the UUID version, variant, and whether it is well-formed.

### Compare UUID Versions Side by Side

1. Call `GET /uuid/version/1` to generate a v1 (timestamp) UUID.
2. Call `GET /uuid/version/4` to generate a v4 (random) UUID.
3. Call `POST /uuid` on each result to parse their components.
4. Present the structural differences (timestamp presence, node ID, randomness).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
