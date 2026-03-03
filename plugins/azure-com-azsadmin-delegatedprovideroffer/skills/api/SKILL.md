---
name: subscriptionsmanagementclient
description: "SubscriptionsManagementClient API skill. Use when working with SubscriptionsManagementClient for subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# SubscriptionsManagementClient
API version: 2015-11-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers | Get the list of delegated provider offers. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers/{offer} | Get the specified delegated provider offer. |

## Enhanced Skill Content
## Question Mapping

- "What offers are available from a delegated provider?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers
- "List all offers for delegated provider X" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers
- "Get details of a specific delegated provider offer" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers/{offer}
- "Does delegated provider X have offer Y?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers/{offer}
- "What plans or services does a delegated provider expose?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers
- "Show me the properties of offer Z under delegated provider X" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers/{offer}
- "How many offers does a delegated provider have?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers
- "Is a specific offer still active for a delegated provider?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers/{offer}
- "What subscription-level offers exist for provider subscription ABC?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers
- "Retrieve the offer named 'default' from delegated provider X" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers/{offer}
- "Compare offers across delegated providers" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers (call per provider)

## Response Tips

- **Offer listings**: Response is a JSON object with a `value` array of offer resources; check `nextLink` for pagination if the provider exposes many offers.
- **Single offer**: Returns the full offer resource object including `properties`, `id`, `name`, and `type`; a 404 means the offer name is wrong or has been removed.
- **All endpoints**: Require `api-version=2015-11-01` as a query parameter; omitting it returns a version-mismatch error.

## Anomaly Flags

- **Deprecated API version**: This API uses version `2015-11-01` -- surface a warning that newer API versions may be available and this version could be retired.
- **Empty offer list**: If the `value` array is empty, flag that the delegated provider may not have published any offers or the provider subscription ID may be incorrect.
- **404 on single offer**: Proactively suggest verifying the offer name against the list endpoint before assuming it was deleted.
- **OAuth2 token expiry**: If a 401 is returned, surface that the bearer token may have expired and needs refresh.
- **Throttling (429)**: Azure ARM APIs enforce rate limits; surface `Retry-After` header value and recommend backing off.

## Playbook

### 1. Discover all offers for a delegated provider

1. Identify your `subscriptionId` and the `delegatedProviderSubscriptionId`.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers?api-version=2015-11-01`.
3. Parse the `value` array from the response.
4. If `nextLink` is present, follow it to retrieve additional pages.

### 2. Inspect a specific offer

1. List all offers (Playbook 1) to confirm the exact offer name.
2. Call `GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/delegatedProviders/{delegatedProviderSubscriptionId}/offers/{offer}?api-version=2015-11-01`.
3. Examine `properties` for offer state, display name, description, and quota details.

### 3. Audit offers across multiple delegated providers

1. Obtain the list of delegated provider subscription IDs (from the parent Subscriptions Admin API or your records).
2. For each provider, call the list offers endpoint.
3. Aggregate results and compare offer names, states, and properties.
4. Flag any provider with zero offers or offers in a non-active state.

### 4. Verify a delegated provider is properly configured

1. Call the list offers endpoint for the delegated provider.
2. Confirm at least one offer exists in the response.
3. For each offer, call the get-single-offer endpoint and verify `properties.state` is active.
4. If no offers or all are inactive, the provider may need reconfiguration in Azure Stack.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
