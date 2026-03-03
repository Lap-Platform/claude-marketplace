---
name: aws-shield
description: "AWS Shield API skill. Use when working with AWS Shield for root. Covers 36 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Shield
API version: 2016-06-02

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
| POST | / | Authorizes the Shield Response Team (SRT) to access the specified Amazon S3 bucket containing log data such as Application Load Balancer access logs, CloudFront logs, or logs from third party sources. You can associate up to 10 Amazon S3 buckets with your subscription. To use the services of the SRT and make an AssociateDRTLogBucket request, you must be subscribed to the Business Support plan or the Enterprise Support plan. |
| POST | / | Authorizes the Shield Response Team (SRT) using the specified role, to access your Amazon Web Services account to assist with DDoS attack mitigation during potential attacks. This enables the SRT to inspect your WAF configuration and create or update WAF rules and web ACLs. You can associate only one RoleArn with your subscription. If you submit an AssociateDRTRole request for an account that already has an associated role, the new RoleArn will replace the existing RoleArn.  Prior to making the AssociateDRTRole request, you must attach the AWSShieldDRTAccessPolicy managed policy to the role that you'll specify in the request. You can access this policy in the IAM console at AWSShieldDRTAccessPolicy. For more information see Adding and removing IAM identity permissions. The role must also trust the service principal drt.shield.amazonaws.com. For more information, see IAM JSON policy elements: Principal. The SRT will have access only to your WAF and Shield resources. By submitting this request, you authorize the SRT to inspect your WAF and Shield configuration and create and update WAF rules and web ACLs on your behalf. The SRT takes these actions only if explicitly authorized by you. You must have the iam:PassRole permission to make an AssociateDRTRole request. For more information, see Granting a user permissions to pass a role to an Amazon Web Services service.  To use the services of the SRT and make an AssociateDRTRole request, you must be subscribed to the Business Support plan or the Enterprise Support plan. |
| POST | / | Adds health-based detection to the Shield Advanced protection for a resource. Shield Advanced health-based detection uses the health of your Amazon Web Services resource to improve responsiveness and accuracy in attack detection and response.  You define the health check in Route 53 and then associate it with your Shield Advanced protection. For more information, see Shield Advanced Health-Based Detection in the WAF Developer Guide. |
| POST | / | Initializes proactive engagement and sets the list of contacts for the Shield Response Team (SRT) to use. You must provide at least one phone number in the emergency contact list.  After you have initialized proactive engagement using this call, to disable or enable proactive engagement, use the calls DisableProactiveEngagement and EnableProactiveEngagement.   This call defines the list of email addresses and phone numbers that the SRT can use to contact you for escalations to the SRT and to initiate proactive customer support. The contacts that you provide in the request replace any contacts that were already defined. If you already have contacts defined and want to use them, retrieve the list using DescribeEmergencyContactSettings and then provide it to this call. |
| POST | / | Enables Shield Advanced for a specific Amazon Web Services resource. The resource can be an Amazon CloudFront distribution, Amazon Route 53 hosted zone, Global Accelerator standard accelerator, Elastic IP Address, Application Load Balancer, or a Classic Load Balancer. You can protect Amazon EC2 instances and Network Load Balancers by association with protected Amazon EC2 Elastic IP addresses. You can add protection to only a single resource with each CreateProtection request. You can add protection to multiple resources at once through the Shield Advanced console at https://console.aws.amazon.com/wafv2/shieldv2#/. For more information see Getting Started with Shield Advanced and Adding Shield Advanced protection to Amazon Web Services resources. |
| POST | / | Creates a grouping of protected resources so they can be handled as a collective. This resource grouping improves the accuracy of detection and reduces false positives. |
| POST | / | Activates Shield Advanced for an account.  For accounts that are members of an Organizations organization, Shield Advanced subscriptions are billed against the organization's payer account, regardless of whether the payer account itself is subscribed.   When you initially create a subscription, your subscription is set to be automatically renewed at the end of the existing subscription period. You can change this by submitting an UpdateSubscription request. |
| POST | / | Deletes an Shield Advanced Protection. |
| POST | / | Removes the specified protection group. |
| POST | / | Removes Shield Advanced from an account. Shield Advanced requires a 1-year subscription commitment. You cannot delete a subscription prior to the completion of that commitment. |
| POST | / | Describes the details of a DDoS attack. |
| POST | / | Provides information about the number and type of attacks Shield has detected in the last year for all resources that belong to your account, regardless of whether you've defined Shield protections for them. This operation is available to Shield customers as well as to Shield Advanced customers. The operation returns data for the time range of midnight UTC, one year ago, to midnight UTC, today. For example, if the current time is 2020-10-26 15:39:32 PDT, equal to 2020-10-26 22:39:32 UTC, then the time range for the attack data returned is from 2019-10-26 00:00:00 UTC to 2020-10-26 00:00:00 UTC.  The time range indicates the period covered by the attack statistics data items. |
| POST | / | Returns the current role and list of Amazon S3 log buckets used by the Shield Response Team (SRT) to access your Amazon Web Services account while assisting with attack mitigation. |
| POST | / | A list of email addresses and phone numbers that the Shield Response Team (SRT) can use to contact you if you have proactive engagement enabled, for escalations to the SRT and to initiate proactive customer support. |
| POST | / | Lists the details of a Protection object. |
| POST | / | Returns the specification for the specified protection group. |
| POST | / | Provides details about the Shield Advanced subscription for an account. |
| POST | / | Disable the Shield Advanced automatic application layer DDoS mitigation feature for the protected resource. This stops Shield Advanced from creating, verifying, and applying WAF rules for attacks that it detects for the resource. |
| POST | / | Removes authorization from the Shield Response Team (SRT) to notify contacts about escalations to the SRT and to initiate proactive customer support. |
| POST | / | Removes the Shield Response Team's (SRT) access to the specified Amazon S3 bucket containing the logs that you shared previously. |
| POST | / | Removes the Shield Response Team's (SRT) access to your Amazon Web Services account. |
| POST | / | Removes health-based detection from the Shield Advanced protection for a resource. Shield Advanced health-based detection uses the health of your Amazon Web Services resource to improve responsiveness and accuracy in attack detection and response.  You define the health check in Route 53 and then associate or disassociate it with your Shield Advanced protection. For more information, see Shield Advanced Health-Based Detection in the WAF Developer Guide. |
| POST | / | Enable the Shield Advanced automatic application layer DDoS mitigation for the protected resource.   This feature is available for Amazon CloudFront distributions and Application Load Balancers only.  This causes Shield Advanced to create, verify, and apply WAF rules for DDoS attacks that it detects for the resource. Shield Advanced applies the rules in a Shield rule group inside the web ACL that you've associated with the resource. For information about how automatic mitigation works and the requirements for using it, see Shield Advanced automatic application layer DDoS mitigation.  Don't use this action to make changes to automatic mitigation settings when it's already enabled for a resource. Instead, use UpdateApplicationLayerAutomaticResponse.  To use this feature, you must associate a web ACL with the protected resource. The web ACL must be created using the latest version of WAF (v2). You can associate the web ACL through the Shield Advanced console at https://console.aws.amazon.com/wafv2/shieldv2#/. For more information, see Getting Started with Shield Advanced. You can also associate the web ACL to the resource through the WAF console or the WAF API, but you must manage Shield Advanced automatic mitigation through Shield Advanced. For information about WAF, see WAF Developer Guide. |
| POST | / | Authorizes the Shield Response Team (SRT) to use email and phone to notify contacts about escalations to the SRT and to initiate proactive customer support. |
| POST | / | Returns the SubscriptionState, either Active or Inactive. |
| POST | / | Returns all ongoing DDoS attacks or all DDoS attacks during a specified time period. |
| POST | / | Retrieves ProtectionGroup objects for the account. You can retrieve all protection groups or you can provide filtering criteria and retrieve just the subset of protection groups that match the criteria. |
| POST | / | Retrieves Protection objects for the account. You can retrieve all protections or you can provide filtering criteria and retrieve just the subset of protections that match the criteria. |
| POST | / | Retrieves the resources that are included in the protection group. |
| POST | / | Gets information about Amazon Web Services tags for a specified Amazon Resource Name (ARN) in Shield. |
| POST | / | Adds or updates tags for a resource in Shield. |
| POST | / | Removes tags from a resource in Shield. |
| POST | / | Updates an existing Shield Advanced automatic application layer DDoS mitigation configuration for the specified resource. |
| POST | / | Updates the details of the list of email addresses and phone numbers that the Shield Response Team (SRT) can use to contact you if you have proactive engagement enabled, for escalations to the SRT and to initiate proactive customer support. |
| POST | / | Updates an existing protection group. A protection group is a grouping of protected resources so they can be handled as a collective. This resource grouping improves the accuracy of detection and reduces false positives. |
| POST | / | Updates the details of an existing subscription. Only enter values for parameters you want to change. Empty parameters are not updated.  For accounts that are members of an Organizations organization, Shield Advanced subscriptions are billed against the organization's payer account, regardless of whether the payer account itself is subscribed. |

