---
name: spoonacular-api
description: "spoonacular API skill. Use when working with spoonacular for recipes, food, mealplanner. Covers 99 endpoints."
version: 1.0.0
generator: lapsh
---

# spoonacular API
API version: 1.1

## Auth
ApiKey x-api-key in header

## Base URL
https://api.spoonacular.com

## Setup
1. Set your API key in the appropriate header
2. GET /recipes/complexSearch -- verify access
3. POST /recipes/visualizeTaste -- create first visualizeTaste

## Endpoints

99 endpoints across 4 groups. See references/api-spec.lap for full details.

### recipes
| Method | Path | Description |
|--------|------|-------------|
| GET | /recipes/complexSearch | Search Recipes |
| GET | /recipes/findByIngredients | Search Recipes by Ingredients |
| GET | /recipes/findByNutrients | Search Recipes by Nutrients |
| GET | /recipes/{id}/information | Get Recipe Information |
| GET | /recipes/informationBulk | Get Recipe Information Bulk |
| GET | /recipes/{id}/similar | Get Similar Recipes |
| GET | /recipes/random | Get Random Recipes |
| GET | /recipes/autocomplete | Autocomplete Recipe Search |
| GET | /recipes/{id}/tasteWidget.json | Taste by ID |
| GET | /recipes/{id}/tasteWidget.png | Recipe Taste by ID Image |
| GET | /recipes/{id}/equipmentWidget.json | Equipment by ID |
| GET | /recipes/{id}/equipmentWidget.png | Equipment by ID Image |
| GET | /recipes/{id}/priceBreakdownWidget.json | Price Breakdown by ID |
| GET | /recipes/{id}/priceBreakdownWidget.png | Price Breakdown by ID Image |
| GET | /recipes/{id}/ingredientWidget.json | Ingredients by ID |
| GET | /recipes/{id}/ingredientWidget.png | Ingredients by ID Image |
| GET | /recipes/{id}/nutritionWidget.json | Nutrition by ID |
| GET | /recipes/{id}/nutritionWidget.png | Recipe Nutrition by ID Image |
| GET | /recipes/{id}/nutritionLabel | Recipe Nutrition Label Widget |
| GET | /recipes/{id}/nutritionLabel.png | Recipe Nutrition Label Image |
| GET | /recipes/{id}/analyzedInstructions | Get Analyzed Recipe Instructions |
| GET | /recipes/extract | Extract Recipe from Website |
| GET | /recipes/{id}/ingredientWidget | Ingredients by ID Widget |
| GET | /recipes/{id}/tasteWidget | Recipe Taste by ID Widget |
| GET | /recipes/{id}/equipmentWidget | Equipment by ID Widget |
| GET | /recipes/{id}/priceBreakdownWidget | Price Breakdown by ID Widget |
| POST | /recipes/visualizeTaste | Recipe Taste Widget |
| POST | /recipes/visualizeNutrition | Recipe Nutrition Widget |
| POST | /recipes/visualizePriceEstimator | Price Breakdown Widget |
| POST | /recipes/visualizeEquipment | Equipment Widget |
| POST | /recipes/analyze | Analyze Recipe |
| GET | /recipes/{id}/summary | Summarize Recipe |
| GET | /recipes/{id}/card | Create Recipe Card |
| POST | /recipes/visualizeRecipe | Create Recipe Card |
| POST | /recipes/analyzeInstructions | Analyze Recipe Instructions |
| POST | /recipes/cuisine | Classify Cuisine |
| GET | /recipes/queries/analyze | Analyze a Recipe Search Query |
| GET | /recipes/convert | Convert Amounts |
| POST | /recipes/parseIngredients | Parse Ingredients |
| GET | /recipes/{id}/nutritionWidget | Recipe Nutrition by ID Widget |
| POST | /recipes/visualizeIngredients | Ingredients Widget |
| GET | /recipes/guessNutrition | Guess Nutrition by Dish Name |
| GET | /recipes/quickAnswer | Quick Answer |

