---
name: aws-price-list-service
description: "AWS Price List Service API skill. Use when working with AWS Price List Service for root. Covers 5 endpoints."
version: 1.0.0
generator: lapsh
---

# AWS Price List Service
API version: 2017-10-15

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

5 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Returns the metadata for one service or a list of the metadata for all services. Use this without a service code to get the service codes for all services. Use it with a service code, such as AmazonEC2, to get information specific to that service, such as the attribute names available for that service. For example, some of the attribute names available for EC2 are volumeType, maxIopsVolume, operation, locationType, and instanceCapacity10xlarge. |
| POST | / | Returns a list of attribute values. Attributes are similar to the details in a Price List API offer file. For a list of available attributes, see Offer File Definitions in the Billing and Cost Management User Guide. |
| POST | / | This feature is in preview release and is subject to change. Your use of Amazon Web Services Price List API is subject to the Beta Service Participation terms of the Amazon Web Services Service Terms (Section 1.10).   This returns the URL that you can retrieve your Price List file from. This URL is based on the PriceListArn and FileFormat that you retrieve from the ListPriceLists response. |
| POST | / | Returns a list of all products that match the filter criteria. |
| POST | / | This feature is in preview release and is subject to change. Your use of Amazon Web Services Price List API is subject to the Beta Service Participation terms of the Amazon Web Services Service Terms (Section 1.10).   This returns a list of Price List references that the requester if authorized to view, given a ServiceCode, CurrencyCode, and an EffectiveDate. Use without a RegionCode filter to list Price List references from all available Amazon Web Services Regions. Use with a RegionCode filter to get the Price List reference that's specific to a specific Amazon Web Services Region. You can use the PriceListArn from the response to get your preferred Price List files through the GetPriceListFileUrl API. |

## Enhanced Skill Content
## Question Mapping

- "What AWS services are available in the pricing catalog?" -> POST / (DescribeServices)
- "What attributes does AmazonEC2 support for filtering?" -> POST / (GetAttributeValues with ServiceCode + AttributeName)
- "What are the possible values for the 'instanceType' attribute in EC2?" -> POST / (GetAttributeValues)
- "How much does an m5.xlarge EC2 instance cost?" -> POST / (GetProducts with Filters)
- "Get all pricing data for AmazonS3." -> POST / (GetProducts with ServiceCode)
- "Filter RDS prices by region and engine type." -> POST / (GetProducts with multiple Filters)
- "Give me a download URL for a specific price list." -> POST / (GetPriceListFileUrl)
- "What price lists exist for AmazonEC2 as of today in USD?" -> POST / (ListPriceLists)
- "Are there price lists for AmazonEC2 in a specific region?" -> POST / (ListPriceLists with RegionCode)
- "How many services does AWS offer in the pricing API?" -> POST / (DescribeServices, count results)
- "What format versions are supported for pricing data?" -> POST / (DescribeServices with FormatVersion)
- "Page through all EC2 products matching a filter." -> POST / (GetProducts, follow NextToken)
- "Download the full price list JSON for Lambda." -> POST / (ListPriceLists) then POST / (GetPriceListFileUrl)

## Response Tips

- **DescribeServices**: `Services` array may be null if no matches; always check `NextToken` for additional pages since the default page size is small.
- **GetAttributeValues**: `AttributeValues` contains `{Value: str}` objects; paginate with `NextToken` and `MaxResults` (max 100).
- **GetPriceListFileUrl**: Returns a single pre-signed `Url` string; URL expires after a short window, so fetch it promptly.
- **GetProducts**: `PriceList` is an array of JSON-encoded strings (not objects) -- each entry must be parsed individually.
- **ListPriceLists**: `PriceLists` contains metadata objects with `PriceListArn`, `RegionCode`, `CurrencyCode`, and `EffectiveDate`; use the ARN to fetch the actual file via GetPriceListFileUrl.

## Anomaly Flags

- **Pagination truncation**: If `NextToken` is present in any response, warn the user that results are incomplete and offer to fetch the next page.
- **Empty result sets**: Surface when `Services`, `AttributeValues`, `PriceList`, or `PriceLists` is null or empty -- likely indicates an invalid ServiceCode or overly restrictive filters.
- **Throttling (429 / rate limit errors)**: AWS Pricing API has low default rate limits; flag when requests are being throttled and suggest adding delays.
- **Unparseable PriceList entries**: GetProducts returns JSON strings that may fail to parse; flag malformed entries rather than silently dropping them.
- **Expired download URLs**: If a GetPriceListFileUrl result is used after a delay, the pre-signed URL may have expired; flag HTTP 403 from the download as an expiry issue.
- **Stale EffectiveDate**: When using ListPriceLists, flag if the user-provided date is far in the past, as pricing data may not be available for old dates.

## Playbook

### 1. Discover available services and their filterable attributes

1. Call DescribeServices with no parameters to list all services.
2. Pick a ServiceCode from the results (e.g., `AmazonEC2`).
3. Call GetAttributeValues with that ServiceCode and an AttributeName (e.g., `instanceType`) to see valid filter values.
4. Repeat for other attribute names like `location`, `operatingSystem`, or `tenancy`.

### 2. Look up pricing for a specific product configuration

1. Call DescribeServices with `ServiceCode` to confirm the service exists and see its attributes.
2. Call GetAttributeValues for each relevant attribute to discover valid filter values.
3. Call GetProducts with `ServiceCode` and a `Filters` array matching your criteria (e.g., `instanceType=m5.xlarge`, `location=US East (N. Virginia)`).
4. Parse each string in the `PriceList` array as JSON to extract `OnDemand`, `Reserved`, or other pricing terms.
5. Follow `NextToken` if present to retrieve all matching products.

### 3. Download a full price list file

1. Call ListPriceLists with `ServiceCode`, `EffectiveDate` (today's date as ISO timestamp), and `CurrencyCode` (`USD`).
2. Optionally filter by `RegionCode` to narrow results.
3. Select the desired `PriceListArn` from the results.
4. Call GetPriceListFileUrl with that ARN and `FileFormat` (`json` or `csv`).
5. Fetch the returned `Url` immediately (it is a time-limited pre-signed URL).

### 4. Compare pricing across regions

1. Call ListPriceLists with `ServiceCode`, `EffectiveDate`, and `CurrencyCode` -- omit `RegionCode` to get all regions.
2. Collect the list of available `RegionCode` values from the results.
3. For each region of interest, call GetProducts with `ServiceCode` and a `location` filter matching that region.
4. Parse and compare the pricing terms across regions.

### 5. Page through a large result set

1. Make the initial API call (e.g., GetProducts) with `MaxResults` set to your preferred page size.
2. Check if `NextToken` is present in the response.
3. If present, repeat the same call with `NextToken` set to the returned value.
4. Continue until `NextToken` is absent, indicating the final page.
5. Aggregate all `PriceList` entries from every page before processing.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
