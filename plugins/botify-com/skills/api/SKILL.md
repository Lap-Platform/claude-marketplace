---
name: botify-api
description: "Botify API skill. Use when working with Botify for analyses, projects. Covers 26 endpoints."
version: 1.0.0
generator: lapsh
---

# Botify API
API version: 1.0.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.botify.com/v1

## Setup
1. Set your API key in the appropriate header
2. GET /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics -- verify access
3. POST /analyses/{username}/{project_slug}/{analysis_slug}/urls -- create first urls

## Endpoints

26 endpoints across 2 groups. See references/api-spec.lap for full details.

### analyses
| Method | Path | Description |
|--------|------|-------------|
| GET | /analyses/{username}/{project_slug} | List all analyses for a project |
| GET | /analyses/{username}/{project_slug}/{analysis_slug} | Get an Analysis detail |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics | Return global statistics for an analysis |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics/time | Return crawl statistics grouped by time frequency (1 min, 5 mins or 60 min) |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics/urls/{list_type} | Return a list of 1000 latest URLs crawled (all crawled URLs or only URLS with HTTP errors) |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/features/ganalytics/orphan_urls/{medium}/{source} | List of Orphan URLs |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/features/links/percentiles | Get inlinks percentiles |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/features/pagerank/lost | Lost pagerank |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/features/sitemaps/report | Get global information of the sitemaps found (sitemaps indexes, invalid sitemaps urls, etc |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/features/sitemaps/samples/out_of_config | Sample list of URLs which were found in your sitemaps but outside of the |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/features/sitemaps/samples/sitemap_only | Sample list of URLs which were found in your sitemaps, within the project |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/features/top_domains/domains | Top domains |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/features/top_domains/subdomains | Top subddomains |
| POST | /analyses/{username}/{project_slug}/{analysis_slug}/urls | Executes a query and returns a paginated response |
| POST | /analyses/{username}/{project_slug}/{analysis_slug}/urls/aggs | Query aggregator |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/urls/datamodel | Gets an Analysis datamodel |
| POST | /analyses/{username}/{project_slug}/{analysis_slug}/urls/export | Creates a new UrlExport object and starts a task that will export the results into a csv |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/urls/export | A list of the CSV Exports requests and their current status |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/urls/export/{url_export_id} | Checks the status of an CSVUrlExportJob object |
| POST | /analyses/{username}/{project_slug}/{analysis_slug}/urls/suggested_filters | Return most frequent segments (= suggested patterns in the previous version) |
| GET | /analyses/{username}/{project_slug}/{analysis_slug}/urls/{url} | Gets the detail of an URL for an analysis |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{username} | List all active projects for the user |
| POST | /projects/{username}/{project_slug}/features/url_rewriting/rules_validator | Match and replace parts of a URL based on rules passed in POST data |
| GET | /projects/{username}/{project_slug}/filters | List all the project's saved filters (each filter's name, ID and filter value) |
| GET | /projects/{username}/{project_slug}/filters/{identifier} | Retrieves a specific saved filter's name, ID and filter value |
| POST | /projects/{username}/{project_slug}/urls/aggs | Project Query aggregator |

## Enhanced Skill Content
## Question Mapping

- "What analyses exist for my project?" -> GET /analyses/{username}/{project_slug}
- "Show me details for a specific analysis" -> GET /analyses/{username}/{project_slug}/{analysis_slug}
- "How did my last crawl perform?" -> GET /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics
- "How did crawl speed change over time?" -> GET /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics/time
- "Which URLs were crawled or not crawled?" -> GET /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics/urls/{list_type}
- "What are my orphan URLs from Google Analytics?" -> GET /analyses/{username}/{project_slug}/{analysis_slug}/features/ganalytics/orphan_urls/{medium}/{source}
- "Which pages lost PageRank since last crawl?" -> GET /analyses/{username}/{project_slug}/{analysis_slug}/features/pagerank/lost
- "What does my sitemap report look like?" -> GET /analyses/{username}/{project_slug}/{analysis_slug}/features/sitemaps/report
- "Find URLs matching specific filters in an analysis" -> POST /analyses/{username}/{project_slug}/{analysis_slug}/urls
- "Get aggregate metrics for URLs in an analysis" -> POST /analyses/{username}/{project_slug}/{analysis_slug}/urls/aggs
- "What fields are available for URL queries?" -> GET /analyses/{username}/{project_slug}/{analysis_slug}/urls/datamodel
- "Export filtered URL data for offline analysis" -> POST /analyses/{username}/{project_slug}/{analysis_slug}/urls/export
- "Check the status of my URL export" -> GET /analyses/{username}/{project_slug}/{analysis_slug}/urls/export/{url_export_id}
- "List all my projects" -> GET /projects/{username}
- "Compare URL metrics across multiple analyses" -> POST /projects/{username}/{project_slug}/urls/aggs

