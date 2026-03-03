---
name: feed-api
description: "Feed API skill. Use when working with Feed for order_task, inventory_task, schedule. Covers 23 endpoints."
version: 1.0.0
generator: lapsh
---

# Feed API
API version: v1.3.1

## Auth
OAuth2

## Base URL
https://api.ebay.com{basePath}

## Setup
1. Configure auth: OAuth2
2. GET /order_task -- verify access
3. POST /order_task -- create first order_task

## Endpoints

23 endpoints across 6 groups. See references/api-spec.lap for full details.

### order_task
| Method | Path | Description |
|--------|------|-------------|
| GET | /order_task | This method returns the details and status for an array of order tasks based on a specified <strong>feed_type</strong> or <strong>schedule_id</strong>. Specifying both <strong>feed_type</strong> and <strong>schedule_id</strong> results in an error. Since schedules are based on feed types, you can specify a schedule (<strong>schedule_id</strong>) that returns the needed <strong>feed_type</strong>.<br /><br />If specifying the <strong>feed_type</strong>, limit which order tasks are returned by specifying filters such as the creation date range or period of time using <strong>look_back_days</strong>. <br /><br />If specifying a <strong>schedule_id</strong>, the schedule template (that the <strong>schedule_id</strong> is based on) determines which order tasks are returned (see <strong>schedule_id</strong> for additional information). Each <strong>schedule_id</strong> applies to one <strong>feed_type</strong>. |
| POST | /order_task | This method creates an order download task with filter criteria for the order report. When using this method, specify the <b> feedType</b>, <b> schemaVersion</b>, and <b> filterCriteria</b> for the report. The method returns the <b> location</b> response header containing the getOrderTask call URI to retrieve the order task you just created. The URL includes the eBay-assigned task ID, which you can use to reference the order task. <br /><br />To retrieve the status of the task, use the <b>getOrderTask</b> method to retrieve a single task ID or the <b>getOrderTasks</b> method to retrieve multiple order task IDs.<p> <span class="tablenote"><strong>Note:</strong> The scope depends on the feed type. An error message results when an unsupported scope or feed type is specified.</span></p><p>The following list contains this method's authorization scope and its corresponding feed type:<ul><li>https://api.ebay.com/oauth/api_scope/sell.fulfillment: LMS_ORDER_REPORT</li></ul> </p><p>For details about how this method is used, see <a href="/api-docs/sell/static/feed/general-feed-tasks.html" target="_blank">General feed types</a> in the Selling Integration Guide. <p> <span class="tablenote"><strong>Note:</strong> At this time, the <strong>createOrderTask</strong> method only supports order creation date filters and not modified order date filters. Do not include the <strong>modifiedDateRange</strong> filter in your request payload.</span></p> |
| GET | /order_task/{task_id} | This method retrieves the task details and status of the specified task. The input is <strong>task_id</strong>. <p>For details about how this method is used, see <a href="/api-docs/sell/static/orders/generating-and-retrieving-order-reports.html">Working with Order Feeds</a> in the Selling Integration Guide.  </p> |

### inventory_task
| Method | Path | Description |
|--------|------|-------------|
| GET | /inventory_task | This method searches for multiple tasks of a specific feed type, and includes date filters and pagination. |
| POST | /inventory_task | This method creates an inventory-related download task for a specified feed type with optional filter criteria. When using this method, specify the <strong>feedType</strong>. <br/><br/>This method returns the location response header containing the <strong>getInventoryTask</strong> call URI to retrieve the inventory task you just created. The URL includes the eBay-assigned task ID, which you can use to reference the inventory task.<br/><br/>To retrieve the status of the task, use the <strong>getInventoryTask</strong> method to retrieve a single task ID or the <strong>getInventoryTasks</strong> method to retrieve multiple task IDs.<p> <span class="tablenote"><strong>Note:</strong> The scope depends on the feed type. An error message results when an unsupported scope or feed type is specified.</span></p>Presently, this method supports Active Inventory Report. The <strong>ActiveInventoryReport</strong> returns a report that contains price and quantity information for all of the active listings for a specific seller. A seller can use this information to maintain their inventory on eBay. |
| GET | /inventory_task/{task_id} | This method retrieves the task details and status of the specified inventory-related task. The input is <strong>task_id</strong>. |

