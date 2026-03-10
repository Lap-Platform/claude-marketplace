---
name: shopify-admin-api
description: "Shopify Admin API skill. Use when working with Shopify Admin for admin, fetch_tracking_numbers, fetch_stock. Covers 1473 endpoints."
version: 1.0.0
generator: lapsh
---

# Shopify Admin API
API version: 2020-10

## Auth
ApiKey token in path

## Base URL
Not specified.

## Setup
1. Set your API key in the appropriate header
2. GET /admin/oauth/access_scopes.json -- verify access
3. POST /admin/api/2020-01/storefront_access_tokens.json -- create first storefront_access_tokens.json

## Endpoints

1473 endpoints across 3 groups. See references/api-spec.lap for full details.

### admin
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin/oauth/access_scopes.json | Retrieves a list of access scopes associated to the access token. |
| POST | /admin/api/2020-01/storefront_access_tokens.json | Creates a new storefront access token |
| GET | /admin/api/2020-01/storefront_access_tokens.json | Retrieves a list of storefront access tokens that have been issued |
| DELETE | /admin/api/2020-01/storefront_access_tokens/{storefront_access_token_id}.json | Deletes an existing storefront access token |
| POST | /admin/api/2020-04/storefront_access_tokens.json | Creates a new storefront access token |
| GET | /admin/api/2020-04/storefront_access_tokens.json | Retrieves a list of storefront access tokens that have been issued |
| DELETE | /admin/api/2020-04/storefront_access_tokens/{storefront_access_token_id}.json | Deletes an existing storefront access token |
| POST | /admin/api/2020-07/storefront_access_tokens.json | Creates a new storefront access token |
| GET | /admin/api/2020-07/storefront_access_tokens.json | Retrieves a list of storefront access tokens that have been issued |
| DELETE | /admin/api/2020-07/storefront_access_tokens/{storefront_access_token_id}.json | Deletes an existing storefront access token |
| POST | /admin/api/2020-10/storefront_access_tokens.json | Creates a new storefront access token |
| GET | /admin/api/2020-10/storefront_access_tokens.json | Retrieves a list of storefront access tokens that have been issued |
| DELETE | /admin/api/2020-10/storefront_access_tokens/{storefront_access_token_id}.json | Deletes an existing storefront access token |
| POST | /admin/api/2021-01/storefront_access_tokens.json | Creates a new storefront access token |
| GET | /admin/api/2021-01/storefront_access_tokens.json | Retrieves a list of storefront access tokens that have been issued |
| DELETE | /admin/api/2021-01/storefront_access_tokens/{storefront_access_token_id}.json | Deletes an existing storefront access token |
| POST | /admin/api/unstable/storefront_access_tokens.json | Creates a new storefront access token |
| GET | /admin/api/unstable/storefront_access_tokens.json | Retrieves a list of storefront access tokens that have been issued |
| DELETE | /admin/api/unstable/storefront_access_tokens/{storefront_access_token_id}.json | Deletes an existing storefront access token |
| GET | /admin/api/2020-01/reports.json | Retrieves a list of reports. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/reports.json | Creates a new report |
| GET | /admin/api/2020-01/reports/{report_id}.json | Retrieves a single report created by your app |
| PUT | /admin/api/2020-01/reports/{report_id}.json | Updates a report |
| DELETE | /admin/api/2020-01/reports/{report_id}.json | Deletes a report |
| GET | /admin/api/2020-04/reports.json | Retrieves a list of reports. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/reports.json | Creates a new report |
| GET | /admin/api/2020-04/reports/{report_id}.json | Retrieves a single report created by your app |
| PUT | /admin/api/2020-04/reports/{report_id}.json | Updates a report |
| DELETE | /admin/api/2020-04/reports/{report_id}.json | Deletes a report |
| GET | /admin/api/2020-07/reports.json | Retrieves a list of reports. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/reports.json | Creates a new report |
| GET | /admin/api/2020-07/reports/{report_id}.json | Retrieves a single report created by your app |
| PUT | /admin/api/2020-07/reports/{report_id}.json | Updates a report |
| DELETE | /admin/api/2020-07/reports/{report_id}.json | Deletes a report |
| GET | /admin/api/2020-10/reports.json | Retrieves a list of reports. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/reports.json | Creates a new report |
| GET | /admin/api/2020-10/reports/{report_id}.json | Retrieves a single report created by your app |
| PUT | /admin/api/2020-10/reports/{report_id}.json | Updates a report |
| DELETE | /admin/api/2020-10/reports/{report_id}.json | Deletes a report |
| GET | /admin/api/2021-01/reports.json | Retrieves a list of reports. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/reports.json | Creates a new report |
| GET | /admin/api/2021-01/reports/{report_id}.json | Retrieves a single report created by your app |
| PUT | /admin/api/2021-01/reports/{report_id}.json | Updates a report |
| DELETE | /admin/api/2021-01/reports/{report_id}.json | Deletes a report |
| GET | /admin/api/unstable/reports.json | Retrieves a list of reports. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/reports.json | Creates a new report |
| GET | /admin/api/unstable/reports/{report_id}.json | Retrieves a single report created by your app |
| PUT | /admin/api/unstable/reports/{report_id}.json | Updates a report |
| DELETE | /admin/api/unstable/reports/{report_id}.json | Deletes a report |
| POST | /admin/api/2020-01/application_charges.json | Creates an application charge |
| GET | /admin/api/2020-01/application_charges.json | Retrieves a list of application charges |
| GET | /admin/api/2020-01/application_charges/{application_charge_id}.json | Retrieves an application charge |
| POST | /admin/api/2020-01/application_charges/{application_charge_id}/activate.json | Caution |
| POST | /admin/api/2020-04/application_charges.json | Creates an application charge |
| GET | /admin/api/2020-04/application_charges.json | Retrieves a list of application charges |
| GET | /admin/api/2020-04/application_charges/{application_charge_id}.json | Retrieves an application charge |
| POST | /admin/api/2020-04/application_charges/{application_charge_id}/activate.json | Caution |
| POST | /admin/api/2020-07/application_charges.json | Creates an application charge |
| GET | /admin/api/2020-07/application_charges.json | Retrieves a list of application charges |
| GET | /admin/api/2020-07/application_charges/{application_charge_id}.json | Retrieves an application charge |
| POST | /admin/api/2020-07/application_charges/{application_charge_id}/activate.json | Caution |
| POST | /admin/api/2020-10/application_charges.json | Creates an application charge |
| GET | /admin/api/2020-10/application_charges.json | Retrieves a list of application charges |
| GET | /admin/api/2020-10/application_charges/{application_charge_id}.json | Retrieves an application charge |
| POST | /admin/api/2020-10/application_charges/{application_charge_id}/activate.json | Caution |
| POST | /admin/api/2021-01/application_charges.json | Creates an application charge |
| GET | /admin/api/2021-01/application_charges.json | Retrieves a list of application charges |
| GET | /admin/api/2021-01/application_charges/{application_charge_id}.json | Retrieves an application charge |
| POST | /admin/api/unstable/application_charges.json | Creates an application charge |
| GET | /admin/api/unstable/application_charges.json | Retrieves a list of application charges |
| GET | /admin/api/unstable/application_charges/{application_charge_id}.json | Retrieves an application charge |
| POST | /admin/api/2020-01/application_credits.json | Creates an application credit |
| GET | /admin/api/2020-01/application_credits.json | Retrieves all application credits |
| GET | /admin/api/2020-01/application_credits/{application_credit_id}.json | Retrieves a single application credit |
| POST | /admin/api/2020-04/application_credits.json | Creates an application credit |
| GET | /admin/api/2020-04/application_credits.json | Retrieves all application credits |
| GET | /admin/api/2020-04/application_credits/{application_credit_id}.json | Retrieves a single application credit |
| POST | /admin/api/2020-07/application_credits.json | Creates an application credit |
| GET | /admin/api/2020-07/application_credits.json | Retrieves all application credits |
| GET | /admin/api/2020-07/application_credits/{application_credit_id}.json | Retrieves a single application credit |
| POST | /admin/api/2020-10/application_credits.json | Creates an application credit |
| GET | /admin/api/2020-10/application_credits.json | Retrieves all application credits |
| GET | /admin/api/2020-10/application_credits/{application_credit_id}.json | Retrieves a single application credit |
| POST | /admin/api/2021-01/application_credits.json | Creates an application credit |
| GET | /admin/api/2021-01/application_credits.json | Retrieves all application credits |
| GET | /admin/api/2021-01/application_credits/{application_credit_id}.json | Retrieves a single application credit |
| POST | /admin/api/unstable/application_credits.json | Creates an application credit |
| GET | /admin/api/unstable/application_credits.json | Retrieves all application credits |
| GET | /admin/api/unstable/application_credits/{application_credit_id}.json | Retrieves a single application credit |
| POST | /admin/api/2020-01/recurring_application_charges.json | Creates a recurring application charge |
| GET | /admin/api/2020-01/recurring_application_charges.json | Retrieves a list of recurring application charges |
| GET | /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}.json | Retrieves a single charge |
| DELETE | /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}.json | Cancels a recurring application charge |
| POST | /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/activate.json | Caution |
| PUT | /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/customize.json | Updates the capped amount of an active recurring application charge |
| POST | /admin/api/2020-04/recurring_application_charges.json | Creates a recurring application charge |
| GET | /admin/api/2020-04/recurring_application_charges.json | Retrieves a list of recurring application charges |
| GET | /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}.json | Retrieves a single charge |
| DELETE | /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}.json | Cancels a recurring application charge |
| POST | /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/activate.json | Caution |
| PUT | /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/customize.json | Updates the capped amount of an active recurring application charge |
| POST | /admin/api/2020-07/recurring_application_charges.json | Creates a recurring application charge |
| GET | /admin/api/2020-07/recurring_application_charges.json | Retrieves a list of recurring application charges |
| GET | /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}.json | Retrieves a single charge |
| DELETE | /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}.json | Cancels a recurring application charge |
| POST | /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/activate.json | Caution |
| PUT | /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/customize.json | Updates the capped amount of an active recurring application charge |
| POST | /admin/api/2020-10/recurring_application_charges.json | Creates a recurring application charge |
| GET | /admin/api/2020-10/recurring_application_charges.json | Retrieves a list of recurring application charges |
| GET | /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}.json | Retrieves a single charge |
| DELETE | /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}.json | Cancels a recurring application charge |
| POST | /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/activate.json | Caution |
| PUT | /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/customize.json | Updates the capped amount of an active recurring application charge |
| POST | /admin/api/2021-01/recurring_application_charges.json | Creates a recurring application charge |
| GET | /admin/api/2021-01/recurring_application_charges.json | Retrieves a list of recurring application charges |
| GET | /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}.json | Retrieves a single charge |
| DELETE | /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}.json | Cancels a recurring application charge |
| PUT | /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}/customize.json | Updates the capped amount of an active recurring application charge |
| POST | /admin/api/unstable/recurring_application_charges.json | Creates a recurring application charge |
| GET | /admin/api/unstable/recurring_application_charges.json | Retrieves a list of recurring application charges |
| GET | /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}.json | Retrieves a single charge |
| DELETE | /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}.json | Cancels a recurring application charge |
| PUT | /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}/customize.json | Updates the capped amount of an active recurring application charge |
| POST | /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Creates a usage charge |
| GET | /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Retrieves a list of usage charges |
| GET | /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json | Retrieves a single charge |
| POST | /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Creates a usage charge |
| GET | /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Retrieves a list of usage charges |
| GET | /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json | Retrieves a single charge |
| POST | /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Creates a usage charge |
| GET | /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Retrieves a list of usage charges |
| GET | /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json | Retrieves a single charge |
| POST | /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Creates a usage charge |
| GET | /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Retrieves a list of usage charges |
| GET | /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json | Retrieves a single charge |
| POST | /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Creates a usage charge |
| GET | /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Retrieves a list of usage charges |
| GET | /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json | Retrieves a single charge |
| POST | /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Creates a usage charge |
| GET | /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json | Retrieves a list of usage charges |
| GET | /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json | Retrieves a single charge |
| GET | /admin/api/2020-01/customers.json | Retrieves a list of customers. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/customers.json | Creates a customer. |
| GET | /admin/api/2020-01/customers/search.json | Searches for customers that match a supplied query. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/customers/{customer_id}.json | Retrieves a single customer. |
| PUT | /admin/api/2020-01/customers/{customer_id}.json | Updates a customer. |
| DELETE | /admin/api/2020-01/customers/{customer_id}.json | Deletes a customer. A customer can't be deleted if they have existing orders. |
| POST | /admin/api/2020-01/customers/{customer_id}/account_activation_url.json | Generate an account activation URL for a customer whose account is not yet enabled. This is useful when you've imported a large number of customers and want to send them activation emails all at once. Using this approach, you'll need to generate and send the activation emails yourself. |
| POST | /admin/api/2020-01/customers/{customer_id}/send_invite.json | Sends an account invite to a customer. |
| GET | /admin/api/2020-01/customers/count.json | Retrieves a count of all customers. |
| GET | /admin/api/2020-01/customers/{customer_id}/orders.json | Retrieves all orders belonging to a customer. The query string parameters that are available to the  Order resource are also available to this endpoint. |
| GET | /admin/api/2020-04/customers.json | Retrieves a list of customers. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/customers.json | Creates a customer. |
| GET | /admin/api/2020-04/customers/search.json | Searches for customers that match a supplied query. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/customers/{customer_id}.json | Retrieves a single customer. |
| PUT | /admin/api/2020-04/customers/{customer_id}.json | Updates a customer. |
| DELETE | /admin/api/2020-04/customers/{customer_id}.json | Deletes a customer. A customer can't be deleted if they have existing orders. |
| POST | /admin/api/2020-04/customers/{customer_id}/account_activation_url.json | Generate an account activation URL for a customer whose account is not yet enabled. This is useful when you've imported a large number of customers and want to send them activation emails all at once. Using this approach, you'll need to generate and send the activation emails yourself. |
| POST | /admin/api/2020-04/customers/{customer_id}/send_invite.json | Sends an account invite to a customer. |
| GET | /admin/api/2020-04/customers/count.json | Retrieves a count of all customers. |
| GET | /admin/api/2020-04/customers/{customer_id}/orders.json | Retrieves all orders belonging to a customer. The query string parameters that are available to the  Order resource are also available to this endpoint. |
| GET | /admin/api/2020-07/customers.json | Retrieves a list of customers. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/customers.json | Creates a customer. |
| GET | /admin/api/2020-07/customers/search.json | Searches for customers that match a supplied query. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/customers/{customer_id}.json | Retrieves a single customer. |
| PUT | /admin/api/2020-07/customers/{customer_id}.json | Updates a customer. |
| DELETE | /admin/api/2020-07/customers/{customer_id}.json | Deletes a customer. A customer can't be deleted if they have existing orders. |
| POST | /admin/api/2020-07/customers/{customer_id}/account_activation_url.json | Generate an account activation URL for a customer whose account is not yet enabled. This is useful when you've imported a large number of customers and want to send them activation emails all at once. Using this approach, you'll need to generate and send the activation emails yourself. |
| POST | /admin/api/2020-07/customers/{customer_id}/send_invite.json | Sends an account invite to a customer. |
| GET | /admin/api/2020-07/customers/count.json | Retrieves a count of all customers. |
| GET | /admin/api/2020-07/customers/{customer_id}/orders.json | Retrieves all orders belonging to a customer. The query string parameters that are available to the  Order resource are also available to this endpoint. |
| GET | /admin/api/2020-10/customers.json | Retrieves a list of customers. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/customers.json | Creates a customer. |
| GET | /admin/api/2020-10/customers/search.json | Searches for customers that match a supplied query. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/customers/{customer_id}.json | Retrieves a single customer. |
| PUT | /admin/api/2020-10/customers/{customer_id}.json | Updates a customer. |
| DELETE | /admin/api/2020-10/customers/{customer_id}.json | Deletes a customer. A customer can't be deleted if they have existing orders. |
| POST | /admin/api/2020-10/customers/{customer_id}/account_activation_url.json | Generate an account activation URL for a customer whose account is not yet enabled. This is useful when you've imported a large number of customers and want to send them activation emails all at once. Using this approach, you'll need to generate and send the activation emails yourself. |
| POST | /admin/api/2020-10/customers/{customer_id}/send_invite.json | Sends an account invite to a customer. |
| GET | /admin/api/2020-10/customers/count.json | Retrieves a count of all customers. |
| GET | /admin/api/2020-10/customers/{customer_id}/orders.json | Retrieves all orders belonging to a customer. The query string parameters that are available to the  Order resource are also available to this endpoint. |
| GET | /admin/api/2021-01/customers.json | Retrieves a list of customers. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/customers.json | Creates a customer. |
| GET | /admin/api/2021-01/customers/search.json | Searches for customers that match a supplied query. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/customers/{customer_id}.json | Retrieves a single customer. |
| PUT | /admin/api/2021-01/customers/{customer_id}.json | Updates a customer. |
| DELETE | /admin/api/2021-01/customers/{customer_id}.json | Deletes a customer. A customer can't be deleted if they have existing orders. |
| POST | /admin/api/2021-01/customers/{customer_id}/account_activation_url.json | Generate an account activation URL for a customer whose account is not yet enabled. This is useful when you've imported a large number of customers and want to send them activation emails all at once. Using this approach, you'll need to generate and send the activation emails yourself. |
| POST | /admin/api/2021-01/customers/{customer_id}/send_invite.json | Sends an account invite to a customer. |
| GET | /admin/api/2021-01/customers/count.json | Retrieves a count of all customers. |
| GET | /admin/api/2021-01/customers/{customer_id}/orders.json | Retrieves all orders belonging to a customer. The query string parameters that are available to the  Order resource are also available to this endpoint. |
| GET | /admin/api/unstable/customers.json | Retrieves a list of customers. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/customers.json | Creates a customer. |
| GET | /admin/api/unstable/customers/search.json | Searches for customers that match a supplied query. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/customers/{customer_id}.json | Retrieves a single customer. |
| PUT | /admin/api/unstable/customers/{customer_id}.json | Updates a customer. |
| DELETE | /admin/api/unstable/customers/{customer_id}.json | Deletes a customer. A customer can't be deleted if they have existing orders. |
| POST | /admin/api/unstable/customers/{customer_id}/account_activation_url.json | Generate an account activation URL for a customer whose account is not yet enabled. This is useful when you've imported a large number of customers and want to send them activation emails all at once. Using this approach, you'll need to generate and send the activation emails yourself. |
| POST | /admin/api/unstable/customers/{customer_id}/send_invite.json | Sends an account invite to a customer. |
| GET | /admin/api/unstable/customers/count.json | Retrieves a count of all customers. |
| GET | /admin/api/unstable/customers/{customer_id}/orders.json | Retrieves all orders belonging to a customer. The query string parameters that are available to the  Order resource are also available to this endpoint. |
| GET | /admin/api/2020-01/customers/{customer_id}/addresses.json | Retrieves a list of addresses for a customer. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/customers/{customer_id}/addresses.json | Creates a new address for a customer. |
| GET | /admin/api/2020-01/customers/{customer_id}/addresses/{address_id}.json | Retrieves details a single customer address. |
| PUT | /admin/api/2020-01/customers/{customer_id}/addresses/{address_id}.json | Updates an existing customer address. |
| DELETE | /admin/api/2020-01/customers/{customer_id}/addresses/{address_id}.json | Removes an address from a customer’s address list. |
| PUT | /admin/api/2020-01/customers/{customer_id}/addresses/set.json | Performs bulk operations for multiple customer addresses. |
| PUT | /admin/api/2020-01/customers/{customer_id}/addresses/{address_id}/default.json | Sets the default address for a customer. |
| GET | /admin/api/2020-04/customers/{customer_id}/addresses.json | Retrieves a list of addresses for a customer. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/customers/{customer_id}/addresses.json | Creates a new address for a customer. |
| GET | /admin/api/2020-04/customers/{customer_id}/addresses/{address_id}.json | Retrieves details a single customer address. |
| PUT | /admin/api/2020-04/customers/{customer_id}/addresses/{address_id}.json | Updates an existing customer address. |
| DELETE | /admin/api/2020-04/customers/{customer_id}/addresses/{address_id}.json | Removes an address from a customer’s address list. |
| PUT | /admin/api/2020-04/customers/{customer_id}/addresses/set.json | Performs bulk operations for multiple customer addresses. |
| PUT | /admin/api/2020-04/customers/{customer_id}/addresses/{address_id}/default.json | Sets the default address for a customer. |
| GET | /admin/api/2020-07/customers/{customer_id}/addresses.json | Retrieves a list of addresses for a customer. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/customers/{customer_id}/addresses.json | Creates a new address for a customer. |
| GET | /admin/api/2020-07/customers/{customer_id}/addresses/{address_id}.json | Retrieves details a single customer address. |
| PUT | /admin/api/2020-07/customers/{customer_id}/addresses/{address_id}.json | Updates an existing customer address. |
| DELETE | /admin/api/2020-07/customers/{customer_id}/addresses/{address_id}.json | Removes an address from a customer’s address list. |
| PUT | /admin/api/2020-07/customers/{customer_id}/addresses/set.json | Performs bulk operations for multiple customer addresses. |
| PUT | /admin/api/2020-07/customers/{customer_id}/addresses/{address_id}/default.json | Sets the default address for a customer. |
| GET | /admin/api/2020-10/customers/{customer_id}/addresses.json | Retrieves a list of addresses for a customer. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/customers/{customer_id}/addresses.json | Creates a new address for a customer. |
| GET | /admin/api/2020-10/customers/{customer_id}/addresses/{address_id}.json | Retrieves details a single customer address. |
| PUT | /admin/api/2020-10/customers/{customer_id}/addresses/{address_id}.json | Updates an existing customer address. |
| DELETE | /admin/api/2020-10/customers/{customer_id}/addresses/{address_id}.json | Removes an address from a customer’s address list. |
| PUT | /admin/api/2020-10/customers/{customer_id}/addresses/set.json | Performs bulk operations for multiple customer addresses. |
| PUT | /admin/api/2020-10/customers/{customer_id}/addresses/{address_id}/default.json | Sets the default address for a customer. |
| GET | /admin/api/2021-01/customers/{customer_id}/addresses.json | Retrieves a list of addresses for a customer. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/customers/{customer_id}/addresses.json | Creates a new address for a customer. |
| GET | /admin/api/2021-01/customers/{customer_id}/addresses/{address_id}.json | Retrieves details a single customer address. |
| PUT | /admin/api/2021-01/customers/{customer_id}/addresses/{address_id}.json | Updates an existing customer address. |
| DELETE | /admin/api/2021-01/customers/{customer_id}/addresses/{address_id}.json | Removes an address from a customer’s address list. |
| PUT | /admin/api/2021-01/customers/{customer_id}/addresses/set.json | Performs bulk operations for multiple customer addresses. |
| PUT | /admin/api/2021-01/customers/{customer_id}/addresses/{address_id}/default.json | Sets the default address for a customer. |
| GET | /admin/api/unstable/customers/{customer_id}/addresses.json | Retrieves a list of addresses for a customer. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/customers/{customer_id}/addresses.json | Creates a new address for a customer. |
| GET | /admin/api/unstable/customers/{customer_id}/addresses/{address_id}.json | Retrieves details a single customer address. |
| PUT | /admin/api/unstable/customers/{customer_id}/addresses/{address_id}.json | Updates an existing customer address. |
| DELETE | /admin/api/unstable/customers/{customer_id}/addresses/{address_id}.json | Removes an address from a customer’s address list. |
| PUT | /admin/api/unstable/customers/{customer_id}/addresses/set.json | Performs bulk operations for multiple customer addresses. |
| PUT | /admin/api/unstable/customers/{customer_id}/addresses/{address_id}/default.json | Sets the default address for a customer. |
| GET | /admin/api/2020-01/customer_saved_searches.json | Retrieves a list of customer saved searches. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/customer_saved_searches.json | Creates a customer saved search. |
| GET | /admin/api/2020-01/customer_saved_searches/count.json | Retrieves a count of all customer saved searches. |
| GET | /admin/api/2020-01/customer_saved_searches/{customer_saved_search_id}.json | Retrieves a single customer saved search. |
| PUT | /admin/api/2020-01/customer_saved_searches/{customer_saved_search_id}.json | Updates a customer saved search. |
| DELETE | /admin/api/2020-01/customer_saved_searches/{customer_saved_search_id}.json | Deletes a customer saved search. |
| GET | /admin/api/2020-01/customer_saved_searches/{customer_saved_search_id}/customers.json | Retrieves all customers returned by a customer saved search. |
| GET | /admin/api/2020-04/customer_saved_searches.json | Retrieves a list of customer saved searches. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/customer_saved_searches.json | Creates a customer saved search. |
| GET | /admin/api/2020-04/customer_saved_searches/count.json | Retrieves a count of all customer saved searches. |
| GET | /admin/api/2020-04/customer_saved_searches/{customer_saved_search_id}.json | Retrieves a single customer saved search. |
| PUT | /admin/api/2020-04/customer_saved_searches/{customer_saved_search_id}.json | Updates a customer saved search. |
| DELETE | /admin/api/2020-04/customer_saved_searches/{customer_saved_search_id}.json | Deletes a customer saved search. |
| GET | /admin/api/2020-04/customer_saved_searches/{customer_saved_search_id}/customers.json | Retrieves all customers returned by a customer saved search. |
| GET | /admin/api/2020-07/customer_saved_searches.json | Retrieves a list of customer saved searches. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/customer_saved_searches.json | Creates a customer saved search. |
| GET | /admin/api/2020-07/customer_saved_searches/count.json | Retrieves a count of all customer saved searches. |
| GET | /admin/api/2020-07/customer_saved_searches/{customer_saved_search_id}.json | Retrieves a single customer saved search. |
| PUT | /admin/api/2020-07/customer_saved_searches/{customer_saved_search_id}.json | Updates a customer saved search. |
| DELETE | /admin/api/2020-07/customer_saved_searches/{customer_saved_search_id}.json | Deletes a customer saved search. |
| GET | /admin/api/2020-07/customer_saved_searches/{customer_saved_search_id}/customers.json | Retrieves all customers returned by a customer saved search. |
| GET | /admin/api/2020-10/customer_saved_searches.json | Retrieves a list of customer saved searches. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/customer_saved_searches.json | Creates a customer saved search. |
| GET | /admin/api/2020-10/customer_saved_searches/count.json | Retrieves a count of all customer saved searches. |
| GET | /admin/api/2020-10/customer_saved_searches/{customer_saved_search_id}.json | Retrieves a single customer saved search. |
| PUT | /admin/api/2020-10/customer_saved_searches/{customer_saved_search_id}.json | Updates a customer saved search. |
| DELETE | /admin/api/2020-10/customer_saved_searches/{customer_saved_search_id}.json | Deletes a customer saved search. |
| GET | /admin/api/2020-10/customer_saved_searches/{customer_saved_search_id}/customers.json | Retrieves all customers returned by a customer saved search. |
| GET | /admin/api/2021-01/customer_saved_searches.json | Retrieves a list of customer saved searches. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/customer_saved_searches.json | Creates a customer saved search. |
| GET | /admin/api/2021-01/customer_saved_searches/count.json | Retrieves a count of all customer saved searches. |
| GET | /admin/api/2021-01/customer_saved_searches/{customer_saved_search_id}.json | Retrieves a single customer saved search. |
| PUT | /admin/api/2021-01/customer_saved_searches/{customer_saved_search_id}.json | Updates a customer saved search. |
| DELETE | /admin/api/2021-01/customer_saved_searches/{customer_saved_search_id}.json | Deletes a customer saved search. |
| GET | /admin/api/2021-01/customer_saved_searches/{customer_saved_search_id}/customers.json | Retrieves all customers returned by a customer saved search. |
| GET | /admin/api/unstable/customer_saved_searches.json | Retrieves a list of customer saved searches. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/customer_saved_searches.json | Creates a customer saved search. |
| GET | /admin/api/unstable/customer_saved_searches/count.json | Retrieves a count of all customer saved searches. |
| GET | /admin/api/unstable/customer_saved_searches/{customer_saved_search_id}.json | Retrieves a single customer saved search. |
| PUT | /admin/api/unstable/customer_saved_searches/{customer_saved_search_id}.json | Updates a customer saved search. |
| DELETE | /admin/api/unstable/customer_saved_searches/{customer_saved_search_id}.json | Deletes a customer saved search. |
| GET | /admin/api/unstable/customer_saved_searches/{customer_saved_search_id}/customers.json | Retrieves all customers returned by a customer saved search. |
| GET | /admin/api/2021-01/deprecated_api_calls.json | Retrieves a list of deprecated API calls made by the authenticated private app in the past 30 days. |
| GET | /admin/api/unstable/deprecated_api_calls.json | Retrieves a list of deprecated API calls made by the authenticated private app in the past 30 days. |
| POST | /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes.json | Creates a discount code |
| GET | /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes.json | Retrieve a list of discount codes. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| PUT | /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Updates an existing discount code |
| GET | /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Retrieves a single discount code |
| DELETE | /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Deletes a discount code |
| GET | /admin/api/2020-01/discount_codes/lookup.json | Retrieves the location of a discount code. |
| POST | /admin/api/2020-01/price_rules/{price_rule_id}/batch.json | Creates a discount code creation job. |
| GET | /admin/api/2020-01/price_rules/{price_rule_id}/batch/{batch_id}.json | Retrieves a discount code creation job |
| GET | /admin/api/2020-01/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json | Retrieves a list of discount codes for a discount code creation job. |
| POST | /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes.json | Creates a discount code |
| GET | /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes.json | Retrieve a list of discount codes. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| PUT | /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Updates an existing discount code |
| GET | /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Retrieves a single discount code |
| DELETE | /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Deletes a discount code |
| GET | /admin/api/2020-04/discount_codes/lookup.json | Retrieves the location of a discount code. |
| POST | /admin/api/2020-04/price_rules/{price_rule_id}/batch.json | Creates a discount code creation job. |
| GET | /admin/api/2020-04/price_rules/{price_rule_id}/batch/{batch_id}.json | Retrieves a discount code creation job |
| GET | /admin/api/2020-04/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json | Retrieves a list of discount codes for a discount code creation job. |
| POST | /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes.json | Creates a discount code |
| GET | /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes.json | Retrieve a list of discount codes. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| PUT | /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Updates an existing discount code |
| GET | /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Retrieves a single discount code |
| DELETE | /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Deletes a discount code |
| GET | /admin/api/2020-07/discount_codes/lookup.json | Retrieves the location of a discount code. |
| POST | /admin/api/2020-07/price_rules/{price_rule_id}/batch.json | Creates a discount code creation job. |
| GET | /admin/api/2020-07/price_rules/{price_rule_id}/batch/{batch_id}.json | Retrieves a discount code creation job |
| GET | /admin/api/2020-07/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json | Retrieves a list of discount codes for a discount code creation job. |
| POST | /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes.json | Creates a discount code |
| GET | /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes.json | Retrieve a list of discount codes. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| PUT | /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Updates an existing discount code |
| GET | /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Retrieves a single discount code |
| DELETE | /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Deletes a discount code |
| GET | /admin/api/2020-10/discount_codes/lookup.json | Retrieves the location of a discount code. |
| POST | /admin/api/2020-10/price_rules/{price_rule_id}/batch.json | Creates a discount code creation job. |
| GET | /admin/api/2020-10/price_rules/{price_rule_id}/batch/{batch_id}.json | Retrieves a discount code creation job |
| GET | /admin/api/2020-10/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json | Retrieves a list of discount codes for a discount code creation job. |
| POST | /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes.json | Creates a discount code |
| GET | /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes.json | Retrieve a list of discount codes. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| PUT | /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Updates an existing discount code |
| GET | /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Retrieves a single discount code |
| DELETE | /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Deletes a discount code |
| GET | /admin/api/2021-01/discount_codes/lookup.json | Retrieves the location of a discount code. |
| POST | /admin/api/2021-01/price_rules/{price_rule_id}/batch.json | Creates a discount code creation job. |
| GET | /admin/api/2021-01/price_rules/{price_rule_id}/batch/{batch_id}.json | Retrieves a discount code creation job |
| GET | /admin/api/2021-01/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json | Retrieves a list of discount codes for a discount code creation job. |
| POST | /admin/api/unstable/price_rules/{price_rule_id}/discount_codes.json | Creates a discount code |
| GET | /admin/api/unstable/price_rules/{price_rule_id}/discount_codes.json | Retrieve a list of discount codes. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| PUT | /admin/api/unstable/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Updates an existing discount code |
| GET | /admin/api/unstable/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Retrieves a single discount code |
| DELETE | /admin/api/unstable/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json | Deletes a discount code |
| GET | /admin/api/unstable/discount_codes/lookup.json | Retrieves the location of a discount code. |
| POST | /admin/api/unstable/price_rules/{price_rule_id}/batch.json | Creates a discount code creation job. |
| GET | /admin/api/unstable/price_rules/{price_rule_id}/batch/{batch_id}.json | Retrieves a discount code creation job |
| GET | /admin/api/unstable/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json | Retrieves a list of discount codes for a discount code creation job. |
| GET | /admin/api/2020-01/events.json | Retrieves a list of events. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/events/{event_id}.json | Retrieves a single event by its ID |
| GET | /admin/api/2020-01/events/count.json | Retrieves a count of events |
| GET | /admin/api/2020-04/events.json | Retrieves a list of events. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/events/{event_id}.json | Retrieves a single event by its ID |
| GET | /admin/api/2020-04/events/count.json | Retrieves a count of events |
| GET | /admin/api/2020-07/events.json | Retrieves a list of events. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/events/{event_id}.json | Retrieves a single event by its ID |
| GET | /admin/api/2020-07/events/count.json | Retrieves a count of events |
| GET | /admin/api/2020-10/events.json | Retrieves a list of events. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/events/{event_id}.json | Retrieves a single event by its ID |
| GET | /admin/api/2020-10/events/count.json | Retrieves a count of events |
| GET | /admin/api/2021-01/events.json | Retrieves a list of events. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/events/{event_id}.json | Retrieves a single event by its ID |
| GET | /admin/api/2021-01/events/count.json | Retrieves a count of events |
| GET | /admin/api/unstable/events.json | Retrieves a list of events. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/events/{event_id}.json | Retrieves a single event by its ID |
| GET | /admin/api/unstable/events/count.json | Retrieves a count of events |
| GET | /admin/api/2020-01/webhooks.json | Retrieves a list of webhooks. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/webhooks.json | Create a new webhook subscription by specifying both an address and a topic |
| GET | /admin/api/2020-01/webhooks/count.json | Retrieves a count of existing webhook subscriptions |
| GET | /admin/api/2020-01/webhooks/{webhook_id}.json | Retrieves a single webhook subscription |
| PUT | /admin/api/2020-01/webhooks/{webhook_id}.json | Update a webhook subscription's topic or address URIs |
| DELETE | /admin/api/2020-01/webhooks/{webhook_id}.json | Delete a webhook subscription |
| GET | /admin/api/2020-04/webhooks.json | Retrieves a list of webhooks. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/webhooks.json | Create a new webhook subscription by specifying both an address and a topic |
| GET | /admin/api/2020-04/webhooks/count.json | Retrieves a count of existing webhook subscriptions |
| GET | /admin/api/2020-04/webhooks/{webhook_id}.json | Retrieves a single webhook subscription |
| PUT | /admin/api/2020-04/webhooks/{webhook_id}.json | Update a webhook subscription's topic or address URIs |
| DELETE | /admin/api/2020-04/webhooks/{webhook_id}.json | Delete a webhook subscription |
| GET | /admin/api/2020-07/webhooks.json | Retrieves a list of webhooks. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/webhooks.json | Create a new webhook subscription by specifying both an address and a topic |
| GET | /admin/api/2020-07/webhooks/count.json | Retrieves a count of existing webhook subscriptions |
| GET | /admin/api/2020-07/webhooks/{webhook_id}.json | Retrieves a single webhook subscription |
| PUT | /admin/api/2020-07/webhooks/{webhook_id}.json | Update a webhook subscription's topic or address URIs |
| DELETE | /admin/api/2020-07/webhooks/{webhook_id}.json | Delete a webhook subscription |
| GET | /admin/api/2020-10/webhooks.json | Retrieves a list of webhooks. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/webhooks.json | Create a new webhook subscription by specifying both an address and a topic |
| GET | /admin/api/2020-10/webhooks/count.json | Retrieves a count of existing webhook subscriptions |
| GET | /admin/api/2020-10/webhooks/{webhook_id}.json | Retrieves a single webhook subscription |
| PUT | /admin/api/2020-10/webhooks/{webhook_id}.json | Update a webhook subscription's topic or address URIs |
| DELETE | /admin/api/2020-10/webhooks/{webhook_id}.json | Delete a webhook subscription |
| GET | /admin/api/2021-01/webhooks.json | Retrieves a list of webhooks. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/webhooks.json | Create a new webhook subscription by specifying both an address and a topic |
| GET | /admin/api/2021-01/webhooks/count.json | Retrieves a count of existing webhook subscriptions |
| GET | /admin/api/2021-01/webhooks/{webhook_id}.json | Retrieves a single webhook subscription |
| PUT | /admin/api/2021-01/webhooks/{webhook_id}.json | Update a webhook subscription's topic or address URIs |
| DELETE | /admin/api/2021-01/webhooks/{webhook_id}.json | Delete a webhook subscription |
| GET | /admin/api/unstable/webhooks.json | Retrieves a list of webhooks. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/webhooks.json | Create a new webhook subscription by specifying both an address and a topic |
| GET | /admin/api/unstable/webhooks/count.json | Retrieves a count of existing webhook subscriptions |
| GET | /admin/api/unstable/webhooks/{webhook_id}.json | Retrieves a single webhook subscription |
| PUT | /admin/api/unstable/webhooks/{webhook_id}.json | Update a webhook subscription's topic or address URIs |
| DELETE | /admin/api/unstable/webhooks/{webhook_id}.json | Delete a webhook subscription |
| GET | /admin/api/2020-01/inventory_items.json | Retrieves a list of inventory items. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/inventory_items/{inventory_item_id}.json | Retrieves a single inventory item by ID |
| PUT | /admin/api/2020-01/inventory_items/{inventory_item_id}.json | Updates an existing inventory item |
| GET | /admin/api/2020-04/inventory_items.json | Retrieves a list of inventory items. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/inventory_items/{inventory_item_id}.json | Retrieves a single inventory item by ID |
| PUT | /admin/api/2020-04/inventory_items/{inventory_item_id}.json | Updates an existing inventory item |
| GET | /admin/api/2020-07/inventory_items.json | Retrieves a list of inventory items. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/inventory_items/{inventory_item_id}.json | Retrieves a single inventory item by ID |
| PUT | /admin/api/2020-07/inventory_items/{inventory_item_id}.json | Updates an existing inventory item |
| GET | /admin/api/2020-10/inventory_items.json | Retrieves a list of inventory items. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/inventory_items/{inventory_item_id}.json | Retrieves a single inventory item by ID |
| PUT | /admin/api/2020-10/inventory_items/{inventory_item_id}.json | Updates an existing inventory item |
| GET | /admin/api/2021-01/inventory_items.json | Retrieves a list of inventory items. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/inventory_items/{inventory_item_id}.json | Retrieves a single inventory item by ID |
| PUT | /admin/api/2021-01/inventory_items/{inventory_item_id}.json | Updates an existing inventory item |
| GET | /admin/api/unstable/inventory_items.json | Retrieves a list of inventory items. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/inventory_items/{inventory_item_id}.json | Retrieves a single inventory item by ID |
| PUT | /admin/api/unstable/inventory_items/{inventory_item_id}.json | Updates an existing inventory item |
| GET | /admin/api/2020-01/inventory_levels.json | Retrieves a list of inventory levels. |
| DELETE | /admin/api/2020-01/inventory_levels.json | Deletes an inventory level of an inventory item at a location. |
| POST | /admin/api/2020-01/inventory_levels/adjust.json | Adjusts the inventory level of an inventory item at a single location |
| POST | /admin/api/2020-01/inventory_levels/connect.json | Connects an inventory item to a location by creating an inventory level at that location. |
| POST | /admin/api/2020-01/inventory_levels/set.json | Sets the inventory level for an inventory item at a location. |
| GET | /admin/api/2020-04/inventory_levels.json | Retrieves a list of inventory levels. |
| DELETE | /admin/api/2020-04/inventory_levels.json | Deletes an inventory level of an inventory item at a location. |
| POST | /admin/api/2020-04/inventory_levels/adjust.json | Adjusts the inventory level of an inventory item at a single location |
| POST | /admin/api/2020-04/inventory_levels/connect.json | Connects an inventory item to a location by creating an inventory level at that location. |
| POST | /admin/api/2020-04/inventory_levels/set.json | Sets the inventory level for an inventory item at a location. |
| GET | /admin/api/2020-07/inventory_levels.json | Retrieves a list of inventory levels. |
| DELETE | /admin/api/2020-07/inventory_levels.json | Deletes an inventory level of an inventory item at a location. |
| POST | /admin/api/2020-07/inventory_levels/adjust.json | Adjusts the inventory level of an inventory item at a single location |
| POST | /admin/api/2020-07/inventory_levels/connect.json | Connects an inventory item to a location by creating an inventory level at that location. |
| POST | /admin/api/2020-07/inventory_levels/set.json | Sets the inventory level for an inventory item at a location. |
| GET | /admin/api/2020-10/inventory_levels.json | Retrieves a list of inventory levels. |
| DELETE | /admin/api/2020-10/inventory_levels.json | Deletes an inventory level of an inventory item at a location. |
| POST | /admin/api/2020-10/inventory_levels/adjust.json | Adjusts the inventory level of an inventory item at a single location |
| POST | /admin/api/2020-10/inventory_levels/connect.json | Connects an inventory item to a location by creating an inventory level at that location. |
| POST | /admin/api/2020-10/inventory_levels/set.json | Sets the inventory level for an inventory item at a location. |
| GET | /admin/api/2021-01/inventory_levels.json | Retrieves a list of inventory levels. |
| DELETE | /admin/api/2021-01/inventory_levels.json | Deletes an inventory level of an inventory item at a location. |
| POST | /admin/api/2021-01/inventory_levels/adjust.json | Adjusts the inventory level of an inventory item at a single location |
| POST | /admin/api/2021-01/inventory_levels/connect.json | Connects an inventory item to a location by creating an inventory level at that location. |
| POST | /admin/api/2021-01/inventory_levels/set.json | Sets the inventory level for an inventory item at a location. |
| GET | /admin/api/unstable/inventory_levels.json | Retrieves a list of inventory levels. |
| DELETE | /admin/api/unstable/inventory_levels.json | Deletes an inventory level of an inventory item at a location. |
| POST | /admin/api/unstable/inventory_levels/adjust.json | Adjusts the inventory level of an inventory item at a single location |
| POST | /admin/api/unstable/inventory_levels/connect.json | Connects an inventory item to a location by creating an inventory level at that location. |
| POST | /admin/api/unstable/inventory_levels/set.json | Sets the inventory level for an inventory item at a location. |
| GET | /admin/api/2020-01/locations.json | Retrieves a list of locations |
| GET | /admin/api/2020-01/locations/{location_id}.json | Retrieves a single location by its ID |
| GET | /admin/api/2020-01/locations/count.json | Retrieves a count of locations |
| GET | /admin/api/2020-01/locations/{location_id}/inventory_levels.json | Retrieves a list of inventory levels for a location. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/locations.json | Retrieves a list of locations |
| GET | /admin/api/2020-04/locations/{location_id}.json | Retrieves a single location by its ID |
| GET | /admin/api/2020-04/locations/count.json | Retrieves a count of locations |
| GET | /admin/api/2020-04/locations/{location_id}/inventory_levels.json | Retrieves a list of inventory levels for a location. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/locations.json | Retrieves a list of locations |
| GET | /admin/api/2020-07/locations/{location_id}.json | Retrieves a single location by its ID |
| GET | /admin/api/2020-07/locations/count.json | Retrieves a count of locations |
| GET | /admin/api/2020-07/locations/{location_id}/inventory_levels.json | Retrieves a list of inventory levels for a location. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/locations.json | Retrieves a list of locations |
| GET | /admin/api/2020-10/locations/{location_id}.json | Retrieves a single location by its ID |
| GET | /admin/api/2020-10/locations/count.json | Retrieves a count of locations |
| GET | /admin/api/2020-10/locations/{location_id}/inventory_levels.json | Retrieves a list of inventory levels for a location. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/locations.json | Retrieves a list of locations |
| GET | /admin/api/2021-01/locations/{location_id}.json | Retrieves a single location by its ID |
| GET | /admin/api/2021-01/locations/count.json | Retrieves a count of locations |
| GET | /admin/api/2021-01/locations/{location_id}/inventory_levels.json | Retrieves a list of inventory levels for a location. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/locations.json | Retrieves a list of locations |
| GET | /admin/api/unstable/locations/{location_id}.json | Retrieves a single location by its ID |
| GET | /admin/api/unstable/locations/count.json | Retrieves a count of locations |
| GET | /admin/api/unstable/locations/{location_id}/inventory_levels.json | Retrieves a list of inventory levels for a location. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/metafields.json | Retrieves a list of metafields that belong to a Product Image resource. |
| POST | /admin/api/2020-01/metafields.json | Creates a new metafield for a resource. |
| GET | /admin/api/2020-01/metafields/count.json | Retrieves a count of a resource's metafields. |
| GET | /admin/api/2020-01/metafields/{metafield_id}.json | Retrieves a single metafield from a resource by its ID. |
| PUT | /admin/api/2020-01/metafields/{metafield_id}.json | Updates a metafield. |
| DELETE | /admin/api/2020-01/metafields/{metafield_id}.json | Deletes a metafield by its ID. |
| GET | /admin/api/2020-04/metafields.json | Retrieves a list of metafields that belong to a Product Image resource. |
| POST | /admin/api/2020-04/metafields.json | Creates a new metafield for a resource. |
| GET | /admin/api/2020-04/metafields/count.json | Retrieves a count of a resource's metafields. |
| GET | /admin/api/2020-04/metafields/{metafield_id}.json | Retrieves a single metafield from a resource by its ID. |
| PUT | /admin/api/2020-04/metafields/{metafield_id}.json | Updates a metafield. |
| DELETE | /admin/api/2020-04/metafields/{metafield_id}.json | Deletes a metafield by its ID. |
| GET | /admin/api/2020-07/metafields.json | Retrieves a list of metafields that belong to a Product Image resource. |
| POST | /admin/api/2020-07/metafields.json | Creates a new metafield for a resource. |
| GET | /admin/api/2020-07/metafields/count.json | Retrieves a count of a resource's metafields. |
| GET | /admin/api/2020-07/metafields/{metafield_id}.json | Retrieves a single metafield from a resource by its ID. |
| PUT | /admin/api/2020-07/metafields/{metafield_id}.json | Updates a metafield. |
| DELETE | /admin/api/2020-07/metafields/{metafield_id}.json | Deletes a metafield by its ID. |
| GET | /admin/api/2020-10/metafields.json | Retrieves a list of metafields that belong to a Product Image resource. |
| POST | /admin/api/2020-10/metafields.json | Creates a new metafield for a resource. |
| GET | /admin/api/2020-10/metafields/count.json | Retrieves a count of a resource's metafields. |
| GET | /admin/api/2020-10/metafields/{metafield_id}.json | Retrieves a single metafield from a resource by its ID. |
| PUT | /admin/api/2020-10/metafields/{metafield_id}.json | Updates a metafield. |
| DELETE | /admin/api/2020-10/metafields/{metafield_id}.json | Deletes a metafield by its ID. |
| GET | /admin/api/2021-01/metafields.json | Retrieves a list of metafields that belong to a Product Image resource. |
| POST | /admin/api/2021-01/metafields.json | Creates a new metafield for a resource. |
| GET | /admin/api/2021-01/metafields/count.json | Retrieves a count of a resource's metafields. |
| GET | /admin/api/2021-01/metafields/{metafield_id}.json | Retrieves a single metafield from a resource by its ID. |
| PUT | /admin/api/2021-01/metafields/{metafield_id}.json | Updates a metafield. |
| DELETE | /admin/api/2021-01/metafields/{metafield_id}.json | Deletes a metafield by its ID. |
| GET | /admin/api/unstable/metafields.json | Retrieves a list of metafields that belong to a Product Image resource. |
| POST | /admin/api/unstable/metafields.json | Creates a new metafield for a resource. |
| GET | /admin/api/unstable/metafields/count.json | Retrieves a count of a resource's metafields. |
| GET | /admin/api/unstable/metafields/{metafield_id}.json | Retrieves a single metafield from a resource by its ID. |
| PUT | /admin/api/unstable/metafields/{metafield_id}.json | Updates a metafield. |
| DELETE | /admin/api/unstable/metafields/{metafield_id}.json | Deletes a metafield by its ID. |
| GET | /admin/api/2020-01/blogs/{blog_id}/articles.json | Retrieves a list of all articles from a blog. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/blogs/{blog_id}/articles.json | Creates an article for a blog |
| GET | /admin/api/2020-01/blogs/{blog_id}/articles/count.json | Retrieves a count of all articles from a blog |
| GET | /admin/api/2020-01/blogs/{blog_id}/articles/{article_id}.json | Retrieves a single article |
| PUT | /admin/api/2020-01/blogs/{blog_id}/articles/{article_id}.json | Updates an article |
| DELETE | /admin/api/2020-01/blogs/{blog_id}/articles/{article_id}.json | Deletes an article |
| GET | /admin/api/2020-01/articles/authors.json | Retrieves a list all of article authors |
| GET | /admin/api/2020-01/articles/tags.json | Retrieves a list of all the tags |
| GET | /admin/api/2020-04/blogs/{blog_id}/articles.json | Retrieves a list of all articles from a blog. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/blogs/{blog_id}/articles.json | Creates an article for a blog |
| GET | /admin/api/2020-04/blogs/{blog_id}/articles/count.json | Retrieves a count of all articles from a blog |
| GET | /admin/api/2020-04/blogs/{blog_id}/articles/{article_id}.json | Retrieves a single article |
| PUT | /admin/api/2020-04/blogs/{blog_id}/articles/{article_id}.json | Updates an article |
| DELETE | /admin/api/2020-04/blogs/{blog_id}/articles/{article_id}.json | Deletes an article |
| GET | /admin/api/2020-04/articles/authors.json | Retrieves a list all of article authors |
| GET | /admin/api/2020-04/articles/tags.json | Retrieves a list of all the tags |
| GET | /admin/api/2020-07/blogs/{blog_id}/articles.json | Retrieves a list of all articles from a blog. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/blogs/{blog_id}/articles.json | Creates an article for a blog |
| GET | /admin/api/2020-07/blogs/{blog_id}/articles/count.json | Retrieves a count of all articles from a blog |
| GET | /admin/api/2020-07/blogs/{blog_id}/articles/{article_id}.json | Retrieves a single article |
| PUT | /admin/api/2020-07/blogs/{blog_id}/articles/{article_id}.json | Updates an article |
| DELETE | /admin/api/2020-07/blogs/{blog_id}/articles/{article_id}.json | Deletes an article |
| GET | /admin/api/2020-07/articles/authors.json | Retrieves a list all of article authors |
| GET | /admin/api/2020-07/articles/tags.json | Retrieves a list of all the tags |
| GET | /admin/api/2020-10/blogs/{blog_id}/articles.json | Retrieves a list of all articles from a blog. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/blogs/{blog_id}/articles.json | Creates an article for a blog |
| GET | /admin/api/2020-10/blogs/{blog_id}/articles/count.json | Retrieves a count of all articles from a blog |
| GET | /admin/api/2020-10/blogs/{blog_id}/articles/{article_id}.json | Retrieves a single article |
| PUT | /admin/api/2020-10/blogs/{blog_id}/articles/{article_id}.json | Updates an article |
| DELETE | /admin/api/2020-10/blogs/{blog_id}/articles/{article_id}.json | Deletes an article |
| GET | /admin/api/2020-10/articles/authors.json | Retrieves a list all of article authors |
| GET | /admin/api/2020-10/articles/tags.json | Retrieves a list of all the tags |
| GET | /admin/api/2021-01/blogs/{blog_id}/articles.json | Retrieves a list of all articles from a blog. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/blogs/{blog_id}/articles.json | Creates an article for a blog |
| GET | /admin/api/2021-01/blogs/{blog_id}/articles/count.json | Retrieves a count of all articles from a blog |
| GET | /admin/api/2021-01/blogs/{blog_id}/articles/{article_id}.json | Retrieves a single article |
| PUT | /admin/api/2021-01/blogs/{blog_id}/articles/{article_id}.json | Updates an article |
| DELETE | /admin/api/2021-01/blogs/{blog_id}/articles/{article_id}.json | Deletes an article |
| GET | /admin/api/2021-01/articles/authors.json | Retrieves a list all of article authors |
| GET | /admin/api/2021-01/articles/tags.json | Retrieves a list of all the tags |
| GET | /admin/api/unstable/blogs/{blog_id}/articles.json | Retrieves a list of all articles from a blog. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/blogs/{blog_id}/articles.json | Creates an article for a blog |
| GET | /admin/api/unstable/blogs/{blog_id}/articles/count.json | Retrieves a count of all articles from a blog |
| GET | /admin/api/unstable/blogs/{blog_id}/articles/{article_id}.json | Retrieves a single article |
| PUT | /admin/api/unstable/blogs/{blog_id}/articles/{article_id}.json | Updates an article |
| DELETE | /admin/api/unstable/blogs/{blog_id}/articles/{article_id}.json | Deletes an article |
| GET | /admin/api/unstable/articles/authors.json | Retrieves a list all of article authors |
| GET | /admin/api/unstable/articles/tags.json | Retrieves a list of all the tags |
| GET | /admin/api/2020-01/themes/{theme_id}/assets.json | Retrieves a single asset for a theme by its key. |
| PUT | /admin/api/2020-01/themes/{theme_id}/assets.json | Creates or updates an asset for a theme. |
| DELETE | /admin/api/2020-01/themes/{theme_id}/assets.json | Deletes an asset from a theme. |
| GET | /admin/api/2020-04/themes/{theme_id}/assets.json | Retrieves a single asset for a theme by its key. |
| PUT | /admin/api/2020-04/themes/{theme_id}/assets.json | Creates or updates an asset for a theme. |
| DELETE | /admin/api/2020-04/themes/{theme_id}/assets.json | Deletes an asset from a theme. |
| GET | /admin/api/2020-07/themes/{theme_id}/assets.json | Retrieves a single asset for a theme by its key. |
| PUT | /admin/api/2020-07/themes/{theme_id}/assets.json | Creates or updates an asset for a theme. |
| DELETE | /admin/api/2020-07/themes/{theme_id}/assets.json | Deletes an asset from a theme. |
| GET | /admin/api/2020-10/themes/{theme_id}/assets.json | Retrieves a single asset for a theme by its key. |
| PUT | /admin/api/2020-10/themes/{theme_id}/assets.json | Creates or updates an asset for a theme. |
| DELETE | /admin/api/2020-10/themes/{theme_id}/assets.json | Deletes an asset from a theme. |
| GET | /admin/api/2021-01/themes/{theme_id}/assets.json | Retrieves a single asset for a theme by its key. |
| PUT | /admin/api/2021-01/themes/{theme_id}/assets.json | Creates or updates an asset for a theme. |
| DELETE | /admin/api/2021-01/themes/{theme_id}/assets.json | Deletes an asset from a theme. |
| GET | /admin/api/unstable/themes/{theme_id}/assets.json | Retrieves a single asset for a theme by its key. |
| PUT | /admin/api/unstable/themes/{theme_id}/assets.json | Creates or updates an asset for a theme. |
| DELETE | /admin/api/unstable/themes/{theme_id}/assets.json | Deletes an asset from a theme. |
| GET | /admin/api/2020-01/blogs.json | Retrieve a list of all blogs. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/blogs.json | Create a new blog |
| GET | /admin/api/2020-01/blogs/count.json | Get a count of all blogs |
| GET | /admin/api/2020-01/blogs/{blog_id}.json | Get a single blog by its ID |
| PUT | /admin/api/2020-01/blogs/{blog_id}.json | Update a blog |
| DELETE | /admin/api/2020-01/blogs/{blog_id}.json | Delete a blog |
| GET | /admin/api/2020-01/comments.json | Retrieves a list of comments. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/comments.json | Creates a comment for an article |
| GET | /admin/api/2020-01/comments/count.json | Retrieves a count of comments |
| GET | /admin/api/2020-01/comments/{comment_id}.json | Retrieves a single comment by its ID |
| PUT | /admin/api/2020-01/comments/{comment_id}.json | Updates a comment of an article |
| POST | /admin/api/2020-01/comments/{comment_id}/spam.json | Marks a comment as spam |
| POST | /admin/api/2020-01/comments/{comment_id}/not_spam.json | Marks a comment as not spam |
| POST | /admin/api/2020-01/comments/{comment_id}/approve.json | Approves a comment |
| POST | /admin/api/2020-01/comments/{comment_id}/remove.json | Removes a comment |
| POST | /admin/api/2020-01/comments/{comment_id}/restore.json | Restores a previously removed comment |
| GET | /admin/api/2020-01/redirects.json | Retrieves a list of URL redirects. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/redirects.json | Creates a redirect. When you provide a full URL as the value of the path property, it will be saved as an absolute path without the domain. |
| GET | /admin/api/2020-01/redirects/count.json | Retrieves a count of URL redirects |
| GET | /admin/api/2020-01/redirects/{redirect_id}.json | Retrieves a single redirect |
| PUT | /admin/api/2020-01/redirects/{redirect_id}.json | Updates an existing redirect |
| DELETE | /admin/api/2020-01/redirects/{redirect_id}.json | Deletes a redirect |
| GET | /admin/api/2020-04/redirects.json | Retrieves a list of URL redirects. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/redirects.json | Creates a redirect. When you provide a full URL as the value of the path property, it will be saved as an absolute path without the domain. |
| GET | /admin/api/2020-04/redirects/count.json | Retrieves a count of URL redirects |
| GET | /admin/api/2020-04/redirects/{redirect_id}.json | Retrieves a single redirect |
| PUT | /admin/api/2020-04/redirects/{redirect_id}.json | Updates an existing redirect |
| DELETE | /admin/api/2020-04/redirects/{redirect_id}.json | Deletes a redirect |
| GET | /admin/api/2020-07/redirects.json | Retrieves a list of URL redirects. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/redirects.json | Creates a redirect. When you provide a full URL as the value of the path property, it will be saved as an absolute path without the domain. |
| GET | /admin/api/2020-07/redirects/count.json | Retrieves a count of URL redirects |
| GET | /admin/api/2020-07/redirects/{redirect_id}.json | Retrieves a single redirect |
| PUT | /admin/api/2020-07/redirects/{redirect_id}.json | Updates an existing redirect |
| DELETE | /admin/api/2020-07/redirects/{redirect_id}.json | Deletes a redirect |
| GET | /admin/api/2020-10/redirects.json | Retrieves a list of URL redirects. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/redirects.json | Creates a redirect. When you provide a full URL as the value of the path property, it will be saved as an absolute path without the domain. |
| GET | /admin/api/2020-10/redirects/count.json | Retrieves a count of URL redirects |
| GET | /admin/api/2020-10/redirects/{redirect_id}.json | Retrieves a single redirect |
| PUT | /admin/api/2020-10/redirects/{redirect_id}.json | Updates an existing redirect |
| DELETE | /admin/api/2020-10/redirects/{redirect_id}.json | Deletes a redirect |
| GET | /admin/api/2021-01/redirects.json | Retrieves a list of URL redirects. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/redirects.json | Creates a redirect. When you provide a full URL as the value of the path property, it will be saved as an absolute path without the domain. |
| GET | /admin/api/2021-01/redirects/count.json | Retrieves a count of URL redirects |
| GET | /admin/api/2021-01/redirects/{redirect_id}.json | Retrieves a single redirect |
| PUT | /admin/api/2021-01/redirects/{redirect_id}.json | Updates an existing redirect |
| DELETE | /admin/api/2021-01/redirects/{redirect_id}.json | Deletes a redirect |
| GET | /admin/api/unstable/redirects.json | Retrieves a list of URL redirects. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/redirects.json | Creates a redirect. When you provide a full URL as the value of the path property, it will be saved as an absolute path without the domain. |
| GET | /admin/api/unstable/redirects/count.json | Retrieves a count of URL redirects |
| GET | /admin/api/unstable/redirects/{redirect_id}.json | Retrieves a single redirect |
| PUT | /admin/api/unstable/redirects/{redirect_id}.json | Updates an existing redirect |
| DELETE | /admin/api/unstable/redirects/{redirect_id}.json | Deletes a redirect |
| GET | /admin/api/2020-01/script_tags.json | Retrieves a list of all script tags. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/script_tags.json | Creates a new script tag |
| GET | /admin/api/2020-01/script_tags/count.json | Retrieves a count of all script tags |
| GET | /admin/api/2020-01/script_tags/{script_tag_id}.json | Retrieves a single script tag |
| PUT | /admin/api/2020-01/script_tags/{script_tag_id}.json | Updates a script tag |
| DELETE | /admin/api/2020-01/script_tags/{script_tag_id}.json | Deletes a script tag |
| GET | /admin/api/2020-04/script_tags.json | Retrieves a list of all script tags. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/script_tags.json | Creates a new script tag |
| GET | /admin/api/2020-04/script_tags/count.json | Retrieves a count of all script tags |
| GET | /admin/api/2020-04/script_tags/{script_tag_id}.json | Retrieves a single script tag |
| PUT | /admin/api/2020-04/script_tags/{script_tag_id}.json | Updates a script tag |
| DELETE | /admin/api/2020-04/script_tags/{script_tag_id}.json | Deletes a script tag |
| GET | /admin/api/2020-07/script_tags.json | Retrieves a list of all script tags. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/script_tags.json | Creates a new script tag |
| GET | /admin/api/2020-07/script_tags/count.json | Retrieves a count of all script tags |
| GET | /admin/api/2020-07/script_tags/{script_tag_id}.json | Retrieves a single script tag |
| PUT | /admin/api/2020-07/script_tags/{script_tag_id}.json | Updates a script tag |
| DELETE | /admin/api/2020-07/script_tags/{script_tag_id}.json | Deletes a script tag |
| GET | /admin/api/2020-10/script_tags.json | Retrieves a list of all script tags. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/script_tags.json | Creates a new script tag |
| GET | /admin/api/2020-10/script_tags/count.json | Retrieves a count of all script tags |
| GET | /admin/api/2020-10/script_tags/{script_tag_id}.json | Retrieves a single script tag |
| PUT | /admin/api/2020-10/script_tags/{script_tag_id}.json | Updates a script tag |
| DELETE | /admin/api/2020-10/script_tags/{script_tag_id}.json | Deletes a script tag |
| GET | /admin/api/2021-01/script_tags.json | Retrieves a list of all script tags. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/script_tags.json | Creates a new script tag |
| GET | /admin/api/2021-01/script_tags/count.json | Retrieves a count of all script tags |
| GET | /admin/api/2021-01/script_tags/{script_tag_id}.json | Retrieves a single script tag |
| PUT | /admin/api/2021-01/script_tags/{script_tag_id}.json | Updates a script tag |
| DELETE | /admin/api/2021-01/script_tags/{script_tag_id}.json | Deletes a script tag |
| GET | /admin/api/unstable/script_tags.json | Retrieves a list of all script tags. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/script_tags.json | Creates a new script tag |
| GET | /admin/api/unstable/script_tags/count.json | Retrieves a count of all script tags |
| GET | /admin/api/unstable/script_tags/{script_tag_id}.json | Retrieves a single script tag |
| PUT | /admin/api/unstable/script_tags/{script_tag_id}.json | Updates a script tag |
| DELETE | /admin/api/unstable/script_tags/{script_tag_id}.json | Deletes a script tag |
| GET | /admin/api/2020-01/themes.json | Retrieves a list of themes. |
| POST | /admin/api/2020-01/themes.json | Creates a theme by providing the public URL of a ZIP file that contains the theme. |
| GET | /admin/api/2020-01/themes/{theme_id}.json | Retrieves a single theme. |
| PUT | /admin/api/2020-01/themes/{theme_id}.json | Updates an existing theme. |
| DELETE | /admin/api/2020-01/themes/{theme_id}.json | Deletes a theme. |
| GET | /admin/api/2020-04/themes.json | Retrieves a list of themes. |
| POST | /admin/api/2020-04/themes.json | Creates a theme by providing the public URL of a ZIP file that contains the theme. |
| GET | /admin/api/2020-04/themes/{theme_id}.json | Retrieves a single theme. |
| PUT | /admin/api/2020-04/themes/{theme_id}.json | Updates an existing theme. |
| DELETE | /admin/api/2020-04/themes/{theme_id}.json | Deletes a theme. |
| GET | /admin/api/2020-07/themes.json | Retrieves a list of themes. |
| POST | /admin/api/2020-07/themes.json | Creates a theme by providing the public URL of a ZIP file that contains the theme. |
| GET | /admin/api/2020-07/themes/{theme_id}.json | Retrieves a single theme. |
| PUT | /admin/api/2020-07/themes/{theme_id}.json | Updates an existing theme. |
| DELETE | /admin/api/2020-07/themes/{theme_id}.json | Deletes a theme. |
| GET | /admin/api/2020-10/themes.json | Retrieves a list of themes. |
| POST | /admin/api/2020-10/themes.json | Creates a theme by providing the public URL of a ZIP file that contains the theme. |
| GET | /admin/api/2020-10/themes/{theme_id}.json | Retrieves a single theme. |
| PUT | /admin/api/2020-10/themes/{theme_id}.json | Updates an existing theme. |
| DELETE | /admin/api/2020-10/themes/{theme_id}.json | Deletes a theme. |
| GET | /admin/api/2021-01/themes.json | Retrieves a list of themes. |
| POST | /admin/api/2021-01/themes.json | Creates a theme by providing the public URL of a ZIP file that contains the theme. |
| GET | /admin/api/2021-01/themes/{theme_id}.json | Retrieves a single theme. |
| PUT | /admin/api/2021-01/themes/{theme_id}.json | Updates an existing theme. |
| DELETE | /admin/api/2021-01/themes/{theme_id}.json | Deletes a theme. |
| GET | /admin/api/unstable/themes.json | Retrieves a list of themes. |
| POST | /admin/api/unstable/themes.json | Creates a theme by providing the public URL of a ZIP file that contains the theme. |
| GET | /admin/api/unstable/themes/{theme_id}.json | Retrieves a single theme. |
| PUT | /admin/api/unstable/themes/{theme_id}.json | Updates an existing theme. |
| DELETE | /admin/api/unstable/themes/{theme_id}.json | Deletes a theme. |
| GET | /admin/api/2020-01/checkouts/count.json | Retrieves a count of checkouts from the past 90 days |
| POST | /admin/api/2020-01/checkouts.json | Creates a checkout |
| GET | /admin/api/2020-04/checkouts/count.json | Retrieves a count of checkouts from the past 90 days |
| POST | /admin/api/2020-04/checkouts.json | Creates a checkout |
| GET | /admin/api/2020-07/checkouts/count.json | Retrieves a count of checkouts from the past 90 days |
| POST | /admin/api/2020-07/checkouts.json | Creates a checkout |
| GET | /admin/api/2020-10/checkouts/count.json | Retrieves a count of checkouts from the past 90 days |
| POST | /admin/api/2020-10/checkouts.json | Creates a checkout |
| GET | /admin/api/2021-01/checkouts/count.json | Retrieves a count of checkouts from the past 90 days |
| POST | /admin/api/2021-01/checkouts.json | Creates a checkout |
| GET | /admin/api/unstable/checkouts/count.json | Retrieves a count of checkouts from the past 90 days |
| POST | /admin/api/unstable/checkouts.json | Creates a checkout |
| GET | /admin/api/2020-01/orders.json | Retrieves a list of orders. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/orders.json | Creates an order. By default, product inventory is not claimed. |
| GET | /admin/api/2020-01/orders/{order_id}.json | Retrieves a specific order |
| PUT | /admin/api/2020-01/orders/{order_id}.json | Updates an order |
| DELETE | /admin/api/2020-01/orders/{order_id}.json | Deletes an order. Orders that interact with an online gateway can't be deleted. |
| GET | /admin/api/2020-01/orders/count.json | Retrieves an order count |
| POST | /admin/api/2020-01/orders/{order_id}/close.json | Closes an order |
| POST | /admin/api/2020-01/orders/{order_id}/open.json | Re-opens a closed order |
| POST | /admin/api/2020-01/orders/{order_id}/cancel.json | Caution |
| GET | /admin/api/2020-04/orders.json | Retrieves a list of orders. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/orders.json | Creates an order. By default, product inventory is not claimed. |
| GET | /admin/api/2020-04/orders/{order_id}.json | Retrieves a specific order |
| PUT | /admin/api/2020-04/orders/{order_id}.json | Updates an order |
| DELETE | /admin/api/2020-04/orders/{order_id}.json | Deletes an order. Orders that interact with an online gateway can't be deleted. |
| GET | /admin/api/2020-04/orders/count.json | Retrieves an order count |
| POST | /admin/api/2020-04/orders/{order_id}/close.json | Closes an order |
| POST | /admin/api/2020-04/orders/{order_id}/open.json | Re-opens a closed order |
| POST | /admin/api/2020-04/orders/{order_id}/cancel.json | Caution |
| GET | /admin/api/2020-07/orders.json | Retrieves a list of orders. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/orders/{order_id}/risks.json | Creates an order risk for an order |
| GET | /admin/api/2020-01/orders/{order_id}/risks.json | Retrieves a list of all order risks for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/orders/{order_id}/risks/{risk_id}.json | Retrieves a single order risk by its ID |
| PUT | /admin/api/2020-01/orders/{order_id}/risks/{risk_id}.json | Updates an order risk |
| DELETE | /admin/api/2020-01/orders/{order_id}/risks/{risk_id}.json | Deletes an order risk for an order |
| POST | /admin/api/2020-04/orders/{order_id}/risks.json | Creates an order risk for an order |
| GET | /admin/api/2020-04/orders/{order_id}/risks.json | Retrieves a list of all order risks for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/orders/{order_id}/risks/{risk_id}.json | Retrieves a single order risk by its ID |
| PUT | /admin/api/2020-04/orders/{order_id}/risks/{risk_id}.json | Updates an order risk |
| DELETE | /admin/api/2020-04/orders/{order_id}/risks/{risk_id}.json | Deletes an order risk for an order |
| POST | /admin/api/2020-07/orders/{order_id}/risks.json | Creates an order risk for an order |
| GET | /admin/api/2020-07/orders/{order_id}/risks.json | Retrieves a list of all order risks for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/orders/{order_id}/risks/{risk_id}.json | Retrieves a single order risk by its ID |
| PUT | /admin/api/2020-07/orders/{order_id}/risks/{risk_id}.json | Updates an order risk |
| DELETE | /admin/api/2020-07/orders/{order_id}/risks/{risk_id}.json | Deletes an order risk for an order |
| POST | /admin/api/2020-10/orders/{order_id}/risks.json | Creates an order risk for an order |
| GET | /admin/api/2020-10/orders/{order_id}/risks.json | Retrieves a list of all order risks for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/orders/{order_id}/risks/{risk_id}.json | Retrieves a single order risk by its ID |
| PUT | /admin/api/2020-10/orders/{order_id}/risks/{risk_id}.json | Updates an order risk |
| DELETE | /admin/api/2020-10/orders/{order_id}/risks/{risk_id}.json | Deletes an order risk for an order |
| POST | /admin/api/2021-01/orders/{order_id}/risks.json | Creates an order risk for an order |
| GET | /admin/api/2021-01/orders/{order_id}/risks.json | Retrieves a list of all order risks for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/orders/{order_id}/risks/{risk_id}.json | Retrieves a single order risk by its ID |
| PUT | /admin/api/2021-01/orders/{order_id}/risks/{risk_id}.json | Updates an order risk |
| DELETE | /admin/api/2021-01/orders/{order_id}/risks/{risk_id}.json | Deletes an order risk for an order |
| POST | /admin/api/unstable/orders/{order_id}/risks.json | Creates an order risk for an order |
| GET | /admin/api/unstable/orders/{order_id}/risks.json | Retrieves a list of all order risks for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/orders/{order_id}/risks/{risk_id}.json | Retrieves a single order risk by its ID |
| PUT | /admin/api/unstable/orders/{order_id}/risks/{risk_id}.json | Updates an order risk |
| DELETE | /admin/api/unstable/orders/{order_id}/risks/{risk_id}.json | Deletes an order risk for an order |
| GET | /admin/api/2020-01/orders/{order_id}/refunds.json | Retrieves a list of refunds for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/orders/{order_id}/refunds.json | Caution |
| GET | /admin/api/2020-01/orders/{order_id}/refunds/{refund_id}.json | Retrieves a specific refund. |
| POST | /admin/api/2020-01/orders/{order_id}/refunds/calculate.json | Caution |
| GET | /admin/api/2020-04/orders/{order_id}/refunds.json | Retrieves a list of refunds for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/orders/{order_id}/refunds.json | Caution |
| GET | /admin/api/2020-04/orders/{order_id}/refunds/{refund_id}.json | Retrieves a specific refund. |
| POST | /admin/api/2020-04/orders/{order_id}/refunds/calculate.json | Caution |
| GET | /admin/api/2020-07/orders/{order_id}/refunds.json | Retrieves a list of refunds for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/orders/{order_id}/refunds.json | Caution |
| GET | /admin/api/2020-07/orders/{order_id}/refunds/{refund_id}.json | Retrieves a specific refund. |
| POST | /admin/api/2020-07/orders/{order_id}/refunds/calculate.json | Caution |
| GET | /admin/api/2020-10/orders/{order_id}/refunds.json | Retrieves a list of refunds for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/orders/{order_id}/refunds.json | Caution |
| GET | /admin/api/2020-10/orders/{order_id}/refunds/{refund_id}.json | Retrieves a specific refund. |
| POST | /admin/api/2020-10/orders/{order_id}/refunds/calculate.json | Caution |
| GET | /admin/api/2021-01/orders/{order_id}/refunds.json | Retrieves a list of refunds for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/orders/{order_id}/refunds.json | Caution |
| GET | /admin/api/2021-01/orders/{order_id}/refunds/{refund_id}.json | Retrieves a specific refund. |
| POST | /admin/api/2021-01/orders/{order_id}/refunds/calculate.json | Caution |
| GET | /admin/api/unstable/orders/{order_id}/refunds.json | Retrieves a list of refunds for an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/orders/{order_id}/refunds.json | Caution |
| GET | /admin/api/unstable/orders/{order_id}/refunds/{refund_id}.json | Retrieves a specific refund. |
| POST | /admin/api/unstable/orders/{order_id}/refunds/calculate.json | Caution |
| GET | /admin/api/2020-01/gift_cards.json | Retrieves a list of gift cards. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/gift_cards.json | Creates a gift card |
| GET | /admin/api/2020-01/gift_cards/{gift_card_id}.json | Retrieves a single gift card by its ID |
| PUT | /admin/api/2020-01/gift_cards/{gift_card_id}.json | Updates an existing gift card. |
| GET | /admin/api/2020-01/gift_cards/count.json | Retrieves a count of gift cards |
| POST | /admin/api/2020-01/gift_cards/{gift_card_id}/disable.json | Disables a gift card. Disabling a gift card can't be undone. |
| GET | /admin/api/2020-01/gift_cards/search.json | Searches for gift cards that match a supplied query. The following fields are indexed by search: |
| GET | /admin/api/2020-04/gift_cards.json | Retrieves a list of gift cards. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/gift_cards.json | Creates a gift card |
| GET | /admin/api/2020-04/gift_cards/{gift_card_id}.json | Retrieves a single gift card by its ID |
| PUT | /admin/api/2020-04/gift_cards/{gift_card_id}.json | Updates an existing gift card. |
| GET | /admin/api/2020-04/gift_cards/count.json | Retrieves a count of gift cards |
| POST | /admin/api/2020-04/gift_cards/{gift_card_id}/disable.json | Disables a gift card. Disabling a gift card can't be undone. |
| GET | /admin/api/2020-04/gift_cards/search.json | Searches for gift cards that match a supplied query. The following fields are indexed by search: |
| GET | /admin/api/2020-07/gift_cards.json | Retrieves a list of gift cards. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/gift_cards.json | Creates a gift card |
| GET | /admin/api/2020-07/gift_cards/{gift_card_id}.json | Retrieves a single gift card by its ID |
| PUT | /admin/api/2020-07/gift_cards/{gift_card_id}.json | Updates an existing gift card. |
| GET | /admin/api/2020-07/gift_cards/count.json | Retrieves a count of gift cards |
| POST | /admin/api/2020-07/gift_cards/{gift_card_id}/disable.json | Disables a gift card. Disabling a gift card can't be undone. |
| GET | /admin/api/2020-07/gift_cards/search.json | Searches for gift cards that match a supplied query. The following fields are indexed by search: |
| GET | /admin/api/2020-10/gift_cards.json | Retrieves a list of gift cards. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/gift_cards.json | Creates a gift card |
| GET | /admin/api/2020-10/gift_cards/{gift_card_id}.json | Retrieves a single gift card by its ID |
| PUT | /admin/api/2020-10/gift_cards/{gift_card_id}.json | Updates an existing gift card. |
| GET | /admin/api/2020-10/gift_cards/count.json | Retrieves a count of gift cards |
| POST | /admin/api/2020-10/gift_cards/{gift_card_id}/disable.json | Disables a gift card. Disabling a gift card can't be undone. |
| GET | /admin/api/2020-10/gift_cards/search.json | Searches for gift cards that match a supplied query. The following fields are indexed by search: |
| GET | /admin/api/2021-01/gift_cards.json | Retrieves a list of gift cards. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/gift_cards.json | Creates a gift card |
| GET | /admin/api/2021-01/gift_cards/{gift_card_id}.json | Retrieves a single gift card by its ID |
| PUT | /admin/api/2021-01/gift_cards/{gift_card_id}.json | Updates an existing gift card. |
| GET | /admin/api/2021-01/gift_cards/count.json | Retrieves a count of gift cards |
| POST | /admin/api/2021-01/gift_cards/{gift_card_id}/disable.json | Disables a gift card. Disabling a gift card can't be undone. |
| GET | /admin/api/2021-01/gift_cards/search.json | Searches for gift cards that match a supplied query. The following fields are indexed by search: |
| GET | /admin/api/unstable/gift_cards.json | Retrieves a list of gift cards. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/gift_cards.json | Creates a gift card |
| GET | /admin/api/unstable/gift_cards/{gift_card_id}.json | Retrieves a single gift card by its ID |
| PUT | /admin/api/unstable/gift_cards/{gift_card_id}.json | Updates an existing gift card. |
| GET | /admin/api/unstable/gift_cards/count.json | Retrieves a count of gift cards |
| POST | /admin/api/unstable/gift_cards/{gift_card_id}/disable.json | Disables a gift card. Disabling a gift card can't be undone. |
| GET | /admin/api/unstable/gift_cards/search.json | Searches for gift cards that match a supplied query. The following fields are indexed by search: |
| GET | /admin/api/2020-01/users.json | Retrieves a list of all users. Note: As of version 2021-01, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/users/{user_id}.json | Retrieves a single user |
| GET | /admin/api/2020-01/users/current.json | Retrieves information about the user account associated with the access token used to make this API request. This request works only when the access token was created for a specific user of the shop. |
| GET | /admin/api/2020-04/users.json | Retrieves a list of all users. Note: As of version 2021-01, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/users/{user_id}.json | Retrieves a single user |
| GET | /admin/api/2020-04/users/current.json | Retrieves information about the user account associated with the access token used to make this API request. This request works only when the access token was created for a specific user of the shop. |
| GET | /admin/api/2020-07/users.json | Retrieves a list of all users. Note: As of version 2021-01, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/users/{user_id}.json | Retrieves a single user |
| GET | /admin/api/2020-07/users/current.json | Retrieves information about the user account associated with the access token used to make this API request. This request works only when the access token was created for a specific user of the shop. |
| GET | /admin/api/2020-10/users.json | Retrieves a list of all users. Note: As of version 2021-01, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/users/{user_id}.json | Retrieves a single user |
| GET | /admin/api/2020-10/users/current.json | Retrieves information about the user account associated with the access token used to make this API request. This request works only when the access token was created for a specific user of the shop. |
| GET | /admin/api/2021-01/users.json | Retrieves a list of all users. Note: As of version 2021-01, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/users/{user_id}.json | Retrieves a single user |
| GET | /admin/api/2021-01/users/current.json | Retrieves information about the user account associated with the access token used to make this API request. This request works only when the access token was created for a specific user of the shop. |
| GET | /admin/api/unstable/users.json | Retrieves a list of all users. Note: As of version 2021-01, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/users/{user_id}.json | Retrieves a single user |
| GET | /admin/api/unstable/users/current.json | Retrieves information about the user account associated with the access token used to make this API request. This request works only when the access token was created for a specific user of the shop. |
| POST | /admin/api/2020-01/collects.json | Adds a product to a custom collection. |
| GET | /admin/api/2020-01/collects.json | Retrieves a list of collects. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| DELETE | /admin/api/2020-01/collects/{collect_id}.json | Removes a product from a collection. |
| GET | /admin/api/2020-01/collects/{collect_id}.json | Retrieves a specific collect by its ID. |
| GET | /admin/api/2020-01/collects/count.json | Retrieves a count of collects. |
| POST | /admin/api/2020-04/collects.json | Adds a product to a custom collection. |
| GET | /admin/api/2020-04/collects.json | Retrieves a list of collects. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| DELETE | /admin/api/2020-04/collects/{collect_id}.json | Removes a product from a collection. |
| GET | /admin/api/2020-04/collects/{collect_id}.json | Retrieves a specific collect by its ID. |
| GET | /admin/api/2020-04/collects/count.json | Retrieves a count of collects. |
| POST | /admin/api/2020-07/collects.json | Adds a product to a custom collection. |
| GET | /admin/api/2020-07/collects.json | Retrieves a list of collects. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| DELETE | /admin/api/2020-07/collects/{collect_id}.json | Removes a product from a collection. |
| GET | /admin/api/2020-07/collects/{collect_id}.json | Retrieves a specific collect by its ID. |
| GET | /admin/api/2020-07/collects/count.json | Retrieves a count of collects. |
| POST | /admin/api/2020-10/collects.json | Adds a product to a custom collection. |
| GET | /admin/api/2020-10/collects.json | Retrieves a list of collects. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| DELETE | /admin/api/2020-10/collects/{collect_id}.json | Removes a product from a collection. |
| GET | /admin/api/2020-10/collects/{collect_id}.json | Retrieves a specific collect by its ID. |
| GET | /admin/api/2020-10/collects/count.json | Retrieves a count of collects. |
| POST | /admin/api/2021-01/collects.json | Adds a product to a custom collection. |
| GET | /admin/api/2021-01/collects.json | Retrieves a list of collects. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| DELETE | /admin/api/2021-01/collects/{collect_id}.json | Removes a product from a collection. |
| GET | /admin/api/2021-01/collects/{collect_id}.json | Retrieves a specific collect by its ID. |
| GET | /admin/api/2021-01/collects/count.json | Retrieves a count of collects. |
| POST | /admin/api/unstable/collects.json | Adds a product to a custom collection. |
| GET | /admin/api/unstable/collects.json | Retrieves a list of collects. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| DELETE | /admin/api/unstable/collects/{collect_id}.json | Removes a product from a collection. |
| GET | /admin/api/unstable/collects/{collect_id}.json | Retrieves a specific collect by its ID. |
| GET | /admin/api/unstable/collects/count.json | Retrieves a count of collects. |
| GET | /admin/api/2020-01/collections/{collection_id}.json | Retrieves a single collection |
| GET | /admin/api/2020-01/collections/{collection_id}/products.json | Retrieve a list of products belonging to a collection. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints.. The products returned are sorted by the collection's sort order. |
| GET | /admin/api/2020-04/collections/{collection_id}.json | Retrieves a single collection |
| GET | /admin/api/2020-04/collections/{collection_id}/products.json | Retrieve a list of products belonging to a collection. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints.. The products returned are sorted by the collection's sort order. |
| GET | /admin/api/2020-07/collections/{collection_id}.json | Retrieves a single collection |
| GET | /admin/api/2020-07/collections/{collection_id}/products.json | Retrieve a list of products belonging to a collection. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints.. The products returned are sorted by the collection's sort order. |
| GET | /admin/api/2020-10/collections/{collection_id}.json | Retrieves a single collection |
| GET | /admin/api/2020-10/collections/{collection_id}/products.json | Retrieve a list of products belonging to a collection. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints.. The products returned are sorted by the collection's sort order. |
| GET | /admin/api/2021-01/collections/{collection_id}.json | Retrieves a single collection |
| GET | /admin/api/2021-01/collections/{collection_id}/products.json | Retrieve a list of products belonging to a collection. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints.. The products returned are sorted by the collection's sort order. |
| GET | /admin/api/unstable/collections/{collection_id}.json | Retrieves a single collection |
| GET | /admin/api/unstable/collections/{collection_id}/products.json | Retrieve a list of products belonging to a collection. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints.. The products returned are sorted by the collection's sort order. |
| GET | /admin/api/2020-01/custom_collections.json | Retrieves a list of custom collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/custom_collections.json | Creates a custom collection |
| GET | /admin/api/2020-01/custom_collections/count.json | Retrieves a count of custom collections |
| GET | /admin/api/2020-01/custom_collections/{custom_collection_id}.json | Retrieves a single custom collection |
| PUT | /admin/api/2020-01/custom_collections/{custom_collection_id}.json | Updates an existing custom collection |
| DELETE | /admin/api/2020-01/custom_collections/{custom_collection_id}.json | Deletes a custom collection |
| GET | /admin/api/2020-04/custom_collections.json | Retrieves a list of custom collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/custom_collections.json | Creates a custom collection |
| GET | /admin/api/2020-04/custom_collections/count.json | Retrieves a count of custom collections |
| GET | /admin/api/2020-04/custom_collections/{custom_collection_id}.json | Retrieves a single custom collection |
| PUT | /admin/api/2020-04/custom_collections/{custom_collection_id}.json | Updates an existing custom collection |
| DELETE | /admin/api/2020-04/custom_collections/{custom_collection_id}.json | Deletes a custom collection |
| GET | /admin/api/2020-07/custom_collections.json | Retrieves a list of custom collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/custom_collections.json | Creates a custom collection |
| GET | /admin/api/2020-07/custom_collections/count.json | Retrieves a count of custom collections |
| GET | /admin/api/2020-07/custom_collections/{custom_collection_id}.json | Retrieves a single custom collection |
| PUT | /admin/api/2020-07/custom_collections/{custom_collection_id}.json | Updates an existing custom collection |
| DELETE | /admin/api/2020-07/custom_collections/{custom_collection_id}.json | Deletes a custom collection |
| GET | /admin/api/2020-10/custom_collections.json | Retrieves a list of custom collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/custom_collections.json | Creates a custom collection |
| GET | /admin/api/2020-10/custom_collections/count.json | Retrieves a count of custom collections |
| GET | /admin/api/2020-10/custom_collections/{custom_collection_id}.json | Retrieves a single custom collection |
| PUT | /admin/api/2020-10/custom_collections/{custom_collection_id}.json | Updates an existing custom collection |
| DELETE | /admin/api/2020-10/custom_collections/{custom_collection_id}.json | Deletes a custom collection |
| GET | /admin/api/2021-01/custom_collections.json | Retrieves a list of custom collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/custom_collections.json | Creates a custom collection |
| GET | /admin/api/2021-01/custom_collections/count.json | Retrieves a count of custom collections |
| GET | /admin/api/2021-01/custom_collections/{custom_collection_id}.json | Retrieves a single custom collection |
| PUT | /admin/api/2021-01/custom_collections/{custom_collection_id}.json | Updates an existing custom collection |
| DELETE | /admin/api/2021-01/custom_collections/{custom_collection_id}.json | Deletes a custom collection |
| GET | /admin/api/unstable/custom_collections.json | Retrieves a list of custom collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/custom_collections.json | Creates a custom collection |
| GET | /admin/api/unstable/custom_collections/count.json | Retrieves a count of custom collections |
| GET | /admin/api/unstable/custom_collections/{custom_collection_id}.json | Retrieves a single custom collection |
| PUT | /admin/api/unstable/custom_collections/{custom_collection_id}.json | Updates an existing custom collection |
| DELETE | /admin/api/unstable/custom_collections/{custom_collection_id}.json | Deletes a custom collection |
| GET | /admin/api/2020-01/products.json | Retrieves a list of products. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/products.json | Creates a new product. |
| GET | /admin/api/2020-01/products/count.json | Retrieves a count of products. |
| GET | /admin/api/2020-01/products/{product_id}.json | Retrieves a single product. |
| PUT | /admin/api/2020-01/products/{product_id}.json | Updates a product and its variants and images. |
| DELETE | /admin/api/2020-01/products/{product_id}.json | Deletes a product. |
| GET | /admin/api/2020-04/products.json | Retrieves a list of products. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/products.json | Creates a new product. |
| GET | /admin/api/2020-04/products/count.json | Retrieves a count of products. |
| GET | /admin/api/2020-04/products/{product_id}.json | Retrieves a single product. |
| PUT | /admin/api/2020-04/products/{product_id}.json | Updates a product and its variants and images. |
| DELETE | /admin/api/2020-04/products/{product_id}.json | Deletes a product. |
| GET | /admin/api/2020-07/products.json | Retrieves a list of products. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/products.json | Creates a new product. |
| GET | /admin/api/2020-07/products/count.json | Retrieves a count of products. |
| GET | /admin/api/2020-07/products/{product_id}.json | Retrieves a single product. |
| PUT | /admin/api/2020-07/products/{product_id}.json | Updates a product and its variants and images. |
| DELETE | /admin/api/2020-07/products/{product_id}.json | Deletes a product. |
| GET | /admin/api/2020-10/products.json | Retrieves a list of products. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/products.json | Creates a new product. |
| GET | /admin/api/2020-10/products/count.json | Retrieves a count of products. |
| GET | /admin/api/2020-10/products/{product_id}.json | Retrieves a single product. |
| PUT | /admin/api/2020-10/products/{product_id}.json | Updates a product and its variants and images. |
| DELETE | /admin/api/2020-10/products/{product_id}.json | Deletes a product. |
| GET | /admin/api/2021-01/products.json | Retrieves a list of products. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/products.json | Creates a new product. |
| GET | /admin/api/2021-01/products/count.json | Retrieves a count of products. |
| GET | /admin/api/2021-01/products/{product_id}.json | Retrieves a single product. |
| PUT | /admin/api/2021-01/products/{product_id}.json | Updates a product and its variants and images. |
| DELETE | /admin/api/2021-01/products/{product_id}.json | Deletes a product. |
| GET | /admin/api/unstable/products.json | Retrieves a list of products. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/products.json | Creates a new product. |
| GET | /admin/api/unstable/products/count.json | Retrieves a count of products. |
| GET | /admin/api/unstable/products/{product_id}.json | Retrieves a single product. |
| PUT | /admin/api/unstable/products/{product_id}.json | Updates a product and its variants and images. |
| DELETE | /admin/api/unstable/products/{product_id}.json | Deletes a product. |
| GET | /admin/api/2020-01/products/{product_id}/images.json | Get all product images |
| POST | /admin/api/2020-01/products/{product_id}/images.json | Create a new product image |
| GET | /admin/api/2020-01/products/{product_id}/images/count.json | Get a count of all product images |
| GET | /admin/api/2020-01/products/{product_id}/images/{image_id}.json | Get a single product image by id |
| PUT | /admin/api/2020-01/products/{product_id}/images/{image_id}.json | Modify an existing product image |
| DELETE | /admin/api/2020-01/products/{product_id}/images/{image_id}.json | https://shopify.dev/docs/admin-api/rest/reference/products/product-image#destroy-2020-01 |
| GET | /admin/api/2020-04/products/{product_id}/images.json | Get all product images |
| POST | /admin/api/2020-04/products/{product_id}/images.json | Create a new product image |
| GET | /admin/api/2020-04/products/{product_id}/images/count.json | Get a count of all product images |
| GET | /admin/api/2020-04/products/{product_id}/images/{image_id}.json | Get a single product image by id |
| PUT | /admin/api/2020-04/products/{product_id}/images/{image_id}.json | Modify an existing product image |
| DELETE | /admin/api/2020-04/products/{product_id}/images/{image_id}.json | https://shopify.dev/docs/admin-api/rest/reference/products/product-image#destroy-2020-04 |
| GET | /admin/api/2020-07/products/{product_id}/images.json | Get all product images |
| POST | /admin/api/2020-07/products/{product_id}/images.json | Create a new product image |
| GET | /admin/api/2020-07/products/{product_id}/images/count.json | Get a count of all product images |
| GET | /admin/api/2020-07/products/{product_id}/images/{image_id}.json | Get a single product image by id |
| PUT | /admin/api/2020-07/products/{product_id}/images/{image_id}.json | Modify an existing product image |
| DELETE | /admin/api/2020-07/products/{product_id}/images/{image_id}.json | https://shopify.dev/docs/admin-api/rest/reference/products/product-image#destroy-2020-07 |
| GET | /admin/api/2020-10/products/{product_id}/images.json | Get all product images |
| POST | /admin/api/2020-10/products/{product_id}/images.json | Create a new product image |
| GET | /admin/api/2020-10/products/{product_id}/images/count.json | Get a count of all product images |
| GET | /admin/api/2020-10/products/{product_id}/images/{image_id}.json | Get a single product image by id |
| PUT | /admin/api/2020-10/products/{product_id}/images/{image_id}.json | Modify an existing product image |
| DELETE | /admin/api/2020-10/products/{product_id}/images/{image_id}.json | https://shopify.dev/docs/admin-api/rest/reference/products/product-image#destroy-2020-10 |
| GET | /admin/api/2021-01/products/{product_id}/images.json | Get all product images |
| POST | /admin/api/2021-01/products/{product_id}/images.json | Create a new product image |
| GET | /admin/api/2021-01/products/{product_id}/images/count.json | Get a count of all product images |
| GET | /admin/api/2021-01/products/{product_id}/images/{image_id}.json | Get a single product image by id |
| PUT | /admin/api/2021-01/products/{product_id}/images/{image_id}.json | Modify an existing product image |
| DELETE | /admin/api/2021-01/products/{product_id}/images/{image_id}.json | https://shopify.dev/docs/admin-api/rest/reference/products/product-image#destroy-2021-01 |
| GET | /admin/api/unstable/products/{product_id}/images.json | Get all product images |
| POST | /admin/api/unstable/products/{product_id}/images.json | Create a new product image |
| GET | /admin/api/unstable/products/{product_id}/images/count.json | Get a count of all product images |
| GET | /admin/api/unstable/products/{product_id}/images/{image_id}.json | Get a single product image by id |
| PUT | /admin/api/unstable/products/{product_id}/images/{image_id}.json | Modify an existing product image |
| DELETE | /admin/api/unstable/products/{product_id}/images/{image_id}.json | https://shopify.dev/docs/admin-api/rest/reference/products/product-image#destroy-unstable |
| GET | /admin/api/2020-01/smart_collections.json | Retrieves a list of smart collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/smart_collections.json | Creates a new smart collection using the specified rules. |
| GET | /admin/api/2020-01/smart_collections/count.json | Retrieves a count of smart collections |
| GET | /admin/api/2020-01/smart_collections/{smart_collection_id}.json | Retrieves a single smart collection |
| PUT | /admin/api/2020-01/smart_collections/{smart_collection_id}.json | Updates an existing smart collection |
| DELETE | /admin/api/2020-01/smart_collections/{smart_collection_id}.json | Removes a smart collection |
| PUT | /admin/api/2020-01/smart_collections/{smart_collection_id}/order.json | Updates the ordering type of products in a smart collection |
| GET | /admin/api/2020-04/smart_collections.json | Retrieves a list of smart collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/smart_collections.json | Creates a new smart collection using the specified rules. |
| GET | /admin/api/2020-04/smart_collections/count.json | Retrieves a count of smart collections |
| GET | /admin/api/2020-04/smart_collections/{smart_collection_id}.json | Retrieves a single smart collection |
| PUT | /admin/api/2020-04/smart_collections/{smart_collection_id}.json | Updates an existing smart collection |
| DELETE | /admin/api/2020-04/smart_collections/{smart_collection_id}.json | Removes a smart collection |
| PUT | /admin/api/2020-04/smart_collections/{smart_collection_id}/order.json | Updates the ordering type of products in a smart collection |
| GET | /admin/api/2020-07/smart_collections.json | Retrieves a list of smart collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/smart_collections.json | Creates a new smart collection using the specified rules. |
| GET | /admin/api/2020-07/smart_collections/count.json | Retrieves a count of smart collections |
| GET | /admin/api/2020-07/smart_collections/{smart_collection_id}.json | Retrieves a single smart collection |
| PUT | /admin/api/2020-07/smart_collections/{smart_collection_id}.json | Updates an existing smart collection |
| DELETE | /admin/api/2020-07/smart_collections/{smart_collection_id}.json | Removes a smart collection |
| PUT | /admin/api/2020-07/smart_collections/{smart_collection_id}/order.json | Updates the ordering type of products in a smart collection |
| GET | /admin/api/2020-10/smart_collections.json | Retrieves a list of smart collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/smart_collections.json | Creates a new smart collection using the specified rules. |
| GET | /admin/api/2020-10/smart_collections/count.json | Retrieves a count of smart collections |
| GET | /admin/api/2020-10/smart_collections/{smart_collection_id}.json | Retrieves a single smart collection |
| PUT | /admin/api/2020-10/smart_collections/{smart_collection_id}.json | Updates an existing smart collection |
| DELETE | /admin/api/2020-10/smart_collections/{smart_collection_id}.json | Removes a smart collection |
| PUT | /admin/api/2020-10/smart_collections/{smart_collection_id}/order.json | Updates the ordering type of products in a smart collection |
| GET | /admin/api/2021-01/smart_collections.json | Retrieves a list of smart collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/smart_collections.json | Creates a new smart collection using the specified rules. |
| GET | /admin/api/2021-01/smart_collections/count.json | Retrieves a count of smart collections |
| GET | /admin/api/2021-01/smart_collections/{smart_collection_id}.json | Retrieves a single smart collection |
| PUT | /admin/api/2021-01/smart_collections/{smart_collection_id}.json | Updates an existing smart collection |
| DELETE | /admin/api/2021-01/smart_collections/{smart_collection_id}.json | Removes a smart collection |
| PUT | /admin/api/2021-01/smart_collections/{smart_collection_id}/order.json | Updates the ordering type of products in a smart collection |
| GET | /admin/api/unstable/smart_collections.json | Retrieves a list of smart collections. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/smart_collections.json | Creates a new smart collection using the specified rules. |
| GET | /admin/api/unstable/smart_collections/count.json | Retrieves a count of smart collections |
| GET | /admin/api/unstable/smart_collections/{smart_collection_id}.json | Retrieves a single smart collection |
| PUT | /admin/api/unstable/smart_collections/{smart_collection_id}.json | Updates an existing smart collection |
| DELETE | /admin/api/unstable/smart_collections/{smart_collection_id}.json | Removes a smart collection |
| PUT | /admin/api/unstable/smart_collections/{smart_collection_id}/order.json | Updates the ordering type of products in a smart collection |
| POST | /admin/api/2020-01/checkouts/{token}/complete.json | Completes a checkout |
| GET | /admin/api/2020-01/checkouts/{token}.json | Retrieves a checkout |
| PUT | /admin/api/2020-01/checkouts/{token}.json | Modifies an existing checkout |
| GET | /admin/api/2020-01/checkouts/{token}/shipping_rates.json | Retrieves a list of available shipping rates for the specified checkout. Implementers need to poll this endpoint until rates become available. |
| POST | /admin/api/2020-04/checkouts/{token}/complete.json | Completes a checkout |
| GET | /admin/api/2020-04/checkouts/{token}.json | Retrieves a checkout |
| PUT | /admin/api/2020-04/checkouts/{token}.json | Modifies an existing checkout |
| GET | /admin/api/2020-04/checkouts/{token}/shipping_rates.json | Retrieves a list of available shipping rates for the specified checkout. Implementers need to poll this endpoint until rates become available. |
| POST | /admin/api/2020-07/checkouts/{token}/complete.json | Completes a checkout |
| GET | /admin/api/2020-07/checkouts/{token}.json | Retrieves a checkout |
| PUT | /admin/api/2020-07/checkouts/{token}.json | Modifies an existing checkout |
| GET | /admin/api/2020-07/checkouts/{token}/shipping_rates.json | Retrieves a list of available shipping rates for the specified checkout. Implementers need to poll this endpoint until rates become available. |
| POST | /admin/api/2020-10/checkouts/{token}/complete.json | Completes a checkout |
| GET | /admin/api/2020-10/checkouts/{token}.json | Retrieves a checkout |
| PUT | /admin/api/2020-10/checkouts/{token}.json | Modifies an existing checkout |
| GET | /admin/api/2020-10/checkouts/{token}/shipping_rates.json | Retrieves a list of available shipping rates for the specified checkout. Implementers need to poll this endpoint until rates become available. |
| POST | /admin/api/2021-01/checkouts/{token}/complete.json | Completes a checkout |
| GET | /admin/api/2021-01/checkouts/{token}.json | Retrieves a checkout |
| PUT | /admin/api/2021-01/checkouts/{token}.json | Modifies an existing checkout |
| GET | /admin/api/2021-01/checkouts/{token}/shipping_rates.json | Retrieves a list of available shipping rates for the specified checkout. Implementers need to poll this endpoint until rates become available. |
| POST | /admin/api/unstable/checkouts/{token}/complete.json | Completes a checkout |
| GET | /admin/api/unstable/checkouts/{token}.json | Retrieves a checkout |
| PUT | /admin/api/unstable/checkouts/{token}.json | Modifies an existing checkout |
| GET | /admin/api/unstable/checkouts/{token}/shipping_rates.json | Retrieves a list of available shipping rates for the specified checkout. Implementers need to poll this endpoint until rates become available. |
| GET | /admin/api/2020-01/collection_listings.json | Retrieve collection listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/collection_listings/{collection_listing_id}/product_ids.json | Retrieve product_ids that are published to a collection_id.       Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/collection_listings/{collection_listing_id}.json | Retrieve a specific collection listing that is published to your app |
| PUT | /admin/api/2020-01/collection_listings/{collection_listing_id}.json | Create a collection listing to publish a collection to your app |
| DELETE | /admin/api/2020-01/collection_listings/{collection_listing_id}.json | Delete a collection listing to unpublish a collection from your app |
| GET | /admin/api/2020-04/collection_listings.json | Retrieve collection listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/collection_listings/{collection_listing_id}/product_ids.json | Retrieve product_ids that are published to a collection_id.       Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/collection_listings/{collection_listing_id}.json | Retrieve a specific collection listing that is published to your app |
| PUT | /admin/api/2020-04/collection_listings/{collection_listing_id}.json | Create a collection listing to publish a collection to your app |
| DELETE | /admin/api/2020-04/collection_listings/{collection_listing_id}.json | Delete a collection listing to unpublish a collection from your app |
| GET | /admin/api/2020-07/collection_listings.json | Retrieve collection listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/collection_listings/{collection_listing_id}/product_ids.json | Retrieve product_ids that are published to a collection_id.       Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/collection_listings/{collection_listing_id}.json | Retrieve a specific collection listing that is published to your app |
| PUT | /admin/api/2020-07/collection_listings/{collection_listing_id}.json | Create a collection listing to publish a collection to your app |
| DELETE | /admin/api/2020-07/collection_listings/{collection_listing_id}.json | Delete a collection listing to unpublish a collection from your app |
| GET | /admin/api/2020-10/collection_listings.json | Retrieve collection listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/collection_listings/{collection_listing_id}/product_ids.json | Retrieve product_ids that are published to a collection_id.       Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/collection_listings/{collection_listing_id}.json | Retrieve a specific collection listing that is published to your app |
| PUT | /admin/api/2020-10/collection_listings/{collection_listing_id}.json | Create a collection listing to publish a collection to your app |
| DELETE | /admin/api/2020-10/collection_listings/{collection_listing_id}.json | Delete a collection listing to unpublish a collection from your app |
| GET | /admin/api/2021-01/collection_listings.json | Retrieve collection listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/collection_listings/{collection_listing_id}/product_ids.json | Retrieve product_ids that are published to a collection_id.       Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/collection_listings/{collection_listing_id}.json | Retrieve a specific collection listing that is published to your app |
| PUT | /admin/api/2021-01/collection_listings/{collection_listing_id}.json | Create a collection listing to publish a collection to your app |
| DELETE | /admin/api/2021-01/collection_listings/{collection_listing_id}.json | Delete a collection listing to unpublish a collection from your app |
| GET | /admin/api/unstable/collection_listings.json | Retrieve collection listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/collection_listings/{collection_listing_id}/product_ids.json | Retrieve product_ids that are published to a collection_id.       Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/collection_listings/{collection_listing_id}.json | Retrieve a specific collection listing that is published to your app |
| PUT | /admin/api/unstable/collection_listings/{collection_listing_id}.json | Create a collection listing to publish a collection to your app |
| DELETE | /admin/api/unstable/collection_listings/{collection_listing_id}.json | Delete a collection listing to unpublish a collection from your app |
| POST | /admin/api/2020-01/checkouts/{token}/payments.json | Creates a payment on a checkout using the session ID returned by the card vault |
| GET | /admin/api/2020-01/checkouts/{token}/payments.json | Retrieves a list of payments on a particular checkout |
| GET | /admin/api/2020-01/checkouts/{token}/payments/{payment_id}.json | Retrieves the payment information for an existing payment |
| GET | /admin/api/2020-01/checkouts/{token}/payments/count.json | Counts the number of payments attempted on a checkout |
| POST | /admin/api/2020-04/checkouts/{token}/payments.json | Creates a payment on a checkout using the session ID returned by the card vault |
| GET | /admin/api/2020-04/checkouts/{token}/payments.json | Retrieves a list of payments on a particular checkout |
| GET | /admin/api/2020-04/checkouts/{token}/payments/{payment_id}.json | Retrieves the payment information for an existing payment |
| GET | /admin/api/2020-04/checkouts/{token}/payments/count.json | Counts the number of payments attempted on a checkout |
| POST | /admin/api/2020-07/checkouts/{token}/payments.json | Creates a payment on a checkout using the session ID returned by the card vault |
| GET | /admin/api/2020-07/checkouts/{token}/payments.json | Retrieves a list of payments on a particular checkout |
| GET | /admin/api/2020-07/checkouts/{token}/payments/{payment_id}.json | Retrieves the payment information for an existing payment |
| GET | /admin/api/2020-07/checkouts/{token}/payments/count.json | Counts the number of payments attempted on a checkout |
| POST | /admin/api/2020-10/checkouts/{token}/payments.json | Creates a payment on a checkout using the session ID returned by the card vault |
| GET | /admin/api/2020-10/checkouts/{token}/payments.json | Retrieves a list of payments on a particular checkout |
| GET | /admin/api/2020-10/checkouts/{token}/payments/{payment_id}.json | Retrieves the payment information for an existing payment |
| GET | /admin/api/2020-10/checkouts/{token}/payments/count.json | Counts the number of payments attempted on a checkout |
| POST | /admin/api/2021-01/checkouts/{token}/payments.json | Creates a payment on a checkout using the session ID returned by the card vault |
| GET | /admin/api/2021-01/checkouts/{token}/payments.json | Retrieves a list of payments on a particular checkout |
| GET | /admin/api/2021-01/checkouts/{token}/payments/{payment_id}.json | Retrieves the payment information for an existing payment |
| GET | /admin/api/2021-01/checkouts/{token}/payments/count.json | Counts the number of payments attempted on a checkout |
| POST | /admin/api/unstable/checkouts/{token}/payments.json | Creates a payment on a checkout using the session ID returned by the card vault |
| GET | /admin/api/unstable/checkouts/{token}/payments.json | Retrieves a list of payments on a particular checkout |
| GET | /admin/api/unstable/checkouts/{token}/payments/{payment_id}.json | Retrieves the payment information for an existing payment |
| GET | /admin/api/unstable/checkouts/{token}/payments/count.json | Counts the number of payments attempted on a checkout |
| GET | /admin/api/2020-01/product_listings.json | Retrieve product listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-01/product_listings/product_ids.json | Retrieve product_ids that are published to your app. Maximum 1,000 results per page. |
| GET | /admin/api/2020-01/product_listings/count.json | Retrieve a count of products that are published to your app |
| GET | /admin/api/2020-01/product_listings/{product_listing_id}.json | Retrieve a specific product listing that is published to your app |
| PUT | /admin/api/2020-01/product_listings/{product_listing_id}.json | Create a product listing to publish a product to your app |
| DELETE | /admin/api/2020-01/product_listings/{product_listing_id}.json | Delete a product listing to unpublish a product from your app |
| GET | /admin/api/2020-04/product_listings.json | Retrieve product listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/product_listings/product_ids.json | Retrieve product_ids that are published to your app. Maximum 1,000 results per page. |
| GET | /admin/api/2020-04/product_listings/count.json | Retrieve a count of products that are published to your app |
| GET | /admin/api/2020-04/product_listings/{product_listing_id}.json | Retrieve a specific product listing that is published to your app |
| PUT | /admin/api/2020-04/product_listings/{product_listing_id}.json | Create a product listing to publish a product to your app |
| DELETE | /admin/api/2020-04/product_listings/{product_listing_id}.json | Delete a product listing to unpublish a product from your app |
| GET | /admin/api/2020-07/product_listings.json | Retrieve product listings that are published to your app. Note: As of version 2019-07, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/product_listings/product_ids.json | Retrieve product_ids that are published to your app. Maximum 1,000 results per page. |
| GET | /admin/api/2020-07/product_listings/count.json | Retrieve a count of products that are published to your app |
| GET | /admin/api/2020-07/product_listings/{product_listing_id}.json | Retrieve a specific product listing that is published to your app |
| PUT | /admin/api/2020-07/product_listings/{product_listing_id}.json | Create a product listing to publish a product to your app |
| DELETE | /admin/api/2020-07/product_listings/{product_listing_id}.json | Delete a product listing to unpublish a product from your app |
| GET | /admin/api/2020-01/assigned_fulfillment_orders.json | Retrieves a list of fulfillment orders on a shop for a specific app. |
| GET | /admin/api/2020-04/assigned_fulfillment_orders.json | Retrieves a list of fulfillment orders on a shop for a specific app. |
| GET | /admin/api/2020-07/assigned_fulfillment_orders.json | Retrieves a list of fulfillment orders on a shop for a specific app. |
| GET | /admin/api/2020-10/assigned_fulfillment_orders.json | Retrieves a list of fulfillment orders on a shop for a specific app. |
| GET | /admin/api/2021-01/assigned_fulfillment_orders.json | Retrieves a list of fulfillment orders on a shop for a specific app. |
| GET | /admin/api/unstable/assigned_fulfillment_orders.json | Retrieves a list of fulfillment orders on a shop for a specific app. |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json | Sends a cancellation request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json | Accepts a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json | Rejects a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json | Sends a cancellation request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json | Accepts a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json | Rejects a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json | Sends a cancellation request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json | Accepts a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json | Rejects a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json | Sends a cancellation request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json | Accepts a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json | Rejects a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json | Sends a cancellation request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json | Accepts a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json | Rejects a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json | Sends a cancellation request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json | Accepts a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json | Rejects a cancellation request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-01/carrier_services.json | Creates a carrier service |
| GET | /admin/api/2020-01/carrier_services.json | Retrieves a list of carrier services |
| PUT | /admin/api/2020-01/carrier_services/{carrier_service_id}.json | Updates a carrier service. Only the app that creates a carrier service can update it. |
| GET | /admin/api/2020-01/carrier_services/{carrier_service_id}.json | Retrieves a single carrier service by its ID |
| DELETE | /admin/api/2020-01/carrier_services/{carrier_service_id}.json | Deletes a carrier service |
| POST | /admin/api/2020-04/carrier_services.json | Creates a carrier service |
| GET | /admin/api/2020-04/carrier_services.json | Retrieves a list of carrier services |
| PUT | /admin/api/2020-04/carrier_services/{carrier_service_id}.json | Updates a carrier service. Only the app that creates a carrier service can update it. |
| GET | /admin/api/2020-04/carrier_services/{carrier_service_id}.json | Retrieves a single carrier service by its ID |
| DELETE | /admin/api/2020-04/carrier_services/{carrier_service_id}.json | Deletes a carrier service |
| POST | /admin/api/2020-07/carrier_services.json | Creates a carrier service |
| GET | /admin/api/2020-07/carrier_services.json | Retrieves a list of carrier services |
| PUT | /admin/api/2020-07/carrier_services/{carrier_service_id}.json | Updates a carrier service. Only the app that creates a carrier service can update it. |
| GET | /admin/api/2020-07/carrier_services/{carrier_service_id}.json | Retrieves a single carrier service by its ID |
| DELETE | /admin/api/2020-07/carrier_services/{carrier_service_id}.json | Deletes a carrier service |
| POST | /admin/api/2020-10/carrier_services.json | Creates a carrier service |
| GET | /admin/api/2020-10/carrier_services.json | Retrieves a list of carrier services |
| PUT | /admin/api/2020-10/carrier_services/{carrier_service_id}.json | Updates a carrier service. Only the app that creates a carrier service can update it. |
| GET | /admin/api/2020-10/carrier_services/{carrier_service_id}.json | Retrieves a single carrier service by its ID |
| DELETE | /admin/api/2020-10/carrier_services/{carrier_service_id}.json | Deletes a carrier service |
| POST | /admin/api/2021-01/carrier_services.json | Creates a carrier service |
| GET | /admin/api/2021-01/carrier_services.json | Retrieves a list of carrier services |
| PUT | /admin/api/2021-01/carrier_services/{carrier_service_id}.json | Updates a carrier service. Only the app that creates a carrier service can update it. |
| GET | /admin/api/2021-01/carrier_services/{carrier_service_id}.json | Retrieves a single carrier service by its ID |
| DELETE | /admin/api/2021-01/carrier_services/{carrier_service_id}.json | Deletes a carrier service |
| POST | /admin/api/unstable/carrier_services.json | Creates a carrier service |
| GET | /admin/api/unstable/carrier_services.json | Retrieves a list of carrier services |
| PUT | /admin/api/unstable/carrier_services/{carrier_service_id}.json | Updates a carrier service. Only the app that creates a carrier service can update it. |
| GET | /admin/api/unstable/carrier_services/{carrier_service_id}.json | Retrieves a single carrier service by its ID |
| DELETE | /admin/api/unstable/carrier_services/{carrier_service_id}.json | Deletes a carrier service |
| GET | /admin/api/2020-01/orders/{order_id}/fulfillments.json | Retrieves fulfillments associated with an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-01/orders/{order_id}/fulfillments.json | Create a fulfillment for the specified order and line items. |
| GET | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/fulfillments.json | Retrieves fulfillments associated with a fulfillment order. |
| GET | /admin/api/2020-01/orders/{order_id}/fulfillments/count.json | Retrieves a count of fulfillments associated with a specific order |
| GET | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}.json | Retrieve a specific fulfillment |
| PUT | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}.json | Update information associated with a fulfillment |
| POST | /admin/api/2020-01/fulfillments.json | Creates a fulfillment for one or many fulfillment orders. The fulfillment orders are associated with the same order and are assigned to the same location. |
| POST | /admin/api/2020-01/fulfillments/{fulfillment_id}/update_tracking.json | Updates the tracking information for a fulfillment. |
| POST | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json | Mark a fulfillment as complete |
| POST | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/open.json | Mark a fulfillment as open |
| POST | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json | Cancel a fulfillment for a specific order ID |
| POST | /admin/api/2020-01/fulfillments/{fulfillment_id}/cancel.json | Cancels a fulfillment. |
| GET | /admin/api/2020-04/orders/{order_id}/fulfillments.json | Retrieves fulfillments associated with an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-04/orders/{order_id}/fulfillments.json | Create a fulfillment for the specified order and line items. |
| GET | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/fulfillments.json | Retrieves fulfillments associated with a fulfillment order. |
| GET | /admin/api/2020-04/orders/{order_id}/fulfillments/count.json | Retrieves a count of fulfillments associated with a specific order |
| GET | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}.json | Retrieve a specific fulfillment |
| PUT | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}.json | Update information associated with a fulfillment |
| POST | /admin/api/2020-04/fulfillments.json | Creates a fulfillment for one or many fulfillment orders. The fulfillment orders are associated with the same order and are assigned to the same location. |
| POST | /admin/api/2020-04/fulfillments/{fulfillment_id}/update_tracking.json | Updates the tracking information for a fulfillment. |
| POST | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json | Mark a fulfillment as complete |
| POST | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/open.json | Mark a fulfillment as open |
| POST | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json | Cancel a fulfillment for a specific order ID |
| POST | /admin/api/2020-04/fulfillments/{fulfillment_id}/cancel.json | Cancels a fulfillment. |
| GET | /admin/api/2020-07/orders/{order_id}/fulfillments.json | Retrieves fulfillments associated with an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-07/orders/{order_id}/fulfillments.json | Create a fulfillment for the specified order and line items. |
| GET | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/fulfillments.json | Retrieves fulfillments associated with a fulfillment order. |
| GET | /admin/api/2020-07/orders/{order_id}/fulfillments/count.json | Retrieves a count of fulfillments associated with a specific order |
| GET | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}.json | Retrieve a specific fulfillment |
| PUT | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}.json | Update information associated with a fulfillment |
| POST | /admin/api/2020-07/fulfillments.json | Creates a fulfillment for one or many fulfillment orders. The fulfillment orders are associated with the same order and are assigned to the same location. |
| POST | /admin/api/2020-07/fulfillments/{fulfillment_id}/update_tracking.json | Updates the tracking information for a fulfillment. |
| POST | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json | Mark a fulfillment as complete |
| POST | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/open.json | Mark a fulfillment as open |
| POST | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json | Cancel a fulfillment for a specific order ID |
| POST | /admin/api/2020-07/fulfillments/{fulfillment_id}/cancel.json | Cancels a fulfillment. |
| GET | /admin/api/2020-10/orders/{order_id}/fulfillments.json | Retrieves fulfillments associated with an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2020-10/orders/{order_id}/fulfillments.json | Create a fulfillment for the specified order and line items. |
| GET | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/fulfillments.json | Retrieves fulfillments associated with a fulfillment order. |
| GET | /admin/api/2020-10/orders/{order_id}/fulfillments/count.json | Retrieves a count of fulfillments associated with a specific order |
| GET | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}.json | Retrieve a specific fulfillment |
| PUT | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}.json | Update information associated with a fulfillment |
| POST | /admin/api/2020-10/fulfillments.json | Creates a fulfillment for one or many fulfillment orders. The fulfillment orders are associated with the same order and are assigned to the same location. |
| POST | /admin/api/2020-10/fulfillments/{fulfillment_id}/update_tracking.json | Updates the tracking information for a fulfillment. |
| POST | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json | Mark a fulfillment as complete |
| POST | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/open.json | Mark a fulfillment as open |
| POST | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json | Cancel a fulfillment for a specific order ID |
| POST | /admin/api/2020-10/fulfillments/{fulfillment_id}/cancel.json | Cancels a fulfillment. |
| GET | /admin/api/2021-01/orders/{order_id}/fulfillments.json | Retrieves fulfillments associated with an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/2021-01/orders/{order_id}/fulfillments.json | Create a fulfillment for the specified order and line items. |
| GET | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/fulfillments.json | Retrieves fulfillments associated with a fulfillment order. |
| GET | /admin/api/2021-01/orders/{order_id}/fulfillments/count.json | Retrieves a count of fulfillments associated with a specific order |
| GET | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}.json | Retrieve a specific fulfillment |
| PUT | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}.json | Update information associated with a fulfillment |
| POST | /admin/api/2021-01/fulfillments.json | Creates a fulfillment for one or many fulfillment orders. The fulfillment orders are associated with the same order and are assigned to the same location. |
| POST | /admin/api/2021-01/fulfillments/{fulfillment_id}/update_tracking.json | Updates the tracking information for a fulfillment. |
| POST | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json | Mark a fulfillment as complete |
| POST | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/open.json | Mark a fulfillment as open |
| POST | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json | Cancel a fulfillment for a specific order ID |
| POST | /admin/api/2021-01/fulfillments/{fulfillment_id}/cancel.json | Cancels a fulfillment. |
| GET | /admin/api/unstable/orders/{order_id}/fulfillments.json | Retrieves fulfillments associated with an order. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. Sending the page parameter will return an error. To learn more, see Making requests to paginated REST Admin API endpoints. |
| POST | /admin/api/unstable/orders/{order_id}/fulfillments.json | Create a fulfillment for the specified order and line items. |
| GET | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/fulfillments.json | Retrieves fulfillments associated with a fulfillment order. |
| GET | /admin/api/unstable/orders/{order_id}/fulfillments/count.json | Retrieves a count of fulfillments associated with a specific order |
| GET | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}.json | Retrieve a specific fulfillment |
| PUT | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}.json | Update information associated with a fulfillment |
| POST | /admin/api/unstable/fulfillments.json | Creates a fulfillment for one or many fulfillment orders. The fulfillment orders are associated with the same order and are assigned to the same location. |
| POST | /admin/api/unstable/fulfillments/{fulfillment_id}/update_tracking.json | Updates the tracking information for a fulfillment. |
| POST | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json | Mark a fulfillment as complete |
| POST | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/open.json | Mark a fulfillment as open |
| POST | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json | Cancel a fulfillment for a specific order ID |
| POST | /admin/api/unstable/fulfillments/{fulfillment_id}/cancel.json | Cancels a fulfillment. |
| GET | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Retrieves a list of fulfillment events for a specific fulfillment |
| POST | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Creates a fulfillment event |
| GET | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Retrieves a specific fulfillment event |
| DELETE | /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Deletes a fulfillment event |
| GET | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Retrieves a list of fulfillment events for a specific fulfillment |
| POST | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Creates a fulfillment event |
| GET | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Retrieves a specific fulfillment event |
| DELETE | /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Deletes a fulfillment event |
| GET | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Retrieves a list of fulfillment events for a specific fulfillment |
| POST | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Creates a fulfillment event |
| GET | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Retrieves a specific fulfillment event |
| DELETE | /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Deletes a fulfillment event |
| GET | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Retrieves a list of fulfillment events for a specific fulfillment |
| POST | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Creates a fulfillment event |
| GET | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Retrieves a specific fulfillment event |
| DELETE | /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Deletes a fulfillment event |
| GET | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Retrieves a list of fulfillment events for a specific fulfillment |
| POST | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Creates a fulfillment event |
| GET | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Retrieves a specific fulfillment event |
| DELETE | /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Deletes a fulfillment event |
| GET | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Retrieves a list of fulfillment events for a specific fulfillment |
| POST | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/events.json | Creates a fulfillment event |
| GET | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Retrieves a specific fulfillment event |
| DELETE | /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json | Deletes a fulfillment event |
| GET | /admin/api/2020-01/orders/{order_id}/fulfillment_orders.json | Retrieves a list of fulfillment orders for a specific order. |
| GET | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}.json | Retrieves a specific fulfillment order. |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/cancel.json | Marks a fulfillment order as cancelled. |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/close.json | Marks an in progress fulfillment order as incomplete, indicating the fulfillment service |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/move.json | Moves a fulfillment order from one merchant managed location to another merchant managed location. |
| GET | /admin/api/2020-04/orders/{order_id}/fulfillment_orders.json | Retrieves a list of fulfillment orders for a specific order. |
| GET | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}.json | Retrieves a specific fulfillment order. |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/cancel.json | Marks a fulfillment order as cancelled. |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/close.json | Marks an in progress fulfillment order as incomplete, indicating the fulfillment service |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/move.json | Moves a fulfillment order from one merchant managed location to another merchant managed location. |
| GET | /admin/api/2020-07/orders/{order_id}/fulfillment_orders.json | Retrieves a list of fulfillment orders for a specific order. |
| GET | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}.json | Retrieves a specific fulfillment order. |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/cancel.json | Marks a fulfillment order as cancelled. |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/close.json | Marks an in progress fulfillment order as incomplete, indicating the fulfillment service |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/move.json | Moves a fulfillment order from one merchant managed location to another merchant managed location. |
| GET | /admin/api/2020-10/orders/{order_id}/fulfillment_orders.json | Retrieves a list of fulfillment orders for a specific order. |
| GET | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}.json | Retrieves a specific fulfillment order. |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/cancel.json | Marks a fulfillment order as cancelled. |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/close.json | Marks an in progress fulfillment order as incomplete, indicating the fulfillment service |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/move.json | Moves a fulfillment order from one merchant managed location to another merchant managed location. |
| GET | /admin/api/2021-01/orders/{order_id}/fulfillment_orders.json | Retrieves a list of fulfillment orders for a specific order. |
| GET | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}.json | Retrieves a specific fulfillment order. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/cancel.json | Marks a fulfillment order as cancelled. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/close.json | Marks an in progress fulfillment order as incomplete, indicating the fulfillment service |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/move.json | Moves a fulfillment order from one merchant managed location to another merchant managed location. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/open.json | Marks a scheduled fulfillment order as ready for fulfillment. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/reschedule.json | Updates the fulfill_at time of a scheduled fulfillment order. |
| GET | /admin/api/unstable/orders/{order_id}/fulfillment_orders.json | Retrieves a list of fulfillment orders for a specific order. |
| GET | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}.json | Retrieves a specific fulfillment order. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/cancel.json | Marks a fulfillment order as cancelled. |
| POST | /admin/api/unstable/fulfillment_orders/release_hold.json | Releases the fulfillment order holds for a specific order. Fulfillment orders are created |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/close.json | Marks an in progress fulfillment order as incomplete, indicating the fulfillment service |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/move.json | Moves a fulfillment order from one merchant managed location to another merchant managed location. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/open.json | Marks a scheduled fulfillment order as ready for fulfillment. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/reschedule.json | Updates the fulfill_at time of a scheduled fulfillment order. |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json | Sends a fulfillment request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json | Accepts a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json | Rejects a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json | Sends a fulfillment request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json | Accepts a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json | Rejects a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json | Sends a fulfillment request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json | Accepts a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json | Rejects a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json | Sends a fulfillment request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json | Accepts a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json | Rejects a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json | Sends a fulfillment request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json | Accepts a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json | Rejects a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json | Sends a fulfillment request to the fulfillment service of a fulfillment order. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json | Accepts a fulfillment request sent to a fulfillment service for a fulfillment order. |
| POST | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json | Rejects a fulfillment request sent to a fulfillment service for a fulfillment order. |
| GET | /admin/api/2020-01/fulfillment_services.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#index-2020-01 |
| POST | /admin/api/2020-01/fulfillment_services.json | To create a fulfillment service, you can also use a cURL request that uses that fulfillment_service.json payload: |
| GET | /admin/api/2020-01/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#show-2020-01 |
| PUT | /admin/api/2020-01/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#update-2020-01 |
| DELETE | /admin/api/2020-01/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#destroy-2020-01 |
| GET | /admin/api/2020-04/fulfillment_services.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#index-2020-04 |
| POST | /admin/api/2020-04/fulfillment_services.json | To create a fulfillment service, you can also use a cURL request that uses that fulfillment_service.json payload: |
| GET | /admin/api/2020-04/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#show-2020-04 |
| PUT | /admin/api/2020-04/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#update-2020-04 |
| DELETE | /admin/api/2020-04/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#destroy-2020-04 |
| GET | /admin/api/2020-07/fulfillment_services.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#index-2020-07 |
| POST | /admin/api/2020-07/fulfillment_services.json | To create a fulfillment service, you can also use a cURL request that uses that fulfillment_service.json payload: |
| GET | /admin/api/2020-07/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#show-2020-07 |
| PUT | /admin/api/2020-07/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#update-2020-07 |
| DELETE | /admin/api/2020-07/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#destroy-2020-07 |
| GET | /admin/api/2020-10/fulfillment_services.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#index-2020-10 |
| POST | /admin/api/2020-10/fulfillment_services.json | To create a fulfillment service, you can also use a cURL request that uses that fulfillment_service.json payload: |
| GET | /admin/api/2020-10/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#show-2020-10 |
| PUT | /admin/api/2020-10/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#update-2020-10 |
| DELETE | /admin/api/2020-10/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#destroy-2020-10 |
| GET | /admin/api/2021-01/fulfillment_services.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#index-2021-01 |
| POST | /admin/api/2021-01/fulfillment_services.json | To create a fulfillment service, you can also use a cURL request that uses that fulfillment_service.json payload: |
| GET | /admin/api/2021-01/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#show-2021-01 |
| PUT | /admin/api/2021-01/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#update-2021-01 |
| DELETE | /admin/api/2021-01/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#destroy-2021-01 |
| GET | /admin/api/unstable/fulfillment_services.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#index-unstable |
| POST | /admin/api/unstable/fulfillment_services.json | To create a fulfillment service, you can also use a cURL request that uses that fulfillment_service.json payload: |
| GET | /admin/api/unstable/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#show-unstable |
| PUT | /admin/api/unstable/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#update-unstable |
| DELETE | /admin/api/unstable/fulfillment_services/{fulfillment_service_id}.json | https://shopify.dev/docs/admin-api/rest/reference/shipping-and-fulfillment/fulfillmentservice#destroy-unstable |
| GET | /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json | Retrieves a list of locations that a fulfillment order can potentially move to. |
| GET | /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json | Retrieves a list of locations that a fulfillment order can potentially move to. |
| GET | /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json | Retrieves a list of locations that a fulfillment order can potentially move to. |
| GET | /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json | Retrieves a list of locations that a fulfillment order can potentially move to. |
| GET | /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json | Retrieves a list of locations that a fulfillment order can potentially move to. |
| GET | /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json | Retrieves a list of locations that a fulfillment order can potentially move to. |
| GET | /admin/api/2020-01/shopify_payments/balance.json | Retrieves the account's current balance. |
| GET | /admin/api/2020-04/shopify_payments/balance.json | Retrieves the account's current balance. |
| GET | /admin/api/2020-07/shopify_payments/balance.json | Retrieves the account's current balance. |
| GET | /admin/api/2020-10/shopify_payments/balance.json | Retrieves the account's current balance. |
| GET | /admin/api/2021-01/shopify_payments/balance.json | Retrieves the account's current balance. |
| GET | /admin/api/unstable/shopify_payments/balance.json | Retrieves the account's current balance. |
| GET | /admin/api/2020-01/shopify_payments/disputes.json | Retrieve all disputes ordered by initiated_at date and time (ISO 8601 format), with the most recent being first. |
| GET | /admin/api/2020-01/shopify_payments/disputes/{dispute_id}.json | Retrieves a single dispute by ID. |
| GET | /admin/api/2020-04/shopify_payments/disputes.json | Retrieve all disputes ordered by initiated_at date and time (ISO 8601 format), with the most recent being first. |
| GET | /admin/api/2020-01/shopify_payments/payouts.json | Retrieves a list of all payouts ordered by payout date, with the most recent being first. |
| GET | /admin/api/2020-01/shopify_payments/payouts/{payout_id}.json | Retrieves a single payout by id. |
| GET | /admin/api/2020-04/shopify_payments/payouts.json | Retrieves a list of all payouts ordered by payout date, with the most recent being first. |
| GET | /admin/api/2020-04/shopify_payments/payouts/{payout_id}.json | Retrieves a single payout by id. |
| GET | /admin/api/2020-07/shopify_payments/payouts.json | Retrieves a list of all payouts ordered by payout date, with the most recent being first. |
| GET | /admin/api/2020-07/shopify_payments/payouts/{payout_id}.json | Retrieves a single payout by id. |
| GET | /admin/api/2020-10/shopify_payments/payouts.json | Retrieves a list of all payouts ordered by payout date, with the most recent being first. |
| GET | /admin/api/2020-10/shopify_payments/payouts/{payout_id}.json | Retrieves a single payout by id. |
| GET | /admin/api/2021-01/shopify_payments/payouts.json | Retrieves a list of all payouts ordered by payout date, with the most recent being first. |
| GET | /admin/api/2021-01/shopify_payments/payouts/{payout_id}.json | Retrieves a single payout by id. |
| GET | /admin/api/unstable/shopify_payments/payouts.json | Retrieves a list of all payouts ordered by payout date, with the most recent being first. |
| GET | /admin/api/unstable/shopify_payments/payouts/{payout_id}.json | Retrieves a single payout by id. |
| GET | /admin/api/2020-01/shopify_payments/balance/transactions.json | Retrieves a list of all balance transactions ordered by processing |
| GET | /admin/api/2020-01/countries.json | Retrieves a list of countries. |
| POST | /admin/api/2020-01/countries.json | Caution |
| GET | /admin/api/2020-01/countries/count.json | Retrieves a count of countries. |
| GET | /admin/api/2020-01/countries/{country_id}.json | Retrieves a specific county. |
| PUT | /admin/api/2020-01/countries/{country_id}.json | Caution |
| DELETE | /admin/api/2020-01/countries/{country_id}.json | Deletes a country. |
| GET | /admin/api/2020-04/countries.json | Retrieves a list of countries. |
| POST | /admin/api/2020-04/countries.json | Caution |
| GET | /admin/api/2020-04/countries/count.json | Retrieves a count of countries. |
| GET | /admin/api/2020-04/countries/{country_id}.json | Retrieves a specific county. |
| PUT | /admin/api/2020-04/countries/{country_id}.json | Caution |
| DELETE | /admin/api/2020-04/countries/{country_id}.json | Deletes a country. |
| GET | /admin/api/2020-07/countries.json | Retrieves a list of countries. |
| POST | /admin/api/2020-07/countries.json | Caution |
| GET | /admin/api/2020-07/countries/count.json | Retrieves a count of countries. |
| GET | /admin/api/2020-07/countries/{country_id}.json | Retrieves a specific county. |
| PUT | /admin/api/2020-07/countries/{country_id}.json | Caution |
| DELETE | /admin/api/2020-07/countries/{country_id}.json | Deletes a country. |
| GET | /admin/api/2020-10/countries.json | Retrieves a list of countries. |
| POST | /admin/api/2020-10/countries.json | Caution |
| GET | /admin/api/2020-10/countries/count.json | Retrieves a count of countries. |
| GET | /admin/api/2020-10/countries/{country_id}.json | Retrieves a specific county. |
| PUT | /admin/api/2020-10/countries/{country_id}.json | Caution |
| DELETE | /admin/api/2020-10/countries/{country_id}.json | Deletes a country. |
| GET | /admin/api/2021-01/countries.json | Retrieves a list of countries. |
| POST | /admin/api/2021-01/countries.json | Caution |
| GET | /admin/api/2021-01/countries/count.json | Retrieves a count of countries. |
| GET | /admin/api/2021-01/countries/{country_id}.json | Retrieves a specific county. |
| PUT | /admin/api/2021-01/countries/{country_id}.json | Caution |
| DELETE | /admin/api/2021-01/countries/{country_id}.json | Deletes a country. |
| GET | /admin/api/unstable/countries.json | Retrieves a list of countries. |
| POST | /admin/api/unstable/countries.json | Caution |
| GET | /admin/api/unstable/countries/count.json | Retrieves a count of countries. |
| GET | /admin/api/unstable/countries/{country_id}.json | Retrieves a specific county. |
| PUT | /admin/api/unstable/countries/{country_id}.json | Caution |
| DELETE | /admin/api/unstable/countries/{country_id}.json | Deletes a country. |
| GET | /admin/api/2020-01/currencies.json | Retrieves a list of currencies enabled on a shop |
| GET | /admin/api/2020-04/currencies.json | Retrieves a list of currencies enabled on a shop |
| GET | /admin/api/2020-07/currencies.json | Retrieves a list of currencies enabled on a shop |
| GET | /admin/api/2020-10/currencies.json | Retrieves a list of currencies enabled on a shop |
| GET | /admin/api/2021-01/currencies.json | Retrieves a list of currencies enabled on a shop |
| GET | /admin/api/unstable/currencies.json | Retrieves a list of currencies enabled on a shop |
| GET | /admin/api/2020-01/policies.json | Retrieves a list of the shop's policies |
| GET | /admin/api/2020-04/policies.json | Retrieves a list of the shop's policies |
| GET | /admin/api/2020-07/policies.json | Retrieves a list of the shop's policies |
| GET | /admin/api/2020-10/policies.json | Retrieves a list of the shop's policies |
| GET | /admin/api/2021-01/policies.json | Retrieves a list of the shop's policies |
| GET | /admin/api/unstable/policies.json | Retrieves a list of the shop's policies |
| GET | /admin/api/2020-01/countries/{country_id}/provinces.json | Retrieves a list of provinces |
| GET | /admin/api/2020-01/countries/{country_id}/provinces/count.json | Retrieves a count of provinces for a country |
| GET | /admin/api/2020-01/countries/{country_id}/provinces/{province_id}.json | Retrieves a single province for a country |
| PUT | /admin/api/2020-01/countries/{country_id}/provinces/{province_id}.json | Caution |
| GET | /admin/api/2020-04/countries/{country_id}/provinces.json | Retrieves a list of provinces |
| GET | /admin/api/2020-04/countries/{country_id}/provinces/count.json | Retrieves a count of provinces for a country |
| GET | /admin/api/2020-04/countries/{country_id}/provinces/{province_id}.json | Retrieves a single province for a country |
| PUT | /admin/api/2020-04/countries/{country_id}/provinces/{province_id}.json | Caution |
| GET | /admin/api/2020-07/countries/{country_id}/provinces.json | Retrieves a list of provinces |
| GET | /admin/api/2020-07/countries/{country_id}/provinces/count.json | Retrieves a count of provinces for a country |
| GET | /admin/api/2020-07/countries/{country_id}/provinces/{province_id}.json | Retrieves a single province for a country |
| PUT | /admin/api/2020-07/countries/{country_id}/provinces/{province_id}.json | Caution |
| GET | /admin/api/2020-10/countries/{country_id}/provinces.json | Retrieves a list of provinces |
| GET | /admin/api/2020-10/countries/{country_id}/provinces/count.json | Retrieves a count of provinces for a country |
| GET | /admin/api/2020-10/countries/{country_id}/provinces/{province_id}.json | Retrieves a single province for a country |
| PUT | /admin/api/2020-10/countries/{country_id}/provinces/{province_id}.json | Caution |
| GET | /admin/api/2021-01/countries/{country_id}/provinces.json | Retrieves a list of provinces |
| GET | /admin/api/2021-01/countries/{country_id}/provinces/count.json | Retrieves a count of provinces for a country |
| GET | /admin/api/2021-01/countries/{country_id}/provinces/{province_id}.json | Retrieves a single province for a country |
| PUT | /admin/api/2021-01/countries/{country_id}/provinces/{province_id}.json | Caution |
| GET | /admin/api/unstable/countries/{country_id}/provinces.json | Retrieves a list of provinces |
| GET | /admin/api/unstable/countries/{country_id}/provinces/count.json | Retrieves a count of provinces for a country |
| GET | /admin/api/unstable/countries/{country_id}/provinces/{province_id}.json | Retrieves a single province for a country |
| PUT | /admin/api/unstable/countries/{country_id}/provinces/{province_id}.json | Caution |
| GET | /admin/api/2020-01/shipping_zones.json | Get a list of all shipping zones |
| GET | /admin/api/2020-04/shipping_zones.json | Get a list of all shipping zones |
| GET | /admin/api/2020-07/shipping_zones.json | Get a list of all shipping zones |
| GET | /admin/api/2020-10/shipping_zones.json | Get a list of all shipping zones |
| GET | /admin/api/2021-01/shipping_zones.json | Get a list of all shipping zones |
| GET | /admin/api/unstable/shipping_zones.json | Get a list of all shipping zones |
| GET | /admin/api/2020-01/shop.json | Retrieves the shop's configuration |
| GET | /admin/api/2020-04/shop.json | Retrieves the shop's configuration |
| GET | /admin/api/2020-07/shop.json | Retrieves the shop's configuration |
| GET | /admin/api/2020-10/shop.json | Retrieves the shop's configuration |
| GET | /admin/api/2021-01/shop.json | Retrieves the shop's configuration |
| GET | /admin/api/unstable/shop.json | Retrieves the shop's configuration |
| GET | /admin/api/2020-01/tender_transactions.json | Retrieves a list of tender transactions. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-04/tender_transactions.json | Retrieves a list of tender transactions. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-07/tender_transactions.json | Retrieves a list of tender transactions. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2020-10/tender_transactions.json | Retrieves a list of tender transactions. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/2021-01/tender_transactions.json | Retrieves a list of tender transactions. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |
| GET | /admin/api/unstable/tender_transactions.json | Retrieves a list of tender transactions. Note: As of version 2019-10, this endpoint implements pagination by using links that are provided in the response header. To learn more, see Making requests to paginated REST Admin API endpoints. |