### food
| Method | Path | Description |
|--------|------|-------------|
| GET | /food/ingredients/{id}/information | Get Ingredient Information |
| GET | /food/ingredients/{id}/amount | Compute Ingredient Amount |
| POST | /food/ingredients/glycemicLoad | Compute Glycemic Load |
| GET | /food/ingredients/autocomplete | Autocomplete Ingredient Search |
| GET | /food/ingredients/search | Ingredient Search |
| GET | /food/ingredients/substitutes | Get Ingredient Substitutes |
| GET | /food/ingredients/{id}/substitutes | Get Ingredient Substitutes by ID |
| GET | /food/products/search | Search Grocery Products |
| GET | /food/products/upc/{upc} | Search Grocery Products by UPC |
| GET | /food/customFoods/search | Search Custom Foods |
| GET | /food/products/{id} | Get Product Information |
| GET | /food/products/upc/{upc}/comparable | Get Comparable Products |
| GET | /food/products/suggest | Autocomplete Product Search |
| GET | /food/products/{id}/nutritionWidget | Product Nutrition by ID Widget |
| GET | /food/products/{id}/nutritionWidget.png | Product Nutrition by ID Image |
| GET | /food/products/{id}/nutritionLabel | Product Nutrition Label Widget |
| GET | /food/products/{id}/nutritionLabel.png | Product Nutrition Label Image |
| POST | /food/products/classify | Classify Grocery Product |
| POST | /food/products/classifyBatch | Classify Grocery Product Bulk |
| POST | /food/ingredients/map | Map Ingredients to Grocery Products |
| GET | /food/menuItems/suggest | Autocomplete Menu Item Search |
| GET | /food/menuItems/search | Search Menu Items |
| GET | /food/menuItems/{id} | Get Menu Item Information |
| GET | /food/menuItems/{id}/nutritionWidget | Menu Item Nutrition by ID Widget |
| GET | /food/menuItems/{id}/nutritionWidget.png | Menu Item Nutrition by ID Image |
| GET | /food/menuItems/{id}/nutritionLabel | Menu Item Nutrition Label Widget |
| GET | /food/menuItems/{id}/nutritionLabel.png | Menu Item Nutrition Label Image |
| GET | /food/restaurants/search | Search Restaurants |
| GET | /food/wine/dishes | Dish Pairing for Wine |
| GET | /food/wine/pairing | Wine Pairing |
| GET | /food/wine/description | Wine Description |
| GET | /food/wine/recommendation | Wine Recommendation |
| GET | /food/images/classify | Image Classification by URL |
| GET | /food/images/analyze | Image Analysis by URL |
| POST | /food/detect | Detect Food in Text |
| GET | /food/site/search | Search Site Content |
| GET | /food/search | Search All Food |
| GET | /food/videos/search | Search Food Videos |
| GET | /food/jokes/random | Random Food Joke |
| GET | /food/trivia/random | Random Food Trivia |
| GET | /food/converse | Talk to Chatbot |
| GET | /food/converse/suggest | Conversation Suggests |

### mealplanner
| Method | Path | Description |
|--------|------|-------------|
| GET | /mealplanner/generate | Generate Meal Plan |
| GET | /mealplanner/{username}/week/{start-date} | Get Meal Plan Week |
| DELETE | /mealplanner/{username}/day/{date} | Clear Meal Plan Day |
| POST | /mealplanner/{username}/items | Add to Meal Plan |
| DELETE | /mealplanner/{username}/items/{id} | Delete from Meal Plan |
| GET | /mealplanner/{username}/templates | Get Meal Plan Templates |
| POST | /mealplanner/{username}/templates | Add Meal Plan Template |
| GET | /mealplanner/{username}/templates/{id} | Get Meal Plan Template |
| DELETE | /mealplanner/{username}/templates/{id} | Delete Meal Plan Template |
| GET | /mealplanner/{username}/shopping-list | Get Shopping List |
| POST | /mealplanner/{username}/shopping-list/{start-date}/{end-date} | Generate Shopping List |
| POST | /mealplanner/{username}/shopping-list/items | Add to Shopping List |
| DELETE | /mealplanner/{username}/shopping-list/items/{id} | Delete from Shopping List |