### schedule
| Method | Path | Description |
|--------|------|-------------|
| GET | /schedule | This method retrieves an array containing the details and status of all schedules based on the specified <strong>feed_type</strong>. Use this method to find a schedule if you do not know the <strong>schedule_id</strong>. |
| POST | /schedule | This method creates a schedule, which is a subscription to the specified schedule template. A schedule periodically generates a report for the <strong>feedType</strong> specified by the template. Specify the same <strong>feedType</strong> as the <strong>feedType</strong> of the associated schedule template. When creating the schedule, if available from the template, you can specify a preferred trigger hour, day of the week, or day of the month. These and other fields are conditionally available as specified by the template.<p> <span class="tablenote"><strong>Note:</strong> Make sure to include all fields required by the schedule template (<strong>scheduleTemplateId</strong>). Call the <strong>getScheduleTemplate</strong> method (or the <strong>getScheduleTemplates</strong> method), to find out which fields are required or optional. If a field is optional and a default value is provided by the template, the default value will be used if omitted from the payload.</span></p>A successful call returns the location response header containing the <strong>getSchedule</strong> call URI to retrieve the schedule you just created. The URL includes the eBay-assigned schedule ID, which you can use to reference the schedule task. <br /><br />To retrieve the details of the create schedule task, use the <strong>getSchedule</strong> method for a single schedule ID or the <strong>getSchedules</strong> method to retrieve all schedule details for the specified <strong>feed_type</strong>. The number of schedules for each feedType is limited. Error code 160031 is returned when you have reached this maximum.<p> <span class="tablenote"><strong>Note:</strong> Except for schedules with a HALF-HOUR frequency, all schedules will ideally run at the start of each hour ('00' minutes). Actual start time may vary time may vary due to load and other factors.</span></p> |
| GET | /schedule/{schedule_id} | This method retrieves schedule details and status of the specified schedule. Specify the schedule to retrieve using the <strong>schedule_id</strong>. Use the <strong>getSchedules</strong> method to find a schedule if you do not know the <strong>schedule_id</strong>. |
| PUT | /schedule/{schedule_id} | This method updates an existing schedule. Specify the schedule to update using the <strong>schedule_id</strong> path parameter. If the schedule template has changed after the schedule was created or updated, the input will be validated using the changed template.<p> <span class="tablenote"><strong>Note:</strong> Make sure to include all fields required by the schedule template (<strong>scheduleTemplateId</strong>). Call the <strong>getScheduleTemplate</strong> method (or the <strong>getScheduleTemplates</strong> method), to find out which fields are required or optional. If you do not know the <strong>scheduleTemplateId</strong>, call the <strong>getSchedule</strong> method to find out.</span></p> |
| DELETE | /schedule/{schedule_id} | This method deletes an existing schedule. Specify the schedule to delete using the <strong>schedule_id</strong> path parameter. |
| GET | /schedule/{schedule_id}/download_result_file | This method downloads the latest Order Report generated by the schedule. The response of this call is a compressed or uncompressed CSV, XML, or JSON file, with the applicable file extension (for example: csv.gz). Specify the <strong>schedule_id</strong> path parameter to download its last generated file. |

### schedule_template
| Method | Path | Description |
|--------|------|-------------|
| GET | /schedule_template/{schedule_template_id} | This method retrieves the details of the specified template. Specify the template to retrieve using the <strong>schedule_template_id</strong> path parameter. Use the <strong>getScheduleTemplates</strong> method to find a schedule template if you do not know the <strong>schedule_template_id</strong>. |
| GET | /schedule_template | This method retrieves an array containing the details and status of all schedule templates based on the specified <strong>feed_type</strong>. Use this method to find a schedule template if you do not know the <strong>schedule_template_id</strong>. |

