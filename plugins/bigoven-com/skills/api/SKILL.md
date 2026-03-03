---
name: 1000000-recipe-and-grocery-list-api-v2
description: "1,000,000+ Recipe and Grocery List API (v2) API skill. Use when working with 1,000,000+ Recipe and Grocery List API (v2) for collection, collections, grocerylist. Covers 66 endpoints."
version: 1.0.0
generator: lapsh
---

# 1,000,000+ Recipe and Grocery List API (v2)
API version: partner

## Auth
basic | ApiKey X-BigOven-API-Key in header

## Base URL
https://api2.bigoven.com

## Setup
1. Set your API key in the appropriate header
2. GET /collections -- verify access
3. POST /grocerylist/department -- create first department

## Endpoints

66 endpoints across 7 groups. See references/api-spec.lap for full details.

### collection
| Method | Path | Description |
|--------|------|-------------|
| GET | /collection/{id} | Gets a recipe collection. A recipe collection is a curated set of recipes. |
| GET | /collection/{id}/meta | Gets a recipe collection metadata. A recipe collection is a curated set of recipes. |

### collections
| Method | Path | Description |
|--------|------|-------------|
| GET | /collections | Get the list of current, seasonal recipe collections. From here, you can use the /collection/{id} endpoint to retrieve the recipes in those collections. |

### grocerylist
| Method | Path | Description |
|--------|------|-------------|
| POST | /grocerylist/department | Departmentalize a list of strings -- used for ad-hoc grocery list item addition |
| GET | /grocerylist | Get the user's grocery list.  User is determined by Basic Authentication. |
| DELETE | /grocerylist | Delete all the items on a grocery list; faster operation than a sync with deleted items. |
| POST | /grocerylist/recipe | Add a Recipe to the grocery list.  In the request data, pass in recipeId, scale (scale=1.0 says to keep the recipe the same size as originally posted), markAsPending (true/false) to indicate that |
| POST | /grocerylist/line | Add a single line item to the grocery list |
| POST | /grocerylist/item | Add a single line item to the grocery list |
| POST | /grocerylist/sync | Synchronize the grocery list.  Call this with a POST to /grocerylist/sync |
| PUT | /grocerylist/item/{guid} | Update a grocery item by GUID |
| DELETE | /grocerylist/item/{guid} | /grocerylist/item/{guid}  DELETE will delete this item assuming you own it. |
| POST | /grocerylist/clearcheckedlines | Clears the checked lines. |

