---
name: aws-savings-plans
description: "AWS Savings Plans API skill. Use when working with AWS Savings Plans for CreateSavingsPlan, DeleteQueuedSavingsPlan, DescribeSavingsPlanRates. Covers 10 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Savings Plans
API version: 2019-06-28

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST /CreateSavingsPlan -- create first CreateSavingsPlan

## Endpoints

10 endpoints across 10 groups. See references/api-spec.lap for full details.

### CreateSavingsPlan
| Method | Path | Description |
|--------|------|-------------|
| POST | /CreateSavingsPlan | Creates a Savings Plan. |

### DeleteQueuedSavingsPlan
| Method | Path | Description |
|--------|------|-------------|
| POST | /DeleteQueuedSavingsPlan | Deletes the queued purchase for the specified Savings Plan. |

### DescribeSavingsPlanRates
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeSavingsPlanRates | Describes the rates for the specified Savings Plan. |

### DescribeSavingsPlans
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeSavingsPlans | Describes the specified Savings Plans. |

### DescribeSavingsPlansOfferingRates
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeSavingsPlansOfferingRates | Describes the offering rates for the specified Savings Plans. |

### DescribeSavingsPlansOfferings
| Method | Path | Description |
|--------|------|-------------|
| POST | /DescribeSavingsPlansOfferings | Describes the offerings for the specified Savings Plans. |

### ListTagsForResource
| Method | Path | Description |
|--------|------|-------------|
| POST | /ListTagsForResource | Lists the tags for the specified resource. |

### ReturnSavingsPlan
| Method | Path | Description |
|--------|------|-------------|
| POST | /ReturnSavingsPlan | Returns the specified Savings Plan. |

### TagResource
| Method | Path | Description |
|--------|------|-------------|
| POST | /TagResource | Adds the specified tags to the specified resource. |

### UntagResource
| Method | Path | Description |
|--------|------|-------------|
| POST | /UntagResource | Removes the specified tags from the specified resource. |

## Enhanced Skill Content
## Question Mapping

- "What savings plans do I have?" -> POST /DescribeSavingsPlans
- "Show me all active savings plans" -> POST /DescribeSavingsPlans (with states filter)
- "What are the rates for my savings plan?" -> POST /DescribeSavingsPlanRates
- "What savings plan offerings are available?" -> POST /DescribeSavingsPlansOfferings
- "What are the rate details for available offerings?" -> POST /DescribeSavingsPlansOfferingRates
- "How do I purchase a new savings plan?" -> POST /CreateSavingsPlan
- "Can I return a savings plan?" -> POST /ReturnSavingsPlan
- "How do I cancel a queued savings plan before it starts?" -> POST /DeleteQueuedSavingsPlan
- "What tags are on my savings plan?" -> POST /ListTagsForResource
- "How do I tag a savings plan for cost tracking?" -> POST /TagResource
- "How do I remove tags from a savings plan?" -> POST /UntagResource
- "What EC2 savings plan offerings exist for 1-year terms?" -> POST /DescribeSavingsPlansOfferings (with productType, durations, planTypes filters)
- "Compare payment options for available savings plans" -> POST /DescribeSavingsPlansOfferings (with paymentOptions filter)
- "Find all savings plans in a specific state like payment-failed" -> POST /DescribeSavingsPlans (with states filter)

## Response Tips

- **Describe/List endpoints**: All return optional fields (nullable) -- always nil-check `savingsPlans`, `searchResults`, and `tags` before iterating.
- **Pagination**: `nextToken` in response means more results exist; pass it back in the next request with the same filters. Always loop until `nextToken` is absent.
- **Create/Return endpoints**: Return only `savingsPlanId` (nullable) -- confirm success by the 200 status, then use DescribeSavingsPlans to fetch full details.
- **Delete/Tag/Untag endpoints**: Return no body on success -- a 200 status code is the only confirmation.
- **Filters**: `filters` arrays use typed filter objects (not raw key-value) -- check the SDK for valid filter names and values per endpoint.

## Anomaly Flags

- **Nullable savingsPlanId on create**: If `CreateSavingsPlan` returns 200 but `savingsPlanId` is null, surface this immediately -- the purchase may not have completed.
- **Excessive pagination loops**: If DescribeSavingsPlansOfferings requires more than 10 pages, warn the user their filters may be too broad.
- **Queued plan deletion failure**: `DeleteQueuedSavingsPlan` only works on plans in `queued` state -- surface the current state if the call fails.
- **Return eligibility**: `ReturnSavingsPlan` may fail silently (200 with null id) if the plan is outside its return window -- flag when the returned id is null.
- **State transitions**: Alert when `DescribeSavingsPlans` shows plans in `payment-failed` or `retired` states that were previously active.
- **Tag limit proximity**: AWS enforces a 50-tag limit per resource -- warn when `ListTagsForResource` shows 45+ tags before a `TagResource` call.

## Playbook

### 1. Purchase a New Savings Plan

1. Call `POST /DescribeSavingsPlansOfferings` with desired `productType`, `planTypes`, `durations`, and `paymentOptions` to browse options.
2. Review `searchResults` to identify the right `offeringId` based on rate and terms.
3. Optionally call `POST /DescribeSavingsPlansOfferingRates` with the chosen `savingsPlanOfferingIds` to see per-usage-type rate breakdowns.
4. Call `POST /CreateSavingsPlan` with the selected `savingsPlanOfferingId`, `commitment` amount, and optional `upfrontPaymentAmount`.
5. Confirm by calling `POST /DescribeSavingsPlans` with the returned `savingsPlanId` to verify state is `active` or `queued`.

### 2. Audit and Tag Savings Plans for Cost Allocation

1. Call `POST /DescribeSavingsPlans` (paginate fully) to list all plans.
2. For each plan, call `POST /ListTagsForResource` with its ARN to check existing tags.
3. Identify plans missing required cost-allocation tags (e.g., `team`, `environment`).
4. Call `POST /TagResource` with the missing tags for each untagged plan.
5. To clean up stale tags, call `POST /UntagResource` with the `tagKeys` to remove.

### 3. Cancel a Queued Savings Plan

1. Call `POST /DescribeSavingsPlans` with `states: ["queued"]` to find plans not yet active.
2. Identify the target plan's `savingsPlanId` and verify its start date.
3. Call `POST /DeleteQueuedSavingsPlan` with that `savingsPlanId`.
4. Confirm deletion by calling `POST /DescribeSavingsPlans` with the same id -- it should no longer appear or show a terminal state.

### 4. Review Savings Plan Rate Utilization

1. Call `POST /DescribeSavingsPlans` to get active plan ids.
2. For each plan, call `POST /DescribeSavingsPlanRates` (paginate with `nextToken`).
3. Inspect each `SavingsPlanRate` in `searchResults` to see which services and usage types are covered.
4. Cross-reference with `POST /DescribeSavingsPlansOfferingRates` to compare your committed rates against current offering rates for potential upgrades.

### 5. Return a Savings Plan

1. Call `POST /DescribeSavingsPlans` with the target `savingsPlanId` to confirm it exists and check eligibility (must be within return window).
2. Call `POST /ReturnSavingsPlan` with the `savingsPlanId` and an idempotency `clientToken`.
3. Verify the return by calling `POST /DescribeSavingsPlans` again -- the plan state should transition to a terminal state.
4. If `savingsPlanId` comes back null in the return response, investigate -- the plan may not be eligible for return.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
