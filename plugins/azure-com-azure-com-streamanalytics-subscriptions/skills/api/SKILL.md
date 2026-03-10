---
name: streamanalyticsmanagementclient
description: "StreamAnalyticsManagementClient API skill. Use when working with StreamAnalyticsManagementClient for subscriptions. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# StreamAnalyticsManagementClient
API version: 2016-03-01

## Auth
OAuth2

## Base URL
https://management.azure.com

## Setup
1. Configure auth: OAuth2
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas | Retrieves the subscription's current quota information in a particular region. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all quotas?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.StreamAnalytics/locations/{location}/quotas
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
