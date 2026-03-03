---
name: tcgdex-api
description: "TCGdex API skill. Use when working with TCGdex for cards, sets, series. Covers 33 endpoints."
version: 1.0.0
generator: lapsh
---

# TCGdex API
API version: 2

## Auth
No authentication required.

## Base URL
https://api.tcgdex.net/v2/{lang}

## Setup
1. No auth setup needed
2. GET /cards -- verify access

## Endpoints

33 endpoints across 16 groups. See references/api-spec.lap for full details.

### cards
| Method | Path | Description |
|--------|------|-------------|
| GET | /cards | fetch the list of cards |
| GET | /cards/{cardId} | Find card by ID |

### sets
| Method | Path | Description |
|--------|------|-------------|
| GET | /sets | Get all sets |
| GET | /sets/{set} | Find set by ID |
| GET | /sets/{set}/{cardLocalId} | Find card by set and local ID |

### series
| Method | Path | Description |
|--------|------|-------------|
| GET | /series | Get all series |
| GET | /series/{serie} | Find series by ID |

### categories
| Method | Path | Description |
|--------|------|-------------|
| GET | /categories | Get all categories |
| GET | /categories/{category} | Get cards by category |

### hp
| Method | Path | Description |
|--------|------|-------------|
| GET | /hp | Get all HP values |
| GET | /hp/{hp} | Get cards by HP value |

### illustrators
| Method | Path | Description |
|--------|------|-------------|
| GET | /illustrators | Get all illustrators |
| GET | /illustrators/{illustrator} | Get cards by illustrator |

### rarities
| Method | Path | Description |
|--------|------|-------------|
| GET | /rarities | Get all rarities |
| GET | /rarities/{rarity} | Get cards by rarity |

### retreats
| Method | Path | Description |
|--------|------|-------------|
| GET | /retreats | Get all retreat costs |
| GET | /retreats/{retreat} | Get cards by retreat cost |

### types
| Method | Path | Description |
|--------|------|-------------|
| GET | /types | Get all types |
| GET | /types/{type} | Get cards by type |

### dex-ids
| Method | Path | Description |
|--------|------|-------------|
| GET | /dex-ids | Get all Pokedex IDs |
| GET | /dex-ids/{dexId} | Get cards by Pokedex ID |

### energy-types
| Method | Path | Description |
|--------|------|-------------|
| GET | /energy-types | Get all energy types |
| GET | /energy-types/{energy-type} | Get cards by energy type |

### regulation-marks
| Method | Path | Description |
|--------|------|-------------|
| GET | /regulation-marks | Get all regulation marks |
| GET | /regulation-marks/{regulation-mark} | Get cards by regulation mark |

### stages
| Method | Path | Description |
|--------|------|-------------|
| GET | /stages | Get all Pokemon stages |
| GET | /stages/{stage} | Get cards by stage |

### suffixes
| Method | Path | Description |
|--------|------|-------------|
| GET | /suffixes | Get all card suffixes |
| GET | /suffixes/{suffix} | Get cards by suffix |

### trainer-types
| Method | Path | Description |
|--------|------|-------------|
| GET | /trainer-types | Get all trainer types |
| GET | /trainer-types/{trainer-type} | Get cards by trainer type |

### variants
| Method | Path | Description |
|--------|------|-------------|
| GET | /variants | Get all card variants |
| GET | /variants/{variant} | Get cards by variant |

## Enhanced Skill Content
## Question Mapping

- "What Pokemon cards are available?" -> GET /cards
- "Show me details for a specific card" -> GET /cards/{cardId}
- "What sets exist in the TCG?" -> GET /sets
- "What cards are in a specific set?" -> GET /sets/{set}
- "Get a specific card from a set by its local ID" -> GET /sets/{set}/{cardLocalId}
- "List all TCG series" -> GET /series
- "What sets belong to a specific series?" -> GET /series/{serie}
- "Find all cards by a specific illustrator" -> GET /illustrators/{illustrator}
- "What rarities exist in the TCG?" -> GET /rarities
- "Show me all cards with a specific HP value" -> GET /hp/{hp}
- "What Pokemon types are available?" -> GET /types
- "Find cards by their Pokedex number" -> GET /dex-ids/{dexId}
- "Which cards have a specific regulation mark?" -> GET /regulation-marks/{regulation-mark}
- "List all card variants (holo, reverse, etc.)" -> GET /variants
- "What energy types exist?" -> GET /energy-types

## Response Tips

