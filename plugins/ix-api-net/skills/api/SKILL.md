---
name: ix-api
description: "IX-API API skill. Use when working with IX-API for auth, facilities, devices. Covers 115 endpoints."
version: 1.0.0
generator: lapsh
---

# IX-API
API version: 2.7.1

## Auth
Bearer bearer | OAuth2

## Base URL
/api/v2

## Setup
1. Set Authorization header with your Bearer token
2. GET /facilities -- verify access
3. POST /auth/token -- create first token

## Endpoints

115 endpoints across 27 groups. See references/api-spec.lap for full details.

### auth
| Method | Path | Description |
|--------|------|-------------|
| POST | /auth/token | Create Auth Token |
| POST | /auth/refresh | Refresh Auth Token |

### facilities
| Method | Path | Description |
|--------|------|-------------|
| GET | /facilities | List (Query) |
| GET | /facilities/{id} | Read |

### devices
| Method | Path | Description |
|--------|------|-------------|
| GET | /devices | List (Query) |
| GET | /devices/{id} | Read |

### pops
| Method | Path | Description |
|--------|------|-------------|
| GET | /pops | List (Query) |
| GET | /pops/{id} | Read |

### metro-area-networks
| Method | Path | Description |
|--------|------|-------------|
| GET | /metro-area-networks | List (Query) |
| GET | /metro-area-networks/{id} | Read |

### metro-areas
| Method | Path | Description |
|--------|------|-------------|
| GET | /metro-areas | List (Query) |
| GET | /metro-areas/{id} | Read |

### product-offerings
| Method | Path | Description |
|--------|------|-------------|
| GET | /product-offerings | List (Query) |
| GET | /product-offerings/{id} | Read |

### availability-zones
| Method | Path | Description |
|--------|------|-------------|
| GET | /availability-zones | List (Query) |
| GET | /availability-zones/{id} | Read |

### ports
| Method | Path | Description |
|--------|------|-------------|
| GET | /ports | List (Query) |
| GET | /ports/{id} | Read |
| GET | /ports/{id}/statistics | Read Statistics |
| GET | /ports/{id}/statistics/{aggregate}/timeseries | Read Statistics Timeseries |

### port-reservations
| Method | Path | Description |
|--------|------|-------------|
| GET | /port-reservations | List (Query) |
| POST | /port-reservations | Create |
| GET | /port-reservations/{id} | Read |
| PUT | /port-reservations/{id} | Update (Deprecated) |
| PATCH | /port-reservations/{id} | Update |
| DELETE | /port-reservations/{id} | Request Decommission |
| GET | /port-reservations/{id}/cancellation-policy | Read Cancellation Policy |
| GET | /port-reservations/{id}/loa | Download LOA |
| POST | /port-reservations/{id}/loa | Upload LOA |

### connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /connections | List (Query) |
| POST | /connections | Create |
| GET | /connections/{id} | Read |
| PUT | /connections/{id} | Update (Deprecated) |
| PATCH | /connections/{id} | Update |
| DELETE | /connections/{id} | Request Decommission |
| GET | /connections/{id}/statistics | Read Statistics |
| GET | /connections/{id}/statistics/{aggregate}/timeseries | Read Statistics Timeseries |
| GET | /connections/{id}/loa | Download LOA |
| POST | /connections/{id}/loa | Upload LOA |
| GET | /connections/{id}/cancellation-policy | Read Cancellation Policy |

### network-service-configs
| Method | Path | Description |
|--------|------|-------------|
| GET | /network-service-configs | List (Query) |
| POST | /network-service-configs | Create |
| GET | /network-service-configs/{id} | Read |
| PUT | /network-service-configs/{id} | Update (Deprecated) |
| PATCH | /network-service-configs/{id} | Update |
| DELETE | /network-service-configs/{id} | Request Decommission |
| GET | /network-service-configs/{id}/statistics | Read Statistics |
| GET | /network-service-configs/{id}/statistics/{aggregate}/timeseries | Read Statistics Timeseries |
| GET | /network-service-configs/{id}/peer-statistics | Read Peer Statistics |
| GET | /network-service-configs/{id}/peer-statistics/{aggregate}/timeseries | Read Peer Statistics Timeseries |
| GET | /network-service-configs/{id}/cancellation-policy | Read Cancellation Policy |

### network-feature-configs
| Method | Path | Description |
|--------|------|-------------|
| GET | /network-feature-configs | List (Query) |
| POST | /network-feature-configs | Create |
| GET | /network-feature-configs/{id} | Read |
| PUT | /network-feature-configs/{id} | Update (Deprecated) |
| PATCH | /network-feature-configs/{id} | Update |
| DELETE | /network-feature-configs/{id} | Request Decommission |

### account
| Method | Path | Description |
|--------|------|-------------|
| GET | /account | Read |

