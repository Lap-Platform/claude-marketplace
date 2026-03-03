---
name: item-feed-service
description: "Item Feed Service API skill. Use when working with Item Feed Service for item, item_group, item_snapshot. Covers 4 endpoints."
version: 1.0.0
generator: lapsh
---

# Item Feed Service
API version: v1_beta.34.0

## Auth
OAuth2

## Base URL
https://api.ebay.com/buy/feed/v1_beta

## Setup
1. Configure auth: OAuth2
2. GET /item -- verify access

## Endpoints

4 endpoints across 4 groups. See references/api-spec.lap for full details.

### item
| Method | Path | Description |
|--------|------|-------------|
| GET | /item | <p>This method lets you download a TSV_GZIP (tab separated value gzip) <b> Item</b> feed file. The feed file contains all the items from <b> all</b> the child categories of the specified category.  The first line of the file is the header, which labels the columns and indicates the order of the values on each line.  Each header is described in the <a href="/api-docs/buy/feed/resources/item/methods/getItemFeed#h3-response-fields">Response fields</a> section.  </p> <p> There are two types of item feed files generated: <ul> <li>A daily <b>Item</b> feed file containing all the newly listed items for a specific category, date, and marketplace (<b>feed_scope</b> = <code>NEWLY_LISTED</code>)</li>  <li>A weekly <b>Item Bootstrap</b> feed file containing <i> all</i> the items in a specific category and marketplace (<b>feed_scope</b> = <code>ALL_ACTIVE</code>)</li>  </ul>  </p>   <p><span class="tablenote"><b>Note: </b>  Filters are applied to the feed files. For details, see <a href="/api-docs/buy/static/api-feed_beta.html#Feed2">Feed File Filters</a>. When curating the items returned, be sure to code as if these filters are not applied as they can be changed or removed in the future.</span></p><h3><b>Downloading feed files </b></h3>             <p>Item feed files are binary gzip files. If the file is larger than 100 MB, the download must be streamed in chunks. You specify the size of the chunks in bytes using the <a href="#range-header">Range</a> request header. The <a href="#content-range">Content-range</a> response header indicates where in the full resource this partial chunk of data belongs  and the total number of bytes in the file.       For more information about using these headers, see <a href="/api-docs/buy/static/api-feed_beta.html#retrv-gzip">Retrieving a gzip feed file</a>.    </p>    <p>In addition to the API, there is an open source <a href="https://github.com/eBay/FeedSDK" target="_blank">Feed SDK</a> written in Java that downloads, combines files into a single file when needed, and unzips the entire feed file. It also lets you specify field filters to curate the items in the file.</p>              <p><span class="tablenote">  <b> Note:</b> A successful call will always return a TSV.GZIP file; however, unsuccessful calls generate errors that are returned in JSON format. For documentation purposes, the successful call response is shown below as JSON fields so that the value returned in each column can be explained. The order of the response fields shows the order of the columns in the feed file.</span>  </p>                <h3><b>Restrictions </b></h3>                <p>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/feed/overview.html#API">API Restrictions</a>.</p> |

