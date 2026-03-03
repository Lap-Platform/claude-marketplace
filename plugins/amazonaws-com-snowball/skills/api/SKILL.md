---
name: amazon-importexport-snowball
description: "Amazon Import/Export Snowball API skill. Use when working with Amazon Import/Export Snowball for root. Covers 27 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Import/Export Snowball
API version: 2016-06-30

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

27 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Cancels a cluster job. You can only cancel a cluster job while it's in the AwaitingQuorum status. You'll have at least an hour after creating a cluster job to cancel it. |
| POST | / | Cancels the specified job. You can only cancel a job before its JobState value changes to PreparingAppliance. Requesting the ListJobs or DescribeJob action returns a job's JobState as part of the response element data returned. |
| POST | / | Creates an address for a Snow device to be shipped to. In most regions, addresses are validated at the time of creation. The address you provide must be located within the serviceable area of your region. If the address is invalid or unsupported, then an exception is thrown. If providing an address as a JSON file through the cli-input-json option, include the full file path. For example, --cli-input-json file://create-address.json. |
| POST | / | Creates an empty cluster. Each cluster supports five nodes. You use the CreateJob action separately to create the jobs for each of these nodes. The cluster does not ship until these five node jobs have been created. |
| POST | / | Creates a job to import or export data between Amazon S3 and your on-premises data center. Your Amazon Web Services account must have the right trust policies and permissions in place to create a job for a Snow device. If you're creating a job for a node in a cluster, you only need to provide the clusterId value; the other job attributes are inherited from the cluster.   Only the Snowball; Edge device type is supported when ordering clustered jobs. The device capacity is optional. Availability of device types differ by Amazon Web Services Region. For more information about Region availability, see Amazon Web Services Regional Services.    Snow Family devices and their capacities.    Device type: SNC1_SSD    Capacity: T14   Description: Snowcone       Device type: SNC1_HDD    Capacity: T8   Description: Snowcone       Device type: EDGE_S    Capacity: T98   Description: Snowball Edge Storage Optimized for data transfer only       Device type: EDGE_CG    Capacity: T42   Description: Snowball Edge Compute Optimized with GPU      Device type: EDGE_C    Capacity: T42   Description: Snowball Edge Compute Optimized without GPU      Device type: EDGE    Capacity: T100   Description: Snowball Edge Storage Optimized with EC2 Compute    This device is replaced with T98.     Device type: STANDARD    Capacity: T50   Description: Original Snowball device  This device is only available in the Ningxia, Beijing, and Singapore Amazon Web Services Region        Device type: STANDARD    Capacity: T80   Description: Original Snowball device  This device is only available in the Ningxia, Beijing, and Singapore Amazon Web Services Region.        Snow Family device type: RACK_5U_C    Capacity: T13    Description: Snowblade.     Device type: V3_5S    Capacity: T240   Description: Snowball Edge Storage Optimized 210TB |
| POST | / | Creates a job with the long-term usage option for a device. The long-term usage is a 1-year or 3-year long-term pricing type for the device. You are billed upfront, and Amazon Web Services provides discounts for long-term pricing. |
| POST | / | Creates a shipping label that will be used to return the Snow device to Amazon Web Services. |
| POST | / | Takes an AddressId and returns specific details about that address in the form of an Address object. |
| POST | / | Returns a specified number of ADDRESS objects. Calling this API in one of the US regions will return addresses from the list of all addresses associated with this account in all US regions. |
| POST | / | Returns information about a specific cluster including shipping information, cluster status, and other important metadata. |
| POST | / | Returns information about a specific job including shipping information, job status, and other important metadata. |
| POST | / | Information on the shipping label of a Snow device that is being returned to Amazon Web Services. |
| POST | / | Returns a link to an Amazon S3 presigned URL for the manifest file associated with the specified JobId value. You can access the manifest file for up to 60 minutes after this request has been made. To access the manifest file after 60 minutes have passed, you'll have to make another call to the GetJobManifest action. The manifest is an encrypted file that you can download after your job enters the WithCustomer status. This is the only valid status for calling this API as the manifest and UnlockCode code value are used for securing your device and should only be used when you have the device. The manifest is decrypted by using the UnlockCode code value, when you pass both values to the Snow device through the Snowball client when the client is started for the first time.  As a best practice, we recommend that you don't save a copy of an UnlockCode value in the same location as the manifest file for that job. Saving these separately helps prevent unauthorized parties from gaining access to the Snow device associated with that job. The credentials of a given job, including its manifest file and unlock code, expire 360 days after the job is created. |
| POST | / | Returns the UnlockCode code value for the specified job. A particular UnlockCode value can be accessed for up to 360 days after the associated job has been created. The UnlockCode value is a 29-character code with 25 alphanumeric characters and 4 hyphens. This code is used to decrypt the manifest file when it is passed along with the manifest to the Snow device through the Snowball client when the client is started for the first time. The only valid status for calling this API is WithCustomer as the manifest and Unlock code values are used for securing your device and should only be used when you have the device. As a best practice, we recommend that you don't save a copy of the UnlockCode in the same location as the manifest file for that job. Saving these separately helps prevent unauthorized parties from gaining access to the Snow device associated with that job. |
| POST | / | Returns information about the Snow Family service limit for your account, and also the number of Snow devices your account has in use. The default service limit for the number of Snow devices that you can have at one time is 1. If you want to increase your service limit, contact Amazon Web Services Support. |
| POST | / | Returns an Amazon S3 presigned URL for an update file associated with a specified JobId. |
| POST | / | Returns an array of JobListEntry objects of the specified length. Each JobListEntry object is for a job in the specified cluster and contains a job's state, a job's ID, and other information. |
| POST | / | Returns an array of ClusterListEntry objects of the specified length. Each ClusterListEntry object contains a cluster's state, a cluster's ID, and other important status information. |
| POST | / | This action returns a list of the different Amazon EC2-compatible Amazon Machine Images (AMIs) that are owned by your Amazon Web Services accountthat would be supported for use on a Snow device. Currently, supported AMIs are based on the Amazon Linux-2, Ubuntu 20.04 LTS - Focal, or Ubuntu 22.04 LTS - Jammy images, available on the Amazon Web Services Marketplace. Ubuntu 16.04 LTS - Xenial (HVM) images are no longer supported in the Market, but still supported for use on devices through Amazon EC2 VM Import/Export and running locally in AMIs. |
| POST | / | Returns an array of JobListEntry objects of the specified length. Each JobListEntry object contains a job's state, a job's ID, and a value that indicates whether the job is a job part, in the case of export jobs. Calling this API action in one of the US regions will return jobs from the list of all jobs associated with this account in all US regions. |
| POST | / | Lists all long-term pricing types. |
| POST | / | A list of locations from which the customer can choose to pickup a device. |
| POST | / | Lists all supported versions for Snow on-device services. Returns an array of ServiceVersion object containing the supported versions for a particular service. |
| POST | / | While a cluster's ClusterState value is in the AwaitingQuorum state, you can update some of the information associated with a cluster. Once the cluster changes to a different job state, usually 60 minutes after the cluster being created, this action is no longer available. |
| POST | / | While a job's JobState value is New, you can update some of the information associated with a job. Once the job changes to a different job state, usually within 60 minutes of the job being created, this action is no longer available. |
| POST | / | Updates the state when a shipment state changes to a different state. |
| POST | / | Updates the long-term pricing type. |