### task
| Method | Path | Description |
|--------|------|-------------|
| GET | /task | This method returns the details and status for an array of tasks based on a specified <strong>feed_type</strong> or <strong>schedule_id</strong>. Specifying both <strong>feed_type</strong> and <strong>schedule_id</strong> results in an error. Since schedules are based on feed types, you can specify a schedule (<strong>schedule_id</strong>) that returns the needed <strong>feed_type</strong>.<br /><br />If specifying the <strong>feed_type</strong>, limit which tasks are returned by specifying filters, such as the creation date range or period of time using <strong>look_back_days</strong>. Also, by specifying the <strong>feed_type</strong>, both on-demand and scheduled reports are returned.<br /><br />If specifying a <strong>schedule_id</strong>, the schedule template (that the schedule ID is based on) determines which tasks are returned (see <strong>schedule_id</strong> for additional information). Each <strong>scheduledId</strong> applies to one <strong>feed_type</strong>. |
| POST | /task | This method creates an upload task or a download task without filter criteria. When using this method, specify the <b> feedType</b> and the feed file <b> schemaVersion</b>. The feed type specified sets the task as a download or an upload task.  <p>For details about the upload and download flows, see <a href="/api-docs/sell/static/orders/generating-and-retrieving-order-reports.html">Working with Order Feeds</a> in the Selling Integration Guide.</p><p> <span class="tablenote"><strong>Note:</strong> The scope depends on the feed type. An error message results when an unsupported scope or feed type is specified.</span></p><p>The following list contains this method's authorization scopes and their corresponding feed types:</p><ul><li>https://api.ebay.com/oauth/api_scope/sell.inventory: See <a href="/api-docs/sell/static/feed/lms-feeds-quick-reference.html#Availabl" target="_blank">LMS FeedTypes</a></li><li>https://api.ebay.com/oauth/api_scope/sell.fulfillment: LMS_ORDER_ACK (specify for upload tasks). Also see <a href="/api-docs/sell/static/feed/lms-feeds-quick-reference.html#Availabl" target="_blank">LMS FeedTypes</a></li><li>https://api.ebay.com/oauth/api_scope/sell.marketing: None*</li><li>https://api.ebay.com/oauth/api_scope/commerce.catalog.readonly: None*</li></ul><p>* Reserved for future release</p> |
| GET | /task/{task_id}/download_input_file | This method downloads the file previously uploaded using <strong>uploadFile</strong>. Specify the task_id from the <strong>uploadFile</strong> call. <p><span class="tablenote"><strong>Note:</strong> With respect to LMS, this method applies to all feed types except <code>LMS_ORDER_REPORT</code> and <code>LMS_ACTIVE_INVENTORY_REPORT</code>. See <a href="/api-docs/sell/static/feed/lms-feeds.html">LMS API Feeds</a> in the Selling Integration Guide.</span></p> |
| GET | /task/{task_id}/download_result_file | This method retrieves the generated file that is associated with the specified task ID. The response of this call is a compressed or uncompressed CSV, XML, or JSON file, with the applicable file extension (for example: csv.gz). <p>For details about how this method is used, see <a href="/api-docs/sell/static/orders/generating-and-retrieving-order-reports.html">Working with Order Feeds</a> in the Selling Integration Guide. </p><p><span class="tablenote"><strong>Note:</strong> The status of the task to retrieve must be in the COMPLETED or COMPLETED_WITH_ERROR state before this method can retrieve the file. You can use the getTask or getTasks method to retrieve the status of the task.</span></p> |
| GET | /task/{task_id} | This method retrieves the details and status of the specified task. The input is <strong>task_id</strong>. <br /><br />For details of how this method is used, see <a href="/api-docs/sell/static/orders/generating-and-retrieving-order-reports.html">Working with Order Feeds</a> in the Selling Integration Guide. |
| POST | /task/{task_id}/upload_file | This method associates the specified file with the specified task ID and uploads the input file. After the file has been uploaded, the processing of the file begins. <br><br>Reports often take time to generate and it's common for this method to return an HTTP status of 202, which indicates the report is being generated. Use the <b> getTask</b> with the task ID or <b> getTasks</b> to determine the status of a report. <br><br>The status flow is <code>QUEUED</code> &gt; <code>IN_PROCESS</code> &gt; <code>COMPLETED</code> or <code>COMPLETED_WITH_ERROR</code>. When the status is <code>COMPLETED</code> or <code>COMPLETED_WITH_ERROR</code>, this indicates the file has been processed and the order report can be downloaded. If there are errors, they will be indicated in the report file. <br /><br />For details of how this method is used in the upload flow, see <a href="/api-docs/sell/static/orders/generating-and-retrieving-order-reports.html">Working with Order Feeds</a> in the Selling Integration Guide. <br><br>This call does not have a JSON Request payload but uploads the file as form-data. For example:<br /> <pre> fileName: &quot;AddFixedPriceItem_Macbook.xml&quot; <br /> name: &quot;file&quot; <br /> type: &quot;form-data&quot; <br /> file: @&quot;/C:/Users/.../AddFixedPriceItem_Macbook.7z&quot;</pre>See <a href="/api-docs/sell/feed/resources/task/methods/uploadFile#h2-samples">Samples</a> for information.<p><span class="tablenote"><strong>Note:</strong> This method applies to all <a href="/api-docs/sell/static/feed/fx-feeds-quick-reference.html#availabl" target="_blank">Seller Hub feed types</a>, and to all <a href="/api-docs/sell/static/feed/lms-feeds-quick-reference.html#Availabl" target="_blank">LMS feed types</a> except <code>LMS_ORDER_REPORT</code> and <code>LMS_ACTIVE_INVENTORY_REPORT</code>.</span></p><p> <span class="tablenote"><b>Note:</b> You must use a <strong>Content-Type</strong> header with its value set to "<strong>multipart/form-data</strong>". See <a href="/api-docs/sell/feed/resources/task/methods/uploadFile#h2-samples">Samples</a> for information.</span></p><p><span class="tablenote"><b>Note:</b> For LMS feed types, upload a regular XML file or an XML file in zipped format (both formats are allowed).</span></p> |

