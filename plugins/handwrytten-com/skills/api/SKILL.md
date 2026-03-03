---
name: handwrytten-api
description: "Handwrytten API skill. Use when working with Handwrytten for auth, profile, fonts. Covers 30 endpoints."
version: 1.0.0
generator: lapsh
---

# Handwrytten API
API version: 1.0.0

## Auth
No authentication required.

## Base URL
https://api.handwrytten.com/v1

## Setup
1. No auth setup needed
2. GET /fonts/list -- verify access
3. POST /auth/register -- create first register

## Endpoints

30 endpoints across 9 groups. See references/api-spec.lap for full details.

### auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /auth/register | Registers a new account |
| POST | /auth/authorization | Logs in to an existing account |
| POST | /auth/resetPasswordRequest | resets a user's password |
| POST | /auth/changePassword | changes a user's password |
| POST | /auth/logout | logs out a session uid |

### profile
| Method | Path | Description |
|--------|------|-------------|
| POST | /profile/address | gets the user's return address information |
| POST | /profile/updateAddress | update the user's return address information |
| POST | /profile/recipientsList | list the addresses in the user's account |
| POST | /profile/profileAddRecipient | add a new recipient address |
| POST | /profile/updateRecipient | updates an existing new recipient address |
| POST | /profile/deleteRecipient | deletes an existing recipient address |

### fonts
| Method | Path | Description |
|--------|------|-------------|
| GET | /fonts/list | Lists Handwryting styles available for use |
| GET | /fonts/listForCustomizer | Lists fonts available for use with the card customizer |

### cards
| Method | Path | Description |
|--------|------|-------------|
| POST | /cards/uploadCustomLogo | upload logo or cover image for card |
| POST | /cards/createCustomCard | Create a new custom card |
| GET | /cards/list | Lists information on cards |
| POST | /cards/list | Lists information on cards |
| POST | /cards/view | Provides full information on a specific card |

### giftCards
| Method | Path | Description |
|--------|------|-------------|
| POST | /giftCards/view | Lists information on gift cards |
| GET | /giftCards/view | Lists information on gift cards |

### templateCategories
| Method | Path | Description |
|--------|------|-------------|
| GET | /templateCategories/list | List template categories |
| POST | /templateCategories/list | List template categories |

### templates
| Method | Path | Description |
|--------|------|-------------|
| GET | /templates/list | List template categories |
| POST | /templates/list | List template categories |
| POST | /templates/view | Get all info on a template |
| POST | /templates/create | Creates a New Template in the User’s Account |
| POST | /templates/update | Updates an Existing Template in the User’s Account |
| POST | /templates/delete | Deletes a users template |

### countries
| Method | Path | Description |
|--------|------|-------------|
| GET | /countries/list | Lists the countries to which Handwritten can mail, their associated country ID and any costs |

### orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /orders/singleStepOrder | sends an order in a single step.  This is much easier than using other order commands |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new account?" -> POST /auth/register
- "How do I log in to the API?" -> POST /auth/authorization
- "I forgot my password, how do I reset it?" -> POST /auth/resetPasswordRequest
- "How do I change my password?" -> POST /auth/changePassword
- "How do I log out?" -> POST /auth/logout
- "What is my saved address?" -> POST /profile/address
- "How do I update my sender address?" -> POST /profile/updateAddress
- "How do I list all my recipients?" -> POST /profile/recipientsList
- "How do I add a new recipient to my address book?" -> POST /profile/profileAddRecipient
- "How do I delete a recipient?" -> POST /profile/deleteRecipient
- "What handwriting fonts are available?" -> GET /fonts/list
- "What card designs can I choose from?" -> GET /cards/list
- "How do I send a handwritten card?" -> POST /orders/singleStepOrder
- "How do I create a custom card with my logo?" -> POST /cards/uploadCustomLogo + POST /cards/createCustomCard
- "What message templates are available?" -> GET /templates/list

## Response Tips