## Enhanced Skill Content
## Question Mapping

- "How do I protect a new AWS resource with Shield Advanced?" -> POST / (CreateProtection: Name, ResourceArn)
- "How do I set up a protection group for multiple resources?" -> POST / (CreateProtectionGroup: ProtectionGroupId, Aggregation, Pattern)
- "What are the details of a specific DDoS attack?" -> POST / (DescribeAttack: AttackId)
- "What attacks have happened in a given time range?" -> POST / (ListAttacks: StartTime, EndTime, ResourceArns)
- "What protections are currently active on my account?" -> POST / (ListProtections: InclusionFilters, NextToken, MaxResults)
- "How do I associate a Route 53 health check with a protection?" -> POST / (AssociateHealthCheck: ProtectionId, HealthCheckArn)
- "What is my current Shield Advanced subscription status?" -> POST / (DescribeSubscription) or POST / (GetSubscriptionState)
- "How do I grant the DDoS Response Team access to my logs?" -> POST / (AssociateDRTLogBucket: LogBucket) + POST / (AssociateDRTRole: RoleArn)
- "How do I enable automatic application-layer DDoS mitigation?" -> POST / (EnableApplicationLayerAutomaticResponse: ResourceArn, Action)
- "Who are my emergency contacts for DDoS events?" -> POST / (DescribeEmergencyContactSettings)
- "How do I tag a Shield resource for cost tracking?" -> POST / (TagResource: ResourceARN, Tags)
- "What resources belong to a specific protection group?" -> POST / (ListResourcesInProtectionGroup: ProtectionGroupId)
- "How do I turn on proactive engagement with the DDoS Response Team?" -> POST / (EnableProactiveEngagement)
- "How do I remove a protection I no longer need?" -> POST / (DeleteProtection: ProtectionId)
- "What are the overall DDoS attack statistics for my account?" -> POST / (DescribeAttackStatistics)

