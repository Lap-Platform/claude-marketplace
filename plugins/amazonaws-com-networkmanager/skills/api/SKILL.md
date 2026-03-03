---
name: aws-network-manager
description: "AWS Network Manager API skill. Use when working with AWS Network Manager for attachments, global-networks, connect-attachments. Covers 85 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Network Manager
API version: 2019-07-05

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /global-networks -- verify access
3. POST /attachments/{attachmentId}/accept -- create first accept

## Endpoints

85 endpoints across 13 groups. See references/api-spec.lap for full details.

### attachments
| Method | Path | Description |
|--------|------|-------------|
| POST | /attachments/{attachmentId}/accept | Accepts a core network attachment request.  Once the attachment request is accepted by a core network owner, the attachment is created and connected to a core network. |
| DELETE | /attachments/{attachmentId} | Deletes an attachment. Supports all attachment types. |
| GET | /attachments | Returns a list of core network attachments. |
| POST | /attachments/{attachmentId}/reject | Rejects a core network attachment request. |

### global-networks
| Method | Path | Description |
|--------|------|-------------|
| POST | /global-networks/{globalNetworkId}/connect-peer-associations | Associates a core network Connect peer with a device and optionally, with a link.  If you specify a link, it must be associated with the specified device. You can only associate core network Connect peers that have been created on a core network Connect attachment on a core network. |
| POST | /global-networks/{globalNetworkId}/customer-gateway-associations | Associates a customer gateway with a device and optionally, with a link. If you specify a link, it must be associated with the specified device.  You can only associate customer gateways that are connected to a VPN attachment on a transit gateway or core network registered in your global network. When you register a transit gateway or core network, customer gateways that are connected to the transit gateway are automatically included in the global network. To list customer gateways that are connected to a transit gateway, use the DescribeVpnConnections EC2 API and filter by transit-gateway-id. You cannot associate a customer gateway with more than one device and link. |
| POST | /global-networks/{globalNetworkId}/link-associations | Associates a link to a device. A device can be associated to multiple links and a link can be associated to multiple devices. The device and link must be in the same global network and the same site. |
| POST | /global-networks/{globalNetworkId}/transit-gateway-connect-peer-associations | Associates a transit gateway Connect peer with a device, and optionally, with a link. If you specify a link, it must be associated with the specified device.  You can only associate transit gateway Connect peers that have been created on a transit gateway that's registered in your global network. You cannot associate a transit gateway Connect peer with more than one device and link. |
| POST | /global-networks/{globalNetworkId}/connections | Creates a connection between two devices. The devices can be a physical or virtual appliance that connects to a third-party appliance in a VPC, or a physical appliance that connects to another physical appliance in an on-premises network. |
| POST | /global-networks/{globalNetworkId}/devices | Creates a new device in a global network. If you specify both a site ID and a location, the location of the site is used for visualization in the Network Manager console. |
| POST | /global-networks | Creates a new, empty global network. |
| POST | /global-networks/{globalNetworkId}/links | Creates a new link for a specified site. |
| POST | /global-networks/{globalNetworkId}/sites | Creates a new site in a global network. |
| DELETE | /global-networks/{globalNetworkId}/connections/{connectionId} | Deletes the specified connection in your global network. |
| DELETE | /global-networks/{globalNetworkId}/devices/{deviceId} | Deletes an existing device. You must first disassociate the device from any links and customer gateways. |
| DELETE | /global-networks/{globalNetworkId} | Deletes an existing global network. You must first delete all global network objects (devices, links, and sites), deregister all transit gateways, and delete any core networks. |
| DELETE | /global-networks/{globalNetworkId}/links/{linkId} | Deletes an existing link. You must first disassociate the link from any devices and customer gateways. |
| DELETE | /global-networks/{globalNetworkId}/sites/{siteId} | Deletes an existing site. The site cannot be associated with any device or link. |
| DELETE | /global-networks/{globalNetworkId}/transit-gateway-registrations/{transitGatewayArn} | Deregisters a transit gateway from your global network. This action does not delete your transit gateway, or modify any of its attachments. This action removes any customer gateway associations. |
| GET | /global-networks | Describes one or more global networks. By default, all global networks are described. To describe the objects in your global network, you must use the appropriate Get* action. For example, to list the transit gateways in your global network, use GetTransitGatewayRegistrations. |
| DELETE | /global-networks/{globalNetworkId}/connect-peer-associations/{connectPeerId} | Disassociates a core network Connect peer from a device and a link. |
| DELETE | /global-networks/{globalNetworkId}/customer-gateway-associations/{customerGatewayArn} | Disassociates a customer gateway from a device and a link. |
| DELETE | /global-networks/{globalNetworkId}/link-associations | Disassociates an existing device from a link. You must first disassociate any customer gateways that are associated with the link. |
| DELETE | /global-networks/{globalNetworkId}/transit-gateway-connect-peer-associations/{transitGatewayConnectPeerArn} | Disassociates a transit gateway Connect peer from a device and link. |
| GET | /global-networks/{globalNetworkId}/connect-peer-associations | Returns information about a core network Connect peer associations. |
| GET | /global-networks/{globalNetworkId}/connections | Gets information about one or more of your connections in a global network. |
| GET | /global-networks/{globalNetworkId}/customer-gateway-associations | Gets the association information for customer gateways that are associated with devices and links in your global network. |
| GET | /global-networks/{globalNetworkId}/devices | Gets information about one or more of your devices in a global network. |
| GET | /global-networks/{globalNetworkId}/link-associations | Gets the link associations for a device or a link. Either the device ID or the link ID must be specified. |
| GET | /global-networks/{globalNetworkId}/links | Gets information about one or more links in a specified global network. If you specify the site ID, you cannot specify the type or provider in the same request. You can specify the type and provider in the same request. |
| GET | /global-networks/{globalNetworkId}/network-resource-count | Gets the count of network resources, by resource type, for the specified global network. |
| GET | /global-networks/{globalNetworkId}/network-resource-relationships | Gets the network resource relationships for the specified global network. |
| GET | /global-networks/{globalNetworkId}/network-resources | Describes the network resources for the specified global network. The results include information from the corresponding Describe call for the resource, minus any sensitive information such as pre-shared keys. |
| POST | /global-networks/{globalNetworkId}/network-routes | Gets the network routes of the specified global network. |
| GET | /global-networks/{globalNetworkId}/network-telemetry | Gets the network telemetry of the specified global network. |
| GET | /global-networks/{globalNetworkId}/route-analyses/{routeAnalysisId} | Gets information about the specified route analysis. |
| GET | /global-networks/{globalNetworkId}/sites | Gets information about one or more of your sites in a global network. |
| GET | /global-networks/{globalNetworkId}/transit-gateway-connect-peer-associations | Gets information about one or more of your transit gateway Connect peer associations in a global network. |
| GET | /global-networks/{globalNetworkId}/transit-gateway-registrations | Gets information about the transit gateway registrations in a specified global network. |
| POST | /global-networks/{globalNetworkId}/transit-gateway-registrations | Registers a transit gateway in your global network. Not all Regions support transit gateways for global networks. For a list of the supported Regions, see Region Availability in the Amazon Web Services Transit Gateways for Global Networks User Guide. The transit gateway can be in any of the supported Amazon Web Services Regions, but it must be owned by the same Amazon Web Services account that owns the global network. You cannot register a transit gateway in more than one global network. |
| POST | /global-networks/{globalNetworkId}/route-analyses | Starts analyzing the routing path between the specified source and destination. For more information, see Route Analyzer. |
| PATCH | /global-networks/{globalNetworkId}/connections/{connectionId} | Updates the information for an existing connection. To remove information for any of the parameters, specify an empty string. |
| PATCH | /global-networks/{globalNetworkId}/devices/{deviceId} | Updates the details for an existing device. To remove information for any of the parameters, specify an empty string. |
| PATCH | /global-networks/{globalNetworkId} | Updates an existing global network. To remove information for any of the parameters, specify an empty string. |
| PATCH | /global-networks/{globalNetworkId}/links/{linkId} | Updates the details for an existing link. To remove information for any of the parameters, specify an empty string. |
| PATCH | /global-networks/{globalNetworkId}/network-resources/{resourceArn}/metadata | Updates the resource metadata for the specified global network. |
| PATCH | /global-networks/{globalNetworkId}/sites/{siteId} | Updates the information for an existing site. To remove information for any of the parameters, specify an empty string. |