### recipe
| Method | Path | Description |
|--------|------|-------------|
| GET | /recipe/{recipeId}/images | Get all the images for a recipe. DEPRECATED. Please use /recipe/{recipeId}/photos. |
| GET | /recipe/photos/pending | Gets the pending by user. |
| GET | /recipe/{recipeId}/photos | Get all the photos for a recipe |
| GET | /recipe/{recipeId}/scans | Gets a list of RecipeScan images for the recipe. There will be at most 3 per recipe. |
| POST | /recipe/{recipeId}/image | POST: /recipe/{recipeId}/image?lat=42&amp;lng=21&amp;caption=this%20is%20my%20caption |
| GET | /recipe/{recipeId}/note/{noteId} | Get a given note. Make sure you're passing authentication information in the header for the user who owns the note. |
| PUT | /recipe/{recipeId}/note/{noteId} | HTTP PUT (update) a Recipe note (RecipeNote). |
| DELETE | /recipe/{recipeId}/note/{noteId} | Delete a review |
| GET | /recipe/{recipeId}/notes | recipe/100/notes |
| POST | /recipe/{recipeId}/note | HTTP POST a new note into the system. |
| GET | /recipe/{id}/zap | Zaps the recipe. |
| GET | /recipe/{id} | Return full Recipe detail. Returns 403 if the recipe is owned by someone else. |
| DELETE | /recipe/{id} | Deletes specified recipe (you must be authenticated as the owner of the recipe) |
| GET | /recipe/steps/{id} | Return full Recipe detail with steps. Returns 403 if the recipe is owned by someone else. |
| POST | /recipe/post/step | Stores recipe step number and returns saved step data |
| POST | /recipe/get/step/number | Returns stored step number and number of steps in recipe |
| GET | /recipe/get/active/recipe | Returns last active recipe for the user |
| POST | /recipe/get/saved/step | Gets recipe single step as text |
| GET | /recipe/{recipeId}/related | Get recipes related to the given recipeId |
| POST | /recipe/{recipeId}/feedback | Feedback on a Recipe -- for internal BigOven editors |
| GET | /recipe/categories | Get a list of recipe categories (the ID field can be used for include_cat in search parameters) |
| GET | /recipe/autocomplete | Given a query, return recipe titles starting with query. Query must be at least 3 chars in length. |
| GET | /recipe/autocomplete/mine | Automatics the complete my recipes. |
| GET | /recipe/autocomplete/all | Automatics the complete all recipes. |
| POST | /recipe/scan | POST an image as a new RecipeScan request |
| PUT | /recipe | Update a recipe |
| POST | /recipe | Add a new recipe |
| GET | /recipe/{recipeId}/review/{reviewId} | Get a given review - DEPRECATED. See recipe/review/{reviewId} for the current usage. |
| PUT | /recipe/{recipeId}/review/{reviewId} | HTTP PUT (update) a recipe review. DEPRECATED. Please see recipe/review/{reviewId} PUT for the new endpoint. |
| DELETE | /recipe/{recipeId}/review/{reviewId} | DEPRECATED! - Deletes a review by recipeId and reviewId. Please use recipe/review/{reviewId} instead. |
| GET | /recipe/review/{reviewId} | Get a given review by string-style ID. This will return a payload with FeaturedReply, ReplyCount. |
| PUT | /recipe/review/{reviewId} | Update a given top-level review. |
| GET | /recipe/{recipeId}/review | Get *my* review for the recipe {recipeId}, where "me" is determined by standard authentication headers |
| POST | /recipe/{recipeId}/review | Add a new review. Only one review can be provided per {userId, recipeId} pair. Otherwise your review will be updated. |
| GET | /recipe/{recipeId}/reviews | Get paged list of reviews for a recipe. Each review will have at most one FeaturedReply, as well as a ReplyCount. |
| GET | /recipe/review/{reviewId}/replies | Get a paged list of replies for a given review. |
| POST | /recipe/review/{reviewId}/replies | POST a reply to a given review. The date will be set by server. Note that replies no longer have star ratings, only top-level reviews do. |
| PUT | /recipe/review/replies/{replyId} | Update (PUT) a reply to a given review. Authenticated user must be the original one that posted the reply. |
| DELETE | /recipe/review/replies/{replyId} | DELETE a reply to a given review. Authenticated user must be the one who originally posted the reply. |

### image
| Method | Path | Description |
|--------|------|-------------|
| POST | /image/avatar | POST: /image/avatar |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /me | Indexes this instance. |
| PUT | /me | Puts me. |
| GET | /me/skinny | Skinnies this instance. |
| GET | /me/preferences/options | Gets the options. |
| PUT | /me/profile | Puts me. |
| PUT | /me/personal | Puts me personal. |
| PUT | /me/preferences | Puts me preferences. |

### recipes
| Method | Path | Description |
|--------|------|-------------|
| GET | /recipes/raves | Get the recipe/comment tuples for those recipes with 4 or 5 star ratings |
| GET | /recipes/{id} | Same as GET recipe but also includes the recipe videos (if any) |
| GET | /recipes/random | Get a random, home-page-quality Recipe. |
| GET | /recipes/top25random | Search for recipes. There are many parameters that you can apply. Starting with the most common, use title_kw to search within a title. |
| GET | /recipes | Search for recipes. There are many parameters that you can apply. Starting with the most common, use title_kw to search within a title. |
| GET | /recipes/recentviews | Get a list of recipes that the authenticated user has most recently viewed |

## Enhanced Skill Content
## Question Mapping

- "How do I search for recipes by ingredient?" -> GET /recipes (use `include_ing` param)
- "What's a random recipe I can make tonight?" -> GET /recipes/random
- "Show me the details for a specific recipe" -> GET /recipe/{id}
- "How do I add a recipe's ingredients to my grocery list?" -> POST /grocerylist/recipe
- "What's on my grocery list?" -> GET /grocerylist
- "How do I check off items on my grocery list?" -> POST /grocerylist/clearcheckedlines
- "Can I find gluten-free vegetarian recipes?" -> GET /recipes (combine `glf=1` and `vtn=1`)
- "How do I leave a review on a recipe?" -> POST /recipe/{recipeId}/review
- "What recipes have I looked at recently?" -> GET /recipes/recentviews
- "How do I update my profile?" -> PUT /me/profile
- "What are the top-rated recipes?" -> GET /recipes/raves
- "How do I add a personal note to a recipe?" -> POST /recipe/{recipeId}/note
- "Can I upload a photo of a dish I made?" -> POST /recipe/{recipeId}/image
- "How do I delete a recipe I created?" -> DELETE /recipe/{id}
- "What recipes are related to one I like?" -> GET /recipe/{recipeId}/related

