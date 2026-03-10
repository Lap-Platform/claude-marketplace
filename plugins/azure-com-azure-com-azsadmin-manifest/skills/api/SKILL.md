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
2. GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests -- verify access

## Endpoints

2 endpoints across 1 groups. See references/api-spec.lap for full details.

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests | Get a list of all manifests. |
| GET | /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName} | Get the specified manifest. |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all manifests?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests
- "Get manifest details?" -> GET /subscriptions/{subscriptionId}/providers/Microsoft.Subscriptions.Admin/manifests/{manifestName}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