## Enhanced Skill Content
## Question Mapping

- "How do I order a new Snowball device?" -> POST / (CreateJob)
- "How do I create a cluster of Snowball devices?" -> POST / (CreateCluster)
- "What is the current status of my job?" -> POST / (DescribeJob)
- "How many Snowballs am I currently using vs my limit?" -> POST / (GetSnowballUsage)
- "Where is my Snowball shipment right now?" -> POST / (DescribeJob, check ShippingDetails.InboundShipment/OutboundShipment)
- "How do I cancel a job I no longer need?" -> POST / (CancelJob)
- "How do I get the unlock code for my device?" -> POST / (GetJobUnlockCode)
- "How do I download the manifest for my job?" -> POST / (GetJobManifest)
- "What jobs belong to my cluster?" -> POST / (ListClusterJobs)
- "How do I set up long-term pricing for Snowball?" -> POST / (CreateLongTermPricing)
- "How do I create a return shipping label?" -> POST / (CreateReturnShippingLabel)
- "What AMIs are compatible with my Snowball Edge?" -> POST / (ListCompatibleImages)
- "How do I update the notification settings on an existing job?" -> POST / (UpdateJob)
- "How do I register a new shipping address?" -> POST / (CreateAddress)
- "What software updates are available for my device?" -> POST / (GetSoftwareUpdates)

## Response Tips

