---
name: qnamaker-runtime-client
description: "QnAMaker Runtime Client API skill. Use when working with QnAMaker Runtime Client for knowledgebases. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# QnAMaker Runtime Client
API version: 4.0

## Auth
ApiKey Authorization in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
3. POST /knowledgebases/{kbId}/generateAnswer -- create first generateAnswer

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### knowledgebases
| Method | Path | Description |
|--------|------|-------------|
| POST | /knowledgebases/{kbId}/generateAnswer | GenerateAnswer call to query the knowledgebase. |
| POST | /knowledgebases/{kbId}/train | Train call to add suggestions to the knowledgebase. |

## Enhanced Skill Content
## Question Mapping

- "How do I get an answer from my knowledge base?" -> POST /knowledgebases/{kbId}/generateAnswer
- "Ask my QnA bot a question" -> POST /knowledgebases/{kbId}/generateAnswer
- "Query the knowledge base for a specific topic" -> POST /knowledgebases/{kbId}/generateAnswer
- "How do I test my knowledge base with a sample question?" -> POST /knowledgebases/{kbId}/generateAnswer
- "Get the top answers for a user question" -> POST /knowledgebases/{kbId}/generateAnswer
- "How do I filter answers by metadata?" -> POST /knowledgebases/{kbId}/generateAnswer
- "Can I get multiple ranked answers from the KB?" -> POST /knowledgebases/{kbId}/generateAnswer
- "How do I train my knowledge base on user feedback?" -> POST /knowledgebases/{kbId}/train
- "Submit feedback to improve answer quality" -> POST /knowledgebases/{kbId}/train
- "Mark an answer as correct or incorrect for active learning" -> POST /knowledgebases/{kbId}/train
- "How do I retrain after adding new QnA pairs?" -> POST /knowledgebases/{kbId}/train
- "Ask a question and then train on the result" -> POST /knowledgebases/{kbId}/generateAnswer + POST /knowledgebases/{kbId}/train
- "How do I do active learning with QnA Maker?" -> POST /knowledgebases/{kbId}/generateAnswer then POST /knowledgebases/{kbId}/train

## Response Tips

- **generateAnswer (200):** Response contains ranked answer array with score, id, source, and metadata. Higher scores indicate better matches. An empty answers array means no confident match was found -- check the question phrasing or KB content.
- **train (204):** No response body on success. Any non-204 status indicates the training payload was rejected -- verify feedback body references valid QnA IDs from a prior generateAnswer call.
- **Errors (4xx/5xx):** Look for `error.code` and `error.message` fields. Common codes: `BadArgument` (malformed payload), `Unspecified` (invalid kbId), `Unauthorized` (bad or missing API key).

## Anomaly Flags

- **Low confidence scores:** Surface when the top answer score falls below 30 -- the KB likely lacks coverage for that question.
- **Empty answer arrays:** Proactively warn that the knowledge base returned no matches; suggest rephrasing or checking KB content.
- **401/403 responses:** Flag immediately -- the `Authorization` header API key is missing, expired, or belongs to a different resource.
- **404 on kbId:** The knowledge base ID does not exist or has not been published to the runtime endpoint. Prompt user to verify the KB is published.
- **Train after delete:** If training references QnA IDs that no longer exist, flag the stale feedback loop.
- **Rate limiting (429):** Surface throttling and recommend backing off before retrying; QnA Maker runtime has per-second call limits tied to the pricing tier.

## Playbook

### 1. Ask a Question and Get the Best Answer

1. Identify your knowledge base ID (`kbId`) from the QnA Maker portal.
2. POST to `/knowledgebases/{kbId}/generateAnswer` with `{"question": "your question here"}`.
3. Read the `answers` array from the 200 response.
4. Use the first answer (highest score) as the primary result.
5. If the score is below 50, consider returning a fallback message to the user.

### 2. Active Learning Feedback Loop

1. POST to `/knowledgebases/{kbId}/generateAnswer` with the user's question.
2. Present the top answer(s) to the user and collect feedback (correct/incorrect).
3. Build a train payload mapping the question to the correct QnA pair ID.
4. POST to `/knowledgebases/{kbId}/train` with the feedback body.
5. Confirm the 204 response -- the runtime model will improve on subsequent queries.

### 3. Multi-Turn Conversation with Context

1. POST to `/knowledgebases/{kbId}/generateAnswer` with the initial question.
2. Capture the `context` object from the response (contains prompt suggestions).
3. For the follow-up question, include the previous `context` in the next `generateAnswer` request body.
4. Repeat until the conversation resolves or the user changes topic.

### 4. Metadata-Filtered Query

1. Define metadata key-value pairs in your knowledge base (e.g., `category:billing`).
2. POST to `/knowledgebases/{kbId}/generateAnswer` with `strictFilters` in the payload specifying the metadata filter.
3. Only answers matching the metadata criteria will be returned.
4. Combine with `top` parameter to control how many filtered results come back.

### 5. Batch Testing a Knowledge Base

1. Prepare a list of expected question-answer pairs.
2. For each question, POST to `/knowledgebases/{kbId}/generateAnswer`.
3. Compare the top returned answer against the expected answer.
4. Log mismatches with their scores for review.
5. Use mismatched results to build a train payload and POST to `/knowledgebases/{kbId}/train` to improve accuracy.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
