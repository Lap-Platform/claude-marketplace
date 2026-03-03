---
name: hashlookup-circl-api
description: "hashlookup CIRCL API skill. Use when working with hashlookup CIRCL for bulk, children, info. Covers 11 endpoints."
version: 1.0.0
generator: lapsh
---

# hashlookup CIRCL API
API version: 1.3

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /info -- verify access
3. POST /bulk/md5 -- create first md5

## Endpoints

11 endpoints across 7 groups. See references/api-spec.lap for full details.

### bulk
| Method | Path | Description |
|--------|------|-------------|
| POST | /bulk/md5 | Bulk search of MD5 hashes in a JSON array with the key 'hashes'. |
| POST | /bulk/sha1 | Bulk search of SHA1 hashes in a JSON array with the 'hashes'. |

### children
| Method | Path | Description |
|--------|------|-------------|
| GET | /children/{sha1}/{count}/{cursor} | Return children from a given SHA1.  A number of element to return and an offset must be given. If not set it will be the 100 first elements. A cursor must be given to paginate over. The starting cursor is 0. |

### info
| Method | Path | Description |
|--------|------|-------------|
| GET | /info | Info about the hashlookup database |

### lookup
| Method | Path | Description |
|--------|------|-------------|
| GET | /lookup/md5/{md5} | Lookup MD5. |
| GET | /lookup/sha1/{sha1} | Lookup SHA-1. |
| GET | /lookup/sha256/{sha256} | Lookup SHA-256. |

### parents
| Method | Path | Description |
|--------|------|-------------|
| GET | /parents/{sha1}/{count}/{cursor} | Return parents from a given SHA1. A number of element to return and an offset must be given. If not set it will be the 100 first elements. A cursor must be given to paginate over. The starting cursor is 0. |

### session
| Method | Path | Description |
|--------|------|-------------|
| GET | /session/create/{name} | Create a session key to keep search context. The session is attached to a name. After the session is created, the header `hashlookup_session` can be set to the session name. |
| GET | /session/get/{name} | Return set of matching and non-matching hashes from a session. |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats/top | Return the top 100 of most queried values. |

## Enhanced Skill Content
## Question Mapping

- "What is this file hash?" -> GET /lookup/md5/{md5}
- "Look up a SHA1 hash" -> GET /lookup/sha1/{sha1}
- "Check if a SHA256 hash is known" -> GET /lookup/sha256/{sha256}
- "Look up multiple MD5 hashes at once" -> POST /bulk/md5
- "Bulk check a list of SHA1 hashes" -> POST /bulk/sha1
- "What files are contained inside this package?" -> GET /children/{sha1}/{count}/{cursor}
- "What parent archives contain this file?" -> GET /parents/{sha1}/{count}/{cursor}
- "What version of the hashlookup API is running?" -> GET /info
- "Show me the most looked-up hashes" -> GET /stats/top
- "Create a named session to group my lookups" -> GET /session/create/{name}
- "Retrieve results from a previous session" -> GET /session/get/{name}
- "Is this file malicious or known-good?" -> GET /lookup/sha256/{sha256}
- "Page through all children of a known archive" -> GET /children/{sha1}/{count}/{cursor}
- "I have a list of hashes from a forensic image, check them all" -> POST /bulk/md5

## Response Tips

- **lookup**: Returns file metadata (filename, size, known source) or 404 when the hash is not in the database -- a 404 is normal and means "unknown," not an error.
- **bulk**: Accepts a JSON array of hashes; response is an array in the same order -- check individual entries for null/missing to identify unknown hashes.
- **children/parents**: Paginated via `{count}` (page size) and `{cursor}` (offset); an empty array signals the last page.
- **session**: `create` initializes server-side state; `get` retrieves it -- 500 typically means the backend store is unavailable, not a client mistake.
- **stats/info**: Simple flat objects with no pagination; info returns version and database size metadata.

## Anomaly Flags

- **High 404 rate on bulk lookups**: If most hashes in a bulk request return unknown, surface this -- it may indicate the hashes come from a private or very new dataset not yet indexed.
- **Session 500 errors**: Proactively warn the user that the session backend may be degraded; suggest falling back to client-side result aggregation.
- **400 on lookup endpoints**: Flag malformed hash input immediately -- MD5 must be 32 hex chars, SHA1 must be 40, SHA256 must be 64.
- **Empty children/parents responses on first page**: Surface that the SHA1 may not be a known archive or contained file, rather than silently returning nothing.
- **Unusual stats/top entries**: If top-queried hashes correspond to known malware samples, flag this context to the user.

## Playbook

### 1. Identify an Unknown File by Hash

1. Compute the file's SHA256: `sha256sum <file>`
2. Call GET /lookup/sha256/{sha256}
3. If 404, retry with MD5 or SHA1 (some older entries lack SHA256)
4. Review the response for filename, known source, and trust level

### 2. Bulk Triage a Set of Hashes from a Forensic Image

1. Collect all MD5 or SHA1 hashes into a JSON array
2. Call POST /bulk/md5 (or /bulk/sha1) with the array as the request body
3. Iterate the response; separate known files from unknown (null) entries
4. Unknown hashes are candidates for deeper malware analysis

### 3. Explore an Archive's Contents

1. Look up the archive's SHA1 via GET /lookup/sha1/{sha1} to confirm it exists
2. Call GET /children/{sha1}/50/0 to fetch the first 50 child files
3. If results fill the page, increment the cursor and repeat
4. Cross-reference child hashes with lookup endpoints for file-level detail

### 4. Track Lookups Across a Session

1. Call GET /session/create/{name} to initialize a named session
2. Perform your lookup or bulk queries (results are associated with the session server-side)
3. Call GET /session/get/{name} to retrieve aggregated session results
4. Use sessions to group related investigations (e.g., per-incident or per-host)

### 5. Check API Health and Database Coverage

1. Call GET /info to confirm the API version and database statistics
2. Call GET /stats/top to see the most frequently queried hashes
3. Use the database size from /info to gauge coverage before running large batch jobs


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