### users
| Method | Path | Description |
|--------|------|-------------|
| POST | /users/connect | Connect User |

## Enhanced Skill Content
## Question Mapping

- "Find me a vegan pasta recipe under 500 calories?" -> GET /recipes/complexSearch
- "What can I cook with chicken, rice, and broccoli?" -> GET /recipes/findByIngredients
- "Give me a random dessert recipe" -> GET /recipes/random
- "What are the full details for recipe 716429?" -> GET /recipes/{id}/information
- "How many calories are in a Big Mac?" -> GET /food/menuItems/search
- "What wine pairs well with salmon?" -> GET /food/wine/pairing
- "Can I substitute buttermilk in this recipe?" -> GET /food/ingredients/substitutes
- "Convert 2 cups of flour to grams" -> GET /recipes/convert
- "Generate a 2000-calorie meal plan for the week" -> GET /mealplanner/generate
- "What's the nutrition breakdown of recipe 123?" -> GET /recipes/{id}/nutritionWidget.json
- "Show me my shopping list" -> GET /mealplanner/{username}/shopping-list
- "Scan this barcode (UPC 041631000564) for product info" -> GET /food/products/upc/{upc}
- "Find restaurants near me serving Thai food" -> GET /food/restaurants/search
- "Extract the recipe from this blog URL" -> GET /recipes/extract
- "How much iron is in 100g of spinach?" -> GET /food/ingredients/{id}/information

## Response Tips

- **Recipe search** (`complexSearch`, `findByIngredients`, `findByNutrients`): Results are paginated via `offset`/`number`/`totalResults`. Default page size is 10. Set `addRecipeInformation=true` to avoid a follow-up call per recipe.
- **Recipe detail** (`/recipes/{id}/information`): Returns deeply nested objects -- `extendedIngredients[].measures`, `winePairing.productMatches[]`, and `analyzedInstructions[].steps[]` each contain further maps. Check `diets[]` and boolean flags (`vegan`, `glutenFree`, etc.) for dietary filtering.
- **Ingredient/product search** (`/food/ingredients/search`, `/food/products/search`): Same pagination pattern (`offset`/`number`/`totalResults`). Ingredient results use `results[]`, products use `products[]` -- field names differ.
- **Meal planner** endpoints: All user-scoped endpoints require `username` + `hash` (obtained from `POST /users/connect`). Week plans return `days[]` with nested meal slots.
- **Shopping list**: Returns items grouped by `aisles[]` with a total `cost`. Date range is in epoch seconds, not ISO strings.
- **Nutrition widgets**: `.json` variants return structured data; bare paths and `.png` variants return rendered HTML or images respectively. Use the `.json` suffix when you need parseable data.
- **Wine endpoints**: `pairing` takes a food name and returns wines; `dishes` takes a wine name and returns foods -- they are inverses.
- **Error responses**: All endpoints return 401 (invalid/missing API key), 403 (quota exceeded or plan limitation), 404 (resource not found). Error bodies typically include `status`, `code`, and `message` fields.

## Anomaly Flags

