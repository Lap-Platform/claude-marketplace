---
name: nookipedia
description: "Nookipedia API skill. Use when working with Nookipedia for villagers, nh. Covers 32 endpoints."
version: 1.0.0
generator: lapsh
---

# Nookipedia
API version: 1.7.0

## Auth
ApiKey X-API-KEY in header

## Base URL
https://api.nookipedia.com/

## Setup
1. Set your API key in the appropriate header
2. GET /villagers -- verify access

## Endpoints

32 endpoints across 2 groups. See references/api-spec.lap for full details.

### villagers
| Method | Path | Description |
|--------|------|-------------|
| GET | /villagers | Villagers |

### nh
| Method | Path | Description |
|--------|------|-------------|
| GET | /nh/fish | All New Horizons fish |
| GET | /nh/fish/{fish} | Single New Horizons fish |
| GET | /nh/bugs | All New Horizons bugs |
| GET | /nh/bugs/{bug} | Single New Horizons bug |
| GET | /nh/sea | All New Horizons sea creatures |
| GET | /nh/sea/{sea_creature} | Single New Horizons sea creature |
| GET | /nh/events | All New Horizons events |
| GET | /nh/art | All New Horizons artwork |
| GET | /nh/art/{artwork} | Single New Horizons artwork |
| GET | /nh/furniture | All New Horizons furniture |
| GET | /nh/furniture/{furniture} | Single New Horizons furniture |
| GET | /nh/clothing | All New Horizons clothing |
| GET | /nh/clothing/{clothing} | Single New Horizons clothing |
| GET | /nh/interior | All New Horizons interior items |
| GET | /nh/interior/{item} | Single New Horizons interior item |
| GET | /nh/tools | All New Horizons tools |
| GET | /nh/tools/{tool} | Single New Horizons tool |
| GET | /nh/photos | All New Horizons photos and posters |
| GET | /nh/photos/{item} | Single New Horizons photo or poster |
| GET | /nh/items | Miscellaneous New Horizons items |
| GET | /nh/items/{item} | Single New Horizons miscellaneous item |
| GET | /nh/recipes | All New Horizons recipes |
| GET | /nh/recipes/{item} | Single New Horizons recipe |
| GET | /nh/fossils/individuals | All New Horizons fossils |
| GET | /nh/fossils/individuals/{fossil} | Single New Horizons fossil |
| GET | /nh/fossils/groups | All New Horizons fossil groups |
| GET | /nh/fossils/groups/{fossil_group} | Single New Horizons fossil group |
| GET | /nh/fossils/all | All New Horizons fossil groups or individual fossil |
| GET | /nh/fossils/all/{fossil} | Single New Horizons fossil group with individual fossils |
| GET | /nh/gyroids | All New Horizons gyroids |
| GET | /nh/gyroids/{gyroid} | Single New Horizons gyroid |

## Enhanced Skill Content
## Question Mapping

- "What villagers are in Animal Crossing?" -> GET /villagers
- "Show me all lazy cat villagers" -> GET /villagers?species=cat&personality=lazy
- "Which fish can I catch in July?" -> GET /nh/fish?month=july
- "Tell me about the sea bass" -> GET /nh/fish/{fish}
- "What bugs are available this month?" -> GET /nh/bugs?month={current_month}
- "What sea creatures can I dive for in the southern hemisphere in December?" -> GET /nh/sea?month=december (then filter by south availability)
- "Is there a fake version of the Mona Lisa in the game?" -> GET /nh/art/{artwork}
- "What events are happening in Animal Crossing this month?" -> GET /nh/events?month={month}&year={year}
- "Show me all red furniture" -> GET /nh/furniture?color=red
- "What materials do I need to craft a garden bench?" -> GET /nh/recipes/{item}
- "What fossils are in the T. Rex group?" -> GET /nh/fossils/groups/{fossil_group}
- "How much does a gyroid sell for?" -> GET /nh/gyroids/{gyroid}
- "What formal clothing can I wear to Labelle's shop?" -> GET /nh/clothing?labeltheme=Formal
- "How many uses does a golden axe have?" -> GET /nh/tools/{tool}
- "Which villagers have a birthday in March?" -> GET /villagers?birthmonth=march

## Response Tips

