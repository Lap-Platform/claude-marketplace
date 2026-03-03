---
name: computer-vision-api
description: "Computer Vision API skill. Use when working with Computer Vision for models, analyze, generateThumbnail. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# Computer Vision API
API version: 1.0

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /models -- verify access
3. POST /analyze -- create first analyze

## Endpoints

9 endpoints across 8 groups. See references/api-spec.lap for full details.

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /models | This operation returns the list of domain-specific models that are supported by the Computer Vision API.  Currently, the API only supports one domain-specific model: a celebrity recognizer. A successful response will be returned in JSON.  If the request failed, the response will contain an error code and a message to help understand what went wrong. |
| POST | /models/{model}/analyze | This operation recognizes content within an image by applying a domain-specific model.  The list of domain-specific models that are supported by the Computer Vision API can be retrieved using the /models GET request.  Currently, the API only provides a single domain-specific model: celebrities. Two input methods are supported -- (1) Uploading an image or (2) specifying an image URL. A successful response will be returned in JSON.  If the request failed, the response will contain an error code and a message to help understand what went wrong. |

### analyze
| Method | Path | Description |
|--------|------|-------------|
| POST | /analyze | This operation extracts a rich set of visual features based on the image content. Two input methods are supported -- (1) Uploading an image or (2) specifying an image URL.  Within your request, there is an optional parameter to allow you to choose which features to return.  By default, image categories are returned in the response. |

### generateThumbnail
| Method | Path | Description |
|--------|------|-------------|
| POST | /generateThumbnail | This operation generates a thumbnail image with the user-specified width and height. By default, the service analyzes the image, identifies the region of interest (ROI), and generates smart cropping coordinates based on the ROI. Smart cropping helps when you specify an aspect ratio that differs from that of the input image. A successful response contains the thumbnail image binary. If the request failed, the response contains an error code and a message to help determine what went wrong. |

### ocr
| Method | Path | Description |
|--------|------|-------------|
| POST | /ocr | Optical Character Recognition (OCR) detects printed text in an image and extracts the recognized characters into a machine-usable character stream.   Upon success, the OCR results will be returned. Upon failure, the error code together with an error message will be returned. The error code can be one of InvalidImageUrl, InvalidImageFormat, InvalidImageSize, NotSupportedImage,  NotSupportedLanguage, or InternalServerError. |

### describe
| Method | Path | Description |
|--------|------|-------------|
| POST | /describe | This operation generates a description of an image in human readable language with complete sentences.  The description is based on a collection of content tags, which are also returned by the operation. More than one description can be generated for each image.  Descriptions are ordered by their confidence score. All descriptions are in English. Two input methods are supported -- (1) Uploading an image or (2) specifying an image URL.A successful response will be returned in JSON.  If the request failed, the response will contain an error code and a message to help understand what went wrong. |

### tag
| Method | Path | Description |
|--------|------|-------------|
| POST | /tag | This operation generates a list of words, or tags, that are relevant to the content of the supplied image. The Computer Vision API can return tags based on objects, living beings, scenery or actions found in images. Unlike categories, tags are not organized according to a hierarchical classification system, but correspond to image content. Tags may contain hints to avoid ambiguity or provide context, for example the tag 'cello' may be accompanied by the hint 'musical instrument'. All tags are in English. |

### recognizeText
| Method | Path | Description |
|--------|------|-------------|
| POST | /recognizeText | Recognize Text operation. When you use the Recognize Text interface, the response contains a field called 'Operation-Location'. The 'Operation-Location' field contains the URL that you must use for your Get Handwritten Text Operation Result operation. |

### textOperations
| Method | Path | Description |
|--------|------|-------------|
| GET | /textOperations/{operationId} | This interface is used for getting text operation result. The URL to this interface should be retrieved from 'Operation-Location' field returned from Recognize Text interface. |

## Enhanced Skill Content
## Question Mapping

- "What vision models are available?" -> GET /models
- "Analyze this image for objects and faces" -> POST /analyze
- "What categories does this image belong to?" -> POST /analyze (with visualFeatures=Categories)
- "Generate a thumbnail from this image" -> POST /generateThumbnail
- "Create a smart-cropped 200x200 thumbnail" -> POST /generateThumbnail (with smartCropping=true)
- "Extract text from this image" -> POST /ocr
- "What language is the text in this image?" -> POST /ocr (with detectOrientation=true)
- "Describe what's in this photo" -> POST /describe
- "Give me multiple descriptions of this image" -> POST /describe (with maxCandidates)
- "Tag this image with keywords" -> POST /tag
- "Analyze this image using a specific domain model" -> POST /models/{model}/analyze
- "Read handwritten text from this image" -> POST /recognizeText (with detectHandwriting=true)
- "Check the status of my text recognition request" -> GET /textOperations/{operationId}
- "Extract printed and handwritten text from a document scan" -> POST /recognizeText then GET /textOperations/{operationId}
- "What objects and adult content flags does this image have?" -> POST /analyze (with visualFeatures=Adult,Objects)

