---
name: json2video-api
description: "JSON2Video API skill. Use when working with JSON2Video for movies. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# JSON2Video API
API version: 2.0.0

## Auth
No authentication required.

## Base URL
https://api.json2video.com/v2

## Setup
1. No auth setup needed
2. GET /movies -- verify access
3. POST /movies -- create first movies

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### movies
| Method | Path | Description |
|--------|------|-------------|
| GET | /movies | Get the status of your movies |
| POST | /movies | Create a new movie |

## Enhanced Skill Content
## Question Mapping

- "How do I create a video from JSON?" -> POST /movies
- "List all my movies" -> GET /movies
- "What videos have I rendered?" -> GET /movies
- "Generate a video with custom resolution" -> POST /movies (set `resolution`, `width`, `height`)
- "How do I add transitions between scenes?" -> POST /movies (use `scenes[].transition`)
- "Can I create a draft video without rendering?" -> POST /movies (set `draft: true`)
- "How do I set video quality to HD?" -> POST /movies (set `resolution: "hd"`, `quality: "high"`)
- "How do I make an Instagram Story video?" -> POST /movies (set `resolution: "instagram-story"`)
- "Can I cache my rendered video?" -> POST /movies (set `cache: true`, default)
- "How do I add background color to a scene?" -> POST /movies (use `scenes[].background-color`)
- "How do I export the video in different formats?" -> POST /movies (use `exports` array)
- "Can I use variables in my video template?" -> POST /movies (set top-level `variables` and per-scene `scenes[].variables`)
- "How do I check the status of a rendered movie?" -> GET /movies
- "What's the default resolution and FPS?" -> POST /movies defaults: 640x360 custom, 25 fps

## Response Tips

- **GET /movies**: Returns movie objects; check for render status fields -- a movie may still be processing. Paginate by inspecting result count if the response is truncated.
- **POST /movies**: Returns immediately with a movie ID (rendering is async). Store the returned `id` to poll status via GET. A `draft: true` request validates without rendering -- useful for preflight checks.

## Anomaly Flags

- **Long render times**: If GET /movies shows a movie stuck in processing state, surface this -- the video may have failed silently.
- **Missing scenes array**: POST /movies requires at least one scene; flag requests with an empty `scenes` array before sending.
- **Draft mode left on**: If `draft: true` is set, the video won't actually render -- flag this if the user seems to expect a rendered output.
- **Custom resolution without dimensions**: When `resolution: "custom"` (the default), missing or zero `width`/`height` values will likely produce errors -- warn proactively.
- **Cache disabled unnecessarily**: If `cache: false` is set, re-renders will not be cached -- flag if the same payload is sent repeatedly.
- **Low quality + high resolution mismatch**: Flag when `quality: "low"` is paired with `resolution: "full-hd"` as this is typically unintentional.

## Playbook

### 1. Create and Monitor a Simple Video

1. Build a scenes array with at least one scene containing elements (text, images, etc.)
2. POST /movies with `{"scenes": [...], "resolution": "hd", "quality": "high"}`
3. Capture the returned movie `id` from the response
4. Poll GET /movies to check render status until complete
5. Retrieve the final video URL from the completed movie object

### 2. Generate an Instagram Story Video

1. POST /movies with `resolution: "instagram-story"` (9:16 vertical format)
2. Add scenes with appropriate vertical layout elements
3. Set `quality: "high"` and `fps: 25` for smooth playback
4. Monitor render status via GET /movies
5. Use the output URL directly for social upload

### 3. Template-Based Batch Video Generation

1. Design a base movie payload with `variables` as placeholders in scene elements
2. POST /movies with `draft: true` first to validate the template structure
3. Confirm the draft response has no errors
4. For each set of variable values, POST /movies with `draft: false` and the specific `variables` map
5. Collect all returned movie IDs and poll GET /movies to track batch progress

### 4. Preview Before Full Render

1. POST /movies with `draft: true` and your full scene configuration
2. Inspect the response for validation errors or warnings
3. Adjust scenes, transitions, or elements as needed
4. Re-submit with `draft: false` (or omit it, default is `true`) to trigger the actual render
5. Poll GET /movies for the final rendered output


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
