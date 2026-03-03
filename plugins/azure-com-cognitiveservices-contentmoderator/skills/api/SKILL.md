---
name: content-moderator-client
description: "Content Moderator Client API skill. Use when working with Content Moderator Client for contentmoderator. Covers 35 endpoints."
version: 1.0.0
generator: lapsh
---

# Content Moderator Client
API version: 1.0

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /contentmoderator/lists/v1.0/imagelists -- verify access
3. POST /contentmoderator/moderate/v1.0/ProcessImage/FindFaces -- create first FindFaces

## Endpoints

35 endpoints across 1 groups. See references/api-spec.lap for full details.

### contentmoderator
| Method | Path | Description |
|--------|------|-------------|
| POST | /contentmoderator/moderate/v1.0/ProcessImage/FindFaces | Returns the list of faces found. |
| POST | /contentmoderator/moderate/v1.0/ProcessImage/OCR | Returns any text found in the image for the specified language. If no language is specified in the input, the detection defaults to English. |
| POST | /contentmoderator/moderate/v1.0/ProcessImage/Evaluate | Returns probabilities of the image containing racy or adult content. |
| POST | /contentmoderator/moderate/v1.0/ProcessImage/Match | Fuzzily match an image against one of your custom image lists. You can create and manage your custom image lists by using <a href="/docs/services/578ff44d2703741568569ab9/operations/578ff7b12703741568569abe">this API</a>. |
| POST | /contentmoderator/moderate/v1.0/ProcessText/Screen/ | Detect profanity and match against custom and shared blocklists |
| POST | /contentmoderator/moderate/v1.0/ProcessText/DetectLanguage | This operation detects the language of input content. It returns the <a href="http://www-01.sil.org/iso639-3/codes.asp">ISO 639-3 code</a> for the predominant language in the submitted text. More than 110 languages are supported. |
| GET | /contentmoderator/lists/v1.0/imagelists/{listId} | Returns the details of the image list with listId equal to the passed list ID. |
| DELETE | /contentmoderator/lists/v1.0/imagelists/{listId} | Deletes the image list with listId equal to the passed list ID. |
| PUT | /contentmoderator/lists/v1.0/imagelists/{listId} | Updates an image list with listId equal to the passed list ID. |
| POST | /contentmoderator/lists/v1.0/imagelists | Creates an image list. |
| GET | /contentmoderator/lists/v1.0/imagelists | Gets all the image lists. |
| POST | /contentmoderator/lists/v1.0/imagelists/{listId}/RefreshIndex | Refreshes the index of the list with listId equal to the passed list ID. |
| GET | /contentmoderator/lists/v1.0/termlists/{listId} | Returns list ID details of the term list with listId equal to the passed list ID. |
| DELETE | /contentmoderator/lists/v1.0/termlists/{listId} | Deletes the term list with listId equal to the passed list ID. |
| PUT | /contentmoderator/lists/v1.0/termlists/{listId} | Updates a term list. |
| POST | /contentmoderator/lists/v1.0/termlists | Creates a term list. |
| GET | /contentmoderator/lists/v1.0/termlists | Gets all the term lists. |
| POST | /contentmoderator/lists/v1.0/termlists/{listId}/RefreshIndex | Refreshes the index of the list with listId equal to the passed list ID. |
| POST | /contentmoderator/lists/v1.0/imagelists/{listId}/images | Add an image to the list with listId equal to the passed list ID. |
| DELETE | /contentmoderator/lists/v1.0/imagelists/{listId}/images | Deletes all images from the list with listId equal to the passed list ID. |
| GET | /contentmoderator/lists/v1.0/imagelists/{listId}/images | Gets all image IDs from the list with listId equal to the passed list ID. |
| DELETE | /contentmoderator/lists/v1.0/imagelists/{listId}/images/{ImageId} | Deletes an image from the list with the passed list ID and image ID. |
| POST | /contentmoderator/lists/v1.0/termlists/{listId}/terms/{term} | Adds a term to the term list with listId equal to the passed list ID. |
| DELETE | /contentmoderator/lists/v1.0/termlists/{listId}/terms/{term} | Deletes a term from the list with listId equal to the passed list ID. |
| GET | /contentmoderator/lists/v1.0/termlists/{listId}/terms | Gets all terms from the list with listId equal to the passed list ID. |
| DELETE | /contentmoderator/lists/v1.0/termlists/{listId}/terms | Deletes all terms from the list with listId equal to the passed list ID. |
| GET | /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId} | Returns review details for the passed review ID. |
| GET | /contentmoderator/review/v1.0/teams/{teamName}/jobs/{JobId} | Get the job details for a job ID. |
| POST | /contentmoderator/review/v1.0/teams/{teamName}/reviews | The created reviews appear for reviewers on your team. As reviewers finish reviewing, results of the reviews are posted (that is, HTTP POST) on the specified CallBackEndpoint value. |
| POST | /contentmoderator/review/v1.0/teams/{teamName}/jobs | A job ID will be returned for the content posted on this endpoint. |
| POST | /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId}/frames | The created reviews appear for reviewers on your team. As reviewers finish reviewing, results of the reviews are posted (that is, HTTP POST) on the specified CallBackEndpoint value. |
| GET | /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId}/frames | The created reviews appear for reviewers on your team. As reviewers finish reviewing, results of the reviews are posted (that is, HTTP POST) on the specified CallBackEndpoint value. |
| POST | /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId}/publish | Publish a video review. |
| PUT | /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId}/transcriptmoderationresult | This API adds a transcript screen text result file for a video review. The transcript screen text result file is a result of the Screen Text API. To generate a transcript screen text result file, you must screen a transcript file for profanity by using the Screen Text API. |
| PUT | /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId}/transcript | This API adds a transcript file (text version of all the words spoken in a video) to a video review. The file should be in a valid WebVTT format. |