### connect-attachments
| Method | Path | Description |
|--------|------|-------------|
| POST | /connect-attachments | Creates a core network Connect attachment from a specified core network attachment.  A core network Connect attachment is a GRE-based tunnel attachment that you can use to establish a connection between a core network and an appliance. A core network Connect attachment uses an existing VPC attachment as the underlying transport mechanism. |
| GET | /connect-attachments/{attachmentId} | Returns information about a core network Connect attachment. |

### connect-peers
| Method | Path | Description |
|--------|------|-------------|
| POST | /connect-peers | Creates a core network Connect peer for a specified core network connect attachment between a core network and an appliance. The peer address and transit gateway address must be the same IP address family (IPv4 or IPv6). |
| DELETE | /connect-peers/{connectPeerId} | Deletes a Connect peer. |
| GET | /connect-peers/{connectPeerId} | Returns information about a core network Connect peer. |
| GET | /connect-peers | Returns a list of core network Connect peers. |

### core-networks
| Method | Path | Description |
|--------|------|-------------|
| POST | /core-networks | Creates a core network as part of your global network, and optionally, with a core network policy. |
| DELETE | /core-networks/{coreNetworkId} | Deletes a core network along with all core network policies. This can only be done if there are no attachments on a core network. |
| DELETE | /core-networks/{coreNetworkId}/core-network-policy-versions/{policyVersionId} | Deletes a policy version from a core network. You can't delete the current LIVE policy. |
| POST | /core-networks/{coreNetworkId}/core-network-change-sets/{policyVersionId}/execute | Executes a change set on your core network. Deploys changes globally based on the policy submitted.. |
| GET | /core-networks/{coreNetworkId} | Returns information about the LIVE policy for a core network. |
| GET | /core-networks/{coreNetworkId}/core-network-change-events/{policyVersionId} | Returns information about a core network change event. |
| GET | /core-networks/{coreNetworkId}/core-network-change-sets/{policyVersionId} | Returns a change set between the LIVE core network policy and a submitted policy. |
| GET | /core-networks/{coreNetworkId}/core-network-policy | Returns details about a core network policy. You can get details about your current live policy or any previous policy version. |
| GET | /core-networks/{coreNetworkId}/core-network-policy-versions | Returns a list of core network policy versions. |
| GET | /core-networks | Returns a list of owned and shared core networks. |
| POST | /core-networks/{coreNetworkId}/core-network-policy | Creates a new, immutable version of a core network policy. A subsequent change set is created showing the differences between the LIVE policy and the submitted policy. |
| POST | /core-networks/{coreNetworkId}/core-network-policy-versions/{policyVersionId}/restore | Restores a previous policy version as a new, immutable version of a core network policy. A subsequent change set is created showing the differences between the LIVE policy and restored policy. |
| PATCH | /core-networks/{coreNetworkId} | Updates the description of a core network. |

