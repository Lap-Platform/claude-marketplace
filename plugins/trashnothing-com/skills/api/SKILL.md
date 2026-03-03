---
name: trash-nothing
description: "Trash Nothing API skill. Use when working with Trash Nothing for users, groups, posts. Covers 12 endpoints."
version: 1.0.0
generator: lapsh
---

# Trash Nothing
API version: 1.4

## Auth
ApiKey api_key in query

## Base URL
https://trashnothing.com/api/v1.4

## Setup
1. Set your API key in the appropriate header
2. GET /groups -- verify access

## Endpoints

12 endpoints across 3 groups. See references/api-spec.lap for full details.

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users/{user_id}/posts | List posts by a user |
| GET | /users/{user_id}/posts/search | Search posts by a user |

### groups
| Method | Path | Description |
|--------|------|-------------|
| GET | /groups | Search groups |
| GET | /groups/{group_id} | Retrieve a group |
| GET | /groups/multiple | Retrieve multiple groups |

### posts
| Method | Path | Description |
|--------|------|-------------|
| GET | /posts | List posts |
| GET | /posts/search | Search posts |
| GET | /posts/all | List all posts |
| GET | /posts/all/changes | List all post changes |
| GET | /posts/{post_id}/display | Retrieve post display data |
| GET | /posts/{post_id} | Retrieve a post |
| GET | /posts/multiple | Retrieve multiple posts |

## Enhanced Skill Content
## Question Mapping

- "What free stuff is available near me?" -> GET /posts (with latitude, longitude, radius params)
- "Search for furniture being given away" -> GET /posts/search (search=furniture)
- "What has a specific user posted?" -> GET /users/{user_id}/posts
- "Search a user's posts for electronics" -> GET /users/{user_id}/posts/search (search=electronics)
- "Find freecycle groups in my area" -> GET /groups (with latitude, longitude, distance)
- "Get details about a specific group" -> GET /groups/{group_id}
- "Look up multiple groups at once" -> GET /groups/multiple (group_ids=id1,id2)
- "Show me the full details of a post" -> GET /posts/{post_id}
- "Get the display-ready version of a post" -> GET /posts/{post_id}/display
- "What was posted in the last 24 hours?" -> GET /posts (with date_min set to yesterday)
- "Fetch several posts by their IDs" -> GET /posts/multiple (post_ids=id1,id2)
- "What posts have been added or changed since yesterday?" -> GET /posts/all/changes (date_min, date_max)
- "Get all posts in a date range for archiving" -> GET /posts/all (types, date_min, date_max)
- "Find groups by postal code" -> GET /groups (postal_code param)
- "Show only completed/taken posts from a user" -> GET /users/{user_id}/posts (outcomes filter)

## Response Tips

- **Posts endpoints**: Paginated via `page` and `per_page`. Always pass `types` (offer/wanted) and `sources` (groups/trashnothing) -- these are required even on listing endpoints.
- **Groups endpoints**: Group lookup by ID returns a single object; the list and multiple endpoints return arrays. A 404 on group detail means the group_id is invalid or the group is private.
- **Search endpoints**: Same pagination and filtering as their non-search counterparts; the `search` param is required and matches against post titles/descriptions.
- **Display vs Detail**: `/posts/{post_id}/display` returns HTML-ready content; `/posts/{post_id}` returns raw structured data. A 403 means the post is restricted to group members.
- **Bulk endpoints**: `/posts/multiple` and `/groups/multiple` accept comma-separated IDs and return partial results silently if some IDs are invalid.
- **Changes endpoint**: `/posts/all/changes` returns modifications (edits, status changes, deletions) within a date window -- not new posts.

## Anomaly Flags

- **403 on post access**: The post is group-members-only. Surface this clearly -- the user may need to join the group first.
- **Empty results with location params**: If latitude/longitude/radius returns nothing, suggest widening the radius or checking coordinate accuracy.
- **Missing `types` or `sources`**: These are required on most post endpoints but easy to forget. Flag 400 errors that likely stem from omitting them.
- **Stale date ranges**: If `date_min`/`date_max` span more than 30 days on `/posts/all`, warn about potentially large result sets and pagination overhead.
- **High page numbers with zero results**: Pagination past available data returns empty arrays silently. Flag when a page returns no results to stop further pagination.
- **`include_reposts` defaulting off**: Cross-posted items may be hidden by default. Surface this when result counts seem unexpectedly low.

## Playbook

### 1. Find Free Items Near a Location

1. Call `GET /groups` with `latitude`, `longitude`, and `distance` to discover local groups
2. Collect the returned `group_id` values
3. Call `GET /posts` with `types=offer`, `sources=trashnothing`, `group_ids` set to the discovered IDs, and `latitude`/`longitude`/`radius` for proximity sorting
4. Page through results using `page` and `per_page` until no more results

### 2. Search for a Specific Item

1. Call `GET /posts/search` with `search` set to the item name, `types=offer`, `sources=trashnothing`
2. Optionally add `latitude`, `longitude`, `radius` to limit to nearby results
3. For each interesting result, call `GET /posts/{post_id}/display` to get the full rendered listing
4. If nothing found, widen the radius or try alternate search terms

### 3. Monitor New Posts in a Date Range

1. Determine your last sync timestamp as `date_min`
2. Call `GET /posts/all` with `types=offer`, `date_min`, and `date_max` set to now
3. Page through all results to capture new posts
4. Call `GET /posts/all/changes` with the same date range to catch edits, status changes, and deletions
5. Update your sync timestamp to `date_max`

### 4. Review a User's Posting History

1. Call `GET /users/{user_id}/posts` with `types=offer,wanted`, `sources=trashnothing`
2. Use `sort_by` to order by date and `outcomes` to filter by status (available, taken, etc.)
3. To find something specific, switch to `GET /users/{user_id}/posts/search` with a `search` term
4. Page through with `page`/`per_page` for complete history

### 5. Bulk-Fetch Post and Group Details

1. Collect the IDs you need (from search results, bookmarks, etc.)
2. Call `GET /posts/multiple` with `post_ids` as a comma-separated list to fetch all posts in one request
3. Extract unique group IDs from the returned posts
4. Call `GET /groups/multiple` with those `group_ids` to get group metadata in a single call


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
