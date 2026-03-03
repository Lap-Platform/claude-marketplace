---
name: notion-api
description: "Notion API skill. Use when working with Notion for users, search, blocks. Covers 22 endpoints."
version: 1.0.0
generator: lapsh
---

# Notion API
API version: 2.0.0

## Auth
Bearer bearer | Bearer basic

## Base URL
https://api.notion.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /v1/users -- verify access
3. POST /v1/search -- create first search

## Endpoints

22 endpoints across 7 groups. See references/api-spec.lap for full details.

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/users/{user_id} | Retrieve a user |
| GET | /v1/users | List all users |
| GET | /v1/users/me | Retrieve your token's bot user |

### search
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/search | Search by title |

### blocks
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/blocks/{block_id}/children | Retrieve block children |
| PATCH | /v1/blocks/{block_id}/children | Append block children |
| GET | /v1/blocks/{block_id} | Retrieve a block |
| PATCH | /v1/blocks/{block_id} | Update a block |
| DELETE | /v1/blocks/{block_id} | Delete a block |

### pages
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/pages/{page_id} | Retrieve a page |
| PATCH | /v1/pages/{page_id} | Update page properties |
| POST | /v1/pages | Create a page |
| GET | /v1/pages/{page_id}/properties/{property_id} | Retrieve a page property item |
| POST | /v1/pages/{page_id}/move | Move a page |

### comments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/comments | Retrieve comments |
| POST | /v1/comments | Create comment |

### data_sources
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/data_sources/{data_source_id}/query | Query a data source |
| GET | /v1/data_sources/{data_source_id} | Retrieve a data source |
| PATCH | /v1/data_sources/{data_source_id} | Update a data source |
| POST | /v1/data_sources | Create a data source |
| GET | /v1/data_sources/{data_source_id}/templates | List templates in a data source |

### databases
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/databases/{database_id} | Retrieve a database |

## Enhanced Skill Content
## Question Mapping

- "Who am I authenticated as?" -> GET /v1/users/me
- "Get details about a specific user" -> GET /v1/users/{user_id}
- "List all users in the workspace" -> GET /v1/users
- "Search for a page or database by name" -> POST /v1/search
- "Get the contents of a page" -> GET /v1/blocks/{block_id}/children
- "Add content blocks to a page" -> PATCH /v1/blocks/{block_id}/children
- "Create a new page in a database" -> POST /v1/pages
- "Update a page's properties or icon" -> PATCH /v1/pages/{page_id}
- "Move a page to a different parent" -> POST /v1/pages/{page_id}/move
- "Query a database with filters and sorts" -> POST /v1/data_sources/{data_source_id}/query
- "Get a database schema and its properties" -> GET /v1/data_sources/{data_source_id}
- "Create a new database inside a page" -> POST /v1/data_sources
- "Read comments on a page or block" -> GET /v1/comments
- "Add a comment to a page" -> POST /v1/comments
- "Delete a block from a page" -> DELETE /v1/blocks/{block_id}

## Response Tips

- **Users**: Response includes `type` field (`person` or `bot`) -- check this before accessing nested `person` or `bot` objects.
- **Search**: Results are polymorphic (`object` field is `page` or `database`); always check `object` before parsing properties.
- **Blocks**: Children responses are paginated; `has_more: true` means you must follow `next_cursor`. Block `type` field determines which nested object holds the content.
- **Pages**: Property values are wrapped in type-specific objects (e.g., `title`, `rich_text`, `number`); use `property.type` to pick the right accessor.
- **Comments**: Flat list of `rich_text` arrays; each comment has a `created_by` user reference.
- **Data Sources / Databases**: Query results return `results[]` with full page objects; schema lives in the `properties` map of the data source itself.

## Anomaly Flags

- **Rate limiting**: Notion returns `429` with `Retry-After` header -- surface this immediately and back off before retrying.
- **Notion-Version drift**: The spec pins `2025-09-03`. If responses include unfamiliar fields or deprecated warnings in headers, flag the version mismatch.
- **Partial results**: Any paginated response with `has_more: true` but fewer results than `page_size` may indicate server-side filtering -- warn the user that not all items were returned.
- **Archived/trashed items**: Pages and blocks can be `archived: true` or `in_trash: true` -- surface these states so users don't unknowingly edit soft-deleted content.
- **Empty search results**: If `POST /v1/search` returns zero results for a term the user expects to find, flag that search only covers pages/databases the integration has access to (not all workspace content).
- **Bot user ownership**: `GET /v1/users/me` returns `bot.owner` -- if `owner.type` is `workspace` vs `user`, integration permissions differ significantly. Flag this on first call.

## Playbook

### 1. Find and read a page by title

1. Call `POST /v1/search` with `query` set to the page title and `filter: {value: "page", property: "object"}`.
2. Pick the best match from `results[]` by comparing `properties.title` text content.
3. Call `GET /v1/blocks/{page_id}/children` using the matched page's `id`.
4. If `has_more` is `true`, paginate with `start_cursor` until all blocks are retrieved.
5. Recursively fetch children for any block that `has_children: true`.

### 2. Create a database entry (row) with properties

1. Call `GET /v1/data_sources/{database_id}` to retrieve the schema and inspect `properties` for field names and types.
2. Build the `properties` map matching each field's type (e.g., `title`, `rich_text`, `number`, `select`).
3. Call `POST /v1/pages` with `parent: {database_id: "..."}` and the constructed `properties`.
4. Verify the response contains the new page `id` and expected property values.

### 3. Query a database with filtering and sorting

1. Call `GET /v1/data_sources/{database_id}` to confirm available properties and their types.
2. Build a `filter` object using compound filters (`and`/`or`) referencing property names and type-specific conditions.
3. Build a `sorts` array with `{property: "Name", direction: "ascending"}` entries.
4. Call `POST /v1/data_sources/{database_id}/query` with `filter`, `sorts`, and `page_size`.
5. Paginate using `start_cursor` from each response until `has_more` is `false`.

### 4. Append content to an existing page

1. Call `GET /v1/blocks/{page_id}/children` to see existing content and find the last block's `id`.
2. Build a `children` array of block objects (e.g., `{type: "paragraph", paragraph: {rich_text: [{text: {content: "..."}}]}}`).
3. Call `PATCH /v1/blocks/{page_id}/children` with the `children` array. Optionally set `after` to a block `id` to insert at a specific position.
4. Confirm the response includes the newly created block objects with their assigned `id` values.

### 5. Add a comment and verify it was posted

1. Identify the target page's `id` (search for it if needed via `POST /v1/search`).
2. Call `POST /v1/comments` with `parent: {page_id: "..."}` and `rich_text: [{text: {content: "Your comment"}}]`.
3. Confirm the response includes the comment's `id` and `created_time`.
4. Call `GET /v1/comments` with `block_id` set to the page `id` to verify the comment appears in the list.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
