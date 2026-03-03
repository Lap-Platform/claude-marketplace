---
name: deep-art-effects
description: "Deep Art Effects API skill. Use when working with Deep Art Effects for noauth. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Deep Art Effects
API version: 2017-02-10T16:24:46Z

## Auth
ApiKey x-api-key in header | ApiKey Authorization in header

## Base URL
https://api.deeparteffects.com/v1

## Setup
1. Set your API key in the appropriate header
2. GET /noauth/result -- verify access
3. POST /noauth/upload -- create first upload

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### noauth
| Method | Path | Description |
|--------|------|-------------|
| GET | /noauth/result |  |
| GET | /noauth/styles |  |
| POST | /noauth/upload |  |

## Enhanced Skill Content
## Question Mapping

- "What art styles are available?" -> GET /noauth/styles
- "How do I apply a style to an image?" -> POST /noauth/upload
- "How do I check the status of my image?" -> GET /noauth/result
- "Is my stylized image ready yet?" -> GET /noauth/result
- "How do I upload a photo for art processing?" -> POST /noauth/upload
- "Can I list all supported art filters?" -> GET /noauth/styles
- "How do I get the final result image?" -> GET /noauth/result
- "What do I pass in the upload request body?" -> POST /noauth/upload
- "How do I know which submissionId to use?" -> POST /noauth/upload then GET /noauth/result
- "Can I process an image without authentication?" -> POST /noauth/upload (all endpoints are noauth)
- "How do I retrieve a specific submission?" -> GET /noauth/result with submissionId
- "What happens if my upload fails?" -> POST /noauth/upload (check 400 error)
- "How do I apply a specific style to my photo end-to-end?" -> GET /noauth/styles -> POST /noauth/upload -> GET /noauth/result

## Response Tips

- **Styles** (GET /noauth/styles): Returns a list of style objects. Iterate to find style IDs needed for upload requests.
- **Upload** (POST /noauth/upload): Returns a submission reference on 200. Capture the submissionId from the response for polling results. 400 indicates a malformed or missing UploadRequest body.
- **Result** (GET /noauth/result): Returns the processed image or processing status. 400 typically means the submissionId is invalid or missing. If processing is not yet complete, expect a status field indicating progress rather than a final image URL.

## Anomaly Flags

- **Missing submissionId**: If a result request returns 400, surface that the submissionId parameter was likely omitted or malformed.
- **Processing not complete**: If GET /noauth/result returns successfully but contains a pending/processing status instead of a finished image, alert the user that polling is needed.
- **Empty styles list**: If GET /noauth/styles returns an empty array, flag that the service may be temporarily unavailable or misconfigured.
- **Upload 400 errors**: Surface the specific validation failure from the response body -- the UploadRequest map likely has required fields (image data, styleId) that were missing.
- **Auth headers present but unused**: All endpoints are under /noauth. If the user sets x-api-key or Authorization headers, note that these endpoints do not require them but the headers may be needed for rate limit elevation or future authenticated endpoints.

## Playbook

### 1. Apply an Art Style to an Image

1. Call GET /noauth/styles to retrieve available styles
2. Select the desired style and note its ID
3. Call POST /noauth/upload with an UploadRequest containing the image data and chosen style ID
4. Capture the submissionId from the upload response
5. Poll GET /noauth/result?submissionId={id} until the result indicates completion
6. Extract the final stylized image URL from the completed result

### 2. Browse Available Styles

1. Call GET /noauth/styles
2. Parse the response to list style names, thumbnails, and IDs
3. Present the styles to the user for selection

### 3. Check on a Previously Submitted Image

1. Retrieve the submissionId from a prior upload response
2. Call GET /noauth/result?submissionId={id}
3. If the status indicates processing, wait and retry after a short interval
4. If complete, extract and return the result image URL
5. If 400, verify the submissionId is correct and has not expired

### 4. Batch Process Multiple Images

1. Call GET /noauth/styles once to cache available styles
2. For each image, call POST /noauth/upload with the image data and desired style ID
3. Collect all returned submissionIds
4. Poll GET /noauth/result for each submissionId, tracking which are complete
5. Return results as each finishes, or wait for all to complete before returning


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