## Response Tips

- **Recipes/Collections** (`GET /recipes`, `/collections`, `/collection/{id}`): Paginated via `pg` (page) and `rpp` (results per page) -- always check if more pages exist before stopping iteration.
- **Grocery list** (`GET /grocerylist`): Returns line items with GUIDs -- use these GUIDs for update (`PUT`) and delete (`DELETE`) operations, not positional indices.
- **Recipe detail** (`GET /recipe/{id}`): Use `prefetch=true` to inline related data; without it, images/notes/reviews require separate calls.
- **Reviews/Notes** (`GET .../reviews`, `.../notes`): Paginated; nested replies on reviews require a separate call to `/recipe/review/{reviewId}/replies`.
- **Search filters**: Dietary flags (`vtn`, `vgn`, `glf`, `ntf`, `dyf`, `sff`, `slf`, `tnf`, `wmf`, `rmf`, `cps`) are binary toggles -- combine freely for intersection filtering.
- **Errors**: 401 means missing or invalid API key/auth; 403 means you lack ownership of the resource; 415 appears on image uploads with wrong content type.

## Anomaly Flags

- **401 on write operations**: Surface immediately -- likely an expired or missing API key. Prompt user to verify `X-BigOven-API-Key` header or Basic auth credentials.
- **403 on recipe delete/access**: User does not own the recipe. Flag clearly rather than retrying.
- **415 on image/scan uploads**: Wrong content type. Alert user to check that the request body is multipart form data with a valid image MIME type.
- **402 on recipe scan**: Payment required -- the user's account tier may not support OCR scanning. Surface the upgrade requirement.
- **Empty paginated results unexpectedly**: If `pg` exceeds available pages, the API may return empty rather than an error. Flag when a non-first page returns zero results.
- **Grocery list sync conflicts**: `POST /grocerylist/sync` can produce merge issues. Surface any discrepancies between local and server state after sync.
- **Deprecated `GET /recipe/{id}` vs `GET /recipes/{id}`**: Two similar endpoints exist with different error handling (the plural form returns 400/403/404/500). Flag if the singular form silently returns stale or incomplete data.

## Playbook

### 1. Search and Save a Recipe to Grocery List

1. Search for recipes: `GET /recipes?any_kw=chicken&glf=1&rpp=10&pg=1`
2. Browse results, pick a recipe ID from the response
3. Fetch full details: `GET /recipe/{recipeId}`
4. Review ingredients, then add to grocery list: `POST /grocerylist/recipe` with `{ recipeId: ... }`
5. Verify grocery list: `GET /grocerylist`

### 2. Review and Rate a Recipe

1. Fetch the recipe: `GET /recipe/{recipeId}`
2. Check existing reviews: `GET /recipe/{recipeId}/reviews?pg=1&rpp=5`
3. Post your review: `POST /recipe/{recipeId}/review` with rating and comment in the body
4. Optionally reply to another review: `POST /recipe/review/{reviewId}/replies` with your reply data

### 3. Manage Your Grocery List

1. View current list: `GET /grocerylist`
2. Add a standalone item: `POST /grocerylist/item` with item details
3. Update an item (e.g., change quantity): `PUT /grocerylist/item/{guid}` with updated fields
4. Clear all checked-off items after shopping: `POST /grocerylist/clearcheckedlines`
5. To start fresh: `DELETE /grocerylist`

### 4. Create and Publish a New Recipe

1. Check available categories: `GET /recipe/categories`
2. Create the recipe: `POST /recipe` with full recipe map (title, ingredients, instructions, category)
3. Upload a hero image: `POST /recipe/{recipeId}/image` with the photo file and optional caption
4. Add personal notes: `POST /recipe/{recipeId}/note` with note content
5. Verify it appears: `GET /recipe/{recipeId}`

### 5. Discover Recipes for Meal Planning

1. Get random inspiration: `GET /recipes/random` or `GET /recipes/top25random`
2. Filter by dietary needs: `GET /recipes?vgn=1&maxIngredients=8&totalMins=30&rpp=10`
3. Check related recipes for variety: `GET /recipe/{recipeId}/related?rpp=5`
4. Review recently viewed recipes: `GET /recipes/recentviews?pg=1&rpp=10`
5. Bulk-add selected recipes to grocery list: repeat `POST /grocerylist/recipe` for each chosen recipe


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
