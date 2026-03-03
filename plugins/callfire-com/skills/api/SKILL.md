---
name: callfire-api-documentation
description: "CallFire API Documentation API skill. Use when working with CallFire API Documentation for calls, campaigns, contacts. Covers 123 endpoints."
version: 1.0.0
generator: lapsh
---

# CallFire API Documentation
API version: V2

## Auth
basic

## Base URL
https://api.callfire.com/v2

## Setup
1. Configure auth: basic
2. GET /calls -- verify access
3. POST /calls -- create first calls

## Endpoints

123 endpoints across 11 groups. See references/api-spec.lap for full details.

### calls
| Method | Path | Description |
|--------|------|-------------|
| GET | /calls | Find calls |
| POST | /calls | Send calls |
| GET | /calls/broadcasts | Find call broadcasts |
| POST | /calls/broadcasts | Create a call broadcast |
| GET | /calls/broadcasts/{id} | Find a specific call broadcast |
| PUT | /calls/broadcasts/{id} | Update a call broadcast |
| POST | /calls/broadcasts/{id}/archive | Archive voice broadcast |
| GET | /calls/broadcasts/{id}/batches | Find batches in a call broadcast |
| POST | /calls/broadcasts/{id}/batches | Add batches to a call broadcast |
| GET | /calls/broadcasts/{id}/calls | Find calls in a call broadcast |
| POST | /calls/broadcasts/{id}/recipients | Add recipients to a call broadcast |
| POST | /calls/broadcasts/{id}/start | Start voice broadcast |
| GET | /calls/broadcasts/{id}/stats | Get statistics on call broadcast |
| POST | /calls/broadcasts/{id}/stop | Stop voice broadcast |
| POST | /calls/broadcasts/{id}/toggleRecipientsStatus | Disable/enable undialed recipients in broadcast |
| GET | /calls/recordings/{id} | Get call recording by id |
| GET | /calls/recordings/{id}.mp3 | Get call recording in mp3 format |
| GET | /calls/{id} | Find a specific call |
| GET | /calls/{id}/recordings | Get call recordings for a call |
| GET | /calls/{id}/recordings/{name} | Get call recording by name |
| GET | /calls/{id}/recordings/{name}.mp3 | Get call mp3 recording by name |

### campaigns
| Method | Path | Description |
|--------|------|-------------|
| GET | /campaigns/batches/{id} | Find a specific batch |
| PUT | /campaigns/batches/{id} | Update a batch |
| GET | /campaigns/sounds | Find sounds |
| POST | /campaigns/sounds/calls | Add sound via call |
| POST | /campaigns/sounds/files | Add sound via file |
| POST | /campaigns/sounds/tts | Add sound via text-to-speech |
| GET | /campaigns/sounds/{id} | Find a specific sound |
| DELETE | /campaigns/sounds/{id} | Delete a specific sound |
| GET | /campaigns/sounds/{id}.mp3 | Download a MP3 sound |
| GET | /campaigns/sounds/{id}.wav | Download a WAV sound |

### contacts
| Method | Path | Description |
|--------|------|-------------|
| GET | /contacts | Find contacts |
| POST | /contacts | Create contacts |
| GET | /contacts/dncs | Find do not contact (dnc) items |
| POST | /contacts/dncs | Add do not contact (dnc) numbers |
| DELETE | /contacts/dncs/sources/{source} | Delete do not contact (dnc) numbers contained in source. |
| GET | /contacts/dncs/universals/{toNumber} | Find universal do not contacts (udnc) associated with toNumber |
| GET | /contacts/dncs/{number} | Get do not contact (dnc) |
| PUT | /contacts/dncs/{number} | Update an individual do not contact (dnc) number |
| DELETE | /contacts/dncs/{number} | Delete do not contact (dnc) number. If number contains commas treat as list of numbers |
| GET | /contacts/lists | Find contact lists |
| POST | /contacts/lists | Create contact lists |
| POST | /contacts/lists/upload | Create contact list from file |
| GET | /contacts/lists/{id} | Find a specific contact list |
| PUT | /contacts/lists/{id} | Update a contact list |
| DELETE | /contacts/lists/{id} | Delete a contact list |
| GET | /contacts/lists/{id}/items | Find contacts in a contact list |
| POST | /contacts/lists/{id}/items | Add contacts to a contact list |
| DELETE | /contacts/lists/{id}/items | Delete contacts from a contact list |
| DELETE | /contacts/lists/{id}/items/{contactId} | Delete a contact from a contact list |
| GET | /contacts/{id} | Find a specific contact |
| PUT | /contacts/{id} | Update a contact |
| DELETE | /contacts/{id} | Delete a contact |
| GET | /contacts/{id}/history | Find a contact's history |

### keywords
| Method | Path | Description |
|--------|------|-------------|
| GET | /keywords | Find keywords |
| GET | /keywords/leases | Find keyword leases |
| GET | /keywords/leases/configs | Find keyword lease configs |
| GET | /keywords/leases/configs/{keyword} | Find a specific keyword lease config |
| PUT | /keywords/leases/configs/{keyword} | Update a keyword lease config |
| GET | /keywords/leases/id/{id} | Find a keyword by id |
| GET | /keywords/leases/{keyword} | Find a specific lease |
| PUT | /keywords/leases/{keyword} | Update a lease |
| GET | /keywords/{keyword}/available | Check for a specific keyword |