- **Auth endpoints**: Return session/token data on success; 400 on bad credentials at login, 405 on malformed requests elsewhere. Always capture the auth token from `/auth/authorization` for subsequent calls.
- **Profile endpoints**: All use POST (even reads like address lookup). Expect nested address objects with country codes. Recipient lists may return paginated arrays.
- **Fonts endpoints**: GET returns flat lists. `/fonts/list` is the general list; `/fonts/listForCustomizer` returns a filtered subset for the card editor.
- **Cards endpoints**: Both GET and POST variants exist for `/cards/list` -- POST allows filtering. `/cards/view` returns full card detail including image URLs. 400 errors indicate missing or invalid card IDs.
- **Gift cards**: Both GET and POST on `/giftCards/view` return the same data; POST may accept filter parameters.
- **Templates**: CRUD operations all use POST. List endpoints (GET and POST) mirror the cards pattern. Delete and update require a template ID in the body.
- **Orders**: `singleStepOrder` is a compound call -- expect it to require card ID, recipient, sender, message, and font selection all in one payload.

## Anomaly Flags

- **Auth token missing or expired**: Surface immediately if any non-auth endpoint returns 401/403 -- prompt re-authentication via `/auth/authorization`.
- **405 errors on auth endpoints**: Indicates malformed request body structure, not just wrong method -- flag the likely missing required fields.
- **Custom logo upload failure**: `/cards/uploadCustomLogo` requires multipart form data (file, type, uid) -- flag if the request uses JSON body instead.
- **Dual-method endpoints**: `/cards/list`, `/giftCards/view`, `/templateCategories/list`, and `/templates/list` each have GET and POST variants -- flag if the user sends filter params via GET (they will be ignored).
- **Order failure without clear error**: `singleStepOrder` bundles many steps -- if it fails, surface which sub-component (card, recipient, address, payment) is likely the cause based on error detail.
- **Recipient limit approaching**: If `/profile/recipientsList` returns a large number of entries, warn about potential account limits.

## Playbook

### 1. Send Your First Handwritten Card

1. Register an account via `POST /auth/register` with your details
2. Log in via `POST /auth/authorization` to get your auth token
3. Set your sender address via `POST /profile/address`
4. Add a recipient via `POST /profile/profileAddRecipient`
5. Browse available cards via `GET /cards/list`
6. Pick a handwriting font via `GET /fonts/list`
7. Submit the order via `POST /orders/singleStepOrder` with card ID, recipient, message, and font

### 2. Create and Send a Custom Branded Card

1. Authenticate via `POST /auth/authorization`
2. Upload your logo via `POST /cards/uploadCustomLogo` (multipart: file, type, uid)
3. Create the custom card design via `POST /cards/createCustomCard` referencing the uploaded logo
4. Preview the card via `POST /cards/view` with the new card ID
5. Send the card via `POST /orders/singleStepOrder`

### 3. Manage Your Recipient Address Book

1. Authenticate via `POST /auth/authorization`
2. List all current recipients via `POST /profile/recipientsList`
3. Add new recipients via `POST /profile/profileAddRecipient`
4. Update existing entries via `POST /profile/updateRecipient`
5. Remove outdated entries via `POST /profile/deleteRecipient`

### 4. Build a Message Template Library

1. Authenticate via `POST /auth/authorization`
2. Browse template categories via `GET /templateCategories/list`
3. View existing templates via `GET /templates/list` or filter with `POST /templates/list`
4. Create a new reusable template via `POST /templates/create`
5. Edit templates as needed via `POST /templates/update`
6. Clean up unused templates via `POST /templates/delete`

### 5. Account Setup and Password Recovery

1. Register via `POST /auth/register`
2. If you forget your password, request a reset via `POST /auth/resetPasswordRequest`
3. Change your password via `POST /auth/changePassword`
4. Set your return address via `POST /profile/address`
5. Verify your address is saved by calling `POST /profile/address` again to retrieve it


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
