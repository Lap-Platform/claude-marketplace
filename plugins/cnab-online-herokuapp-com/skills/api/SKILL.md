---
name: cnab-online
description: "Cnab Online API skill. Use when working with Cnab Online for file. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Cnab Online
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://cnab-online.herokuapp.com/v1

## Setup
1. No auth setup needed
2. GET /file/{fileId}/occurrences -- verify access
3. POST /file -- create first file

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### file
| Method | Path | Description |
|--------|------|-------------|
| POST | /file | Faz o upload de um arquivo |
| GET | /file/{fileId} | Retorna as informações básicas de um arquivo previamente processado |
| GET | /file/{fileId}/occurrences | Retorna as informações de baixa de boletos e outros tipos de ocorrências |
| GET | /file/{fileId}/lines | Retorna todas as linhas e seus respectivos campos (de forma não processada, apenas indicando os campos reconhecidos) |

## Enhanced Skill Content
## Question Mapping

- "How do I upload a CNAB file for parsing?" -> POST /file
- "What formats does the file upload accept?" -> POST /file
- "How do I check the status of an uploaded file?" -> GET /file/{fileId}
- "Can I retrieve metadata about a previously uploaded CNAB file?" -> GET /file/{fileId}
- "How do I list all occurrences (records) in a CNAB file?" -> GET /file/{fileId}/occurrences
- "What transaction records are in my CNAB return file?" -> GET /file/{fileId}/occurrences
- "How do I get the raw lines from a parsed CNAB file?" -> GET /file/{fileId}/lines
- "Can I see the line-by-line breakdown of a CNAB file?" -> GET /file/{fileId}/lines
- "How do I upload a CNAB 240 or CNAB 400 file?" -> POST /file
- "What is the difference between occurrences and lines?" -> GET /file/{fileId}/occurrences + GET /file/{fileId}/lines
- "How do I parse a bank return file (arquivo de retorno)?" -> POST /file then GET /file/{fileId}/occurrences
- "How do I extract payment details from a CNAB file?" -> POST /file then GET /file/{fileId}/occurrences
- "Can I retrieve a file I uploaded earlier by its ID?" -> GET /file/{fileId}

## Response Tips

- **POST /file**: Returns a file object with a `fileId` -- store this ID for all subsequent queries against the uploaded file.
- **GET /file/{fileId}**: Returns file-level metadata (format type, bank, dates). Check for CNAB 240 vs CNAB 400 designation in the response.
- **GET /file/{fileId}/occurrences**: Returns an array of parsed occurrence records. Each occurrence represents a structured banking transaction or event extracted from the file.
- **GET /file/{fileId}/lines**: Returns raw line data as parsed segments. Useful for debugging when occurrence-level parsing does not surface expected fields.
- **Errors**: A 404 on any `{fileId}` endpoint means the file was not found or has expired. Re-upload if needed.

## Anomaly Flags

- **File not found (404)**: Uploaded files may expire. Surface this if a previously valid `fileId` starts returning 404.
- **Malformed file upload**: If POST /file returns an error, the file likely is not valid CNAB 240 or CNAB 400 format. Flag the format mismatch to the user.
- **Empty occurrences array**: A successful response with zero occurrences suggests the file was parsed but contained no transaction records -- flag this as it likely indicates a header-only file or wrong file type.
- **Mismatched line count**: If the number of lines returned by /lines does not align with expected occurrences, surface this as a potential parsing anomaly.
- **Heroku cold starts**: The API is hosted on Heroku. First requests after inactivity may be slow (>5s). Flag unexpected latency on initial calls.

## Playbook

### 1. Parse a CNAB Return File and Extract Transactions

1. Upload the CNAB file via `POST /file` with the file in the request body.
2. Capture the `fileId` from the response.
3. Call `GET /file/{fileId}` to confirm the file was parsed and check its format (CNAB 240 or 400).
4. Call `GET /file/{fileId}/occurrences` to retrieve all structured transaction records.
5. Iterate over the occurrences array to extract payment statuses, amounts, and dates.

### 2. Debug a CNAB File That Parses With Missing Data

1. Upload the file via `POST /file` and note the `fileId`.
2. Call `GET /file/{fileId}/occurrences` to see what records were extracted.
3. Call `GET /file/{fileId}/lines` to get the raw line-by-line breakdown.
4. Compare the raw lines against the occurrences to identify which segments were not parsed into structured records.
5. Check the file metadata via `GET /file/{fileId}` to confirm the detected CNAB format matches the actual file format.

### 3. Validate a CNAB File Format Before Processing

1. Upload the file via `POST /file`.
2. If the upload fails, the file is not a recognized CNAB format -- inform the user.
3. If successful, call `GET /file/{fileId}` to retrieve the detected format and bank information.
4. Verify the format (240 or 400) and bank code match expectations before proceeding with occurrence extraction.

### 4. Batch Review of File Contents

1. Upload the CNAB file via `POST /file` and store the returned `fileId`.
2. Retrieve file metadata with `GET /file/{fileId}` to confirm successful parsing.
3. Fetch all occurrences with `GET /file/{fileId}/occurrences` for the structured view.
4. Fetch all lines with `GET /file/{fileId}/lines` for the complete raw view.
5. Cross-reference both datasets to produce a full audit of the file contents.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
