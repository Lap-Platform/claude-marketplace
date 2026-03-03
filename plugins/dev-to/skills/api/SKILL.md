---
name: forem-api-v1
description: "Forem API V1 API skill. Use when working with Forem API V1 for api. Covers 58 endpoints."
version: 1.0.0
generator: lapsh
---

# Forem API V1
API version: 1.0.0

## Auth
ApiKey api-key in header

## Base URL
https://dev.to/api

## Setup
1. Set your API key in the appropriate header
2. GET /api/articles -- verify access
3. POST /api/articles -- create first articles

## Endpoints

58 endpoints across 1 groups. See references/api-spec.lap for full details.

### api
| Method | Path | Description |
|--------|------|-------------|
| POST | /api/articles | Publish article |
| GET | /api/articles | Published articles |
| GET | /api/articles/latest | Published articles sorted by published date |
| GET | /api/articles/{id} | Published article by id |
| PUT | /api/articles/{id} | Update an article by id |
| GET | /api/articles/{username}/{slug} | Published article by path |
| GET | /api/articles/me | User's articles |
| GET | /api/articles/me/published | User's published articles |
| GET | /api/articles/me/unpublished | User's unpublished articles |
| GET | /api/articles/me/all | User's all articles |
| PUT | /api/articles/{id}/unpublish | Unpublish an article |
| GET | /api/segments | Manually managed audience segments |
| POST | /api/segments | Create a manually managed audience segment |
| GET | /api/segments/{id} | A manually managed audience segment |
| DELETE | /api/segments/{id} | Delete a manually managed audience segment |
| GET | /api/segments/{id}/users | Users in a manually managed audience segment |
| PUT | /api/segments/{id}/add_users | Add users to a manually managed audience segment |
| PUT | /api/segments/{id}/remove_users | Remove users from a manually managed audience segment |
| GET | /api/billboards | Billboards |
| POST | /api/billboards | Create a billboard |
| GET | /api/billboards/{id} | A billboard (by id) |
| PUT | /api/billboards/{id} | Update a billboard by ID |
| PUT | /api/billboards/{id}/unpublish | Unpublish a billboard |
| GET | /api/comments | Comments |
| GET | /api/comments/{id} | Comment by id |
| GET | /api/follows/tags | Followed Tags |
| GET | /api/followers/users | Followers |
| GET | /api/organizations/{username} | An organization (by username) |
| GET | /api/organizations/{organization_id_or_username}/users | Organization's users |
| GET | /api/organizations/{organization_id_or_username}/articles | Organization's Articles |
| GET | /api/organizations | Organizations |
| POST | /api/organizations | Create an Organization |
| GET | /api/organizations/{id} | An organization (by id) |
| PUT | /api/organizations/{id} | Update an organization by id |
| DELETE | /api/organizations/{id} | Delete an Organization by id |
| GET | /api/pages | show details for all pages |
| POST | /api/pages | pages |
| GET | /api/pages/{id} | show details for a page |
| PUT | /api/pages/{id} | update details for a page |
| DELETE | /api/pages/{id} | remove a page |
| GET | /api/podcast_episodes | Podcast Episodes |
| GET | /api/profile_images/{username} | A Users or organizations profile image |
| POST | /api/reactions/toggle | toggle reaction |
| POST | /api/reactions | create reaction |
| GET | /api/readinglist | Readinglist |
| GET | /api/tags | Tags |
| PUT | /api/users/{id}/suspend | Suspend a User |
| PUT | /api/users/{id}/limited | Add limited role for a User |
| DELETE | /api/users/{id}/limited | Remove limited for a User |
| PUT | /api/users/{id}/spam | Add spam role for a User |
| DELETE | /api/users/{id}/spam | Remove spam role from a User |
| PUT | /api/users/{id}/trusted | Add trusted role for a User |
| DELETE | /api/users/{id}/trusted | Remove trusted role from a User |
| GET | /api/users/me | The authenticated user |
| GET | /api/users/{id} | A User |
| PUT | /api/users/{id}/unpublish | Unpublish a User's Articles and Comments |
| POST | /api/admin/users | Invite a User |
| GET | /api/videos | Articles with a video |

## Enhanced Skill Content
## Question Mapping

- "How do I publish a new article on DEV?" -> POST /api/articles
- "Show me the latest articles on DEV" -> GET /api/articles/latest
- "Find articles tagged with javascript and react" -> GET /api/articles?tags=javascript,react&tags_exclude=
- "Get my unpublished drafts" -> GET /api/articles/me/unpublished
- "Update an existing article's title or body" -> PUT /api/articles/{id}
- "Unpublish an article and add a moderation note" -> PUT /api/articles/{id}/unpublish
- "Look up a specific article by author and slug" -> GET /api/articles/{username}/{slug}
- "Who are my followers?" -> GET /api/followers/users
- "React to an article with a unicorn" -> POST /api/reactions/toggle
- "What's in my reading list?" -> GET /api/readinglist
- "Get profile info for a user by ID or username" -> GET /api/users/{id}
- "List all members of an organization" -> GET /api/organizations/{organization_id_or_username}/users
- "Suspend a user account (admin)" -> PUT /api/users/{id}/suspend
- "Create a new organization" -> POST /api/organizations
- "Manage billboard ads" -> GET /api/billboards

