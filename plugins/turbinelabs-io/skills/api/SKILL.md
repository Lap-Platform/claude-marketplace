---
name: turbine-labs-api
description: "Turbine Labs API skill. Use when working with Turbine Labs for admin, changelog, zone. Covers 44 endpoints."
version: 1.0.0
generator: lapsh
---

# Turbine Labs API
API version: 1.0

## Auth
ApiKey Authorization in header

## Base URL
https://api.turbinelabs.io/v1.0

## Setup
1. Set your API key in the appropriate header
2. GET /admin/user/self -- verify access
3. POST /admin/user/self/access_tokens -- create first access_tokens

## Endpoints

44 endpoints across 9 groups. See references/api-spec.lap for full details.

### admin
| Method | Path | Description |
|--------|------|-------------|
| GET | /admin/user/self | Returns the user object for the account authorized and making this request. |
| GET | /admin/user/self/access_tokens | Lists Access Tokens that are configured for the authenticated user. |
| POST | /admin/user/self/access_tokens | Creates a new Access Token and associates it with the authenticated user. |
| DELETE | /admin/user/self/access_token/{access-token-key} | Delete the specified access token. |

### changelog
| Method | Path | Description |
|--------|------|-------------|
| GET | /changelog/adhoc | Allows an arbitrary filter to be specified and applied to the org\'s change log. |
| GET | /changelog/domain-graph/{domainKey} | get changes related to the indicated domain |
| GET | /changelog/route-graph/{routeKey} | get changes related to the indicated route |
| GET | /changelog/shared-rules-graph/{sharedRulesKey} | get changes related to the indicated SharedRules |
| GET | /changelog/cluster-graph/{clusterKey} | get changes related to the indicated cluster |
| GET | /changelog/zone/{zoneKey} | get changes in a specified zone |

### zone
| Method | Path | Description |
|--------|------|-------------|
| GET | /zone | get a list of zones |
| POST | /zone | create zone |
| GET | /zone/{zoneKey} | get zone |
| DELETE | /zone/{zoneKey} | delete zone |

### domain
| Method | Path | Description |
|--------|------|-------------|
| GET | /domain | get domains |
| POST | /domain | create domain |
| GET | /domain/{domainKey} | get domain |
| DELETE | /domain/{domainKey} | delete domain |

### proxy
| Method | Path | Description |
|--------|------|-------------|
| GET | /proxy | list proxies |
| POST | /proxy | create proxy |
| GET | /proxy/{proxyKey} | get proxy |
| DELETE | /proxy/{proxyKey} | delete proxy |

### listener
| Method | Path | Description |
|--------|------|-------------|
| GET | /listener | list listeners |
| POST | /listener | create listener |
| GET | /listener/{listenerKey} | get listener |
| PUT | /listener/{listenerKey} | modify listener |
| DELETE | /listener/{listenerKey} | delete listener |

### shared_rules
| Method | Path | Description |
|--------|------|-------------|
| GET | /shared_rules | get shared_rules |
| POST | /shared_rules | create shared_rules |
| GET | /shared_rules/{sharedRulesKey} | get shared_rules object |
| PUT | /shared_rules/{sharedRulesKey} | modify shared_rules object |
| DELETE | /shared_rules/{sharedRulesKey} | delete shared_rules object |

### route
| Method | Path | Description |
|--------|------|-------------|
| GET | /route | get routes |
| POST | /route | create route |
| GET | /route/{routeKey} | get route |
| PUT | /route/{routeKey} | modify route |
| DELETE | /route/{routeKey} | delete route |

### cluster
| Method | Path | Description |
|--------|------|-------------|
| GET | /cluster | get clusters |
| POST | /cluster | create cluster |
| GET | /cluster/{clusterKey} | get cluster |
| PUT | /cluster/{clusterKey} | modify cluster |
| DELETE | /cluster/{clusterKey} | delete cluster |
| POST | /cluster/{clusterKey}/instances | add instance |
| DELETE | /cluster/{clusterKey}/instances/{instanceIdentifier} | remove instance |

## Enhanced Skill Content
## Question Mapping

