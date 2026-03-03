---
name: aws-network-firewall
description: "AWS Network Firewall API skill. Use when working with AWS Network Firewall for root. Covers 36 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Network Firewall
API version: 2020-11-12

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

36 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Associates a FirewallPolicy to a Firewall.  A firewall policy defines how to monitor and manage your VPC network traffic, using a collection of inspection rule groups and other settings. Each firewall requires one firewall policy association, and you can use the same firewall policy for multiple firewalls. |
| POST | / | Associates the specified subnets in the Amazon VPC to the firewall. You can specify one subnet for each of the Availability Zones that the VPC spans.  This request creates an Network Firewall firewall endpoint in each of the subnets. To enable the firewall's protections, you must also modify the VPC's route tables for each subnet's Availability Zone, to redirect the traffic that's coming into and going out of the zone through the firewall endpoint. |
| POST | / | Creates an Network Firewall Firewall and accompanying FirewallStatus for a VPC.  The firewall defines the configuration settings for an Network Firewall firewall. The settings that you can define at creation include the firewall policy, the subnets in your VPC to use for the firewall endpoints, and any tags that are attached to the firewall Amazon Web Services resource.  After you create a firewall, you can provide additional settings, like the logging configuration.  To update the settings for a firewall, you use the operations that apply to the settings themselves, for example UpdateLoggingConfiguration, AssociateSubnets, and UpdateFirewallDeleteProtection.  To manage a firewall's tags, use the standard Amazon Web Services resource tagging operations, ListTagsForResource, TagResource, and UntagResource. To retrieve information about firewalls, use ListFirewalls and DescribeFirewall. |
| POST | / | Creates the firewall policy for the firewall according to the specifications.  An Network Firewall firewall policy defines the behavior of a firewall, in a collection of stateless and stateful rule groups and other settings. You can use one firewall policy for multiple firewalls. |
| POST | / | Creates the specified stateless or stateful rule group, which includes the rules for network traffic inspection, a capacity setting, and tags.  You provide your rule group specification in your request using either RuleGroup or Rules. |
| POST | / | Creates an Network Firewall TLS inspection configuration. Network Firewall uses TLS inspection configurations to decrypt your firewall's inbound and outbound SSL/TLS traffic. After decryption, Network Firewall inspects the traffic according to your firewall policy's stateful rules, and then re-encrypts it before sending it to its destination. You can enable inspection of your firewall's inbound traffic, outbound traffic, or both. To use TLS inspection with your firewall, you must first import or provision certificates using ACM, create a TLS inspection configuration, add that configuration to a new firewall policy, and then associate that policy with your firewall. To update the settings for a TLS inspection configuration, use UpdateTLSInspectionConfiguration. To manage a TLS inspection configuration's tags, use the standard Amazon Web Services resource tagging operations, ListTagsForResource, TagResource, and UntagResource. To retrieve information about TLS inspection configurations, use ListTLSInspectionConfigurations and DescribeTLSInspectionConfiguration.  For more information about TLS inspection configurations, see Inspecting SSL/TLS traffic with TLS inspection configurations in the Network Firewall Developer Guide. |
| POST | / | Deletes the specified Firewall and its FirewallStatus. This operation requires the firewall's DeleteProtection flag to be FALSE. You can't revert this operation.  You can check whether a firewall is in use by reviewing the route tables for the Availability Zones where you have firewall subnet mappings. Retrieve the subnet mappings by calling DescribeFirewall. You define and update the route tables through Amazon VPC. As needed, update the route tables for the zones to remove the firewall endpoints. When the route tables no longer use the firewall endpoints, you can remove the firewall safely. To delete a firewall, remove the delete protection if you need to using UpdateFirewallDeleteProtection, then delete the firewall by calling DeleteFirewall. |
| POST | / | Deletes the specified FirewallPolicy. |
| POST | / | Deletes a resource policy that you created in a PutResourcePolicy request. |
| POST | / | Deletes the specified RuleGroup. |
| POST | / | Deletes the specified TLSInspectionConfiguration. |
| POST | / | Returns the data objects for the specified firewall. |
| POST | / | Returns the data objects for the specified firewall policy. |
| POST | / | Returns the logging configuration for the specified firewall. |
| POST | / | Retrieves a resource policy that you created in a PutResourcePolicy request. |
| POST | / | Returns the data objects for the specified rule group. |
| POST | / | High-level information about a rule group, returned by operations like create and describe. You can use the information provided in the metadata to retrieve and manage a rule group. You can retrieve all objects for a rule group by calling DescribeRuleGroup. |
| POST | / | Returns the data objects for the specified TLS inspection configuration. |
| POST | / | Removes the specified subnet associations from the firewall. This removes the firewall endpoints from the subnets and removes any network filtering protections that the endpoints were providing. |
| POST | / | Retrieves the metadata for the firewall policies that you have defined. Depending on your setting for max results and the number of firewall policies, a single call might not return the full list. |
| POST | / | Retrieves the metadata for the firewalls that you have defined. If you provide VPC identifiers in your request, this returns only the firewalls for those VPCs. Depending on your setting for max results and the number of firewalls, a single call might not return the full list. |
| POST | / | Retrieves the metadata for the rule groups that you have defined. Depending on your setting for max results and the number of rule groups, a single call might not return the full list. |
| POST | / | Retrieves the metadata for the TLS inspection configurations that you have defined. Depending on your setting for max results and the number of TLS inspection configurations, a single call might not return the full list. |
| POST | / | Retrieves the tags associated with the specified resource. Tags are key:value pairs that you can use to categorize and manage your resources, for purposes like billing. For example, you might set the tag key to "customer" and the value to the customer name or ID. You can specify one or more tags to add to each Amazon Web Services resource, up to 50 tags for a resource. You can tag the Amazon Web Services resources that you manage through Network Firewall: firewalls, firewall policies, and rule groups. |
| POST | / | Creates or updates an IAM policy for your rule group or firewall policy. Use this to share rule groups and firewall policies between accounts. This operation works in conjunction with the Amazon Web Services Resource Access Manager (RAM) service to manage resource sharing for Network Firewall.  Use this operation to create or update a resource policy for your rule group or firewall policy. In the policy, you specify the accounts that you want to share the resource with and the operations that you want the accounts to be able to perform.  When you add an account in the resource policy, you then run the following Resource Access Manager (RAM) operations to access and accept the shared rule group or firewall policy.     GetResourceShareInvitations - Returns the Amazon Resource Names (ARNs) of the resource share invitations.     AcceptResourceShareInvitation - Accepts the share invitation for a specified resource share.    For additional information about resource sharing using RAM, see Resource Access Manager User Guide. |
| POST | / | Adds the specified tags to the specified resource. Tags are key:value pairs that you can use to categorize and manage your resources, for purposes like billing. For example, you might set the tag key to "customer" and the value to the customer name or ID. You can specify one or more tags to add to each Amazon Web Services resource, up to 50 tags for a resource. You can tag the Amazon Web Services resources that you manage through Network Firewall: firewalls, firewall policies, and rule groups. |
| POST | / | Removes the tags with the specified keys from the specified resource. Tags are key:value pairs that you can use to categorize and manage your resources, for purposes like billing. For example, you might set the tag key to "customer" and the value to the customer name or ID. You can specify one or more tags to add to each Amazon Web Services resource, up to 50 tags for a resource. You can manage tags for the Amazon Web Services resources that you manage through Network Firewall: firewalls, firewall policies, and rule groups. |
| POST | / | Modifies the flag, DeleteProtection, which indicates whether it is possible to delete the firewall. If the flag is set to TRUE, the firewall is protected against deletion. This setting helps protect against accidentally deleting a firewall that's in use. |
| POST | / | Modifies the description for the specified firewall. Use the description to help you identify the firewall when you're working with it. |
| POST | / | A complex type that contains settings for encryption of your firewall resources. |
| POST | / | Updates the properties of the specified firewall policy. |
| POST | / | Modifies the flag, ChangeProtection, which indicates whether it is possible to change the firewall. If the flag is set to TRUE, the firewall is protected from changes. This setting helps protect against accidentally changing a firewall that's in use. |
| POST | / | Sets the logging configuration for the specified firewall.  To change the logging configuration, retrieve the LoggingConfiguration by calling DescribeLoggingConfiguration, then change it and provide the modified object to this update call. You must change the logging configuration one LogDestinationConfig at a time inside the retrieved LoggingConfiguration object.  You can perform only one of the following actions in any call to UpdateLoggingConfiguration:    Create a new log destination object by adding a single LogDestinationConfig array element to LogDestinationConfigs.   Delete a log destination object by removing a single LogDestinationConfig array element from LogDestinationConfigs.   Change the LogDestination setting in a single LogDestinationConfig array element.   You can't change the LogDestinationType or LogType in a LogDestinationConfig. To change these settings, delete the existing LogDestinationConfig object and create a new one, using two separate calls to this update operation. |
| POST | / | Updates the rule settings for the specified rule group. You use a rule group by reference in one or more firewall policies. When you modify a rule group, you modify all firewall policies that use the rule group.  To update a rule group, first call DescribeRuleGroup to retrieve the current RuleGroup object, update the object as needed, and then provide the updated object to this call. |
| POST | / |  |
| POST | / | Updates the TLS inspection configuration settings for the specified TLS inspection configuration. You use a TLS inspection configuration by referencing it in one or more firewall policies. When you modify a TLS inspection configuration, you modify all firewall policies that use the TLS inspection configuration.  To update a TLS inspection configuration, first call DescribeTLSInspectionConfiguration to retrieve the current TLSInspectionConfiguration object, update the object as needed, and then provide the updated object to this call. |