## Response Tips

- **Describe/Get calls**: Return a single nested object (Attack, Protection, Subscription); always check for `null` -- the top-level field is optional (`?`) when the resource may not exist.
- **List calls**: All return `NextToken` for pagination -- keep calling with the returned token until it is absent or empty; respect `MaxResults` (default varies by endpoint).
- **Mutating calls** (Create/Update/Delete/Associate/Disassociate): Return empty 200 on success except `CreateProtection` which returns `ProtectionId`; treat any non-200 as a failure.
- **DescribeAttack**: The `AttackDetail` response nests deeply -- `SubResources`, `AttackCounters`, `AttackProperties`, and `Mitigations` are all optional arrays; iterate defensively.
- **DescribeSubscription**: Contains nested `SubscriptionLimits` with sub-objects for protection and group limits; parse two levels deep to extract quota information.
- **Timestamps**: All time fields use `str(timestamp)` format; convert before comparison or display.

## Anomaly Flags

- **Subscription not active**: If `GetSubscriptionState` returns anything other than `ACTIVE`, surface immediately -- protections may not be enforced.
- **ProactiveEngagementStatus is DISABLED or PENDING**: Warn that the DDoS Response Team cannot proactively reach out during attacks until engagement is fully enabled.
- **AutoRenew set to NO**: Flag that the Shield Advanced subscription will expire and not auto-renew, risking a gap in protection.
- **Empty HealthCheckIds on a Protection**: The protection exists but has no associated health check, meaning Shield cannot use health-based detection -- recommend associating one.
- **Protection or ProtectionGroup limits approaching**: Compare current counts from `ListProtections`/`ListProtectionGroups` against limits in `DescribeSubscription.SubscriptionLimits` and warn at 80%+ usage.
- **Attack with no Mitigations**: If `DescribeAttack` returns an attack where `Mitigations` is empty or null, flag it -- this may indicate an unmitigated or ongoing event.
- **ApplicationLayerAutomaticResponse status is DISABLED**: If a protection has this field with `Status: DISABLED`, surface as a recommendation to enable for Layer 7 coverage.
- **DRT access not configured**: If `DescribeDRTAccess` returns empty `RoleArn` and `LogBucketList`, warn that the DDoS Response Team cannot assist during incidents.

