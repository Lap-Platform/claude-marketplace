---
name: ingestion-api
description: "Ingestion API skill. Use when working with Ingestion for import, track, engage#profile-set. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# Ingestion API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://{region}.mixpanel.com

## Setup
1. No auth setup needed
2. GET /lookup-tables -- verify access
3. POST /import -- create first import

## Endpoints

20 endpoints across 19 groups. See references/api-spec.lap for full details.

### import
| Method | Path | Description |
|--------|------|-------------|
| POST | /import | Import Events |

### track
| Method | Path | Description |
|--------|------|-------------|
| POST | /track | Track Events |

### engage#profile-set
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-set | Set Property |

### engage#profile-set-once
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-set-once | Set Property Once |

### engage#profile-numerical-add
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-numerical-add | Increment Numerical Property |

### engage#profile-union
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-union | Union To List Property |

### engage#profile-list-append
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-list-append | Append to List Property |

### engage#profile-list-remove
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-list-remove | Remove from List Property |

### engage#profile-unset
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-unset | Delete Property |

### engage#profile-batch-update
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-batch-update | Update Multiple Profiles |

### engage#profile-delete
| Method | Path | Description |
|--------|------|-------------|
| POST | /engage#profile-delete | Delete Profile |

### groups#group-set
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups#group-set | Update Property |

### groups#group-set-once
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups#group-set-once | Set Property Once |

### groups#group-unset
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups#group-unset | Delete Property |

### groups#group-remove-from-list
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups#group-remove-from-list | Remove from List Property |

### groups#group-union
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups#group-union | Union To List Property |

### groups#group-batch-update
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups#group-batch-update | Batch Update Group Profiles |

### groups#group-delete
| Method | Path | Description |
|--------|------|-------------|
| POST | /groups#group-delete | Delete Group |

### lookup-tables
| Method | Path | Description |
|--------|------|-------------|
| GET | /lookup-tables | List Lookup Tables |
| PUT | /lookup-tables/{id} | Replace a Lookup Table |

## Enhanced Skill Content
## Question Mapping

- "How do I send events to Mixpanel?" -> POST /track
- "How do I bulk import historical events?" -> POST /import
- "How do I set properties on a user profile?" -> POST /engage#profile-set
- "How do I increment a numeric property like login count?" -> POST /engage#profile-numerical-add
- "How do I delete a user profile?" -> POST /engage#profile-delete
- "How do I add a tag to a profile list without duplicates?" -> POST /engage#profile-union
- "How do I remove a value from a profile list property?" -> POST /engage#profile-list-remove
- "How do I set profile properties only if they don't exist yet?" -> POST /engage#profile-set-once
- "How do I update properties on a group profile?" -> POST /groups#group-set
- "How do I batch update multiple user profiles at once?" -> POST /engage#profile-batch-update
- "How do I upload or replace a lookup table?" -> PUT /lookup-tables/{id}
- "How do I list all lookup tables in my project?" -> GET /lookup-tables
- "How do I delete a group profile?" -> POST /groups#group-delete
- "How do I remove specific profile properties?" -> POST /engage#profile-unset

## Response Tips

- **Import:** Check `num_records_imported` against your sent count; partial imports return 200 with a lower count, not an error.
- **Track/Engage/Groups:** Responses are minimal (200 = accepted); these endpoints are fire-and-forget, so absence of error is confirmation.
- **Lookup Tables GET:** Results are in `results` array of maps; each entry represents one table with its metadata.
- **Lookup Tables PUT:** Returns `code` + `status` only; a 200 means the full CSV was accepted and will replace the existing table.
- **All endpoints:** 401 means bad or missing auth; 403 means the token lacks permission for this operation; distinguish between the two when debugging.

## Anomaly Flags

- **429 Too Many Requests** on `/import` or `PUT /lookup-tables/{id}`: Rate limit hit. Back off exponentially and surface the retry-after interval to the user.
- **413 Payload Too Large** on `/import` or `PUT /lookup-tables/{id}`: Batch or CSV exceeds size limit. Agent should recommend splitting into smaller chunks.
- **Partial import (`num_records_imported` < records sent)**: Some events were rejected silently. Agent should flag the discrepancy and suggest re-sending with `strict=1` to get detailed error info.
- **401 across multiple endpoints**: Likely a project-wide auth misconfiguration (expired token, wrong project_id). Surface once, not per-call.
- **Region mismatch**: Base URL is `https://{region}.mixpanel.com`. If all calls fail with network errors, agent should verify the region (e.g., `api` for US, `api-eu` for EU).
- **strict=0 used on import**: Non-strict mode silently drops malformed events. Agent should warn that data loss may go unnoticed.

## Playbook

### 1. Bulk Import Historical Events

1. Prepare events as JSON array or NDJSON file.
2. Set `Content-Type` to `application/json` or `application/x-ndjson` accordingly.
3. If payload is large, set `Content-Encoding: gzip` and compress the body.
4. Call `POST /import` with `project_id` and `strict=1`.
5. Compare `num_records_imported` in the response against your sent count.
6. If count mismatches, inspect error details and fix malformed events.
7. On 429, wait and retry the failed batch. On 413, split into smaller batches.

### 2. Set Up and Enrich User Profiles

1. Use `POST /engage#profile-set-once` to initialize immutable properties (e.g., `$created`, `first_source`).
2. Use `POST /engage#profile-set` to update mutable properties (e.g., `plan`, `email`).
3. Use `POST /engage#profile-numerical-add` to increment counters (e.g., `login_count`, `purchase_total`).
4. Use `POST /engage#profile-union` to add tags to list properties without duplicates.
5. For bulk operations, use `POST /engage#profile-batch-update` to combine multiple profile updates in a single call.

### 3. Manage Group Profiles

1. Create or update a group profile with `POST /groups#group-set`, providing the group key and group ID.
2. Use `POST /groups#group-set-once` for properties that should only be written once (e.g., `created_date`).
3. Add values to list properties with `POST /groups#group-union`.
4. Remove specific values from lists with `POST /groups#group-remove-from-list`.
5. Delete a group profile entirely with `POST /groups#group-delete` when it is no longer needed.

### 4. Upload and Maintain Lookup Tables

1. Call `GET /lookup-tables` with your `project_id` to list existing tables and find the target table's `id`.
2. Prepare your lookup data as a CSV file with a header row.
3. Call `PUT /lookup-tables/{id}` with `Content-Type: text/csv` and the CSV body.
4. Confirm the response returns `status: "OK"` and `code: 200`.
5. On 413, reduce CSV size. On 429, retry after a delay.

### 5. Real-Time Event Tracking

1. Instrument your app to call `POST /track` for each user action.
2. Ensure the correct region is used in the base URL (`api.mixpanel.com` for US, `api-eu.mixpanel.com` for EU).
3. Verify 200 responses. On 401, check your project token. On 403, verify your token's permissions.
4. For associated profile updates (e.g., updating last-seen), follow up with `POST /engage#profile-set` in the same flow.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
