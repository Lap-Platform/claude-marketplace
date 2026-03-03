---
name: amazon-personalize-runtime
description: "Amazon Personalize Runtime API skill. Use when working with Amazon Personalize Runtime for action-recommendations, personalize-ranking, recommendations. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Personalize Runtime
API version: 2018-05-22

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /action-recommendations -- create first action-recommendations

## Endpoints

3 endpoints across 3 groups. See references/api-spec.lap for full details.

### action-recommendations
| Method | Path | Description |
|--------|------|-------------|
| POST | /action-recommendations | Returns a list of recommended actions in sorted in descending order by prediction score. Use the GetActionRecommendations API if you have a custom campaign that deploys a solution version trained with a PERSONALIZED_ACTIONS recipe.  For more information about PERSONALIZED_ACTIONS recipes, see PERSONALIZED_ACTIONS recipes. For more information about getting action recommendations, see Getting action recommendations. |

### personalize-ranking
| Method | Path | Description |
|--------|------|-------------|
| POST | /personalize-ranking | Re-ranks a list of recommended items for the given user. The first item in the list is deemed the most likely item to be of interest to the user.  The solution backing the campaign must have been created using a recipe of type PERSONALIZED_RANKING. |

### recommendations
| Method | Path | Description |
|--------|------|-------------|
| POST | /recommendations | Returns a list of recommended items. For campaigns, the campaign's Amazon Resource Name (ARN) is required and the required user and item input depends on the recipe type used to create the solution backing the campaign as follows:   USER_PERSONALIZATION - userId required, itemId not used   RELATED_ITEMS - itemId required, userId not used    Campaigns that are backed by a solution created using a recipe of type PERSONALIZED_RANKING use the API.   For recommenders, the recommender's ARN is required and the required item and user input depends on the use case (domain-based recipe) backing the recommender. For information on use case requirements see Choosing recommender use cases. |

## Enhanced Skill Content
## Question Mapping

- "What items should I recommend to this user?" -> POST /recommendations
- "How do I get personalized recommendations for a specific user?" -> POST /recommendations
- "What actions should a user take next?" -> POST /action-recommendations
- "How do I re-rank a list of items for a specific user?" -> POST /personalize-ranking
- "How do I filter recommendations by category or attribute?" -> POST /recommendations (use filterArn + filterValues)
- "Can I boost specific items in recommendation results?" -> POST /recommendations (use promotions)
- "How do I get similar item recommendations?" -> POST /recommendations (use itemId without userId)
- "How do I rank search results using personalization?" -> POST /personalize-ranking
- "How do I limit the number of recommended items returned?" -> POST /recommendations (use numResults)
- "How do I pass real-time context like device type or location into recommendations?" -> POST /recommendations (use context)
- "What actions should I suggest when I only have a campaign ARN?" -> POST /action-recommendations
- "How do I get metadata columns back with my recommendations?" -> POST /personalize-ranking (use metadataColumns)
- "How do I use a recommender ARN instead of a campaign ARN?" -> POST /recommendations (use recommenderArn)
- "How do I combine user-based and item-based recommendations with filtering?" -> POST /recommendations (use userId + itemId + filterArn + filterValues)

## Response Tips

- **Recommendations & Action-Recommendations**: Results arrive in `itemList` or `actionList` arrays of scored objects; both fields are nullable, so always check for empty/null before iterating. Save `recommendationId` for A/B testing attribution.
- **Personalize-Ranking**: `personalizedRanking` returns items in re-ranked order matching your `inputList` length; a null array means the model could not rank -- fall back to original order.
- **Errors**: All three endpoints use standard AWS error shapes; watch for `ResourceNotFoundException` (bad ARN), `InvalidInputException` (missing required fields or malformed filterValues), and `TooManyRequestsException` (throttling).

## Anomaly Flags

- **TooManyRequestsException (429)**: Surface immediately -- indicates campaign TPS limit hit; suggest backing off or requesting a limit increase.
- **Null/empty result arrays**: Flag when `itemList`, `actionList`, or `personalizedRanking` returns null or empty -- may indicate a cold-start problem, expired campaign, or misconfigured solution version.
- **Missing recommendationId**: If absent from response, event tracking and A/B attribution will break -- warn the user.
- **filterValues without filterArn**: If the request includes `filterValues` but omits `filterArn`, the filter is silently ignored -- flag the mismatch.
- **campaignArn and recommenderArn both absent**: POST /recommendations requires at least one; surface this before sending the request.
- **inputList length in ranking**: If `personalizedRanking` returns fewer items than `inputList`, some items were filtered out -- alert the caller to the discrepancy.

## Playbook

### 1. Get User Recommendations with Filtering

1. Identify the campaign ARN or recommender ARN for your use case.
2. Call `POST /recommendations` with `userId`, `campaignArn` (or `recommenderArn`), and desired `numResults`.
3. To filter, add `filterArn` pointing to your Personalize filter and populate `filterValues` with dynamic parameters.
4. Parse `itemList` from the response and render results.
5. Store `recommendationId` to log impression events back to Personalize for model improvement.

### 2. Re-rank Search Results for a User

1. Obtain a list of candidate item IDs from your search engine or catalog query.
2. Call `POST /personalize-ranking` with `campaignArn`, `userId`, and `inputList` containing the candidate IDs.
3. Optionally pass `context` (e.g., `{"device": "mobile"}`) for real-time context signals.
4. Replace your original result order with the `personalizedRanking` array.
5. Fall back to original order if the response array is null.

### 3. Suggest Next Best Actions

1. Call `POST /action-recommendations` with `campaignArn` and `userId`.
2. Optionally set `numResults` to limit returned actions and `filterArn`/`filterValues` to exclude completed actions.
3. Iterate over `actionList` and present the top-scored actions to the user.
4. Track which action the user selects using the `recommendationId`.

### 4. Similar Items (Item-to-Item) Recommendations

1. Call `POST /recommendations` with `itemId` set to the seed item and `campaignArn` pointing to a SIMS or Similar-Items campaign.
2. Omit `userId` for pure item similarity, or include it to blend collaborative filtering.
3. Use `numResults` to control how many related items come back.
4. Optionally add `promotions` to ensure specific business-priority items appear in results.
5. Render `itemList` as "customers also viewed" or "related items."

### 5. Contextual Recommendations with Metadata

1. Call `POST /recommendations` with `userId`, `campaignArn`, and a `context` map containing real-time signals (e.g., `{"timeOfDay": "evening", "platform": "ios"}`).
2. Add `metadataColumns` to request item metadata inline (e.g., `{"ITEMS": ["GENRE", "TITLE"]}`) so you avoid a separate catalog lookup.
3. Parse each entry in `itemList` for both the item ID and any returned metadata fields.
4. Use the metadata to render rich recommendation cards without additional API calls.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
