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
## ClassAttr: AI.mockingPolicy

### Description
Governs whether mock responses registered via [AI.addMockResponses](#classmethod-aiaddmockresponses) are used in place of real AI calls, and whether the [AIInterceptDialog](../reference.md#class-aiinterceptdialog) is shown to let a user inspect or edit each response before it is returned. Alias for the older [AI.responseSpoofingMode](#classattr-airesponsespoofingmode).

Value mappings to the legacy attribute:

*   `"none"` = legacy `"none"` (never use mock responses; always contact the AI server)
*   `"auto"` = legacy `"hybrid"` (use a registered mock response when one matches the current request; otherwise contact the AI server)
*   `"interactive"` = legacy `"full"` (always show the intercept dialog for every AI request; the user can edit the response, forward the prompt to the real AI, or cancel)

This attribute operates at the raw AI-request layer and is independent of the CoT-level mocking flags [CoTProcess.mockMode](CoTProcess.md#attr-cotprocessmockmode) / [CoTProcess.mockInteractive](CoTProcess.md#attr-cotprocessmockinteractive). When both layers are active, the CoT-level dialog appears first and the AI-level dialog appears subsequently when the user forwards the request to the AI engine.

### Groups

- AIMocking

**Flags**: IRW

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
## ClassAttr: AI.maxActiveAnswerEngineOperations

### Description
The maximum number of Answer Engine operations that can be active (not paused and not canceled) at any given time.

### Groups

- answerEngine

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
## ClassMethod: AI.resumeDataQuestion

### Description
Resumes a data question if paused.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| questionId | [String](#type-string) | false | — | The ID of the data question to resume. |

### Groups

- answerEngine

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
## ClassMethod: AI.sendPrompt

### Description
Evaluates the given [dynamic string](../kb_topics/dynamicStrings.md#kb-topic-dynamic-strings) to form a prompt string that is then sent as the request to the default AI engine.

Within `dynamicString`, any evaluated JavaScript expressions have access to all of the values in the `context` ValueMap.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dynamicString | [DynamicString](../reference_2.md#type-dynamicstring) | false | — | A dynamic string. |
| context | [ValueMap](../reference_2.md#type-valuemap) | false | — | A map from each in-scope [Identifier](../reference_2.md#type-identifier) to its value. |
| callback | [AIResponseCallback](#type-airesponsecallback) | false | — | The callback to fire with the response from AI. |

### Groups

- dynamicStrings

---
## ClassMethod: AI.pauseDataQuestion

### Description
Pauses a data question if not already paused or canceled.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| questionId | [String](#type-string) | false | — | The ID of the data question to pause. |

### Groups

- answerEngine

---
## ClassMethod: AI.askDataQuestion

### Description
Asks AI to answer a question about the data of the application.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| question | [String](#type-string)|[UserAIRequest](#type-userairequest) | false | — | The text of the end-user's question or their request for an answer to a data question. |
| dataSources | [Array of DataSource](#type-array-of-datasource)|[Array of GlobalId](#type-array-of-globalid) | true | — | The available data sources. All data sources in the array must have a global ID. If `null`, then the array of all DataSources available to the AI module is used. |
| settings | [DataQuestionSettings](#type-dataquestionsettings) | true | — | Settings to use when answering the data question. |
| callback | [AskDataQuestionResultCallback](#type-askdataquestionresultcallback) | true | — | The callback to call with the result. |

### Groups

- answerEngine

---
## ClassMethod: AI.getMockingPolicy

### Description
Returns the current [AI.mockingPolicy](#classattr-aimockingpolicy). The return value is always one of `"none"`, `"auto"`, or `"interactive"`; the legacy [AI.responseSpoofingMode](#classattr-airesponsespoofingmode) values `"hybrid"` and `"full"` are normalized before returning.

### Returns

`[String](#type-string)` — The current mocking policy: "none", "auto", or "interactive"

### Groups

- AIMocking

---
## ClassMethod: AI.setMockingPolicy

### Description
Sets [AI.mockingPolicy](#classattr-aimockingpolicy). Pass one of `"none"`, `"auto"`, or `"interactive"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| policy | [String](#type-string) | false | — | The mocking policy: "none", "auto", or "interactive" |

### Groups

- AIMocking

---
## ClassMethod: AI.addMockResponses

### Description
Alias for [AI.addSpoofedResponses](#classmethod-aiaddspoofedresponses).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| responses | [Array of Object](#type-array-of-object) | false | — | mock response entries |

### Groups

- AIMocking

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
## ClassMethod: AI.getDataSourceSummary

### Description
Returns a structured summary of a DataSource at a configurable detail level. In `"compact"` mode (default), only identity metadata, primary key, and foreign key relationships are included — suitable for large-app DS selection where full field listings would exceed the AI context window. Higher detail levels progressively add field information via an `otherFields` property.

**Detail levels** (set via `settings.detail`):

*   `"compact"` — ID, title, description, fieldCount, pk, fk. No field list.
*   `"salientNames"` — adds `otherFields` as an array of field name strings for salient/critical fields (PK and FK fields already shown in `pk`/`fk` are excluded).
*   `"salientTyped"` — like salientNames but each entry is an object with `name`, `type`, and optionally `required` and `valueMap`.
*   `"allTyped"` — like salientTyped but includes all fields, not just salient ones.
*   `"full"` — all fields with the full [AI.salientFieldAttributes](#aisalientfieldattributes) attribute mask.

**Settings**:

*   `detail` (String) — one of the levels above; default `"compact"`.
*   `maxFields` (Integer) — cap on the number of fields in `otherFields`.
*   `excludeHousekeeping` (Boolean) — omit auto-populated fields (creator, modifier, creatorTimestamp, modifierTimestamp); default `true` for all modes except `"full"`.
*   `includeData` (String) — if set, includes representative data samples from available client-side caches. Values: `"fieldValues"` (per-field unique sample values added as `sampleValues` on each field entry) or `"records"` (whole sample records added as `sampleRecords`). Data is sourced from clientOnly cacheData, cacheAllData cacheResultSet, or any default-fetch (no operationId) ResultSet observing the DataSource — no server requests are triggered.
*   `dataSampleCount` (Integer) — maximum unique sample values per field (fieldValues mode) or sample records (records mode); default 3.
*   `dataSampleMaxSearch` (Integer) — maximum cache records to scan when collecting unique sample values; default 100.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSource | [DataSource](#type-datasource)|[String](#type-string) | false | — | DataSource or ID |
| settings | [Object](../reference.md#type-object) | true | — | detail level and field options |

### Returns

`[Object](../reference.md#type-object)` — structured summary

### Groups

- answerEngine

### See Also

- [AI.getDataSourceSummaries](#classmethod-aigetdatasourcesummaries)

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
## ClassMethod: AI.cancelDataQuestion

### Description
Cancels a data question if not already canceled.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| questionId | [String](#type-string) | false | — | The ID of the data question to cancel. |

### Groups

- answerEngine

---
## ClassMethod: AI.clearMockResponses

### Description
Alias for [AI.clearSpoofedResponses](#method-aiclearspoofedresponses).

### Groups

- AIMocking

---
## ClassMethod: AI.getDataSourceSummaries

### Description
Returns an array of summaries (see [AI.getDataSourceSummary](#classmethod-aigetdatasourcesummary)) for the specified DataSources, or all registered application DataSources if no list is provided. The `settings` parameter is passed through to each [AI.getDataSourceSummary](#classmethod-aigetdatasourcesummary) call.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSourceNames | [Array of String](#type-array-of-string) | true | — | DataSource IDs to summarize; defaults to [AI.getDataSourceNames](#method-aigetdatasourcenames) |
| settings | [Object](../reference.md#type-object) | true | — | passed through to [AI.getDataSourceSummary](#classmethod-aigetdatasourcesummary) |

### Returns

`[Array of Object](#type-array-of-object)` — array of summary objects

### Groups

- answerEngine

---
