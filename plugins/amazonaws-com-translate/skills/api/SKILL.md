---
name: amazon-translate
description: "Amazon Translate API skill. Use when working with Amazon Translate for root. Covers 19 endpoints."
version: 1.0.0
generator: lapsh
---

# Amazon Translate
API version: 2017-07-01

## Auth
AWS SigV4

## Base URL
Not specified.

## Setup
1. Configure auth: AWS SigV4
3. POST / -- create first resource

## Endpoints

19 endpoints across 1 groups. See references/api-spec.lap for full details.

### root
| Method | Path | Description |
|--------|------|-------------|
| POST | / | Creates a parallel data resource in Amazon Translate by importing an input file from Amazon S3. Parallel data files contain examples that show how you want segments of text to be translated. By adding parallel data, you can influence the style, tone, and word choice in your translation output. |
| POST | / | Deletes a parallel data resource in Amazon Translate. |
| POST | / | A synchronous action that deletes a custom terminology. |
| POST | / | Gets the properties associated with an asynchronous batch translation job including name, ID, status, source and target languages, input/output S3 buckets, and so on. |
| POST | / | Provides information about a parallel data resource. |
| POST | / | Retrieves a custom terminology. |
| POST | / | Creates or updates a custom terminology, depending on whether one already exists for the given terminology name. Importing a terminology with the same name as an existing one will merge the terminologies based on the chosen merge strategy. The only supported merge strategy is OVERWRITE, where the imported terminology overwrites the existing terminology of the same name. If you import a terminology that overwrites an existing one, the new terminology takes up to 10 minutes to fully propagate. After that, translations have access to the new terminology. |
| POST | / | Provides a list of languages (RFC-5646 codes and names) that Amazon Translate supports. |
| POST | / | Provides a list of your parallel data resources in Amazon Translate. |
| POST | / | Lists all tags associated with a given Amazon Translate resource. For more information, see  Tagging your resources. |
| POST | / | Provides a list of custom terminologies associated with your account. |
| POST | / | Gets a list of the batch translation jobs that you have submitted. |
| POST | / | Starts an asynchronous batch translation job. Use batch translation jobs to translate large volumes of text across multiple documents at once. For batch translation, you can input documents with different source languages (specify auto as the source language). You can specify one or more target languages. Batch translation translates each input document into each of the target languages. For more information, see Asynchronous batch processing. Batch translation jobs can be described with the DescribeTextTranslationJob operation, listed with the ListTextTranslationJobs operation, and stopped with the StopTextTranslationJob operation. |
| POST | / | Stops an asynchronous batch translation job that is in progress. If the job's state is IN_PROGRESS, the job will be marked for termination and put into the STOP_REQUESTED state. If the job completes before it can be stopped, it is put into the COMPLETED state. Otherwise, the job is put into the STOPPED state. Asynchronous batch translation jobs are started with the StartTextTranslationJob operation. You can use the DescribeTextTranslationJob or ListTextTranslationJobs operations to get a batch translation job's JobId. |
| POST | / | Associates a specific tag with a resource. A tag is a key-value pair that adds as a metadata to a resource. For more information, see  Tagging your resources. |
| POST | / | Translates the input document from the source language to the target language. This synchronous operation supports text, HTML, or Word documents as the input document. TranslateDocument supports translations from English to any supported language, and from any supported language to English. Therefore, specify either the source language code or the target language code as “en” (English).   If you set the Formality parameter, the request will fail if the target language does not support formality. For a list of target languages that support formality, see Setting formality. |
| POST | / | Translates input text from the source language to the target language. For a list of available languages and language codes, see Supported languages. |
| POST | / | Removes a specific tag associated with an Amazon Translate resource. For more information, see  Tagging your resources. |
| POST | / | Updates a previously created parallel data resource by importing a new input file from Amazon S3. |

## Enhanced Skill Content
## Question Mapping

- "How do I translate text from English to Spanish?" -> POST / (TranslateText: Text, SourceLanguageCode, TargetLanguageCode)
- "How do I translate a document file?" -> POST / (TranslateDocument: Document, SourceLanguageCode, TargetLanguageCode)
- "What languages does Amazon Translate support?" -> POST / (ListLanguages)
- "How do I start a batch translation job?" -> POST / (StartTextTranslationJob: InputDataConfig, OutputDataConfig, DataAccessRoleArn, SourceLanguageCode, TargetLanguageCodes, ClientToken)
- "How do I check the status of my translation job?" -> POST / (DescribeTextTranslationJob: JobId)
- "How do I stop a running translation job?" -> POST / (StopTextTranslationJob: JobId)
- "How do I list all my batch translation jobs?" -> POST / (ListTextTranslationJobs, optional Filter)
- "How do I create a custom terminology?" -> POST / (ImportTerminology: Name, MergeStrategy, TerminologyData)
- "How do I download or view a terminology?" -> POST / (GetTerminology: Name, optional TerminologyDataFormat)
- "How do I create parallel data for Active Custom Translation?" -> POST / (CreateParallelData: Name, ParallelDataConfig, ClientToken)
- "How do I get details about my parallel data?" -> POST / (GetParallelData: Name)
- "How do I apply formality or profanity settings to a translation?" -> POST / (TranslateText or TranslateDocument with Settings: {Formality, Profanity, Brevity})
- "How do I tag a Translate resource for cost tracking?" -> POST / (TagResource: ResourceArn, Tags)
- "How do I clean up unused terminologies or parallel data?" -> POST / (DeleteTerminology: Name) or POST / (DeleteParallelData: Name)