## Playbook

### 1. Onboard a New Resource to Shield Advanced

1. Ensure you have an active subscription: call `GetSubscriptionState` and verify `SubscriptionState` is `ACTIVE`. If not, call `CreateSubscription`.
2. Create a protection: call `CreateProtection` with `Name` and `ResourceArn` of the resource (ALB, CloudFront, EIP, etc.). Save the returned `ProtectionId`.
3. Associate a Route 53 health check: call `AssociateHealthCheck` with the `ProtectionId` and your `HealthCheckArn` for health-based detection.
4. Enable automatic L7 mitigation (if applicable): call `EnableApplicationLayerAutomaticResponse` with `ResourceArn` and `Action` set to `{Count: {}}` (observe mode) or `{Block: {}}`.
5. Tag the protection for tracking: call `TagResource` with the protection ARN and relevant tags.

### 2. Set Up DDoS Response Team (DRT) Access

1. Create an IAM role granting DRT access and note the `RoleArn`.
2. Call `AssociateDRTRole` with the `RoleArn` to authorize the team.
3. For each relevant S3 log bucket, call `AssociateDRTLogBucket` with the `LogBucket` name.
4. Set emergency contacts: call `AssociateProactiveEngagementDetails` (or `UpdateEmergencyContactSettings`) with your `EmergencyContactList`.
5. Enable proactive engagement: call `EnableProactiveEngagement` so the DRT can contact you during detected events.
6. Verify setup: call `DescribeDRTAccess` and confirm both `RoleArn` and `LogBucketList` are populated.

### 3. Investigate a DDoS Attack

1. List recent attacks: call `ListAttacks` with a `StartTime` and `EndTime` range. Paginate with `NextToken` if needed.
2. Identify the target: review `AttackSummaries` for the affected `ResourceArn` and note the `AttackId`.
3. Get full details: call `DescribeAttack` with the `AttackId`.
4. Analyze vectors: inspect `SubResources` and `AttackCounters` to understand the attack type and volume.
5. Review mitigations: check the `Mitigations` array to confirm Shield took action. If empty, escalate.
6. Check broader trends: call `DescribeAttackStatistics` to see if this is part of a pattern.

### 4. Organize Resources into Protection Groups

1. Decide on a grouping strategy: by resource type (`ResourceType`), by explicit list (`Members`), or all resources (`ALL`).
2. Create the group: call `CreateProtectionGroup` with `ProtectionGroupId`, `Aggregation` (SUM, MEAN, or MAX), and `Pattern` (ALL, ARBITRARY, or BY_RESOURCE_TYPE).
3. If using `ARBITRARY` pattern, provide the `Members` list of resource ARNs. If using `BY_RESOURCE_TYPE`, set `ResourceType`.
4. Verify membership: call `ListResourcesInProtectionGroup` with the group ID and confirm the expected resources appear.
5. To modify later: call `UpdateProtectionGroup` with the same required fields plus any changes.

### 5. Manage Subscription Lifecycle

1. Check current state: call `GetSubscriptionState` for a quick status, or `DescribeSubscription` for full details including limits and renewal.
2. Review quotas: parse `SubscriptionLimits.ProtectionLimits` and `ProtectionGroupLimits` to understand your ceilings.
3. Toggle auto-renew: call `UpdateSubscription` with `AutoRenew` set to `ENABLED` or `DISABLED`.
4. Audit usage: call `ListProtections` and `ListProtectionGroups` and compare counts against your subscription limits.
5. If decommissioning: remove all protections and groups first, then call `DeleteSubscription` (note: Shield Advanced has a 1-year commitment).


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
