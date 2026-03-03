---
name: bc-data-catalogue-api
description: "BC Data Catalogue API skill. Use when working with BC Data Catalogue for action. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# BC Data Catalogue API
API version: 3.0.1

## Auth
OAuth2 | ApiKey ckan_api_key in header

## Base URL
https://catalogue.data.gov.bc.ca/api/3

## Setup
1. Set your API key in the appropriate header
2. GET /action/tag_list -- verify access

## Endpoints

22 endpoints across 1 groups. See references/api-spec.lap for full details.

### action
| Method | Path | Description |
|--------|------|-------------|
| GET | /action/tag_list | Get a list of tags |
| GET | /action/status_show | Get the site status |
| GET | /action/package_list | Get a list of all packages (datasets) |
| GET | /action/package_search | Find packages (datasets) matching query terms |
| GET | /action/package_show | Get metadata about one specific package (dataset) |
| GET | /action/package_activity_list | Get the activity stream of a package (dataset) |
| GET | /action/package_activity_list_html | Get the activity stream of a package (dataset), HTML format |
| GET | /action/package_autocomplete | Find packages (datasets) matching a query |
| GET | /action/package_relationships_list | Get package (dataset) relationships |
| GET | /action/package_revision_list | Get list of revisions for a package (dataset) |
| GET | /action/organization_activity_list | Get the activity stream of an organization |
| GET | /action/organization_activity_list_html | Get the activity stream of an organization, HTML format |
| GET | /action/organization_follower_count | Get number of followers of an organization |
| GET | /action/organization_follower_list | Get users following an organization |
| GET | /action/organization_list_for_user | Get organizations that a user has a given permission for |
| GET | /action/organization_revision_list | Get organization revisions |
| GET | /action/organization_show | Get details of a specific organization |
| GET | /action/organization_list | Get names of all organizations |
| GET | /action/organization_autocomplete | Get names of organizations that match a query string |
| GET | /action/resource_search | Find resources |
| GET | /action/resource_show | Get metadata for a specific resource |
| GET | /action/related_list | Gets items related to a package (dataset) |

## Enhanced Skill Content
## Question Mapping

- "What datasets are available in the BC Data Catalogue?" -> GET /action/package_list
- "Search for datasets about water quality" -> GET /action/package_search
- "Show me details for a specific dataset" -> GET /action/package_show
- "What tags are used in the catalogue?" -> GET /action/tag_list
- "Find all CSV resources in the catalogue" -> GET /action/resource_search
- "What organizations publish data in BC?" -> GET /action/organization_list
- "Show me info about the Ministry of Agriculture" -> GET /action/organization_show
- "What changed recently on this dataset?" -> GET /action/package_activity_list
- "Is the BC Data Catalogue API up?" -> GET /action/status_show
- "Autocomplete a dataset name starting with 'Okanagan'" -> GET /action/package_autocomplete
- "Which organizations can I edit?" -> GET /action/organization_list_for_user
- "How many followers does this organization have?" -> GET /action/organization_follower_count
- "What are the relationships between two datasets?" -> GET /action/package_relationships_list
- "Show me the revision history of this organization" -> GET /action/organization_revision_list
- "Get details about a specific resource by ID" -> GET /action/resource_show

## Response Tips

- **Package endpoints**: All responses wrap results in `{"success": true, "result": ...}` -- always read from `.result`, never the top-level object.
- **List endpoints** (package_list, tag_list, organization_list): Return arrays; use `offset`/`limit` for pagination -- there is no `next` cursor, so increment `offset` by `limit` manually until results come back empty.
- **Search endpoints** (package_search, resource_search): Return `{count, results}` inside `.result` -- use `count` to know total matches and compute remaining pages.
- **Show endpoints** (package_show, organization_show, resource_show): Return a single object with nested arrays (e.g., `resources`, `groups`, `tags` inside a package).
- **Activity endpoints**: Return timestamped activity objects -- sort is newest-first by default; the HTML variants return pre-rendered markup, not structured data.
- **Autocomplete endpoints**: Return lightweight stub objects (name + title only) -- follow up with the full `_show` endpoint for complete details.
- **Error responses**: Return `{"success": false, "error": {"message": "...", "__type": "..."}}` -- check `__type` for `Not Found Error`, `Validation Error`, or `Authorization Error`.

## Anomaly Flags

- **Empty result sets on broad queries**: If `package_search` with a common term returns zero results, the API may be experiencing index issues -- surface this to the user.
- **Authentication failures on read endpoints**: All listed endpoints are GET (read-only) and should work without auth; a 403 on these suggests IP blocking or misconfigured proxy -- flag immediately.
- **Stale activity timestamps**: If `package_activity_list` shows no activity in 90+ days for an active dataset, the activity log may be incomplete or the dataset orphaned.
- **Pagination exhaustion**: If `offset + limit` exceeds `count` and the API still returns results, flag the inconsistency -- CKAN pagination can drift during concurrent writes.
- **Deprecated or missing fields**: If `resource_show` returns resources without `format`, `url`, or `last_modified`, the resource record is likely corrupt or migrated -- notify the user before downstream processing.
- **Unusually large `count` in search**: If `package_search` returns a count over 50,000, recommend narrowing the query with `fq` filters to avoid timeouts on iteration.

## Playbook

### 1. Find and Download a Dataset

1. Search for datasets: `GET /action/package_search?q=drinking water quality`
2. Review results in `.result.results[]` -- pick the dataset by name/title
3. Get full dataset details: `GET /action/package_show?id={dataset-name}`
4. Inspect `.result.resources[]` for available formats (CSV, JSON, SHP, etc.)
5. Get resource metadata: `GET /action/resource_show?id={resource-id}`
6. Download the file from the `url` field in the resource object

### 2. Explore an Organization's Published Data

1. Search for the org: `GET /action/organization_autocomplete?q=ministry`
2. Get full org details with datasets: `GET /action/organization_show?id={org-name}&include_datasets=True`
3. Browse `.result.packages[]` for published datasets
4. Check recent activity: `GET /action/organization_activity_list?id={org-name}`
5. Check follower engagement: `GET /action/organization_follower_count?id={org-name}`

### 3. Monitor Dataset Changes Over Time

1. Get the dataset: `GET /action/package_show?id={dataset-name}`
2. Pull activity log: `GET /action/package_activity_list?id={dataset-name}&limit=31`
3. Review timestamps and activity types for recent changes
4. Check revision history: `GET /action/package_revision_list?id={dataset-name}`
5. For human-readable summaries, use: `GET /action/package_activity_list_html?id={dataset-name}`

### 4. Bulk Catalogue Inventory

1. Get total dataset count: `GET /action/package_search?q=&rows=0` (read `.result.count`)
2. Page through all datasets: `GET /action/package_list?offset=0&limit=100`, then `offset=100`, `offset=200`, etc.
3. For each dataset name, fetch metadata: `GET /action/package_show?id={name}`
4. Find all CSV resources across the catalogue: `GET /action/resource_search?query=format:csv&offset=0&limit=100`
5. Compile tags for categorization: `GET /action/tag_list?limit=100`

### 5. Check API Health and Your Permissions

1. Verify the API is operational: `GET /action/status_show`
2. Confirm your auth works by listing your orgs: `GET /action/organization_list_for_user?permission=edit_group` (requires valid `ckan_api_key`)
3. If the status endpoint returns but authenticated calls fail, check that the `ckan_api_key` header or OAuth2 token is set correctly
4. Test a simple read: `GET /action/package_list?limit=1` -- if this fails too, the issue is network/proxy, not auth


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
