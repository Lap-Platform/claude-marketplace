---
name: awsmarketplace-metering
description: "AWSMarketplace Metering API skill. Use when working with AWSMarketplace Metering for root. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# AWSMarketplace Metering
API version: 2016-01-14

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

4 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | BatchMeterUsage is called from a SaaS application listed on AWS Marketplace to post metering records for a set of customers. For identical requests, the API is idempotent; requests can be retried with the same records or a subset of the input records. Every request to BatchMeterUsage is for one product. If you need to meter usage for multiple products, you must make multiple calls to BatchMeterUsage. Usage records are expected to be submitted as quickly as possible after the event that is being recorded, and are not accepted more than 6 hours after the event.  BatchMeterUsage can process up to 25 UsageRecords at a time. A UsageRecord can optionally include multiple usage allocations, to provide customers with usage data split into buckets by tags that you define (or allow the customer to define).  BatchMeterUsage returns a list of UsageRecordResult objects, showing the result for each UsageRecord, as well as a list of UnprocessedRecords, indicating errors in the service side that you should retry.  BatchMeterUsage requests must be less than 1MB in size.  For an example of using BatchMeterUsage, see  BatchMeterUsage code example in the AWS Marketplace Seller Guide. |
| POST | / | API to emit metering records. For identical requests, the API is idempotent. It simply returns the metering record ID.  MeterUsage is authenticated on the buyer's AWS account using credentials from the EC2 instance, ECS task, or EKS pod.  MeterUsage can optionally include multiple usage allocations, to provide customers with usage data split into buckets by tags that you define (or allow the customer to define). Usage records are expected to be submitted as quickly as possible after the event that is being recorded, and are not accepted more than 6 hours after the event. |
| POST | / | Paid container software products sold through AWS Marketplace must integrate with the AWS Marketplace Metering Service and call the RegisterUsage operation for software entitlement and metering. Free and BYOL products for Amazon ECS or Amazon EKS aren't required to call RegisterUsage, but you may choose to do so if you would like to receive usage data in your seller reports. The sections below explain the behavior of RegisterUsage. RegisterUsage performs two primary functions: metering and entitlement.    Entitlement: RegisterUsage allows you to verify that the customer running your paid software is subscribed to your product on AWS Marketplace, enabling you to guard against unauthorized use. Your container image that integrates with RegisterUsage is only required to guard against unauthorized use at container startup, as such a CustomerNotSubscribedException or PlatformNotSupportedException will only be thrown on the initial call to RegisterUsage. Subsequent calls from the same Amazon ECS task instance (e.g. task-id) or Amazon EKS pod will not throw a CustomerNotSubscribedException, even if the customer unsubscribes while the Amazon ECS task or Amazon EKS pod is still running.    Metering: RegisterUsage meters software use per ECS task, per hour, or per pod for Amazon EKS with usage prorated to the second. A minimum of 1 minute of usage applies to tasks that are short lived. For example, if a customer has a 10 node Amazon ECS or Amazon EKS cluster and a service configured as a Daemon Set, then Amazon ECS or Amazon EKS will launch a task on all 10 cluster nodes and the customer will be charged: (10 * hourly_rate). Metering for software use is automatically handled by the AWS Marketplace Metering Control Plane -- your software is not required to perform any metering specific actions, other than call RegisterUsage once for metering of software use to commence. The AWS Marketplace Metering Control Plane will also continue to bill customers for running ECS tasks and Amazon EKS pods, regardless of the customers subscription state, removing the need for your software to perform entitlement checks at runtime. |
| POST | / | ResolveCustomer is called by a SaaS application during the registration process. When a buyer visits your website during the registration process, the buyer submits a registration token through their browser. The registration token is resolved through this API to obtain a CustomerIdentifier along with the CustomerAWSAccountId and ProductCode.  The API needs to called from the seller account id used to publish the SaaS application to successfully resolve the token. For an example of using ResolveCustomer, see  ResolveCustomer code example in the AWS Marketplace Seller Guide. |

## Enhanced Skill Content
## Question Mapping

