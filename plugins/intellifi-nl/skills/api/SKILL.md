---
name: brain-web-api
description: "Brain Web API skill. Use when working with Brain Web for authinfo, blobs, events. Covers 77 endpoints."
version: 1.0.0
generator: lapsh
---

# Brain Web API
API version: 2.27.2+0.gd5006bf.dirty

## Auth
ApiKey key in query | ApiKey X-Api-Key in header | ApiKey brain.sid in cookie

## Base URL
{protocol}://{customer}.intellifi.{tld}/api

## Setup
1. Set your API key in the appropriate header
2. GET /authinfo -- verify access
3. POST /blobs -- create first blobs

## Endpoints

77 endpoints across 15 groups. See references/api-spec.lap for full details.

### authinfo
| Method | Path | Description |
|--------|------|-------------|
| GET | /authinfo | Authentication information |

### blobs
| Method | Path | Description |
|--------|------|-------------|
| GET | /blobs | Get all binary large objects (blob) |
| POST | /blobs | Create binary large object (blob) metadata |
| GET | /blobs/{id} | Get binary large object (blob) |
| DELETE | /blobs/{id} | Delete binary large object (blob) |
| GET | /blobs/{id}/download/{filename} | Download a binary large object (blob) |
| POST | /blobs/{id}/upload | Create binary large object (blob) |

### events
| Method | Path | Description |
|--------|------|-------------|
| GET | /events | Get all events |
| GET | /events/{id} | Get event |

### items
| Method | Path | Description |
|--------|------|-------------|
| GET | /items | Get all items |
| POST | /items | Create item |
| GET | /items/{id} | Get item |
| PUT | /items/{id} | Update existing item |
| DELETE | /items/{id} | Delete item |

### keys
| Method | Path | Description |
|--------|------|-------------|
| GET | /keys | Get all keys |
| POST | /keys | Create key |
| GET | /keys/{id} | Get key |
| PUT | /keys/{id} | Update existing key |
| DELETE | /keys/{id} | Delete key |

### kvpairs
| Method | Path | Description |
|--------|------|-------------|
| GET | /kvpairs | Get all key-value pairs |
| POST | /kvpairs | Create key-value pair |
| GET | /kvpairs/{id} | Get key-value pair |
| PUT | /kvpairs/{id} | Update existing Key-value pair |
| DELETE | /kvpairs/{id} | Delete key-value pair |

### locations
| Method | Path | Description |
|--------|------|-------------|
| GET | /locations | Get all locations |
| POST | /locations | Create location |
| GET | /locations/{id} | Get location |
| PUT | /locations/{id} | Update existing location |
| DELETE | /locations/{id} | Delete location |

### locationrules
| Method | Path | Description |
|--------|------|-------------|
| GET | /locationrules | Get all location rules |
| POST | /locationrules | Create location rule |
| GET | /locationrules/{id} | Get location rule |
| PUT | /locationrules/{id} | Update existing location rule |
| DELETE | /locationrules/{id} | Delete location rule |

### presences
| Method | Path | Description |
|--------|------|-------------|
| GET | /presences | Get all presences |
| GET | /presences/{id} | Get presence |

### services
| Method | Path | Description |
|--------|------|-------------|
| GET | /services | Get all services |
| GET | /services/{id} | Get service |
| PUT | /services/{id} | Update existing service |

### sets
| Method | Path | Description |
|--------|------|-------------|
| GET | /sets/itemlists | Get all item lists |
| POST | /sets/itemlists | Create item list |
| GET | /sets/itemlists/{id} | Get item list |
| PUT | /sets/itemlists/{id} | Update existing item list |
| DELETE | /sets/itemlists/{id} | Delete item list |
| GET | /sets/itemlists/{id}/ids | Get item ids for this list |
| POST | /sets/itemlists/{id}/ids | Add items to an existing list |
| DELETE | /sets/itemlists/{id}/ids/{itemId} | Delete item from list |
| GET | /sets/spotlists | Get all spot lists |
| POST | /sets/spotlists | Create spot list |
| GET | /sets/spotlists/{id} | Info for a specific spot list |
| PUT | /sets/spotlists/{id} | Update existing spot list |
| DELETE | /sets/spotlists/{id} | Delete spot list |
| GET | /sets/spotlists/{id}/ids | Get spot ids for this list |
| POST | /sets/spotlists/{id}/ids | Add spots to an existing list |
| DELETE | /sets/spotlists/{id}/ids/{itemId} | Delete spot from list |

### spots
| Method | Path | Description |
|--------|------|-------------|
| GET | /spots | Get all spots |
| GET | /spots/{id} | Get spot |
| PUT | /spots/{id} | Update existing spot |
| GET | /spots/{id}/sets | Get spotsets |
| POST | /spots/{id}/sets | Create spotset |
| PUT | /spots/{id}/sets/{setId} | Update existing spotset |
| GET | /spots/{id}/sets/{setId} | Get spotset |

### spotsets
| Method | Path | Description |
|--------|------|-------------|
| GET | /spotsets | Get spotsets |
| POST | /spotsets | Create spotset |
| PUT | /spotsets/{id} | Update existing spotset |
| GET | /spotsets/{id} | Get spotset |

### subscriptions
| Method | Path | Description |
|--------|------|-------------|
| GET | /subscriptions | Get all subscriptions |
| POST | /subscriptions | Create subscription |
| GET | /subscriptions/{id} | Get subscription |
| PUT | /subscriptions/{id} | Update existing subscription |
| DELETE | /subscriptions/{id} | Delete subscription |
| GET | /subscriptions/{id}/events | Get subscription events |

