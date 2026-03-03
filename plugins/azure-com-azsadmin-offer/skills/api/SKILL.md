---
name: subscriptionclient
description: "SubscriptionClient API skill. Use when working with SubscriptionClient for delegatedProviders, offers. Covers 3 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /offers -- verify access

## Endpoints

3 endpoints across 2 groups. See references/api-spec.lap for full details.

### delegatedProviders
| Method | Path | Description |
|--------|------|-------------|
| GET | /delegatedProviders/{delegatedProviderId}/offers | Get the list of offers for the specified delegated provider. |
| GET | /delegatedProviders/{delegatedProviderId}/offers/{offerName} | Get the specified offer for the delegated provider. |

### offers
| Method | Path | Description |
|--------|------|-------------|
| GET | /offers | Get the list of public offers for the root provider. |

## Enhanced Skill Content
## Question Mapping

- "What offers are available for a delegated provider?" -> GET /delegatedProviders/{delegatedProviderId}/offers
- "List all offers from delegated provider X" -> GET /delegatedProviders/{delegatedProviderId}/offers
- "Get details about a specific offer from a delegated provider" -> GET /delegatedProviders/{delegatedProviderId}/offers/{offerName}
- "Does delegated provider X have offer Y?" -> GET /delegatedProviders/{delegatedProviderId}/offers/{offerName}
- "What offers exist in the subscription?" -> GET /offers
- "List all available offers" -> GET /offers
- "Show me everything a delegated provider is offering" -> GET /delegatedProviders/{delegatedProviderId}/offers
- "What are the properties of offer Z under provider X?" -> GET /delegatedProviders/{delegatedProviderId}/offers/{offerName}
- "Compare offers across all delegated providers" -> GET /delegatedProviders/{delegatedProviderId}/offers (iterate per provider)
- "Which delegated provider has a specific offer?" -> GET /offers then GET /delegatedProviders/{delegatedProviderId}/offers/{offerName} per provider
- "Are there any offers I can subscribe to?" -> GET /offers
- "Verify a specific offer still exists for a provider" -> GET /delegatedProviders/{delegatedProviderId}/offers/{offerName}

## Response Tips

- **delegatedProviders/offers (list):** Response is typically a JSON array wrapper with a `value` property containing offer objects. Check for `nextLink` for pagination -- follow it until absent.
- **delegatedProviders/offers (single):** Returns a single offer object with `id`, `name`, `type`, and `properties`. A 404 means the offer does not exist under that provider.
- **offers (global list):** Same paginated array pattern as the provider-scoped list. May return a superset -- filter client-side if you need provider-specific results.

## Anomaly Flags

- **404 on a previously valid offer:** The offer may have been removed or the delegated provider ID is incorrect -- surface this to the user immediately.
- **Empty `value` array:** A delegated provider with zero offers is unusual and worth flagging; the provider may be misconfigured or decommissioned.
- **Throttling (429 or Retry-After header):** Azure ARM endpoints enforce rate limits. Surface the retry delay and pause before continuing.
- **API version mismatch warnings:** This spec uses `2015-11-01`. If responses include deprecation headers or redirect to a newer API version, flag it.
- **Authentication failures (401/403):** OAuth2 token may have expired or lack the required scope for subscription-level reads. Prompt the user to re-authenticate.
- **Unexpected `nextLink` loops:** If pagination returns the same `nextLink` repeatedly, break the loop and alert the user to a possible API issue.

## Playbook

### 1. List All Offers for a Delegated Provider

1. Identify the `delegatedProviderId` (from your Azure Stack configuration or admin portal).
2. Call `GET /delegatedProviders/{delegatedProviderId}/offers`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it with another GET until no `nextLink` is returned.
5. Present the consolidated list of offers with their names and properties.

### 2. Inspect a Specific Offer

1. Obtain the `delegatedProviderId` and `offerName`.
2. Call `GET /delegatedProviders/{delegatedProviderId}/offers/{offerName}`.
3. If 200, extract the `properties` block for plan details, quotas, and state.
4. If 404, inform the user the offer does not exist under that provider and suggest listing all offers to find the correct name.

### 3. Discover All Available Offers Globally

1. Call `GET /offers` to retrieve the full catalog.
2. Follow any `nextLink` pagination.
3. Group results by provider or category if the response includes those fields.
4. Use this as a starting point to identify which delegated provider hosts a desired offer.

### 4. Verify Offer Availability Across Providers

1. Collect a list of delegated provider IDs.
2. For each provider, call `GET /delegatedProviders/{delegatedProviderId}/offers`.
3. Search each response's `value` array for the target offer name.
4. Report which providers carry the offer and flag any that return errors or empty results.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
