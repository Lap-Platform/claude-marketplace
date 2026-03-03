---
name: debian-code-search
description: "Debian Code Search API skill. Use when working with Debian Code Search for search, searchperpackage. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Debian Code Search
API version: 1.4.0

## Auth
ApiKey x-dcs-apikey in header

## Base URL
https://codesearch.debian.net/api/v1

## Setup
1. Set your API key in the appropriate header
2. GET /search -- verify access

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search | Searches through source code |

### searchperpackage
| Method | Path | Description |
|--------|------|-------------|
| GET | /searchperpackage | Like /search, but aggregates per package |

## Enhanced Skill Content


## Question Mapping

- "Search for a string in all Debian packages?" -> GET /search
- "Find all occurrences of a regex pattern across Debian source code?" -> GET /search
- "Search for a literal string instead of a regex?" -> GET /search (with match_mode=literal)
- "How many Debian packages contain a specific function call?" -> GET /searchperpackage
- "Which packages import a particular library?" -> GET /searchperpackage
- "Find all uses of a deprecated function grouped by package?" -> GET /searchperpackage
- "Search Debian source code for a CVE identifier?" -> GET /search
- "List packages that reference a specific config file path?" -> GET /searchperpackage (with match_mode=literal)
- "Find regex matches and see which packages they belong to?" -> GET /searchperpackage
- "Search for an exact filename across all Debian sources?" -> GET /search (with match_mode=literal)
- "How widespread is usage of a specific API pattern in Debian?" -> GET /searchperpackage
- "Find hardcoded credentials or secrets in Debian packages?" -> GET /search
- "Compare how many packages use library A vs library B?" -> GET /searchperpackage (two calls, compare counts)

## Response Tips

- **search**: Returns flat result list with file paths and matching lines. Results may be large for common patterns -- narrow your query or use literal mode to reduce noise.
- **searchperpackage**: Returns results grouped by package name. Use this when you need a count of affected packages or want to browse matches per-package rather than as a flat list.
- **Errors**: A 403 means your API key is missing or invalid -- check the `x-dcs-apikey` header. No other documented error codes, so treat unexpected status codes as transient server issues.

## Anomaly Flags

- **403 responses**: Surface immediately -- indicates authentication failure. Prompt user to verify their `x-dcs-apikey` header value.
- **Empty result sets**: Flag when a query returns zero results -- suggest checking for typos or switching between `regexp` and `literal` match modes.
- **Very large result sets**: Warn when results are unusually large, as broad regex patterns (e.g., `.*`) can return overwhelming data.
- **Slow responses**: Debian Code Search indexes a massive corpus. Flag if response times exceed 10s -- the query may be too broad or the service may be under load.
- **Regex syntax errors**: If search returns unexpected results, surface the possibility that the query contains unescaped regex metacharacters when literal mode was intended.

## Playbook

### 1. Basic Code Search

1. Set the `x-dcs-apikey` header with your API key
2. Call `GET /search?query=your_search_term` (defaults to regexp mode)
3. Review the returned file paths and matching lines
4. If too many results, add `match_mode=literal` or refine the regex

### 2. Audit a Function Across All Packages

1. Call `GET /searchperpackage?query=function_name&match_mode=literal`
2. Count the number of unique packages in the response
3. Review each package's matches to assess usage patterns
4. For deeper inspection of specific matches, use `GET /search` with a narrower query targeting the package name in the path

### 3. Compare Adoption of Two Patterns

1. Call `GET /searchperpackage?query=pattern_A&match_mode=literal`
2. Record the package count for pattern A
3. Call `GET /searchperpackage?query=pattern_B&match_mode=literal`
4. Record the package count for pattern B
5. Compare counts and surface the list of packages unique to each pattern

### 4. Find and Triage Security-Sensitive Code

1. Call `GET /search?query=CVE-YYYY-NNNNN&match_mode=literal` to find references to a specific CVE
2. Call `GET /searchperpackage` with the same query to see which packages are affected
3. For each affected package, search for the vulnerable function with `GET /search?query=vulnerable_function_name`
4. Compile a list of packages still referencing the vulnerability for triage


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
