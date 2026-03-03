---
name: amazon-pinpoint-email-service
description: "Amazon Pinpoint Email Service API skill. Use when working with Amazon Pinpoint Email Service for email. Covers 42 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Pinpoint Email Service
API version: 2018-07-26

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
2. GET /v1/email/account -- verify access
3. POST /v1/email/configuration-sets -- create first configuration-sets

## Endpoints

42 endpoints across 1 groups. See references/api-spec.lap for full details.

### email
| Method | Path | Description |
|--------|------|-------------|
| POST | /v1/email/configuration-sets | Create a configuration set. Configuration sets are groups of rules that you can apply to the emails you send using Amazon Pinpoint. You apply a configuration set to an email by including a reference to the configuration set in the headers of the email. When you apply a configuration set to an email, all of the rules in that configuration set are applied to the email. |
| POST | /v1/email/configuration-sets/{ConfigurationSetName}/event-destinations | Create an event destination. In Amazon Pinpoint, events include message sends, deliveries, opens, clicks, bounces, and complaints. Event destinations are places that you can send information about these events to. For example, you can send event data to Amazon SNS to receive notifications when you receive bounces or complaints, or you can use Amazon Kinesis Data Firehose to stream data to Amazon S3 for long-term storage. A single configuration set can include more than one event destination. |
| POST | /v1/email/dedicated-ip-pools | Create a new pool of dedicated IP addresses. A pool can include one or more dedicated IP addresses that are associated with your Amazon Pinpoint account. You can associate a pool with a configuration set. When you send an email that uses that configuration set, Amazon Pinpoint sends it using only the IP addresses in the associated pool. |
| POST | /v1/email/deliverability-dashboard/test | Create a new predictive inbox placement test. Predictive inbox placement tests can help you predict how your messages will be handled by various email providers around the world. When you perform a predictive inbox placement test, you provide a sample message that contains the content that you plan to send to your customers. Amazon Pinpoint then sends that message to special email addresses spread across several major email providers. After about 24 hours, the test is complete, and you can use the GetDeliverabilityTestReport operation to view the results of the test. |
| POST | /v1/email/identities | Verifies an email identity for use with Amazon Pinpoint. In Amazon Pinpoint, an identity is an email address or domain that you use when you send email. Before you can use an identity to send email with Amazon Pinpoint, you first have to verify it. By verifying an address, you demonstrate that you're the owner of the address, and that you've given Amazon Pinpoint permission to send email from the address. When you verify an email address, Amazon Pinpoint sends an email to the address. Your email address is verified as soon as you follow the link in the verification email.  When you verify a domain, this operation provides a set of DKIM tokens, which you can convert into CNAME tokens. You add these CNAME tokens to the DNS configuration for your domain. Your domain is verified when Amazon Pinpoint detects these records in the DNS configuration for your domain. It usually takes around 72 hours to complete the domain verification process. |
| DELETE | /v1/email/configuration-sets/{ConfigurationSetName} | Delete an existing configuration set. In Amazon Pinpoint, configuration sets are groups of rules that you can apply to the emails you send. You apply a configuration set to an email by including a reference to the configuration set in the headers of the email. When you apply a configuration set to an email, all of the rules in that configuration set are applied to the email. |
| DELETE | /v1/email/configuration-sets/{ConfigurationSetName}/event-destinations/{EventDestinationName} | Delete an event destination. In Amazon Pinpoint, events include message sends, deliveries, opens, clicks, bounces, and complaints. Event destinations are places that you can send information about these events to. For example, you can send event data to Amazon SNS to receive notifications when you receive bounces or complaints, or you can use Amazon Kinesis Data Firehose to stream data to Amazon S3 for long-term storage. |
| DELETE | /v1/email/dedicated-ip-pools/{PoolName} | Delete a dedicated IP pool. |
| DELETE | /v1/email/identities/{EmailIdentity} | Deletes an email identity that you previously verified for use with Amazon Pinpoint. An identity can be either an email address or a domain name. |
| GET | /v1/email/account | Obtain information about the email-sending status and capabilities of your Amazon Pinpoint account in the current AWS Region. |
| GET | /v1/email/deliverability-dashboard/blacklist-report | Retrieve a list of the blacklists that your dedicated IP addresses appear on. |
| GET | /v1/email/configuration-sets/{ConfigurationSetName} | Get information about an existing configuration set, including the dedicated IP pool that it's associated with, whether or not it's enabled for sending email, and more. In Amazon Pinpoint, configuration sets are groups of rules that you can apply to the emails you send. You apply a configuration set to an email by including a reference to the configuration set in the headers of the email. When you apply a configuration set to an email, all of the rules in that configuration set are applied to the email. |
| GET | /v1/email/configuration-sets/{ConfigurationSetName}/event-destinations | Retrieve a list of event destinations that are associated with a configuration set. In Amazon Pinpoint, events include message sends, deliveries, opens, clicks, bounces, and complaints. Event destinations are places that you can send information about these events to. For example, you can send event data to Amazon SNS to receive notifications when you receive bounces or complaints, or you can use Amazon Kinesis Data Firehose to stream data to Amazon S3 for long-term storage. |
| GET | /v1/email/dedicated-ips/{IP} | Get information about a dedicated IP address, including the name of the dedicated IP pool that it's associated with, as well information about the automatic warm-up process for the address. |
| GET | /v1/email/dedicated-ips | List the dedicated IP addresses that are associated with your Amazon Pinpoint account. |
| GET | /v1/email/deliverability-dashboard | Retrieve information about the status of the Deliverability dashboard for your Amazon Pinpoint account. When the Deliverability dashboard is enabled, you gain access to reputation, deliverability, and other metrics for the domains that you use to send email using Amazon Pinpoint. You also gain the ability to perform predictive inbox placement tests. When you use the Deliverability dashboard, you pay a monthly subscription charge, in addition to any other fees that you accrue by using Amazon Pinpoint. For more information about the features and cost of a Deliverability dashboard subscription, see Amazon Pinpoint Pricing. |
| GET | /v1/email/deliverability-dashboard/test-reports/{ReportId} | Retrieve the results of a predictive inbox placement test. |
| GET | /v1/email/deliverability-dashboard/campaigns/{CampaignId} | Retrieve all the deliverability data for a specific campaign. This data is available for a campaign only if the campaign sent email by using a domain that the Deliverability dashboard is enabled for (PutDeliverabilityDashboardOption operation). |
| GET | /v1/email/deliverability-dashboard/statistics-report/{Domain} | Retrieve inbox placement and engagement rates for the domains that you use to send email. |
| GET | /v1/email/identities/{EmailIdentity} | Provides information about a specific identity associated with your Amazon Pinpoint account, including the identity's verification status, its DKIM authentication status, and its custom Mail-From settings. |
| GET | /v1/email/configuration-sets | List all of the configuration sets associated with your Amazon Pinpoint account in the current region. In Amazon Pinpoint, configuration sets are groups of rules that you can apply to the emails you send. You apply a configuration set to an email by including a reference to the configuration set in the headers of the email. When you apply a configuration set to an email, all of the rules in that configuration set are applied to the email. |
| GET | /v1/email/dedicated-ip-pools | List all of the dedicated IP pools that exist in your Amazon Pinpoint account in the current AWS Region. |
| GET | /v1/email/deliverability-dashboard/test-reports | Show a list of the predictive inbox placement tests that you've performed, regardless of their statuses. For predictive inbox placement tests that are complete, you can use the GetDeliverabilityTestReport operation to view the results. |
| GET | /v1/email/deliverability-dashboard/domains/{SubscribedDomain}/campaigns | Retrieve deliverability data for all the campaigns that used a specific domain to send email during a specified time range. This data is available for a domain only if you enabled the Deliverability dashboard (PutDeliverabilityDashboardOption operation) for the domain. |
| GET | /v1/email/identities | Returns a list of all of the email identities that are associated with your Amazon Pinpoint account. An identity can be either an email address or a domain. This operation returns identities that are verified as well as those that aren't. |
| GET | /v1/email/tags | Retrieve a list of the tags (keys and values) that are associated with a specified resource. A tag is a label that you optionally define and associate with a resource in Amazon Pinpoint. Each tag consists of a required tag key and an optional associated tag value. A tag key is a general label that acts as a category for more specific tag values. A tag value acts as a descriptor within a tag key. |
| PUT | /v1/email/account/dedicated-ips/warmup | Enable or disable the automatic warm-up feature for dedicated IP addresses. |
| PUT | /v1/email/account/sending | Enable or disable the ability of your account to send email. |
| PUT | /v1/email/configuration-sets/{ConfigurationSetName}/delivery-options | Associate a configuration set with a dedicated IP pool. You can use dedicated IP pools to create groups of dedicated IP addresses for sending specific types of email. |
| PUT | /v1/email/configuration-sets/{ConfigurationSetName}/reputation-options | Enable or disable collection of reputation metrics for emails that you send using a particular configuration set in a specific AWS Region. |
| PUT | /v1/email/configuration-sets/{ConfigurationSetName}/sending | Enable or disable email sending for messages that use a particular configuration set in a specific AWS Region. |
| PUT | /v1/email/configuration-sets/{ConfigurationSetName}/tracking-options | Specify a custom domain to use for open and click tracking elements in email that you send using Amazon Pinpoint. |
| PUT | /v1/email/dedicated-ips/{IP}/pool | Move a dedicated IP address to an existing dedicated IP pool.  The dedicated IP address that you specify must already exist, and must be associated with your Amazon Pinpoint account.  The dedicated IP pool you specify must already exist. You can create a new pool by using the CreateDedicatedIpPool operation. |
| PUT | /v1/email/dedicated-ips/{IP}/warmup |  |
| PUT | /v1/email/deliverability-dashboard | Enable or disable the Deliverability dashboard for your Amazon Pinpoint account. When you enable the Deliverability dashboard, you gain access to reputation, deliverability, and other metrics for the domains that you use to send email using Amazon Pinpoint. You also gain the ability to perform predictive inbox placement tests. When you use the Deliverability dashboard, you pay a monthly subscription charge, in addition to any other fees that you accrue by using Amazon Pinpoint. For more information about the features and cost of a Deliverability dashboard subscription, see Amazon Pinpoint Pricing. |
| PUT | /v1/email/identities/{EmailIdentity}/dkim | Used to enable or disable DKIM authentication for an email identity. |
| PUT | /v1/email/identities/{EmailIdentity}/feedback | Used to enable or disable feedback forwarding for an identity. This setting determines what happens when an identity is used to send an email that results in a bounce or complaint event. When you enable feedback forwarding, Amazon Pinpoint sends you email notifications when bounce or complaint events occur. Amazon Pinpoint sends this notification to the address that you specified in the Return-Path header of the original email. When you disable feedback forwarding, Amazon Pinpoint sends notifications through other mechanisms, such as by notifying an Amazon SNS topic. You're required to have a method of tracking bounces and complaints. If you haven't set up another mechanism for receiving bounce or complaint notifications, Amazon Pinpoint sends an email notification when these events occur (even if this setting is disabled). |
| PUT | /v1/email/identities/{EmailIdentity}/mail-from | Used to enable or disable the custom Mail-From domain configuration for an email identity. |
| POST | /v1/email/outbound-emails | Sends an email message. You can use the Amazon Pinpoint Email API to send two types of messages:    Simple – A standard email message. When you create this type of message, you specify the sender, the recipient, and the message body, and Amazon Pinpoint assembles the message for you.    Raw – A raw, MIME-formatted email message. When you send this type of email, you have to specify all of the message headers, as well as the message body. You can use this message type to send messages that contain attachments. The message that you specify has to be a valid MIME message. |
| POST | /v1/email/tags | Add one or more tags (keys and values) to a specified resource. A tag is a label that you optionally define and associate with a resource in Amazon Pinpoint. Tags can help you categorize and manage resources in different ways, such as by purpose, owner, environment, or other criteria. A resource can have as many as 50 tags. Each tag consists of a required tag key and an associated tag value, both of which you define. A tag key is a general label that acts as a category for more specific tag values. A tag value acts as a descriptor within a tag key. |
| DELETE | /v1/email/tags | Remove one or more tags (keys and values) from a specified resource. |
| PUT | /v1/email/configuration-sets/{ConfigurationSetName}/event-destinations/{EventDestinationName} | Update the configuration of an event destination for a configuration set. In Amazon Pinpoint, events include message sends, deliveries, opens, clicks, bounces, and complaints. Event destinations are places that you can send information about these events to. For example, you can send event data to Amazon SNS to receive notifications when you receive bounces or complaints, or you can use Amazon Kinesis Data Firehose to stream data to Amazon S3 for long-term storage. |

