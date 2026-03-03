---
name: mixed-reality
description: "Mixed Reality API skill. Use when working with Mixed Reality for providers, subscriptions. Covers 2 endpoints."
version: 1.0.0
generator: lapsh
---

# Mixed Reality
API version: 2019-12-02-preview

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /providers/Microsoft.MixedReality/operations -- verify access
3. POST /subscriptions/{subscriptionId}/providers/Microsoft.MixedReality/locations/{location}/checkNameAvailability -- create first checkNameAvailability

## Endpoints

2 endpoints across 2 groups. See references/api-spec.lap for full details.

### providers
| Method | Path | Description |
|--------|------|-------------|
| GET | /providers/Microsoft.MixedReality/operations | Exposing Available Operations |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| POST | /subscriptions/{subscriptionId}/providers/Microsoft.MixedReality/locations/{location}/checkNameAvailability | Check Name Availability for local uniqueness |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all operations?" -> GET /providers/Microsoft.MixedReality/operations
- "Create a checkNameAvailability?" -> POST /subscriptions/{subscriptionId}/providers/Microsoft.MixedReality/locations/{location}/checkNameAvailability
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
