---
name: amazon-worklink
description: "Amazon WorkLink API skill. Use when working with Amazon WorkLink for associateDomain, associateWebsiteAuthorizationProvider, associateWebsiteCertificateAuthority. Covers 33 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon WorkLink
API version: 2018-09-25

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /tags/{ResourceArn} -- verify access
3. POST /associateDomain -- create first associateDomain

## Endpoints

33 endpoints across 31 groups. See references/api-spec.lap for full details.

### associateDomain
| Method | Path | Description |
|--------|------|-------------|
| POST | /associateDomain | Specifies a domain to be associated to Amazon WorkLink. |

### associateWebsiteAuthorizationProvider
| Method | Path | Description |
|--------|------|-------------|
| POST | /associateWebsiteAuthorizationProvider | Associates a website authorization provider with a specified fleet. This is used to authorize users against associated websites in the company network. |

### associateWebsiteCertificateAuthority
| Method | Path | Description |
|--------|------|-------------|
| POST | /associateWebsiteCertificateAuthority | Imports the root certificate of a certificate authority (CA) used to obtain TLS certificates used by associated websites within the company network. |

### createFleet
| Method | Path | Description |
|--------|------|-------------|
| POST | /createFleet | Creates a fleet. A fleet consists of resources and the configuration that delivers associated websites to authorized users who download and set up the Amazon WorkLink app. |

### deleteFleet
| Method | Path | Description |
|--------|------|-------------|
| POST | /deleteFleet | Deletes a fleet. Prevents users from accessing previously associated websites. |

### describeAuditStreamConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeAuditStreamConfiguration | Describes the configuration for delivering audit streams to the customer account. |

### describeCompanyNetworkConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeCompanyNetworkConfiguration | Describes the networking configuration to access the internal websites associated with the specified fleet. |

### describeDevice
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeDevice | Provides information about a user's device. |

### describeDevicePolicyConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeDevicePolicyConfiguration | Describes the device policy configuration for the specified fleet. |

### describeDomain
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeDomain | Provides information about the domain. |

### describeFleetMetadata
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeFleetMetadata | Provides basic information for the specified fleet, excluding identity provider, networking, and device configuration details. |

### describeIdentityProviderConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeIdentityProviderConfiguration | Describes the identity provider configuration of the specified fleet. |

### describeWebsiteCertificateAuthority
| Method | Path | Description |
|--------|------|-------------|
| POST | /describeWebsiteCertificateAuthority | Provides information about the certificate authority. |

### disassociateDomain
| Method | Path | Description |
|--------|------|-------------|
| POST | /disassociateDomain | Disassociates a domain from Amazon WorkLink. End users lose the ability to access the domain with Amazon WorkLink. |

### disassociateWebsiteAuthorizationProvider
| Method | Path | Description |
|--------|------|-------------|
| POST | /disassociateWebsiteAuthorizationProvider | Disassociates a website authorization provider from a specified fleet. After the disassociation, users can't load any associated websites that require this authorization provider. |

### disassociateWebsiteCertificateAuthority
| Method | Path | Description |
|--------|------|-------------|
| POST | /disassociateWebsiteCertificateAuthority | Removes a certificate authority (CA). |

### listDevices
| Method | Path | Description |
|--------|------|-------------|
| POST | /listDevices | Retrieves a list of devices registered with the specified fleet. |

### listDomains
| Method | Path | Description |
|--------|------|-------------|
| POST | /listDomains | Retrieves a list of domains associated to a specified fleet. |

### listFleets
| Method | Path | Description |
|--------|------|-------------|
| POST | /listFleets | Retrieves a list of fleets for the current account and Region. |

### tags
| Method | Path | Description |
|--------|------|-------------|
| GET | /tags/{ResourceArn} | Retrieves a list of tags for the specified resource. |
| POST | /tags/{ResourceArn} | Adds or overwrites one or more tags for the specified resource, such as a fleet. Each tag consists of a key and an optional value. If a resource already has a tag with the same key, this operation updates its value. |
| DELETE | /tags/{ResourceArn} | Removes one or more tags from the specified resource. |