### users
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | Get all users |
| POST | /users | Create user |
| GET | /users/{id} | Get user |
| PUT | /users/{id} | Update existing user |
| DELETE | /users/{id} | Delete user |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with the Brain API?" -> GET /authinfo
- "What items are currently present in the system?" -> GET /items with `is_present=true`
- "Where is a specific item located right now?" -> GET /items/{id} (check `location` field)
- "Which spots are online?" -> GET /spots with `is_online=true`
- "How do I upload a file to the system?" -> POST /blobs then POST /blobs/{id}/upload
- "What events happened in the last hour?" -> GET /events with `from` set to one hour ago
- "How do I set up a webhook to receive notifications?" -> POST /subscriptions with `target_url` and `topic_filter`
- "Why is my subscription not delivering events?" -> GET /subscriptions/{id} (check `target_delivery_status` and `target_delivery_last_failure`)
- "How do I create a rule that prevents items from moving to a location?" -> POST /locationrules with `type=disallow`
- "Can I get just the IDs without full objects?" -> GET /items (or any list endpoint) with `id_only=true`
- "How do I add an item to an item list?" -> POST /sets/itemlists/{id}/ids
- "What API keys exist and which are read-only?" -> GET /keys with `is_read_only=true`
- "How do I track which items a specific spot has seen?" -> GET /presences with `location={spotLocationId}`
- "How do I store custom key-value data?" -> POST /kvpairs then PUT /kvpairs/{id} with `kv_value`
- "How do I long-poll for new items?" -> GET /items with `timeout_s` and `after_id` set to the last seen ID

## Response Tips

- **List endpoints** (GET /items, /blobs, /events, etc.): Default limit is 100. Use `after_id`/`before_id` for cursor-based pagination; combine with `sort=-id` (default, newest first) or `sort=id` for chronological order. Set `results_only=true` to skip envelope metadata.
- **Create endpoints** (POST): Return 201 with `{resource: {id, url}, status}` -- always capture `resource.id` for subsequent operations.
- **Update/Delete endpoints** (PUT/DELETE): Return 200 with the same `{resource: {id, url}, status}` envelope -- check `status` field, not just HTTP code.
- **Events and subscriptions**: Event payloads use nested `topic` object with `resource_type`, `action`, and `resource_id` -- filter server-side via `topic.resource_type` and `topic.action` query params rather than client-side.
- **Presences**: Responses nest full `location` and `item` objects when populated -- use `select` param to reduce payload size if you only need IDs.

## Anomaly Flags

- **Subscription delivery failures**: Surface `target_delivery_last_failure` and `target_delivery_status` whenever a subscription is read -- failed webhooks silently drop events if `database_hold_time_h` expires.
- **Spot offline status**: Flag when `is_online=false` on any spot, as this means the reader hardware is disconnected and no new presences will be recorded.
- **Item move without location rule**: Alert when an item's `location` changes and active location rules of type `disallow` exist for that path -- may indicate a rule misconfiguration.
- **Stale presence data**: Warn if `time_last_present` on an item is significantly older than expected -- the item may have left range without a departure event.
- **Unverified TLS on subscriptions**: Flag subscriptions where `verify_target_certificate=false` -- events are being delivered without certificate validation.
- **Read-only key used for mutation**: If `GET /authinfo` returns `permissions.mutate=false`, proactively warn before attempting any POST/PUT/DELETE call.
- **Large list sets**: Surface when an itemlist or spotlist `total` is high (e.g., >1000) as bulk operations on these may be slow or hit timeouts.

## Playbook

### 1. Track an Item Through Locations in Real Time

1. `GET /items?code_hex={tagCode}` to find the item by its RFID/NFC code
2. Note the `id` from the result
3. `POST /subscriptions` with `topic_filter=items.{id}.moved` and your `target_url`
4. Receive webhook events whenever the item moves between locations
5. `GET /presences?item={id}` at any time to see current location and proximity

### 2. Set Up a Geofence (Disallow Rule)

1. `GET /locations` to find the source and restricted location IDs
2. `POST /locationrules` with `type=disallow`, `conditions.from_location={sourceId}`, `conditions.to_location={restrictedId}`, and `enabled=true`
3. `POST /subscriptions` with `topic_filter=locationrules.*.triggered` to get alerts
4. Verify with `GET /locationrules/{id}` to confirm the rule is active

### 3. Upload and Attach a Blob to an Item

1. `POST /blobs` with `filename` and `content_type` to create a blob record
2. Capture `resource.id` from the response
3. `POST /blobs/{id}/upload` with the file binary in the request body
4. `PUT /items/{itemId}` with `metadata: {blob_id: "{blobId}"}` to link the blob
5. Later retrieve via `GET /blobs/{id}/download/{filename}`

### 4. Build an Event-Driven Dashboard

1. `GET /spots` to list all reader hardware and their online status
2. `GET /locations` to map location IDs to labels
3. `POST /subscriptions` with `topic_filter=*` and `populate_events=true` for a firehose subscription
4. `GET /subscriptions/{id}/events?sort=-id&limit=50` to poll recent events (or use the webhook `target_url` for push)
5. `GET /items?is_present=true&populate=location` to snapshot current item distribution

### 5. Manage API Keys for Team Access

1. `GET /authinfo` to verify your current permissions (must have `mutate=true`)
2. `POST /keys` with `label="team-member-name"` and `is_read_only=true` for read-only access
3. Share the `secret` from `GET /keys/{id}` -- this is the only time the full key is readable
4. To revoke access: `DELETE /keys/{id}`
5. Audit existing keys: `GET /keys?select=id,label,is_read_only` for a summary view


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
