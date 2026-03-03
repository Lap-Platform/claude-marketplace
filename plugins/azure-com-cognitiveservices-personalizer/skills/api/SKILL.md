---
name: personalizer-client
description: "Personalizer Client API skill. Use when working with Personalizer Client for configurations, evaluations, events. Covers 17 endpoints."
version: 1.0.0
generator: lapsh
---

# Personalizer Client
API version: v1.0

## Auth
ApiKey Ocp-Apim-Subscription-Key in header

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /configurations/service -- verify access
3. POST /evaluations -- create first evaluations

## Endpoints

17 endpoints across 6 groups. See references/api-spec.lap for full details.

### configurations
| Method | Path | Description |
|--------|------|-------------|
| GET | /configurations/service | Get Service Configuration. |
| PUT | /configurations/service | Update Service Configuration. |
| GET | /configurations/policy | Get Policy. |
| PUT | /configurations/policy | Update Policy. |
| DELETE | /configurations/policy | Reset Policy. |

### evaluations
| Method | Path | Description |
|--------|------|-------------|
| GET | /evaluations/{evaluationId} | Get Evaluation. |
| DELETE | /evaluations/{evaluationId} | Delete Evaluation. |
| GET | /evaluations | List Evaluations. |
| POST | /evaluations | Create Evaluation. |

### events
| Method | Path | Description |
|--------|------|-------------|
| POST | /events/{eventId}/reward | Post Reward. |
| POST | /events/{eventId}/activate | Activate Event. |

### logs
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /logs | Deletes Logs. |
| GET | /logs/properties | Get Log Properties. |

### model
| Method | Path | Description |
|--------|------|-------------|
| GET | /model | Get Model. |
| DELETE | /model | Reset Model. |
| GET | /model/properties | Get Model Properties. |

### rank
| Method | Path | Description |
|--------|------|-------------|
| POST | /rank | Post Rank. |

## Enhanced Skill Content
## Question Mapping

- "How do I get personalized recommendations for a user?" -> POST /rank
- "How do I send a reward signal after a user clicked?" -> POST /events/{eventId}/reward
- "How do I activate an event for billing?" -> POST /events/{eventId}/activate
- "What is my current service configuration?" -> GET /configurations/service
- "How do I update the exploration percentage?" -> PUT /configurations/service
- "What learning policy is currently active?" -> GET /configurations/policy
- "How do I upload a custom learning policy?" -> PUT /configurations/policy
- "How do I reset the policy to default?" -> DELETE /configurations/policy
- "How do I run an offline evaluation?" -> POST /evaluations
- "What is the status of my evaluation?" -> GET /evaluations/{evaluationId}
- "How do I list all past evaluations?" -> GET /evaluations
- "How do I cancel or remove an evaluation?" -> DELETE /evaluations/{evaluationId}
- "How do I download the current model?" -> GET /model
- "How do I reset the model and start fresh?" -> DELETE /model
- "What features is the model currently using?" -> GET /model/properties

## Response Tips

- **rank**: Response includes `rewardActionId` and `eventId` -- always store the `eventId` to send rewards later.
- **events**: Reward and activate return 204 with no body; any other status means the eventId was invalid or expired.
- **configurations**: Service config returns nested maps with exploration rate, reward settings, and learning parameters -- check `rewardWaitTime` and `explorationPercentage` specifically.
- **evaluations**: POST returns 201 with the evaluation object including status; poll GET /evaluations/{id} until status is complete.
- **logs**: DELETE returns 204 on success; GET /logs/properties returns feature metadata used in logged interactions.
- **model**: GET returns binary model data (not JSON) -- set Accept header appropriately; /model/properties returns JSON feature summaries.

## Anomaly Flags

- **Reward not sent**: If a Rank call is made but no corresponding reward is posted within the configured `rewardWaitTime`, flag it -- the model trains on default reward values which degrades performance.
- **Event activation missing**: Events that are ranked but never activated may indicate wasted billing or misconfigured client integration.
- **Model reset triggered**: DELETE /model wipes all learned behavior -- surface a warning before and after this call.
- **Policy reset**: DELETE /configurations/policy reverts to default -- flag when this happens unexpectedly.
- **Evaluation backlog**: Multiple evaluations in pending state may indicate resource contention or misconfigured evaluation parameters.
- **Low exploration rate**: If GET /configurations/service shows explorationPercentage near 0, flag that the model cannot discover better actions.
- **429 or 503 responses**: Rate limiting or service degradation -- back off and surface the retry-after header if present.

## Playbook

### 1. Basic Rank-Reward Loop

1. Build a rank request with context features and action features
2. Call POST /rank with the request body
3. Display the recommended action (`rewardActionId`) to the user
4. Observe the outcome (click, purchase, dwell time)
5. Call POST /events/{eventId}/reward with the computed reward value (0.0 to 1.0)

### 2. Run an Offline Evaluation

1. Call GET /configurations/policy to note the current policy
2. Call POST /evaluations with the evaluation name, start/end dates, and candidate policies
3. Poll GET /evaluations/{evaluationId} until status shows complete
4. Compare reward scores across policies in the response
5. If a candidate policy wins, call PUT /configurations/policy to deploy it

### 3. Tune Service Configuration

1. Call GET /configurations/service to retrieve current settings
2. Review `explorationPercentage`, `rewardWaitTime`, `rewardAggregation`, and `modelExportFrequency`
3. Modify the desired fields in the config map
4. Call PUT /configurations/service with the updated configuration
5. Monitor rank responses over the next few hours to confirm behavior change

### 4. Reset and Retrain from Scratch

1. Call GET /model/properties to document current feature usage (save for comparison)
2. Call DELETE /model to wipe the learned model
3. Call DELETE /configurations/policy to revert to the default learning policy
4. Optionally call DELETE /logs to clear historical interaction data
5. Resume the rank-reward loop -- the model will retrain from new interactions

### 5. Diagnose Feature Utilization

1. Call GET /model/properties to see which context and action features the model uses
2. Call GET /logs/properties to see which features appear in logged interactions
3. Compare the two -- features logged but not used by the model may need different encoding
4. Adjust context or action features in your rank requests accordingly
5. After collecting new data, re-check GET /model/properties to confirm the model picks up the changes


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
