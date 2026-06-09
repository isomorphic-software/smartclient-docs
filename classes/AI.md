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
## ClassAttr: AI.delegatorPrompts

### Description
Customizable prompt templates used by the [AIDelegator](AIDelegator.md#class-aidelegator) CoTProcess to decide which registered [AI service](#type-aiservicedescriptor) should handle a user's request. Override any of these to change the delegator's behavior without writing code; see the [AI Assist overview](../kb_topics/aiAssist.md#kb-topic-ai-assist) for the full request flow.

Properties:

*   **introPrompt** - explains the Delegator's role to the AI
*   **serviceListPrimer** - text before the list of available services
*   **decisionPrompt** - the task prompt for the decision step, as a template string with `${...}` expressions evaluated against the [CoT prompt scope](../kb_topics/CoTPromptScope.md#kb-topic-cotpromptscope)

### See Also

- [AI.delegate](#classmethod-aidelegate)
- [AIDelegator](AIDelegator.md#class-aidelegator)

**Flags**: IRW

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
## ClassAttr: AI.onAPIKeyError

### Description
Optional callback fired when any AI engine response is classified as an API key authentication error (invalid key, missing key, or permission denied). The callback receives a single `errorMessage` string argument containing the provider's error text.

This fires before the per-request callback, regardless of whether the request was made with [AIRequest.willHandleError](AIRequest.md#attr-airequestwillhandleerror). Set to `null` (default) to disable. The Showcase uses this to surface [FeatureExplorer.showAPIKeyErrorDialog](#featureexplorershowapikeyerrordialog) automatically on any API key failure.

### See Also

- [AIEngine.isAPIKeyError](AIEngine.md#method-aiengineisapikeyerror)

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
## ClassMethod: AI.registerAIService

### Description
Registers an AI service globally so [AI.delegate](#classmethod-aidelegate) can discover and invoke it. Global services are available regardless of which component has focus.

To register a service scoped to a specific component (and its descendants), use [Canvas.registerAIService](Canvas.md#method-canvasregisteraiservice) instead — canvas-scoped services shadow global ones with the same name.

See the [AI Assist overview](../kb_topics/aiAssist.md#kb-topic-ai-assist) for the registration model and an end-to-end example.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| service | [AIServiceDescriptor](#type-aiservicedescriptor) | false | — | the service to register |

### See Also

- [Canvas.registerAIService](Canvas.md#method-canvasregisteraiservice)
- [AI.unregisterAIService](#classmethod-aiunregisteraiservice)
- [AI.delegate](#classmethod-aidelegate)
- [aiAssist](../kb_topics/aiAssist.md#kb-topic-ai-assist)

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
## ClassMethod: AI.getSupportedEngineData

### Description
Returns display records for all built-in [AI engines](AIEngine.md#class-aiengine), suitable for populating a UI grid or list. Each record has the following properties:

*   `engineId` — the engine ID (use as `ai.defaultEngineId` in server.properties)
*   `name` — a human-readable model name
*   `provider` — the AI service provider (OpenAI, Google, etc.)
*   `apiKeyProperty` — the `server.properties` key that holds this provider's API key (e.g. `OpenAI.api.key`), or `null` for engines that use provider-specific configuration

Custom engines added via [AI.registerEngine](#classmethod-airegisterengine) are not included.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| foundationalOnly | [boolean](../reference.md#type-boolean) | true | — | pass `true` to return only foundational AI chat/completion models, excluding specialized engines such as embedding models and vector database engines. Use this when presenting a list of engines a user can select as [AI.defaultEngineId](#classattr-aidefaultengineid). |

### Returns

`[Array of Object](#type-array-of-object)` — engine display records

### See Also

- [AI.getSupportedEngineIds](#classmethod-aigetsupportedengineids)

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
## ClassMethod: AI.unregisterAIService

### Description
Removes a previously registered global AI service.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | the name of the service to remove |

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
## ClassMethod: AI.getSupportedEngineIds

### Description
Returns the engine IDs of all built-in [AI engines](AIEngine.md#class-aiengine) — those available without registration, provided the appropriate API key is set in [server.properties](#groupdef-server_properties).

Note that custom engines added via [AI.registerEngine](#classmethod-airegisterengine) are not included.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| foundationalOnly | [boolean](../reference.md#type-boolean) | true | — | pass `true` to return only foundational AI chat/completion models, excluding specialized engines such as embedding models and vector database engines. Use this when presenting a list of engines a user can select as [AI.defaultEngineId](#classattr-aidefaultengineid). |

### Returns

`[Array of String](#type-array-of-string)` — the engine IDs of matching built-in AI engines

### See Also

- [AI.getSupportedEngineData](#classmethod-aigetsupportedenginedata)
- [AI.getEngine](#classmethod-aigetengine)

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
## ClassMethod: AI.getAIServicesForContext

### Description
Collects AI services available for a given context by walking the component hierarchy from `focusCanvas` upward and merging with global services. Component-level registrations shadow global ones of the same name.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| focusCanvas | [Canvas](#type-canvas) | false | — | the canvas that currently has focus (may be null) |

### Returns

`[Object](../reference.md#type-object)` — merged map of service name to [AIServiceDescriptor](../reference.md#object-aiservicedescriptor)

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
## ClassMethod: AI.getRegisteredAIServices

### Description
Returns the map of all globally registered AI services (name to descriptor).

### Returns

`[Object](../reference.md#type-object)` — map of service name to [AIServiceDescriptor](../reference.md#object-aiservicedescriptor)

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
## ClassMethod: AI.delegate

### Description
Primary entry point for the AI Assist system. Routes a user request to the most appropriate registered [AI service](#type-aiservicedescriptor) by running the [AIDelegator](AIDelegator.md#class-aidelegator) — see the [AI Assist overview](../kb_topics/aiAssist.md#kb-topic-ai-assist) for the full registration and routing model.

Behavior:

*   If no services are registered, logs a warning and returns.
*   If only one service is registered, invokes it directly (no AI call).
*   Otherwise, runs the [AIDelegator](AIDelegator.md#class-aidelegator) to ask the AI which service best matches the user's intent, then calls that service's `invoke()`.
*   If the AI call fails or returns an unknown service name, falls back to the first registered service so the request is never silently dropped.

Services are resolved by walking the component hierarchy from `context.focusCanvas` upward (see [AI.getAIServicesForContext](#classmethod-aigetaiservicesforcontext)), so canvas-scoped services registered via [Canvas.registerAIService](Canvas.md#method-canvasregisteraiservice) take precedence over globals of the same name.

Built-in UI entry points — [AIAssistItem](../reference.md#class-aiassistitem) and [VoiceAssist](VoiceAssist.md#class-voiceassist) — call this method automatically. Application code typically calls it directly only when building its own entry point.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| userPrompt | [String](#type-string) | false | — | the user's request text |
| context | [Object](../reference.md#type-object) | true | — | optional context with `rootCanvas` and/or `focusCanvas`. `focusCanvas` is used for component-scoped service resolution; if omitted, the canvas with keyboard focus is used |
| callback | [Function](#type-function) | true | — | optional callback fired when delegation completes, with arguments `(serviceName, fellBack)`. `fellBack` is truthy if the first-service fallback was used |

### See Also

- [AI.registerAIService](#classmethod-airegisteraiservice)
- [Canvas.registerAIService](Canvas.md#method-canvasregisteraiservice)
- [AI.delegatorPrompts](#classattr-aidelegatorprompts)
- [aiAssist](../kb_topics/aiAssist.md#kb-topic-ai-assist)

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