### item_group
| Method | Path | Description |
|--------|------|-------------|
| GET | /item_group | <p>This method lets you download a TSV_GZIP (tab separated value gzip) <b> Item Group</b> feed file. An item group is an item that has various aspect differences, such as color, size, storage capacity, etc. </p> <p>There are two types of item group feed files generated: <ul> <li>A daily <b>Item Group</b> feed file containing the item group variation information associated with items returned in the <a href="/api-docs/buy/feed/resources/item/methods/getItemFeed">Item</a> feed file for a specific day, category, and marketplace. (<b>feed_scope</b> = <code>NEWLY_LISTED</code>)</li>  <li>A weekly <b>Item Group Bootstrap</b> feed file containing all the item group variation information associated with items returned in the <a href="/api-docs/buy/feed/resources/item/methods/getItemFeed">Item Bootstrap</a> feed file for all the items in a specific category.  (<b>feed_scope</b> = <code>ALL_ACTIVE</code>)</li>  </ul></p>  <p><span class="tablenote"><b>Note: </b>  Filters are applied to the feed files. For details, see <a href="/api-docs/buy/static/api-feed.html#feed-filters">Feed File Filters</a>.  When curating the items returned, be sure to code as if these filters are not applied as they can be changed or removed in the future.</span></p>    <p>The contents of these feed files are based on the contents of the corresponding daily <b> Item</b> or <b>Item Bootstrap</b> feed file. When a new <b> Item</b> or <b>Item Bootstrap</b> feed file is generated, the service reads the file and if an item in the file has a <b> primaryItemGroupId</b> value, which indicates the item is part of an item group, it uses that value to return the item group (parent item) information for that item in the corresponding <b> Item Group</b> or <b> Item Group Bootstrap</b> feed file.</p>  <p>  This information includes the  name/value pair of the aspects of the items in this group returned in the <b> variesByLocalizedAspects </b> column. For example, if the item was a shirt some of the variation names could be Size, Color, etc. Also the images for the various aspects are returned in the <b>additionalImageUrls</b> column.</p>              <p>The first line in any feed file is the header, which labels the columns and indicates the order of the values on each line.  Each header is described in the <a href="/api-docs/buy/feed/resources/item_group/methods/getItemGroupFeed#h3-response-fields">Response fields</a> section.</p>                                  <h3><b>Combining the Item Group and Item feed files</b></h3>              <p>The <b> Item Group</b> or <b> Item Group Bootstrap</b> feed file contains details about the item group (parent item), including the item group ID <b> itemGroupId</b>.  You match the value of <b> itemGroupId</b> from the <b> Item Group</b> feed file with the value of <b> primaryItemGroupId</b> from the corresponding daily <b> Item</b> or <b>Item Bootstrap</b> feed file.</p><h3><b>Downloading feed files </b></h3>                          <p>Item Group feed files are binary gzip files. If the file is larger than 100 MB, the download must be streamed in chunks. You specify the size of the chunks in bytes using the <a href="#range-header">Range</a> request header. The <a href="#content-range">content-range</a> response header indicates where in the full resource this partial chunk of data belongs  and the total number of bytes in the file.       For more information about using these headers, see <a href="/api-docs/{swift-folder}/buy/static/api-feed_beta.html#retrv-gzip">Retrieving a gzip feed file</a>. </p>                 <p><span class="tablenote">  <b> Note:</b>  A successful call will always return a TSV.GZIP file; however, unsuccessful calls generate errors that are returned in JSON format. For documentation purposes, the successful call response is shown below as JSON fields so that the value returned in each column can be explained. The order of the response fields shows the order of the columns in the feed file.</span>          </p>                        <h3><b>Restrictions </b></h3>                        <p>For a list of supported sites and other restrictions, see <a href="/api-docs/{swift-folder}/buy/feed/overview.html#API">API Restrictions</a>.  </p> |

### item_snapshot
| Method | Path | Description |
|--------|------|-------------|
| GET | /item_snapshot | <p>The <b> Hourly Snapshot</b> feed file is generated each hour every day for most categories. This method lets you download an <b> Hourly Snapshot</b> TSV_GZIP (tab-separated value gzip) feed file containing the details of all the items that have <a href="/api-docs/buy/static/api-feed.html#changed-items">changed</a> <i> within</i> the specified day and hour for a specific category.  This means to generate the 8AM file of items that have changed from 8AM and 8:59AM, the service starts at 9AM. You can retrieve the 8AM snapshot file at 10AM.</p>    <p>Snapshot feeds now include new listings. You can check <a href="/api-docs/buy/feed/resources/item_snapshot/methods/getItemSnapshotFeed#response.items.itemCreationDate">itemCreationDate</a> to identify listings that were newly created within the specified hour.</p>     <p><span class="tablenote"><b>Note: </b>  Filters are applied to the feed files. For details, see <a href="/api-docs/buy/static/api-feed.html#feed-filters">Feed File Filters</a>.  When curating the items returned, be sure to code as if these filters are not applied as they can be changed or removed in the future.</span></p>                  <p>You can use the response from this method to update the item details of items stored in your database. By looking at the value of <a href="/api-docs/buy/feed/resources/item_snapshot/methods/getItemSnapshotFeed#response.items.itemSnapshotDate">itemSnapshotDate</a> for a given item, you will be able to tell which information is the latest.</p>   <p><span class="tablenote"><span style="color:#FF0000"> <b> Important:</b> </span> When the value of the <b> availability</b> column is <code>UNAVAILABLE</code>, only the <b>itemId</b> and <b> availability</b> columns are populated. </span></p><h3><b>Downloading feed files </b></h3><p>Hourly snapshot feed files are binary gzip files. If the file is larger than 100 MB, the download must be streamed in chunks. You specify the size of the chunks in bytes using the <a href="#range-header">Range</a> request header. The <a href="#content-range">Content-range</a> response header indicates where in the full resource this partial chunk of data belongs and the total number of bytes in the file.       For more information about using these headers, see <a href="/api-docs/buy/static/api-feed_beta.html#retrv-gzip">Retrieving a gzip feed file</a>.  </p>                                <p><span class="tablenote">  <b> Note:</b> A successful call will always return a TSV.GZIP file; however, unsuccessful calls generate errors that are returned in JSON format. For documentation purposes, the successful call response is shown below as JSON fields so that the value returned in each column can be explained. The order of the response fields shows the order of the columns in the feed file.</span></p><h3><b>Restrictions </b></h3><p>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/feed/overview.html#API">API Restrictions</a>.</p> |