### accounts
| Method | Path | Description |
|--------|------|-------------|
| GET | /accounts | List (Query) |
| POST | /accounts | Create |
| GET | /accounts/{id} | Read |
| PUT | /accounts/{id} | Update (Deprecated) |
| PATCH | /accounts/{id} | Update |
| DELETE | /accounts/{id} | Destroy |

### roles
| Method | Path | Description |
|--------|------|-------------|
| GET | /roles | List (Query) |
| GET | /roles/{id} | Read |

### contacts
| Method | Path | Description |
|--------|------|-------------|
| GET | /contacts | List (Query) |
| POST | /contacts | Create |
| GET | /contacts/{id} | Read |
| PUT | /contacts/{id} | Update (Deprecated) |
| PATCH | /contacts/{id} | Update |
| DELETE | /contacts/{id} | Destroy |

### role-assignments
| Method | Path | Description |
|--------|------|-------------|
| GET | /role-assignments | List (Query) |
| POST | /role-assignments | Create |
| GET | /role-assignments/{id} | Read |
| DELETE | /role-assignments/{id} | Destroy |

### health
| Method | Path | Description |
|--------|------|-------------|
| GET | /health | Read |

### implementation
| Method | Path | Description |
|--------|------|-------------|
| GET | /implementation | Read |

### extensions
| Method | Path | Description |
|--------|------|-------------|
| GET | /extensions | List (Query) |

### ips
| Method | Path | Description |
|--------|------|-------------|
| GET | /ips | List (Query) |
| POST | /ips | Create |
| GET | /ips/{id} | Read |
| PUT | /ips/{id} | Update |
| PATCH | /ips/{id} | Update |

### macs
| Method | Path | Description |
|--------|------|-------------|
| GET | /macs | List (Query) |
| POST | /macs | Create |
| GET | /macs/{id} | Read |
| DELETE | /macs/{id} | Destroy |

### network-services
| Method | Path | Description |
|--------|------|-------------|
| GET | /network-services | List (Query) |
| POST | /network-services | Create |
| GET | /network-services/{id} | Read |
| PUT | /network-services/{id} | Update (Deprecated) |
| PATCH | /network-services/{id} | Update |
| DELETE | /network-services/{id} | Request Decommission |
| GET | /network-services/{id}/statistics | Read Statistics |
| GET | /network-services/{id}/statistics/{aggregate}/timeseries | Read Statistics Timeseries |
| GET | /network-services/{id}/rtt-statistics | Read RTT Statistics |
| GET | /network-services/{id}/change-request | Read Change Request |
| POST | /network-services/{id}/change-request | Create Change Request |
| DELETE | /network-services/{id}/change-request | Delete Change Request |
| GET | /network-services/{id}/cancellation-policy | Read Cancellation Policy |

### network-features
| Method | Path | Description |
|--------|------|-------------|
| GET | /network-features | List (Query) |
| GET | /network-features/{id} | Read |

### member-joining-rules
| Method | Path | Description |
|--------|------|-------------|
| GET | /member-joining-rules | List (Query) |
| POST | /member-joining-rules | Create |
| GET | /member-joining-rules/{id} | Read |
| PUT | /member-joining-rules/{id} | Update (Deprecated) |
| PATCH | /member-joining-rules/{id} | Update |
| DELETE | /member-joining-rules/{id} | Destroy |

### routing-functions
| Method | Path | Description |
|--------|------|-------------|
| GET | /routing-functions | List (Query) |
| POST | /routing-functions | Create |
| GET | /routing-functions/{id} | Read |
| PATCH | /routing-functions/{id} | Update |
| DELETE | /routing-functions/{id} | Request Decommission |
| GET | /routing-functions/{id}/cancellation-policy | Read Cancellation Policy |

## Enhanced Skill Content
## Question Mapping

- "How do I authenticate with IX-API?" -> POST /auth/token
- "My token expired, how do I get a new one?" -> POST /auth/refresh
- "What facilities are available in a specific metro area?" -> GET /facilities (with `metro_area` filter)
- "Show me all my active connections" -> GET /connections (with `state` filter and `managing_account`)
- "What ports are assigned to a connection?" -> GET /ports (with `connection` filter)
- "How do I order a new connection at a specific PoP?" -> POST /connections (requires `product_offering`, `mode`, `pop` via offering)
- "What product offerings support cloud connectivity?" -> GET /product-offerings (with `type=cloud_vc`)
- "How much bandwidth is my port using?" -> GET /ports/{id}/statistics
- "What is my cancellation window for a network service?" -> GET /network-services/{id}/cancellation-policy
- "List all accounts I manage" -> GET /accounts (with `managing_account` filter)
- "How do I set up a peering session on an exchange LAN?" -> POST /network-service-configs (with `type=exchange_lan`)
- "What IP addresses are allocated to my service config?" -> GET /ips (with `network_service_config` filter)
- "Is the IX-API healthy right now?" -> GET /health
- "What network service types does this implementation support?" -> GET /implementation
- "How do I decommission a connection with a future date?" -> DELETE /connections/{id} (with `decommission_at`)