## Response Tips

- **Translation responses** (TranslateText, TranslateDocument): Always check `AppliedTerminologies` and `AppliedSettings` to confirm your custom terminology and formality/profanity/brevity settings were actually applied; absence means they were silently ignored.
- **List endpoints** (ListLanguages, ListParallelData, ListTerminologies, ListTextTranslationJobs): Paginated via `NextToken`/`MaxResults` -- keep calling with the returned `NextToken` until it is null; default page size is small.
- **Batch job responses** (DescribeTextTranslationJob): The `JobDetails` nested object contains `TranslatedDocumentsCount`, `DocumentsWithErrorsCount`, and `InputDocumentsCount` -- use these to compute progress percentage and error rate.
- **Parallel data and terminology responses**: Status field indicates lifecycle (`CREATING`, `ACTIVE`, `DELETING`, `FAILED`) -- resources are not usable until status is `ACTIVE`.
- **TranslateDocument**: Returns `TranslatedDocument.Content` as raw bytes -- handle binary content appropriately based on the original document format.

## Anomaly Flags

- **Job stuck in non-terminal state**: Surface if `DescribeTextTranslationJob` returns `JobStatus` of `IN_PROGRESS` or `SUBMITTED` for an extended period without progress in `JobDetails` counters.
- **High error rate in batch jobs**: Flag when `DocumentsWithErrorsCount` exceeds 10% of `InputDocumentsCount` in job details.
- **Parallel data import failures**: Alert when `FailedRecordCount` or `SkippedRecordCount` is non-zero after creation or update, as this silently degrades translation quality.
- **Terminology skipped terms**: Flag when `SkippedTermCount` in TerminologyProperties is non-zero -- indicates some terms were invalid and silently dropped.
- **Settings not applied**: If `AppliedSettings` in a translation response differs from what was requested (e.g., Formality requested but not returned), the language pair likely does not support that setting.
- **LatestUpdateAttemptStatus failure**: On `UpdateParallelData`, if `LatestUpdateAttemptStatus` is not `ACTIVE`, the update failed and the previous version is still in use.
- **Throttling**: AWS SigV4 APIs return HTTP 429 -- exponential backoff is required; surface if multiple consecutive requests are throttled.

## Playbook

### 1. Translate Text with Custom Terminology and Formality

1. Call **ImportTerminology** with `Name`, `MergeStrategy: "OVERWRITE"`, and `TerminologyData` (CSV or TMX format) to create or update your glossary.
2. Verify the terminology is ready by calling **GetTerminology** with the `Name` and confirming the status is active and `SkippedTermCount` is 0.
3. Call **TranslateText** with `Text`, `SourceLanguageCode`, `TargetLanguageCode`, `TerminologyNames: ["your-terminology"]`, and `Settings: {Formality: "FORMAL"}`.
4. Check `AppliedTerminologies` in the response to confirm your terms were used; check `AppliedSettings` to confirm formality was applied.

### 2. Run a Batch Translation Job and Monitor Progress

1. Call **StartTextTranslationJob** with `InputDataConfig` (S3 URI + content type), `OutputDataConfig` (S3 URI), `DataAccessRoleArn`, `SourceLanguageCode`, `TargetLanguageCodes`, and `ClientToken` (idempotency key).
2. Capture the returned `JobId`.
3. Poll **DescribeTextTranslationJob** with `JobId` periodically (e.g., every 60 seconds).
4. Monitor `JobStatus` (SUBMITTED -> IN_PROGRESS -> COMPLETED or COMPLETED_WITH_ERROR or FAILED) and `JobDetails` for document counts.
5. If the job is stuck or producing errors, call **StopTextTranslationJob** with the `JobId` to cancel it.

### 3. Set Up Parallel Data for Active Custom Translation

1. Upload your parallel data file (TMX, CSV, or TSV) to S3.
2. Call **CreateParallelData** with `Name`, `ParallelDataConfig: {S3Uri, Format}`, and `ClientToken`.
3. Poll **GetParallelData** with `Name` until `Status` is `ACTIVE`; check `FailedRecordCount` and `SkippedRecordCount` for quality issues.
4. Reference the parallel data in batch jobs via `ParallelDataNames` in **StartTextTranslationJob**.
5. To update, call **UpdateParallelData** with the new S3 file and check `LatestUpdateAttemptStatus` for success.

### 4. Manage Resource Tags for Cost Allocation

1. Call **TagResource** with the `ResourceArn` of your terminology, parallel data, or other Translate resource, plus `Tags: [{Key, Value}]`.
2. Verify tags by calling **ListTagsForResource** with the `ResourceArn`.
3. To remove tags, call **UntagResource** with the `ResourceArn` and `TagKeys` array of keys to remove.

### 5. Discover Supported Languages and Capabilities

1. Call **ListLanguages** with optional `DisplayLanguageCode` (e.g., `"en"`) to get language names in your preferred display language.
2. Paginate through results using `NextToken` if the list is truncated.
3. Use the returned language codes as valid values for `SourceLanguageCode` and `TargetLanguageCode` in translation calls.
4. Note: use `"auto"` as `SourceLanguageCode` in **TranslateText** for automatic language detection; the response's `SourceLanguageCode` will contain the detected language.


## Response Tips
- Check response schemas in references/api-spec.lap for field details
- Create/update endpoints typically return the created/updated object

## References
- Full spec: See references/api-spec.lap for complete endpoint details, parameter tables, and response schemas

> Generated from the official API spec by [LAP](https://lap.sh)