### customer_service_metric_task
| Method | Path | Description |
|--------|------|-------------|
| GET | /customer_service_metric_task | Use this method to return an array of customer service metric tasks. You can limit the tasks returned by specifying a date range. </p> <p> <span class="tablenote"><strong>Note:</strong> You can pass in either the <code>look_back_days </code>or<code> date_range</code>, but not both.</span></p> |
| POST | /customer_service_metric_task | <p>Use this method to create a customer service metrics download task with filter criteria for the customer service metrics report. When using this method, specify the <strong>feedType</strong> and <strong>filterCriteria</strong> including both <strong>evaluationMarketplaceId</strong> and <strong>customerServiceMetricType</strong> for the report. The method returns the location response header containing the call URI to use with <strong>getCustomerServiceMetricTask</strong> to retrieve status and details on the task.</p><p>Only CURRENT Customer Service Metrics reports can be generated with the Sell Feed API. PROJECTED reports are not supported at this time. See the <a href="/api-docs/sell/analytics/resources/customer_service_metric/methods/getCustomerServiceMetric">getCustomerServiceMetric</a> method document in the Analytics API for more information about these two types of reports.</p><p><span class="tablenote"><strong>Note:</strong> Before calling this API, retrieve the summary of the seller's performance and rating for the customer service metric by calling <strong>getCustomerServiceMetric</strong> (part of the <a href="/api-docs/sell/analytics/resources/methods">Analytics API</a>). You can then populate the create task request fields with the values from the response. This technique eliminates failed tasks that request a report for a <strong>customerServiceMetricType</strong> and <strong>evaluationMarketplaceId</strong> that are without evaluation.</span></p> |
| GET | /customer_service_metric_task/{task_id} | <p>Use this method to retrieve customer service metric task details for the specified task. The input is <strong>task_id</strong>.</p> |

## Enhanced Skill Content
## Question Mapping

- "How do I list my order feed tasks?" -> GET /order_task
- "How do I create a new order feed task with date filtering?" -> POST /order_task
- "What is the status of my order task?" -> GET /order_task/{task_id}
- "How do I list my inventory feed tasks?" -> GET /inventory_task
- "How do I create an inventory task filtered by listing format?" -> POST /inventory_task
- "How do I check if my inventory task finished?" -> GET /inventory_task/{task_id}
- "What feed schedules exist for a given feed type?" -> GET /schedule
- "How do I set up a recurring feed schedule?" -> POST /schedule
- "How do I change the trigger time on an existing schedule?" -> PUT /schedule/{schedule_id}
- "How do I cancel a feed schedule?" -> DELETE /schedule/{schedule_id}
- "How do I download the result file from a scheduled feed?" -> GET /schedule/{schedule_id}/download_result_file
- "What schedule templates are available for a feed type?" -> GET /schedule_template
- "How do I upload a file to a feed task?" -> POST /task/{task_id}/upload_file
- "How do I download the results of a completed task?" -> GET /task/{task_id}/download_result_file
- "How do I check my customer service metric tasks?" -> GET /customer_service_metric_task

