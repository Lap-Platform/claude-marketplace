---
name: automata-market-intelligence-api
description: "Automata Market Intelligence API skill. Use when working with Automata Market Intelligence for similar, search, contentpro-similar-text. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Automata Market Intelligence API
API version: 1.0.1

## Auth
ApiKey x-api-key in header

## Base URL
https://api.byautomata.io/

## Setup
1. Set your API key in the appropriate header
2. GET /similar -- verify access
3. POST /contentpro-similar-text -- create first contentpro-similar-text

## Endpoints

4 endpoints across 4 groups. See references/api-spec.lap for full details.

### similar
| Method | Path | Description |
|--------|------|-------------|
| GET | /similar | Send a company website to receive a list of companies related to them. |

### search
| Method | Path | Description |
|--------|------|-------------|
| GET | /search | Send search terms to receive the most relevant companies along with text snippets. |

### contentpro-similar-text
| Method | Path | Description |
|--------|------|-------------|
| POST | /contentpro-similar-text | The /contentpro-similar-text endpoint accepts and arbitrary piece of text and returns similar articles and blogs written by companies. |

### contentpro-search
| Method | Path | Description |
|--------|------|-------------|
| GET | /contentpro-search | Send search terms to receive the most relevant articles and companies. |

## Enhanced Skill Content


## Question Mapping

- "Find companies similar to this website?" -> GET /similar
- "What companies are related to competitor.com?" -> GET /similar
- "Search for companies by industry keywords?" -> GET /search
- "Find businesses matching 'machine learning SaaS'?" -> GET /search
- "Get the next page of similar company results?" -> GET /similar (with page param)
- "Get page 3 of my search results?" -> GET /search (with page param)
- "Find content similar to this paragraph of text?" -> POST /contentpro-similar-text
- "What articles or pages match this text snippet?" -> POST /contentpro-similar-text
- "Search for content by topic keywords?" -> GET /contentpro-search
- "Find market intelligence content about 'fintech payments'?" -> GET /contentpro-search
- "Compare two companies by finding overlaps in their similar sets?" -> GET /similar (x2, then diff)
- "Build a competitive landscape for a given URL?" -> GET /similar, then GET /search to enrich
- "Discover content and companies around a new market term?" -> GET /search + GET /contentpro-search

## Response Tips

- **similar/search**: Responses are paginated -- pass `page` to advance. Check if the result set is empty to detect the last page.
- **contentpro endpoints**: Content results may nest source metadata inside each item -- extract `link` or `title` fields for display.
- **All endpoints**: 403 means invalid or missing `x-api-key`. 501 means the feature is not implemented for the given input. 400 is malformed request -- check required params.

## Anomaly Flags

- **403 responses**: Surface immediately -- likely an expired, missing, or revoked API key. Prompt user to verify `x-api-key`.
- **501 responses**: Flag as a capability gap -- the endpoint does not support this input type or feature yet. Suggest alternative endpoints.
- **Empty result sets on page 1**: Unusual -- flag that the query terms or link may be too narrow or malformed.
- **Pagination exhaustion**: If incrementing `page` returns empty, notify the user that all results have been retrieved rather than silently stopping.
- **Repeated 400 errors**: Likely a parameter format issue -- surface the exact params being sent for user review.

## Playbook

### 1. Find and Explore Companies Similar to a Competitor

1. Call `GET /similar` with `link` set to the competitor's URL (e.g., `https://competitor.com`).
2. Review the returned companies -- note names, links, and relevance.
3. Page through results by incrementing the `page` parameter until an empty set is returned.
4. For each interesting result, call `GET /similar` again with that company's link to expand the map.

### 2. Research a Market Segment by Keywords

1. Call `GET /search` with `terms` describing the segment (e.g., `"AI healthcare diagnostics"`).
2. Collect all company results, paginating as needed.
3. Call `GET /contentpro-search` with the same `terms` to find related content and articles.
4. Cross-reference company results with content results to build a complete market picture.

### 3. Analyze a Block of Text for Related Content and Companies

1. Call `POST /contentpro-similar-text` with the text body to find related content.
2. Extract key terms or company names from the content results.
3. Call `GET /search` with those extracted terms to find matching companies.
4. Call `GET /similar` with any discovered company URLs to expand the network.

### 4. Build a Competitive Landscape Report

1. Start with `GET /similar` using the target company's URL to get direct competitors.
2. For each top competitor, call `GET /similar` to find second-degree connections.
3. Call `GET /search` with the target company's core industry terms for broader coverage.
4. Call `GET /contentpro-search` with the same terms to gather market content and trends.
5. Deduplicate and rank results by frequency of appearance across queries.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