### me
| Method | Path | Description |
|--------|------|-------------|
| GET | /me/account | Find account details |
| GET | /me/api/credentials | Find api credentials |
| POST | /me/api/credentials | Create api credentials |
| GET | /me/api/credentials/{id} | Find a specific api credential |
| DELETE | /me/api/credentials/{id} | Delete api credentials |
| POST | /me/api/credentials/{id}/disable | Disable specified API credentials |
| POST | /me/api/credentials/{id}/enable | Enable specified API credentials |
| GET | /me/billing/credit-usage | Find credit usage |
| GET | /me/billing/credit-usage/grouped/{rollupBinType} | Find credit usage grouped by period |
| GET | /me/billing/plan-usage | Find plan usage |
| GET | /me/callerids | Find caller ids |
| POST | /me/callerids/{callerid} | Create a caller id |
| POST | /me/callerids/{callerid}/verification-code | Verify a caller id |

### media
| Method | Path | Description |
|--------|------|-------------|
| GET | /media | Find media |
| POST | /media | Create media |
| GET | /media/public/{key}.{extension} | Download media by extension |
| GET | /media/{id} | Get a specific media |
| GET | /media/{id}.{extension} | Download media by extension |
| GET | /media/{id}/file | Download a MP3 media |

### numbers
| Method | Path | Description |
|--------|------|-------------|
| GET | /numbers/leases | Find leases |
| GET | /numbers/leases/configs | Find lease configs |
| GET | /numbers/leases/configs/{number} | Find a specific lease config |
| PUT | /numbers/leases/configs/{number} | Update a lease config |
| GET | /numbers/leases/{number} | Find a specific lease |
| PUT | /numbers/leases/{number} | Update a lease |
| GET | /numbers/local | Find local numbers |
| GET | /numbers/regions | Find number regions |
| GET | /numbers/tollfree | Find tollfree numbers |

### orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /orders | Find orders |
| POST | /orders/keywords | Purchase keywords |
| POST | /orders/numbers | Purchase numbers |
| GET | /orders/{id} | Find a specific order |

### reports
| Method | Path | Description |
|--------|------|-------------|
| GET | /reports/delivery | Get delivery reports by ad hoc criteria |

### texts
| Method | Path | Description |
|--------|------|-------------|
| GET | /texts | Find texts |
| POST | /texts | Send texts |
| GET | /texts/auto-replys | Find auto replies |
| POST | /texts/auto-replys | Create an auto reply |
| GET | /texts/auto-replys/{id} | Find a specific auto reply |
| DELETE | /texts/auto-replys/{id} | Delete an auto reply |
| GET | /texts/broadcasts | Find text broadcasts |
| POST | /texts/broadcasts | Create a text broadcast |
| GET | /texts/broadcasts/{id} | Find a specific text broadcast |
| PUT | /texts/broadcasts/{id} | Update a text broadcast |
| POST | /texts/broadcasts/{id}/archive | Archive text broadcast |
| GET | /texts/broadcasts/{id}/batches | Find batches in a text broadcast |
| POST | /texts/broadcasts/{id}/batches | Add batches to a text broadcast |
| POST | /texts/broadcasts/{id}/recipients | Add recipients to a text broadcast |
| POST | /texts/broadcasts/{id}/start | Start text broadcast |
| GET | /texts/broadcasts/{id}/stats | Get statistics on text broadcast |
| POST | /texts/broadcasts/{id}/stop | Stop text broadcast |
| GET | /texts/broadcasts/{id}/texts | Find texts in a text broadcast |
| POST | /texts/broadcasts/{id}/toggleRecipientsStatus | Disable/enable undialed recipients in broadcast |
| GET | /texts/{id} | Find a specific text |

### webhooks
| Method | Path | Description |
|--------|------|-------------|
| GET | /webhooks | Find webhooks |
| POST | /webhooks | Create a webhook |
| GET | /webhooks/resources | Find webhook resources |
| GET | /webhooks/resources/{resource} | Find specific webhook resource |
| GET | /webhooks/{id} | Find a specific webhook |
| PUT | /webhooks/{id} | Update a webhook |
| DELETE | /webhooks/{id} | Delete a webhook |

## Enhanced Skill Content
## Question Mapping

- "How do I send a voice call to a list of phone numbers?" -> POST /calls
- "How do I send a text message to someone?" -> POST /texts
- "What calls have been made in the last 24 hours?" -> GET /calls (with intervalBegin/intervalEnd)
- "How do I create a text broadcast campaign?" -> POST /texts/broadcasts
- "How do I check my account balance and credit usage?" -> GET /me/billing/credit-usage
- "Is the keyword PROMO available to lease?" -> GET /keywords/{keyword}/available
- "How do I add a number to the Do Not Call list?" -> POST /contacts/dncs
- "How do I upload a contact list from a CSV file?" -> POST /contacts/lists/upload
- "How do I stop a running call broadcast?" -> POST /calls/broadcasts/{id}/stop
- "What phone numbers are available in California?" -> GET /numbers/local (with state=CA)
- "How do I set up a webhook for incoming texts?" -> POST /webhooks
- "How do I download a call recording as MP3?" -> GET /calls/recordings/{id}.mp3
- "What is the delivery status of my text messages?" -> GET /reports/delivery
- "How do I verify a caller ID number?" -> POST /me/callerids/{callerid}/verification-code
- "How do I purchase a toll-free number?" -> POST /orders/numbers

