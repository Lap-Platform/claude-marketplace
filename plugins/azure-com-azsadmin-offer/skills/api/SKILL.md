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

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all offers?" -> GET /delegatedProviders/{delegatedProviderId}/offers
- "Get offer details?" -> GET /delegatedProviders/{delegatedProviderId}/offers/{offerName}
- "List all offers?" -> GET /offers
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