### listWebsiteAuthorizationProviders
| Method | Path | Description |
|--------|------|-------------|
| POST | /listWebsiteAuthorizationProviders | Retrieves a list of website authorization providers associated with a specified fleet. |

### listWebsiteCertificateAuthorities
| Method | Path | Description |
|--------|------|-------------|
| POST | /listWebsiteCertificateAuthorities | Retrieves a list of certificate authorities added for the current account and Region. |

### restoreDomainAccess
| Method | Path | Description |
|--------|------|-------------|
| POST | /restoreDomainAccess | Moves a domain to ACTIVE status if it was in the INACTIVE status. |

### revokeDomainAccess
| Method | Path | Description |
|--------|------|-------------|
| POST | /revokeDomainAccess | Moves a domain to INACTIVE status if it was in the ACTIVE status. |

### signOutUser
| Method | Path | Description |
|--------|------|-------------|
| POST | /signOutUser | Signs the user out from all of their devices. The user can sign in again if they have valid credentials. |

### updateAuditStreamConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateAuditStreamConfiguration | Updates the audit stream configuration for the fleet. |

### updateCompanyNetworkConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateCompanyNetworkConfiguration | Updates the company network configuration for the fleet. |

### updateDevicePolicyConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateDevicePolicyConfiguration | Updates the device policy configuration for the fleet. |

### updateDomainMetadata
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateDomainMetadata | Updates domain metadata, such as DisplayName. |

### UpdateFleetMetadata
| Method | Path | Description |
|--------|------|-------------|
| POST | /UpdateFleetMetadata | Updates fleet metadata, such as DisplayName. |

### updateIdentityProviderConfiguration
| Method | Path | Description |
|--------|------|-------------|
| POST | /updateIdentityProviderConfiguration | Updates the identity provider configuration for the fleet. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new fleet?" -> POST /createFleet
- "What fleets do I have?" -> POST /listFleets
- "How do I delete a fleet?" -> POST /deleteFleet
- "What are the details of my fleet?" -> POST /describeFleetMetadata
- "How do I add a domain to my fleet?" -> POST /associateDomain
- "What domains are associated with my fleet?" -> POST /listDomains
- "How do I remove a domain from my fleet?" -> POST /disassociateDomain
- "What devices are connected to my fleet?" -> POST /listDevices
- "How do I get details about a specific device?" -> POST /describeDevice
- "How do I force sign out a user?" -> POST /signOutUser
- "How do I set up a SAML identity provider for my fleet?" -> POST /updateIdentityProviderConfiguration
- "How do I configure the company VPN/network for my fleet?" -> POST /updateCompanyNetworkConfiguration
- "How do I add a certificate authority for internal sites?" -> POST /associateWebsiteCertificateAuthority
- "How do I tag or untag a fleet resource?" -> POST /tags/{ResourceArn} (add), DELETE /tags/{ResourceArn} (remove)
- "How do I revoke or restore domain access?" -> POST /revokeDomainAccess (revoke), POST /restoreDomainAccess (restore)

## Response Tips

- **List endpoints** (listFleets, listDevices, listDomains, listWebsiteAuthorizationProviders, listWebsiteCertificateAuthorities): All return a `NextToken` field; pass it back as `NextToken` in subsequent requests to paginate. Array field may be absent or empty when no results exist.
- **Describe endpoints** (describeDevice, describeFleetMetadata, describeDomain, etc.): All fields are nullable (marked `?`); check for missing values rather than assuming presence. Timestamp fields are ISO 8601 strings.
- **Create/Associate endpoints** (createFleet, associateWebsiteCertificateAuthority, associateWebsiteAuthorizationProvider): Return a single identifier (ARN or ID) on success, which may be null -- always verify the returned ID before storing.
- **Mutate endpoints** (delete, disassociate, update, revoke, restore, signOutUser): Return empty 200 responses on success; non-200 status codes indicate failure with an error message body.
- **Tags** (GET/POST/DELETE /tags/{ResourceArn}): GET returns a `Tags` map that may be null or empty; POST expects a `Tags` map in the body; DELETE expects a `tagKeys` array as a query parameter.

