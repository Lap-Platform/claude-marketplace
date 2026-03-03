---
name: swagger-petstore-openapi-30
description: "Swagger Petstore - OpenAPI 3.0 API skill. Use when working with Swagger Petstore - OpenAPI 3.0 for pet, store, user. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# Swagger Petstore - OpenAPI 3.0
API version: 1.0.27

## Auth
OAuth2 | ApiKey api_key in header

## Base URL
/api/v3

## Setup
1. Set your API key in the appropriate header
2. GET /pet/findByStatus -- verify access
3. POST /pet -- create first pet

## Endpoints

19 endpoints across 3 groups. See references/api-spec.lap for full details.

### pet
| Method | Path | Description |
|--------|------|-------------|
| PUT | /pet | Update an existing pet. |
| POST | /pet | Add a new pet to the store. |
| GET | /pet/findByStatus | Finds Pets by status. |
| GET | /pet/findByTags | Finds Pets by tags. |
| GET | /pet/{petId} | Find pet by ID. |
| POST | /pet/{petId} | Updates a pet in the store with form data. |
| DELETE | /pet/{petId} | Deletes a pet. |
| POST | /pet/{petId}/uploadImage | Uploads an image. |

### store
| Method | Path | Description |
|--------|------|-------------|
| GET | /store/inventory | Returns pet inventories by status. |
| POST | /store/order | Place an order for a pet. |
| GET | /store/order/{orderId} | Find purchase order by ID. |
| DELETE | /store/order/{orderId} | Delete purchase order by identifier. |

### user
| Method | Path | Description |
|--------|------|-------------|
| POST | /user | Create user. |
| POST | /user/createWithList | Creates list of users with given input array. |
| GET | /user/login | Logs user into the system. |
| GET | /user/logout | Logs out current logged in user session. |
| GET | /user/{username} | Get user by user name. |
| PUT | /user/{username} | Update user resource. |
| DELETE | /user/{username} | Delete user resource. |

## Enhanced Skill Content
## Question Mapping

- "How do I add a new pet to the store?" -> POST /pet
- "How do I update an existing pet's details?" -> PUT /pet
- "What pets are currently available for sale?" -> GET /pet/findByStatus (status=available)
- "Find all pets with a specific tag" -> GET /pet/findByTags
- "Get the details of pet #42" -> GET /pet/{petId}
- "Change a pet's name or status without sending the full object?" -> POST /pet/{petId}
- "How do I upload a photo for a pet?" -> POST /pet/{petId}/uploadImage
- "Delete a pet listing" -> DELETE /pet/{petId}
- "What's currently in stock?" -> GET /store/inventory
- "Place an order for a pet" -> POST /store/order
- "Check the status of my order" -> GET /store/order/{orderId}
- "Cancel an order" -> DELETE /store/order/{orderId}
- "Create a new user account" -> POST /user
- "Bulk-create multiple users at once" -> POST /user/createWithList
- "Log in and get a session token" -> GET /user/login

## Response Tips

- **Pet endpoints**: All pet responses return the full pet object with nested `category` (map) and `tags` (array of maps). Always check that `id` is present in the response to confirm server-side assignment.
- **Store inventory**: `GET /store/inventory` returns a dynamic key-value map of status strings to counts -- keys are not fixed and vary with data.
- **Store orders**: The `status` field cycles through `placed` -> `approved` -> `delivered`. The `complete` boolean may lag behind status transitions.
- **User endpoints**: `GET /user/login` returns a session token in the response header or body (not a JSON object). Watch for the `X-Rate-Limit` and `X-Expires-After` headers.
- **Error responses**: 400 means bad input (invalid ID format, missing required fields). 404 means the resource does not exist. 422 means the request body was well-formed but semantically invalid.

## Anomaly Flags

- **Rate limit headers**: Surface `X-Rate-Limit` from login responses. Alert the user when approaching the cap.
- **404 on pet or order**: Proactively suggest verifying the ID exists via `GET /pet/{petId}` or `GET /store/order/{orderId}` before attempting updates or deletes.
- **422 on create/update**: Flag that the body passed validation but failed business rules (e.g., duplicate pet name, invalid status transition). Surface the full error message.
- **Stale inventory**: If `GET /store/inventory` returns all zeros or an empty map, flag that the store may be in maintenance or data may not have synced.
- **Missing auth**: If any write operation returns 401/403, remind the user that OAuth2 or the `api_key` header is required for mutations and that `DELETE /pet/{petId}` accepts an optional `api_key` parameter.
- **Deprecated tag search**: `GET /pet/findByTags` is commonly marked deprecated in Petstore implementations. Warn users to prefer `findByStatus` or direct ID lookup where possible.

## Playbook

### 1. Add a Pet and Upload Its Photo

1. `POST /pet` with `name` and `photoUrls` (can be empty array initially)
2. Capture the returned `id` from the response
3. `POST /pet/{petId}/uploadImage` with the pet's `id` and the image file
4. Verify by calling `GET /pet/{petId}` to confirm the photo URL was attached

### 2. Place and Track an Order

1. Browse available pets: `GET /pet/findByStatus` with `status=available`
2. Pick a pet and note its `id`
3. `POST /store/order` with `petId`, `quantity`, and optionally `shipDate`
4. Capture the returned `orderId`
5. Poll `GET /store/order/{orderId}` to watch `status` progress from `placed` to `approved` to `delivered`

### 3. User Registration and Login Flow

1. `POST /user` with username, email, password, and profile fields
2. `GET /user/login` with `username` and `password` to obtain a session
3. Store the session token from the response for subsequent authenticated calls
4. When done, call `GET /user/logout` to invalidate the session

### 4. Bulk User Onboarding

1. Prepare an array of user objects with unique usernames
2. `POST /user/createWithList` with the full array
3. Verify each user was created by calling `GET /user/{username}` for a sample
4. If any user needs corrections, `PUT /user/{username}` with the updated fields

### 5. Full Pet Lifecycle Management

1. `POST /pet` to create the listing with `status: "available"`
2. `POST /pet/{petId}/uploadImage` to attach photos
3. `POST /pet/{petId}` to update name or status as needed (e.g., set to `pending` when interest is shown)
4. Once sold, `PUT /pet` with `status: "sold"` to update the full record
5. Optionally `DELETE /pet/{petId}` to remove the listing entirely after the sale completes


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