### site-to-site-vpn-attachments
| Method | Path | Description |
|--------|------|-------------|
| POST | /site-to-site-vpn-attachments | Creates an Amazon Web Services site-to-site VPN attachment on an edge location of a core network. |
| GET | /site-to-site-vpn-attachments/{attachmentId} | Returns information about a site-to-site VPN attachment. |

### transit-gateway-peerings
| Method | Path | Description |
|--------|------|-------------|
| POST | /transit-gateway-peerings | Creates a transit gateway peering connection. |
| GET | /transit-gateway-peerings/{peeringId} | Returns information about a transit gateway peer. |

### transit-gateway-route-table-attachments
| Method | Path | Description |
|--------|------|-------------|
| POST | /transit-gateway-route-table-attachments | Creates a transit gateway route table attachment. |
| GET | /transit-gateway-route-table-attachments/{attachmentId} | Returns information about a transit gateway route table attachment. |

### vpc-attachments
| Method | Path | Description |
|--------|------|-------------|
| POST | /vpc-attachments | Creates a VPC attachment on an edge location of a core network. |
| GET | /vpc-attachments/{attachmentId} | Returns information about a VPC attachment. |
| PATCH | /vpc-attachments/{attachmentId} | Updates a VPC attachment. |

### peerings
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /peerings/{peeringId} | Deletes an existing peering connection. |
| GET | /peerings | Lists the peerings for a core network. |

### resource-policy
| Method | Path | Description |
|--------|------|-------------|
| DELETE | /resource-policy/{resourceArn} | Deletes a resource policy for the specified resource. This revokes the access of the principals specified in the resource policy. |
| GET | /resource-policy/{resourceArn} | Returns information about a resource policy. |
| POST | /resource-policy/{resourceArn} | Creates or updates a resource policy. |

