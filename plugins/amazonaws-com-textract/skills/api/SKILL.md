---
name: amazon-textract
description: "Amazon Textract API skill. Use when working with Amazon Textract for root. Covers 25 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Textract
API version: 2018-06-27

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

25 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Analyzes an input document for relationships between detected items.  The types of information returned are as follows:    Form data (key-value pairs). The related information is returned in two Block objects, each of type KEY_VALUE_SET: a KEY Block object and a VALUE Block object. For example, Name: Ana Silva Carolina contains a key and value. Name: is the key. Ana Silva Carolina is the value.   Table and table cell data. A TABLE Block object contains information about a detected table. A CELL Block object is returned for each cell in a table.   Lines and words of text. A LINE Block object contains one or more WORD Block objects. All lines and words that are detected in the document are returned (including text that doesn't have a relationship with the value of FeatureTypes).    Signatures. A SIGNATURE Block object contains the location information of a signature in a document. If used in conjunction with forms or tables, a signature can be given a Key-Value pairing or be detected in the cell of a table.   Query. A QUERY Block object contains the query text, alias and link to the associated Query results block object.   Query Result. A QUERY_RESULT Block object contains the answer to the query and an ID that connects it to the query asked. This Block also contains a confidence score.   Selection elements such as check boxes and option buttons (radio buttons) can be detected in form data and in tables. A SELECTION_ELEMENT Block object contains information about a selection element, including the selection status. You can choose which type of analysis to perform by specifying the FeatureTypes list.  The output is returned in a list of Block objects.  AnalyzeDocument is a synchronous operation. To analyze documents asynchronously, use StartDocumentAnalysis. For more information, see Document Text Analysis. |
| POST | / | AnalyzeExpense synchronously analyzes an input document for financially related relationships between text. Information is returned as ExpenseDocuments and seperated as follows:    LineItemGroups- A data set containing LineItems which store information about the lines of text, such as an item purchased and its price on a receipt.    SummaryFields- Contains all other information a receipt, such as header information or the vendors name. |
| POST | / | Analyzes identity documents for relevant information. This information is extracted and returned as IdentityDocumentFields, which records both the normalized field and value of the extracted text. Unlike other Amazon Textract operations, AnalyzeID doesn't return any Geometry data. |
| POST | / | Creates an adapter, which can be fine-tuned for enhanced performance on user provided documents. Takes an AdapterName and FeatureType. Currently the only supported feature type is QUERIES. You can also provide a Description, Tags, and a ClientRequestToken. You can choose whether or not the adapter should be AutoUpdated with the AutoUpdate argument. By default, AutoUpdate is set to DISABLED. |
| POST | / | Creates a new version of an adapter. Operates on a provided AdapterId and a specified dataset provided via the DatasetConfig argument. Requires that you specify an Amazon S3 bucket with the OutputConfig argument. You can provide an optional KMSKeyId, an optional ClientRequestToken, and optional tags. |
| POST | / | Deletes an Amazon Textract adapter. Takes an AdapterId and deletes the adapter specified by the ID. |
| POST | / | Deletes an Amazon Textract adapter version. Requires that you specify both an AdapterId and a AdapterVersion. Deletes the adapter version specified by the AdapterId and the AdapterVersion. |
| POST | / | Detects text in the input document. Amazon Textract can detect lines of text and the words that make up a line of text. The input document must be in one of the following image formats: JPEG, PNG, PDF, or TIFF. DetectDocumentText returns the detected text in an array of Block objects.  Each document page has as an associated Block of type PAGE. Each PAGE Block object is the parent of LINE Block objects that represent the lines of detected text on a page. A LINE Block object is a parent for each word that makes up the line. Words are represented by Block objects of type WORD.  DetectDocumentText is a synchronous operation. To analyze documents asynchronously, use StartDocumentTextDetection. For more information, see Document Text Detection. |
| POST | / | Gets configuration information for an adapter specified by an AdapterId, returning information on AdapterName, Description, CreationTime, AutoUpdate status, and FeatureTypes. |
| POST | / | Gets configuration information for the specified adapter version, including: AdapterId, AdapterVersion, FeatureTypes, Status, StatusMessage, DatasetConfig, KMSKeyId, OutputConfig, Tags and EvaluationMetrics. |
| POST | / | Gets the results for an Amazon Textract asynchronous operation that analyzes text in a document. You start asynchronous text analysis by calling StartDocumentAnalysis, which returns a job identifier (JobId). When the text analysis operation finishes, Amazon Textract publishes a completion status to the Amazon Simple Notification Service (Amazon SNS) topic that's registered in the initial call to StartDocumentAnalysis. To get the results of the text-detection operation, first check that the status value published to the Amazon SNS topic is SUCCEEDED. If so, call GetDocumentAnalysis, and pass the job identifier (JobId) from the initial call to StartDocumentAnalysis.  GetDocumentAnalysis returns an array of Block objects. The following types of information are returned:    Form data (key-value pairs). The related information is returned in two Block objects, each of type KEY_VALUE_SET: a KEY Block object and a VALUE Block object. For example, Name: Ana Silva Carolina contains a key and value. Name: is the key. Ana Silva Carolina is the value.   Table and table cell data. A TABLE Block object contains information about a detected table. A CELL Block object is returned for each cell in a table.   Lines and words of text. A LINE Block object contains one or more WORD Block objects. All lines and words that are detected in the document are returned (including text that doesn't have a relationship with the value of the StartDocumentAnalysis FeatureTypes input parameter).    Query. A QUERY Block object contains the query text, alias and link to the associated Query results block object.   Query Results. A QUERY_RESULT Block object contains the answer to the query and an ID that connects it to the query asked. This Block also contains a confidence score.    While processing a document with queries, look out for INVALID_REQUEST_PARAMETERS output. This indicates that either the per page query limit has been exceeded or that the operation is trying to query a page in the document which doesn’t exist.   Selection elements such as check boxes and option buttons (radio buttons) can be detected in form data and in tables. A SELECTION_ELEMENT Block object contains information about a selection element, including the selection status. Use the MaxResults parameter to limit the number of blocks that are returned. If there are more results than specified in MaxResults, the value of NextToken in the operation response contains a pagination token for getting the next set of results. To get the next page of results, call GetDocumentAnalysis, and populate the NextToken request parameter with the token value that's returned from the previous call to GetDocumentAnalysis. For more information, see Document Text Analysis. |
| POST | / | Gets the results for an Amazon Textract asynchronous operation that detects text in a document. Amazon Textract can detect lines of text and the words that make up a line of text. You start asynchronous text detection by calling StartDocumentTextDetection, which returns a job identifier (JobId). When the text detection operation finishes, Amazon Textract publishes a completion status to the Amazon Simple Notification Service (Amazon SNS) topic that's registered in the initial call to StartDocumentTextDetection. To get the results of the text-detection operation, first check that the status value published to the Amazon SNS topic is SUCCEEDED. If so, call GetDocumentTextDetection, and pass the job identifier (JobId) from the initial call to StartDocumentTextDetection.  GetDocumentTextDetection returns an array of Block objects.  Each document page has as an associated Block of type PAGE. Each PAGE Block object is the parent of LINE Block objects that represent the lines of detected text on a page. A LINE Block object is a parent for each word that makes up the line. Words are represented by Block objects of type WORD. Use the MaxResults parameter to limit the number of blocks that are returned. If there are more results than specified in MaxResults, the value of NextToken in the operation response contains a pagination token for getting the next set of results. To get the next page of results, call GetDocumentTextDetection, and populate the NextToken request parameter with the token value that's returned from the previous call to GetDocumentTextDetection. For more information, see Document Text Detection. |
| POST | / | Gets the results for an Amazon Textract asynchronous operation that analyzes invoices and receipts. Amazon Textract finds contact information, items purchased, and vendor name, from input invoices and receipts. You start asynchronous invoice/receipt analysis by calling StartExpenseAnalysis, which returns a job identifier (JobId). Upon completion of the invoice/receipt analysis, Amazon Textract publishes the completion status to the Amazon Simple Notification Service (Amazon SNS) topic. This topic must be registered in the initial call to StartExpenseAnalysis. To get the results of the invoice/receipt analysis operation, first ensure that the status value published to the Amazon SNS topic is SUCCEEDED. If so, call GetExpenseAnalysis, and pass the job identifier (JobId) from the initial call to StartExpenseAnalysis. Use the MaxResults parameter to limit the number of blocks that are returned. If there are more results than specified in MaxResults, the value of NextToken in the operation response contains a pagination token for getting the next set of results. To get the next page of results, call GetExpenseAnalysis, and populate the NextToken request parameter with the token value that's returned from the previous call to GetExpenseAnalysis. For more information, see Analyzing Invoices and Receipts. |
| POST | / | Gets the results for an Amazon Textract asynchronous operation that analyzes text in a lending document.  You start asynchronous text analysis by calling StartLendingAnalysis, which returns a job identifier (JobId). When the text analysis operation finishes, Amazon Textract publishes a completion status to the Amazon Simple Notification Service (Amazon SNS) topic that's registered in the initial call to StartLendingAnalysis.  To get the results of the text analysis operation, first check that the status value published to the Amazon SNS topic is SUCCEEDED. If so, call GetLendingAnalysis, and pass the job identifier (JobId) from the initial call to StartLendingAnalysis. |
| POST | / | Gets summarized results for the StartLendingAnalysis operation, which analyzes text in a lending document. The returned summary consists of information about documents grouped together by a common document type. Information like detected signatures, page numbers, and split documents is returned with respect to the type of grouped document.  You start asynchronous text analysis by calling StartLendingAnalysis, which returns a job identifier (JobId). When the text analysis operation finishes, Amazon Textract publishes a completion status to the Amazon Simple Notification Service (Amazon SNS) topic that's registered in the initial call to StartLendingAnalysis.  To get the results of the text analysis operation, first check that the status value published to the Amazon SNS topic is SUCCEEDED. If so, call GetLendingAnalysisSummary, and pass the job identifier (JobId) from the initial call to StartLendingAnalysis. |
| POST | / | List all version of an adapter that meet the specified filtration criteria. |
| POST | / | Lists all adapters that match the specified filtration criteria. |
| POST | / | Lists all tags for an Amazon Textract resource. |
| POST | / | Starts the asynchronous analysis of an input document for relationships between detected items such as key-value pairs, tables, and selection elements.  StartDocumentAnalysis can analyze text in documents that are in JPEG, PNG, TIFF, and PDF format. The documents are stored in an Amazon S3 bucket. Use DocumentLocation to specify the bucket name and file name of the document.   StartDocumentAnalysis returns a job identifier (JobId) that you use to get the results of the operation. When text analysis is finished, Amazon Textract publishes a completion status to the Amazon Simple Notification Service (Amazon SNS) topic that you specify in NotificationChannel. To get the results of the text analysis operation, first check that the status value published to the Amazon SNS topic is SUCCEEDED. If so, call GetDocumentAnalysis, and pass the job identifier (JobId) from the initial call to StartDocumentAnalysis. For more information, see Document Text Analysis. |
| POST | / | Starts the asynchronous detection of text in a document. Amazon Textract can detect lines of text and the words that make up a line of text.  StartDocumentTextDetection can analyze text in documents that are in JPEG, PNG, TIFF, and PDF format. The documents are stored in an Amazon S3 bucket. Use DocumentLocation to specify the bucket name and file name of the document.   StartTextDetection returns a job identifier (JobId) that you use to get the results of the operation. When text detection is finished, Amazon Textract publishes a completion status to the Amazon Simple Notification Service (Amazon SNS) topic that you specify in NotificationChannel. To get the results of the text detection operation, first check that the status value published to the Amazon SNS topic is SUCCEEDED. If so, call GetDocumentTextDetection, and pass the job identifier (JobId) from the initial call to StartDocumentTextDetection. For more information, see Document Text Detection. |
| POST | / | Starts the asynchronous analysis of invoices or receipts for data like contact information, items purchased, and vendor names.  StartExpenseAnalysis can analyze text in documents that are in JPEG, PNG, and PDF format. The documents must be stored in an Amazon S3 bucket. Use the DocumentLocation parameter to specify the name of your S3 bucket and the name of the document in that bucket.   StartExpenseAnalysis returns a job identifier (JobId) that you will provide to GetExpenseAnalysis to retrieve the results of the operation. When the analysis of the input invoices/receipts is finished, Amazon Textract publishes a completion status to the Amazon Simple Notification Service (Amazon SNS) topic that you provide to the NotificationChannel. To obtain the results of the invoice and receipt analysis operation, ensure that the status value published to the Amazon SNS topic is SUCCEEDED. If so, call GetExpenseAnalysis, and pass the job identifier (JobId) that was returned by your call to StartExpenseAnalysis. For more information, see Analyzing Invoices and Receipts. |
| POST | / | Starts the classification and analysis of an input document. StartLendingAnalysis initiates the classification and analysis of a packet of lending documents. StartLendingAnalysis operates on a document file located in an Amazon S3 bucket.  StartLendingAnalysis can analyze text in documents that are in one of the following formats: JPEG, PNG, TIFF, PDF. Use DocumentLocation to specify the bucket name and the file name of the document.   StartLendingAnalysis returns a job identifier (JobId) that you use to get the results of the operation. When the text analysis is finished, Amazon Textract publishes a completion status to the Amazon Simple Notification Service (Amazon SNS) topic that you specify in NotificationChannel. To get the results of the text analysis operation, first check that the status value published to the Amazon SNS topic is SUCCEEDED. If the status is SUCCEEDED you can call either GetLendingAnalysis or GetLendingAnalysisSummary and provide the JobId to obtain the results of the analysis. If using OutputConfig to specify an Amazon S3 bucket, the output will be contained within the specified prefix in a directory labeled with the job-id. In the directory there are 3 sub-directories:    detailedResponse (contains the GetLendingAnalysis response)   summaryResponse (for the GetLendingAnalysisSummary response)   splitDocuments (documents split across logical boundaries) |
| POST | / | Adds one or more tags to the specified resource. |
| POST | / | Removes any tags with the specified keys from the specified resource. |
| POST | / | Update the configuration for an adapter. FeatureTypes configurations cannot be updated. At least one new parameter must be specified as an argument. |