- **Villagers**: Returns a flat array; filter client-side for compound queries (e.g., species + birthday). Use `nhdetails=true` for New Horizons-specific fields.
- **Critters (fish/bugs/sea)**: Single-item endpoints return `north` and `south` hemisphere objects with `availability_array`, `times_by_month` (keyed 1-12), and `months_array`. Always check both hemispheres.
- **Items (furniture/clothing/interior/tools/photos)**: Contain nested `availability`, `buy`, and `variations` arrays of maps. `buy` can have multiple sources; `variations` lists cosmetic options.
- **Art**: Check `has_fake` boolean before accessing `fake_info`. If `has_fake` is false, `fake_info` will be empty or null.
- **Recipes**: `materials` is an array of maps; iterate to build a shopping list. `recipes_to_unlock` indicates how many recipes the player needs before this one becomes available.
- **Fossils**: Three sub-endpoints exist -- `/individuals` for standalone pieces, `/groups` for complete sets, `/all` for a merged view. Use `/all/{fossil}` when unsure which type.
- **Events**: Filter by `date`, `year`, `month`, or `day`; no pagination -- all matching events return in one response.
- **Errors**: 401 means missing or invalid `X-API-KEY`. 404 on detail endpoints means the item name is misspelled or does not exist. 500 is a server-side issue -- retry after a short delay.

## Anomaly Flags

- **401 on any request**: API key is missing, expired, or malformed. Surface immediately and prompt the user to verify their `X-API-KEY` header.
- **404 on detail endpoints**: The item/villager/critter name was not found. Suggest fuzzy alternatives by fetching the list endpoint and matching client-side.
- **Empty availability arrays**: A critter or item returned with an empty `availability_array` likely means it is event-exclusive or unobtainable through normal gameplay. Flag this to the user.
- **`has_fake: true` on art**: Proactively warn the user about forgery differences when looking up artwork, and surface the `fake_info.description` for spotting fakes.
- **Critter not available in current month**: When a user asks about a critter and the current month is not in `months_array` for their hemisphere, proactively note when it next becomes available.
- **`excludedetails` misuse**: If responses seem unexpectedly sparse, check whether `excludedetails` was inadvertently set, stripping nested data.
- **500 errors**: Nookipedia API server issues. Flag as transient and suggest retrying in 30 seconds.

## Playbook

### 1. Find What You Can Catch Right Now

1. Determine the current month and the user's hemisphere (north or south).
2. Call `GET /nh/fish?month={month}` to get available fish.
3. Call `GET /nh/bugs?month={month}` to get available bugs.
4. Call `GET /nh/sea?month={month}` to get available sea creatures.
5. For each result, check the relevant hemisphere's `times_by_month` for the current hour to confirm real-time availability.
6. Present a combined checklist sorted by rarity or sell price.

### 2. Spot Fake Art Before Buying from Redd

1. Call `GET /nh/art` to list all artwork.
2. Filter results where `has_fake` is true.
3. For the specific piece the user is evaluating, call `GET /nh/art/{artwork}`.
4. Compare `real_info.description` vs `fake_info.description` and surface the visual difference.
5. If `has_fake` is false, reassure the user that the piece is always genuine.

### 3. Plan a Crafting Session

1. Identify the item the user wants to craft.
2. Call `GET /nh/recipes/{item}` to retrieve the recipe.
3. Extract the `materials` array and list each material with its required quantity.
4. For each material, call `GET /nh/items/{item}` to check how to obtain it (e.g., shaking trees, hitting rocks).
5. Summarize a shopping list with acquisition methods.

### 4. Build a Themed Room

1. Ask the user for a theme (e.g., "zen", "cute") or HHA category.
2. Call `GET /nh/furniture` and filter by relevant `category` or `color`.
3. Call `GET /nh/interior` for matching rugs, wallpaper, and flooring.
4. For each candidate item, check `hha_base` score to maximize Happy Home Academy points.
5. Present a curated list with buy prices, customization options, and grid dimensions for layout planning.

### 5. Find a Dreamie Villager

1. Ask the user for preferred species, personality, or birthday.
2. Call `GET /villagers` with the relevant filters (e.g., `species=cat&personality=smug`).
3. For each match, note the `game` array to confirm they appear in the user's game version.
4. If the user wants New Horizons details, re-query with `nhdetails=true` for catchphrase, hobby, and house info.
5. Present a shortlist with key traits for the user to choose from.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