- **403 responses**: Surface immediately -- this almost always means the API quota is exhausted or the user's plan does not cover the endpoint. Recommend checking usage at spoonacular.com/food-api/console.
- **Empty `results` with `totalResults > 0`**: The offset has overshot the result set. Alert the user and reset pagination.
- **`confidence` below 0.5** on cuisine classification (`POST /recipes/cuisine`) or image classification (`GET /food/images/classify`): Flag the low-confidence result and suggest the user verify manually.
- **Missing `analyzedInstructions`**: Some recipes return an empty array -- this means spoonacular could not parse steps. Surface this so the user knows to check `instructions` (raw HTML string) or `sourceUrl` instead.
- **Nutrition values of zero**: When `calories`, `protein`, `fat`, or `carbs` come back as `"0"` or zero on a real food item, flag it as likely incomplete data rather than a genuinely zero-calorie food.
- **`guessNutrition` wide confidence ranges**: When `confidenceRange95Percent.max` is more than 3x the `min`, warn the user the estimate is unreliable and suggest using a specific recipe ID lookup instead.
- **Rate limiting / 429 responses**: Although not explicitly in the spec's `@errors`, spoonacular enforces daily point quotas. If requests start failing, surface the remaining quota context.
- **Deprecated `limitLicense` parameter**: Present on many endpoints with a default of `true` -- if it starts returning warnings or behaving unexpectedly, flag for review.

## Playbook

### 1. Search and get full recipe details

1. Call `GET /recipes/complexSearch` with your filters (`query`, `diet`, `cuisine`, `maxCalories`, etc.). Set `number=5` for a manageable list.
2. Review the `results[]` array. Each result has an `id` and `title`.
3. For the chosen recipe, call `GET /recipes/{id}/information` with `includeNutrition=true` to get ingredients, instructions, nutrition, and wine pairing in one call.
4. If step-by-step cooking instructions are needed, call `GET /recipes/{id}/analyzedInstructions` with `stepBreakdown=true`.

### 2. Build a weekly meal plan with shopping list

1. Call `POST /users/connect` with user details to get the `username` and `hash` pair (skip if already connected).
2. Call `GET /mealplanner/generate` with `timeFrame=week`, `targetCalories=2000`, and any `diet`/`exclude` preferences.
3. For each meal in the response, call `POST /mealplanner/{username}/items` to save it to the user's plan with the correct `date`, `slot`, and `position`.
4. Once all meals are added, call `POST /mealplanner/{username}/shopping-list/{start-date}/{end-date}` to generate the consolidated shopping list.
5. Review the shopping list via `GET /mealplanner/{username}/shopping-list` -- items are organized by `aisles[]` with estimated `cost`.

### 3. Identify a food from an image and get nutrition

1. Host or obtain a public URL for the food image.
2. Call `GET /food/images/classify` with `imageUrl` to identify what the food is. Check `probability` -- if below 0.5, ask the user to confirm.
3. Call `GET /food/images/analyze` with the same `imageUrl` to get estimated nutrition (calories, fat, protein, carbs) with confidence ranges.
4. If the analysis suggests matching recipes, use the `recipes[]` array from the response to call `GET /recipes/{id}/information` for full details.

### 4. Find ingredient substitutes and convert units

1. Call `GET /food/ingredients/search` with `query` to find the ingredient and get its `id`.
2. Call `GET /food/ingredients/{id}/substitutes` to get a list of possible substitutes with context.
3. If a unit conversion is needed (e.g., cups to grams), call `GET /recipes/convert` with `ingredientName`, `sourceAmount`, `sourceUnit`, and `targetUnit`.
4. For full nutritional detail on the ingredient, call `GET /food/ingredients/{id}/information` with the desired `amount` and `unit`.

### 5. Scan a product barcode and compare alternatives

1. Call `GET /food/products/upc/{upc}` with the barcode number to get product details, nutrition, and `spoonacularScore`.
2. Call `GET /food/products/upc/{upc}/comparable` to find alternatives ranked by calories, protein, price, sugar, and score.
3. For any promising alternative, call `GET /food/products/{id}` to get full details.
4. Use `GET /food/products/{id}/nutritionWidget.json` (via `Accept: application/json`) to get a structured nutrition comparison between the original and the alternative.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