## Enhanced Skill Content
## Question Mapping

- "How do I extract text from a single-page document?" -> POST / (DetectDocumentText: Document)
- "How do I analyze a document for tables and forms?" -> POST / (AnalyzeDocument: Document + FeatureTypes)
- "How do I process a receipt or invoice?" -> POST / (AnalyzeExpense: Document)
- "How do I extract data from an ID card or passport?" -> POST / (AnalyzeID: DocumentPages)
- "How do I process a large multi-page PDF stored in S3?" -> POST / (StartDocumentAnalysis: DocumentLocation + FeatureTypes)
- "How do I check if my async document job is done?" -> POST / (GetDocumentAnalysis: JobId)
- "How do I analyze lending documents like mortgage applications?" -> POST / (StartLendingAnalysis: DocumentLocation)
- "How do I get a summary of classified lending documents?" -> POST / (GetLendingAnalysisSummary: JobId)
- "How do I create a custom adapter for specialized documents?" -> POST / (CreateAdapter: AdapterName + FeatureTypes)
- "How do I train a new version of my adapter?" -> POST / (CreateAdapterVersion: AdapterId + DatasetConfig + OutputConfig)
- "How do I list all my custom adapters?" -> POST / (ListAdapters)
- "How do I check the training status of an adapter version?" -> POST / (GetAdapterVersion: AdapterId + AdapterVersion)
- "How do I tag a Textract resource for cost tracking?" -> POST / (TagResource: ResourceARN + Tags)
- "How do I paginate through async job results?" -> POST / (GetDocumentAnalysis: JobId + NextToken + MaxResults)
- "How do I use queries to ask specific questions about a document?" -> POST / (AnalyzeDocument: Document + FeatureTypes + QueriesConfig)

