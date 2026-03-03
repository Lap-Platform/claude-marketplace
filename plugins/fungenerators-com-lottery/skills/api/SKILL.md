---
name: random-lottery-number-generator-api
description: "Random Lottery Number generator API skill. Use when working with Random Lottery Number generator for lottery. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# Random Lottery Number generator API
API version: 1.5

## Auth
Bearer bearer

## Base URL
https://api.fungenerators.com

## Setup
1. Set Authorization header with your Bearer token
2. GET /lottery/countries -- verify access

## Endpoints

3 endpoints across 1 groups. See references/api-spec.lap for full details.

### lottery
| Method | Path | Description |
|--------|------|-------------|
| GET | /lottery/countries | Get the complete list of countries supported in the number generation API. |
| GET | /lottery/supported | Get the list of supported lottery games supported in the given country. |
| GET | /lottery/draw | Generate random draw for a given lottery game. |

## Enhanced Skill Content
## Question Mapping

- "What countries have lotteries available?" -> GET /lottery/countries
- "Which lottery games are supported?" -> GET /lottery/supported
- "List lotteries for the United States" -> GET /lottery/supported
- "Generate lottery numbers" -> GET /lottery/draw
- "Draw Powerball numbers" -> GET /lottery/draw
- "Give me 5 sets of lottery numbers" -> GET /lottery/draw
- "What games can I play in the UK?" -> GET /lottery/supported
- "Pick random EuroMillions numbers" -> GET /lottery/draw
- "Is there a lottery for Canada?" -> GET /lottery/supported
- "Generate multiple lottery draws at once" -> GET /lottery/draw
- "What lottery options exist for my country?" -> GET /lottery/countries + GET /lottery/supported
- "Help me pick numbers for tonight's draw" -> GET /lottery/supported + GET /lottery/draw
- "Show me all available lottery regions" -> GET /lottery/countries

## Response Tips

- **Countries/Supported**: Expect list responses; iterate to find valid country codes or game identifiers before calling downstream endpoints.
- **Draw**: Results contain generated number sets; when `count` > 1, expect an array of draws rather than a single result.
- **Errors (all endpoints)**: 401 means the Bearer token is missing or invalid -- re-check the `Authorization` header.

## Anomaly Flags

- **401 on any call**: Auth token expired or misconfigured -- surface immediately and prompt for a valid Bearer token.
- **Empty country list**: API may be experiencing issues; warn the user rather than silently returning nothing.
- **Unknown game name in /lottery/draw**: If the game string does not match a value from /lottery/supported, flag the mismatch before making the request.
- **High count values**: Large `count` parameter may slow responses or hit undocumented limits -- warn if count exceeds 10.
- **Missing required params**: `country` is required for /supported and `game` is required for /draw -- catch omissions before calling.

## Playbook

### 1. Discover and Draw Lottery Numbers for a Country

1. Call `GET /lottery/countries` to retrieve the list of available countries.
2. Identify the target country code from the response.
3. Call `GET /lottery/supported?country={code}` to list available games.
4. Pick a game identifier from the results.
5. Call `GET /lottery/draw?game={game}` to generate numbers.

### 2. Generate Multiple Draws for a Specific Game

1. Call `GET /lottery/supported?country={code}` to confirm the game exists.
2. Call `GET /lottery/draw?game={game}&count={n}` with the desired number of draws.
3. Present each draw set to the user individually.

### 3. Compare Lottery Options Across Countries

1. Call `GET /lottery/countries` to get all supported regions.
2. For each country of interest, call `GET /lottery/supported?country={code}`.
3. Compile and compare the available games across countries.
4. Recommend a game based on the user's preference, then draw with `GET /lottery/draw`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
