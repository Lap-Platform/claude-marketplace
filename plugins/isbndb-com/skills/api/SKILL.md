---
name: isbndb-api
description: "ISBNdb API skill. Use when working with ISBNdb for author, authors, book. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# ISBNdb API
API version: 1.0.1

## Auth
ApiKey x-api-key in header

## Base URL
https://api.isbndb.com

## Setup
1. Set your API key in the appropriate header
2. GET /search -- verify access

## Endpoints

10 endpoints across 10 groups. See references/api-spec.lap for full details.

### author
| Method | Path | Description |
|--------|------|-------------|
| GET | /author/{name} | Gets author details |

### authors
| Method | Path | Description |
|--------|------|-------------|
| GET | /authors/{query} | Search authors |

### book
| Method | Path | Description |
|--------|------|-------------|
| GET | /book/{isbn} | Gets book details |

### books
| Method | Path | Description |
|--------|------|-------------|
| GET | /books/{query} | Search books |

### publisher
| Method | Path | Description |
|--------|------|-------------|
| GET | /publisher/{name} | Gets publisher details |

### publishers
| Method | Path | Description |
|--------|------|-------------|
| GET | /publishers/{query} | Search publishers |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search | Search all ISBNDB databases |

### stats
| Method | Path | Description |
|--------|------|-------------|
| GET | /stats | Gets status on the ISBNDB Database |

### subject
| Method | Path | Description |
|--------|------|-------------|
| GET | /subject/{name} | Gets subject details |

### subjects
| Method | Path | Description |
|--------|------|-------------|
| GET | /subjects/{query} | Search subjects |

## Enhanced Skill Content
## Question Mapping

- "What books has Stephen King written?" -> GET /author/{name}
- "Find authors whose name contains 'Tolkien'?" -> GET /authors/{query}
- "Look up the book with ISBN 9780140328721?" -> GET /book/{isbn}
- "Search for books about machine learning?" -> GET /books/{query}
- "What books has O'Reilly Media published?" -> GET /publisher/{name}
- "Find publishers matching 'penguin'?" -> GET /publishers/{query}
- "Search the entire database for 'climate change'?" -> GET /search
- "How many books are in the ISBNdb database?" -> GET /stats
- "What books fall under the subject 'Artificial Intelligence'?" -> GET /subject/{name}
- "Find subjects related to 'history'?" -> GET /subjects/{query}
- "Show me page 3 of Stephen King's books?" -> GET /author/{name} with page=3
- "Get 50 results per page for books about Python?" -> GET /books/{query} with pageSize=50
- "Find books by a specific author about a specific topic?" -> GET /books/{query} with author filter
- "What are the available subject categories matching 'science'?" -> GET /subjects/{query}

## Response Tips

- **Single-resource endpoints** (book, author, publisher, subject): Return a single object; 404 means the exact name/ISBN was not found -- check spelling and formatting.
- **List/search endpoints** (books, authors, publishers, subjects, search): Return paginated arrays; always check `page` and `pageSize` in responses to determine if more pages exist.
- **Stats endpoint**: Returns aggregate counts with no pagination; useful for health checks and capacity monitoring.
- **All endpoints**: Require `x-api-key` header; missing or invalid keys typically return 401/403 before any 404.

## Anomaly Flags

- **404 on single lookups**: Surface when an ISBN, author name, or publisher returns 404 -- suggest alternative spellings or a broader search via the plural endpoint.
- **Empty result sets**: Flag when a list endpoint returns 200 but with zero results, as the query may need broadening.
- **Pagination exhaustion**: Alert when the current page appears to be the last page so the user knows all results have been retrieved.
- **Rate limiting signals**: Watch for 429 status codes or unexpected delays; ISBNdb plans have daily request caps that vary by tier.
- **ISBN format issues**: Proactively validate ISBN-10 vs ISBN-13 format before calling /book/{isbn} to avoid unnecessary 404s.
- **API key misconfiguration**: Surface immediately if any call returns 401 or 403 -- the x-api-key header may be missing or expired.

## Playbook

### 1. Look Up a Book by ISBN

1. Validate the ISBN format (10 or 13 digits, correct check digit).
2. Call `GET /book/{isbn}` with the `x-api-key` header.
3. If 404, try the alternate ISBN format (ISBN-10 vs ISBN-13).
4. If still not found, fall back to `GET /books/{query}` using the book title.

### 2. Get All Books by an Author

1. Call `GET /author/{name}` with `page=1` and desired `pageSize`.
2. Inspect the response for total count and current page.
3. Loop through subsequent pages incrementing `page` until all results are collected.
4. If 404 on the exact name, use `GET /authors/{query}` to find the correct author name first.

### 3. Discover Books on a Topic

1. Call `GET /subjects/{query}` to find the exact subject name matching your topic.
2. Pick the best-matching subject from results.
3. Call `GET /subject/{name}` with the exact subject name to retrieve books under that subject.
4. Optionally cross-reference with `GET /books/{query}` for broader keyword coverage.

### 4. Explore a Publisher's Catalog

1. Call `GET /publishers/{query}` to find the exact publisher name.
2. Call `GET /publisher/{name}` with `page=1` and `pageSize=50`.
3. Paginate through all results to build the full catalog.
4. Use `GET /book/{isbn}` on individual results for detailed metadata.

### 5. Database Overview and General Search

1. Call `GET /stats` to understand the current database size and coverage.
2. Use `GET /search?q={term}` for a broad cross-category search when unsure whether the query is an author, title, subject, or publisher.
3. Based on result types, drill into the appropriate specific endpoint (book, author, publisher, or subject) for full details.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
