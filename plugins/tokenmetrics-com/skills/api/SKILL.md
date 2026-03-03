---
name: endpoints
description: "Endpoints API skill. Use when working with Endpoints for tokens, trader-grades, investor-grades. Covers 14 endpoints."
version: 1.0.0
generator: lapsh
---

# Endpoints

## Auth
ApiKey key in header

## Base URL
https://api.tokenmetrics.com

## Setup
1. Set your API key in the appropriate header
2. GET /v1/tokens -- verify access

## Endpoints

14 endpoints across 14 groups. See references/api-spec.lap for full details.

### tokens
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/tokens | Tokens |

### trader-grades
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/trader-grades | Trader Grades |

### investor-grades
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/investor-grades | Investor Grades |

### market-indicator
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/market-indicator | Market Indicator |

### trading-indicator
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/trading-indicator | Trading Indicator |

### resistance-support
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/resistance-support | Resistance & Support |

### price
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/price | Price |

### price-prediction
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/price-prediction | Price Prediction |

### sentiments
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/sentiments | Sentiments |

### quantmetrics-tier-1
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/quantmetrics-tier-1 | Quantmetrics Tier 1 |

### quantmetrics-tier-2
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/quantmetrics-tier-2 | Quantmetrics Tier 2 |

### scenario-analysis
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/scenario-analysis | Scenario Analysis |

### correlation
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/correlation | Correlation |

### indices
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/indices | Indices |

## Enhanced Skill Content


## Question Mapping

- "What tokens are available on TokenMetrics?" -> GET /v1/tokens
- "Look up a token by its symbol or name" -> GET /v1/tokens
- "What is the trader grade for Bitcoin this month?" -> GET /v1/trader-grades
- "Show me investor grades for ETH over the last 90 days" -> GET /v1/investor-grades
- "Is the overall crypto market bullish or bearish right now?" -> GET /v1/market-indicator
- "What are the current trading signals for SOL?" -> GET /v1/trading-indicator
- "Where are the support and resistance levels for BTC?" -> GET /v1/resistance-support
- "Get the historical price of Ethereum for the past week" -> GET /v1/price
- "What is the price prediction for Bitcoin tomorrow?" -> GET /v1/price-prediction
- "What is the market sentiment around Cardano?" -> GET /v1/sentiments
- "Show quant metrics for my token portfolio" -> GET /v1/quantmetrics-tier-1
- "Get advanced quantitative analysis for SOL" -> GET /v1/quantmetrics-tier-2
- "What happens to BTC price under different market scenarios?" -> GET /v1/scenario-analysis
- "How correlated are ETH and BTC?" -> GET /v1/correlation
- "Show me index performance across exchanges" -> GET /v1/indices

## Response Tips

- **Tokens**: Results are lookup records; use `token_ids` from here as the `tokens` param in all other endpoints.
- **Grades (trader/investor)**: Grades are date-ranged; always check `startDate`/`endDate` bounds in the response to confirm coverage.
- **Market Indicator**: Returns market-wide signals, not per-token; no `tokens` param needed.
- **Price**: Only endpoint with `page` param; paginate when `limit` is reached and more data exists.
- **Predictions & Scenarios**: Point-in-time results tied to a single `date`; absence of data means the model has no prediction for that token/date.
- **Quant Metrics (Tier 1 vs 2)**: Tier 2 includes deeper analytics; use Tier 1 for screening, Tier 2 for deep dives.
- **Sentiments**: Scores are date-ranged aggregates; short ranges give daily granularity, long ranges may be summarized.
- **Correlation & Resistance-Support**: Multi-token queries return pairwise or per-token blocks; parse by token identifier.
- **Indices**: Requires `exchanges` and `timeHorizon`; `lowCap` flag filters small-cap tokens in/out.

## Anomaly Flags

- **Missing token data**: If a grades, prediction, or quant endpoint returns empty for a known token, surface that the token may be unsupported or too new for model coverage.
- **Date range gaps**: When response data does not span the full requested `startDate`-`endDate`, flag the missing intervals.
- **Stale predictions**: If `price-prediction` returns a date older than the requested date, warn that predictions may not be current.
- **Pagination exhaustion**: On `/v1/price`, if results equal the `limit` and a `page` param was used, alert that more pages likely exist.
- **Market indicator extremes**: When market indicator values hit historical extremes (strong bull/bear), proactively surface the signal.
- **API key errors**: Any 401/403 response should immediately surface an authentication issue; the API uses header-based ApiKey auth.
- **Rate limiting**: Surface any 429 responses or rate-limit headers before they cause workflow failures.

## Playbook

### 1. Portfolio Health Check

1. Call `GET /v1/tokens` with your token symbols to resolve token IDs.
2. Call `GET /v1/trader-grades` with those tokens and a 30-day date range.
3. Call `GET /v1/investor-grades` with the same tokens and range.
4. Call `GET /v1/sentiments` for the same set.
5. Compare trader vs investor grades and sentiment to flag divergences.

### 2. Trade Setup Analysis

1. Call `GET /v1/tokens` to resolve the target token.
2. Call `GET /v1/trading-indicator` for the current signal (buy/sell/hold).
3. Call `GET /v1/resistance-support` for key price levels.
4. Call `GET /v1/price-prediction` with today's date for the model forecast.
5. Cross-reference the trading signal with support/resistance and the prediction to form a thesis.

### 3. Market Regime Assessment

1. Call `GET /v1/market-indicator` for the past 30 days.
2. Call `GET /v1/indices` across major exchanges with a matching date range.
3. Call `GET /v1/correlation` for top tokens (BTC, ETH) to check if correlations are tightening.
4. Synthesize: rising indicator + tightening correlation = risk-on regime; diverging signals = transitional.

### 4. Deep Dive on a Single Token

1. Resolve the token via `GET /v1/tokens`.
2. Pull 90-day price history via `GET /v1/price` (paginate if needed).
3. Fetch `GET /v1/quantmetrics-tier-1` for a quick score, then `GET /v1/quantmetrics-tier-2` for full analysis.
4. Run `GET /v1/scenario-analysis` to see upside/downside projections.
5. Check `GET /v1/sentiments` for recent sentiment shifts that quant models may not capture.

### 5. Historical Price Export

1. Resolve token IDs via `GET /v1/tokens`.
2. Call `GET /v1/price` with `startDate`, `endDate`, `limit`, and `page=1`.
3. If results fill the limit, increment `page` and repeat until fewer results than `limit` are returned.
4. Concatenate all pages into the full dataset.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
