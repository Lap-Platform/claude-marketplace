---
name: aws-outposts
description: "AWS Outposts API skill. Use when working with AWS Outposts for outposts, orders, sites. Covers 31 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Outposts
API version: 2019-12-03

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /capacity/tasks -- verify access
3. POST /outposts/{OutpostId}/capacity/{CapacityTaskId} -- create first capacity

## Endpoints

31 endpoints across 8 groups. See references/api-spec.lap for full details.

### outposts
| Method | Path | Description |
|--------|------|-------------|
| POST | /outposts/{OutpostId}/capacity/{CapacityTaskId} | Cancels the capacity task. |
| POST | /outposts | Creates an Outpost. You can specify either an Availability one or an AZ ID. |
| DELETE | /outposts/{OutpostId} | Deletes the specified Outpost. |
| GET | /outposts/{OutpostId}/capacity/{CapacityTaskId} | Gets details of the specified capacity task. |
| GET | /outposts/{OutpostId} | Gets information about the specified Outpost. |
| GET | /outposts/{OutpostId}/instanceTypes | Gets the instance types for the specified Outpost. |
| GET | /outposts/{OutpostId}/supportedInstanceTypes | Gets the instance types that an Outpost can support in InstanceTypeCapacity. This will generally include instance types that are not currently configured and therefore cannot be launched with the current Outpost capacity configuration. |
| GET | /outposts/{OutpostId}/assets | Lists the hardware assets for the specified Outpost. Use filters to return specific results. If you specify multiple filters, the results include only the resources that match all of the specified filters. For a filter where you can specify multiple values, the results include items that match any of the values that you specify for the filter. |
| GET | /outposts | Lists the Outposts for your Amazon Web Services account. Use filters to return specific results. If you specify multiple filters, the results include only the resources that match all of the specified filters. For a filter where you can specify multiple values, the results include items that match any of the values that you specify for the filter. |
| POST | /outposts/{OutpostId}/capacity | Starts the specified capacity task. You can have one active capacity task for an order. |
| PATCH | /outposts/{OutpostId} | Updates an Outpost. |

### orders
| Method | Path | Description |
|--------|------|-------------|
| POST | /orders/{OrderId}/cancel | Cancels the specified order for an Outpost. |
| POST | /orders | Creates an order for an Outpost. |
| GET | /orders/{OrderId} | Gets information about the specified order. |

### sites
| Method | Path | Description |
|--------|------|-------------|
| POST | /sites | Creates a site for an Outpost. |
| DELETE | /sites/{SiteId} | Deletes the specified site. |
| GET | /sites/{SiteId} | Gets information about the specified Outpost site. |
| GET | /sites/{SiteId}/address | Gets the site address of the specified site. |
| GET | /sites | Lists the Outpost sites for your Amazon Web Services account. Use filters to return specific results. Use filters to return specific results. If you specify multiple filters, the results include only the resources that match all of the specified filters. For a filter where you can specify multiple values, the results include items that match any of the values that you specify for the filter. |
| PATCH | /sites/{SiteId} | Updates the specified site. |
| PUT | /sites/{SiteId}/address | Updates the address of the specified site. You can't update a site address if there is an order in progress. You must wait for the order to complete or cancel the order. You can update the operating address before you place an order at the site, or after all Outposts that belong to the site have been deactivated. |
| PATCH | /sites/{SiteId}/rackPhysicalProperties | Update the physical and logistical details for a rack at a site. For more information about hardware requirements for racks, see Network readiness checklist in the Amazon Web Services Outposts User Guide.  To update a rack at a site with an order of IN_PROGRESS, you must wait for the order to complete or cancel the order. |

### catalog
| Method | Path | Description |
|--------|------|-------------|
| GET | /catalog/item/{CatalogItemId} | Gets information about the specified catalog item. |
| GET | /catalog/items | Lists the items in the catalog. Use filters to return specific results. If you specify multiple filters, the results include only the resources that match all of the specified filters. For a filter where you can specify multiple values, the results include items that match any of the values that you specify for the filter. |

