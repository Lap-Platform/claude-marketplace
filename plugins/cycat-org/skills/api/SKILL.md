---
name: cycatorg-api
description: "CyCAT.org API skill. Use when working with CyCAT.org for child, generate, info. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# CyCAT.org API
API version: 0.9

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /generate/uuid -- verify access
3. POST /propose -- create first propose

## Endpoints

14 endpoints across 10 groups. See references/api-spec.lap for full details.

### child
| Method | Path | Description |
|--------|------|-------------|
| GET | /child/{uuid} | Get child UUID(s) from a specified project or publisher UUID. |

### generate
| Method | Path | Description |
|--------|------|-------------|
| GET | /generate/uuid | Generate an UUID version 4 RFC4122-compliant. |

### info
| Method | Path | Description |
|--------|------|-------------|
| GET | /info | Get information about the CyCAT backend services including status, overall statistics and version. |

### list
| Method | Path | Description |
|--------|------|-------------|
| GET | /list/project/{start}/{end} | List projects registered in CyCAT by pagination (start,end). |
| GET | /list/publisher/{start}/{end} | List publishers registered in CyCAT by pagination (start,end). |

### lookup
| Method | Path | Description |
|--------|------|-------------|
| GET | /lookup/{uuid} | Lookup UUID registered in CyCAT. |

### namespace
| Method | Path | Description |
|--------|------|-------------|
| GET | /namespace/finduuid/{namespace}/{namespaceid} | Get all known UUID for a given namespace id. |
| GET | /namespace/getall | List all known namespaces. |
| GET | /namespace/getid/{namespace} | Get all ID from a given namespace. |

### parent
| Method | Path | Description |
|--------|------|-------------|
| GET | /parent/{uuid} | Get parent UUID(s) from a specified project or item UUID. |

### propose
| Method | Path | Description |
|--------|------|-------------|
| POST | /propose | Propose new resource to CyCAT. |

### relationships
| Method | Path | Description |
|--------|------|-------------|
| GET | /relationships/expanded/{uuid} | Get relationship(s) UUID from a specified UUID including the relationships meta information. |
| GET | /relationships/{uuid} | Get relationship(s) UUID from a specified UUID. |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search/{searchquery} | Full-text search in CyCAT and return matching UUID. |

## Enhanced Skill Content
## Question Mapping

- "What is CyCAT and what version is the API?" -> GET /info
- "Generate a new UUID for a CyCAT entry" -> GET /generate/uuid
- "Look up details for a specific UUID" -> GET /lookup/{uuid}
- "What are the child entries of this UUID?" -> GET /child/{uuid}
- "What is the parent of this UUID?" -> GET /parent/{uuid}
- "Show me all relationships for a UUID" -> GET /relationships/{uuid}
- "Show me expanded relationships with full details for a UUID" -> GET /relationships/expanded/{uuid}
- "List all available namespaces" -> GET /namespace/getall
- "What is the ID for a specific namespace?" -> GET /namespace/getid/{namespace}
- "Find the UUID for an item in a given namespace" -> GET /namespace/finduuid/{namespace}/{namespaceid}
- "List projects in a paginated range" -> GET /list/project/{start}/{end}
- "List publishers in a paginated range" -> GET /list/publisher/{start}/{end}
- "Search for cybersecurity entries by keyword" -> GET /search/{searchquery}
- "Propose a new entry to the CyCAT catalog" -> POST /propose

## Response Tips

- **Info/Generate**: Flat JSON objects; `/info` returns version and instance metadata, `/generate/uuid` returns a single UUID string.
- **Lookup/Child/Parent**: Keyed by UUID; check for empty or null responses when a UUID has no children or no parent.
- **Relationships**: `/relationships/{uuid}` returns direct links; `/relationships/expanded/{uuid}` nests full objects for each related entry -- expect deeper payloads.
- **List (project/publisher)**: `{start}` and `{end}` are offset indices, not page numbers; an empty array signals you have passed the last entry.
- **Namespace**: `/getall` returns a flat list; `/getid` and `/finduuid` return single-value lookups that may return empty when the namespace or ID is unregistered.
- **Search**: Results are returned as an array; no result count header -- an empty array means zero matches.
- **Propose**: POST body format is not documented in the spec; expect a confirmation object or error message on 200.

## Anomaly Flags

- **Empty relationship graph**: If `/child/{uuid}` and `/parent/{uuid}` both return empty while `/lookup/{uuid}` succeeds, the entry may be orphaned -- surface this to the user.
- **UUID not found**: Any lookup/child/parent/relationships call returning empty or null likely means the UUID is unregistered; suggest using `/search` or `/namespace/finduuid` instead.
- **List range overshoot**: If `/list/project/{start}/{end}` returns fewer items than `(end - start)`, the user has reached the end of the catalog -- note this proactively.
- **Namespace mismatch**: If `/namespace/getid/{namespace}` returns empty, the namespace may be misspelled or not yet registered; list available namespaces with `/namespace/getall`.
- **Proposal without UUID**: If a user tries `/propose` without first generating a UUID via `/generate/uuid`, flag that they may need to generate one first.
- **Expanded relationships payload size**: `/relationships/expanded/{uuid}` can return significantly larger payloads than the compact variant; warn when traversing many UUIDs in sequence.

## Playbook

### Register and Propose a New Entry

1. Call `GET /generate/uuid` to obtain a fresh UUID.
2. Call `GET /namespace/getall` to review available namespaces and pick the right one.
3. Call `POST /propose` with the generated UUID, chosen namespace, and entry metadata.
4. Call `GET /lookup/{uuid}` to confirm the entry is now registered.

### Explore an Entry's Full Context

1. Call `GET /lookup/{uuid}` to retrieve the entry's core metadata.
2. Call `GET /parent/{uuid}` to find the parent entry (if any).
3. Call `GET /child/{uuid}` to list all child entries.
4. Call `GET /relationships/expanded/{uuid}` to get the full relationship graph with nested details.

### Search and Resolve a Cybersecurity Item

1. Call `GET /search/{searchquery}` with a keyword (e.g., CVE ID, tool name).
2. Pick the best-matching UUID from the results.
3. Call `GET /lookup/{uuid}` to get full details.
4. Optionally call `GET /relationships/{uuid}` to see linked advisories, tools, or actors.

### Enumerate All Projects or Publishers

1. Call `GET /list/project/0/50` to fetch the first 50 projects.
2. If 50 results are returned, call `GET /list/project/50/100` for the next batch.
3. Repeat, incrementing by 50, until fewer than 50 results are returned.
4. Apply the same pattern with `/list/publisher/{start}/{end}` for publishers.

### Cross-Reference a Namespace ID to Full Entry

1. Call `GET /namespace/getall` to confirm the namespace exists.
2. Call `GET /namespace/finduuid/{namespace}/{namespaceid}` to resolve the namespace-specific ID to a CyCAT UUID.
3. Call `GET /lookup/{uuid}` with the resolved UUID to get the full entry.
4. Call `GET /relationships/{uuid}` to discover linked entries across namespaces.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
