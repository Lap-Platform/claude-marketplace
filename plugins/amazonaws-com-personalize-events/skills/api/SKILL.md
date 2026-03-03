---
name: amazon-personalize-events
description: "Amazon Personalize Events API skill. Use when working with Amazon Personalize Events for action-interactions, actions, events. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Personalize Events
API version: 2018-03-22

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /action-interactions -- create first action-interactions

## Endpoints

5 endpoints across 5 groups. See references/api-spec.lap for full details.

### action-interactions
| Method | Path | Description |
|--------|------|-------------|
| POST | /action-interactions | Records action interaction event data. An action interaction event is an interaction between a user and an action. For example, a user taking an action, such a enrolling in a membership program or downloading your app.  For more information about recording action interactions, see Recording action interaction events. For more information about actions in an Actions dataset, see Actions dataset. |

### actions
| Method | Path | Description |
|--------|------|-------------|
| POST | /actions | Adds one or more actions to an Actions dataset. For more information see Importing actions individually. |

### events
| Method | Path | Description |
|--------|------|-------------|
| POST | /events | Records item interaction event data. For more information see Recording item interaction events. |

### items
| Method | Path | Description |
|--------|------|-------------|
| POST | /items | Adds one or more items to an Items dataset. For more information see Importing items individually. |

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /users | Adds one or more users to a Users dataset. For more information see Importing users individually. |

## Enhanced Skill Content
## Question Mapping

- "How do I record a user clicking on a recommendation?" -> POST /events
- "How do I send user interaction events to Personalize?" -> POST /events
- "How do I track what actions users take on recommended items?" -> POST /action-interactions
- "How do I import actions into my Personalize dataset?" -> POST /actions
- "How do I add or update items in my catalog?" -> POST /items
- "How do I add or update user profiles?" -> POST /users
- "How do I send a batch of events for a single session?" -> POST /events (multiple entries in eventList)
- "How do I record anonymous user activity without a userId?" -> POST /events (omit optional userId)
- "How do I bulk-import item metadata?" -> POST /items (multiple entries in items array)
- "How do I associate a tracking ID with user interactions?" -> POST /events or POST /action-interactions (trackingId required)
- "How do I record that a user dismissed a recommendation?" -> POST /action-interactions
- "How do I update a user's properties after they edit their profile?" -> POST /users
- "What dataset ARN do I need for importing items?" -> POST /items (datasetArn is required)
- "How do I send real-time events for a logged-in user?" -> POST /events (include userId)

## Response Tips

- **Events / Action-Interactions**: Fire-and-forget ingestion; a 200 means accepted. No response body beyond confirmation. Watch for 4xx validation errors on malformed eventList or missing trackingId.
- **Actions / Items / Users**: Batch import endpoints; partial failures may not raise a top-level error. Check for per-record error details in the response if the batch is large.
- **All endpoints**: AWS errors return `__type` and `message` fields. Common codes: `InvalidInputException` (bad payload), `ResourceNotFoundException` (wrong ARN or trackingId), `ResourceInUseException` (dataset locked).

## Anomaly Flags

- **Throttling**: Surface `ThrottlingException` or HTTP 429 immediately; recommend exponential backoff and smaller batch sizes.
- **Invalid ARN references**: Flag `ResourceNotFoundException` early since it usually means the dataset ARN is wrong or the event tracker was deleted.
- **Missing trackingId**: If a user tries to call /events or /action-interactions without a trackingId, warn that this must come from `CreateEventTracker` in the main Personalize API (not this Events API).
- **Large batch sizes**: Warn when items/actions/users arrays exceed ~10 entries per call, as the service has per-request size limits.
- **Anonymous sessions**: If /events calls consistently omit userId, surface a note that Personalize recommendations work best with identified users.
- **Deprecated dataset types**: Flag if datasetArn points to a dataset type not aligned with the endpoint (e.g., passing an Items dataset ARN to /users).

## Playbook

### 1. Record Real-Time User Events

1. Obtain your `trackingId` from `CreateEventTracker` (main Personalize API).
2. Generate or reuse a `sessionId` for the user's browsing session.
3. Build an `eventList` array with one or more Event objects (eventType, sentAt, etc.).
4. Call `POST /events` with `trackingId`, `sessionId`, `eventList`, and optionally `userId`.
5. Verify a 200 response. On throttle (429), back off and retry.

### 2. Import Item Catalog

1. Locate your Items dataset ARN from the Personalize console or `DescribeDataset`.
2. Build an `items` array with Item objects containing itemId and metadata properties.
3. Call `POST /items` with `datasetArn` and the `items` array.
4. Check the response for per-record errors.
5. Repeat in batches if you have more items than the per-request limit.

### 3. Sync User Profiles

1. Retrieve your Users dataset ARN.
2. Collect user property updates (userId, properties map).
3. Call `POST /users` with `datasetArn` and the `users` array.
4. Confirm success; handle `InvalidInputException` if properties don't match the schema.

### 4. Track Action Interactions for Contextual Recommendations

1. Obtain your `trackingId` from the event tracker.
2. Build an `actionInteractions` array with ActionInteraction objects (actionId, eventType, etc.).
3. Call `POST /action-interactions` with `trackingId` and `actionInteractions`.
4. Use these interaction signals alongside /events data to improve action-based recommendations.

### 5. Bootstrap a New Personalize Campaign with Historical Data

1. Import your item catalog via `POST /items` (batch by dataset ARN).
2. Import user profiles via `POST /users` (batch by dataset ARN).
3. Import historical actions via `POST /actions` if using action-based recommendations.
4. Begin streaming real-time events via `POST /events` once your solution version is active.
5. Monitor for throttling across all endpoints during the initial bulk load.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
