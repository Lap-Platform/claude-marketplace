---
name: commerce-api
description: "Commerce API skill. Use when working with Commerce for companies. Covers 21 endpoints."
version: 1.0.0
generator: lapsh
---

# Commerce API
API version: 3.0.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.codat.io

## Setup
1. Set your API key in the appropriate header
2. GET /companies/{companyId}/connections/{connectionId}/data/commerce-customers -- verify access

## Endpoints

21 endpoints across 1 groups. See references/api-spec.lap for full details.

### companies
| Method | Path | Description |
|--------|------|-------------|
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-customers | List customers |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-customers/{customerId} | Get customer |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-disputes | List disputes |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-disputes/{disputeId} | Get dispute |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-info | Get company info |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-locations | List locations |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-locations/{locationId} | Get location |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-orders | List orders |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-orders/{orderId} | Get order |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-payments | List payments |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-payments/{paymentId} | Get payment |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-paymentMethods | List payment methods |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-paymentMethods/{paymentMethodId} | Get payment method |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-products | List products |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-products/{productId} | Get product |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-transactions | List transactions |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-transactions/{transactionId} | Get transaction |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-productCategories | List product categories |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-productCategories/{productId} | Get product category |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-taxComponents | List tax components |
| GET | /companies/{companyId}/connections/{connectionId}/data/commerce-taxComponents/{taxId} | Get tax component |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "Search commerce-customers?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-customers
- "Get commerce-customer details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-customers/{customerId}
- "Search commerce-disputes?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-disputes
- "Get commerce-dispute details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-disputes/{disputeId}
- "List all commerce-info?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-info
- "List all commerce-locations?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-locations
- "Get commerce-location details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-locations/{locationId}
- "Search commerce-orders?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-orders
- "Get commerce-order details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-orders/{orderId}
- "Search commerce-payments?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-payments
- "Get commerce-payment details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-payments/{paymentId}
- "Search commerce-paymentMethods?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-paymentMethods
- "Get commerce-paymentMethod details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-paymentMethods/{paymentMethodId}
- "Search commerce-products?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-products
- "Get commerce-product details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-products/{productId}
- "Search commerce-transactions?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-transactions
- "Get commerce-transaction details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-transactions/{transactionId}
- "Search commerce-productCategories?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-productCategories
- "Get commerce-productCategory details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-productCategories/{productId}
- "Search commerce-taxComponents?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-taxComponents
- "Get commerce-taxComponent details?" -> GET /companies/{companyId}/connections/{connectionId}/data/commerce-taxComponents/{taxId}
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