- "Who am I logged in as?" -> GET /admin/user/self
- "List my API access tokens" -> GET /admin/user/self/access_tokens
- "Create a new access token" -> POST /admin/user/self/access_tokens
- "Revoke an access token" -> DELETE /admin/user/self/access_token/{access-token-key}
- "What changed recently in my zone?" -> GET /changelog/zone/{zoneKey}
- "Show the change history for a specific cluster" -> GET /changelog/cluster-graph/{clusterKey}
- "List all zones" -> GET /zone
- "Get details for a specific domain" -> GET /domain/{domainKey}
- "Register a new cluster" -> POST /cluster
- "Add an instance to a cluster" -> POST /cluster/{clusterKey}/instances
- "Remove an instance from a cluster" -> DELETE /cluster/{clusterKey}/instances/{instanceIdentifier}
- "Update routing rules for a route" -> PUT /route/{routeKey}
- "Delete a domain and clean up" -> DELETE /domain/{domainKey}
- "List all listeners and their configurations" -> GET /listener
- "What shared rules are applied across my routes?" -> GET /shared_rules

## Response Tips

- **Admin endpoints**: Returns user profile and token arrays directly; token creation returns the full token object including the secret (only shown once).
- **Changelog endpoints**: Results are time-ordered; use `start`/`end` for date ranges and `max_results` to cap output; `ref_id` + `direction` enable cursor-based pagination.
- **CRUD resources (zone, domain, proxy, listener, shared_rules, route, cluster)**: List endpoints return arrays of objects; single-resource GETs return the object with a `checksum` field required for DELETE and PUT operations.
- **Delete operations**: All deletes require a `checksum` parameter for optimistic concurrency; fetch the resource first to obtain the current checksum.
- **Cluster instances**: Instance endpoints are nested under `/cluster/{clusterKey}/instances`; the instance identifier in the DELETE path is distinct from the cluster key.

## Anomaly Flags

- **Checksum mismatch on delete/update**: If a DELETE or PUT fails, the resource was modified since last read. Re-fetch and retry. Surface this as a concurrent modification warning.
- **Empty changelog results**: If changelog queries return no entries for a wide time range, the resource may have been recreated or the key may be stale.
- **Orphaned resources**: After deleting a zone, check for domains, routes, and clusters that may still reference it. Surface any dangling references.
- **Token proliferation**: If GET /admin/user/self/access_tokens returns a large number of tokens, flag that unused tokens should be revoked for security hygiene.
- **Missing checksum in responses**: If a resource response lacks a checksum field, the resource may be in a transitional state. Warn before attempting mutations.
- **Listener without routes**: A listener with no associated routes is accepting traffic with nowhere to send it. Flag after creation.

## Playbook

### 1. Set up a new traffic route end-to-end

1. GET /zone to find your target zone (or POST /zone to create one)
2. POST /cluster with your backend service definition
3. POST /cluster/{clusterKey}/instances to register backend instances
4. POST /domain to define the domain that receives traffic
5. POST /shared_rules if you need common rules across routes
6. POST /route linking the domain to the cluster
7. POST /listener to bind a port and start accepting traffic

### 2. Rotate an access token

1. GET /admin/user/self/access_tokens to list current tokens
2. POST /admin/user/self/access_tokens with a description for the new token
3. Save the returned token secret immediately (shown only once)
4. Update your client configuration to use the new token
5. DELETE /admin/user/self/access_token/{access-token-key} to revoke the old token (fetch checksum first)

### 3. Investigate recent changes to a route

1. GET /route/{routeKey} to confirm the route exists and note its current state
2. GET /changelog/route-graph/{routeKey} with `max_results=20` to see recent changes
3. Narrow with `start` and `end` timestamps if investigating a specific incident window
4. Cross-reference with GET /changelog/cluster-graph/{clusterKey} for any backend changes in the same period

### 4. Scale a cluster by adding/removing instances

1. GET /cluster/{clusterKey} to review the current cluster and its checksum
2. POST /cluster/{clusterKey}/instances with the new instance definition to scale up
3. To scale down: identify the target instance identifier from the cluster details
4. DELETE /cluster/{clusterKey}/instances/{instanceIdentifier} with the current checksum
5. GET /cluster/{clusterKey} again to verify the updated instance list

### 5. Decommission a domain safely

1. GET /route with filters to find all routes referencing the domain
2. For each route: PUT /route/{routeKey} to redirect traffic or DELETE /route/{routeKey} with its checksum
3. GET /listener to check for listeners bound to the domain; update or delete as needed
4. GET /domain/{domainKey} to retrieve the current checksum
5. DELETE /domain/{domainKey} with the checksum
6. GET /changelog/domain-graph/{domainKey} to confirm the deletion event was recorded


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