## Response Tips

- **List endpoints** (facilities, connections, ports, etc.): Return 200 for complete results or 206 for partial -- always check for `page_token` in the response to fetch the next page. Use `page_limit` and `page_offset` for cursor control.
- **Create/Update endpoints**: POST returns 201, PUT/PATCH return 202 (accepted, may provision asynchronously) -- poll the resource by ID to track `state` and `status` progression.
- **Statistics endpoints**: The `aggregates` map keys vary by resource type; timeseries `samples` are arrays of arrays where column order matches the `fields` array.
- **Polymorphic resources** (network-services, network-service-configs, network-feature-configs, member-joining-rules): The `type` field in requests and responses determines the full schema -- always include `type` to interpret the payload correctly.
- **Error responses**: 400 = invalid input, 401 = expired or missing token, 403 = insufficient permissions, 404 = resource not found, 409 = conflict (contact deletion with active assignments).

## Anomaly Flags

- **State = "decommissioning" or unexpected state**: Surface when any managed resource (connection, port, network service) enters a decommission or error state without explicit user action.
- **206 Partial Content without pagination follow-up**: Warn when a list response returns 206, indicating more results exist that the caller has not fetched.
- **`charged_until` date approaching**: Proactively flag when a cancellation policy shows billing continuing past the intended decommission date.
- **`status` array contains error or warning entries**: The `status: [map]` field on connections, ports, and accounts can contain provisioning warnings -- surface any non-normal status entries.
- **Token expiry**: If a 401 is returned on a previously authenticated call, prompt for token refresh via POST /auth/refresh before retrying.
- **`capacity_allocation_limit` near `capacity_allocated`**: On connections, flag when allocated capacity is approaching the limit to prevent failed service config provisioning.
- **409 Conflict on contact deletion**: Indicates the contact still has active role assignments -- surface this and suggest removing assignments first.

## Playbook

### 1. Provision a New Exchange LAN Peering Connection

1. Authenticate: POST /auth/token with `api_key` and `api_secret`
2. Find a metro area: GET /metro-areas, pick the target metro
3. List product offerings: GET /product-offerings with `type=exchange_lan` and `handover_metro_area={metro_id}`
4. Create the connection: POST /connections with the chosen `product_offering`, `mode`, account IDs, and `port_quantity`
5. Wait for port reservations to appear: GET /connections/{id} and check `port_reservations` array
6. Download LOA: GET /connections/{id}/loa to hand to the facility for cross-connect
7. Create a network service config: POST /network-service-configs with `type=exchange_lan`, referencing the connection and network service
8. Assign IPs: POST /ips with the service config reference and your peering IP

### 2. Monitor Port and Connection Bandwidth

1. List active ports: GET /ports with `state=production`
2. For each port, fetch aggregate stats: GET /ports/{id}/statistics with desired `start` and `end` range
3. Drill into timeseries: GET /ports/{id}/statistics/{aggregate}/timeseries with `fields` to select specific metrics
4. Repeat for connections: GET /connections/{id}/statistics and the corresponding timeseries endpoint
5. Compare `capacity_allocated` from GET /connections/{id} against observed throughput to identify saturation

### 3. Set Up Account Hierarchy with Contacts and Roles

1. Create a sub-account: POST /accounts with `managing_account` set to your parent account ID
2. Create a contact: POST /contacts with `managing_account` and `consuming_account` referencing the new account
3. List available roles: GET /roles to find the role ID (e.g., technical, billing, admin)
4. Assign the contact to a role: POST /role-assignments with the `role` and `contact` IDs
5. Reference the role assignment ID when creating connections or services (the `role_assignments` array)

### 4. Decommission a Network Service Gracefully

1. Check the cancellation policy: GET /network-services/{id}/cancellation-policy with desired `decommission_at` date
2. Review `charged_until` in the response to understand billing impact
3. If acceptable, delete with future date: DELETE /network-services/{id} with `decommission_at` in the body
4. Monitor state: GET /network-services/{id} periodically -- state will transition through decommissioning
5. Clean up related configs: DELETE /network-service-configs/{id} for any configs attached to this service

### 5. Upgrade a Network Service via Change Request

1. List available product offerings: GET /product-offerings with `type` matching your service and `upgrade_allowed=true`
2. Check current service: GET /network-services/{id} to note the current `product_offering`
3. Submit the change request: POST /network-services/{id}/change-request with the new `product_offering` and optional `capacity`
4. Review pending change: GET /network-services/{id}/change-request to confirm details
5. To abort: DELETE /network-services/{id}/change-request before it is applied


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
