---
name: calorieninjas
description: "CalorieNinjas API skill. Use when working with CalorieNinjas for nutrition. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# CalorieNinjas
API version: 1.0.0

## Auth
ApiKey api_key in header

## Base URL
api.calorieninjas.com

## Setup
1. Set your API key in the appropriate header
2. GET /v1/nutrition -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### nutrition
| Method | Path | Description |
|--------|------|-------------|
| GET | /v1/nutrition | Get nutrition text for an input string containing food and beverage words. |

## Enhanced Skill Content
## Question Mapping

- "How many calories are in a banana?" -> GET /v1/nutrition
- "What is the protein content of chicken breast?" -> GET /v1/nutrition
- "Give me the full nutrition breakdown for 200g of rice" -> GET /v1/nutrition
- "How much fat is in a tablespoon of olive oil?" -> GET /v1/nutrition
- "Compare the carbs in white bread vs whole wheat bread" -> GET /v1/nutrition (x2, one per food)
- "What are the macros for a meal of steak and potatoes?" -> GET /v1/nutrition (compound query)
- "How much sugar is in 2 cups of orange juice?" -> GET /v1/nutrition
- "Is salmon or tuna higher in protein?" -> GET /v1/nutrition (x2, compare results)
- "What's the sodium content of canned soup?" -> GET /v1/nutrition
- "How many calories in a recipe with 3 eggs, 100g flour, and 50g sugar?" -> GET /v1/nutrition (multi-item query)
- "What are the micronutrients in spinach?" -> GET /v1/nutrition
- "How much fiber is in an avocado?" -> GET /v1/nutrition
- "What's the cholesterol in 200g of shrimp?" -> GET /v1/nutrition

## Response Tips

- **Nutrition results**: Response returns an array of item objects -- each matched food gets its own entry with `calories`, `fat_total_g`, `protein_g`, `carbohydrates_total_g`, `sugar_g`, `fiber_g`, `sodium_mg`, `cholesterol_mg`, `fat_saturated_g`, `serving_size_g`, and `name`. Always check array length; a vague query may return multiple matches or zero.

## Anomaly Flags

- **Empty results array**: The query did not match any known food -- surface this immediately and suggest rephrasing (e.g., use common names, add quantities).
- **Multiple items returned for a single food query**: The API may split compound queries (e.g., "chicken and rice") into separate items -- confirm the user intended a multi-item lookup.
- **Missing API key or 401 response**: The `X-Api-Key` header is required on every request -- prompt the user to set their CalorieNinjas API key.
- **Rate limit (429)**: Free-tier keys have monthly limits -- warn the user when they are making high-volume batch requests.
- **Unexpected serving size**: If `serving_size_g` does not match what the user specified, flag the discrepancy so they can adjust calculations.

## Playbook

### 1. Look Up Nutrition for a Single Food

1. Set the `X-Api-Key` header with your CalorieNinjas API key.
2. Call `GET /v1/nutrition?query=100g chicken breast`.
3. Parse the first item in the response array.
4. Present calories, protein, fat, and carbs to the user.

### 2. Compare Two Foods Side by Side

1. Call `GET /v1/nutrition?query=100g salmon`.
2. Call `GET /v1/nutrition?query=100g tuna`.
3. Extract matching fields (calories, protein, fat) from both responses.
4. Present a side-by-side comparison table.

### 3. Estimate Nutrition for a Full Recipe

1. Break the recipe into individual ingredients with quantities (e.g., "3 eggs", "200g flour", "50g butter").
2. Call `GET /v1/nutrition?query=3 eggs, 200g flour, 50g butter` as a single compound query.
3. Sum the per-item values across all returned items for total recipe nutrition.
4. Optionally divide totals by serving count for per-serving values.

### 4. Daily Intake Tracking

1. For each meal, call `GET /v1/nutrition` with the foods consumed.
2. Accumulate calories, protein, carbs, and fat across all meals.
3. Compare running totals against the user's daily targets.
4. Flag if any macronutrient exceeds or falls significantly short of the goal.

### 5. Find Low-Calorie Alternatives

1. Call `GET /v1/nutrition` for the food the user wants to replace.
2. Note the calorie count and dominant macronutrient.
3. Call `GET /v1/nutrition` for 2-3 suggested alternatives.
4. Present options that are lower in calories while similar in protein or fiber.
5. Highlight the percentage calorie reduction for each alternative.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