## Response Tips

- **Analysis listings** (`GET /analyses/...`): Paginated with `page` and `size` params; default page size varies -- always check `count` or total in response to know if more pages exist.
- **Crawl statistics**: Nested time-series data; `frequency` is required for `/time` endpoint (e.g., daily, hourly) -- omitting it will error.
- **URL queries** (`POST .../urls`, `.../urls/aggs`): Request bodies use `UrlsQuery` or `UrlsAggsQueries` maps -- consult the datamodel endpoint first to discover valid field names and filter operators.
- **Exports** (`POST .../urls/export`): Returns 201 (accepted, async job); poll the GET export status endpoint until completion before downloading.
- **Feature endpoints** (sitemaps, top_domains, links, pagerank): Return precomputed reports -- no query body needed, but results are analysis-snapshot specific.
- **Projects**: Paginated list; `filters` sub-resource returns saved filter configurations, not URL results.

## Anomaly Flags

- **Export stuck**: If `GET .../urls/export/{id}` returns the same incomplete status across multiple polls, surface a warning -- the export job may have failed silently.
- **Empty crawl statistics**: If `/crawl_statistics` returns zero URLs crawled, flag that the analysis may still be in progress or the crawl configuration is misconfigured.
- **PageRank lost spike**: If `/features/pagerank/lost` returns a significantly higher count than previous analyses, proactively alert -- this may indicate broken internal links or removed pages.
- **Sitemap out-of-config URLs**: If `/features/sitemaps/samples/out_of_config` returns results, flag URLs present in sitemaps but outside the crawl scope -- these are likely configuration gaps.
- **Orphan URL count**: If the orphan URLs endpoint returns a large paginated set, surface this as a potential SEO issue -- these pages get traffic but have no internal links.
- **Pagination exhaustion**: If a response returns a full page of results (size == count returned), warn that there are likely more pages -- the caller should paginate to get complete data.

## Playbook

### 1. Audit a New Crawl Analysis

1. `GET /projects/{username}` to list projects and find the target `project_slug`
2. `GET /analyses/{username}/{project_slug}` to list analyses and identify the latest `analysis_slug`
3. `GET /analyses/{username}/{project_slug}/{analysis_slug}` to review analysis summary
4. `GET /analyses/{username}/{project_slug}/{analysis_slug}/crawl_statistics` for crawl health overview
5. `GET /analyses/{username}/{project_slug}/{analysis_slug}/features/sitemaps/report` to check sitemap coverage
6. `GET /analyses/{username}/{project_slug}/{analysis_slug}/features/pagerank/lost` to spot link equity losses

### 2. Export Filtered URL Data

1. `GET /analyses/{username}/{project_slug}/{analysis_slug}/urls/datamodel` to discover available fields and filter operators
2. `POST /analyses/{username}/{project_slug}/{analysis_slug}/urls` with a `UrlsQuery` body to preview matching URLs and refine filters
3. `POST /analyses/{username}/{project_slug}/{analysis_slug}/urls/export` with the same `UrlsQuery` to start an async export (returns 201)
4. `GET /analyses/{username}/{project_slug}/{analysis_slug}/urls/export/{url_export_id}` to poll until the export is ready
5. Download the completed export file from the returned URL

### 3. Investigate Orphan Pages

1. `GET /analyses/{username}/{project_slug}/{analysis_slug}/features/ganalytics/orphan_urls/{medium}/{source}` with medium=`organic` and source=`google` to find pages with search traffic but no internal links
2. `POST /analyses/{username}/{project_slug}/{analysis_slug}/urls` with a filter for the orphan URLs to inspect their metadata (status codes, depth, etc.)
3. `GET /analyses/{username}/{project_slug}/{analysis_slug}/features/links/percentiles` to understand the internal link distribution and set a baseline
4. Use the results to prioritize which orphan pages to link from existing content

### 4. Compare Metrics Across Analyses

1. `GET /analyses/{username}/{project_slug}` to list all available analyses with their slugs and dates
2. `POST /projects/{username}/{project_slug}/urls/aggs` with `nb_analyses` set to the number of analyses to compare, and `UrlsAggsQueries` defining the metrics to aggregate
3. Compare the returned aggregate values across time periods to spot trends (e.g., crawled URL count, average load time, indexable page ratio)

### 5. Validate URL Rewriting Rules

1. `GET /projects/{username}/{project_slug}/filters` to review existing saved filters
2. `POST /projects/{username}/{project_slug}/features/url_rewriting/rules_validator` with your proposed rewriting rules in the request body
3. Check the 201 response for validation results -- fix any flagged rule conflicts or syntax errors before applying to the project configuration


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
