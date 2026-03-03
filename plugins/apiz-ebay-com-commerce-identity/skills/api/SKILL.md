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
https://apiz.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /user/ -- verify access

## Endpoints

1 endpoints across 1 groups. See references/api-spec.lap for full details.

### user
| Method | Path | Description |
|--------|------|-------------|
| GET | /user/ | This method retrieves the account profile information for an authenticated user, which requires a <a href="/api-docs/static/oauth-authorization-code-grant.html">User access token</a>. What is returned is controlled by the <a href="#scopes">scopes</a>. <p>For a business account you use the default scope <code>commerce.identity.readonly</code>, which returns all the fields in the <a href="/api-docs/commerce/identity/resources/user/methods/getUser#response.businessAccount">businessAccount</a> container. These are returned  because this is all public information.</p>  <p> For an individual account, the fields returned in the <a href="/api-docs/commerce/identity/resources/user/methods/getUser#response.individualAccount">individualAccount</a> container are based on the scope you use. Using the default scope, only public information, such as eBay user ID, are returned. For details about what each scope returns, see the <a href="/api-docs/commerce/identity/overview.html">Identity API Overview</a>.</p> <p>In the Sandbox, this API returns mock data. <b>Note: </b> You must use the correct scope or scopes for the data you want returned.</p> |

## Enhanced Skill Content
## Question Mapping

- "Who am I on eBay?" -> GET /user/
- "What is my eBay username?" -> GET /user/
- "Am I a business or individual account?" -> GET /user/
- "What email is on my eBay account?" -> GET /user/
- "What is my eBay user ID?" -> GET /user/
- "What marketplace am I registered on?" -> GET /user/
- "Is my eBay account active?" -> GET /user/
- "What is my business address on eBay?" -> GET /user/
- "What phone number is on my eBay account?" -> GET /user/
- "What is my eBay business name (DBA)?" -> GET /user/
- "Show my eBay registration details" -> GET /user/
- "Does my eBay account have a website listed?" -> GET /user/
- "What is the primary contact for my eBay business?" -> GET /user/

## Response Tips

- **User endpoint**: Response contains either `businessAccount` or `individualAccount` (not both) depending on `accountType`. Always check `accountType` first to know which nested object to read. Phone numbers split across `countryCode`, `number`, and `phoneType` fields -- combine them for display. Address fields may be partially populated; `country` is the most reliable.

## Anomaly Flags

- **Account status not active**: Surface immediately if `status` is anything other than the expected active state -- the user may be suspended or restricted.
- **Missing contact info**: Flag if `primaryPhone` or email fields are empty, as this can block seller actions.
- **404 response**: Indicates the OAuth token may be valid but not linked to a recognizable eBay identity -- suggest re-authenticating.
- **500 response**: eBay platform issue -- recommend retry after a short delay; do not retry more than twice.
- **Empty businessAccount and individualAccount**: If both nested objects are absent or null, the account may be in an incomplete registration state.

## Playbook

### 1. Verify Account Identity

1. Call `GET /user/` with a valid OAuth2 token.
2. Read `username` and `userId` from the response.
3. Check `status` to confirm the account is active.
4. Display `accountType` to clarify business vs individual.

### 2. Retrieve Business Contact Details

1. Call `GET /user/`.
2. Confirm `accountType` is `"BUSINESS"`.
3. Read `businessAccount.primaryContact` for first/last name.
4. Read `businessAccount.email` for the business email.
5. Combine `businessAccount.primaryPhone.countryCode` and `businessAccount.primaryPhone.number` for the full phone number.
6. Read `businessAccount.address` for the registered business address.

### 3. Check Registration Marketplace

1. Call `GET /user/`.
2. Read `registrationMarketplaceId` (e.g., `EBAY_US`, `EBAY_GB`).
3. Use this value to determine which eBay site the account was created on and which regional policies apply.

### 4. Audit Account Completeness

1. Call `GET /user/`.
2. Check that `status` is active.
3. Verify email is present in the relevant account object (`businessAccount.email` or `individualAccount.email`).
4. Verify `primaryPhone` is populated with both `countryCode` and `number`.
5. For business accounts, confirm `address` has at minimum `addressLine1`, `city`, `country`, and `postalCode`.
6. Flag any missing fields to the user as potential blockers for selling or verification.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