### item_priority
| Method | Path | Description |
|--------|------|-------------|
| GET | /item_priority | <p>Using this method, you can download a TSV_GZIP (tab separated value gzip) <b>Item Priority</b> feed file, which allows you to track changes (deltas) in the status of your priority items, such as when an item is added or removed from a campaign.  The delta feed tracks the changes to the status of items within a category you specify in the input URI. You can also specify a specific date for the feed you want returned.</p><p><span class="tablenote"><span style="color:#FF0000"> <b> Important:</b> </span> You must consume the daily feeds (<b>Item</b>, <b>Item Group</b>) before consuming the <b>Item Priority</b> feed. This ensures that your inventory is up to date.</span></p><h3><b>Downloading feed files </b></h3>             <p><span class="tablenote"><b>Note: </b> Filters are applied to the feed files. For details, see <a href="/api-docs/buy/static/api-feed.html#feed-filters">Feed File Filters</a>. When curating the items returned, be sure to code as if these filters are not applied as they can be changed or removed in the future.</span></p><p>Priority Item feed files are binary gzip files. If the file is larger than 100 MB, the download must be streamed in chunks. You specify the size of the chunks in bytes using the <a href="#range-header">Range</a> request header. The <a href="#content-range">Content-range</a> response header indicates where in the full resource this partial chunk of data belongs  and the total number of bytes in the file.       For more information about using these headers, see <a href="/api-docs/buy/static/api-feed_beta.html#retrv-gzip">Retrieving a gzip feed file</a>.    </p>    <p>In addition to the API, there is an open source <a href="https://github.com/eBay/FeedSDK" target="_blank">Feed SDK</a> written in Java that downloads, combines files into a single file when needed, and unzips the entire feed file. It also lets you specify field filters to curate the items in the file.</p>              <p><span class="tablenote">  <b> Note:</b>  A successful call will always return a TSV.GZIP file; however, unsuccessful calls generate errors that are returned in JSON format. For documentation purposes, the successful call response is shown below as JSON fields so that the value returned in each column can be explained. The order of the response fields shows the order of the columns in the feed file.</span>  </p>                <h3><b>Restrictions </b></h3>                <p>For a list of supported sites and other restrictions, see <a href="/api-docs/buy/feed/overview.html#API">API Restrictions</a>.</p> |

## Enhanced Skill Content
## Question Mapping

- "How do I get a bulk feed of all active items in a category?" -> GET /item
- "How do I download items listed today in a specific marketplace?" -> GET /item
- "How do I get item group (variant) data for a category?" -> GET /item_group
- "How do I find multi-variant listings like color/size options?" -> GET /item_group
- "How do I get a full snapshot of items on a specific date?" -> GET /item_snapshot
- "How do I compare item data between two dates?" -> GET /item_snapshot (call twice, diff results)
- "How do I get price-reduced or priority items in a category?" -> GET /item_priority
- "How do I download a large feed file in chunks?" -> GET /item (or any endpoint, use Range header)
- "How do I check if a feed exists before downloading?" -> GET /item (check for 204 vs 200/206)
- "How do I get newly listed items since a specific date?" -> GET /item with feed_scope=NEWLY_LISTED and date param
- "What marketplaces can I pull feeds from?" -> Any endpoint, set X-EBAY-C-MARKETPLACE-ID (e.g., EBAY_US, EBAY_GB)
- "How do I get daily deal or priority listings?" -> GET /item_priority with date param
- "How do I resume a failed feed download?" -> GET /item (reissue with updated Range header)