## Enhanced Skill Content
## Question Mapping

- "How do I create a new network firewall in my VPC?" -> POST / (CreateFirewall)
- "How do I list all my firewalls or filter by VPC?" -> POST / (ListFirewalls with optional VpcIds filter)
- "What is the current status and configuration of my firewall?" -> POST / (DescribeFirewall)
- "How do I create a firewall policy with stateful and stateless rules?" -> POST / (CreateFirewallPolicy)
- "How do I create a rule group for domain filtering or IPS?" -> POST / (CreateRuleGroup)
- "How do I attach a firewall policy to an existing firewall?" -> POST / (AssociateFirewallPolicy)
- "How do I add or remove subnets from my firewall?" -> POST / (AssociateSubnets or DisassociateSubnets)
- "How do I enable TLS inspection on my firewall?" -> POST / (CreateTLSInspectionConfiguration, then reference its ARN in the firewall policy)
- "How do I set up logging for my firewall to S3 or CloudWatch?" -> POST / (UpdateLoggingConfiguration)
- "How do I protect my firewall from accidental deletion?" -> POST / (UpdateFirewallDeleteProtection with DeleteProtection: true)
- "How do I check how much rule capacity I have left?" -> POST / (DescribeFirewallPolicy -- check ConsumedStatelessRuleCapacity / ConsumedStatefulRuleCapacity)
- "How do I share a rule group or firewall policy across accounts?" -> POST / (PutResourcePolicy)
- "How do I find all AWS-managed rule groups available?" -> POST / (ListRuleGroups with Scope: "MANAGED")
- "How do I validate a rule group change without applying it?" -> POST / (UpdateRuleGroup or CreateRuleGroup with DryRun: true)
- "How do I check CIDR capacity usage on my firewall?" -> POST / (DescribeFirewall -- inspect FirewallStatus.CapacityUsageSummary.CIDRs)