## Response Tips

- **Task lists** (order_task, inventory_task, task, customer_service_metric_task): Paginated via `limit`/`offset`; use `next`/`prev` hrefs to navigate. `total` gives the full count. The `tasks` array contains maps -- always check array length before accessing.
- **Single task lookups**: Check `status` field for completion state before attempting file downloads. `uploadSummary.failureCount` and `successCount` tell you partial success outcomes.
- **Schedules**: `status` and `statusReason` on GET explain why a schedule may be inactive. 204 on PUT/DELETE means success with no body.
- **Schedule templates**: `supportedConfigurations` is an array of maps describing valid options -- iterate it to discover allowed trigger settings before creating a schedule.
- **File downloads**: 200 returns the raw file content (not JSON). Handle as binary/stream. No body schema is defined -- expect a file attachment.
- **Error responses**: All endpoints share 400 (bad input), 403 (auth/permission), 500 (server error). 404 appears on single-resource GETs. 409 on POSTs/PUTs means a conflicting resource already exists.

## Anomaly Flags

- **409 Conflict on task creation**: A task or schedule with the same parameters already exists. Surface this clearly -- the user likely needs to check existing tasks rather than retry.
- **Task stuck in non-complete status**: If `GET /order_task/{task_id}` or similar returns a status other than complete and `completionDate` is null after a long period, flag potential processing delays.
- **High failureCount in uploadSummary**: When `failureCount` exceeds `successCount`, proactively warn the user that most records in the feed failed processing and suggest downloading the result file for details.
- **Empty task lists with non-zero total**: If `tasks` array is empty but `total > 0`, the offset/limit combination is past the result set -- flag pagination misconfiguration.
- **Missing detailHref on completed tasks**: If a task is complete but `detailHref` is empty or null, the result file may not be available -- alert the user before they attempt a download.
- **Schedule statusReason populated**: When a schedule has a non-empty `statusReason`, surface it immediately as it usually indicates a problem (paused, failed template, expired).

## Playbook

### 1. Create and Monitor an Order Feed Task

1. Call `POST /order_task` with `feedType` and optional `filterCriteria` (date ranges, order status).
2. Capture the task ID from the 202 response Location header.
3. Poll `GET /order_task/{task_id}` until `status` indicates completion.
4. Check `uploadSummary.failureCount` -- if non-zero, investigate partial failures.
5. Use `detailHref` to download the completed feed file.

### 2. Set Up a Recurring Inventory Feed Schedule

1. Call `GET /schedule_template?feed_type=<type>` to discover available templates and supported configurations.
2. Pick a `scheduleTemplateId` from the results.
3. Call `POST /schedule` with `feedType`, `scheduleTemplateId`, trigger preferences (day/hour), and start/end dates.
4. Verify creation with `GET /schedule/{schedule_id}`.
5. Periodically call `GET /schedule/{schedule_id}/download_result_file` to retrieve outputs.

### 3. Upload and Process a Feed File

1. Call `POST /task` with `X-EBAY-C-MARKETPLACE-ID` header and `feedType` to create the task.
2. Capture the task ID from the 202 response.
3. Call `POST /task/{task_id}/upload_file` with `Content-Type` header and the file payload.
4. Poll `GET /task/{task_id}` until `status` shows completion.
5. Call `GET /task/{task_id}/download_result_file` to retrieve processing results and check for errors.

### 4. Review Customer Service Metrics

1. Call `POST /customer_service_metric_task` with `Accept-Language`, desired `feedType`, and `filterCriteria` (metric type, marketplace, categories, shipping regions).
2. Capture the task ID from the 202 response.
3. Poll `GET /customer_service_metric_task/{task_id}` until the task completes.
4. Use `detailHref` to access the resulting metrics file.

### 5. Manage and Update Feed Schedules

1. Call `GET /schedule?feed_type=<type>` to list all schedules for a feed type.
2. Identify the schedule to modify by `scheduleId`.
3. Call `PUT /schedule/{schedule_id}` with updated trigger preferences or date range. Expect 204 on success.
4. To deactivate, call `DELETE /schedule/{schedule_id}`. Expect 204 on success.
5. Confirm changes with `GET /schedule/{schedule_id}` and check `status`/`statusReason`.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- List endpoints may support pagination; check for limit, offset, or cursor params
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