### connections
| Method | Path | Description |
|--------|------|-------------|
| GET | /connections/{ConnectionId} | Amazon Web Services uses this action to install Outpost servers.   Gets information about the specified connection.   Use CloudTrail to monitor this action or Amazon Web Services managed policy for Amazon Web Services Outposts to secure it. For more information, see  Amazon Web Services managed policies for Amazon Web Services Outposts and  Logging Amazon Web Services Outposts API calls with Amazon Web Services CloudTrail in the Amazon Web Services Outposts User Guide. |
| POST | /connections | Amazon Web Services uses this action to install Outpost servers.   Starts the connection required for Outpost server installation.   Use CloudTrail to monitor this action or Amazon Web Services managed policy for Amazon Web Services Outposts to secure it. For more information, see  Amazon Web Services managed policies for Amazon Web Services Outposts and  Logging Amazon Web Services Outposts API calls with Amazon Web Services CloudTrail in the Amazon Web Services Outposts User Guide. |

### capacity
| Method | Path | Description |
|--------|------|-------------|
| GET | /capacity/tasks | Lists the capacity tasks for your Amazon Web Services account. Use filters to return specific results. If you specify multiple filters, the results include only the resources that match all of the specified filters. For a filter where you can specify multiple values, the results include items that match any of the values that you specify for the filter. |

### list-orders
| Method | Path | Description |
|--------|------|-------------|
| GET | /list-orders | Lists the Outpost orders for your Amazon Web Services account. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{ResourceArn} | Lists the tags for the specified resource. |
| POST | /tags/{ResourceArn} | Adds tags to the specified resource. |
| DELETE | /tags/{ResourceArn} | Removes tags from the specified resource. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new Outpost?" -> POST /outposts
- "What Outposts do I have?" -> GET /outposts
- "Show me details for a specific Outpost" -> GET /outposts/{OutpostId}
- "What instance types are available on my Outpost?" -> GET /outposts/{OutpostId}/instanceTypes
- "How do I place an order for Outpost hardware?" -> POST /orders
- "What is the status of my order?" -> GET /orders/{OrderId}
- "How do I cancel an Outpost order?" -> POST /orders/{OrderId}/cancel
- "List all my Outpost sites" -> GET /sites
- "What are the rack specs for a site?" -> GET /sites/{SiteId} (check RackPhysicalProperties)
- "How do I update a site's shipping address?" -> PUT /sites/{SiteId}/address
- "What catalog items can I order?" -> GET /catalog/items
- "How do I start a capacity task on my Outpost?" -> POST /outposts/{OutpostId}/capacity
- "What assets are deployed on my Outpost?" -> GET /outposts/{OutpostId}/assets
- "How do I establish a local connection to an Outpost asset?" -> POST /connections
- "How do I tag an Outpost or site resource?" -> POST /tags/{ResourceArn}

## Response Tips

- **Outposts/Sites/Orders (list endpoints):** Paginated via `NextToken` + `MaxResults`. Keep calling with the returned `NextToken` until it is absent or null.
- **Single-resource GETs:** Response wraps the object in a top-level key (`Outpost`, `Site`, `Order`, `CatalogItem`). Fields are nullable -- always nil-check before accessing nested properties.
- **Capacity tasks:** `CapacityTaskStatus` drives the lifecycle. A non-null `Failed` object (with `Reason` and optional `Type`) means the task errored -- surface it immediately.
- **Connections:** Response returns `ConnectionId` and `UnderlayIpAddress` on creation; use `GET /connections/{ConnectionId}` to retrieve tunnel details (`ClientTunnelAddress`, `ServerTunnelAddress`, `AllowedIps`).
- **Tags:** `GET /tags/{ResourceArn}` returns a flat `map<str,str>`. `DELETE /tags/{ResourceArn}` requires `tagKeys` as a list of key names, not key-value pairs.

## Anomaly Flags

