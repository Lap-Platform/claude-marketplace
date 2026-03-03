---
name: psycholinguistic-text-analytics
description: "Psycholinguistic Text Analytics API skill. Use when working with Psycholinguistic Text Analytics for communication, emotion, ekman-emotion. Covers 8 endpoints."
version: 1.0.0
generator: lapsh
---

# Psycholinguistic Text Analytics
API version: 1.0

## Auth
ApiKey x-api-key in header

## Base URL
https://api.symanto.net

## Setup
1. Set your API key in the appropriate header
3. POST /communication -- create first communication

## Endpoints

8 endpoints across 8 groups. See references/api-spec.lap for full details.

### communication
| Method | Path | Description |
|--------|------|-------------|
| POST | /communication | Communication & Tonality |

### emotion
| Method | Path | Description |
|--------|------|-------------|
| POST | /emotion | Emotion Analysis |

### ekman-emotion
| Method | Path | Description |
|--------|------|-------------|
| POST | /ekman-emotion | Emotion Analysis |

### personality
| Method | Path | Description |
|--------|------|-------------|
| POST | /personality | Personality Traits |

### sentiment
| Method | Path | Description |
|--------|------|-------------|
| POST | /sentiment | Sentiment Analysis |

### topic-sentiment
| Method | Path | Description |
|--------|------|-------------|
| POST | /topic-sentiment | Extracts topics and sentiments and relates them. |

### brand-recommendation
| Method | Path | Description |
|--------|------|-------------|
| POST | /brand-recommendation | Predicts whether a phrase is a promoter, detractor or indifferent |

### language-detection
| Method | Path | Description |
|--------|------|-------------|
| POST | /language-detection | Language Detection |

## Enhanced Skill Content
## Question Mapping

- "What communication style does this text use?" -> POST /communication
- "Is this text fact-oriented or feeling-oriented?" -> POST /communication
- "What emotion does this review express?" -> POST /emotion
- "Detect all emotions in this customer feedback" -> POST /emotion (all=True)
- "What Ekman basic emotion is in this text?" -> POST /ekman-emotion
- "Is the author angry, sad, or happy?" -> POST /ekman-emotion (all=True)
- "What personality traits does this writer show?" -> POST /personality
- "Is this text written by an introvert or extrovert?" -> POST /personality
- "Is this review positive or negative?" -> POST /sentiment
- "What's the sentiment of these survey responses?" -> POST /sentiment
- "What topics are mentioned and how do people feel about them?" -> POST /topic-sentiment
- "What aspects of this hotel do guests complain about?" -> POST /topic-sentiment (domain=Hotel)
- "Would this customer recommend the brand?" -> POST /brand-recommendation
- "Predict brand advocacy from these airline reviews" -> POST /brand-recommendation (domain=Airlines)
- "What language is this text written in?" -> POST /language-detection

## Response Tips

- **Communication/Personality**: Results return psycholinguistic trait predictions per input text; when `all=True`, expect multiple scored categories instead of just the top prediction.
- **Emotion/Ekman-Emotion**: Each input returns detected emotion labels with confidence scores; Ekman limits to the six universal emotions (anger, disgust, fear, joy, sadness, surprise).
- **Sentiment**: Returns polarity (positive/negative) per text item; batch inputs return an array in the same order as the request.
- **Topic-Sentiment**: Returns extracted topics with per-topic sentiment; the `domain` parameter tunes extraction to industry-specific vocabulary.
- **Brand-Recommendation**: Returns a recommendation likelihood score; the `domain` parameter selects the industry-tuned model.
- **Language-Detection**: Returns ISO language codes with confidence; useful as a pre-processing step before calling other endpoints.
- **Errors (422)**: Validation error -- check that request body is a valid array of text objects and no fields are missing or malformed.

## Anomaly Flags

- **422 on any endpoint**: Surface the validation error detail immediately -- most common cause is malformed request body (missing `text` or `language` fields in input objects).
- **Empty predictions**: If emotion, sentiment, or personality returns with low confidence or empty results, flag that the input text may be too short or ambiguous for reliable analysis.
- **Domain mismatch**: If topic-sentiment or brand-recommendation is called with a domain that doesn't match the input text's industry, warn that results may be unreliable.
- **Language not supported**: If language-detection returns an unexpected language, proactively suggest whether the other endpoints support that language before making further calls.
- **Batch size**: If a large batch returns partial results or timeouts, flag potential payload size limits and suggest splitting the request.

## Playbook

### 1. Full Psycholinguistic Profile of a Text

1. Call `POST /language-detection` to confirm the text language is supported.
2. Call `POST /sentiment` to get overall polarity.
3. Call `POST /emotion` with `all=True` to get the full emotional spectrum.
4. Call `POST /personality` with `all=True` to extract personality traits.
5. Call `POST /communication` to determine communication style.
6. Combine results into a unified profile: language, sentiment, dominant emotions, personality traits, and communication style.

### 2. Analyze Customer Reviews by Topic

1. Determine the industry domain (e.g., Hotel, Restaurant, Ecom).
2. Call `POST /topic-sentiment` with the matching `domain` parameter to extract topics and per-topic sentiment.
3. Call `POST /sentiment` on the same texts to get overall sentiment as a baseline.
4. Compare per-topic sentiments against overall sentiment to identify specific pain points or strengths.

### 3. Brand Advocacy Prediction Pipeline

1. Call `POST /language-detection` to filter out unsupported languages.
2. Call `POST /sentiment` to separate positive and negative reviews.
3. Call `POST /brand-recommendation` with the appropriate `domain` to predict advocacy likelihood.
4. Cross-reference: flag cases where sentiment is positive but recommendation is low (or vice versa) as items needing human review.

### 4. Multilingual Feedback Triage

1. Call `POST /language-detection` on all incoming feedback.
2. Group texts by detected language.
3. For each language group, call `POST /ekman-emotion` with `all=True` to detect urgent emotions (anger, sadness).
4. Call `POST /sentiment` on the high-urgency subset to confirm negative polarity.
5. Route angry/negative items to priority support queues.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