## Response Tips

- **List endpoints** (ListFirewalls, ListFirewallPolicies, ListRuleGroups, ListTLSInspectionConfigurations, ListTagsForResource): Paginated via `NextToken`/`MaxResults`. Keep calling with the returned `NextToken` until it is null. MaxResults caps per-page count, not total.
- **Describe endpoints** (DescribeFirewall, DescribeFirewallPolicy, DescribeRuleGroup, DescribeTLSInspectionConfiguration): Always return an `UpdateToken` -- you must pass this token on subsequent update calls for optimistic concurrency control.
- **Create endpoints**: Return an `UpdateToken` and a response object with generated IDs (FirewallId, RuleGroupId, etc.) and an ARN -- capture these for downstream operations.
- **Update endpoints**: Require `UpdateToken` from the most recent Describe or prior Update; a stale token causes a conflict error. Response includes a fresh `UpdateToken`.
- **Delete endpoints**: Return the deleted resource's final state. If the resource has `NumberOfAssociations > 0`, the delete will fail -- disassociate first.
- **Tag endpoints** (TagResource, UntagResource): Return no body on success. Use ListTagsForResource to verify.
- **Resource policy endpoints** (PutResourcePolicy, DescribeResourcePolicy, DeleteResourcePolicy): Policy is a JSON string, not an object. Parse it separately.

## Anomaly Flags

- **Stale UpdateToken**: If an update call fails with a conflict/validation error, the UpdateToken is outdated. Re-describe the resource and retry with the fresh token.
- **ConfigurationSyncStateSummary != "IN_SYNC"**: After changes, the firewall's sync state may show "PENDING" or "CAPACITY_CONSTRAINED". Surface this -- traffic rules are not yet active across all availability zones.
- **FirewallStatus.Status != "READY"**: Firewall is provisioning, deleting, or in an error state. Operations may be rejected or have no effect until status returns to READY.
- **Capacity approaching limits**: Compare `ConsumedStatelessRuleCapacity` / `ConsumedStatefulRuleCapacity` against the policy's allocated capacity. Alert when utilization exceeds 80%.
- **CIDR capacity exhaustion**: Check `CapacityUsageSummary.CIDRs.AvailableCIDRCount` -- if zero or near-zero, IP set references will fail to resolve new entries.
- **TLS certificate status != "ACTIVE"**: Surface `Certificates[].Status` and `CertificateAuthority.Status` values that are not active, along with their `StatusMessage`.
- **RuleGroupStatus == "DELETING"**: A rule group stuck in DELETING state indicates a dependency issue. Check `NumberOfAssociations`.
- **AnalysisResults present**: When `AnalyzeRuleGroup: true` is used, non-empty `AnalysisResults` in the response signals rule conflicts or redundancies -- surface these warnings.
- **DryRun rejected**: If a CreateRuleGroup or UpdateFirewallPolicy with `DryRun: true` returns errors, the planned change would exceed capacity or violate constraints.