- **Cards**: Single card responses contain deeply nested objects (`set`, `variants`, `legal`, `item`, `attacks`, `abilities`); list responses return summary maps -- fetch individual cards for full detail.
- **Sets**: Set detail includes a full `cards` array and nested `serie` object; `cardCount` breaks down by variant type (`normal`, `reverse`, `holo`, `firstEd`), not just `total`/`official`.
- **Series**: Series detail nests `firstSet` and `lastSet` as full set summary objects and includes a `sets` array for all sets in the series.
- **Lookup endpoints** (categories, hp, illustrators, rarities, retreats, types, etc.): All return `{name, cards}` where `cards` is an array of card summary maps; use pagination params to control result size.
- **Pagination**: All list endpoints accept `pagination:page` (default 1) and `pagination:itemsPerPage` (default 100); always check if more pages exist by comparing returned count to `itemsPerPage`.
- **Errors**: 400 means malformed filters or sort params; 404 means the specific resource ID does not exist; 500 is a server-side issue -- retry with backoff.
- **Language**: The `{lang}` path segment in the base URL controls localization (e.g., `en`, `fr`, `ja`) -- all responses reflect the chosen language.

## Anomaly Flags

- **404 on known IDs**: If a card, set, or series ID that previously resolved now returns 404, flag it as possibly removed or renamed in a data update.
- **Empty card arrays**: When a lookup endpoint (e.g., `/hp/300`, `/types/Dragon`) returns `{name, cards: []}`, surface this -- the filter value exists but has no matching cards, which may indicate a data gap or wrong parameter.
- **Pagination overflow**: If the requested page returns zero results but page 1 had data, the user has paginated past the end -- surface a "no more results" notice.
- **Missing optional fields**: Card responses have many optional fields (`hp`, `types`, `evolveFrom`, `abilities`, `attacks`, `variant_detailed`). If a user expects these but they are absent, flag that the card category (e.g., Trainer, Energy) does not carry those fields.
- **Variant discrepancies**: If `variants` shows a variant as `true` but `variant_detailed` is null or empty, flag the inconsistency for investigation.
- **Stale data**: The `updated` field on card responses is a datetime -- if significantly old relative to the set's `releaseDate`, surface that data may not reflect the latest errata.
- **Large result sets**: If a list endpoint returns exactly `itemsPerPage` results, proactively note that more pages likely exist and suggest pagination.

## Playbook

### 1. Build a Complete Set Checklist

1. Call `GET /sets` to browse available sets (use `sort:field=releaseDate&sort:order=DESC` for newest first).
2. Pick a set and call `GET /sets/{set}` to get full details including the `cards` array and `cardCount` breakdown.
3. Iterate through the `cards` array to build your checklist; use `cardCount.official` as the target total.
4. For each card needing full detail, call `GET /cards/{cardId}` or `GET /sets/{set}/{cardLocalId}`.
5. Check `variants` on each card to know which print versions (normal, reverse, holo, first edition) exist.

### 2. Find All Cards for a Specific Pokemon

1. Call `GET /dex-ids` to list available Pokedex numbers if you don't know the exact ID.
2. Call `GET /dex-ids/{dexId}` with the Pokemon's national dex number to get all cards featuring that Pokemon.
3. For each card in the results, call `GET /cards/{cardId}` to get full details including attacks, abilities, and set info.
4. Optionally filter by legality using the `legal.standard` or `legal.expanded` fields on each card.

### 3. Explore an Illustrator's Portfolio

1. Call `GET /illustrators` to list all known illustrators (paginate if needed).
2. Call `GET /illustrators/{illustrator}` with the artist name to get all cards they illustrated.
3. Cross-reference with `GET /cards/{cardId}` on interesting results to see full card data including rarity and set.
4. Use `sort:field=name&sort:order=ASC` to alphabetize results for easier browsing.

### 4. Check Format Legality for a Deck

1. For each card in the deck, call `GET /cards/{cardId}` to retrieve the full card object.
2. Inspect the `legal` field: `legal.standard` for Standard format, `legal.expanded` for Expanded.
3. Check `regulationMark` to understand which rotation the card falls under.
4. If any card shows `false` for the target format, flag it as illegal and suggest alternatives by searching `GET /cards` with appropriate filters.

### 5. Compare Cards Across a Series

1. Call `GET /series/{serie}` to get all sets in the target series.
2. For each set in `sets`, call `GET /sets/{set}` to retrieve the card list.
3. Aggregate cards and use `GET /cards/{cardId}` to pull full stats (HP, attacks, weaknesses, retreat cost).
4. Compare by type using `GET /types/{type}` to find all cards of a given type across the series.
5. Sort and rank by HP, retreat cost, or attack damage for competitive analysis.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
