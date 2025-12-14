# AI Documentation

[← Back to API Index](../reference.md)

---

## Class: AI

### Description
Provides class methods for enabling and disabling the use of AI technology, registering and unregistering [AI engines](AIEngine.md#class-aiengine), and performing high-level operations using installed AI engines.

### See Also

- [integratingAI](../kb_topics/integratingAI.md#kb-topic-integrating-ai-technology)

---
## ClassAttr: AI.dataSourceIsRequiredErrorMessage

### Description
—

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AI.noAIEngineSupportingVisionRequestsIsRegisteredErrorMessage

### Description
—

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AI.aiWasDisabledMessage

### Description
Message to use for the [disabledMessage](AsyncOperationResult.md#attr-asyncoperationresultdisabledmessage) when [AI.isEnabled](#classmethod-aiisenabled) returned `false`.

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AI.noDataSourcesAvailableOrFoundErrorMessage

### Description
—

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AI.willSubsetFieldsDetailMessage

### Description
—

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AI.finishedSubsettingFieldsDetailMessage

### Description
—

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AI.disabled

### Description
Whether AI is disabled.

By default, AI is disabled. This static property must be set to `false` and the [default](#classattr-aidefaultengineid) [AIEngine](AIEngine.md#class-aiengine) must be registered in order to enable the use of AI in the application.

### See Also

- [AI.isEnabled](#classmethod-aiisenabled)
- [AI.registerEngine](#classmethod-airegisterengine)

**Flags**: IRW

---
## ClassAttr: AI.defaultEngineId

### Description
The ID of the default [AIEngine](AIEngine.md#class-aiengine) to use.

**Flags**: IRW

---
## ClassAttr: AI.startingYourRequestDetailMessage

### Description
—

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AI.aiNotAbleToProcessRequestErrorMessage

### Description
An error message displayed when AI is unable to respond to a request.

### Groups

- i18nMessages

**Flags**: RW

---
## ClassAttr: AI.defaultMaxRetries

### Description
The defualt maximum number of retries for any one particular request to AI.

**Flags**: IRW

---
## ClassAttr: AI.defaultAIEngineNotRegisteredErrorMessage

### Description
—

### Groups

- i18nMessages

**Flags**: RW

---
## ClassMethod: AI.summarizeValue

### Description
Requests that available AI engine(s) be used to generate a summary of a value according to a natural language description of how to summarize the value.

See [AI.asyncSummarizeValue](#classmethod-aiasyncsummarizevalue) for a [Promise](../reference_2.md#object-promise)-based version of this class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| request | [SummarizeValueRequest](#type-summarizevaluerequest) | false | — | The request. |
| callback | [SummarizeValueResultCallback](#type-summarizevalueresultcallback) | false | — | The callback to fire with the [SummarizeValueResult](../reference.md#object-summarizevalueresult). |

---
## ClassMethod: AI.asyncSummarizeValue

### Description
Requests that available AI engine(s) be used to generate a summary of a value according to a natural language description of how to summarize the value.

See [AI.summarizeValue](#classmethod-aisummarizevalue) for a callback-based version of this class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| request | [SummarizeValueRequest](#type-summarizevaluerequest) | false | — | The request. |

### Returns

`[Promise](#type-promise)` — A `Promise` for a [SummarizeValueResult](../reference.md#object-summarizevalueresult). This `Promise` resolves if the summarize value operation is successful ([SummarizeValueResult.type](AsyncOperationResult.md#attr-asyncoperationresulttype) is "success"); otherwise it rejects.

---
## ClassMethod: AI.asyncSuggestRecordSummaryTitle

### Description
Requests that available [AIEngine](AIEngine.md#class-aiengine)(s) be used to suggest an appropriate title for a new field that will contain AI-generated record summaries.

See [AI.suggestRecordSummaryTitle](#classmethod-aisuggestrecordsummarytitle) for a callback-based version of this class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| request | [SuggestRecordSummaryTitleRequest](#type-suggestrecordsummarytitlerequest) | false | — | The request. |

### Returns

`[Promise](#type-promise)` — A `Promise` for a [SuggestRecordSummaryTitleResult](../reference.md#object-suggestrecordsummarytitleresult). This `Promise` resolves if the suggest-title operation is successful ([SuggestRecordSummaryTitleResult.type](AsyncOperationResult.md#attr-asyncoperationresulttype) is "success"); otherwise it rejects.

---
## ClassMethod: AI.suggestRecordSummaryTitle

### Description
Requests that available [AIEngine](AIEngine.md#class-aiengine)(s) be used to suggest an appropriate title for a new field that will contain AI-generated record summaries.

See [AI.asyncSuggestRecordSummaryTitle](#classmethod-aiasyncsuggestrecordsummarytitle) for a [Promise](../reference_2.md#object-promise)-based version of this class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| request | [SuggestRecordSummaryTitleRequest](#type-suggestrecordsummarytitlerequest) | false | — | The request. |
| callback | [SuggestRecordSummaryTitleCallback](#type-suggestrecordsummarytitlecallback) | false | — | The callback to [fire](Class.md#classmethod-classfirecallback) with the result. |

---
## ClassMethod: AI.clearAIFilterCaches

### Description
Removes information for all records to which an "aiFilter" [AdvancedCriteria](../reference.md#object-advancedcriteria) has been applied.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| aiCriterion | [AdvancedCriteria](#type-advancedcriteria) | false | — | The "aiFilter" `AdvancedCriteria` to update. |

---
## ClassMethod: AI.isEnabled

### Description
Determines whether AI support is enabled. [AI.disabled](#classattr-aidisabled) must be set to `false` and the default [AIEngine](AIEngine.md#class-aiengine) must be registered in order to enable the use of AI.

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if the use of AI is enabled; `false` otherwise.

### See Also

- [AI.disabled](#classattr-aidisabled)
- [AI.defaultEngineId](#classattr-aidefaultengineid)

---
## ClassMethod: AI.buildDataBoundUI

### Description
Requests that available AI engine(s) be used to build data-bound UI component(s) according to a user's description of what they would like to build.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buildRequest | [BuildDataBoundUIViaAIRequest](#type-builddatabounduiviaairequest) | false | — | The request to AI to build data-bound UI. |
| callback | [BuildUIViaAIResponseCallback](#type-builduiviaairesponsecallback) | false | — | The callback to call with the result. |

---
## ClassMethod: AI.buildHilites

### Description
Requests that available AI engine(s) be used to build one or more [Hilite](../reference.md#object-hilite) objects according to the user's natural language description of hilite criteria and styling to apply.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buildRequest | [BuildHilitesRequest](#type-buildhilitesrequest) | false | — | The request to AI to build `Hilite` object(s). |
| callback | [BuildHilitesResponseCallback](#type-buildhilitesresponsecallback) | false | — | The callback to call with the result. |

---
## ClassMethod: AI.unregisterEngine

### Description
Unregisters an [AIEngine](AIEngine.md#class-aiengine) specified by its ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| engineId | [String](#type-string) | false | — | the ID of the `AIEngine` to unregister. |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if the `AIEngine` was successfully unregistered; `false` otherwise.

### See Also

- [AI.registerEngine](#classmethod-airegisterengine)

---
## ClassMethod: AI.asyncReapplyAIFilter

### Description
Requests that available AI engine(s) be used to re-evaluate an "aiFilter" [AdvancedCriteria](../reference.md#object-advancedcriteria) on a list of updated records.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reapplyRequest | [ReapplyAIFilterRequest](#type-reapplyaifilterrequest) | false | — | The request to AI to re-evaluate an "aiFilter" [AdvancedCriteria](../reference.md#object-advancedcriteria). |

### Returns

`[Promise](#type-promise)` — A Promise for a [ReapplyAIFilterResponse](../reference.md#object-reapplyaifilterresponse). If the [ReapplyAIFilterResponse.type](AsyncOperationResult.md#attr-asyncoperationresulttype) is "success", then the returned Promise is resolved; otherwise, the returned Promise is rejected.

---
## ClassMethod: AI.buildAIFieldRequest

### Description
Requests that available AI engine(s) be used to build an [AIFieldRequest](../reference_2.md#object-aifieldrequest) from a natural language description of the per-record values to generate for a new AI-generated field.

See [AI.asyncBuildAIFieldRequest](#classmethod-aiasyncbuildaifieldrequest) for a [Promise](../reference_2.md#object-promise)-based version of this class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buildRequest | [BuildAIFieldRequestRequest](#type-buildaifieldrequestrequest) | false | — | The request. |
| callback | [BuildAIFieldRequestResponseCallback](#type-buildaifieldrequestresponsecallback) | false | — | The callback to [fire](Class.md#classmethod-classfirecallback) with the result. |

---
## ClassMethod: AI.isAIFieldRequestNumerical

### Description
Returns `true` if the given [AIFieldRequest](../reference_2.md#object-aifieldrequest) is numerical (its [valueClass](AIFieldRequest.md#attr-aifieldrequestvalueclass) is "ordinal", "interval", or "ratio"); `false` otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| aiFieldRequest | [AIFieldRequest](#type-aifieldrequest) | false | — | The `AIFieldRequest` to test. |

### Returns

`[Boolean](#type-boolean)` — `true` if and only if the given `AIFieldRequest` is numerical.

---
## ClassMethod: AI.summarizeRecords

### Description
Requests that available AI engine(s) be used to generate summaries of records according to the user's natural language description of how to summarize each record.

See [AI.asyncSummarizeRecords](#classmethod-aiasyncsummarizerecords) for a [Promise](../reference_2.md#object-promise)-based version of this class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| request | [SummarizeRecordsRequest](#type-summarizerecordsrequest) | false | — | The request. |
| partialResultCallback | [SummarizeRecordsPartialResultCallback](#type-summarizerecordspartialresultcallback) | true | — | The callback to [fire](Class.md#classmethod-classfirecallback) with each partial result. |
| callback | [SummarizeRecordsResultCallback](#type-summarizerecordsresultcallback) | false | — | The callback to fire with the result. |

---
## ClassMethod: AI.applyAIFilter

### Description
Requests that available AI engine(s) be used to evaluate an "aiFilter" [AdvancedCriteria](../reference.md#object-advancedcriteria) on a list of records.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| applyRequest | [ApplyAIFilterRequest](#type-applyaifilterrequest) | false | — | The request to AI to evaluate an "aiFilter" `AdvancedCriteria`. |
| callback | [ApplyAIFilterResponseCallback](#type-applyaifilterresponsecallback) | false | — | The callback to call with the result. |

---
## ClassMethod: AI.asyncSummarizeRecords

### Description
Requests that available AI engine(s) be used to generate summaries of records according to the user's natural language description of how to summarize each record.

See [AI.summarizeRecords](#classmethod-aisummarizerecords) for a callback-based version of this class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| request | [SummarizeRecordsRequest](#type-summarizerecordsrequest) | false | — | The request. |
| partialResultCallback | [SummarizeRecordsPartialResultCallback](#type-summarizerecordspartialresultcallback) | true | — | The callback to [fire](Class.md#classmethod-classfirecallback) with each partial result. |

### Returns

`[Promise](#type-promise)` — A `Promise` for a [SummarizeRecordsResult](../reference.md#object-summarizerecordsresult).

---
## ClassMethod: AI.asyncBuildAIFieldRequest

### Description
Requests that available AI engine(s) be used to build an [AIFieldRequest](../reference_2.md#object-aifieldrequest) from a natural language description of the per-record values to generate for a new AI-generated field.

See [AI.buildAIFieldRequest](#classmethod-aibuildaifieldrequest) for a callback-based version of this class method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buildRequest | [BuildAIFieldRequestRequest](#type-buildaifieldrequestrequest) | false | — | The request. |

### Returns

`[Promise](#type-promise)` — A `Promise` for a [BuildAIFieldRequestResponse](../reference.md#object-buildaifieldrequestresponse). This `Promise` resolves if the build operation is successful ([BuildAIFieldRequestResponse.type](AsyncOperationResult.md#attr-asyncoperationresulttype) is "success"); otherwise it rejects.

---
## ClassMethod: AI.removeFromAIFilterCaches

### Description
Removes information for the given records from an "aiFilter" [AdvancedCriteria](../reference.md#object-advancedcriteria).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| aiCriterion | [AdvancedCriteria](#type-advancedcriteria) | false | — | The "aiFilter" `AdvancedCriteria` to update. |
| records | [Array of Record](#type-array-of-record) | false | — | The records, about which any information held in `aiCriterion` will be removed. |

---
## ClassMethod: AI.registerEngine

### Description
Registers the given [AIEngine](AIEngine.md#class-aiengine).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| engine | [AIEngine](#type-aiengine) | false | — | The `AIEngine` to register. |

### Returns

`[boolean](../reference.md#type-boolean)` — `true` if the `AIEngine` was successfully registered; `false` otherwise.

### See Also

- [AI.unregisterEngine](#classmethod-aiunregisterengine)

---
## ClassMethod: AI.buildCriterion

### Description
Requests that available AI engine(s) be used to build an [AdvancedCriteria](../reference.md#object-advancedcriteria) object according to the user's natural language description of a filter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| buildRequest | [BuildCriterionRequest](#type-buildcriterionrequest) | false | — | The request. |
| callback | [BuildCriterionResponseCallback](#type-buildcriterionresponsecallback) | false | — | The callback to [fire](Class.md#classmethod-classfirecallback) with the result. |

---
## ClassMethod: AI.getEngine

### Description
Returns the [AIEngine](AIEngine.md#class-aiengine) having the given engine ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| engineId | [String](#type-string) | true | — | the engineId of the `AIEngine` to get. If not specified, [AI.defaultEngineId](#classattr-aidefaultengineid) is used. |

### Returns

`[AIEngine](#type-aiengine)` — the `AIEngine`, or `null` if the `AIEngine` could not be found.

---