### organizations
| Method | Path | Description |
|--------|------|-------------|
| GET | /organizations/service-access | Gets the status of the Service Linked Role (SLR) deployment for the accounts in a given Amazon Web Services Organization. |
| POST | /organizations/service-access | Enables the Network Manager service for an Amazon Web Services Organization. This can only be called by a management account within the organization. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{resourceArn} | Lists the tags for a specified resource. |
| POST | /tags/{resourceArn} | Tags a specified resource. |
| DELETE | /tags/{resourceArn} | Removes tags from a specified resource. |

## Enhanced Skill Content
## Question Mapping

- "How do I list all my global networks?" -> GET /global-networks
- "What devices are registered in my global network?" -> GET /global-networks/{globalNetworkId}/devices
- "How do I attach a VPC to my core network?" -> POST /vpc-attachments
- "How do I accept a pending attachment?" -> POST /attachments/{attachmentId}/accept
- "What's the current policy on my core network?" -> GET /core-networks/{coreNetworkId}/core-network-policy
- "How do I trace a route between two transit gateways?" -> POST /global-networks/{globalNetworkId}/route-analyses
- "How do I connect an on-prem site via VPN?" -> POST /site-to-site-vpn-attachments
- "What are all the attachments on my core network?" -> GET /attachments
- "How do I remove a device from my global network?" -> DELETE /global-networks/{globalNetworkId}/devices/{deviceId}
- "How do I check the status of a route analysis?" -> GET /global-networks/{globalNetworkId}/route-analyses/{routeAnalysisId}
- "How do I update the subnets on a VPC attachment?" -> PATCH /vpc-attachments/{attachmentId}
- "How do I roll back a core network policy?" -> POST /core-networks/{coreNetworkId}/core-network-policy-versions/{policyVersionId}/restore
- "What resources exist in my global network by region?" -> GET /global-networks/{globalNetworkId}/network-resources
- "How do I enable AWS Organizations integration?" -> POST /organizations/service-access
- "How do I tag a network resource?" -> POST /tags/{resourceArn}

## Response Tips

- **List endpoints** (devices, sites, links, attachments, peerings): Always paginated via `NextToken` -- loop until `NextToken` is absent or null. Use `maxResults` to control page size.
- **Create/Update endpoints**: Return the full resource object on success (200). Check the nested `State` field to confirm the resource reached the expected lifecycle state (e.g., `AVAILABLE`, `PENDING_ATTACHMENT_ACCEPTANCE`).
- **Attachment responses**: Deeply nested -- the actual attachment metadata is inside `{TypeAttachment}.Attachment`. Watch for `LastModificationErrors` array for async failure details.
- **Route analysis**: The `ForwardPath` and `ReturnPath` each contain a `CompletionStatus` with `ResultCode` and `ReasonCode` -- always inspect both before trusting the path.
- **Policy endpoints**: `PolicyDocument` is a JSON string inside the response, not a parsed object -- deserialize it separately. Check `PolicyErrors` array and `ChangeSetState` before assuming success.
- **Delete endpoints**: Return the deleted resource's final state (200). A successful HTTP response does not mean instant deletion -- poll `State` until it shows `DELETING` or the resource disappears from list calls.

## Anomaly Flags

- **Attachment stuck in non-terminal state**: Surface when any attachment `State` remains `PENDING_ATTACHMENT_ACCEPTANCE`, `CREATING`, or `UPDATING` for an extended period -- the caller likely needs to accept/reject or investigate errors.
- **LastModificationErrors populated**: Proactively warn whenever `LastModificationErrors` (attachments) or `LastModificationErrors` (connect peers) is non-empty, even on 200 responses -- these indicate async failures that succeeded at the API level but failed during provisioning.
- **PolicyErrors on core network policy**: After PUT/restore of a policy, always check `PolicyErrors` array. A 200 with policy errors means the policy was accepted but contains validation problems that will block execution.
- **ChangeSetState is FAILED_GENERATION or EXECUTION_FAILED**: Flag immediately -- the core network policy change did not apply. The user must fix the policy document or restore a previous version.
- **Route analysis CompletionStatus with non-CONNECTED ResultCode**: When `ResultCode` is `NOT_CONNECTED` or `ROUTE_NOT_FOUND`, surface the `ReasonCode` and `ReasonContext` map -- these contain the specific hop or segment that broke the path.
- **TransitGatewayRegistration state degraded**: If `State.Code` is `FAILED` or `DELETED`, flag it -- the transit gateway is no longer usable in the global network and associations will fail silently.
- **Organizations SLRDeploymentStatus not SUCCEEDED**: If `SLRDeploymentStatus` is `NOT_STARTED` or `IN_PROGRESS` after enabling service access, warn that cross-account features won't work until the service-linked role finishes deploying.
- **Proposed segment/function group changes present**: When `ProposedSegmentChange` or `ProposedNetworkFunctionGroupChange` is non-null on an attachment, the attachment is pending a policy-driven reassignment -- surface this so the user doesn't assume current segment placement is final.