## Response Tips

- **Articles**: Lists return arrays paginated via `page`/`per_page` (default 30). No total count header -- keep paging until an empty array is returned. Single-article responses include `body_html` and `body_markdown` as top-level fields.
- **Comments**: Use `a_id` (article ID) or `p_id` (podcast episode ID) to scope comments. Responses are nested trees; child comments appear inside a `children` array on parent objects.
- **Reactions**: Toggle endpoint returns the reaction's current state (`result` field indicates created or destroyed). Idempotent -- calling toggle twice removes the reaction.
- **Users/Orgs**: User lookup accepts both numeric ID and username as a string path param. Organization member lists are paginated the same way as articles.
- **Admin endpoints** (suspend, limited, spam, trusted, unpublish user): Return 204 No Content on success -- do not attempt to parse a response body.
- **Pages**: GET returns both `body_markdown` and `body_json`; one may be null depending on the template type chosen at creation.
- **Segments**: User list sub-resource on segments is paginated via `per_page` only (no `page` param documented); iterate by checking for fewer results than `per_page`.
- **Errors**: 401 means missing or invalid API key. 422 means validation failure -- the response body contains field-level error messages. 404 means the resource does not exist or you lack permission to see it.

## Anomaly Flags

- **401 on any endpoint**: API key is missing, expired, or lacks required scope. Surface immediately -- all subsequent authenticated calls will also fail.
- **422 with field errors**: Parse and display the specific validation failures (e.g., missing title, body too short) rather than a generic error message.
- **404 on user-owned resources** (`/articles/me/*`): May indicate the API key belongs to a different user than expected. Flag the identity mismatch.
- **409 on segment delete**: The segment is in active use. Surface the conflict reason before retrying or suggesting alternatives.
- **Empty page results unexpectedly early**: If page 1 returns fewer items than `per_page`, the dataset is small. If page 1 returns zero items for a filtered query, surface that the filter may be too restrictive.
- **Reaction toggle flip-flopping**: If a toggle call returns "destroyed" when the user expected to add a reaction, warn that the reaction already existed and was removed.
- **Unpublish operations returning 204**: Confirm to the user that the action succeeded since there is no response body to display.
- **Deprecated or removed fields**: If any response includes fields not in the spec (e.g., legacy `flare_tag`), flag them as potentially deprecated and unreliable for long-term use.
- **Rate limiting signals**: If responses start returning 429 or include `Retry-After` headers, surface the throttle immediately and pause further requests.

## Playbook

### 1. Write and Publish an Article

1. Call `POST /api/articles` with `article.title`, `article.body_markdown`, and `article.published: false` to create a draft.
2. Note the returned `id` from the response.
3. Review the draft by calling `GET /api/articles/{id}` and checking `body_html` for rendering issues.
4. When ready, call `PUT /api/articles/{id}` with `article.published: true` to go live.
5. Optionally set `article.series`, `article.tags`, and `article.canonical_url` in the update call.

### 2. Moderate a Problematic User (Admin)

1. Call `GET /api/users/{id}` to confirm the user identity and review their profile.
2. Call `PUT /api/users/{id}/limited` to restrict the user's posting ability as a first step.
3. If the behavior is spam, escalate with `PUT /api/users/{id}/spam` to flag the account.
4. To remove all their published content, call `PUT /api/users/{id}/unpublish`.
5. As a last resort, call `PUT /api/users/{id}/suspend` to fully suspend the account.
6. To reverse any action, use the corresponding `DELETE` endpoint (e.g., `DELETE /api/users/{id}/limited`).

### 3. Build an Organization and Populate Content

1. Call `POST /api/organizations` with `username`, `name`, `summary`, and optional fields like `github_username` and `tech_stack`.
2. Note the returned organization `id`.
3. Publish articles under the org by calling `POST /api/articles` with `article.organization_id` set to the org ID.
4. List the org's articles with `GET /api/organizations/{username}/articles` to verify they appear correctly.
5. View org members via `GET /api/organizations/{username}/users`.

### 4. Manage a Reading List and React to Content

1. Call `GET /api/readinglist?per_page=30` to fetch saved articles.
2. Page through results by incrementing `page` until an empty array is returned.
3. For each interesting article, call `GET /api/articles/{id}` to read the full content.
4. React with `POST /api/reactions/toggle` using `category: "like"`, `reactable_id`, and `reactable_type: "Article"`.
5. To change your reaction, call toggle again with a different `category` (e.g., `"unicorn"`). Note: each category is independent, so toggle the old one off separately if needed.

### 5. Set Up Audience Segments for Targeted Billboards

1. Call `POST /api/segments` to create a new audience segment.
2. Call `PUT /api/segments/{id}/add_users` with a `user_ids` array to populate the segment.
3. Call `POST /api/billboards` to create a new billboard ad unit.
4. Verify the billboard with `GET /api/billboards/{id}`.
5. To retire the campaign, call `PUT /api/billboards/{id}/unpublish`.
6. Clean up by calling `PUT /api/segments/{id}/remove_users` and then `DELETE /api/segments/{id}` if the segment is no longer needed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