## Enhanced Skill Content
## Question Mapping

- "How do I send an email?" -> POST /v1/email/outbound-emails
- "What is my current sending quota and rate limit?" -> GET /v1/email/account
- "How do I verify a new email identity or domain?" -> POST /v1/email/identities
- "Is my domain verified for sending?" -> GET /v1/email/identities/{EmailIdentity}
- "How do I run a deliverability test for my email?" -> POST /v1/email/deliverability-dashboard/test
- "What were the results of my deliverability test?" -> GET /v1/email/deliverability-dashboard/test-reports/{ReportId}
- "How do I create a configuration set for tracking?" -> POST /v1/email/configuration-sets
- "Which IPs are warming up and what percentage are they at?" -> GET /v1/email/dedicated-ips
- "How do I move a dedicated IP to a different pool?" -> PUT /v1/email/dedicated-ips/{IP}/pool
- "What campaigns ran on my domain this month?" -> GET /v1/email/deliverability-dashboard/domains/{SubscribedDomain}/campaigns
- "Is my domain blacklisted anywhere?" -> GET /v1/email/deliverability-dashboard/blacklist-report
- "How do I enable or disable sending for my account?" -> PUT /v1/email/account/sending
- "What are the inbox vs spam placement stats for my domain?" -> GET /v1/email/deliverability-dashboard/statistics-report/{Domain}
- "How do I set up event destinations for bounce/complaint tracking?" -> POST /v1/email/configuration-sets/{ConfigurationSetName}/event-destinations

