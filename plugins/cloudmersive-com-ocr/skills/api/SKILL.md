---
name: ocrapi
description: "ocrapi API skill. Use when working with ocrapi for ocr. Covers 20 endpoints."
version: 1.0.0
generator: lapsh
---

# ocrapi
API version: v1

## Auth
ApiKey Apikey in header

## Base URL
http://localhost

## Setup
1. Set your API key in the appropriate header
2. GET /ocr/pdf/get-job-status -- verify access
3. POST /ocr/image/toText -- create first toText

## Endpoints

20 endpoints across 1 groups. See references/api-spec.lap for full details.

### ocr
| Method | Path | Description |
|--------|------|-------------|
| POST | /ocr/image/toText | Convert a scanned image into text |
| POST | /ocr/image/to/words-with-location | Convert a scanned image into words with location |
| POST | /ocr/image/to/lines-with-location | Convert a scanned image into words with location |
| POST | /ocr/photo/toText | Convert a photo of a document into text |
| POST | /ocr/photo/to/words-with-location | Convert a photo of a document or receipt into words with location |
| POST | /ocr/photo/recognize/receipt | Recognize a photo of a receipt, extract key business information |
| POST | /ocr/photo/recognize/business-card | Recognize a photo of a business card, extract key business information |
| POST | /ocr/photo/recognize/form | Recognize a photo of a form, extract key fields and business information |
| POST | /ocr/photo/recognize/form/advanced | Recognize a photo of a form, extract key fields using stored templates |
| POST | /ocr/pdf/toText | Converts an uploaded PDF file into text via Optical Character Recognition. |
| GET | /ocr/pdf/get-job-status | Returns the result of the Async Job - possible states can be STARTED or COMPLETED |
| POST | /ocr/pdf/to/words-with-location | Convert a PDF into words with location |
| POST | /ocr/pdf/to/lines-with-location | Convert a PDF into text lines with location |
| POST | /ocr/preprocessing/image/binarize | Convert an image of text into a binarized (light and dark) view |
| POST | /ocr/preprocessing/image/binarize/advanced | Convert an image of text into a binary (light and dark) view with ML |
| POST | /ocr/preprocessing/image/get-page-angle | Get the angle of the page / document / receipt |
| POST | /ocr/preprocessing/image/unrotate | Detect and unrotate a document image |
| POST | /ocr/preprocessing/image/unrotate/advanced | Detect and unrotate a document image (advanced) |
| POST | /ocr/preprocessing/image/unskew | Detect and unskew a photo of a document |
| POST | /ocr/receipts/photo/to/csv | Convert a photo of a receipt into a CSV file containing structured information from the receipt |

## Enhanced Skill Content
## Question Mapping

- "How do I extract text from an image?" -> POST /ocr/image/toText
- "Can I get word positions/coordinates from an image?" -> POST /ocr/image/to/words-with-location
- "How do I OCR a photo with scene text?" -> POST /ocr/photo/toText
- "How do I extract text from a PDF?" -> POST /ocr/pdf/toText
- "How do I check if my PDF OCR job is done?" -> GET /ocr/pdf/get-job-status
- "Can I scan a receipt and get structured data?" -> POST /ocr/photo/recognize/receipt
- "How do I extract contact info from a business card?" -> POST /ocr/photo/recognize/business-card
- "How do I extract fields from a structured form?" -> POST /ocr/photo/recognize/form
- "Can I get line-by-line text with coordinates from a PDF?" -> POST /ocr/pdf/to/lines-with-location
- "How do I straighten a skewed document image before OCR?" -> POST /ocr/preprocessing/image/unskew
- "How do I fix a rotated scan?" -> POST /ocr/preprocessing/image/unrotate
- "How do I convert a receipt photo to CSV?" -> POST /ocr/receipts/photo/to/csv
- "Can I binarize an image to improve OCR quality?" -> POST /ocr/preprocessing/image/binarize
- "How do I detect the page rotation angle?" -> POST /ocr/preprocessing/image/get-page-angle

## Response Tips

- **Text extraction** (`toText` endpoints): Returns plain recognized text. Check for empty strings indicating no text was detected or a preprocessing issue.
- **Location endpoints** (`words-with-location`, `lines-with-location`): Responses contain nested coordinate objects per word/line. Iterate results carefully -- coordinates are relative to the original image dimensions.
- **Recognition endpoints** (`receipt`, `business-card`, `form`): Return structured key-value data. Fields may be null when the recognizer has low confidence or the field is absent from the source document.
- **PDF async jobs** (`get-job-status`): Poll with the `AsyncJobID` returned from the initial PDF request. Status will transition through processing states before completion.
- **Preprocessing endpoints**: Return the processed image binary. Content-Type of the response will differ from typical JSON responses.

## Anomaly Flags

- **Empty OCR results**: If a `toText` call returns blank output, surface a suggestion to apply preprocessing (binarize, unskew, unrotate) before retrying.
- **Async job stalls**: If `get-job-status` returns a non-complete status after repeated polls, flag the job as potentially stuck and suggest resubmission.
- **Missing API key**: All endpoints require `Apikey` in the header. Surface auth errors immediately rather than letting them cascade into opaque 200s with error bodies.
- **Photo vs Image mismatch**: Flag when a user sends a scene photo to an `/ocr/image/` endpoint (optimized for scanned documents) instead of `/ocr/photo/` (optimized for real-world photos). Recognition quality will degrade silently.
- **Preprocessing without follow-up**: If the user calls a preprocessing endpoint but never follows up with an OCR call, remind them that preprocessing only transforms the image -- they still need to run OCR on the result.
- **Large PDF without async awareness**: If a user calls `/ocr/pdf/toText` on a large file, proactively mention `get-job-status` for polling, as the request may return an async job ID rather than immediate results.

## Playbook

### 1. Extract clean text from a poor-quality scan

1. Upload the image to `POST /ocr/preprocessing/image/get-page-angle` to detect rotation.
2. If the angle is non-zero, send the image to `POST /ocr/preprocessing/image/unrotate` to correct it.
3. Send the corrected image to `POST /ocr/preprocessing/image/binarize` to improve contrast.
4. Send the binarized image to `POST /ocr/image/toText` with the desired `language` parameter.

### 2. Process a multi-page PDF and retrieve results

1. Submit the PDF to `POST /ocr/pdf/toText` with `recognitionMode` and `language` set as needed.
2. Capture the `AsyncJobID` from the response.
3. Poll `GET /ocr/pdf/get-job-status?AsyncJobID={id}` until the status indicates completion.
4. Extract the final text from the completed job response.

### 3. Digitize a batch of receipts to CSV

1. For each receipt photo, send it to `POST /ocr/receipts/photo/to/csv`.
2. Collect the CSV output from each response.
3. Concatenate or merge the CSVs, deduplicating headers as needed.

### 4. Extract structured data from a custom form

1. Define the form template with field regions in `formTemplateDefinition`.
2. Submit the form image to `POST /ocr/photo/recognize/form` with the template and `preprocessing` enabled.
3. If results are unreliable, retry with `POST /ocr/photo/recognize/form/advanced` using cloud bucket storage for the template (`bucketID`, `bucketSecretKey`).
4. Enable `diagnostics` to inspect per-field confidence scores.

### 5. Get word-level coordinates from a photo for overlay/annotation

1. Send the photo to `POST /ocr/photo/to/words-with-location` with the appropriate `language`.
2. Parse the response for each word's bounding box coordinates.
3. Map coordinates back to the original image dimensions to render text overlay or bounding boxes.
4. If coordinates seem misaligned, preprocess with `POST /ocr/preprocessing/image/unskew` first and resubmit.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