- **Describe endpoints** (DescribeJob, DescribeCluster): Deeply nested metadata objects -- always drill into sub-objects like `ShippingDetails.InboundShipment`, `DataTransferProgress`, and `OnDeviceServiceConfiguration` for the fields you need.
- **List endpoints** (ListJobs, ListClusters, ListClusterJobs, ListLongTermPricingEntries, ListCompatibleImages, ListPickupLocations): All use `MaxResults`/`NextToken` cursor-based pagination -- keep calling with the returned `NextToken` until it is null.
- **Create endpoints** (CreateJob, CreateCluster, CreateAddress): Return only the new resource ID (e.g., `JobId`, `ClusterId`, `AddressId`) -- follow up with the matching Describe call for full details.
- **Update/Cancel endpoints**: Return no body on success (HTTP 200 with empty JSON) -- treat any non-error response as confirmation.
- **URI endpoints** (GetJobManifest, GetSoftwareUpdates, DescribeReturnShippingLabel): Return pre-signed S3 URIs that expire -- download promptly and do not cache long-term.
- **Error responses**: AWS errors come as JSON with `__type` and `message` fields; watch for `InvalidJobStateException` when operating on jobs in terminal states.

## Anomaly Flags

- **Snowball usage nearing limit**: After `GetSnowballUsage`, surface a warning when `SnowballsInUse` exceeds 80% of `SnowballLimit`.
- **Job stuck in non-terminal state**: If `DescribeJob` returns `JobState` of `InProgress` or `Listing` for an extended period with zero `DataTransferProgress.BytesTransferred`, flag as potentially stalled.
- **Return shipping label expiring**: `DescribeReturnShippingLabel` returns `ExpirationDate` -- alert if expiration is within 7 days.
- **Inbound/outbound shipment status mismatch**: If `OutboundShipment.Status` shows delivered but `JobState` has not advanced, flag for investigation.
- **Long-term pricing auto-renew off**: When listing long-term pricing entries, surface any that are approaching expiration without auto-renew enabled.
- **Cluster in partially degraded state**: If `ListClusterJobs` returns jobs with mixed states (some failed, some active), flag the cluster for review.
- **Data transfer incomplete at job completion**: If `JobState` is `Complete` but `TotalBytes` does not equal `BytesTransferred`, surface the discrepancy.

## Playbook

### 1. Order and Track a New Snowball Device

1. Call **CreateAddress** with your shipping address to get an `AddressId`.
2. Call **CreateJob** with `JobType`, `AddressId`, `SnowballType`, `ShippingOption`, and any S3/Lambda resources.
3. Note the returned `JobId`.
4. Call **DescribeJob** with the `JobId` to monitor `JobState` and `ShippingDetails.OutboundShipment`.
5. Once `JobState` reaches `WithCustomer`, call **GetJobUnlockCode** and **GetJobManifest** to prepare the device.
6. After data transfer, call **CreateReturnShippingLabel** and ship the device back.
7. Monitor with **DescribeJob** until `JobState` reaches `Complete`.

### 2. Set Up a Multi-Device Cluster

1. Call **CreateAddress** if you need a new shipping destination.
2. Call **CreateCluster** with `JobType`, `AddressId`, `SnowballType`, `ShippingOption`, and `InitialClusterSize`.
3. Note the returned `ClusterId` and any `JobListEntries`.
4. Call **ListClusterJobs** with `ClusterId` to see all member jobs and their states.
5. Call **DescribeJob** on each member job to track individual device progress.
6. Use **UpdateCluster** to modify resources, notifications, or forwarding address as needed.

### 3. Manage Long-Term Pricing

1. Call **CreateLongTermPricing** with `LongTermPricingType` (one-year or three-year) and `SnowballType`.
2. Note the returned `LongTermPricingId`.
3. Call **ListLongTermPricingEntries** periodically to review all active pricing agreements.
4. To assign a replacement job, call **UpdateLongTermPricing** with `ReplacementJob`.
5. To toggle auto-renewal, call **UpdateLongTermPricing** with `IsLongTermPricingAutoRenew`.

### 4. Cancel and Clean Up Resources

1. Call **DescribeJob** to verify the job is in a cancellable state (not yet `InProgress` with data).
2. Call **CancelJob** with the `JobId`.
3. If the job belongs to a cluster, call **DescribeCluster** to check remaining cluster health.
4. If all cluster jobs are cancelled or failed, call **CancelCluster** with the `ClusterId`.
5. Confirm cleanup by calling **GetSnowballUsage** to verify device counts have decremented.

### 5. Retrieve Device Credentials and Updates

1. Call **DescribeJob** to confirm `JobState` is `WithCustomer`.
2. Call **GetJobManifest** to get the `ManifestURI` -- download the manifest file immediately.
3. Call **GetJobUnlockCode** to get the `UnlockCode` for the device.
4. Call **GetSoftwareUpdates** to get `UpdatesURI` and apply any available firmware updates.
5. Use the manifest and unlock code together to authenticate to the Snowball device locally.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