## Playbook

### 1. Build a Hub-and-Spoke Network from Scratch

1. Create a global network: `POST /global-networks` with a description.
2. Create a core network: `POST /core-networks` with the `GlobalNetworkId` and a `PolicyDocument` defining segments and edge locations.
3. Wait for core network `State` to be `AVAILABLE`.
4. Attach VPCs as spokes: `POST /vpc-attachments` for each VPC, providing `CoreNetworkId`, `VpcArn`, and `SubnetArns`.
5. Accept each attachment: `POST /attachments/{attachmentId}/accept`.
6. Verify attachments reach `AVAILABLE` state via `GET /attachments?coreNetworkId=...`.

### 2. Connect an On-Premises Site via Site-to-Site VPN

1. Create a site in your global network: `POST /global-networks/{id}/sites` with location details.
2. Create a device representing the on-prem equipment: `POST /global-networks/{id}/devices` with `SiteId`.
3. Register your transit gateway: `POST /global-networks/{id}/transit-gateway-registrations`.
4. Create the VPN attachment: `POST /site-to-site-vpn-attachments` with `CoreNetworkId` and `VpnConnectionArn`.
5. Accept the attachment: `POST /attachments/{attachmentId}/accept`.
6. Associate the customer gateway with the device: `POST /global-networks/{id}/customer-gateway-associations`.

### 3. Update a Core Network Policy with Rollback Safety

1. List existing policy versions: `GET /core-networks/{id}/core-network-policy-versions` -- note the current `LIVE` version ID.
2. Submit the new policy: `POST /core-networks/{id}/core-network-policy` with updated `PolicyDocument` and `LatestVersionId` for optimistic locking.
3. Check the response `PolicyErrors` array -- if non-empty, fix and resubmit.
4. Review the change set: `GET /core-networks/{id}/core-network-change-sets/{versionId}`.
5. Execute the change set: `POST /core-networks/{id}/core-network-change-sets/{versionId}/execute`.
6. If something goes wrong, restore the previous version: `POST /core-networks/{id}/core-network-policy-versions/{previousVersionId}/restore`, then execute that change set.

### 4. Diagnose Connectivity Issues with Route Analysis

1. Start a route analysis: `POST /global-networks/{id}/route-analyses` with `Source` and `Destination` transit gateway details. Set `IncludeReturnPath: true` for full round-trip analysis.
2. Poll the result: `GET /global-networks/{id}/route-analyses/{analysisId}` until `Status` is `COMPLETED`.
3. Inspect `ForwardPath.CompletionStatus.ResultCode` -- if not `CONNECTED`, read `ReasonCode` and `ReasonContext` for the failing hop.
4. Check `ReturnPath` separately -- asymmetric routing issues only show up here.
5. Cross-reference broken segments with `GET /global-networks/{id}/network-routes` using the relevant route table identifier to verify route table entries.

### 5. Set Up Transit Gateway Peering Across Regions

1. Ensure both regions have edge locations defined in your core network policy.
2. Create the transit gateway peering: `POST /transit-gateway-peerings` with `CoreNetworkId` and `TransitGatewayArn`.
3. Wait for the peering `State` to become `AVAILABLE` via `GET /transit-gateway-peerings/{peeringId}`.
4. Attach the transit gateway route table: `POST /transit-gateway-route-table-attachments` with the `PeeringId` and `TransitGatewayRouteTableArn`.
5. Accept the route table attachment: `POST /attachments/{attachmentId}/accept`.
6. Verify cross-region routing with a route analysis between the two transit gateways.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