## Response Tips

- **Account & Sending:** `SendQuota` nests `Max24HourSend`, `MaxSendRate`, and `SentLast24Hours` as floats -- compare `SentLast24Hours` against `Max24HourSend` to gauge headroom.
- **List endpoints (configuration-sets, IPs, identities, pools, test-reports, campaigns):** All paginate via `NextToken` + `PageSize`; keep calling until `NextToken` is null.
- **Identity creation:** Returns partial verification state immediately; `DkimAttributes.Status` will be `PENDING` until DNS records propagate -- poll with the GET endpoint.
- **Deliverability test reports:** `OverallPlacement` percentages (Inbox, Spam, Missing, SPF, DKIM) are floats 0-100; `IspPlacements` is an array breaking this down per ISP.
- **Campaign stats:** Counts (`InboxCount`, `SpamCount`) are i64 integers; rates (`ReadRate`, `DeleteRate`) are floats between 0 and 1.
- **Blacklist report:** Returns `map<str, [BlacklistEntry]>` keyed by IP address -- iterate keys to check each IP's listing status.
- **Send email:** Success returns `{ MessageId }` -- a null or missing `MessageId` with a 200 is abnormal and should be flagged.

## Anomaly Flags

- **Sending quota near limit:** Surface a warning when `SentLast24Hours` exceeds 80% of `Max24HourSend` from GET /v1/email/account.
- **Sending disabled:** Alert if `SendingEnabled` is `false` on the account or on a configuration set the user is trying to use.
- **DKIM not verified:** Flag when `DkimAttributes.Status` is anything other than `SUCCESS` after identity creation, especially `FAILED` or `TEMPORARY_FAILURE`.
- **IP warmup incomplete:** Warn when `WarmupStatus` is `IN_PROGRESS` and `WarmupPercentage` is below 50% -- sending high volume on cold IPs harms reputation.
- **Blacklist detections:** Proactively surface any non-empty entries in the blacklist report response.
- **Deliverability dashboard expired or inactive:** Flag if `DashboardEnabled` is `false` or `SubscriptionExpiryDate` is in the past.
- **High spam placement:** Alert when `SpamPercentage` exceeds 5% in deliverability test results or domain statistics.
- **Production access not enabled:** Warn if `ProductionAccessEnabled` is `false` -- the account is in sandbox mode and can only send to verified identities.
- **Mail-from domain misconfigured:** Flag when `MailFromDomainStatus` is `FAILED` on an identity, as this degrades authentication alignment.

