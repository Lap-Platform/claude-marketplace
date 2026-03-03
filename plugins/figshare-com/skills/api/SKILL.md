---
name: figshare-api
description: "Figshare API skill. Use when working with Figshare for token, articles, account. Covers 151 endpoints."
version: 1.0.0
generator: lapsh
---

# Figshare API
API version: 2.0.0

## Auth
OAuth2

## Base URL
https://api.figshare.com/v2

## Setup
1. Configure auth: OAuth2
2. GET /token -- verify access
3. POST /token -- create first token

## Endpoints

151 endpoints across 11 groups. See references/api-spec.lap for full details.

### token
| Method | Path | Description |
|--------|------|-------------|
| GET | /token | Get OAuth token information |
| POST | /token | Create OAuth token |

### articles
| Method | Path | Description |
|--------|------|-------------|
| GET | /articles | Public Articles |
| POST | /articles/search | Public Articles Search |
| GET | /articles/{article_id} | View article details |
| GET | /articles/{article_id}/versions | List article versions |
| GET | /articles/{article_id}/versions/{version_id} | Article details for version |
| GET | /articles/{article_id}/versions/{version_id}/files | Article version file details |
| GET | /articles/{article_id}/download | Public Article Download |
| GET | /articles/{article_id}/versions/{version_id}/download | Public Article Version Download |
| GET | /articles/{article_id}/versions/{version_id}/embargo | Public Article Embargo for article version |
| GET | /articles/{article_id}/versions/{version_id}/confidentiality | Public Article Confidentiality for article version |
| GET | /articles/{article_id}/files | List article files |
| GET | /articles/{article_id}/files/{file_id} | Article file details |