## Enhanced Skill Content
## Question Mapping

- "How do I check an image for adult or racy content?" -> POST /contentmoderator/moderate/v1.0/ProcessImage/Evaluate
- "Can I detect faces in an image?" -> POST /contentmoderator/moderate/v1.0/ProcessImage/FindFaces
- "How do I extract text from an image?" -> POST /contentmoderator/moderate/v1.0/ProcessImage/OCR
- "Does this image match anything on my block list?" -> POST /contentmoderator/moderate/v1.0/ProcessImage/Match
- "How do I screen text for profanity, PII, or classification?" -> POST /contentmoderator/moderate/v1.0/ProcessText/Screen/
- "What language is this text written in?" -> POST /contentmoderator/moderate/v1.0/ProcessText/DetectLanguage
- "How do I create a custom image list for matching?" -> POST /contentmoderator/lists/v1.0/imagelists
- "How do I add a banned term to my custom term list?" -> POST /contentmoderator/lists/v1.0/termlists/{listId}/terms/{term}
- "How do I create a human review for flagged content?" -> POST /contentmoderator/review/v1.0/teams/{teamName}/reviews
- "How do I check the status of a moderation job?" -> GET /contentmoderator/review/v1.0/teams/{teamName}/jobs/{JobId}
- "How do I publish a completed review?" -> POST /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId}/publish
- "Why isn't my custom list matching new entries?" -> POST /contentmoderator/lists/v1.0/imagelists/{listId}/RefreshIndex
- "How do I list all terms in a custom term list?" -> GET /contentmoderator/lists/v1.0/termlists/{listId}/terms
- "How do I remove all terms from a list at once?" -> DELETE /contentmoderator/lists/v1.0/termlists/{listId}/terms
- "How do I add video frames to an existing review?" -> POST /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId}/frames

## Response Tips

- **Image moderation** (Evaluate, FindFaces, OCR, Match): Responses include confidence scores -- treat values above 0.75 as high-confidence flags; `IsImageAdultClassified`/`IsImageRacyClassified` booleans give quick pass/fail.
- **Text moderation** (Screen, DetectLanguage): Screen returns nested `PII`, `Classification`, and `Terms` objects -- always check each sub-object independently since text can fail on multiple categories.
- **List management** (image lists, term lists): All list mutations return the updated list metadata; after adding or removing items you must call RefreshIndex before the changes take effect in matching.
- **Term retrieval** (GET terms): Supports `offset` and `limit` for pagination -- iterate until the returned array is shorter than `limit`.
- **Review workflow** (reviews, jobs, frames): GET review returns `Status` and `ReviewerResultTags` -- a missing or empty tags array means the review is still pending; `publish` returns 204 with no body on success.
- **Transcript endpoints**: Return 204 on success with no body -- check the status code rather than parsing a response.

## Anomaly Flags