## Playbook

### 1. Set Up a New Sending Domain from Scratch

1. Create the email identity: POST /v1/email/identities with `EmailIdentity` set to your domain.
2. Note the `DkimAttributes.Tokens` array from the response -- create CNAME DNS records for each token.
3. Poll GET /v1/email/identities/{EmailIdentity} until `DkimAttributes.Status` becomes `SUCCESS`.
4. Optionally configure a custom MAIL FROM domain: PUT /v1/email/identities/{EmailIdentity}/mail-from.
5. Verify account sending is enabled: GET /v1/email/account, check `SendingEnabled` and `ProductionAccessEnabled`.
6. Send a test email: POST /v1/email/outbound-emails.

### 2. Run a Deliverability Test and Analyze Results

1. Create a deliverability test: POST /v1/email/deliverability-dashboard/test with `FromEmailAddress` and `Content`.
2. Note the `ReportId` from the response.
3. Poll GET /v1/email/deliverability-dashboard/test-reports/{ReportId} until `DeliverabilityTestStatus` is `COMPLETED`.
4. Review `OverallPlacement` for inbox vs spam percentages.
5. Drill into `IspPlacements` to identify ISPs with low inbox rates.
6. If spam placement is high, check GET /v1/email/deliverability-dashboard/blacklist-report for IP reputation issues.