### account
| Method | Path | Description |
|--------|------|-------------|
| POST | /account/articles/search | Private Articles search |
| GET | /account/articles | Private Articles |
| POST | /account/articles | Create new Article |
| GET | /account/articles/{article_id} | Article details |
| PUT | /account/articles/{article_id} | Update article |
| PATCH | /account/articles/{article_id} | Partially update article |
| DELETE | /account/articles/{article_id} | Delete article |
| GET | /account/articles/{article_id}/embargo | Article Embargo Details |
| PUT | /account/articles/{article_id}/embargo | Update Article Embargo |
| DELETE | /account/articles/{article_id}/embargo | Delete Article Embargo |
| POST | /account/articles/{article_id}/resource | Private Article Resource |
| POST | /account/articles/{article_id}/publish | Private Article Publish |
| POST | /account/articles/{article_id}/unpublish | Public Article Unpublish |
| POST | /account/articles/{article_id}/reserve_doi | Private Article Reserve DOI |
| POST | /account/articles/{article_id}/reserve_handle | Private Article Reserve Handle |
| GET | /account/articles/{article_id}/download | Private Article Download |
| PUT | /account/articles/{article_id}/versions/{version_id} | Update article version |
| PATCH | /account/articles/{article_id}/versions/{version_id} | Partially update article version |
| PUT | /account/articles/{article_id}/versions/{version_id}/update_thumb | Update article version thumbnail |
| GET | /account/articles/{article_id}/authors | List article authors |
| POST | /account/articles/{article_id}/authors | Add article authors |
| PUT | /account/articles/{article_id}/authors | Replace article authors |
| DELETE | /account/articles/{article_id}/authors/{author_id} | Delete article author |
| GET | /account/articles/{article_id}/categories | List article categories |
| POST | /account/articles/{article_id}/categories | Add article categories |
| PUT | /account/articles/{article_id}/categories | Replace article categories |
| DELETE | /account/articles/{article_id}/categories/{category_id} | Delete article category |
| GET | /account/articles/{article_id}/confidentiality | Article confidentiality details |
| PUT | /account/articles/{article_id}/confidentiality | Update article confidentiality |
| DELETE | /account/articles/{article_id}/confidentiality | Delete article confidentiality |
| GET | /account/articles/{article_id}/private_links | List private links |
| POST | /account/articles/{article_id}/private_links | Create private link |
| PUT | /account/articles/{article_id}/private_links/{link_id} | Update private link |
| DELETE | /account/articles/{article_id}/private_links/{link_id} | Disable private link |
| GET | /account/articles/{article_id}/files | List article files |
| POST | /account/articles/{article_id}/files | Initiate Upload |
| GET | /account/articles/{article_id}/files/{file_id} | Single File |
| POST | /account/articles/{article_id}/files/{file_id} | Complete Upload |
| DELETE | /account/articles/{article_id}/files/{file_id} | File Delete |
| GET | /account/articles/export | Account Article Report |
| POST | /account/articles/export | Initiate a new Report |
| GET | /account/collections | Private Collections List |
| POST | /account/collections | Create collection |
| GET | /account/collections/{collection_id} | Collection details |
| PUT | /account/collections/{collection_id} | Update collection |
| PATCH | /account/collections/{collection_id} | Partially update collection |
| DELETE | /account/collections/{collection_id} | Delete collection |
| POST | /account/collections/search | Private Collections Search |
| POST | /account/collections/{collection_id}/reserve_doi | Private Collection Reserve DOI |
| POST | /account/collections/{collection_id}/reserve_handle | Private Collection Reserve Handle |
| POST | /account/collections/{collection_id}/resource | Private Collection Resource |
| POST | /account/collections/{collection_id}/publish | Private Collection Publish |
| GET | /account/collections/{collection_id}/authors | List collection authors |
| POST | /account/collections/{collection_id}/authors | Add collection authors |
| PUT | /account/collections/{collection_id}/authors | Replace collection authors |
| DELETE | /account/collections/{collection_id}/authors/{author_id} | Delete collection author |
| GET | /account/collections/{collection_id}/categories | List collection categories |
| POST | /account/collections/{collection_id}/categories | Add collection categories |
| PUT | /account/collections/{collection_id}/categories | Replace collection categories |
| DELETE | /account/collections/{collection_id}/categories/{category_id} | Delete collection category |
| GET | /account/collections/{collection_id}/articles | List collection articles |
| POST | /account/collections/{collection_id}/articles | Add collection articles |
| PUT | /account/collections/{collection_id}/articles | Replace collection articles |
| DELETE | /account/collections/{collection_id}/articles/{article_id} | Delete collection article |
| GET | /account/collections/{collection_id}/private_links | List collection private links |
| POST | /account/collections/{collection_id}/private_links | Create collection private link |
| GET | /account/collections/{collection_id}/private_links/{link_id} | View collection private link |
| PUT | /account/collections/{collection_id}/private_links/{link_id} | Update collection private link |
| DELETE | /account/collections/{collection_id}/private_links/{link_id} | Disable private link |
| POST | /account/projects/search | Private Projects search |
| GET | /account/projects | Private Projects |
| POST | /account/projects | Create project |
| GET | /account/projects/{project_id} | View project details |
| PUT | /account/projects/{project_id} | Update project |
| PATCH | /account/projects/{project_id} | Partially update project |
| DELETE | /account/projects/{project_id} | Delete project |
| POST | /account/projects/{project_id}/publish | Private Project Publish |
| GET | /account/projects/{project_id}/notes | List project notes |
| POST | /account/projects/{project_id}/notes | Create project note |
| GET | /account/projects/{project_id}/notes/{note_id} | Project note details |
| PUT | /account/projects/{project_id}/notes/{note_id} | Update project note |
| DELETE | /account/projects/{project_id}/notes/{note_id} | Delete project note |
| POST | /account/projects/{project_id}/leave | Private Project Leave |
| GET | /account/projects/{project_id}/collaborators | List project collaborators |
| POST | /account/projects/{project_id}/collaborators | Invite project collaborators |
| DELETE | /account/projects/{project_id}/collaborators/{user_id} | Remove project collaborator |
| GET | /account/projects/{project_id}/articles | List project articles |
| POST | /account/projects/{project_id}/articles | Create project article |
| GET | /account/projects/{project_id}/articles/{article_id} | Project article details |
| DELETE | /account/projects/{project_id}/articles/{article_id} | Delete project article |
| GET | /account/projects/{project_id}/articles/{article_id}/files | Project article list files |
| GET | /account/projects/{project_id}/articles/{article_id}/files/{file_id} | Project article file details |
| POST | /account/authors/search | Search Authors |
| GET | /account/authors/{author_id} | Author details |
| POST | /account/funding/search | Search Funding |
| GET | /account | Private Account information |
| GET | /account/licenses | Private Account Licenses |
| GET | /account/institution | Private Account Institutions |
| GET | /account/institution/embargo_options | Private Account Institution embargo options |
| GET | /account/institution/articles | Private Institution Articles |
| GET | /account/institution/custom_fields | Private account institution group custom fields |
| POST | /account/institution/custom_fields/{custom_field_id}/items/upload | Custom fields values files upload |
| GET | /account/categories | Private Account Categories |
| GET | /account/institution/groups | Private Account Institution Groups |
| GET | /account/institution/groups/{group_id}/embargo_options | Private Account Institution Group Embargo Options |
| GET | /account/institution/roles | Private Account Institution Roles |
| GET | /account/institution/accounts | Private Account Institution Accounts |
| POST | /account/institution/accounts | Create new Institution Account |
| GET | /account/institution/accounts/{account_id} | Private Institution Account information |
| PUT | /account/institution/accounts/{account_id} | Update Institution Account |
| GET | /account/institution/roles/{account_id} | List Institution Account Group Roles |
| POST | /account/institution/roles/{account_id} | Add Institution Account Group Roles |
| DELETE | /account/institution/roles/{account_id}/{group_id}/{role_id} | Delete Institution Account Group Role |
| POST | /account/institution/accounts/search | Private Account Institution Accounts Search |
| GET | /account/institution/users/{account_id} | Private Account Institution User |
| GET | /account/institution/reviews | Institution Curation Reviews |
| GET | /account/institution/review/{curation_id} | Institution Curation Review |
| GET | /account/institution/review/{curation_id}/comments | Institution Curation Review Comments |
| POST | /account/institution/review/{curation_id}/comments | POST Institution Curation Review Comment |
| PUT | /account/profile | Update public profile |
| POST | /account/profile/{user_id}/picture | Update public profile picture |