## Response Tips

- **Calls & Texts lists**: Paginated via `limit`/`offset`; default limit varies, always check `totalCount` in response to know if more pages exist.
- **Broadcast operations** (start/stop/archive): Return no body on success (2xx); rely on status code alone to confirm action.
- **Create endpoints** (POST broadcasts, orders): Return `201` with the created resource `id` in the response body; use that `id` for all subsequent operations.
- **Contact/DNC lookups**: Nested objects may contain custom property maps; iterate `properties` keys rather than assuming fixed fields.
- **Recording downloads** (.mp3/.wav): Return binary streams, not JSON; set `Accept` header accordingly and handle as file data.
- **Error responses** (400-500): Return a JSON object with `errorCode`, `message`, and `details` array; parse `details` for field-level validation failures.

## Anomaly Flags

- **401 on any endpoint**: API credentials may be expired or disabled; check credential status via `GET /me/api/credentials` and re-enable if needed with `POST /me/api/credentials/{id}/enable`.
- **Strict validation failures (400)**: When `strictValidation=true`, invalid phone numbers in batch sends are rejected entirely rather than skipped; surface which recipients failed.
- **Broadcast stuck in non-running state**: If `POST .../start` returns success but `GET .../stats` shows zero activity, the broadcast may have no valid recipients or the account may lack credits.
- **DNC conflicts**: A 400 when sending calls/texts may indicate recipients are on the Do Not Call list; proactively check `GET /contacts/dncs/{number}` before large campaigns.
- **Credit depletion**: Monitor `GET /me/billing/credit-usage` and `GET /me/billing/plan-usage`; surface warnings when usage approaches plan limits.
- **Order status not FINISHED**: After `POST /orders/numbers` or `POST /orders/keywords`, poll `GET /orders/{id}` and flag if status stays PENDING beyond a reasonable window.
- **Deprecated or disabled credentials**: `GET /me/api/credentials` may show credentials with disabled status; flag any that the user might unknowingly be relying on.

## Playbook

### 1. Launch a Text Broadcast Campaign

1. Create or select a contact list: `POST /contacts/lists` or `POST /contacts/lists/upload` (CSV)
2. Create the text broadcast: `POST /texts/broadcasts` with message body and recipient list reference
3. Start the broadcast: `POST /texts/broadcasts/{id}/start`
4. Monitor progress: `GET /texts/broadcasts/{id}/stats` (poll periodically)
5. Review individual message results: `GET /texts/broadcasts/{id}/texts`
6. When finished, archive: `POST /texts/broadcasts/{id}/archive`

### 2. Purchase a Number and Configure It

1. Search available local numbers: `GET /numbers/local` (filter by state, city, zipcode, or prefix)
2. Alternatively, search toll-free: `GET /numbers/tollfree` (filter by pattern)
3. Place the order: `POST /orders/numbers` with selected number(s)
4. Confirm order completion: `GET /orders/{id}` (check status = FINISHED)
5. Configure the leased number: `PUT /numbers/leases/configs/{number}` (set call/text forwarding, IVR, etc.)

### 3. Set Up Webhook Notifications for Inbound Texts

1. List available webhook resources and events: `GET /webhooks/resources`
2. Inspect events for the text resource: `GET /webhooks/resources/TextBroadcast` (or relevant resource name)
3. Create the webhook: `POST /webhooks` with `resource`, `event`, `callback` URL, and `enabled: true`
4. Verify it was registered: `GET /webhooks` and confirm your entry appears
5. Test by sending an inbound text to your leased number and checking your callback endpoint

### 4. Manage Do Not Call (DNC) Compliance

1. Check if a number is on your DNC list: `GET /contacts/dncs/{number}`
2. Check universal DNC registry: `GET /contacts/dncs/universals/{toNumber}` (with your fromNumber)
3. Add numbers to DNC: `POST /contacts/dncs` with the number(s) and source
4. Remove a number from DNC if consent is re-obtained: `DELETE /contacts/dncs/{number}`
5. Before any campaign, filter recipients: `GET /contacts/dncs` with relevant prefix/campaign filters

### 5. Review Call Recordings

1. Find calls for a specific broadcast or time range: `GET /calls` (filter by campaignId, intervalBegin, intervalEnd)
2. List recordings for a specific call: `GET /calls/{id}/recordings`
3. Get recording metadata: `GET /calls/recordings/{id}`
4. Download the audio file: `GET /calls/recordings/{id}.mp3`
5. For named recordings: `GET /calls/{id}/recordings/{name}.mp3`


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
