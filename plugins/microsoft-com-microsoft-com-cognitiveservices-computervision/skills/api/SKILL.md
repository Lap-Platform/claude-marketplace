---
name: computer-vision-client
description: "Computer Vision Client API skill. Use when working with Computer Vision Client for analyze, describe, detect. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# Computer Vision Client
API version: 2.1

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
https://westcentralus.api.cognitive.microsoft.com/vision/v2.1

## Setup
1. Set your API key in the appropriate header
2. GET /models -- verify access
3. POST /analyze -- create first analyze

## Endpoints

9 endpoints across 8 groups. See references/api-spec.lap for full details.

### analyze
| Method | Path | Description |
|--------|------|-------------|
| POST | /analyze | This operation extracts a rich set of visual features based on the image content. |

### describe
| Method | Path | Description |
|--------|------|-------------|
| POST | /describe | This operation generates a description of an image in human readable language with complete sentences. The description is based on a collection of content tags, which are also returned by the operation. More than one description can be generated for each image. Descriptions are ordered by their confidence score. Descriptions may include results from celebrity and landmark domain models, if applicable. |

### detect
| Method | Path | Description |
|--------|------|-------------|
| POST | /detect | Performs object detection on the specified image. |

### models
| Method | Path | Description |
|--------|------|-------------|
| GET | /models | This operation returns the list of domain-specific models that are supported by the Computer Vision API. Currently, the API supports following domain-specific models: celebrity recognizer, landmark recognizer. |
| POST | /models/{model}/analyze | This operation recognizes content within an image by applying a domain-specific model. The list of domain-specific models that are supported by the Computer Vision API can be retrieved using the /models GET request. Currently, the API provides following domain-specific models: celebrities, landmarks. |

### ocr
| Method | Path | Description |
|--------|------|-------------|
| POST | /ocr | Optical Character Recognition (OCR) detects text in an image and extracts the recognized characters into a machine-usable character stream. |

### tag
| Method | Path | Description |
|--------|------|-------------|
| POST | /tag | This operation generates a list of words, or tags, that are relevant to the content of the supplied image. The Computer Vision API can return tags based on objects, living beings, scenery or actions found in images. Unlike categories, tags are not organized according to a hierarchical classification system, but correspond to image content. Tags may contain hints to avoid ambiguity or provide context, for example the tag "ascomycete" may be accompanied by the hint "fungus". |

### generateThumbnail
| Method | Path | Description |
|--------|------|-------------|
| POST | /generateThumbnail | This operation generates a thumbnail image with the user-specified width and height. By default, the service analyzes the image, identifies the region of interest (ROI), and generates smart cropping coordinates based on the ROI. Smart cropping helps when you specify an aspect ratio that differs from that of the input image. |

### areaOfInterest
| Method | Path | Description |
|--------|------|-------------|
| POST | /areaOfInterest | This operation returns a bounding box around the most important area of the image. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Create a analyze?" -> POST /analyze
- "Create a describe?" -> POST /describe
- "Create a detect?" -> POST /detect
- "List all models?" -> GET /models
- "Create a analyze?" -> POST /models/{model}/analyze
- "Create a ocr?" -> POST /ocr
- "Create a tag?" -> POST /tag
- "Create a generateThumbnail?" -> POST /generateThumbnail
- "Create a areaOfInterest?" -> POST /areaOfInterest
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