### collections
| Method | Path | Description |
|--------|------|-------------|
| GET | /collections | Public Collections |
| POST | /collections/search | Public Collections Search |
| GET | /collections/{collection_id} | Collection details |
| GET | /collections/{collection_id}/versions | Collection Versions list |
| GET | /collections/{collection_id}/versions/{version_id} | Collection Version details |
| GET | /collections/{collection_id}/articles | Public Collection Articles |

### item_types
| Method | Path | Description |
|--------|------|-------------|
| GET | /item_types | Item Types |

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects | Public Projects |
| POST | /projects/search | Public Projects Search |
| GET | /projects/{project_id} | Public Project |
| GET | /projects/{project_id}/articles | Public Project Articles |

### institutions
| Method | Path | Description |
|--------|------|-------------|
| GET | /institutions/{institution_string_id}/articles/filter-by | Public Institution Articles |

### categories
| Method | Path | Description |
|--------|------|-------------|
| GET | /categories | Public Categories |

### licenses
| Method | Path | Description |
|--------|------|-------------|
| GET | /licenses | Public Licenses |

### institution
| Method | Path | Description |
|--------|------|-------------|
| POST | /institution/hrfeed/upload | Private Institution HRfeed Upload |

### file
| Method | Path | Description |
|--------|------|-------------|
| GET | /file/download/{file_id} | Public File Download |

## Enhanced Skill Content
## Question Mapping

- "How do I search for published articles on Figshare?" -> POST /articles/search
- "What are the details of a specific article?" -> GET /articles/{article_id}
- "How do I list all my draft articles?" -> GET /account/articles
- "How do I upload a new article to my account?" -> POST /account/articles
- "How do I publish an article draft?" -> POST /account/articles/{article_id}/publish
- "How do I download a file from an article?" -> GET /file/download/{file_id}
- "What versions exist for this article?" -> GET /articles/{article_id}/versions
- "How do I add authors to my article?" -> POST /account/articles/{article_id}/authors
- "How do I create a collection and add articles to it?" -> POST /account/collections then POST /account/collections/{collection_id}/articles
- "How do I reserve a DOI before publishing?" -> POST /account/articles/{article_id}/reserve_doi
- "How do I set an embargo on my article?" -> PUT /account/articles/{article_id}/embargo
- "How do I share a private link to an unpublished article?" -> POST /account/articles/{article_id}/private_links
- "How do I manage collaborators on a project?" -> POST /account/projects/{project_id}/collaborators
- "How do I find articles within my institution?" -> GET /account/institution/articles
- "How do I review and comment on a curation item?" -> GET /account/institution/review/{curation_id} then POST /account/institution/review/{curation_id}/comments

