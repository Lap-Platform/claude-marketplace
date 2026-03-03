---
name: barcode-api
description: "Barcode API skill. Use when working with Barcode for barcode. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Barcode API
API version: 1.5

## Auth
Bearer bearer

## Base URL
http://api.fungenerators.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /barcode/encode/types -- verify access
3. POST /barcode/decode -- create first decode

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### barcode
| Method | Path | Description |
|--------|------|-------------|
| GET | /barcode/encode/types | Get the supported barcode types for encoding / image generation. |
| GET | /barcode/encode | Get a Bar Code image for the given barcode number |
| GET | /barcode/decode/types | Get the supported barcode types for the decoding process. |
| POST | /barcode/decode | Decode a Barcode image and return the cotents if successful |

## Enhanced Skill Content


## Question Mapping

- "What barcode formats can I encode?" -> GET /barcode/encode/types
- "What barcode formats can I decode?" -> GET /barcode/decode/types
- "How do I generate a barcode from a number?" -> GET /barcode/encode
- "Can I create a QR code from a string?" -> GET /barcode/encode
- "How do I decode a barcode image?" -> POST /barcode/decode
- "What output formats are available for encoding?" -> GET /barcode/encode/types
- "How do I resize a generated barcode?" -> GET /barcode/encode
- "Can I control the height of the barcode image?" -> GET /barcode/encode
- "What happens if I encode without specifying a format?" -> GET /barcode/encode
- "How do I read a barcode from a file?" -> POST /barcode/decode
- "Which encoding types support width customization?" -> GET /barcode/encode/types, then GET /barcode/encode
- "How do I verify a barcode encodes the right data?" -> GET /barcode/encode, then POST /barcode/decode

## Response Tips

- **Encode/Decode types** (GET /barcode/encode/types, GET /barcode/decode/types): Returns a list of supported format strings. Use these values for the `barcodeformat` parameter.
- **Encode** (GET /barcode/encode): Returns barcode image or data. The `outputformat` parameter controls the response content type.
- **Decode** (POST /barcode/decode): Returns the decoded string value from the submitted barcode image. Check for empty or null results indicating unreadable input.
- **All endpoints**: 401 means the Bearer token is missing or invalid. No pagination -- responses are single-result.

## Anomaly Flags

- **401 on any call**: Surface immediately -- likely an expired or missing API key. Prompt user to check their Bearer token.
- **Empty type lists**: If encode/decode types return empty arrays, the API may be experiencing issues. Flag this as unexpected.
- **Decode returning null/empty**: The submitted image may be unreadable. Suggest checking image quality, format, and resolution.
- **Unusual response times on encode**: Large `widthfactor` or `totalheight` values may cause slow generation. Flag if response exceeds 5s.
- **Unsupported barcodeformat value**: If encoding fails after specifying a format, cross-check against /barcode/encode/types results.

## Playbook

### Generate a Barcode from a Number

1. Call `GET /barcode/encode/types` to list supported formats.
2. Pick a format (e.g., `QR_CODE`, `CODE_128`).
3. Call `GET /barcode/encode` with `number` set to your data string, `barcodeformat` to your chosen format.
4. Optionally set `outputformat`, `widthfactor`, and `totalheight` for sizing.
5. Save or display the returned barcode image.

### Decode a Barcode Image

1. Call `GET /barcode/decode/types` to confirm the barcode format is supported.
2. Call `POST /barcode/decode` with the barcode image in the request body.
3. Read the decoded value from the response.
4. If the result is empty, retry with a higher-resolution image.

### Round-Trip Verification (Encode then Decode)

1. Encode your data using `GET /barcode/encode` with a known `number` value.
2. Take the generated barcode output.
3. Submit it to `POST /barcode/decode`.
4. Compare the decoded value against the original `number` to verify integrity.

### Explore All Supported Formats

1. Call `GET /barcode/encode/types` to get encoding-capable formats.
2. Call `GET /barcode/decode/types` to get decoding-capable formats.
3. Compare the two lists to identify formats that support both encoding and decoding.
4. Use overlapping formats for workflows that require round-trip support.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