## Response Tips

- **models**: Returns a flat list of domain models (celebrities, landmarks); check `models[].name` for use with `/models/{model}/analyze`.
- **analyze/describe/tag**: Nested under `categories`, `tags`, `description.captions` -- always traverse into these sub-objects rather than reading top-level fields alone.
- **generateThumbnail**: Returns raw image bytes (binary), not JSON -- set your Accept header accordingly and handle the response as a blob.
- **ocr**: Results nest under `regions[].lines[].words[]` -- flatten this hierarchy to reconstruct full text.
- **recognizeText/textOperations**: Async pair -- POST returns 202 with an `Operation-Location` header; poll GET until `status` is `Succeeded` or `Failed`.
- **errors**: All endpoints return `{ code, message }` under an `error` object; always check for this wrapper before accessing result fields.

## Anomaly Flags

- **202 without Operation-Location**: If `POST /recognizeText` returns 202 but no `Operation-Location` header, the request was accepted but tracking is broken -- surface immediately.
- **Rate limit (429)**: The API enforces per-second and per-minute quotas via `Ocp-Apim-Subscription-Key`. Surface `Retry-After` header value and warn before retrying.
- **Async polling stalls**: If `GET /textOperations/{operationId}` returns `Running` for more than 60 seconds, flag the operation as potentially stuck.
- **Empty analysis results**: If `POST /analyze` returns 200 but `categories`, `tags`, and `description.captions` are all empty, the image may be unrecognizable or corrupt -- surface this rather than silently returning nothing.
- **Model not found**: If `POST /models/{model}/analyze` returns a 404 or error referencing the model name, suggest calling `GET /models` first to verify available models.
- **OCR low confidence**: If OCR word-level confidence scores fall below 0.5 across most results, flag that the source image quality may be too low for reliable extraction.
- **Missing auth key**: Any 401 response means `Ocp-Apim-Subscription-Key` is missing or invalid -- prompt the user to verify their key before retrying.

## Playbook

### 1. Full Image Analysis Pipeline

1. Call `GET /models` to discover available domain models.
2. Call `POST /analyze` with `visualFeatures=Categories,Tags,Description,Faces,Objects` for a broad analysis.
3. If celebrities or landmarks are relevant, call `POST /models/celebrities/analyze` or `POST /models/landmarks/analyze`.
4. Call `POST /tag` if you need a dedicated keyword list beyond what analyze returned.
5. Combine results into a unified image profile.

### 2. Extract All Text from a Document Image

1. Call `POST /recognizeText` with `detectHandwriting=true` if handwriting may be present.
2. Capture the `Operation-Location` URL from the 202 response headers.
3. Poll `GET /textOperations/{operationId}` every 2-3 seconds until `status` is `Succeeded`.
4. Parse `recognitionResult.lines[].text` to reconstruct the full document text.
5. If the result is empty or low-confidence, fall back to `POST /ocr` for printed text with orientation detection.

### 3. Generate Optimized Thumbnails

1. Call `POST /generateThumbnail` with desired `width` and `height` and `smartCropping=true`.
2. Receive the raw image bytes in the response body.
3. If the crop looks wrong (subject cut off), retry without `smartCropping` for a center-crop fallback.
4. For batch processing, loop with different dimensions but reuse the same source image URL in the request body.

### 4. Multilingual OCR Workflow

1. Call `POST /describe` with `language=en` to get an initial sense of the image content.
2. Call `POST /ocr` with `detectOrientation=true` and omit `language` to let the API auto-detect.
3. Check the `language` field in the response to confirm detected language.
4. If auto-detection is wrong, retry `POST /ocr` with the correct `language` parameter (e.g., `zh-Hans`, `de`, `fr`).
5. Flatten `regions[].lines[].words[].text` and join to reconstruct the extracted text.

### 5. Domain-Specific Model Analysis

1. Call `GET /models` to list available domain models and their supported categories.
2. Pick the relevant model name (e.g., `celebrities`, `landmarks`).
3. Call `POST /models/{model}/analyze` with the chosen model name and optional `language`.
4. Parse the `result` object for domain-specific fields (e.g., celebrity names with confidence scores, landmark identification).
5. Cross-reference with `POST /analyze` results if you need both general and domain-specific insights.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