- **Order status stuck:** If `Order.Status` remains unchanged across repeated polls, flag that fulfillment may be stalled and suggest contacting AWS support.
- **Capacity task failure:** Surface `Failed.Reason` and `Failed.Type` immediately when `CapacityTaskStatus` is not progressing or the `Failed` object is present.
- **LifeCycleStatus unexpected values:** If an Outpost's `LifeCycleStatus` is anything other than `ACTIVE` (e.g., `PENDING`, `DECOMMISSIONING`), proactively warn the user before they attempt operations on it.
- **Pagination truncation:** If a list response returns `NextToken` but the user did not request all pages, warn that results are incomplete.
- **Empty instance type lists:** If `GET /outposts/{OutpostId}/instanceTypes` returns an empty `InstanceTypes` array, flag that the Outpost may not be fully provisioned yet.
- **Rack physical properties all null:** If a site's `RackPhysicalProperties` has all null fields, alert the user that site specs are incomplete -- this can block order fulfillment.
- **DryRun capacity responses:** When `DryRun: true` is returned, remind the user that no capacity was actually allocated.

## Playbook

### 1. Provision a New Outpost End-to-End

1. Create a site: `POST /sites` with `Name`, `OperatingAddress`, and `RackPhysicalProperties`.
2. Set the site address: `PUT /sites/{SiteId}/address` with `AddressType: SHIPPING_ADDRESS`.
3. Create the Outpost: `POST /outposts` with `Name`, `SiteId`, and desired `AvailabilityZone`.
4. Browse the catalog: `GET /catalog/items` to find the right `CatalogItemId` for your needs.
5. Place an order: `POST /orders` with `OutpostIdentifier`, `LineItems` referencing catalog items, and `PaymentOption`.
6. Monitor the order: Poll `GET /orders/{OrderId}` until `Status` shows fulfillment.

### 2. Start and Monitor a Capacity Task

1. Identify the Outpost and order: Note `OutpostId` and `OrderId` from previous steps.
2. Check supported instance types: `GET /outposts/{OutpostId}/supportedInstanceTypes` with the `OrderId`.
3. Start capacity allocation: `POST /outposts/{OutpostId}/capacity` with `InstancePools` (optionally set `DryRun: true` first).
4. Poll task status: `GET /outposts/{OutpostId}/capacity/{CapacityTaskId}` until `CapacityTaskStatus` is terminal.
5. If `Failed` is present, read `Failed.Reason` and adjust instance pools or contact support.

### 3. Manage Site Infrastructure Details

1. Retrieve site info: `GET /sites/{SiteId}` to review current configuration.
2. Update rack specs: `PATCH /sites/{SiteId}/rackPhysicalProperties` with power, uplink, and weight parameters.
3. Update site metadata: `PATCH /sites/{SiteId}` to change `Name`, `Description`, or `Notes`.
4. Verify address: `GET /sites/{SiteId}/address` with `AddressType: OPERATING_ADDRESS` to confirm.

### 4. Establish a Local Connection to an Outpost Asset

1. List assets: `GET /outposts/{OutpostId}/assets` to find the target `AssetId`.
2. Create connection: `POST /connections` with `AssetId`, `ClientPublicKey`, and `NetworkInterfaceDeviceIndex`.
3. Retrieve tunnel details: `GET /connections/{ConnectionId}` to get `ServerEndpoint`, tunnel addresses, and `AllowedIps`.
4. Configure local WireGuard or tunnel client using the returned keys and addresses.

### 5. Tag and Organize Resources

1. Get the resource ARN from any Outpost or Site response (`OutpostArn` or `SiteArn`).
2. Add tags: `POST /tags/{ResourceArn}` with a `Tags` map (e.g., `{"env": "production", "team": "infra"}`).
3. Verify tags: `GET /tags/{ResourceArn}` to confirm they were applied.
4. Remove tags: `DELETE /tags/{ResourceArn}` with `tagKeys: ["env"]` to remove specific keys.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
