---
name: identity-api
description: "Identity API skill. Use when working with Identity for user. Covers 1 endpoint."
version: 1.0.0
generator: lapsh
---

# Identity API
API version: v2.0.0

## Auth
OAuth2

## Base URL
https://apiz.ebay.com/commerce/identity/v1

## Setup
1. Configure auth: OAuth2
2. GET /user/ -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user/ | This method retrieves the account profile information for an authenticated user, which requires a <a href="/api-docs/static/oauth-authorization-code-grant.html">User access token</a>. What is returned is controlled by the <a href="#scopes">scopes</a>. <p>For a business account you use the default scope <code>commerce.identity.readonly</code>, which returns all the fields in the <a href="/api-docs/commerce/identity/resources/user/methods/getUser#response.businessAccount">businessAccount</a> container. These are returned  because this is all public information.</p>  <p> For an individual account, the fields returned in the <a href="/api-docs/commerce/identity/resources/user/methods/getUser#response.individualAccount">individualAccount</a> container are based on the scope you use. Using the default scope, only public information, such as eBay user ID, are returned. For details about what each scope returns, see the <a href="/api-docs/commerce/identity/overview.html">Identity API Overview</a>.</p> <p>In the Sandbox, this API returns mock data. <b>Note: </b> You must use the correct scope or scopes for the data you want returned.</p> |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all user?" -> GET /user/
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
