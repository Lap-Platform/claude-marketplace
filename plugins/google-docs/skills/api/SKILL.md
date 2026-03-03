---
name: google-docs-api
description: "Google Docs API skill. Use when working with Google Docs for documents. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Google Docs API
API version: v1

## Auth
OAuth2 | OAuth2

## Base URL
https://docs.googleapis.com/

## Setup
1. Configure auth: OAuth2 | OAuth2
2. GET /v1/documents/{documentId} -- verify access
3. POST /v1/documents -- create first documents

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### documents
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/documents | Creates a blank document using the title given in the request. Other fields in the request, including any provided content, are ignored. Returns the created document. |
| GET | /v1/documents/{documentId} | Gets the latest version of the specified document. |
| POST | /v1/documents/{documentId}:batchUpdate | Applies one or more updates to the document. Each request is validated before being applied. If any request is not valid, then the entire request will fail and nothing will be applied. Some requests have replies to give you some information about how they are applied. Other requests do not need to return information; these each return an empty reply. The order of replies matches that of the requests. For example, suppose you call batchUpdate with four updates, and only the third one returns information. The response would have two empty replies, the reply to the third request, and another empty reply, in that order. Because other users may be editing the document, the document might not exactly reflect your changes: your changes may be altered with respect to collaborator changes. If there are no collaborators, the document should reflect your changes. In any case, the updates in your request are guaranteed to be applied together atomically. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new Google Doc?" -> POST /v1/documents
- "How do I read the contents of a document?" -> GET /v1/documents/{documentId}
- "How do I insert text into a document?" -> POST /v1/documents/{documentId}:batchUpdate (insertText request)
- "How do I replace all occurrences of a word in a doc?" -> POST /v1/documents/{documentId}:batchUpdate (replaceAllText request)
- "How do I add a table to a document?" -> POST /v1/documents/{documentId}:batchUpdate (insertTable request)
- "How do I delete a section of content?" -> POST /v1/documents/{documentId}:batchUpdate (deleteContentRange request)
- "How do I insert an image into a doc?" -> POST /v1/documents/{documentId}:batchUpdate (insertInlineImage request)
- "How do I change the formatting or style of text?" -> POST /v1/documents/{documentId}:batchUpdate (updateTextStyle request)
- "How do I add bullet points to paragraphs?" -> POST /v1/documents/{documentId}:batchUpdate (createParagraphBullets request)
- "How do I view a document with suggestions accepted?" -> GET /v1/documents/{documentId} with suggestionsViewMode=PREVIEW_SUGGESTIONS_ACCEPTED
- "How do I create a header or footer?" -> POST /v1/documents/{documentId}:batchUpdate (createHeader / createFooter request)
- "How do I update page margins or document style?" -> POST /v1/documents/{documentId}:batchUpdate (updateDocumentStyle request)
- "How do I merge or unmerge table cells?" -> POST /v1/documents/{documentId}:batchUpdate (mergeTableCells / unmergeTableCells request)
- "How do I create a named range for bookmarking?" -> POST /v1/documents/{documentId}:batchUpdate (createNamedRange request)
- "How do I do a safe concurrent edit using revision control?" -> POST /v1/documents/{documentId}:batchUpdate with writeControl.requiredRevisionId

## Response Tips

- **Create document (POST /v1/documents):** Returns the full document object including the assigned `documentId` -- save this ID for all subsequent operations.
- **Get document (GET /v1/documents/{documentId}):** The `body.content` array contains structural elements (paragraphs, tables, section breaks) each with `startIndex`/`endIndex` -- these indices are critical for batch update operations. `suggestedDocumentStyleChanges` and `suggestedNamedStylesChanges` are only populated when viewing with suggestions.
- **Batch update (POST batchUpdate):** Returns `replies` as an array matching the order of your `requests` array -- empty objects for operations with no meaningful return value; `writeControl` in the response provides the new `requiredRevisionId` for subsequent safe writes.

## Anomaly Flags

- **Stale revision conflict:** If `batchUpdate` fails with a 409/conflict when using `writeControl.requiredRevisionId`, the document was modified since your last read -- re-fetch and retry.
- **Index out of range:** Inserting or deleting at invalid `startIndex`/`endIndex` values returns 400 -- always fetch the document first to get current indices, as they shift after every mutation.
- **Empty body.content:** A newly created document returns a minimal `body.content` array (typically one empty paragraph) -- do not assume it is truly empty or errored.
- **OAuth scope mismatch:** 403 errors usually mean the OAuth token lacks `documents` or `documents.readonly` scope rather than a permissions issue on the document itself.
- **Request ordering in batchUpdate:** Requests execute sequentially and indices shift after each operation -- process deletions from highest index to lowest, or use named ranges to avoid index arithmetic.
- **Large document payload:** GET responses for complex documents can be very large due to nested `inlineObjects`, `positionedObjects`, and suggestion metadata -- watch for response size limits or timeouts.

## Playbook

### 1. Create a document and populate it with content

1. `POST /v1/documents` with `{ "title": "My Document" }` to create a new doc.
2. Save the `documentId` from the response.
3. `POST /v1/documents/{documentId}:batchUpdate` with an `insertText` request: `{ "requests": [{ "insertText": { "location": { "index": 1 }, "text": "Hello, world!" } }] }`.
4. Optionally follow up with an `updateTextStyle` request to format the inserted text.

### 2. Find and replace text across a document

1. `GET /v1/documents/{documentId}` to confirm the document exists and note the `revisionId`.
2. `POST /v1/documents/{documentId}:batchUpdate` with a `replaceAllText` request: `{ "requests": [{ "replaceAllText": { "containsText": { "text": "old term", "matchCase": true }, "replaceText": "new term" } }] }`.
3. Check `replies[0]` for the count of replacements made.

### 3. Insert a table and style it

1. `GET /v1/documents/{documentId}` to find the target `index` where the table should go.
2. `POST /v1/documents/{documentId}:batchUpdate` with `insertTable`: `{ "requests": [{ "insertTable": { "rows": 3, "columns": 2, "location": { "index": <target> } } }] }`.
3. Re-fetch the document with `GET /v1/documents/{documentId}` to discover the table's cell indices.
4. Send another `batchUpdate` with `insertText` requests targeting each cell's start index.
5. Optionally add `updateTableCellStyle` or `updateTableColumnProperties` requests to adjust column widths or cell padding.

### 4. Safe concurrent editing with revision control

1. `GET /v1/documents/{documentId}` and save the `revisionId` from the response.
2. `POST /v1/documents/{documentId}:batchUpdate` with `writeControl: { "requiredRevisionId": "<saved revisionId>" }` and your desired `requests`.
3. If the call succeeds, save the new `requiredRevisionId` from the response's `writeControl` for the next edit.
4. If it fails with a conflict, re-fetch the document, rebase your changes against the new content/indices, and retry.

### 5. Add headers, footers, and page formatting

1. `POST /v1/documents/{documentId}:batchUpdate` with a `createHeader` request: `{ "requests": [{ "createHeader": { "type": "DEFAULT" } }] }`.
2. The reply contains the new `headerId` -- use it to insert text into the header via a second `batchUpdate` with `insertText` targeting the header segment.
3. Add an `updateDocumentStyle` request to set margins, page size, or enable first-page headers: `{ "updateDocumentStyle": { "documentStyle": { "useFirstPageHeaderFooter": true, "marginTop": { "magnitude": 72, "unit": "PT" } }, "fields": "useFirstPageHeaderFooter,marginTop" } }`.
4. Repeat with `createFooter` for footers.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