## Response Tips

- **Item & Item Group feeds**: 200 returns the full file; 206 means partial content (check Content-Range header for byte offsets and total size). 204 means no data exists for that category/date/scope combination -- do not retry, adjust parameters instead.
- **Item Snapshot**: Response is a point-in-time dump; snapshot_date must be a valid past date. 204 means no snapshot was generated for that date.
- **Item Priority**: Always requires date; returns only items flagged for priority (deals, price drops). Expect smaller response bodies than /item.
- **All endpoints**: Feed files are gzipped TSV. Set `Accept: application/gzip`. Error 416 means the Range header is unsatisfiable (requested bytes beyond file size). Error 409 indicates a feed file is still being generated -- wait and retry.

## Anomaly Flags

- **204 No Content on expected feeds**: Surface when a category that previously returned data now returns empty -- may indicate category ID changes or feed generation issues.
- **409 Conflict responses**: Feed file is still being generated. Agent should flag this and suggest retrying after a delay rather than looping immediately.
- **416 Range Not Satisfiable**: The requested byte range exceeds the file size. Agent should recalculate the Range header using the Content-Range from the previous 206 response.
- **403 Forbidden**: OAuth2 token may be expired or the application lacks Buy Feed API scope. Surface token refresh guidance proactively.
- **Repeated 500 errors**: eBay server-side issue. Agent should flag for user awareness rather than retrying indefinitely.
- **Missing date parameter on /item**: Without date, returns the bootstrap file (very large). Agent should warn when date is omitted to avoid unintentionally large downloads.

## Playbook

### 1. Bootstrap a Category Feed (First-Time Full Download)

1. Authenticate via OAuth2 and obtain a valid access token.
2. Call `GET /item` with `feed_scope=ALL_ACTIVE`, `category_id`, marketplace header, and `Range: bytes=0-10485760`.
3. If response is 206, read the `Content-Range` header to get total file size.
4. Loop: increment the Range offset by chunk size and repeat until you receive 200 (final chunk) or the full range is covered.
5. Decompress the gzipped response and parse the TSV data.

### 2. Daily Incremental Sync

1. Call `GET /item` with `feed_scope=NEWLY_LISTED`, `category_id`, `date` set to today's date, and appropriate Range header.
2. If 204, no new items since last sync -- stop.
3. Download in chunks if 206, as in the bootstrap playbook.
4. Call `GET /item_priority` with the same `category_id` and `date` to capture price changes and deals.
5. Merge incremental results with your local dataset, updating changed items and appending new ones.

### 3. Download Item Group (Variant) Data

1. Call `GET /item_group` with `feed_scope=NEWLY_LISTED` (or `ALL_ACTIVE`), `category_id`, and marketplace header.
2. If 204, no group data exists for this category -- some categories have no multi-variant listings.
3. Download in chunks using Range header if the response is 206.
4. Parse the TSV to extract parent-child item relationships, variant attributes (size, color), and group pricing.

### 4. Point-in-Time Snapshot Comparison

1. Call `GET /item_snapshot` with `category_id`, `snapshot_date` set to the earlier date, and Range header.
2. Download and store the full snapshot.
3. Repeat with `snapshot_date` set to the later date.
4. Diff the two snapshots to identify added, removed, and changed items between the two dates.

### 5. Handling Download Failures and Resumption

1. Track the last successfully received byte offset from the `Content-Range` header.
2. On failure (network error, timeout), reissue the request with `Range: bytes={last_offset+1}-{last_offset+chunk_size}`.
3. If you receive 416, the file has been regenerated with a different size -- restart from `Range: bytes=0-...` to get the new version.
4. If you receive 409, the feed is being regenerated -- wait 10-15 minutes before retrying.


## Response Tips
- Check response schemas in references/api-spec.lap for field details

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