## Response Tips

- **Sync document operations** (AnalyzeDocument, DetectDocumentText, AnalyzeExpense, AnalyzeID): Results return immediately in `Blocks` or `ExpenseDocuments` arrays; `DocumentMetadata.Pages` tells you total page count.
- **Async job operations** (Get*): Always check `JobStatus` first -- only parse `Blocks`/`Results` when status is `SUCCEEDED`; use `NextToken` to paginate through large result sets.
- **Start* operations**: Return only a `JobId` string; poll the corresponding Get* endpoint until `JobStatus` leaves `IN_PROGRESS`.
- **Adapter operations**: `Status` field on adapter versions tracks training progress (`CREATION_IN_PROGRESS`, `CREATION_SUCCESSFUL`, `CREATION_ERROR`); check `EvaluationMetrics` for accuracy data.
- **List operations**: All support `MaxResults` + `NextToken` pagination and optional timestamp filters (`AfterCreationTime`, `BeforeCreationTime`).
- **Tag operations**: TagResource and UntagResource return no body on success; ListTagsForResource returns a `Tags` map.

## Anomaly Flags

- **Job stuck in IN_PROGRESS**: Surface if polling GetDocumentAnalysis/GetDocumentTextDetection returns `IN_PROGRESS` for more than 5 minutes on a small document.
- **Warnings array present**: Any non-empty `Warnings` array in async results indicates pages that could not be processed -- always surface these to the user.
- **HumanLoopActivationOutput populated**: When AnalyzeDocument triggers a Human Loop (A2I), flag that results require human review before use.
- **StatusMessage on failure**: When `JobStatus` is `FAILED` or adapter `Status` is `CREATION_ERROR`, surface `StatusMessage` immediately -- it contains the root cause.
- **Empty Blocks/Results**: A successful response with an empty or missing `Blocks` array likely means the document is blank, encrypted, or unsupported format.
- **Throttling (429/TooManyRequestsException)**: AWS Textract has per-account TPS limits; surface when hitting rate limits and suggest reducing concurrency or requesting a quota increase.
- **Adapter AutoUpdate value**: Flag if an adapter has `AutoUpdate` set to a non-default value, as this affects model behavior over time.