## Response Tips

- **Listings** (articles, collections, projects): Paginated via `page`/`page_size` or `offset`/`limit`; use `X-Cursor` header for cursor-based pagination on large result sets. Empty arrays mean no more results.
- **Search results**: Same pagination as listings; the response is an array of summary objects -- fetch individual IDs for full metadata.
- **Mutative writes** (PUT/PATCH): Return 205 Reset Content with no body -- do not attempt to parse a response object. POST creates return 201 with a `location` field.
- **Deletes**: Return 204 No Content -- success means empty body.
- **File endpoints**: `POST /account/articles/{article_id}/files` returns 201 with upload token/URL; `POST .../files/{file_id}` (202) signals async processing -- poll the file endpoint until status is complete.
- **Error bodies**: 400 = malformed request (check required fields), 403 = missing/invalid OAuth token, 404 = resource not found or not owned, 422 = validation failure (check field constraints), 500 = server-side issue (retry with backoff).

## Anomaly Flags

- **429 on export**: `POST /account/articles/export` is the only endpoint returning 429 -- surface rate limit warnings and suggest waiting before retry.
- **202 on file upload completion**: `POST /account/articles/{article_id}/files/{file_id}` returns 202 (accepted, not done) -- alert the user that file processing is async and they should poll for status.
- **205 without body**: Many update endpoints return 205 -- flag if the caller tries to read a response body (there is none).
- **Embargo and confidentiality conflicts**: Setting both embargo and confidentiality on the same article can produce unexpected visibility states -- warn when both are configured.
- **Missing OAuth on account routes**: All `/account/*` endpoints require OAuth2 -- surface a clear error if a 403 comes back on any account operation suggesting token refresh or re-auth.
- **Unpublish requires reason**: `POST /account/articles/{article_id}/unpublish` requires a reason body -- flag if the caller omits it.
- **409 on custom field upload**: `POST /account/institution/custom_fields/{custom_field_id}/items/upload` can return 409 Conflict -- surface duplicate data warnings.

## Playbook

### 1. Create and Publish an Article

1. `POST /account/articles` with title, description, and item type to create a draft (returns 201 with article location)
2. `POST /account/articles/{article_id}/files` to initiate file upload (returns upload token)
3. `POST /account/articles/{article_id}/files/{file_id}` to complete the upload (returns 202; poll `GET .../files/{file_id}` until processed)
4. `POST /account/articles/{article_id}/authors` to add co-authors
5. `POST /account/articles/{article_id}/categories` to assign categories
6. `POST /account/articles/{article_id}/reserve_doi` to get a DOI before publishing
7. `POST /account/articles/{article_id}/publish` to make it public (returns 201)

### 2. Build and Publish a Collection

1. `POST /account/collections` with title and description (returns 201)
2. `POST /account/collections/{collection_id}/articles` to add existing article IDs
3. `POST /account/collections/{collection_id}/authors` to credit contributors
4. `POST /account/collections/{collection_id}/categories` to classify the collection
5. `POST /account/collections/{collection_id}/reserve_doi` to reserve a DOI
6. `POST /account/collections/{collection_id}/publish` to make it public

### 3. Search and Download Public Data

1. `POST /articles/search` with keywords, filters (institution, item_type, published_since) to find articles
2. `GET /articles/{article_id}` on a result to get full metadata including file list
3. `GET /articles/{article_id}/files` to list all attached files with download URLs
4. `GET /file/download/{file_id}` to download a specific file
5. Alternatively, `GET /articles/{article_id}/download` to get the full article bundle

### 4. Manage a Research Project with Collaborators

1. `POST /account/projects` with title and funding info (returns 201)
2. `POST /account/projects/{project_id}/collaborators` to invite team members by user ID
3. `POST /account/projects/{project_id}/articles` to create articles within the project
4. `POST /account/projects/{project_id}/notes` to add internal research notes
5. `POST /account/projects/{project_id}/publish` when the project is ready for public release

### 5. Institutional Curation Review

1. `GET /account/institution/reviews` with optional `status` filter to list pending items
2. `GET /account/institution/review/{curation_id}` to inspect a specific submission
3. `GET /account/institution/review/{curation_id}/comments` to read existing reviewer feedback
4. `POST /account/institution/review/{curation_id}/comments` to add your review comment or approval decision


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