### 3. Configure Event Tracking for Bounces and Complaints

1. Create a configuration set: POST /v1/email/configuration-sets with a descriptive `ConfigurationSetName`.
2. Enable reputation metrics: PUT /v1/email/configuration-sets/{ConfigurationSetName}/reputation-options with `ReputationMetricsEnabled: true`.
3. Add an event destination (e.g., SNS, CloudWatch, Kinesis): POST /v1/email/configuration-sets/{ConfigurationSetName}/event-destinations.
4. Enable sending on the configuration set: PUT /v1/email/configuration-sets/{ConfigurationSetName}/sending with `SendingEnabled: true`.
5. Reference `ConfigurationSetName` in POST /v1/email/outbound-emails to route events through this configuration.

### 4. Manage Dedicated IP Warm-Up

1. Create a dedicated IP pool: POST /v1/email/dedicated-ip-pools with a `PoolName`.
2. List dedicated IPs: GET /v1/email/dedicated-ips to find IPs and their current pool assignments.
3. Move an IP into your pool: PUT /v1/email/dedicated-ips/{IP}/pool with `DestinationPoolName`.
4. Enable auto warm-up at the account level: PUT /v1/email/account/dedicated-ips/warmup with `AutoWarmupEnabled: true`.
5. Monitor warm-up progress: GET /v1/email/dedicated-ips/{IP} -- check `WarmupPercentage` and `WarmupStatus`.
6. Optionally set a manual warm-up percentage: PUT /v1/email/dedicated-ips/{IP}/warmup.

### 5. Audit Domain Reputation and Campaign Performance

1. Check overall deliverability dashboard status: GET /v1/email/deliverability-dashboard.
2. Pull domain statistics for a date range: GET /v1/email/deliverability-dashboard/statistics-report/{Domain} with `StartDate` and `EndDate`.
3. Review `OverallVolume.VolumeStatistics` for inbox vs spam raw counts and projections.
4. List campaigns for the domain: GET /v1/email/deliverability-dashboard/domains/{SubscribedDomain}/campaigns.
5. For each campaign, check `ReadRate` and `DeleteRate` -- a high delete rate signals content or targeting issues.
6. Cross-reference with blacklist data: GET /v1/email/deliverability-dashboard/blacklist-report to rule out IP reputation problems.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