- **RefreshIndex not called**: Surface a warning whenever images or terms are added/deleted from a custom list without a subsequent RefreshIndex call -- matches will be stale until the index is refreshed.
- **Rate limit headers**: Watch for `Retry-After` or `429` responses; the API enforces per-second and per-month quotas on the `Ocp-Apim-Subscription-Key`. Alert when approaching documented tier limits.
- **OCR with wrong language**: If OCR returns empty or garbled text, flag that the `language` parameter may not match the image content -- suggest re-running with a different language code or using DetectLanguage on extracted text.
- **PII detected in text screening**: When `PII` is true and personal data (emails, phones, addresses) appear in the response, proactively alert the user since PII findings often require immediate action under compliance frameworks.
- **Review stuck unpublished**: If a review was created more than 24 hours ago and `publish` has not been called, flag it as potentially abandoned -- unpublished reviews do not trigger downstream callbacks.
- **Empty custom lists**: Alert when a Match or Screen call references a `listId` whose corresponding GET returns zero items -- the call will always return no matches, which is likely unintended.
- **201/204 vs 200 status codes**: Term creation returns 201 and deletions return 204 -- flag any unexpected 200 on these endpoints as a potential API version mismatch.

## Playbook

### 1. Set up a custom image block list and match against it

1. Create a new image list: `POST /contentmoderator/lists/v1.0/imagelists` with a name and description in the body.
2. Note the returned `listId`.
3. Add images to the list: `POST /contentmoderator/lists/v1.0/imagelists/{listId}/images` with optional `tag` and `label`.
4. Repeat step 3 for each image to block.
5. Refresh the index: `POST /contentmoderator/lists/v1.0/imagelists/{listId}/RefreshIndex` -- this is required before matching works.
6. Match incoming images: `POST /contentmoderator/moderate/v1.0/ProcessImage/Match` with `listId` set to your list. Omit `listId` to match against all lists.

### 2. Screen user-generated text with full analysis

1. Detect the language if unknown: `POST /contentmoderator/moderate/v1.0/ProcessText/DetectLanguage` with the text body.
2. Screen the text: `POST /contentmoderator/moderate/v1.0/ProcessText/Screen/` with `language` from step 1, and set `PII=true`, `classify=true`, `autocorrect=true` for full analysis.
3. Inspect the response: check `Terms` for profanity matches, `PII` for personal data, and `Classification` for category scores.
4. If custom term filtering is needed, pass the `listId` of your custom term list in the Screen call.

### 3. Create and manage a human review workflow

1. Run automated moderation first (e.g., `POST ProcessImage/Evaluate` or `POST ProcessText/Screen`).
2. For borderline results, create a review: `POST /contentmoderator/review/v1.0/teams/{teamName}/reviews` with the content URL and metadata.
3. Optionally assign to a sub-team by setting `subTeam`.
4. Monitor review status: `GET /contentmoderator/review/v1.0/teams/{teamName}/reviews/{reviewId}` -- check `Status` field.
5. Once the reviewer completes their assessment, publish the review: `POST .../reviews/{reviewId}/publish` to finalize and trigger callbacks.

### 4. Moderate video content with frame-level review

1. Create a moderation job: `POST /contentmoderator/review/v1.0/teams/{teamName}/jobs` with `ContentType`, `ContentId`, `WorkflowName`, and optionally a `CallBackEndpoint` for async notification.
2. Check job progress: `GET /contentmoderator/review/v1.0/teams/{teamName}/jobs/{JobId}`.
3. Once the job completes, add extracted frames to a review: `POST .../reviews/{reviewId}/frames` with optional `timescale`.
4. Retrieve frames for inspection: `GET .../reviews/{reviewId}/frames` using `startSeed`, `noOfRecords`, and `filter` for pagination.
5. Upload transcript moderation results: `PUT .../reviews/{reviewId}/transcriptmoderationresult` with flagged segments.
6. Upload the full transcript: `PUT .../reviews/{reviewId}/transcript`.
7. Publish the review: `POST .../reviews/{reviewId}/publish`.

### 5. Maintain custom term lists for multi-language moderation

1. Create a term list: `POST /contentmoderator/lists/v1.0/termlists` with a name and description.
2. Add terms: `POST /contentmoderator/lists/v1.0/termlists/{listId}/terms/{term}` with the `language` parameter for each term.
3. Refresh the index: `POST /contentmoderator/lists/v1.0/termlists/{listId}/RefreshIndex` with the `language` -- required after any add/delete.
4. Verify terms: `GET /contentmoderator/lists/v1.0/termlists/{listId}/terms` with `language`, using `offset` and `limit` to paginate.
5. Remove a specific term: `DELETE .../termlists/{listId}/terms/{term}` with `language`.
6. Bulk clear all terms: `DELETE .../termlists/{listId}/terms` with `language`.
7. Always call RefreshIndex again after removals before using the list in text screening.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