## Anomaly Flags

- **Deprecated service**: Amazon WorkLink was deprecated by AWS. Surface a warning if a user attempts to create new resources, as the service may return errors or be fully decommissioned.
- **Fleet status changes**: When `describeFleetMetadata` returns a `FleetStatus` other than `ACTIVE` (e.g., `DELETING`, `FAILED_TO_CREATE`), proactively alert the user.
- **Domain status anomalies**: If `describeDomain` returns a `DomainStatus` of `FAILED_TO_ASSOCIATE`, `FAILED_TO_DISASSOCIATE`, or `INACTIVE`, flag it immediately.
- **Stale devices**: When `describeDevice` shows a `LastAccessedTime` older than 30 days, surface a suggestion to review or remove the device.
- **Pagination truncation**: If a list response includes `NextToken` but the caller did not request all pages, warn that results are incomplete.
- **Missing audit stream**: If `describeAuditStreamConfiguration` returns a null `AuditStreamArn`, flag that audit logging is not configured for the fleet.
- **Empty network configuration**: If `describeCompanyNetworkConfiguration` returns null VPC/subnet/security group IDs, alert that the company network is not set up.

## Playbook

### 1. Set Up a New Fleet with Domain and Identity Provider

1. Call `POST /createFleet` with `FleetName` and optional `DisplayName` and `Tags`. Save the returned `FleetArn`.
2. Call `POST /associateDomain` with the `FleetArn`, your `DomainName`, and `AcmCertificateArn`.
3. Call `POST /updateIdentityProviderConfiguration` with the `FleetArn`, `IdentityProviderType` (e.g., `SAML`), and `IdentityProviderSamlMetadata`.
4. Call `POST /describeFleetMetadata` to verify the fleet is `ACTIVE`.
5. Call `POST /describeDomain` to confirm the domain status is `ACTIVE`.

### 2. Audit and Manage Devices Across a Fleet

1. Call `POST /listFleets` to get all fleet ARNs (paginate with `NextToken` if needed).
2. For each fleet, call `POST /listDevices` with the `FleetArn` (paginate as needed).
3. For devices requiring investigation, call `POST /describeDevice` with `FleetArn` and `DeviceId`.
4. To force-remove a user session from a device, call `POST /signOutUser` with `FleetArn` and `Username`.

### 3. Configure Company Network Access

1. Call `POST /describeCompanyNetworkConfiguration` with `FleetArn` to check existing configuration.
2. Call `POST /updateCompanyNetworkConfiguration` with `FleetArn`, `VpcId`, `SubnetIds`, and `SecurityGroupIds`.
3. Call `POST /updateDevicePolicyConfiguration` with `FleetArn` and `DeviceCaCertificate` if client certificates are needed.
4. Call `POST /updateAuditStreamConfiguration` with `FleetArn` and `AuditStreamArn` to enable audit logging.

### 4. Manage Certificate Authorities and Authorization Providers

1. Call `POST /associateWebsiteCertificateAuthority` with `FleetArn` and `Certificate` PEM content. Save the returned `WebsiteCaId`.
2. Call `POST /associateWebsiteAuthorizationProvider` with `FleetArn` and `AuthorizationProviderType`. Save the returned `AuthorizationProviderId`.
3. To review, call `POST /listWebsiteCertificateAuthorities` and `POST /listWebsiteAuthorizationProviders`.
4. To remove, call `POST /disassociateWebsiteCertificateAuthority` with `WebsiteCaId` or `POST /disassociateWebsiteAuthorizationProvider` with `AuthorizationProviderId`.

### 5. Revoke and Restore Domain Access

1. Call `POST /listDomains` with `FleetArn` to see all associated domains and their statuses.
2. To block access, call `POST /revokeDomainAccess` with `FleetArn` and `DomainName`.
3. Call `POST /describeDomain` to confirm the domain status changed to `INACTIVE`.
4. To reinstate access, call `POST /restoreDomainAccess` with the same `FleetArn` and `DomainName`.
5. Call `POST /describeDomain` again to verify the domain is back to `ACTIVE`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