- "How do I submit usage records in bulk?" -> POST / (BatchMeterUsage)
- "How do I report a single metering event?" -> POST / (MeterUsage)
- "Can I test metering without actually reporting usage?" -> POST / (MeterUsage with DryRun: true)
- "How do I resolve a buyer's registration token to get their customer ID?" -> POST / (ResolveCustomer)
- "How do I get the public key for verifying entitlements?" -> POST / (RegisterUsage)
- "What happens to records that fail in a batch submission?" -> POST / (BatchMeterUsage, check UnprocessedRecords)
- "How do I allocate usage across multiple customers or tags?" -> POST / (MeterUsage with UsageAllocations)
- "How do I verify a SaaS subscriber during redirect from AWS Marketplace?" -> POST / (ResolveCustomer)
- "When was the public key last rotated?" -> POST / (RegisterUsage, check PublicKeyRotationTimestamp)
- "How do I meter usage for a specific dimension?" -> POST / (MeterUsage with UsageDimension)
- "How do I get the AWS account ID of a marketplace buyer?" -> POST / (ResolveCustomer)
- "What product code is associated with a registration token?" -> POST / (ResolveCustomer)
- "How do I submit metering data for a container product?" -> POST / (RegisterUsage)

## Response Tips

- **BatchMeterUsage**: Results array maps 1:1 with input UsageRecords; always check UnprocessedRecords for partial failures and retry those entries.
- **MeterUsage**: A successful call returns a single MeteringRecordId string; null means the record was not accepted. DryRun responses validate without persisting.
- **RegisterUsage**: Signature is used for container-based entitlement verification; PublicKeyRotationTimestamp indicates when to refresh cached keys.
- **ResolveCustomer**: All three return fields (CustomerIdentifier, ProductCode, CustomerAWSAccountId) are optional -- a missing field signals incomplete marketplace registration.
- **General**: All endpoints use AWS SigV4 auth. Action is determined by the `X-Amz-Target` header, not the path (all share POST /).

## Anomaly Flags

- **UnprocessedRecords is non-empty**: Partial batch failure -- surface immediately with count and suggest retry with exponential backoff.
- **MeteringRecordId is null on 200**: Silent metering failure -- the call succeeded but no record was created. Flag for investigation.
- **PublicKeyRotationTimestamp changed**: Key rotation detected -- cached signatures may be invalid. Alert to refresh entitlement verification logic.
- **ResolveCustomer returns null fields**: Incomplete subscriber setup -- buyer may not have finished marketplace onboarding. Surface as a blocking issue for provisioning.
- **ThrottlingException (429)**: Rate limit hit -- AWS Marketplace Metering has strict per-second limits. Surface current call rate and recommend batching via BatchMeterUsage.
- **DuplicateRequest errors**: Idempotency conflict -- a record with the same timestamp and dimension was already submitted. Flag as informational, not failure.
- **InvalidProductCodeException**: Product code mismatch -- likely a configuration error between environments (staging vs production). Escalate immediately.

## Playbook

### 1. Onboard a New SaaS Subscriber

1. Receive the POST redirect from AWS Marketplace containing a `registration_token`
2. Call **ResolveCustomer** with the `RegistrationToken` to get `CustomerIdentifier`, `ProductCode`, and `CustomerAWSAccountId`
3. Verify all three fields are non-null; if any is missing, show the buyer a "registration pending" message
4. Store the `CustomerIdentifier` in your database, linked to the user account
5. Begin metering usage against that `CustomerIdentifier`

### 2. Report Hourly Usage for a SaaS Product

1. Aggregate usage data for each customer and dimension over the past hour
2. Build `UsageRecord` objects with `CustomerIdentifier`, `Dimension`, `Quantity`, and `Timestamp` (hour boundary)
3. Call **BatchMeterUsage** with the full array and your `ProductCode`
4. Inspect the response: process `Results` for confirmation, check `UnprocessedRecords` for failures
5. Retry any `UnprocessedRecords` with exponential backoff (max 3 attempts)

### 3. Validate Metering Before Going Live

1. Set up your product's usage dimensions in the AWS Marketplace Management Portal
2. Construct a **MeterUsage** request with a valid `ProductCode`, `UsageDimension`, current `Timestamp`, and `UsageQuantity`
3. Set `DryRun: true` to validate without persisting
4. Confirm a 200 response with no errors -- this verifies your auth, product code, and dimension names are correct
5. Remove `DryRun` (or set to false) to begin live metering

### 4. Set Up Container Entitlement Verification

1. Call **RegisterUsage** with your `ProductCode` and current `PublicKeyVersion`
2. Store the returned `Signature` and `PublicKeyRotationTimestamp`
3. Use the signature to verify the container is running with a valid AWS Marketplace entitlement
4. Periodically re-call RegisterUsage and compare `PublicKeyRotationTimestamp` -- if it changes, refresh your cached signature
5. Handle `CustomerNotEntitledException` by shutting down or degrading the container gracefully


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