## Playbook

### 1. Deploy a New Firewall End-to-End

1. **Create a rule group**: POST / (CreateRuleGroup) with your Suricata rules or domain list. Note the returned `RuleGroupArn`.
2. **Create a firewall policy**: POST / (CreateFirewallPolicy) referencing the rule group ARN in `StatefulRuleGroupReferences` or `StatelessRuleGroupReferences`. Note the returned `FirewallPolicyArn`.
3. **Create the firewall**: POST / (CreateFirewall) with `FirewallName`, `VpcId`, `SubnetMappings` (one per AZ), and the `FirewallPolicyArn`.
4. **Wait for READY**: POST / (DescribeFirewall) repeatedly until `FirewallStatus.Status` is `READY` and `ConfigurationSyncStateSummary` is `IN_SYNC`.
5. **Configure logging**: POST / (UpdateLoggingConfiguration) to send ALERT and FLOW logs to S3, CloudWatch, or Kinesis.
6. **Update VPC route tables**: Point traffic through the firewall endpoint IDs found in `FirewallStatus.SyncStates[az].Attachment.EndpointId`.

### 2. Update a Rule Group Safely

1. **Describe current state**: POST / (DescribeRuleGroup) to get the current `UpdateToken` and rule definitions.
2. **Dry run the change**: POST / (UpdateRuleGroup) with `DryRun: true`, your modified `RuleGroup` or `Rules` string, and the `UpdateToken`. Check for capacity or validation errors.
3. **Apply the update**: POST / (UpdateRuleGroup) with `DryRun: false` (or omit it) and the same `UpdateToken`.
4. **Verify sync**: POST / (DescribeFirewall) for each associated firewall. Confirm `ConfigurationSyncStateSummary` returns to `IN_SYNC`.
5. **Review analysis**: If `AnalyzeRuleGroup: true` was set, inspect `AnalysisResults` for rule conflicts.

### 3. Enable TLS Inspection

1. **Provision certificates**: Ensure your ACM certificates (server cert + CA cert) are in the same region.
2. **Create TLS config**: POST / (CreateTLSInspectionConfiguration) with `ServerCertificateConfigurations` referencing your ACM certificate ARNs.
3. **Update firewall policy**: POST / (DescribeFirewallPolicy) to get the current `UpdateToken`, then POST / (UpdateFirewallPolicy) adding `TLSInspectionConfigurationArn` to the policy.
4. **Verify certificates**: POST / (DescribeTLSInspectionConfiguration) and confirm all `Certificates[].Status` values are `ACTIVE`.

### 4. Cross-Account Rule Group Sharing

1. **Create a resource policy**: POST / (PutResourcePolicy) on the rule group ARN with a JSON policy granting `network-firewall:ListRuleGroups` and `network-firewall:DescribeRuleGroup` to the target account principals.
2. **Verify the policy**: POST / (DescribeResourcePolicy) to confirm the policy is attached.
3. **Reference from other account**: In the consuming account, reference the shared rule group ARN in a firewall policy's `StatefulRuleGroupReferences` using `SourceMetadata.SourceArn`.
4. **To revoke access**: POST / (DeleteResourcePolicy) on the source account's rule group ARN.

### 5. Safely Decommission a Firewall

1. **Check associations**: POST / (DescribeFirewall) and note `FirewallPolicyArn`, subnet mappings, and any logging config.
2. **Update route tables**: Remove or redirect routes that point to the firewall endpoints before deleting.
3. **Disable protections**: POST / (UpdateFirewallDeleteProtection) with `DeleteProtection: false`. Also disable `SubnetChangeProtection` and `FirewallPolicyChangeProtection` if enabled.
4. **Delete the firewall**: POST / (DeleteFirewall) using the firewall name or ARN.
5. **Clean up orphaned resources**: Delete unused firewall policies (POST / DeleteFirewallPolicy), rule groups (POST / DeleteRuleGroup), and TLS configs (POST / DeleteTLSInspectionConfiguration) after confirming `NumberOfAssociations` is 0 for each.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
