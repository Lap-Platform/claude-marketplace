---
name: annotations-api
description: "Annotations API skill. Use when working with Annotations for projects. Covers 7 endpoints."
version: 1.0.0
generator: lapsh
---

# Annotations API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
Not specified.

## Setup
1. No auth setup needed
2. GET /projects/{projectId}/annotations -- verify access
3. POST /projects/{projectId}/annotations -- create first annotations

## Endpoints

7 endpoints across 1 groups. See references/api-spec.lap for full details.

### projects
| Method | Path | Description |
|--------|------|-------------|
| GET | /projects/{projectId}/annotations | List Annotations |
| POST | /projects/{projectId}/annotations | Create Annotations |
| GET | /projects/{projectId}/annotations/{annotationId} | Get Annotation |
| PATCH | /projects/{projectId}/annotations/{annotationId} | Patch Annotation |
| DELETE | /projects/{projectId}/annotations/{annotationId} | Delete Annotation |
| GET | /projects/{projectId}/annotations/tags | Get Annotation Tags |
| POST | /projects/{projectId}/annotations/tags | Create Annotation Tag |

## Enhanced Skill Content
## Question Mapping

- "What annotations exist for this project?" -> GET /projects/{projectId}/annotations
- "Show me a specific annotation" -> GET /projects/{projectId}/annotations/{annotationId}
- "Add a note to my project" -> POST /projects/{projectId}/annotations
- "Create an annotation with tags" -> POST /projects/{projectId}/annotations
- "Update the description of an annotation" -> PATCH /projects/{projectId}/annotations/{annotationId}
- "Change the tags on an annotation" -> PATCH /projects/{projectId}/annotations/{annotationId}
- "Remove an annotation" -> DELETE /projects/{projectId}/annotations/{annotationId}
- "What tags are available for annotations?" -> GET /projects/{projectId}/annotations/tags
- "Create a new annotation tag" -> POST /projects/{projectId}/annotations/tags
- "Who created this annotation?" -> GET /projects/{projectId}/annotations/{annotationId}
- "List all annotations then delete a specific one" -> GET /projects/{projectId}/annotations + DELETE /projects/{projectId}/annotations/{annotationId}
- "Tag an existing annotation with new labels" -> PATCH /projects/{projectId}/annotations/{annotationId}
- "Add an annotation for today's date" -> POST /projects/{projectId}/annotations

## Response Tips

- **Annotations list** (GET /annotations): Returns `results` as an array of maps; iterate over it to extract individual annotation objects.
- **Single annotation / create / update** (GET/POST/PATCH by ID): Returns `results` as a single map; `user` is a nested object with `id`, `first_name`, `last_name`; `tags` is an array of maps.
- **Delete**: Returns only the deleted annotation's `id` inside `results`; confirm success via `status` field.
- **Tags**: GET returns a bare 200 with no documented body structure; POST returns a flat object with `id`, `name`, `project_id`, and `has_annotations` (no `status` wrapper).
- **Errors**: All endpoints return 401 (unauthenticated) or 403 (unauthorized); no 404 is documented, so missing resources may surface as 403.

## Anomaly Flags

- **Missing 404 responses**: No endpoint documents a 404 error. If a request for a nonexistent annotation or project returns 403 instead of 404, surface this to the user as it may mask "not found" vs "not permitted."
- **Inconsistent response wrappers**: Tags POST returns a flat object (`{id, name, ...}`) without the `{status, results}` wrapper used everywhere else. Flag if the user expects uniform response parsing.
- **Tags GET has no response body spec**: The GET tags endpoint documents no response shape. If the actual response differs from POST tags, surface the discrepancy.
- **No pagination fields**: The annotations list endpoint shows no pagination parameters or cursor fields. If the project has many annotations, all results may be returned in one payload. Flag large result sets.
- **Tag IDs are numeric in creation but referenced as arrays**: POST annotations accepts `tags: [num]` (IDs), but the response returns `tags: [map]`. Surface if tag ID references fail to resolve.

## Playbook

### 1. Create an Annotation with Tags

1. GET /projects/{projectId}/annotations/tags to list available tags and note their IDs.
2. If the needed tag does not exist, POST /projects/{projectId}/annotations/tags with `{name: "your-tag"}` and note the returned `id`.
3. POST /projects/{projectId}/annotations with `{date: "YYYY-MM-DD", description: "...", tags: [tagId1, tagId2]}`.
4. Confirm the annotation was created by checking the `id` and `tags` array in the response.

### 2. Update an Annotation's Tags

1. GET /projects/{projectId}/annotations/{annotationId} to see current tags.
2. GET /projects/{projectId}/annotations/tags to find IDs for desired tags.
3. PATCH /projects/{projectId}/annotations/{annotationId} with `{tags: [newTagId1, newTagId2]}` (replaces existing tags).
4. Verify the updated `tags` array in the response matches expectations.

### 3. Audit and Clean Up Annotations

1. GET /projects/{projectId}/annotations to retrieve all annotations.
2. Review each annotation's `date`, `description`, and `user` to identify stale or duplicate entries.
3. For each unwanted annotation, DELETE /projects/{projectId}/annotations/{annotationId}.
4. Confirm each deletion by checking for `{status: "...", results: {id: ...}}` in the response.

### 4. Set Up a Tag Taxonomy

1. GET /projects/{projectId}/annotations/tags to see what tags already exist.
2. For each new category, POST /projects/{projectId}/annotations/tags with `{name: "category-name"}`.
3. Note each returned `id` for use when creating or updating annotations.
4. Verify tags are linked by checking `has_annotations: false` on newly created tags.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
