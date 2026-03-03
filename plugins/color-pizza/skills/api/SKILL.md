---
name: color-name-api
description: "Color Name API skill. Use when working with Color Name for root, health, docs. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Color Name API
API version: 1.1.0

## Auth
No authentication required.

## Base URL
https://api.color.pizza/

## Setup
1. No auth setup needed
2. GET / -- verify access

## Endpoints

7 endpoints across 7 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| GET | / | Get API metadata and discovery information |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Health check endpoint |

### docs
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/docs/ | Get API Documentation |

### v1
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/ | Get color names for specific hex values |

### names
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/names/ | Search for colors by name |

### lists
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/lists/ | Get available color name lists |

### swatch
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/swatch/ | Generate a color swatch for any color |

## Enhanced Skill Content
## Question Mapping

- "What is the Color Name API?" -> GET /
- "Is the Color Name API up?" -> GET /health
- "Show me the API documentation" -> GET /v1/docs/
- "What color names are available?" -> GET /v1/names/
- "Give me a list of all colors" -> GET /v1/
- "What color is #ff5733?" -> GET /v1/ (pass hex value as query)
- "Generate a swatch for navy blue" -> GET /v1/swatch/?color=navy+blue
- "Get a swatch image for hex #2a9d8f" -> GET /v1/swatch/?color=2a9d8f
- "What color lists are available?" -> GET /v1/lists/
- "Show me colors from a specific list" -> GET /v1/lists/?list={listName}
- "What is the palette title for a set of colors?" -> GET /v1/
- "Look up a color by name and get its swatch" -> GET /v1/names/ then GET /v1/swatch/?color={hex}
- "What version of the API is running?" -> GET /
- "Where can I find the source code for this API?" -> GET /

## Response Tips

- **Root/Meta (/):** Returns API version, description, and an `endpoints` map linking to all available routes -- use this for discovery.
- **Health (/health):** Returns `status` and ISO 8601 `timestamp`; treat any non-200 or missing `status: "ok"` as degraded.
- **Colors (/v1/):** Returns a `colors` array of maps and a `paletteTitle` string; watch for 400 (bad input), 404 (not found), and 409 (conflict on ambiguous matches).
- **Names (/v1/names/):** Returns a `colors` array of maps; 404 means no matching name was found.
- **Lists (/v1/lists/):** Response shape varies by whether `list` param is provided; 400 means invalid list name, 404 means list not found.
- **Swatch (/v1/swatch/):** Returns image data (not JSON) -- check Content-Type header; 400 means the `color` param was missing or unparseable.

## Anomaly Flags

- **Health degradation:** If `/health` returns non-200 or `status` is anything other than the expected healthy value, surface immediately.
- **409 Conflict on color lookup:** Indicates ambiguous input matching multiple colors -- prompt the user to be more specific.
- **404 on names or lists:** Could indicate a typo or a removed entry -- suggest fuzzy alternatives from `/v1/names/`.
- **400 on swatch:** The `color` parameter is required; flag if the caller omitted it or passed an unparseable format.
- **Unexpected Content-Type:** If `/v1/swatch/` returns JSON instead of an image, the request likely failed -- surface the error body.
- **Missing paletteTitle:** If `/v1/` returns an empty or null `paletteTitle`, the input may not form a coherent palette.

## Playbook

### 1. Look Up a Color by Hex Code

1. Call `GET /v1/?values=ff5733` (pass the hex without the `#` prefix)
2. Read the `colors` array from the response
3. Extract the `name` field from the first match
4. If you get a 404, verify the hex format is valid (6 characters, 0-9/a-f)

### 2. Generate a Color Swatch

1. Call `GET /v1/swatch/?color=ff5733` with the hex value or color name
2. Optionally add `&name=Sunset` to label the swatch
3. The response is an image -- save or display it directly
4. If you get a 400, check that the `color` parameter is present and correctly formatted

### 3. Browse Available Color Lists

1. Call `GET /v1/lists/` to see all available list names
2. Pick a list and call `GET /v1/lists/?list=bestOf` (replace with actual list name)
3. Parse the returned color entries for display or further lookup

### 4. Get All Named Colors

1. Call `GET /v1/names/` to retrieve the full color dictionary
2. Filter the `colors` array client-side by name substring or category
3. For any color of interest, pass its hex to `GET /v1/swatch/?color={hex}` for a visual

### 5. Health Check and API Discovery

1. Call `GET /health` to confirm the API is operational
2. Call `GET /` to retrieve the current version and available endpoints map
3. Use the `endpoints` map to dynamically build links to each feature
4. Optionally visit `GET /v1/docs/` for full human-readable documentation


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
