# AI Documentation

[← Back to API Index](../main.md)

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

`[boolean](../main.md#type-boolean)` — `true` if the use of AI is enabled; `false` otherwise.

### See Also

- [AI.disabled](#classattr-aidisabled)
- [AI.defaultEngineId](#classattr-aidefaultengineid)

---
## ClassMethod: AI.sendPrompt

### Description
Evaluates the given [dynamic string](../kb_topics/dynamicStrings.md#kb-topic-dynamic-strings) to form a prompt string that is then sent as the request to the default AI engine.

Within `dynamicString`, any evaluated JavaScript expressions have access to all of the values in the `context` ValueMap.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dynamicString | [DynamicString](../main_2.md#type-dynamicstring) | false | — | A dynamic string. |
| context | [ValueMap](../main_2.md#type-valuemap) | false | — | A map from each in-scope [Identifier](../main.md#type-identifier) to its value. |
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