### fetch_tracking_numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /fetch_tracking_numbers | Get tracking numbers for orders |

### fetch_stock
| Method | Path | Description |
|--------|------|-------------|
| GET | /fetch_stock | Get inventory levels |

## Common Questions

Match user requests to endpoints in references/api-spec.lap. Key patterns:
- "List all access_scopes.json?" -> GET /admin/oauth/access_scopes.json
- "Create a storefront_access_tokens.json?" -> POST /admin/api/2020-01/storefront_access_tokens.json
- "List all storefront_access_tokens.json?" -> GET /admin/api/2020-01/storefront_access_tokens.json
- "Delete a storefront_access_token?" -> DELETE /admin/api/2020-01/storefront_access_tokens/{storefront_access_token_id}.json
- "Create a storefront_access_tokens.json?" -> POST /admin/api/2020-04/storefront_access_tokens.json
- "List all storefront_access_tokens.json?" -> GET /admin/api/2020-04/storefront_access_tokens.json
- "Delete a storefront_access_token?" -> DELETE /admin/api/2020-04/storefront_access_tokens/{storefront_access_token_id}.json
- "Create a storefront_access_tokens.json?" -> POST /admin/api/2020-07/storefront_access_tokens.json
- "List all storefront_access_tokens.json?" -> GET /admin/api/2020-07/storefront_access_tokens.json
- "Delete a storefront_access_token?" -> DELETE /admin/api/2020-07/storefront_access_tokens/{storefront_access_token_id}.json
- "Create a storefront_access_tokens.json?" -> POST /admin/api/2020-10/storefront_access_tokens.json
- "List all storefront_access_tokens.json?" -> GET /admin/api/2020-10/storefront_access_tokens.json
- "Delete a storefront_access_token?" -> DELETE /admin/api/2020-10/storefront_access_tokens/{storefront_access_token_id}.json
- "Create a storefront_access_tokens.json?" -> POST /admin/api/2021-01/storefront_access_tokens.json
- "List all storefront_access_tokens.json?" -> GET /admin/api/2021-01/storefront_access_tokens.json
- "Delete a storefront_access_token?" -> DELETE /admin/api/2021-01/storefront_access_tokens/{storefront_access_token_id}.json
- "Create a storefront_access_tokens.json?" -> POST /admin/api/unstable/storefront_access_tokens.json
- "List all storefront_access_tokens.json?" -> GET /admin/api/unstable/storefront_access_tokens.json
- "Delete a storefront_access_token?" -> DELETE /admin/api/unstable/storefront_access_tokens/{storefront_access_token_id}.json
- "List all reports.json?" -> GET /admin/api/2020-01/reports.json
- "Create a reports.json?" -> POST /admin/api/2020-01/reports.json
- "Get report details?" -> GET /admin/api/2020-01/reports/{report_id}.json
- "Update a report?" -> PUT /admin/api/2020-01/reports/{report_id}.json
- "Delete a report?" -> DELETE /admin/api/2020-01/reports/{report_id}.json
- "List all reports.json?" -> GET /admin/api/2020-04/reports.json
- "Create a reports.json?" -> POST /admin/api/2020-04/reports.json
- "Get report details?" -> GET /admin/api/2020-04/reports/{report_id}.json
- "Update a report?" -> PUT /admin/api/2020-04/reports/{report_id}.json
- "Delete a report?" -> DELETE /admin/api/2020-04/reports/{report_id}.json
- "List all reports.json?" -> GET /admin/api/2020-07/reports.json
- "Create a reports.json?" -> POST /admin/api/2020-07/reports.json
- "Get report details?" -> GET /admin/api/2020-07/reports/{report_id}.json
- "Update a report?" -> PUT /admin/api/2020-07/reports/{report_id}.json
- "Delete a report?" -> DELETE /admin/api/2020-07/reports/{report_id}.json
- "List all reports.json?" -> GET /admin/api/2020-10/reports.json
- "Create a reports.json?" -> POST /admin/api/2020-10/reports.json
- "Get report details?" -> GET /admin/api/2020-10/reports/{report_id}.json
- "Update a report?" -> PUT /admin/api/2020-10/reports/{report_id}.json
- "Delete a report?" -> DELETE /admin/api/2020-10/reports/{report_id}.json
- "List all reports.json?" -> GET /admin/api/2021-01/reports.json
- "Create a reports.json?" -> POST /admin/api/2021-01/reports.json
- "Get report details?" -> GET /admin/api/2021-01/reports/{report_id}.json
- "Update a report?" -> PUT /admin/api/2021-01/reports/{report_id}.json
- "Delete a report?" -> DELETE /admin/api/2021-01/reports/{report_id}.json
- "List all reports.json?" -> GET /admin/api/unstable/reports.json
- "Create a reports.json?" -> POST /admin/api/unstable/reports.json
- "Get report details?" -> GET /admin/api/unstable/reports/{report_id}.json
- "Update a report?" -> PUT /admin/api/unstable/reports/{report_id}.json
- "Delete a report?" -> DELETE /admin/api/unstable/reports/{report_id}.json
- "Create a application_charges.json?" -> POST /admin/api/2020-01/application_charges.json
- "List all application_charges.json?" -> GET /admin/api/2020-01/application_charges.json
- "Get application_charge details?" -> GET /admin/api/2020-01/application_charges/{application_charge_id}.json
- "Create a activate.json?" -> POST /admin/api/2020-01/application_charges/{application_charge_id}/activate.json
- "Create a application_charges.json?" -> POST /admin/api/2020-04/application_charges.json
- "List all application_charges.json?" -> GET /admin/api/2020-04/application_charges.json
- "Get application_charge details?" -> GET /admin/api/2020-04/application_charges/{application_charge_id}.json
- "Create a activate.json?" -> POST /admin/api/2020-04/application_charges/{application_charge_id}/activate.json
- "Create a application_charges.json?" -> POST /admin/api/2020-07/application_charges.json
- "List all application_charges.json?" -> GET /admin/api/2020-07/application_charges.json
- "Get application_charge details?" -> GET /admin/api/2020-07/application_charges/{application_charge_id}.json
- "Create a activate.json?" -> POST /admin/api/2020-07/application_charges/{application_charge_id}/activate.json
- "Create a application_charges.json?" -> POST /admin/api/2020-10/application_charges.json
- "List all application_charges.json?" -> GET /admin/api/2020-10/application_charges.json
- "Get application_charge details?" -> GET /admin/api/2020-10/application_charges/{application_charge_id}.json
- "Create a activate.json?" -> POST /admin/api/2020-10/application_charges/{application_charge_id}/activate.json
- "Create a application_charges.json?" -> POST /admin/api/2021-01/application_charges.json
- "List all application_charges.json?" -> GET /admin/api/2021-01/application_charges.json
- "Get application_charge details?" -> GET /admin/api/2021-01/application_charges/{application_charge_id}.json
- "Create a application_charges.json?" -> POST /admin/api/unstable/application_charges.json
- "List all application_charges.json?" -> GET /admin/api/unstable/application_charges.json
- "Get application_charge details?" -> GET /admin/api/unstable/application_charges/{application_charge_id}.json
- "Create a application_credits.json?" -> POST /admin/api/2020-01/application_credits.json
- "List all application_credits.json?" -> GET /admin/api/2020-01/application_credits.json
- "Get application_credit details?" -> GET /admin/api/2020-01/application_credits/{application_credit_id}.json
- "Create a application_credits.json?" -> POST /admin/api/2020-04/application_credits.json
- "List all application_credits.json?" -> GET /admin/api/2020-04/application_credits.json
- "Get application_credit details?" -> GET /admin/api/2020-04/application_credits/{application_credit_id}.json
- "Create a application_credits.json?" -> POST /admin/api/2020-07/application_credits.json
- "List all application_credits.json?" -> GET /admin/api/2020-07/application_credits.json
- "Get application_credit details?" -> GET /admin/api/2020-07/application_credits/{application_credit_id}.json
- "Create a application_credits.json?" -> POST /admin/api/2020-10/application_credits.json
- "List all application_credits.json?" -> GET /admin/api/2020-10/application_credits.json
- "Get application_credit details?" -> GET /admin/api/2020-10/application_credits/{application_credit_id}.json
- "Create a application_credits.json?" -> POST /admin/api/2021-01/application_credits.json
- "List all application_credits.json?" -> GET /admin/api/2021-01/application_credits.json
- "Get application_credit details?" -> GET /admin/api/2021-01/application_credits/{application_credit_id}.json
- "Create a application_credits.json?" -> POST /admin/api/unstable/application_credits.json
- "List all application_credits.json?" -> GET /admin/api/unstable/application_credits.json
- "Get application_credit details?" -> GET /admin/api/unstable/application_credits/{application_credit_id}.json
- "Create a recurring_application_charges.json?" -> POST /admin/api/2020-01/recurring_application_charges.json
- "List all recurring_application_charges.json?" -> GET /admin/api/2020-01/recurring_application_charges.json
- "Get recurring_application_charge details?" -> GET /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}.json
- "Delete a recurring_application_charge?" -> DELETE /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}.json
- "Create a activate.json?" -> POST /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/activate.json
- "Create a recurring_application_charges.json?" -> POST /admin/api/2020-04/recurring_application_charges.json
- "List all recurring_application_charges.json?" -> GET /admin/api/2020-04/recurring_application_charges.json
- "Get recurring_application_charge details?" -> GET /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}.json
- "Delete a recurring_application_charge?" -> DELETE /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}.json
- "Create a activate.json?" -> POST /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/activate.json
- "Create a recurring_application_charges.json?" -> POST /admin/api/2020-07/recurring_application_charges.json
- "List all recurring_application_charges.json?" -> GET /admin/api/2020-07/recurring_application_charges.json
- "Get recurring_application_charge details?" -> GET /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}.json
- "Delete a recurring_application_charge?" -> DELETE /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}.json
- "Create a activate.json?" -> POST /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/activate.json
- "Create a recurring_application_charges.json?" -> POST /admin/api/2020-10/recurring_application_charges.json
- "List all recurring_application_charges.json?" -> GET /admin/api/2020-10/recurring_application_charges.json
- "Get recurring_application_charge details?" -> GET /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}.json
- "Delete a recurring_application_charge?" -> DELETE /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}.json
- "Create a activate.json?" -> POST /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/activate.json
- "Create a recurring_application_charges.json?" -> POST /admin/api/2021-01/recurring_application_charges.json
- "List all recurring_application_charges.json?" -> GET /admin/api/2021-01/recurring_application_charges.json
- "Get recurring_application_charge details?" -> GET /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}.json
- "Delete a recurring_application_charge?" -> DELETE /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}.json
- "Create a recurring_application_charges.json?" -> POST /admin/api/unstable/recurring_application_charges.json
- "List all recurring_application_charges.json?" -> GET /admin/api/unstable/recurring_application_charges.json
- "Get recurring_application_charge details?" -> GET /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}.json
- "Delete a recurring_application_charge?" -> DELETE /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}.json
- "Create a usage_charges.json?" -> POST /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "List all usage_charges.json?" -> GET /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "Get usage_charge details?" -> GET /admin/api/2020-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json
- "Create a usage_charges.json?" -> POST /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "List all usage_charges.json?" -> GET /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "Get usage_charge details?" -> GET /admin/api/2020-04/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json
- "Create a usage_charges.json?" -> POST /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "List all usage_charges.json?" -> GET /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "Get usage_charge details?" -> GET /admin/api/2020-07/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json
- "Create a usage_charges.json?" -> POST /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "List all usage_charges.json?" -> GET /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "Get usage_charge details?" -> GET /admin/api/2020-10/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json
- "Create a usage_charges.json?" -> POST /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "List all usage_charges.json?" -> GET /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "Get usage_charge details?" -> GET /admin/api/2021-01/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json
- "Create a usage_charges.json?" -> POST /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "List all usage_charges.json?" -> GET /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}/usage_charges.json
- "Get usage_charge details?" -> GET /admin/api/unstable/recurring_application_charges/{recurring_application_charge_id}/usage_charges/{usage_charge_id}.json
- "List all customers.json?" -> GET /admin/api/2020-01/customers.json
- "Create a customers.json?" -> POST /admin/api/2020-01/customers.json
- "Search search.json?" -> GET /admin/api/2020-01/customers/search.json
- "Get customer details?" -> GET /admin/api/2020-01/customers/{customer_id}.json
- "Update a customer?" -> PUT /admin/api/2020-01/customers/{customer_id}.json
- "Delete a customer?" -> DELETE /admin/api/2020-01/customers/{customer_id}.json
- "Create a account_activation_url.json?" -> POST /admin/api/2020-01/customers/{customer_id}/account_activation_url.json
- "Create a send_invite.json?" -> POST /admin/api/2020-01/customers/{customer_id}/send_invite.json
- "List all count.json?" -> GET /admin/api/2020-01/customers/count.json
- "List all orders.json?" -> GET /admin/api/2020-01/customers/{customer_id}/orders.json
- "List all customers.json?" -> GET /admin/api/2020-04/customers.json
- "Create a customers.json?" -> POST /admin/api/2020-04/customers.json
- "Search search.json?" -> GET /admin/api/2020-04/customers/search.json
- "Get customer details?" -> GET /admin/api/2020-04/customers/{customer_id}.json
- "Update a customer?" -> PUT /admin/api/2020-04/customers/{customer_id}.json
- "Delete a customer?" -> DELETE /admin/api/2020-04/customers/{customer_id}.json
- "Create a account_activation_url.json?" -> POST /admin/api/2020-04/customers/{customer_id}/account_activation_url.json
- "Create a send_invite.json?" -> POST /admin/api/2020-04/customers/{customer_id}/send_invite.json
- "List all count.json?" -> GET /admin/api/2020-04/customers/count.json
- "List all orders.json?" -> GET /admin/api/2020-04/customers/{customer_id}/orders.json
- "List all customers.json?" -> GET /admin/api/2020-07/customers.json
- "Create a customers.json?" -> POST /admin/api/2020-07/customers.json
- "Search search.json?" -> GET /admin/api/2020-07/customers/search.json
- "Get customer details?" -> GET /admin/api/2020-07/customers/{customer_id}.json
- "Update a customer?" -> PUT /admin/api/2020-07/customers/{customer_id}.json
- "Delete a customer?" -> DELETE /admin/api/2020-07/customers/{customer_id}.json
- "Create a account_activation_url.json?" -> POST /admin/api/2020-07/customers/{customer_id}/account_activation_url.json
- "Create a send_invite.json?" -> POST /admin/api/2020-07/customers/{customer_id}/send_invite.json
- "List all count.json?" -> GET /admin/api/2020-07/customers/count.json
- "List all orders.json?" -> GET /admin/api/2020-07/customers/{customer_id}/orders.json
- "List all customers.json?" -> GET /admin/api/2020-10/customers.json
- "Create a customers.json?" -> POST /admin/api/2020-10/customers.json
- "Search search.json?" -> GET /admin/api/2020-10/customers/search.json
- "Get customer details?" -> GET /admin/api/2020-10/customers/{customer_id}.json
- "Update a customer?" -> PUT /admin/api/2020-10/customers/{customer_id}.json
- "Delete a customer?" -> DELETE /admin/api/2020-10/customers/{customer_id}.json
- "Create a account_activation_url.json?" -> POST /admin/api/2020-10/customers/{customer_id}/account_activation_url.json
- "Create a send_invite.json?" -> POST /admin/api/2020-10/customers/{customer_id}/send_invite.json
- "List all count.json?" -> GET /admin/api/2020-10/customers/count.json
- "List all orders.json?" -> GET /admin/api/2020-10/customers/{customer_id}/orders.json
- "List all customers.json?" -> GET /admin/api/2021-01/customers.json
- "Create a customers.json?" -> POST /admin/api/2021-01/customers.json
- "Search search.json?" -> GET /admin/api/2021-01/customers/search.json
- "Get customer details?" -> GET /admin/api/2021-01/customers/{customer_id}.json
- "Update a customer?" -> PUT /admin/api/2021-01/customers/{customer_id}.json
- "Delete a customer?" -> DELETE /admin/api/2021-01/customers/{customer_id}.json
- "Create a account_activation_url.json?" -> POST /admin/api/2021-01/customers/{customer_id}/account_activation_url.json
- "Create a send_invite.json?" -> POST /admin/api/2021-01/customers/{customer_id}/send_invite.json
- "List all count.json?" -> GET /admin/api/2021-01/customers/count.json
- "List all orders.json?" -> GET /admin/api/2021-01/customers/{customer_id}/orders.json
- "List all customers.json?" -> GET /admin/api/unstable/customers.json
- "Create a customers.json?" -> POST /admin/api/unstable/customers.json
- "Search search.json?" -> GET /admin/api/unstable/customers/search.json
- "Get customer details?" -> GET /admin/api/unstable/customers/{customer_id}.json
- "Update a customer?" -> PUT /admin/api/unstable/customers/{customer_id}.json
- "Delete a customer?" -> DELETE /admin/api/unstable/customers/{customer_id}.json
- "Create a account_activation_url.json?" -> POST /admin/api/unstable/customers/{customer_id}/account_activation_url.json
- "Create a send_invite.json?" -> POST /admin/api/unstable/customers/{customer_id}/send_invite.json
- "List all count.json?" -> GET /admin/api/unstable/customers/count.json
- "List all orders.json?" -> GET /admin/api/unstable/customers/{customer_id}/orders.json
- "List all addresses.json?" -> GET /admin/api/2020-01/customers/{customer_id}/addresses.json
- "Create a addresses.json?" -> POST /admin/api/2020-01/customers/{customer_id}/addresses.json
- "Get address details?" -> GET /admin/api/2020-01/customers/{customer_id}/addresses/{address_id}.json
- "Update a address?" -> PUT /admin/api/2020-01/customers/{customer_id}/addresses/{address_id}.json
- "Delete a address?" -> DELETE /admin/api/2020-01/customers/{customer_id}/addresses/{address_id}.json
- "List all addresses.json?" -> GET /admin/api/2020-04/customers/{customer_id}/addresses.json
- "Create a addresses.json?" -> POST /admin/api/2020-04/customers/{customer_id}/addresses.json
- "Get address details?" -> GET /admin/api/2020-04/customers/{customer_id}/addresses/{address_id}.json
- "Update a address?" -> PUT /admin/api/2020-04/customers/{customer_id}/addresses/{address_id}.json
- "Delete a address?" -> DELETE /admin/api/2020-04/customers/{customer_id}/addresses/{address_id}.json
- "List all addresses.json?" -> GET /admin/api/2020-07/customers/{customer_id}/addresses.json
- "Create a addresses.json?" -> POST /admin/api/2020-07/customers/{customer_id}/addresses.json
- "Get address details?" -> GET /admin/api/2020-07/customers/{customer_id}/addresses/{address_id}.json
- "Update a address?" -> PUT /admin/api/2020-07/customers/{customer_id}/addresses/{address_id}.json
- "Delete a address?" -> DELETE /admin/api/2020-07/customers/{customer_id}/addresses/{address_id}.json
- "List all addresses.json?" -> GET /admin/api/2020-10/customers/{customer_id}/addresses.json
- "Create a addresses.json?" -> POST /admin/api/2020-10/customers/{customer_id}/addresses.json
- "Get address details?" -> GET /admin/api/2020-10/customers/{customer_id}/addresses/{address_id}.json
- "Update a address?" -> PUT /admin/api/2020-10/customers/{customer_id}/addresses/{address_id}.json
- "Delete a address?" -> DELETE /admin/api/2020-10/customers/{customer_id}/addresses/{address_id}.json
- "List all addresses.json?" -> GET /admin/api/2021-01/customers/{customer_id}/addresses.json
- "Create a addresses.json?" -> POST /admin/api/2021-01/customers/{customer_id}/addresses.json
- "Get address details?" -> GET /admin/api/2021-01/customers/{customer_id}/addresses/{address_id}.json
- "Update a address?" -> PUT /admin/api/2021-01/customers/{customer_id}/addresses/{address_id}.json
- "Delete a address?" -> DELETE /admin/api/2021-01/customers/{customer_id}/addresses/{address_id}.json
- "List all addresses.json?" -> GET /admin/api/unstable/customers/{customer_id}/addresses.json
- "Create a addresses.json?" -> POST /admin/api/unstable/customers/{customer_id}/addresses.json
- "Get address details?" -> GET /admin/api/unstable/customers/{customer_id}/addresses/{address_id}.json
- "Update a address?" -> PUT /admin/api/unstable/customers/{customer_id}/addresses/{address_id}.json
- "Delete a address?" -> DELETE /admin/api/unstable/customers/{customer_id}/addresses/{address_id}.json
- "List all customer_saved_searches.json?" -> GET /admin/api/2020-01/customer_saved_searches.json
- "Create a customer_saved_searches.json?" -> POST /admin/api/2020-01/customer_saved_searches.json
- "List all count.json?" -> GET /admin/api/2020-01/customer_saved_searches/count.json
- "Get customer_saved_searche details?" -> GET /admin/api/2020-01/customer_saved_searches/{customer_saved_search_id}.json
- "Update a customer_saved_searche?" -> PUT /admin/api/2020-01/customer_saved_searches/{customer_saved_search_id}.json
- "Delete a customer_saved_searche?" -> DELETE /admin/api/2020-01/customer_saved_searches/{customer_saved_search_id}.json
- "List all customers.json?" -> GET /admin/api/2020-01/customer_saved_searches/{customer_saved_search_id}/customers.json
- "List all customer_saved_searches.json?" -> GET /admin/api/2020-04/customer_saved_searches.json
- "Create a customer_saved_searches.json?" -> POST /admin/api/2020-04/customer_saved_searches.json
- "List all count.json?" -> GET /admin/api/2020-04/customer_saved_searches/count.json
- "Get customer_saved_searche details?" -> GET /admin/api/2020-04/customer_saved_searches/{customer_saved_search_id}.json
- "Update a customer_saved_searche?" -> PUT /admin/api/2020-04/customer_saved_searches/{customer_saved_search_id}.json
- "Delete a customer_saved_searche?" -> DELETE /admin/api/2020-04/customer_saved_searches/{customer_saved_search_id}.json
- "List all customers.json?" -> GET /admin/api/2020-04/customer_saved_searches/{customer_saved_search_id}/customers.json
- "List all customer_saved_searches.json?" -> GET /admin/api/2020-07/customer_saved_searches.json
- "Create a customer_saved_searches.json?" -> POST /admin/api/2020-07/customer_saved_searches.json
- "List all count.json?" -> GET /admin/api/2020-07/customer_saved_searches/count.json
- "Get customer_saved_searche details?" -> GET /admin/api/2020-07/customer_saved_searches/{customer_saved_search_id}.json
- "Update a customer_saved_searche?" -> PUT /admin/api/2020-07/customer_saved_searches/{customer_saved_search_id}.json
- "Delete a customer_saved_searche?" -> DELETE /admin/api/2020-07/customer_saved_searches/{customer_saved_search_id}.json
- "List all customers.json?" -> GET /admin/api/2020-07/customer_saved_searches/{customer_saved_search_id}/customers.json
- "List all customer_saved_searches.json?" -> GET /admin/api/2020-10/customer_saved_searches.json
- "Create a customer_saved_searches.json?" -> POST /admin/api/2020-10/customer_saved_searches.json
- "List all count.json?" -> GET /admin/api/2020-10/customer_saved_searches/count.json
- "Get customer_saved_searche details?" -> GET /admin/api/2020-10/customer_saved_searches/{customer_saved_search_id}.json
- "Update a customer_saved_searche?" -> PUT /admin/api/2020-10/customer_saved_searches/{customer_saved_search_id}.json
- "Delete a customer_saved_searche?" -> DELETE /admin/api/2020-10/customer_saved_searches/{customer_saved_search_id}.json
- "List all customers.json?" -> GET /admin/api/2020-10/customer_saved_searches/{customer_saved_search_id}/customers.json
- "List all customer_saved_searches.json?" -> GET /admin/api/2021-01/customer_saved_searches.json
- "Create a customer_saved_searches.json?" -> POST /admin/api/2021-01/customer_saved_searches.json
- "List all count.json?" -> GET /admin/api/2021-01/customer_saved_searches/count.json
- "Get customer_saved_searche details?" -> GET /admin/api/2021-01/customer_saved_searches/{customer_saved_search_id}.json
- "Update a customer_saved_searche?" -> PUT /admin/api/2021-01/customer_saved_searches/{customer_saved_search_id}.json
- "Delete a customer_saved_searche?" -> DELETE /admin/api/2021-01/customer_saved_searches/{customer_saved_search_id}.json
- "List all customers.json?" -> GET /admin/api/2021-01/customer_saved_searches/{customer_saved_search_id}/customers.json
- "List all customer_saved_searches.json?" -> GET /admin/api/unstable/customer_saved_searches.json
- "Create a customer_saved_searches.json?" -> POST /admin/api/unstable/customer_saved_searches.json
- "List all count.json?" -> GET /admin/api/unstable/customer_saved_searches/count.json
- "Get customer_saved_searche details?" -> GET /admin/api/unstable/customer_saved_searches/{customer_saved_search_id}.json
- "Update a customer_saved_searche?" -> PUT /admin/api/unstable/customer_saved_searches/{customer_saved_search_id}.json
- "Delete a customer_saved_searche?" -> DELETE /admin/api/unstable/customer_saved_searches/{customer_saved_search_id}.json
- "List all customers.json?" -> GET /admin/api/unstable/customer_saved_searches/{customer_saved_search_id}/customers.json
- "List all deprecated_api_calls.json?" -> GET /admin/api/2021-01/deprecated_api_calls.json
- "List all deprecated_api_calls.json?" -> GET /admin/api/unstable/deprecated_api_calls.json
- "Create a discount_codes.json?" -> POST /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes.json
- "List all discount_codes.json?" -> GET /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes.json
- "Update a discount_code?" -> PUT /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Get discount_code details?" -> GET /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Delete a discount_code?" -> DELETE /admin/api/2020-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "List all lookup.json?" -> GET /admin/api/2020-01/discount_codes/lookup.json
- "Create a batch.json?" -> POST /admin/api/2020-01/price_rules/{price_rule_id}/batch.json
- "Get batch details?" -> GET /admin/api/2020-01/price_rules/{price_rule_id}/batch/{batch_id}.json
- "List all discount_codes.json?" -> GET /admin/api/2020-01/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json
- "Create a discount_codes.json?" -> POST /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes.json
- "List all discount_codes.json?" -> GET /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes.json
- "Update a discount_code?" -> PUT /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Get discount_code details?" -> GET /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Delete a discount_code?" -> DELETE /admin/api/2020-04/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "List all lookup.json?" -> GET /admin/api/2020-04/discount_codes/lookup.json
- "Create a batch.json?" -> POST /admin/api/2020-04/price_rules/{price_rule_id}/batch.json
- "Get batch details?" -> GET /admin/api/2020-04/price_rules/{price_rule_id}/batch/{batch_id}.json
- "List all discount_codes.json?" -> GET /admin/api/2020-04/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json
- "Create a discount_codes.json?" -> POST /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes.json
- "List all discount_codes.json?" -> GET /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes.json
- "Update a discount_code?" -> PUT /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Get discount_code details?" -> GET /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Delete a discount_code?" -> DELETE /admin/api/2020-07/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "List all lookup.json?" -> GET /admin/api/2020-07/discount_codes/lookup.json
- "Create a batch.json?" -> POST /admin/api/2020-07/price_rules/{price_rule_id}/batch.json
- "Get batch details?" -> GET /admin/api/2020-07/price_rules/{price_rule_id}/batch/{batch_id}.json
- "List all discount_codes.json?" -> GET /admin/api/2020-07/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json
- "Create a discount_codes.json?" -> POST /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes.json
- "List all discount_codes.json?" -> GET /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes.json
- "Update a discount_code?" -> PUT /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Get discount_code details?" -> GET /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Delete a discount_code?" -> DELETE /admin/api/2020-10/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "List all lookup.json?" -> GET /admin/api/2020-10/discount_codes/lookup.json
- "Create a batch.json?" -> POST /admin/api/2020-10/price_rules/{price_rule_id}/batch.json
- "Get batch details?" -> GET /admin/api/2020-10/price_rules/{price_rule_id}/batch/{batch_id}.json
- "List all discount_codes.json?" -> GET /admin/api/2020-10/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json
- "Create a discount_codes.json?" -> POST /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes.json
- "List all discount_codes.json?" -> GET /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes.json
- "Update a discount_code?" -> PUT /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Get discount_code details?" -> GET /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Delete a discount_code?" -> DELETE /admin/api/2021-01/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "List all lookup.json?" -> GET /admin/api/2021-01/discount_codes/lookup.json
- "Create a batch.json?" -> POST /admin/api/2021-01/price_rules/{price_rule_id}/batch.json
- "Get batch details?" -> GET /admin/api/2021-01/price_rules/{price_rule_id}/batch/{batch_id}.json
- "List all discount_codes.json?" -> GET /admin/api/2021-01/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json
- "Create a discount_codes.json?" -> POST /admin/api/unstable/price_rules/{price_rule_id}/discount_codes.json
- "List all discount_codes.json?" -> GET /admin/api/unstable/price_rules/{price_rule_id}/discount_codes.json
- "Update a discount_code?" -> PUT /admin/api/unstable/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Get discount_code details?" -> GET /admin/api/unstable/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "Delete a discount_code?" -> DELETE /admin/api/unstable/price_rules/{price_rule_id}/discount_codes/{discount_code_id}.json
- "List all lookup.json?" -> GET /admin/api/unstable/discount_codes/lookup.json
- "Create a batch.json?" -> POST /admin/api/unstable/price_rules/{price_rule_id}/batch.json
- "Get batch details?" -> GET /admin/api/unstable/price_rules/{price_rule_id}/batch/{batch_id}.json
- "List all discount_codes.json?" -> GET /admin/api/unstable/price_rules/{price_rule_id}/batch/{batch_id}/discount_codes.json
- "List all events.json?" -> GET /admin/api/2020-01/events.json
- "Get event details?" -> GET /admin/api/2020-01/events/{event_id}.json
- "List all count.json?" -> GET /admin/api/2020-01/events/count.json
- "List all events.json?" -> GET /admin/api/2020-04/events.json
- "Get event details?" -> GET /admin/api/2020-04/events/{event_id}.json
- "List all count.json?" -> GET /admin/api/2020-04/events/count.json
- "List all events.json?" -> GET /admin/api/2020-07/events.json
- "Get event details?" -> GET /admin/api/2020-07/events/{event_id}.json
- "List all count.json?" -> GET /admin/api/2020-07/events/count.json
- "List all events.json?" -> GET /admin/api/2020-10/events.json
- "Get event details?" -> GET /admin/api/2020-10/events/{event_id}.json
- "List all count.json?" -> GET /admin/api/2020-10/events/count.json
- "List all events.json?" -> GET /admin/api/2021-01/events.json
- "Get event details?" -> GET /admin/api/2021-01/events/{event_id}.json
- "List all count.json?" -> GET /admin/api/2021-01/events/count.json
- "List all events.json?" -> GET /admin/api/unstable/events.json
- "Get event details?" -> GET /admin/api/unstable/events/{event_id}.json
- "List all count.json?" -> GET /admin/api/unstable/events/count.json
- "List all webhooks.json?" -> GET /admin/api/2020-01/webhooks.json
- "Create a webhooks.json?" -> POST /admin/api/2020-01/webhooks.json
- "List all count.json?" -> GET /admin/api/2020-01/webhooks/count.json
- "Get webhook details?" -> GET /admin/api/2020-01/webhooks/{webhook_id}.json
- "Update a webhook?" -> PUT /admin/api/2020-01/webhooks/{webhook_id}.json
- "Delete a webhook?" -> DELETE /admin/api/2020-01/webhooks/{webhook_id}.json
- "List all webhooks.json?" -> GET /admin/api/2020-04/webhooks.json
- "Create a webhooks.json?" -> POST /admin/api/2020-04/webhooks.json
- "List all count.json?" -> GET /admin/api/2020-04/webhooks/count.json
- "Get webhook details?" -> GET /admin/api/2020-04/webhooks/{webhook_id}.json
- "Update a webhook?" -> PUT /admin/api/2020-04/webhooks/{webhook_id}.json
- "Delete a webhook?" -> DELETE /admin/api/2020-04/webhooks/{webhook_id}.json
- "List all webhooks.json?" -> GET /admin/api/2020-07/webhooks.json
- "Create a webhooks.json?" -> POST /admin/api/2020-07/webhooks.json
- "List all count.json?" -> GET /admin/api/2020-07/webhooks/count.json
- "Get webhook details?" -> GET /admin/api/2020-07/webhooks/{webhook_id}.json
- "Update a webhook?" -> PUT /admin/api/2020-07/webhooks/{webhook_id}.json
- "Delete a webhook?" -> DELETE /admin/api/2020-07/webhooks/{webhook_id}.json
- "List all webhooks.json?" -> GET /admin/api/2020-10/webhooks.json
- "Create a webhooks.json?" -> POST /admin/api/2020-10/webhooks.json
- "List all count.json?" -> GET /admin/api/2020-10/webhooks/count.json
- "Get webhook details?" -> GET /admin/api/2020-10/webhooks/{webhook_id}.json
- "Update a webhook?" -> PUT /admin/api/2020-10/webhooks/{webhook_id}.json
- "Delete a webhook?" -> DELETE /admin/api/2020-10/webhooks/{webhook_id}.json
- "List all webhooks.json?" -> GET /admin/api/2021-01/webhooks.json
- "Create a webhooks.json?" -> POST /admin/api/2021-01/webhooks.json
- "List all count.json?" -> GET /admin/api/2021-01/webhooks/count.json
- "Get webhook details?" -> GET /admin/api/2021-01/webhooks/{webhook_id}.json
- "Update a webhook?" -> PUT /admin/api/2021-01/webhooks/{webhook_id}.json
- "Delete a webhook?" -> DELETE /admin/api/2021-01/webhooks/{webhook_id}.json
- "List all webhooks.json?" -> GET /admin/api/unstable/webhooks.json
- "Create a webhooks.json?" -> POST /admin/api/unstable/webhooks.json
- "List all count.json?" -> GET /admin/api/unstable/webhooks/count.json
- "Get webhook details?" -> GET /admin/api/unstable/webhooks/{webhook_id}.json
- "Update a webhook?" -> PUT /admin/api/unstable/webhooks/{webhook_id}.json
- "Delete a webhook?" -> DELETE /admin/api/unstable/webhooks/{webhook_id}.json
- "List all inventory_items.json?" -> GET /admin/api/2020-01/inventory_items.json
- "Get inventory_item details?" -> GET /admin/api/2020-01/inventory_items/{inventory_item_id}.json
- "Update a inventory_item?" -> PUT /admin/api/2020-01/inventory_items/{inventory_item_id}.json
- "List all inventory_items.json?" -> GET /admin/api/2020-04/inventory_items.json
- "Get inventory_item details?" -> GET /admin/api/2020-04/inventory_items/{inventory_item_id}.json
- "Update a inventory_item?" -> PUT /admin/api/2020-04/inventory_items/{inventory_item_id}.json
- "List all inventory_items.json?" -> GET /admin/api/2020-07/inventory_items.json
- "Get inventory_item details?" -> GET /admin/api/2020-07/inventory_items/{inventory_item_id}.json
- "Update a inventory_item?" -> PUT /admin/api/2020-07/inventory_items/{inventory_item_id}.json
- "List all inventory_items.json?" -> GET /admin/api/2020-10/inventory_items.json
- "Get inventory_item details?" -> GET /admin/api/2020-10/inventory_items/{inventory_item_id}.json
- "Update a inventory_item?" -> PUT /admin/api/2020-10/inventory_items/{inventory_item_id}.json
- "List all inventory_items.json?" -> GET /admin/api/2021-01/inventory_items.json
- "Get inventory_item details?" -> GET /admin/api/2021-01/inventory_items/{inventory_item_id}.json
- "Update a inventory_item?" -> PUT /admin/api/2021-01/inventory_items/{inventory_item_id}.json
- "List all inventory_items.json?" -> GET /admin/api/unstable/inventory_items.json
- "Get inventory_item details?" -> GET /admin/api/unstable/inventory_items/{inventory_item_id}.json
- "Update a inventory_item?" -> PUT /admin/api/unstable/inventory_items/{inventory_item_id}.json
- "List all inventory_levels.json?" -> GET /admin/api/2020-01/inventory_levels.json
- "Create a adjust.json?" -> POST /admin/api/2020-01/inventory_levels/adjust.json
- "Create a connect.json?" -> POST /admin/api/2020-01/inventory_levels/connect.json
- "Create a set.json?" -> POST /admin/api/2020-01/inventory_levels/set.json
- "List all inventory_levels.json?" -> GET /admin/api/2020-04/inventory_levels.json
- "Create a adjust.json?" -> POST /admin/api/2020-04/inventory_levels/adjust.json
- "Create a connect.json?" -> POST /admin/api/2020-04/inventory_levels/connect.json
- "Create a set.json?" -> POST /admin/api/2020-04/inventory_levels/set.json
- "List all inventory_levels.json?" -> GET /admin/api/2020-07/inventory_levels.json
- "Create a adjust.json?" -> POST /admin/api/2020-07/inventory_levels/adjust.json
- "Create a connect.json?" -> POST /admin/api/2020-07/inventory_levels/connect.json
- "Create a set.json?" -> POST /admin/api/2020-07/inventory_levels/set.json
- "List all inventory_levels.json?" -> GET /admin/api/2020-10/inventory_levels.json
- "Create a adjust.json?" -> POST /admin/api/2020-10/inventory_levels/adjust.json
- "Create a connect.json?" -> POST /admin/api/2020-10/inventory_levels/connect.json
- "Create a set.json?" -> POST /admin/api/2020-10/inventory_levels/set.json
- "List all inventory_levels.json?" -> GET /admin/api/2021-01/inventory_levels.json
- "Create a adjust.json?" -> POST /admin/api/2021-01/inventory_levels/adjust.json
- "Create a connect.json?" -> POST /admin/api/2021-01/inventory_levels/connect.json
- "Create a set.json?" -> POST /admin/api/2021-01/inventory_levels/set.json
- "List all inventory_levels.json?" -> GET /admin/api/unstable/inventory_levels.json
- "Create a adjust.json?" -> POST /admin/api/unstable/inventory_levels/adjust.json
- "Create a connect.json?" -> POST /admin/api/unstable/inventory_levels/connect.json
- "Create a set.json?" -> POST /admin/api/unstable/inventory_levels/set.json
- "List all locations.json?" -> GET /admin/api/2020-01/locations.json
- "Get location details?" -> GET /admin/api/2020-01/locations/{location_id}.json
- "List all count.json?" -> GET /admin/api/2020-01/locations/count.json
- "List all inventory_levels.json?" -> GET /admin/api/2020-01/locations/{location_id}/inventory_levels.json
- "List all locations.json?" -> GET /admin/api/2020-04/locations.json
- "Get location details?" -> GET /admin/api/2020-04/locations/{location_id}.json
- "List all count.json?" -> GET /admin/api/2020-04/locations/count.json
- "List all inventory_levels.json?" -> GET /admin/api/2020-04/locations/{location_id}/inventory_levels.json
- "List all locations.json?" -> GET /admin/api/2020-07/locations.json
- "Get location details?" -> GET /admin/api/2020-07/locations/{location_id}.json
- "List all count.json?" -> GET /admin/api/2020-07/locations/count.json
- "List all inventory_levels.json?" -> GET /admin/api/2020-07/locations/{location_id}/inventory_levels.json
- "List all locations.json?" -> GET /admin/api/2020-10/locations.json
- "Get location details?" -> GET /admin/api/2020-10/locations/{location_id}.json
- "List all count.json?" -> GET /admin/api/2020-10/locations/count.json
- "List all inventory_levels.json?" -> GET /admin/api/2020-10/locations/{location_id}/inventory_levels.json
- "List all locations.json?" -> GET /admin/api/2021-01/locations.json
- "Get location details?" -> GET /admin/api/2021-01/locations/{location_id}.json
- "List all count.json?" -> GET /admin/api/2021-01/locations/count.json
- "List all inventory_levels.json?" -> GET /admin/api/2021-01/locations/{location_id}/inventory_levels.json
- "List all locations.json?" -> GET /admin/api/unstable/locations.json
- "Get location details?" -> GET /admin/api/unstable/locations/{location_id}.json
- "List all count.json?" -> GET /admin/api/unstable/locations/count.json
- "List all inventory_levels.json?" -> GET /admin/api/unstable/locations/{location_id}/inventory_levels.json
- "List all metafields.json?" -> GET /admin/api/2020-01/metafields.json
- "Create a metafields.json?" -> POST /admin/api/2020-01/metafields.json
- "List all count.json?" -> GET /admin/api/2020-01/metafields/count.json
- "Get metafield details?" -> GET /admin/api/2020-01/metafields/{metafield_id}.json
- "Update a metafield?" -> PUT /admin/api/2020-01/metafields/{metafield_id}.json
- "Delete a metafield?" -> DELETE /admin/api/2020-01/metafields/{metafield_id}.json
- "List all metafields.json?" -> GET /admin/api/2020-04/metafields.json
- "Create a metafields.json?" -> POST /admin/api/2020-04/metafields.json
- "List all count.json?" -> GET /admin/api/2020-04/metafields/count.json
- "Get metafield details?" -> GET /admin/api/2020-04/metafields/{metafield_id}.json
- "Update a metafield?" -> PUT /admin/api/2020-04/metafields/{metafield_id}.json
- "Delete a metafield?" -> DELETE /admin/api/2020-04/metafields/{metafield_id}.json
- "List all metafields.json?" -> GET /admin/api/2020-07/metafields.json
- "Create a metafields.json?" -> POST /admin/api/2020-07/metafields.json
- "List all count.json?" -> GET /admin/api/2020-07/metafields/count.json
- "Get metafield details?" -> GET /admin/api/2020-07/metafields/{metafield_id}.json
- "Update a metafield?" -> PUT /admin/api/2020-07/metafields/{metafield_id}.json
- "Delete a metafield?" -> DELETE /admin/api/2020-07/metafields/{metafield_id}.json
- "List all metafields.json?" -> GET /admin/api/2020-10/metafields.json
- "Create a metafields.json?" -> POST /admin/api/2020-10/metafields.json
- "List all count.json?" -> GET /admin/api/2020-10/metafields/count.json
- "Get metafield details?" -> GET /admin/api/2020-10/metafields/{metafield_id}.json
- "Update a metafield?" -> PUT /admin/api/2020-10/metafields/{metafield_id}.json
- "Delete a metafield?" -> DELETE /admin/api/2020-10/metafields/{metafield_id}.json
- "List all metafields.json?" -> GET /admin/api/2021-01/metafields.json
- "Create a metafields.json?" -> POST /admin/api/2021-01/metafields.json
- "List all count.json?" -> GET /admin/api/2021-01/metafields/count.json
- "Get metafield details?" -> GET /admin/api/2021-01/metafields/{metafield_id}.json
- "Update a metafield?" -> PUT /admin/api/2021-01/metafields/{metafield_id}.json
- "Delete a metafield?" -> DELETE /admin/api/2021-01/metafields/{metafield_id}.json
- "List all metafields.json?" -> GET /admin/api/unstable/metafields.json
- "Create a metafields.json?" -> POST /admin/api/unstable/metafields.json
- "List all count.json?" -> GET /admin/api/unstable/metafields/count.json
- "Get metafield details?" -> GET /admin/api/unstable/metafields/{metafield_id}.json
- "Update a metafield?" -> PUT /admin/api/unstable/metafields/{metafield_id}.json
- "Delete a metafield?" -> DELETE /admin/api/unstable/metafields/{metafield_id}.json
- "List all articles.json?" -> GET /admin/api/2020-01/blogs/{blog_id}/articles.json
- "Create a articles.json?" -> POST /admin/api/2020-01/blogs/{blog_id}/articles.json
- "List all count.json?" -> GET /admin/api/2020-01/blogs/{blog_id}/articles/count.json
- "Get article details?" -> GET /admin/api/2020-01/blogs/{blog_id}/articles/{article_id}.json
- "Update a article?" -> PUT /admin/api/2020-01/blogs/{blog_id}/articles/{article_id}.json
- "Delete a article?" -> DELETE /admin/api/2020-01/blogs/{blog_id}/articles/{article_id}.json
- "List all authors.json?" -> GET /admin/api/2020-01/articles/authors.json
- "List all tags.json?" -> GET /admin/api/2020-01/articles/tags.json
- "List all articles.json?" -> GET /admin/api/2020-04/blogs/{blog_id}/articles.json
- "Create a articles.json?" -> POST /admin/api/2020-04/blogs/{blog_id}/articles.json
- "List all count.json?" -> GET /admin/api/2020-04/blogs/{blog_id}/articles/count.json
- "Get article details?" -> GET /admin/api/2020-04/blogs/{blog_id}/articles/{article_id}.json
- "Update a article?" -> PUT /admin/api/2020-04/blogs/{blog_id}/articles/{article_id}.json
- "Delete a article?" -> DELETE /admin/api/2020-04/blogs/{blog_id}/articles/{article_id}.json
- "List all authors.json?" -> GET /admin/api/2020-04/articles/authors.json
- "List all tags.json?" -> GET /admin/api/2020-04/articles/tags.json
- "List all articles.json?" -> GET /admin/api/2020-07/blogs/{blog_id}/articles.json
- "Create a articles.json?" -> POST /admin/api/2020-07/blogs/{blog_id}/articles.json
- "List all count.json?" -> GET /admin/api/2020-07/blogs/{blog_id}/articles/count.json
- "Get article details?" -> GET /admin/api/2020-07/blogs/{blog_id}/articles/{article_id}.json
- "Update a article?" -> PUT /admin/api/2020-07/blogs/{blog_id}/articles/{article_id}.json
- "Delete a article?" -> DELETE /admin/api/2020-07/blogs/{blog_id}/articles/{article_id}.json
- "List all authors.json?" -> GET /admin/api/2020-07/articles/authors.json
- "List all tags.json?" -> GET /admin/api/2020-07/articles/tags.json
- "List all articles.json?" -> GET /admin/api/2020-10/blogs/{blog_id}/articles.json
- "Create a articles.json?" -> POST /admin/api/2020-10/blogs/{blog_id}/articles.json
- "List all count.json?" -> GET /admin/api/2020-10/blogs/{blog_id}/articles/count.json
- "Get article details?" -> GET /admin/api/2020-10/blogs/{blog_id}/articles/{article_id}.json
- "Update a article?" -> PUT /admin/api/2020-10/blogs/{blog_id}/articles/{article_id}.json
- "Delete a article?" -> DELETE /admin/api/2020-10/blogs/{blog_id}/articles/{article_id}.json
- "List all authors.json?" -> GET /admin/api/2020-10/articles/authors.json
- "List all tags.json?" -> GET /admin/api/2020-10/articles/tags.json
- "List all articles.json?" -> GET /admin/api/2021-01/blogs/{blog_id}/articles.json
- "Create a articles.json?" -> POST /admin/api/2021-01/blogs/{blog_id}/articles.json
- "List all count.json?" -> GET /admin/api/2021-01/blogs/{blog_id}/articles/count.json
- "Get article details?" -> GET /admin/api/2021-01/blogs/{blog_id}/articles/{article_id}.json
- "Update a article?" -> PUT /admin/api/2021-01/blogs/{blog_id}/articles/{article_id}.json
- "Delete a article?" -> DELETE /admin/api/2021-01/blogs/{blog_id}/articles/{article_id}.json
- "List all authors.json?" -> GET /admin/api/2021-01/articles/authors.json
- "List all tags.json?" -> GET /admin/api/2021-01/articles/tags.json
- "List all articles.json?" -> GET /admin/api/unstable/blogs/{blog_id}/articles.json
- "Create a articles.json?" -> POST /admin/api/unstable/blogs/{blog_id}/articles.json
- "List all count.json?" -> GET /admin/api/unstable/blogs/{blog_id}/articles/count.json
- "Get article details?" -> GET /admin/api/unstable/blogs/{blog_id}/articles/{article_id}.json
- "Update a article?" -> PUT /admin/api/unstable/blogs/{blog_id}/articles/{article_id}.json
- "Delete a article?" -> DELETE /admin/api/unstable/blogs/{blog_id}/articles/{article_id}.json
- "List all authors.json?" -> GET /admin/api/unstable/articles/authors.json
- "List all tags.json?" -> GET /admin/api/unstable/articles/tags.json
- "List all assets.json?" -> GET /admin/api/2020-01/themes/{theme_id}/assets.json
- "List all assets.json?" -> GET /admin/api/2020-04/themes/{theme_id}/assets.json
- "List all assets.json?" -> GET /admin/api/2020-07/themes/{theme_id}/assets.json
- "List all assets.json?" -> GET /admin/api/2020-10/themes/{theme_id}/assets.json
- "List all assets.json?" -> GET /admin/api/2021-01/themes/{theme_id}/assets.json
- "List all assets.json?" -> GET /admin/api/unstable/themes/{theme_id}/assets.json
- "List all blogs.json?" -> GET /admin/api/2020-01/blogs.json
- "Create a blogs.json?" -> POST /admin/api/2020-01/blogs.json
- "List all count.json?" -> GET /admin/api/2020-01/blogs/count.json
- "Get blog details?" -> GET /admin/api/2020-01/blogs/{blog_id}.json
- "Update a blog?" -> PUT /admin/api/2020-01/blogs/{blog_id}.json
- "Delete a blog?" -> DELETE /admin/api/2020-01/blogs/{blog_id}.json
- "List all comments.json?" -> GET /admin/api/2020-01/comments.json
- "Create a comments.json?" -> POST /admin/api/2020-01/comments.json
- "List all count.json?" -> GET /admin/api/2020-01/comments/count.json
- "Get comment details?" -> GET /admin/api/2020-01/comments/{comment_id}.json
- "Update a comment?" -> PUT /admin/api/2020-01/comments/{comment_id}.json
- "Create a spam.json?" -> POST /admin/api/2020-01/comments/{comment_id}/spam.json
- "Create a not_spam.json?" -> POST /admin/api/2020-01/comments/{comment_id}/not_spam.json
- "Create a approve.json?" -> POST /admin/api/2020-01/comments/{comment_id}/approve.json
- "Create a remove.json?" -> POST /admin/api/2020-01/comments/{comment_id}/remove.json
- "Create a restore.json?" -> POST /admin/api/2020-01/comments/{comment_id}/restore.json
- "List all redirects.json?" -> GET /admin/api/2020-01/redirects.json
- "Create a redirects.json?" -> POST /admin/api/2020-01/redirects.json
- "List all count.json?" -> GET /admin/api/2020-01/redirects/count.json
- "Get redirect details?" -> GET /admin/api/2020-01/redirects/{redirect_id}.json
- "Update a redirect?" -> PUT /admin/api/2020-01/redirects/{redirect_id}.json
- "Delete a redirect?" -> DELETE /admin/api/2020-01/redirects/{redirect_id}.json
- "List all redirects.json?" -> GET /admin/api/2020-04/redirects.json
- "Create a redirects.json?" -> POST /admin/api/2020-04/redirects.json
- "List all count.json?" -> GET /admin/api/2020-04/redirects/count.json
- "Get redirect details?" -> GET /admin/api/2020-04/redirects/{redirect_id}.json
- "Update a redirect?" -> PUT /admin/api/2020-04/redirects/{redirect_id}.json
- "Delete a redirect?" -> DELETE /admin/api/2020-04/redirects/{redirect_id}.json
- "List all redirects.json?" -> GET /admin/api/2020-07/redirects.json
- "Create a redirects.json?" -> POST /admin/api/2020-07/redirects.json
- "List all count.json?" -> GET /admin/api/2020-07/redirects/count.json
- "Get redirect details?" -> GET /admin/api/2020-07/redirects/{redirect_id}.json
- "Update a redirect?" -> PUT /admin/api/2020-07/redirects/{redirect_id}.json
- "Delete a redirect?" -> DELETE /admin/api/2020-07/redirects/{redirect_id}.json
- "List all redirects.json?" -> GET /admin/api/2020-10/redirects.json
- "Create a redirects.json?" -> POST /admin/api/2020-10/redirects.json
- "List all count.json?" -> GET /admin/api/2020-10/redirects/count.json
- "Get redirect details?" -> GET /admin/api/2020-10/redirects/{redirect_id}.json
- "Update a redirect?" -> PUT /admin/api/2020-10/redirects/{redirect_id}.json
- "Delete a redirect?" -> DELETE /admin/api/2020-10/redirects/{redirect_id}.json
- "List all redirects.json?" -> GET /admin/api/2021-01/redirects.json
- "Create a redirects.json?" -> POST /admin/api/2021-01/redirects.json
- "List all count.json?" -> GET /admin/api/2021-01/redirects/count.json
- "Get redirect details?" -> GET /admin/api/2021-01/redirects/{redirect_id}.json
- "Update a redirect?" -> PUT /admin/api/2021-01/redirects/{redirect_id}.json
- "Delete a redirect?" -> DELETE /admin/api/2021-01/redirects/{redirect_id}.json
- "List all redirects.json?" -> GET /admin/api/unstable/redirects.json
- "Create a redirects.json?" -> POST /admin/api/unstable/redirects.json
- "List all count.json?" -> GET /admin/api/unstable/redirects/count.json
- "Get redirect details?" -> GET /admin/api/unstable/redirects/{redirect_id}.json
- "Update a redirect?" -> PUT /admin/api/unstable/redirects/{redirect_id}.json
- "Delete a redirect?" -> DELETE /admin/api/unstable/redirects/{redirect_id}.json
- "List all script_tags.json?" -> GET /admin/api/2020-01/script_tags.json
- "Create a script_tags.json?" -> POST /admin/api/2020-01/script_tags.json
- "List all count.json?" -> GET /admin/api/2020-01/script_tags/count.json
- "Get script_tag details?" -> GET /admin/api/2020-01/script_tags/{script_tag_id}.json
- "Update a script_tag?" -> PUT /admin/api/2020-01/script_tags/{script_tag_id}.json
- "Delete a script_tag?" -> DELETE /admin/api/2020-01/script_tags/{script_tag_id}.json
- "List all script_tags.json?" -> GET /admin/api/2020-04/script_tags.json
- "Create a script_tags.json?" -> POST /admin/api/2020-04/script_tags.json
- "List all count.json?" -> GET /admin/api/2020-04/script_tags/count.json
- "Get script_tag details?" -> GET /admin/api/2020-04/script_tags/{script_tag_id}.json
- "Update a script_tag?" -> PUT /admin/api/2020-04/script_tags/{script_tag_id}.json
- "Delete a script_tag?" -> DELETE /admin/api/2020-04/script_tags/{script_tag_id}.json
- "List all script_tags.json?" -> GET /admin/api/2020-07/script_tags.json
- "Create a script_tags.json?" -> POST /admin/api/2020-07/script_tags.json
- "List all count.json?" -> GET /admin/api/2020-07/script_tags/count.json
- "Get script_tag details?" -> GET /admin/api/2020-07/script_tags/{script_tag_id}.json
- "Update a script_tag?" -> PUT /admin/api/2020-07/script_tags/{script_tag_id}.json
- "Delete a script_tag?" -> DELETE /admin/api/2020-07/script_tags/{script_tag_id}.json
- "List all script_tags.json?" -> GET /admin/api/2020-10/script_tags.json
- "Create a script_tags.json?" -> POST /admin/api/2020-10/script_tags.json
- "List all count.json?" -> GET /admin/api/2020-10/script_tags/count.json
- "Get script_tag details?" -> GET /admin/api/2020-10/script_tags/{script_tag_id}.json
- "Update a script_tag?" -> PUT /admin/api/2020-10/script_tags/{script_tag_id}.json
- "Delete a script_tag?" -> DELETE /admin/api/2020-10/script_tags/{script_tag_id}.json
- "List all script_tags.json?" -> GET /admin/api/2021-01/script_tags.json
- "Create a script_tags.json?" -> POST /admin/api/2021-01/script_tags.json
- "List all count.json?" -> GET /admin/api/2021-01/script_tags/count.json
- "Get script_tag details?" -> GET /admin/api/2021-01/script_tags/{script_tag_id}.json
- "Update a script_tag?" -> PUT /admin/api/2021-01/script_tags/{script_tag_id}.json
- "Delete a script_tag?" -> DELETE /admin/api/2021-01/script_tags/{script_tag_id}.json
- "List all script_tags.json?" -> GET /admin/api/unstable/script_tags.json
- "Create a script_tags.json?" -> POST /admin/api/unstable/script_tags.json
- "List all count.json?" -> GET /admin/api/unstable/script_tags/count.json
- "Get script_tag details?" -> GET /admin/api/unstable/script_tags/{script_tag_id}.json
- "Update a script_tag?" -> PUT /admin/api/unstable/script_tags/{script_tag_id}.json
- "Delete a script_tag?" -> DELETE /admin/api/unstable/script_tags/{script_tag_id}.json
- "List all themes.json?" -> GET /admin/api/2020-01/themes.json
- "Create a themes.json?" -> POST /admin/api/2020-01/themes.json
- "Get theme details?" -> GET /admin/api/2020-01/themes/{theme_id}.json
- "Update a theme?" -> PUT /admin/api/2020-01/themes/{theme_id}.json
- "Delete a theme?" -> DELETE /admin/api/2020-01/themes/{theme_id}.json
- "List all themes.json?" -> GET /admin/api/2020-04/themes.json
- "Create a themes.json?" -> POST /admin/api/2020-04/themes.json
- "Get theme details?" -> GET /admin/api/2020-04/themes/{theme_id}.json
- "Update a theme?" -> PUT /admin/api/2020-04/themes/{theme_id}.json
- "Delete a theme?" -> DELETE /admin/api/2020-04/themes/{theme_id}.json
- "List all themes.json?" -> GET /admin/api/2020-07/themes.json
- "Create a themes.json?" -> POST /admin/api/2020-07/themes.json
- "Get theme details?" -> GET /admin/api/2020-07/themes/{theme_id}.json
- "Update a theme?" -> PUT /admin/api/2020-07/themes/{theme_id}.json
- "Delete a theme?" -> DELETE /admin/api/2020-07/themes/{theme_id}.json
- "List all themes.json?" -> GET /admin/api/2020-10/themes.json
- "Create a themes.json?" -> POST /admin/api/2020-10/themes.json
- "Get theme details?" -> GET /admin/api/2020-10/themes/{theme_id}.json
- "Update a theme?" -> PUT /admin/api/2020-10/themes/{theme_id}.json
- "Delete a theme?" -> DELETE /admin/api/2020-10/themes/{theme_id}.json
- "List all themes.json?" -> GET /admin/api/2021-01/themes.json
- "Create a themes.json?" -> POST /admin/api/2021-01/themes.json
- "Get theme details?" -> GET /admin/api/2021-01/themes/{theme_id}.json
- "Update a theme?" -> PUT /admin/api/2021-01/themes/{theme_id}.json
- "Delete a theme?" -> DELETE /admin/api/2021-01/themes/{theme_id}.json
- "List all themes.json?" -> GET /admin/api/unstable/themes.json
- "Create a themes.json?" -> POST /admin/api/unstable/themes.json
- "Get theme details?" -> GET /admin/api/unstable/themes/{theme_id}.json
- "Update a theme?" -> PUT /admin/api/unstable/themes/{theme_id}.json
- "Delete a theme?" -> DELETE /admin/api/unstable/themes/{theme_id}.json
- "List all count.json?" -> GET /admin/api/2020-01/checkouts/count.json
- "Create a checkouts.json?" -> POST /admin/api/2020-01/checkouts.json
- "List all count.json?" -> GET /admin/api/2020-04/checkouts/count.json
- "Create a checkouts.json?" -> POST /admin/api/2020-04/checkouts.json
- "List all count.json?" -> GET /admin/api/2020-07/checkouts/count.json
- "Create a checkouts.json?" -> POST /admin/api/2020-07/checkouts.json
- "List all count.json?" -> GET /admin/api/2020-10/checkouts/count.json
- "Create a checkouts.json?" -> POST /admin/api/2020-10/checkouts.json
- "List all count.json?" -> GET /admin/api/2021-01/checkouts/count.json
- "Create a checkouts.json?" -> POST /admin/api/2021-01/checkouts.json
- "List all count.json?" -> GET /admin/api/unstable/checkouts/count.json
- "Create a checkouts.json?" -> POST /admin/api/unstable/checkouts.json
- "List all orders.json?" -> GET /admin/api/2020-01/orders.json
- "Create a orders.json?" -> POST /admin/api/2020-01/orders.json
- "Get order details?" -> GET /admin/api/2020-01/orders/{order_id}.json
- "Update a order?" -> PUT /admin/api/2020-01/orders/{order_id}.json
- "Delete a order?" -> DELETE /admin/api/2020-01/orders/{order_id}.json
- "List all count.json?" -> GET /admin/api/2020-01/orders/count.json
- "Create a close.json?" -> POST /admin/api/2020-01/orders/{order_id}/close.json
- "Create a open.json?" -> POST /admin/api/2020-01/orders/{order_id}/open.json
- "Create a cancel.json?" -> POST /admin/api/2020-01/orders/{order_id}/cancel.json
- "List all orders.json?" -> GET /admin/api/2020-04/orders.json
- "Create a orders.json?" -> POST /admin/api/2020-04/orders.json
- "Get order details?" -> GET /admin/api/2020-04/orders/{order_id}.json
- "Update a order?" -> PUT /admin/api/2020-04/orders/{order_id}.json
- "Delete a order?" -> DELETE /admin/api/2020-04/orders/{order_id}.json
- "List all count.json?" -> GET /admin/api/2020-04/orders/count.json
- "Create a close.json?" -> POST /admin/api/2020-04/orders/{order_id}/close.json
- "Create a open.json?" -> POST /admin/api/2020-04/orders/{order_id}/open.json
- "Create a cancel.json?" -> POST /admin/api/2020-04/orders/{order_id}/cancel.json
- "List all orders.json?" -> GET /admin/api/2020-07/orders.json
- "Create a risks.json?" -> POST /admin/api/2020-01/orders/{order_id}/risks.json
- "List all risks.json?" -> GET /admin/api/2020-01/orders/{order_id}/risks.json
- "Get risk details?" -> GET /admin/api/2020-01/orders/{order_id}/risks/{risk_id}.json
- "Update a risk?" -> PUT /admin/api/2020-01/orders/{order_id}/risks/{risk_id}.json
- "Delete a risk?" -> DELETE /admin/api/2020-01/orders/{order_id}/risks/{risk_id}.json
- "Create a risks.json?" -> POST /admin/api/2020-04/orders/{order_id}/risks.json
- "List all risks.json?" -> GET /admin/api/2020-04/orders/{order_id}/risks.json
- "Get risk details?" -> GET /admin/api/2020-04/orders/{order_id}/risks/{risk_id}.json
- "Update a risk?" -> PUT /admin/api/2020-04/orders/{order_id}/risks/{risk_id}.json
- "Delete a risk?" -> DELETE /admin/api/2020-04/orders/{order_id}/risks/{risk_id}.json
- "Create a risks.json?" -> POST /admin/api/2020-07/orders/{order_id}/risks.json
- "List all risks.json?" -> GET /admin/api/2020-07/orders/{order_id}/risks.json
- "Get risk details?" -> GET /admin/api/2020-07/orders/{order_id}/risks/{risk_id}.json
- "Update a risk?" -> PUT /admin/api/2020-07/orders/{order_id}/risks/{risk_id}.json
- "Delete a risk?" -> DELETE /admin/api/2020-07/orders/{order_id}/risks/{risk_id}.json
- "Create a risks.json?" -> POST /admin/api/2020-10/orders/{order_id}/risks.json
- "List all risks.json?" -> GET /admin/api/2020-10/orders/{order_id}/risks.json
- "Get risk details?" -> GET /admin/api/2020-10/orders/{order_id}/risks/{risk_id}.json
- "Update a risk?" -> PUT /admin/api/2020-10/orders/{order_id}/risks/{risk_id}.json
- "Delete a risk?" -> DELETE /admin/api/2020-10/orders/{order_id}/risks/{risk_id}.json
- "Create a risks.json?" -> POST /admin/api/2021-01/orders/{order_id}/risks.json
- "List all risks.json?" -> GET /admin/api/2021-01/orders/{order_id}/risks.json
- "Get risk details?" -> GET /admin/api/2021-01/orders/{order_id}/risks/{risk_id}.json
- "Update a risk?" -> PUT /admin/api/2021-01/orders/{order_id}/risks/{risk_id}.json
- "Delete a risk?" -> DELETE /admin/api/2021-01/orders/{order_id}/risks/{risk_id}.json
- "Create a risks.json?" -> POST /admin/api/unstable/orders/{order_id}/risks.json
- "List all risks.json?" -> GET /admin/api/unstable/orders/{order_id}/risks.json
- "Get risk details?" -> GET /admin/api/unstable/orders/{order_id}/risks/{risk_id}.json
- "Update a risk?" -> PUT /admin/api/unstable/orders/{order_id}/risks/{risk_id}.json
- "Delete a risk?" -> DELETE /admin/api/unstable/orders/{order_id}/risks/{risk_id}.json
- "List all refunds.json?" -> GET /admin/api/2020-01/orders/{order_id}/refunds.json
- "Create a refunds.json?" -> POST /admin/api/2020-01/orders/{order_id}/refunds.json
- "Get refund details?" -> GET /admin/api/2020-01/orders/{order_id}/refunds/{refund_id}.json
- "Create a calculate.json?" -> POST /admin/api/2020-01/orders/{order_id}/refunds/calculate.json
- "List all refunds.json?" -> GET /admin/api/2020-04/orders/{order_id}/refunds.json
- "Create a refunds.json?" -> POST /admin/api/2020-04/orders/{order_id}/refunds.json
- "Get refund details?" -> GET /admin/api/2020-04/orders/{order_id}/refunds/{refund_id}.json
- "Create a calculate.json?" -> POST /admin/api/2020-04/orders/{order_id}/refunds/calculate.json
- "List all refunds.json?" -> GET /admin/api/2020-07/orders/{order_id}/refunds.json
- "Create a refunds.json?" -> POST /admin/api/2020-07/orders/{order_id}/refunds.json
- "Get refund details?" -> GET /admin/api/2020-07/orders/{order_id}/refunds/{refund_id}.json
- "Create a calculate.json?" -> POST /admin/api/2020-07/orders/{order_id}/refunds/calculate.json
- "List all refunds.json?" -> GET /admin/api/2020-10/orders/{order_id}/refunds.json
- "Create a refunds.json?" -> POST /admin/api/2020-10/orders/{order_id}/refunds.json
- "Get refund details?" -> GET /admin/api/2020-10/orders/{order_id}/refunds/{refund_id}.json
- "Create a calculate.json?" -> POST /admin/api/2020-10/orders/{order_id}/refunds/calculate.json
- "List all refunds.json?" -> GET /admin/api/2021-01/orders/{order_id}/refunds.json
- "Create a refunds.json?" -> POST /admin/api/2021-01/orders/{order_id}/refunds.json
- "Get refund details?" -> GET /admin/api/2021-01/orders/{order_id}/refunds/{refund_id}.json
- "Create a calculate.json?" -> POST /admin/api/2021-01/orders/{order_id}/refunds/calculate.json
- "List all refunds.json?" -> GET /admin/api/unstable/orders/{order_id}/refunds.json
- "Create a refunds.json?" -> POST /admin/api/unstable/orders/{order_id}/refunds.json
- "Get refund details?" -> GET /admin/api/unstable/orders/{order_id}/refunds/{refund_id}.json
- "Create a calculate.json?" -> POST /admin/api/unstable/orders/{order_id}/refunds/calculate.json
- "List all gift_cards.json?" -> GET /admin/api/2020-01/gift_cards.json
- "Create a gift_cards.json?" -> POST /admin/api/2020-01/gift_cards.json
- "Get gift_card details?" -> GET /admin/api/2020-01/gift_cards/{gift_card_id}.json
- "Update a gift_card?" -> PUT /admin/api/2020-01/gift_cards/{gift_card_id}.json
- "List all count.json?" -> GET /admin/api/2020-01/gift_cards/count.json
- "Create a disable.json?" -> POST /admin/api/2020-01/gift_cards/{gift_card_id}/disable.json
- "Search search.json?" -> GET /admin/api/2020-01/gift_cards/search.json
- "List all gift_cards.json?" -> GET /admin/api/2020-04/gift_cards.json
- "Create a gift_cards.json?" -> POST /admin/api/2020-04/gift_cards.json
- "Get gift_card details?" -> GET /admin/api/2020-04/gift_cards/{gift_card_id}.json
- "Update a gift_card?" -> PUT /admin/api/2020-04/gift_cards/{gift_card_id}.json
- "List all count.json?" -> GET /admin/api/2020-04/gift_cards/count.json
- "Create a disable.json?" -> POST /admin/api/2020-04/gift_cards/{gift_card_id}/disable.json
- "Search search.json?" -> GET /admin/api/2020-04/gift_cards/search.json
- "List all gift_cards.json?" -> GET /admin/api/2020-07/gift_cards.json
- "Create a gift_cards.json?" -> POST /admin/api/2020-07/gift_cards.json
- "Get gift_card details?" -> GET /admin/api/2020-07/gift_cards/{gift_card_id}.json
- "Update a gift_card?" -> PUT /admin/api/2020-07/gift_cards/{gift_card_id}.json
- "List all count.json?" -> GET /admin/api/2020-07/gift_cards/count.json
- "Create a disable.json?" -> POST /admin/api/2020-07/gift_cards/{gift_card_id}/disable.json
- "Search search.json?" -> GET /admin/api/2020-07/gift_cards/search.json
- "List all gift_cards.json?" -> GET /admin/api/2020-10/gift_cards.json
- "Create a gift_cards.json?" -> POST /admin/api/2020-10/gift_cards.json
- "Get gift_card details?" -> GET /admin/api/2020-10/gift_cards/{gift_card_id}.json
- "Update a gift_card?" -> PUT /admin/api/2020-10/gift_cards/{gift_card_id}.json
- "List all count.json?" -> GET /admin/api/2020-10/gift_cards/count.json
- "Create a disable.json?" -> POST /admin/api/2020-10/gift_cards/{gift_card_id}/disable.json
- "Search search.json?" -> GET /admin/api/2020-10/gift_cards/search.json
- "List all gift_cards.json?" -> GET /admin/api/2021-01/gift_cards.json
- "Create a gift_cards.json?" -> POST /admin/api/2021-01/gift_cards.json
- "Get gift_card details?" -> GET /admin/api/2021-01/gift_cards/{gift_card_id}.json
- "Update a gift_card?" -> PUT /admin/api/2021-01/gift_cards/{gift_card_id}.json
- "List all count.json?" -> GET /admin/api/2021-01/gift_cards/count.json
- "Create a disable.json?" -> POST /admin/api/2021-01/gift_cards/{gift_card_id}/disable.json
- "Search search.json?" -> GET /admin/api/2021-01/gift_cards/search.json
- "List all gift_cards.json?" -> GET /admin/api/unstable/gift_cards.json
- "Create a gift_cards.json?" -> POST /admin/api/unstable/gift_cards.json
- "Get gift_card details?" -> GET /admin/api/unstable/gift_cards/{gift_card_id}.json
- "Update a gift_card?" -> PUT /admin/api/unstable/gift_cards/{gift_card_id}.json
- "List all count.json?" -> GET /admin/api/unstable/gift_cards/count.json
- "Create a disable.json?" -> POST /admin/api/unstable/gift_cards/{gift_card_id}/disable.json
- "Search search.json?" -> GET /admin/api/unstable/gift_cards/search.json
- "List all users.json?" -> GET /admin/api/2020-01/users.json
- "Get user details?" -> GET /admin/api/2020-01/users/{user_id}.json
- "List all current.json?" -> GET /admin/api/2020-01/users/current.json
- "List all users.json?" -> GET /admin/api/2020-04/users.json
- "Get user details?" -> GET /admin/api/2020-04/users/{user_id}.json
- "List all current.json?" -> GET /admin/api/2020-04/users/current.json
- "List all users.json?" -> GET /admin/api/2020-07/users.json
- "Get user details?" -> GET /admin/api/2020-07/users/{user_id}.json
- "List all current.json?" -> GET /admin/api/2020-07/users/current.json
- "List all users.json?" -> GET /admin/api/2020-10/users.json
- "Get user details?" -> GET /admin/api/2020-10/users/{user_id}.json
- "List all current.json?" -> GET /admin/api/2020-10/users/current.json
- "List all users.json?" -> GET /admin/api/2021-01/users.json
- "Get user details?" -> GET /admin/api/2021-01/users/{user_id}.json
- "List all current.json?" -> GET /admin/api/2021-01/users/current.json
- "List all users.json?" -> GET /admin/api/unstable/users.json
- "Get user details?" -> GET /admin/api/unstable/users/{user_id}.json
- "List all current.json?" -> GET /admin/api/unstable/users/current.json
- "Create a collects.json?" -> POST /admin/api/2020-01/collects.json
- "List all collects.json?" -> GET /admin/api/2020-01/collects.json
- "Delete a collect?" -> DELETE /admin/api/2020-01/collects/{collect_id}.json
- "Get collect details?" -> GET /admin/api/2020-01/collects/{collect_id}.json
- "List all count.json?" -> GET /admin/api/2020-01/collects/count.json
- "Create a collects.json?" -> POST /admin/api/2020-04/collects.json
- "List all collects.json?" -> GET /admin/api/2020-04/collects.json
- "Delete a collect?" -> DELETE /admin/api/2020-04/collects/{collect_id}.json
- "Get collect details?" -> GET /admin/api/2020-04/collects/{collect_id}.json
- "List all count.json?" -> GET /admin/api/2020-04/collects/count.json
- "Create a collects.json?" -> POST /admin/api/2020-07/collects.json
- "List all collects.json?" -> GET /admin/api/2020-07/collects.json
- "Delete a collect?" -> DELETE /admin/api/2020-07/collects/{collect_id}.json
- "Get collect details?" -> GET /admin/api/2020-07/collects/{collect_id}.json
- "List all count.json?" -> GET /admin/api/2020-07/collects/count.json
- "Create a collects.json?" -> POST /admin/api/2020-10/collects.json
- "List all collects.json?" -> GET /admin/api/2020-10/collects.json
- "Delete a collect?" -> DELETE /admin/api/2020-10/collects/{collect_id}.json
- "Get collect details?" -> GET /admin/api/2020-10/collects/{collect_id}.json
- "List all count.json?" -> GET /admin/api/2020-10/collects/count.json
- "Create a collects.json?" -> POST /admin/api/2021-01/collects.json
- "List all collects.json?" -> GET /admin/api/2021-01/collects.json
- "Delete a collect?" -> DELETE /admin/api/2021-01/collects/{collect_id}.json
- "Get collect details?" -> GET /admin/api/2021-01/collects/{collect_id}.json
- "List all count.json?" -> GET /admin/api/2021-01/collects/count.json
- "Create a collects.json?" -> POST /admin/api/unstable/collects.json
- "List all collects.json?" -> GET /admin/api/unstable/collects.json
- "Delete a collect?" -> DELETE /admin/api/unstable/collects/{collect_id}.json
- "Get collect details?" -> GET /admin/api/unstable/collects/{collect_id}.json
- "List all count.json?" -> GET /admin/api/unstable/collects/count.json
- "Get collection details?" -> GET /admin/api/2020-01/collections/{collection_id}.json
- "List all products.json?" -> GET /admin/api/2020-01/collections/{collection_id}/products.json
- "Get collection details?" -> GET /admin/api/2020-04/collections/{collection_id}.json
- "List all products.json?" -> GET /admin/api/2020-04/collections/{collection_id}/products.json
- "Get collection details?" -> GET /admin/api/2020-07/collections/{collection_id}.json
- "List all products.json?" -> GET /admin/api/2020-07/collections/{collection_id}/products.json
- "Get collection details?" -> GET /admin/api/2020-10/collections/{collection_id}.json
- "List all products.json?" -> GET /admin/api/2020-10/collections/{collection_id}/products.json
- "Get collection details?" -> GET /admin/api/2021-01/collections/{collection_id}.json
- "List all products.json?" -> GET /admin/api/2021-01/collections/{collection_id}/products.json
- "Get collection details?" -> GET /admin/api/unstable/collections/{collection_id}.json
- "List all products.json?" -> GET /admin/api/unstable/collections/{collection_id}/products.json
- "List all custom_collections.json?" -> GET /admin/api/2020-01/custom_collections.json
- "Create a custom_collections.json?" -> POST /admin/api/2020-01/custom_collections.json
- "List all count.json?" -> GET /admin/api/2020-01/custom_collections/count.json
- "Get custom_collection details?" -> GET /admin/api/2020-01/custom_collections/{custom_collection_id}.json
- "Update a custom_collection?" -> PUT /admin/api/2020-01/custom_collections/{custom_collection_id}.json
- "Delete a custom_collection?" -> DELETE /admin/api/2020-01/custom_collections/{custom_collection_id}.json
- "List all custom_collections.json?" -> GET /admin/api/2020-04/custom_collections.json
- "Create a custom_collections.json?" -> POST /admin/api/2020-04/custom_collections.json
- "List all count.json?" -> GET /admin/api/2020-04/custom_collections/count.json
- "Get custom_collection details?" -> GET /admin/api/2020-04/custom_collections/{custom_collection_id}.json
- "Update a custom_collection?" -> PUT /admin/api/2020-04/custom_collections/{custom_collection_id}.json
- "Delete a custom_collection?" -> DELETE /admin/api/2020-04/custom_collections/{custom_collection_id}.json
- "List all custom_collections.json?" -> GET /admin/api/2020-07/custom_collections.json
- "Create a custom_collections.json?" -> POST /admin/api/2020-07/custom_collections.json
- "List all count.json?" -> GET /admin/api/2020-07/custom_collections/count.json
- "Get custom_collection details?" -> GET /admin/api/2020-07/custom_collections/{custom_collection_id}.json
- "Update a custom_collection?" -> PUT /admin/api/2020-07/custom_collections/{custom_collection_id}.json
- "Delete a custom_collection?" -> DELETE /admin/api/2020-07/custom_collections/{custom_collection_id}.json
- "List all custom_collections.json?" -> GET /admin/api/2020-10/custom_collections.json
- "Create a custom_collections.json?" -> POST /admin/api/2020-10/custom_collections.json
- "List all count.json?" -> GET /admin/api/2020-10/custom_collections/count.json
- "Get custom_collection details?" -> GET /admin/api/2020-10/custom_collections/{custom_collection_id}.json
- "Update a custom_collection?" -> PUT /admin/api/2020-10/custom_collections/{custom_collection_id}.json
- "Delete a custom_collection?" -> DELETE /admin/api/2020-10/custom_collections/{custom_collection_id}.json
- "List all custom_collections.json?" -> GET /admin/api/2021-01/custom_collections.json
- "Create a custom_collections.json?" -> POST /admin/api/2021-01/custom_collections.json
- "List all count.json?" -> GET /admin/api/2021-01/custom_collections/count.json
- "Get custom_collection details?" -> GET /admin/api/2021-01/custom_collections/{custom_collection_id}.json
- "Update a custom_collection?" -> PUT /admin/api/2021-01/custom_collections/{custom_collection_id}.json
- "Delete a custom_collection?" -> DELETE /admin/api/2021-01/custom_collections/{custom_collection_id}.json
- "List all custom_collections.json?" -> GET /admin/api/unstable/custom_collections.json
- "Create a custom_collections.json?" -> POST /admin/api/unstable/custom_collections.json
- "List all count.json?" -> GET /admin/api/unstable/custom_collections/count.json
- "Get custom_collection details?" -> GET /admin/api/unstable/custom_collections/{custom_collection_id}.json
- "Update a custom_collection?" -> PUT /admin/api/unstable/custom_collections/{custom_collection_id}.json
- "Delete a custom_collection?" -> DELETE /admin/api/unstable/custom_collections/{custom_collection_id}.json
- "List all products.json?" -> GET /admin/api/2020-01/products.json
- "Create a products.json?" -> POST /admin/api/2020-01/products.json
- "List all count.json?" -> GET /admin/api/2020-01/products/count.json
- "Get product details?" -> GET /admin/api/2020-01/products/{product_id}.json
- "Update a product?" -> PUT /admin/api/2020-01/products/{product_id}.json
- "Delete a product?" -> DELETE /admin/api/2020-01/products/{product_id}.json
- "List all products.json?" -> GET /admin/api/2020-04/products.json
- "Create a products.json?" -> POST /admin/api/2020-04/products.json
- "List all count.json?" -> GET /admin/api/2020-04/products/count.json
- "Get product details?" -> GET /admin/api/2020-04/products/{product_id}.json
- "Update a product?" -> PUT /admin/api/2020-04/products/{product_id}.json
- "Delete a product?" -> DELETE /admin/api/2020-04/products/{product_id}.json
- "List all products.json?" -> GET /admin/api/2020-07/products.json
- "Create a products.json?" -> POST /admin/api/2020-07/products.json
- "List all count.json?" -> GET /admin/api/2020-07/products/count.json
- "Get product details?" -> GET /admin/api/2020-07/products/{product_id}.json
- "Update a product?" -> PUT /admin/api/2020-07/products/{product_id}.json
- "Delete a product?" -> DELETE /admin/api/2020-07/products/{product_id}.json
- "List all products.json?" -> GET /admin/api/2020-10/products.json
- "Create a products.json?" -> POST /admin/api/2020-10/products.json
- "List all count.json?" -> GET /admin/api/2020-10/products/count.json
- "Get product details?" -> GET /admin/api/2020-10/products/{product_id}.json
- "Update a product?" -> PUT /admin/api/2020-10/products/{product_id}.json
- "Delete a product?" -> DELETE /admin/api/2020-10/products/{product_id}.json
- "List all products.json?" -> GET /admin/api/2021-01/products.json
- "Create a products.json?" -> POST /admin/api/2021-01/products.json
- "List all count.json?" -> GET /admin/api/2021-01/products/count.json
- "Get product details?" -> GET /admin/api/2021-01/products/{product_id}.json
- "Update a product?" -> PUT /admin/api/2021-01/products/{product_id}.json
- "Delete a product?" -> DELETE /admin/api/2021-01/products/{product_id}.json
- "List all products.json?" -> GET /admin/api/unstable/products.json
- "Create a products.json?" -> POST /admin/api/unstable/products.json
- "List all count.json?" -> GET /admin/api/unstable/products/count.json
- "Get product details?" -> GET /admin/api/unstable/products/{product_id}.json
- "Update a product?" -> PUT /admin/api/unstable/products/{product_id}.json
- "Delete a product?" -> DELETE /admin/api/unstable/products/{product_id}.json
- "List all images.json?" -> GET /admin/api/2020-01/products/{product_id}/images.json
- "Create a images.json?" -> POST /admin/api/2020-01/products/{product_id}/images.json
- "List all count.json?" -> GET /admin/api/2020-01/products/{product_id}/images/count.json
- "Get image details?" -> GET /admin/api/2020-01/products/{product_id}/images/{image_id}.json
- "Update a image?" -> PUT /admin/api/2020-01/products/{product_id}/images/{image_id}.json
- "Delete a image?" -> DELETE /admin/api/2020-01/products/{product_id}/images/{image_id}.json
- "List all images.json?" -> GET /admin/api/2020-04/products/{product_id}/images.json
- "Create a images.json?" -> POST /admin/api/2020-04/products/{product_id}/images.json
- "List all count.json?" -> GET /admin/api/2020-04/products/{product_id}/images/count.json
- "Get image details?" -> GET /admin/api/2020-04/products/{product_id}/images/{image_id}.json
- "Update a image?" -> PUT /admin/api/2020-04/products/{product_id}/images/{image_id}.json
- "Delete a image?" -> DELETE /admin/api/2020-04/products/{product_id}/images/{image_id}.json
- "List all images.json?" -> GET /admin/api/2020-07/products/{product_id}/images.json
- "Create a images.json?" -> POST /admin/api/2020-07/products/{product_id}/images.json
- "List all count.json?" -> GET /admin/api/2020-07/products/{product_id}/images/count.json
- "Get image details?" -> GET /admin/api/2020-07/products/{product_id}/images/{image_id}.json
- "Update a image?" -> PUT /admin/api/2020-07/products/{product_id}/images/{image_id}.json
- "Delete a image?" -> DELETE /admin/api/2020-07/products/{product_id}/images/{image_id}.json
- "List all images.json?" -> GET /admin/api/2020-10/products/{product_id}/images.json
- "Create a images.json?" -> POST /admin/api/2020-10/products/{product_id}/images.json
- "List all count.json?" -> GET /admin/api/2020-10/products/{product_id}/images/count.json
- "Get image details?" -> GET /admin/api/2020-10/products/{product_id}/images/{image_id}.json
- "Update a image?" -> PUT /admin/api/2020-10/products/{product_id}/images/{image_id}.json
- "Delete a image?" -> DELETE /admin/api/2020-10/products/{product_id}/images/{image_id}.json
- "List all images.json?" -> GET /admin/api/2021-01/products/{product_id}/images.json
- "Create a images.json?" -> POST /admin/api/2021-01/products/{product_id}/images.json
- "List all count.json?" -> GET /admin/api/2021-01/products/{product_id}/images/count.json
- "Get image details?" -> GET /admin/api/2021-01/products/{product_id}/images/{image_id}.json
- "Update a image?" -> PUT /admin/api/2021-01/products/{product_id}/images/{image_id}.json
- "Delete a image?" -> DELETE /admin/api/2021-01/products/{product_id}/images/{image_id}.json
- "List all images.json?" -> GET /admin/api/unstable/products/{product_id}/images.json
- "Create a images.json?" -> POST /admin/api/unstable/products/{product_id}/images.json
- "List all count.json?" -> GET /admin/api/unstable/products/{product_id}/images/count.json
- "Get image details?" -> GET /admin/api/unstable/products/{product_id}/images/{image_id}.json
- "Update a image?" -> PUT /admin/api/unstable/products/{product_id}/images/{image_id}.json
- "Delete a image?" -> DELETE /admin/api/unstable/products/{product_id}/images/{image_id}.json
- "List all smart_collections.json?" -> GET /admin/api/2020-01/smart_collections.json
- "Create a smart_collections.json?" -> POST /admin/api/2020-01/smart_collections.json
- "List all count.json?" -> GET /admin/api/2020-01/smart_collections/count.json
- "Get smart_collection details?" -> GET /admin/api/2020-01/smart_collections/{smart_collection_id}.json
- "Update a smart_collection?" -> PUT /admin/api/2020-01/smart_collections/{smart_collection_id}.json
- "Delete a smart_collection?" -> DELETE /admin/api/2020-01/smart_collections/{smart_collection_id}.json
- "List all smart_collections.json?" -> GET /admin/api/2020-04/smart_collections.json
- "Create a smart_collections.json?" -> POST /admin/api/2020-04/smart_collections.json
- "List all count.json?" -> GET /admin/api/2020-04/smart_collections/count.json
- "Get smart_collection details?" -> GET /admin/api/2020-04/smart_collections/{smart_collection_id}.json
- "Update a smart_collection?" -> PUT /admin/api/2020-04/smart_collections/{smart_collection_id}.json
- "Delete a smart_collection?" -> DELETE /admin/api/2020-04/smart_collections/{smart_collection_id}.json
- "List all smart_collections.json?" -> GET /admin/api/2020-07/smart_collections.json
- "Create a smart_collections.json?" -> POST /admin/api/2020-07/smart_collections.json
- "List all count.json?" -> GET /admin/api/2020-07/smart_collections/count.json
- "Get smart_collection details?" -> GET /admin/api/2020-07/smart_collections/{smart_collection_id}.json
- "Update a smart_collection?" -> PUT /admin/api/2020-07/smart_collections/{smart_collection_id}.json
- "Delete a smart_collection?" -> DELETE /admin/api/2020-07/smart_collections/{smart_collection_id}.json
- "List all smart_collections.json?" -> GET /admin/api/2020-10/smart_collections.json
- "Create a smart_collections.json?" -> POST /admin/api/2020-10/smart_collections.json
- "List all count.json?" -> GET /admin/api/2020-10/smart_collections/count.json
- "Get smart_collection details?" -> GET /admin/api/2020-10/smart_collections/{smart_collection_id}.json
- "Update a smart_collection?" -> PUT /admin/api/2020-10/smart_collections/{smart_collection_id}.json
- "Delete a smart_collection?" -> DELETE /admin/api/2020-10/smart_collections/{smart_collection_id}.json
- "List all smart_collections.json?" -> GET /admin/api/2021-01/smart_collections.json
- "Create a smart_collections.json?" -> POST /admin/api/2021-01/smart_collections.json
- "List all count.json?" -> GET /admin/api/2021-01/smart_collections/count.json
- "Get smart_collection details?" -> GET /admin/api/2021-01/smart_collections/{smart_collection_id}.json
- "Update a smart_collection?" -> PUT /admin/api/2021-01/smart_collections/{smart_collection_id}.json
- "Delete a smart_collection?" -> DELETE /admin/api/2021-01/smart_collections/{smart_collection_id}.json
- "List all smart_collections.json?" -> GET /admin/api/unstable/smart_collections.json
- "Create a smart_collections.json?" -> POST /admin/api/unstable/smart_collections.json
- "List all count.json?" -> GET /admin/api/unstable/smart_collections/count.json
- "Get smart_collection details?" -> GET /admin/api/unstable/smart_collections/{smart_collection_id}.json
- "Update a smart_collection?" -> PUT /admin/api/unstable/smart_collections/{smart_collection_id}.json
- "Delete a smart_collection?" -> DELETE /admin/api/unstable/smart_collections/{smart_collection_id}.json
- "Create a complete.json?" -> POST /admin/api/2020-01/checkouts/{token}/complete.json
- "Get checkout details?" -> GET /admin/api/2020-01/checkouts/{token}.json
- "Update a checkout?" -> PUT /admin/api/2020-01/checkouts/{token}.json
- "List all shipping_rates.json?" -> GET /admin/api/2020-01/checkouts/{token}/shipping_rates.json
- "Create a complete.json?" -> POST /admin/api/2020-04/checkouts/{token}/complete.json
- "Get checkout details?" -> GET /admin/api/2020-04/checkouts/{token}.json
- "Update a checkout?" -> PUT /admin/api/2020-04/checkouts/{token}.json
- "List all shipping_rates.json?" -> GET /admin/api/2020-04/checkouts/{token}/shipping_rates.json
- "Create a complete.json?" -> POST /admin/api/2020-07/checkouts/{token}/complete.json
- "Get checkout details?" -> GET /admin/api/2020-07/checkouts/{token}.json
- "Update a checkout?" -> PUT /admin/api/2020-07/checkouts/{token}.json
- "List all shipping_rates.json?" -> GET /admin/api/2020-07/checkouts/{token}/shipping_rates.json
- "Create a complete.json?" -> POST /admin/api/2020-10/checkouts/{token}/complete.json
- "Get checkout details?" -> GET /admin/api/2020-10/checkouts/{token}.json
- "Update a checkout?" -> PUT /admin/api/2020-10/checkouts/{token}.json
- "List all shipping_rates.json?" -> GET /admin/api/2020-10/checkouts/{token}/shipping_rates.json
- "Create a complete.json?" -> POST /admin/api/2021-01/checkouts/{token}/complete.json
- "Get checkout details?" -> GET /admin/api/2021-01/checkouts/{token}.json
- "Update a checkout?" -> PUT /admin/api/2021-01/checkouts/{token}.json
- "List all shipping_rates.json?" -> GET /admin/api/2021-01/checkouts/{token}/shipping_rates.json
- "Create a complete.json?" -> POST /admin/api/unstable/checkouts/{token}/complete.json
- "Get checkout details?" -> GET /admin/api/unstable/checkouts/{token}.json
- "Update a checkout?" -> PUT /admin/api/unstable/checkouts/{token}.json
- "List all shipping_rates.json?" -> GET /admin/api/unstable/checkouts/{token}/shipping_rates.json
- "List all collection_listings.json?" -> GET /admin/api/2020-01/collection_listings.json
- "List all product_ids.json?" -> GET /admin/api/2020-01/collection_listings/{collection_listing_id}/product_ids.json
- "Get collection_listing details?" -> GET /admin/api/2020-01/collection_listings/{collection_listing_id}.json
- "Update a collection_listing?" -> PUT /admin/api/2020-01/collection_listings/{collection_listing_id}.json
- "Delete a collection_listing?" -> DELETE /admin/api/2020-01/collection_listings/{collection_listing_id}.json
- "List all collection_listings.json?" -> GET /admin/api/2020-04/collection_listings.json
- "List all product_ids.json?" -> GET /admin/api/2020-04/collection_listings/{collection_listing_id}/product_ids.json
- "Get collection_listing details?" -> GET /admin/api/2020-04/collection_listings/{collection_listing_id}.json
- "Update a collection_listing?" -> PUT /admin/api/2020-04/collection_listings/{collection_listing_id}.json
- "Delete a collection_listing?" -> DELETE /admin/api/2020-04/collection_listings/{collection_listing_id}.json
- "List all collection_listings.json?" -> GET /admin/api/2020-07/collection_listings.json
- "List all product_ids.json?" -> GET /admin/api/2020-07/collection_listings/{collection_listing_id}/product_ids.json
- "Get collection_listing details?" -> GET /admin/api/2020-07/collection_listings/{collection_listing_id}.json
- "Update a collection_listing?" -> PUT /admin/api/2020-07/collection_listings/{collection_listing_id}.json
- "Delete a collection_listing?" -> DELETE /admin/api/2020-07/collection_listings/{collection_listing_id}.json
- "List all collection_listings.json?" -> GET /admin/api/2020-10/collection_listings.json
- "List all product_ids.json?" -> GET /admin/api/2020-10/collection_listings/{collection_listing_id}/product_ids.json
- "Get collection_listing details?" -> GET /admin/api/2020-10/collection_listings/{collection_listing_id}.json
- "Update a collection_listing?" -> PUT /admin/api/2020-10/collection_listings/{collection_listing_id}.json
- "Delete a collection_listing?" -> DELETE /admin/api/2020-10/collection_listings/{collection_listing_id}.json
- "List all collection_listings.json?" -> GET /admin/api/2021-01/collection_listings.json
- "List all product_ids.json?" -> GET /admin/api/2021-01/collection_listings/{collection_listing_id}/product_ids.json
- "Get collection_listing details?" -> GET /admin/api/2021-01/collection_listings/{collection_listing_id}.json
- "Update a collection_listing?" -> PUT /admin/api/2021-01/collection_listings/{collection_listing_id}.json
- "Delete a collection_listing?" -> DELETE /admin/api/2021-01/collection_listings/{collection_listing_id}.json
- "List all collection_listings.json?" -> GET /admin/api/unstable/collection_listings.json
- "List all product_ids.json?" -> GET /admin/api/unstable/collection_listings/{collection_listing_id}/product_ids.json
- "Get collection_listing details?" -> GET /admin/api/unstable/collection_listings/{collection_listing_id}.json
- "Update a collection_listing?" -> PUT /admin/api/unstable/collection_listings/{collection_listing_id}.json
- "Delete a collection_listing?" -> DELETE /admin/api/unstable/collection_listings/{collection_listing_id}.json
- "Create a payments.json?" -> POST /admin/api/2020-01/checkouts/{token}/payments.json
- "List all payments.json?" -> GET /admin/api/2020-01/checkouts/{token}/payments.json
- "Get payment details?" -> GET /admin/api/2020-01/checkouts/{token}/payments/{payment_id}.json
- "List all count.json?" -> GET /admin/api/2020-01/checkouts/{token}/payments/count.json
- "Create a payments.json?" -> POST /admin/api/2020-04/checkouts/{token}/payments.json
- "List all payments.json?" -> GET /admin/api/2020-04/checkouts/{token}/payments.json
- "Get payment details?" -> GET /admin/api/2020-04/checkouts/{token}/payments/{payment_id}.json
- "List all count.json?" -> GET /admin/api/2020-04/checkouts/{token}/payments/count.json
- "Create a payments.json?" -> POST /admin/api/2020-07/checkouts/{token}/payments.json
- "List all payments.json?" -> GET /admin/api/2020-07/checkouts/{token}/payments.json
- "Get payment details?" -> GET /admin/api/2020-07/checkouts/{token}/payments/{payment_id}.json
- "List all count.json?" -> GET /admin/api/2020-07/checkouts/{token}/payments/count.json
- "Create a payments.json?" -> POST /admin/api/2020-10/checkouts/{token}/payments.json
- "List all payments.json?" -> GET /admin/api/2020-10/checkouts/{token}/payments.json
- "Get payment details?" -> GET /admin/api/2020-10/checkouts/{token}/payments/{payment_id}.json
- "List all count.json?" -> GET /admin/api/2020-10/checkouts/{token}/payments/count.json
- "Create a payments.json?" -> POST /admin/api/2021-01/checkouts/{token}/payments.json
- "List all payments.json?" -> GET /admin/api/2021-01/checkouts/{token}/payments.json
- "Get payment details?" -> GET /admin/api/2021-01/checkouts/{token}/payments/{payment_id}.json
- "List all count.json?" -> GET /admin/api/2021-01/checkouts/{token}/payments/count.json
- "Create a payments.json?" -> POST /admin/api/unstable/checkouts/{token}/payments.json
- "List all payments.json?" -> GET /admin/api/unstable/checkouts/{token}/payments.json
- "Get payment details?" -> GET /admin/api/unstable/checkouts/{token}/payments/{payment_id}.json
- "List all count.json?" -> GET /admin/api/unstable/checkouts/{token}/payments/count.json
- "List all product_listings.json?" -> GET /admin/api/2020-01/product_listings.json
- "List all product_ids.json?" -> GET /admin/api/2020-01/product_listings/product_ids.json
- "List all count.json?" -> GET /admin/api/2020-01/product_listings/count.json
- "Get product_listing details?" -> GET /admin/api/2020-01/product_listings/{product_listing_id}.json
- "Update a product_listing?" -> PUT /admin/api/2020-01/product_listings/{product_listing_id}.json
- "Delete a product_listing?" -> DELETE /admin/api/2020-01/product_listings/{product_listing_id}.json
- "List all product_listings.json?" -> GET /admin/api/2020-04/product_listings.json
- "List all product_ids.json?" -> GET /admin/api/2020-04/product_listings/product_ids.json
- "List all count.json?" -> GET /admin/api/2020-04/product_listings/count.json
- "Get product_listing details?" -> GET /admin/api/2020-04/product_listings/{product_listing_id}.json
- "Update a product_listing?" -> PUT /admin/api/2020-04/product_listings/{product_listing_id}.json
- "Delete a product_listing?" -> DELETE /admin/api/2020-04/product_listings/{product_listing_id}.json
- "List all product_listings.json?" -> GET /admin/api/2020-07/product_listings.json
- "List all product_ids.json?" -> GET /admin/api/2020-07/product_listings/product_ids.json
- "List all count.json?" -> GET /admin/api/2020-07/product_listings/count.json
- "Get product_listing details?" -> GET /admin/api/2020-07/product_listings/{product_listing_id}.json
- "Update a product_listing?" -> PUT /admin/api/2020-07/product_listings/{product_listing_id}.json
- "Delete a product_listing?" -> DELETE /admin/api/2020-07/product_listings/{product_listing_id}.json
- "List all assigned_fulfillment_orders.json?" -> GET /admin/api/2020-01/assigned_fulfillment_orders.json
- "List all assigned_fulfillment_orders.json?" -> GET /admin/api/2020-04/assigned_fulfillment_orders.json
- "List all assigned_fulfillment_orders.json?" -> GET /admin/api/2020-07/assigned_fulfillment_orders.json
- "List all assigned_fulfillment_orders.json?" -> GET /admin/api/2020-10/assigned_fulfillment_orders.json
- "List all assigned_fulfillment_orders.json?" -> GET /admin/api/2021-01/assigned_fulfillment_orders.json
- "List all assigned_fulfillment_orders.json?" -> GET /admin/api/unstable/assigned_fulfillment_orders.json
- "Create a cancellation_request.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json
- "Create a accept.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json
- "Create a cancellation_request.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json
- "Create a accept.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json
- "Create a cancellation_request.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json
- "Create a accept.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json
- "Create a cancellation_request.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json
- "Create a accept.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json
- "Create a cancellation_request.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json
- "Create a accept.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json
- "Create a cancellation_request.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/cancellation_request.json
- "Create a accept.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/cancellation_request/accept.json
- "Create a reject.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/cancellation_request/reject.json
- "Create a carrier_services.json?" -> POST /admin/api/2020-01/carrier_services.json
- "List all carrier_services.json?" -> GET /admin/api/2020-01/carrier_services.json
- "Update a carrier_service?" -> PUT /admin/api/2020-01/carrier_services/{carrier_service_id}.json
- "Get carrier_service details?" -> GET /admin/api/2020-01/carrier_services/{carrier_service_id}.json
- "Delete a carrier_service?" -> DELETE /admin/api/2020-01/carrier_services/{carrier_service_id}.json
- "Create a carrier_services.json?" -> POST /admin/api/2020-04/carrier_services.json
- "List all carrier_services.json?" -> GET /admin/api/2020-04/carrier_services.json
- "Update a carrier_service?" -> PUT /admin/api/2020-04/carrier_services/{carrier_service_id}.json
- "Get carrier_service details?" -> GET /admin/api/2020-04/carrier_services/{carrier_service_id}.json
- "Delete a carrier_service?" -> DELETE /admin/api/2020-04/carrier_services/{carrier_service_id}.json
- "Create a carrier_services.json?" -> POST /admin/api/2020-07/carrier_services.json
- "List all carrier_services.json?" -> GET /admin/api/2020-07/carrier_services.json
- "Update a carrier_service?" -> PUT /admin/api/2020-07/carrier_services/{carrier_service_id}.json
- "Get carrier_service details?" -> GET /admin/api/2020-07/carrier_services/{carrier_service_id}.json
- "Delete a carrier_service?" -> DELETE /admin/api/2020-07/carrier_services/{carrier_service_id}.json
- "Create a carrier_services.json?" -> POST /admin/api/2020-10/carrier_services.json
- "List all carrier_services.json?" -> GET /admin/api/2020-10/carrier_services.json
- "Update a carrier_service?" -> PUT /admin/api/2020-10/carrier_services/{carrier_service_id}.json
- "Get carrier_service details?" -> GET /admin/api/2020-10/carrier_services/{carrier_service_id}.json
- "Delete a carrier_service?" -> DELETE /admin/api/2020-10/carrier_services/{carrier_service_id}.json
- "Create a carrier_services.json?" -> POST /admin/api/2021-01/carrier_services.json
- "List all carrier_services.json?" -> GET /admin/api/2021-01/carrier_services.json
- "Update a carrier_service?" -> PUT /admin/api/2021-01/carrier_services/{carrier_service_id}.json
- "Get carrier_service details?" -> GET /admin/api/2021-01/carrier_services/{carrier_service_id}.json
- "Delete a carrier_service?" -> DELETE /admin/api/2021-01/carrier_services/{carrier_service_id}.json
- "Create a carrier_services.json?" -> POST /admin/api/unstable/carrier_services.json
- "List all carrier_services.json?" -> GET /admin/api/unstable/carrier_services.json
- "Update a carrier_service?" -> PUT /admin/api/unstable/carrier_services/{carrier_service_id}.json
- "Get carrier_service details?" -> GET /admin/api/unstable/carrier_services/{carrier_service_id}.json
- "Delete a carrier_service?" -> DELETE /admin/api/unstable/carrier_services/{carrier_service_id}.json
- "List all fulfillments.json?" -> GET /admin/api/2020-01/orders/{order_id}/fulfillments.json
- "Create a fulfillments.json?" -> POST /admin/api/2020-01/orders/{order_id}/fulfillments.json
- "List all fulfillments.json?" -> GET /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/fulfillments.json
- "List all count.json?" -> GET /admin/api/2020-01/orders/{order_id}/fulfillments/count.json
- "Get fulfillment details?" -> GET /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Update a fulfillment?" -> PUT /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Create a fulfillments.json?" -> POST /admin/api/2020-01/fulfillments.json
- "Create a update_tracking.json?" -> POST /admin/api/2020-01/fulfillments/{fulfillment_id}/update_tracking.json
- "Create a complete.json?" -> POST /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json
- "Create a open.json?" -> POST /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/open.json
- "Create a cancel.json?" -> POST /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json
- "Create a cancel.json?" -> POST /admin/api/2020-01/fulfillments/{fulfillment_id}/cancel.json
- "List all fulfillments.json?" -> GET /admin/api/2020-04/orders/{order_id}/fulfillments.json
- "Create a fulfillments.json?" -> POST /admin/api/2020-04/orders/{order_id}/fulfillments.json
- "List all fulfillments.json?" -> GET /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/fulfillments.json
- "List all count.json?" -> GET /admin/api/2020-04/orders/{order_id}/fulfillments/count.json
- "Get fulfillment details?" -> GET /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Update a fulfillment?" -> PUT /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Create a fulfillments.json?" -> POST /admin/api/2020-04/fulfillments.json
- "Create a update_tracking.json?" -> POST /admin/api/2020-04/fulfillments/{fulfillment_id}/update_tracking.json
- "Create a complete.json?" -> POST /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json
- "Create a open.json?" -> POST /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/open.json
- "Create a cancel.json?" -> POST /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json
- "Create a cancel.json?" -> POST /admin/api/2020-04/fulfillments/{fulfillment_id}/cancel.json
- "List all fulfillments.json?" -> GET /admin/api/2020-07/orders/{order_id}/fulfillments.json
- "Create a fulfillments.json?" -> POST /admin/api/2020-07/orders/{order_id}/fulfillments.json
- "List all fulfillments.json?" -> GET /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/fulfillments.json
- "List all count.json?" -> GET /admin/api/2020-07/orders/{order_id}/fulfillments/count.json
- "Get fulfillment details?" -> GET /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Update a fulfillment?" -> PUT /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Create a fulfillments.json?" -> POST /admin/api/2020-07/fulfillments.json
- "Create a update_tracking.json?" -> POST /admin/api/2020-07/fulfillments/{fulfillment_id}/update_tracking.json
- "Create a complete.json?" -> POST /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json
- "Create a open.json?" -> POST /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/open.json
- "Create a cancel.json?" -> POST /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json
- "Create a cancel.json?" -> POST /admin/api/2020-07/fulfillments/{fulfillment_id}/cancel.json
- "List all fulfillments.json?" -> GET /admin/api/2020-10/orders/{order_id}/fulfillments.json
- "Create a fulfillments.json?" -> POST /admin/api/2020-10/orders/{order_id}/fulfillments.json
- "List all fulfillments.json?" -> GET /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/fulfillments.json
- "List all count.json?" -> GET /admin/api/2020-10/orders/{order_id}/fulfillments/count.json
- "Get fulfillment details?" -> GET /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Update a fulfillment?" -> PUT /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Create a fulfillments.json?" -> POST /admin/api/2020-10/fulfillments.json
- "Create a update_tracking.json?" -> POST /admin/api/2020-10/fulfillments/{fulfillment_id}/update_tracking.json
- "Create a complete.json?" -> POST /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json
- "Create a open.json?" -> POST /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/open.json
- "Create a cancel.json?" -> POST /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json
- "Create a cancel.json?" -> POST /admin/api/2020-10/fulfillments/{fulfillment_id}/cancel.json
- "List all fulfillments.json?" -> GET /admin/api/2021-01/orders/{order_id}/fulfillments.json
- "Create a fulfillments.json?" -> POST /admin/api/2021-01/orders/{order_id}/fulfillments.json
- "List all fulfillments.json?" -> GET /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/fulfillments.json
- "List all count.json?" -> GET /admin/api/2021-01/orders/{order_id}/fulfillments/count.json
- "Get fulfillment details?" -> GET /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Update a fulfillment?" -> PUT /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Create a fulfillments.json?" -> POST /admin/api/2021-01/fulfillments.json
- "Create a update_tracking.json?" -> POST /admin/api/2021-01/fulfillments/{fulfillment_id}/update_tracking.json
- "Create a complete.json?" -> POST /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json
- "Create a open.json?" -> POST /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/open.json
- "Create a cancel.json?" -> POST /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json
- "Create a cancel.json?" -> POST /admin/api/2021-01/fulfillments/{fulfillment_id}/cancel.json
- "List all fulfillments.json?" -> GET /admin/api/unstable/orders/{order_id}/fulfillments.json
- "Create a fulfillments.json?" -> POST /admin/api/unstable/orders/{order_id}/fulfillments.json
- "List all fulfillments.json?" -> GET /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/fulfillments.json
- "List all count.json?" -> GET /admin/api/unstable/orders/{order_id}/fulfillments/count.json
- "Get fulfillment details?" -> GET /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Update a fulfillment?" -> PUT /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}.json
- "Create a fulfillments.json?" -> POST /admin/api/unstable/fulfillments.json
- "Create a update_tracking.json?" -> POST /admin/api/unstable/fulfillments/{fulfillment_id}/update_tracking.json
- "Create a complete.json?" -> POST /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/complete.json
- "Create a open.json?" -> POST /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/open.json
- "Create a cancel.json?" -> POST /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/cancel.json
- "Create a cancel.json?" -> POST /admin/api/unstable/fulfillments/{fulfillment_id}/cancel.json
- "List all events.json?" -> GET /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Create a events.json?" -> POST /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Get event details?" -> GET /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "Delete a event?" -> DELETE /admin/api/2020-01/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "List all events.json?" -> GET /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Create a events.json?" -> POST /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Get event details?" -> GET /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "Delete a event?" -> DELETE /admin/api/2020-04/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "List all events.json?" -> GET /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Create a events.json?" -> POST /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Get event details?" -> GET /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "Delete a event?" -> DELETE /admin/api/2020-07/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "List all events.json?" -> GET /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Create a events.json?" -> POST /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Get event details?" -> GET /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "Delete a event?" -> DELETE /admin/api/2020-10/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "List all events.json?" -> GET /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Create a events.json?" -> POST /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Get event details?" -> GET /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "Delete a event?" -> DELETE /admin/api/2021-01/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "List all events.json?" -> GET /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Create a events.json?" -> POST /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/events.json
- "Get event details?" -> GET /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "Delete a event?" -> DELETE /admin/api/unstable/orders/{order_id}/fulfillments/{fulfillment_id}/events/{event_id}.json
- "List all fulfillment_orders.json?" -> GET /admin/api/2020-01/orders/{order_id}/fulfillment_orders.json
- "Get fulfillment_order details?" -> GET /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}.json
- "Create a cancel.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/cancel.json
- "Create a close.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/close.json
- "Create a move.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/move.json
- "List all fulfillment_orders.json?" -> GET /admin/api/2020-04/orders/{order_id}/fulfillment_orders.json
- "Get fulfillment_order details?" -> GET /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}.json
- "Create a cancel.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/cancel.json
- "Create a close.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/close.json
- "Create a move.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/move.json
- "List all fulfillment_orders.json?" -> GET /admin/api/2020-07/orders/{order_id}/fulfillment_orders.json
- "Get fulfillment_order details?" -> GET /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}.json
- "Create a cancel.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/cancel.json
- "Create a close.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/close.json
- "Create a move.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/move.json
- "List all fulfillment_orders.json?" -> GET /admin/api/2020-10/orders/{order_id}/fulfillment_orders.json
- "Get fulfillment_order details?" -> GET /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}.json
- "Create a cancel.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/cancel.json
- "Create a close.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/close.json
- "Create a move.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/move.json
- "List all fulfillment_orders.json?" -> GET /admin/api/2021-01/orders/{order_id}/fulfillment_orders.json
- "Get fulfillment_order details?" -> GET /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}.json
- "Create a cancel.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/cancel.json
- "Create a close.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/close.json
- "Create a move.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/move.json
- "Create a open.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/open.json
- "Create a reschedule.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/reschedule.json
- "List all fulfillment_orders.json?" -> GET /admin/api/unstable/orders/{order_id}/fulfillment_orders.json
- "Get fulfillment_order details?" -> GET /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}.json
- "Create a cancel.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/cancel.json
- "Create a release_hold.json?" -> POST /admin/api/unstable/fulfillment_orders/release_hold.json
- "Create a close.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/close.json
- "Create a move.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/move.json
- "Create a open.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/open.json
- "Create a reschedule.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/reschedule.json
- "Create a fulfillment_request.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json
- "Create a accept.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json
- "Create a fulfillment_request.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json
- "Create a accept.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json
- "Create a fulfillment_request.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json
- "Create a accept.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json
- "Create a fulfillment_request.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json
- "Create a accept.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json
- "Create a fulfillment_request.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json
- "Create a accept.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json
- "Create a reject.json?" -> POST /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json
- "Create a fulfillment_request.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/fulfillment_request.json
- "Create a accept.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/accept.json
- "Create a reject.json?" -> POST /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/fulfillment_request/reject.json
- "List all fetch_tracking_numbers?" -> GET /fetch_tracking_numbers
- "List all fetch_stock?" -> GET /fetch_stock
- "List all fulfillment_services.json?" -> GET /admin/api/2020-01/fulfillment_services.json
- "Create a fulfillment_services.json?" -> POST /admin/api/2020-01/fulfillment_services.json
- "Get fulfillment_service details?" -> GET /admin/api/2020-01/fulfillment_services/{fulfillment_service_id}.json
- "Update a fulfillment_service?" -> PUT /admin/api/2020-01/fulfillment_services/{fulfillment_service_id}.json
- "Delete a fulfillment_service?" -> DELETE /admin/api/2020-01/fulfillment_services/{fulfillment_service_id}.json
- "List all fulfillment_services.json?" -> GET /admin/api/2020-04/fulfillment_services.json
- "Create a fulfillment_services.json?" -> POST /admin/api/2020-04/fulfillment_services.json
- "Get fulfillment_service details?" -> GET /admin/api/2020-04/fulfillment_services/{fulfillment_service_id}.json
- "Update a fulfillment_service?" -> PUT /admin/api/2020-04/fulfillment_services/{fulfillment_service_id}.json
- "Delete a fulfillment_service?" -> DELETE /admin/api/2020-04/fulfillment_services/{fulfillment_service_id}.json
- "List all fulfillment_services.json?" -> GET /admin/api/2020-07/fulfillment_services.json
- "Create a fulfillment_services.json?" -> POST /admin/api/2020-07/fulfillment_services.json
- "Get fulfillment_service details?" -> GET /admin/api/2020-07/fulfillment_services/{fulfillment_service_id}.json
- "Update a fulfillment_service?" -> PUT /admin/api/2020-07/fulfillment_services/{fulfillment_service_id}.json
- "Delete a fulfillment_service?" -> DELETE /admin/api/2020-07/fulfillment_services/{fulfillment_service_id}.json
- "List all fulfillment_services.json?" -> GET /admin/api/2020-10/fulfillment_services.json
- "Create a fulfillment_services.json?" -> POST /admin/api/2020-10/fulfillment_services.json
- "Get fulfillment_service details?" -> GET /admin/api/2020-10/fulfillment_services/{fulfillment_service_id}.json
- "Update a fulfillment_service?" -> PUT /admin/api/2020-10/fulfillment_services/{fulfillment_service_id}.json
- "Delete a fulfillment_service?" -> DELETE /admin/api/2020-10/fulfillment_services/{fulfillment_service_id}.json
- "List all fulfillment_services.json?" -> GET /admin/api/2021-01/fulfillment_services.json
- "Create a fulfillment_services.json?" -> POST /admin/api/2021-01/fulfillment_services.json
- "Get fulfillment_service details?" -> GET /admin/api/2021-01/fulfillment_services/{fulfillment_service_id}.json
- "Update a fulfillment_service?" -> PUT /admin/api/2021-01/fulfillment_services/{fulfillment_service_id}.json
- "Delete a fulfillment_service?" -> DELETE /admin/api/2021-01/fulfillment_services/{fulfillment_service_id}.json
- "List all fulfillment_services.json?" -> GET /admin/api/unstable/fulfillment_services.json
- "Create a fulfillment_services.json?" -> POST /admin/api/unstable/fulfillment_services.json
- "Get fulfillment_service details?" -> GET /admin/api/unstable/fulfillment_services/{fulfillment_service_id}.json
- "Update a fulfillment_service?" -> PUT /admin/api/unstable/fulfillment_services/{fulfillment_service_id}.json
- "Delete a fulfillment_service?" -> DELETE /admin/api/unstable/fulfillment_services/{fulfillment_service_id}.json
- "List all locations_for_move.json?" -> GET /admin/api/2020-01/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json
- "List all locations_for_move.json?" -> GET /admin/api/2020-04/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json
- "List all locations_for_move.json?" -> GET /admin/api/2020-07/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json
- "List all locations_for_move.json?" -> GET /admin/api/2020-10/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json
- "List all locations_for_move.json?" -> GET /admin/api/2021-01/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json
- "List all locations_for_move.json?" -> GET /admin/api/unstable/fulfillment_orders/{fulfillment_order_id}/locations_for_move.json
- "List all balance.json?" -> GET /admin/api/2020-01/shopify_payments/balance.json
- "List all balance.json?" -> GET /admin/api/2020-04/shopify_payments/balance.json
- "List all balance.json?" -> GET /admin/api/2020-07/shopify_payments/balance.json
- "List all balance.json?" -> GET /admin/api/2020-10/shopify_payments/balance.json
- "List all balance.json?" -> GET /admin/api/2021-01/shopify_payments/balance.json
- "List all balance.json?" -> GET /admin/api/unstable/shopify_payments/balance.json
- "List all disputes.json?" -> GET /admin/api/2020-01/shopify_payments/disputes.json
- "Get dispute details?" -> GET /admin/api/2020-01/shopify_payments/disputes/{dispute_id}.json
- "List all disputes.json?" -> GET /admin/api/2020-04/shopify_payments/disputes.json
- "List all payouts.json?" -> GET /admin/api/2020-01/shopify_payments/payouts.json
- "Get payout details?" -> GET /admin/api/2020-01/shopify_payments/payouts/{payout_id}.json
- "List all payouts.json?" -> GET /admin/api/2020-04/shopify_payments/payouts.json
- "Get payout details?" -> GET /admin/api/2020-04/shopify_payments/payouts/{payout_id}.json
- "List all payouts.json?" -> GET /admin/api/2020-07/shopify_payments/payouts.json
- "Get payout details?" -> GET /admin/api/2020-07/shopify_payments/payouts/{payout_id}.json
- "List all payouts.json?" -> GET /admin/api/2020-10/shopify_payments/payouts.json
- "Get payout details?" -> GET /admin/api/2020-10/shopify_payments/payouts/{payout_id}.json
- "List all payouts.json?" -> GET /admin/api/2021-01/shopify_payments/payouts.json
- "Get payout details?" -> GET /admin/api/2021-01/shopify_payments/payouts/{payout_id}.json
- "List all payouts.json?" -> GET /admin/api/unstable/shopify_payments/payouts.json
- "Get payout details?" -> GET /admin/api/unstable/shopify_payments/payouts/{payout_id}.json
- "List all transactions.json?" -> GET /admin/api/2020-01/shopify_payments/balance/transactions.json
- "List all countries.json?" -> GET /admin/api/2020-01/countries.json
- "Create a countries.json?" -> POST /admin/api/2020-01/countries.json
- "List all count.json?" -> GET /admin/api/2020-01/countries/count.json
- "Get country details?" -> GET /admin/api/2020-01/countries/{country_id}.json
- "Update a country?" -> PUT /admin/api/2020-01/countries/{country_id}.json
- "Delete a country?" -> DELETE /admin/api/2020-01/countries/{country_id}.json
- "List all countries.json?" -> GET /admin/api/2020-04/countries.json
- "Create a countries.json?" -> POST /admin/api/2020-04/countries.json
- "List all count.json?" -> GET /admin/api/2020-04/countries/count.json
- "Get country details?" -> GET /admin/api/2020-04/countries/{country_id}.json
- "Update a country?" -> PUT /admin/api/2020-04/countries/{country_id}.json
- "Delete a country?" -> DELETE /admin/api/2020-04/countries/{country_id}.json
- "List all countries.json?" -> GET /admin/api/2020-07/countries.json
- "Create a countries.json?" -> POST /admin/api/2020-07/countries.json
- "List all count.json?" -> GET /admin/api/2020-07/countries/count.json
- "Get country details?" -> GET /admin/api/2020-07/countries/{country_id}.json
- "Update a country?" -> PUT /admin/api/2020-07/countries/{country_id}.json
- "Delete a country?" -> DELETE /admin/api/2020-07/countries/{country_id}.json
- "List all countries.json?" -> GET /admin/api/2020-10/countries.json
- "Create a countries.json?" -> POST /admin/api/2020-10/countries.json
- "List all count.json?" -> GET /admin/api/2020-10/countries/count.json
- "Get country details?" -> GET /admin/api/2020-10/countries/{country_id}.json
- "Update a country?" -> PUT /admin/api/2020-10/countries/{country_id}.json
- "Delete a country?" -> DELETE /admin/api/2020-10/countries/{country_id}.json
- "List all countries.json?" -> GET /admin/api/2021-01/countries.json
- "Create a countries.json?" -> POST /admin/api/2021-01/countries.json
- "List all count.json?" -> GET /admin/api/2021-01/countries/count.json
- "Get country details?" -> GET /admin/api/2021-01/countries/{country_id}.json
- "Update a country?" -> PUT /admin/api/2021-01/countries/{country_id}.json
- "Delete a country?" -> DELETE /admin/api/2021-01/countries/{country_id}.json
- "List all countries.json?" -> GET /admin/api/unstable/countries.json
- "Create a countries.json?" -> POST /admin/api/unstable/countries.json
- "List all count.json?" -> GET /admin/api/unstable/countries/count.json
- "Get country details?" -> GET /admin/api/unstable/countries/{country_id}.json
- "Update a country?" -> PUT /admin/api/unstable/countries/{country_id}.json
- "Delete a country?" -> DELETE /admin/api/unstable/countries/{country_id}.json
- "List all currencies.json?" -> GET /admin/api/2020-01/currencies.json
- "List all currencies.json?" -> GET /admin/api/2020-04/currencies.json
- "List all currencies.json?" -> GET /admin/api/2020-07/currencies.json
- "List all currencies.json?" -> GET /admin/api/2020-10/currencies.json
- "List all currencies.json?" -> GET /admin/api/2021-01/currencies.json
- "List all currencies.json?" -> GET /admin/api/unstable/currencies.json
- "List all policies.json?" -> GET /admin/api/2020-01/policies.json
- "List all policies.json?" -> GET /admin/api/2020-04/policies.json
- "List all policies.json?" -> GET /admin/api/2020-07/policies.json
- "List all policies.json?" -> GET /admin/api/2020-10/policies.json
- "List all policies.json?" -> GET /admin/api/2021-01/policies.json
- "List all policies.json?" -> GET /admin/api/unstable/policies.json
- "List all provinces.json?" -> GET /admin/api/2020-01/countries/{country_id}/provinces.json
- "List all count.json?" -> GET /admin/api/2020-01/countries/{country_id}/provinces/count.json
- "Get province details?" -> GET /admin/api/2020-01/countries/{country_id}/provinces/{province_id}.json
- "Update a province?" -> PUT /admin/api/2020-01/countries/{country_id}/provinces/{province_id}.json
- "List all provinces.json?" -> GET /admin/api/2020-04/countries/{country_id}/provinces.json
- "List all count.json?" -> GET /admin/api/2020-04/countries/{country_id}/provinces/count.json
- "Get province details?" -> GET /admin/api/2020-04/countries/{country_id}/provinces/{province_id}.json
- "Update a province?" -> PUT /admin/api/2020-04/countries/{country_id}/provinces/{province_id}.json
- "List all provinces.json?" -> GET /admin/api/2020-07/countries/{country_id}/provinces.json
- "List all count.json?" -> GET /admin/api/2020-07/countries/{country_id}/provinces/count.json
- "Get province details?" -> GET /admin/api/2020-07/countries/{country_id}/provinces/{province_id}.json
- "Update a province?" -> PUT /admin/api/2020-07/countries/{country_id}/provinces/{province_id}.json
- "List all provinces.json?" -> GET /admin/api/2020-10/countries/{country_id}/provinces.json
- "List all count.json?" -> GET /admin/api/2020-10/countries/{country_id}/provinces/count.json
- "Get province details?" -> GET /admin/api/2020-10/countries/{country_id}/provinces/{province_id}.json
- "Update a province?" -> PUT /admin/api/2020-10/countries/{country_id}/provinces/{province_id}.json
- "List all provinces.json?" -> GET /admin/api/2021-01/countries/{country_id}/provinces.json
- "List all count.json?" -> GET /admin/api/2021-01/countries/{country_id}/provinces/count.json
- "Get province details?" -> GET /admin/api/2021-01/countries/{country_id}/provinces/{province_id}.json
- "Update a province?" -> PUT /admin/api/2021-01/countries/{country_id}/provinces/{province_id}.json
- "List all provinces.json?" -> GET /admin/api/unstable/countries/{country_id}/provinces.json
- "List all count.json?" -> GET /admin/api/unstable/countries/{country_id}/provinces/count.json
- "Get province details?" -> GET /admin/api/unstable/countries/{country_id}/provinces/{province_id}.json
- "Update a province?" -> PUT /admin/api/unstable/countries/{country_id}/provinces/{province_id}.json
- "List all shipping_zones.json?" -> GET /admin/api/2020-01/shipping_zones.json
- "List all shipping_zones.json?" -> GET /admin/api/2020-04/shipping_zones.json
- "List all shipping_zones.json?" -> GET /admin/api/2020-07/shipping_zones.json
- "List all shipping_zones.json?" -> GET /admin/api/2020-10/shipping_zones.json
- "List all shipping_zones.json?" -> GET /admin/api/2021-01/shipping_zones.json
- "List all shipping_zones.json?" -> GET /admin/api/unstable/shipping_zones.json
- "List all shop.json?" -> GET /admin/api/2020-01/shop.json
- "List all shop.json?" -> GET /admin/api/2020-04/shop.json
- "List all shop.json?" -> GET /admin/api/2020-07/shop.json
- "List all shop.json?" -> GET /admin/api/2020-10/shop.json
- "List all shop.json?" -> GET /admin/api/2021-01/shop.json
- "List all shop.json?" -> GET /admin/api/unstable/shop.json
- "List all tender_transactions.json?" -> GET /admin/api/2020-01/tender_transactions.json
- "List all tender_transactions.json?" -> GET /admin/api/2020-04/tender_transactions.json
- "List all tender_transactions.json?" -> GET /admin/api/2020-07/tender_transactions.json
- "List all tender_transactions.json?" -> GET /admin/api/2020-10/tender_transactions.json
- "List all tender_transactions.json?" -> GET /admin/api/2021-01/tender_transactions.json
- "List all tender_transactions.json?" -> GET /admin/api/unstable/tender_transactions.json
- "How to authenticate?" -> See Auth section

## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
