---
name: fun-generators-api
description: "Fun Generators API skill. Use when working with Fun Generators for qrcode. Covers 9 endpoints."
version: 1.0.0
generator: lapsh
---

# Fun Generators API
API version: 1.5

## Auth
ApiKey X-Fungenerators-Api-Secret in header

## Base URL
https://api.fungenerators.com

## Setup
1. Set your API key in the appropriate header
2. GET /qrcode/text -- verify access
3. POST /qrcode/decode -- create first decode

## Endpoints

9 endpoints across 1 groups. See references/api-spec.lap for full details.

### qrcode
| Method | Path | Description |
|--------|------|-------------|
| GET | /qrcode/text | Get a QR Code image for a block of text |
| GET | /qrcode/raw | Get a QR Code image for a block of raw data |
| GET | /qrcode/url | Get a QR Code image for a url |
| GET | /qrcode/phone | Get a QR Code image for a phone number |
| GET | /qrcode/sms | Get a QR Code image for a Phone number for SMS messaging |
| GET | /qrcode/skype | Get a QR Code image for a skype user |
| GET | /qrcode/email | Get a QR Code image for an email |
| GET | /qrcode/business_card | Get a QR Code image for a business card aka VCARD |
| POST | /qrcode/decode | Decode a QR Code image and return the cotents if successful |

## Enhanced Skill Content
## Question Mapping

- "How do I generate a QR code from text?" -> GET /qrcode/text
- "Can I create a QR code for a URL or website link?" -> GET /qrcode/url
- "How do I make a QR code with raw/unescaped data?" -> GET /qrcode/raw
- "Generate a QR code that dials a phone number when scanned" -> GET /qrcode/phone
- "Can I create a QR code that sends an SMS?" -> GET /qrcode/sms
- "How do I make a QR code for a Skype contact?" -> GET /qrcode/skype
- "Generate a QR code that opens a pre-filled email" -> GET /qrcode/email
- "How do I create a vCard/business card QR code?" -> GET /qrcode/business_card
- "Can I decode or read a QR code from an image?" -> POST /qrcode/decode
- "How do I get a QR code in PNG vs SVG format?" -> GET /qrcode/text (use `format` param)
- "I have a QR code image and need to extract its contents" -> POST /qrcode/decode
- "Create a QR code with full contact info including address and company" -> GET /qrcode/business_card
- "How do I authenticate with the Fun Generators API?" -> Set header `X-Fungenerators-Api-Secret`

## Response Tips

- **QR generation endpoints** (GET /qrcode/*): Returns image data or a URL to the generated QR code. Check `Content-Type` header -- response format depends on the `format` parameter.
- **QR decode endpoint** (POST /qrcode/decode): Returns the decoded text/data embedded in the QR image. Expects the image uploaded as `qrimage`.
- **Auth errors (401)**: All endpoints return 401 when `X-Fungenerators-Api-Secret` header is missing or invalid -- always set the key before making requests.
- **Format parameter**: Optional on every generation endpoint; omit it to get the API default format.

## Anomaly Flags

- **401 on every call**: API key is missing or incorrect -- surface immediately rather than retrying.
- **Empty or malformed QR output**: If the response body is unexpectedly small or not a valid image, flag that the input may have been rejected silently.
- **Business card with minimal fields**: If only `firstname`, `lastname`, and `email` are provided, note that the resulting vCard will be sparse -- suggest adding phone/address for a useful contact card.
- **Decode failure**: If POST /qrcode/decode returns an error or empty result, the image may be too low-resolution or corrupted -- suggest a higher-quality source image.
- **SMS/phone with non-numeric input**: If the `number` parameter contains letters or symbols, flag that the QR code may not work on mobile devices.

## Playbook

### 1. Generate a branded QR code for a website

1. Call `GET /qrcode/url` with `url` set to the target website and optionally `format` for preferred output type.
2. Check the response for the generated QR image or download link.
3. Embed the QR image in marketing materials or share directly.

### 2. Create a scannable business card

1. Gather contact details: first name, last name, email (required), plus any optional fields (company, phone numbers, address).
2. Call `GET /qrcode/business_card` with all available fields populated.
3. Download the resulting QR code.
4. Print on physical business cards or add to email signatures.

### 3. Decode an unknown QR code

1. Obtain the QR code image file.
2. Call `POST /qrcode/decode` with the image uploaded as `qrimage`.
3. Inspect the decoded text -- determine if it is a URL, vCard, phone number, or plain text.
4. Take action based on the content type (open URL, save contact, etc.).

### 4. Generate a pre-filled email QR code

1. Decide on the recipient email, subject line, and body text.
2. Call `GET /qrcode/email` with `email` (required) and optionally `subject` and `body`.
3. When scanned, the QR code opens the user's mail client with all fields pre-populated.

### 5. Batch-generate QR codes for multiple data types

1. Prepare a list of items (URLs, phone numbers, text strings).
2. For each item, call the appropriate endpoint (`/qrcode/url`, `/qrcode/phone`, `/qrcode/text`).
3. Collect all generated QR images.
4. Verify each by running them through `POST /qrcode/decode` to confirm accuracy.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