## Playbook

### 1. Extract Tables and Forms from a Multi-Page S3 Document

1. Call StartDocumentAnalysis with `DocumentLocation` pointing to your S3 bucket/key and `FeatureTypes: ["TABLES", "FORMS"]`.
2. Capture the returned `JobId`.
3. Poll GetDocumentAnalysis with the `JobId` every 5 seconds.
4. When `JobStatus` is `SUCCEEDED`, collect all `Blocks` from the response.
5. If `NextToken` is present, continue calling GetDocumentAnalysis with the token until all pages are retrieved.
6. Check the `Warnings` array for any pages that failed processing.

### 2. Process Invoices and Receipts at Scale

1. Upload receipt/invoice files to an S3 bucket.
2. Call StartExpenseAnalysis with `DocumentLocation` for each file, optionally setting `NotificationChannel` to an SNS topic for completion callbacks.
3. When notified (or via polling GetExpenseAnalysis), retrieve `ExpenseDocuments` from the response.
4. Each `ExpenseDocument` contains structured line items and summary fields -- iterate through them for data extraction.
5. Paginate with `NextToken` if the document set is large.

### 3. Build and Deploy a Custom Adapter

1. Call CreateAdapter with a descriptive `AdapterName` and the relevant `FeatureTypes` (e.g., `["TABLES"]`).
2. Note the returned `AdapterId`.
3. Prepare a labeled dataset manifest in S3.
4. Call CreateAdapterVersion with the `AdapterId`, `DatasetConfig` pointing to the manifest, and an `OutputConfig` for training artifacts.
5. Poll GetAdapterVersion until `Status` is `CREATION_SUCCESSFUL`; review `EvaluationMetrics` for accuracy.
6. Use the adapter by passing `AdaptersConfig` in AnalyzeDocument or StartDocumentAnalysis calls.

### 4. Verify Identity Documents

1. Collect front and back images of the ID document.
2. Call AnalyzeID with `DocumentPages` containing both images as `Document` objects (S3 or base64 bytes).
3. Parse the returned `IdentityDocuments` array for extracted fields (name, DOB, document number, expiration).
4. Cross-reference extracted fields against your application requirements.

### 5. Async Text Detection with SNS Notifications

1. Create an SNS topic and IAM role granting Textract publish permissions.
2. Call StartDocumentTextDetection with `DocumentLocation`, and set `NotificationChannel` with the SNS topic ARN and role ARN.
3. Subscribe a Lambda or SQS queue to the SNS topic.
4. When the notification arrives, extract the `JobId` from the message.
5. Call GetDocumentTextDetection with the `JobId` to retrieve all detected `Blocks`.
6. Paginate with `NextToken` and `MaxResults` until all results are consumed.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
