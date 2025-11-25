# Callbacks Documentation

[← Back to API Index](../main.md)

---

## Class: Callbacks

### Description
This object cannot be used; it exists for documentation purposes only as a place to put documentation for callback methods, such as the callback for [DataSource.fetchData()](#method-callbacksdscallback).

---
## Method: Callbacks.RemoteWindowMapCallback

### Description
Callback reporting the result of a [RemoteWindow](RemoteWindow.md#class-remotewindow) operation yielding a map.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| remoteWindow | [RemoteWindow](#type-remotewindow) | false | — | window affected |
| result | [Map](#type-map) | false | — | result |

---
## Method: Callbacks.RunTaskCallback

### Description
Called when [Process.runTask](Process.md#method-processruntask) has finished executing the specified task.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| task | [Task](#type-task) | false | — | The task instance that was executed. |
| process | [Process](#type-process) | false | — | The owning process instance. |
| outputs | [Object](../main.md#type-object) | false | — | Task outputs, if any (for [CoTTask](CoTTask.md#class-cottask), this is the final `$outputs` JSON). May be null if the task does not produce outputs. |

---
## Method: Callbacks.AsyncMultipleValuesGenerationResultCallback

### Description
Callback fired with the result of an asynchronous operation to generate multiple values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [AsyncMultipleValuesGenerationResult](#type-asyncmultiplevaluesgenerationresult) | false | — | The result. |

---
## Method: Callbacks.LoadScreenCallback

### Description
A [Callback](../main.md#type-callback) to evaluate when a screen is loaded via [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screen | [Canvas](#type-canvas) | true | — | The last top-level component loaded |
| rpcResponse | [RPCResponse](#type-rpcresponse) | true | — | — |
| suppressedGlobals | [Map](#type-map) | true | — | A collection of suppressed globals. |

---
## Method: Callbacks.AIResponseCallback

### Description
Callback fired when a response is received from an AI engine.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| aiResponse | [AIResponse](#type-airesponse) | false | — | The response. |
| aiRequest | [AIRequest](#type-airequest) | false | — | The original request. |

---
## Method: Callbacks.AIProgressCallback

### Description
Callback called with progress information about an ongoing AI process.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| context | [AIContext](#type-aicontext) | false | — | — |
| numStepsCompleted | [Integer](../main_2.md#type-integer) | false | — | — |
| estimatedNumTotalSteps | [Integer](../main_2.md#type-integer) | false | — | — |
| newMessages | [Array of AIProgressMessage](#type-array-of-aiprogressmessage) | false | — | Any additional messages about the progress that has been made since the last invocation of the progress callback. This may be `null` or an empty array, if, for example, only the `numStepsCompleted` is being updated. |

---
## Method: Callbacks.RPCCallback

### Description
A [Callback](../main.md#type-callback) to evaluate when an RPCRequest completes.

Parameters passed to this callback are:

*   rpcResponse: an [RPCResponse](RPCResponse.md#class-rpcresponse) encapsulating the server response to your request
*   data: just the "data" property from the RPCResponse, for convenience
*   rpcRequest: the [RPCRequest](../main.md#object-rpcrequest) that was sent. You can use [RPCRequest.clientContext](RPCRequest.md#attr-rpcrequestclientcontext) to track state during the server turnaround.

For example, to take the data returned by the server and display it in a previously created ListGrid with the ID "myGrid":
```
     isc.RPCManager.send("getData", "myGrid.setData(data)");
 
```
Or
```
     isc.RPCManager.send("getData", function (rpcResponse, data, rpcRequest) { 
                                        myGrid.setData(data)
     });
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [RPCResponse](#type-rpcresponse) | false | — | response a RPCResponse encapsulating the server response to your request |
| rawData | [Any](#type-any) | false | — | rawData The "data" property from the RPCResponse, for convenience. The data can also be obtained via {@link RPCResponse#getDataAsMap()}, {@link RPCResponse#getDataAsString()}, or {@link RPCResponse#getDataAsObject()}, depending on the type of data that is expected to be returned from the server. |
| request | [RPCRequest](#type-rpcrequest) | false | — | the RPCRequest that was sent. |

### See Also

- [RPCRequest](../main.md#object-rpcrequest)
- [RPCResponse](RPCResponse.md#class-rpcresponse)

---
## Method: Callbacks.PlaybackCompleteCallback

### Description
A [Callback](../main.md#type-callback) fired when [Sound.play](Sound.md#method-soundplay) completes.

---
## Method: Callbacks.TimingDataCallback

### Description
Callback fired after a call to [RPCManager.getTimingData](RPCManager.md#classmethod-rpcmanagergettimingdata) to report gathered timing data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Object](../main.md#type-object) | false | — | The root object of the timing data tree (note, this is a plain JS object, not an instance of the SmartClient Tree class) |

---
## Method: Callbacks.MultiWindowEventCallback

### Description
Callback scheduled by [MultiWindow.setEvent](MultiWindow.md#classmethod-multiwindowsetevent). The [RemoteWindow](RemoteWindow.md#class-remotewindow) may be null if the associated browser window is unloading or closing.

Note that the event is simply an [OpenFin application event](https://developer.openfin.co/docs/javascript/stable/tutorial-Application.EventEmitter.html) when OpenFin is present, but may not be fully populated in fallback mode without OpenFin.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| remoteWindow | [RemoteWindow](#type-remotewindow) | false | — | window affected by event, or null if not found |
| eventType | [MultiWindowEvent](../main_2.md#type-multiwindowevent) | false | — | event type as passed to [MultiWindow.setEvent](MultiWindow.md#classmethod-multiwindowsetevent) |
| event | [Object](../main.md#type-object) | false | — | event data see MultiWindow.setEvent() see MultiWindow.clearEvent() |

---
## Method: Callbacks.ValidatorConditionCallback

### Description
[Callback](../main.md#type-callback) required for the property [Validator.condition](Validator.md#attr-validatorcondition) and [ValidatorDefinition.condition](ValidatorDefinition.md#attr-validatordefinitioncondition).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [DataSourceField](#type-datasourcefield)|[ListGridField](#type-listgridfield)|[FormItem](#type-formitem) | false | — | FormItem, DataSourceField or ListGridField on which this validator was declared. NOTE: FormItem will not be available during a save performed without a form (eg programmatic save) or if the field is not available in the form. |
| validator | [Validator](#type-validator) | false | — | Validator declaration from eg [DataSourceField.validators](DataSourceField.md#attr-datasourcefieldvalidators). |
| value | [Any](#type-any) | false | — | value to validate |
| record | [Object](../main.md#type-object) | false | — | Field values for record being validated. |
| additionalContext | [Object](../main.md#type-object) | false | — | Object containing extra context which may be useful to the condition function. Contains the following properties:  

*   validatorDefinition: the [ValidatorDefinition](../main_2.md#object-validatordefinition) for the validator being processed. This allows easy access to custom validator defintion properties while evaluating the condition.
*   component: the DynamicForm or ListGrid being validated  
    
*   rowNum: the row number of the cell being validated (only if component is a ListGrid)  
    
*   colNum: the column number of the cell being validated (only if component is a ListGrid) |

### Returns

`[boolean](../main.md#type-boolean)` — whether the value passed validation. True for passed, false for fail.

---
## Method: Callbacks.ShiftFocusCallback

### Description
A [Callback](../main.md#type-callback) fired by the TabIndexManager when application code or user action attempts to synthetically shift focus to some registered target. See [TabIndexManager.shiftFocus](TabIndexManager.md#classmethod-tabindexmanagershiftfocus).

A typical implementation will shift focus to some native element associated with the registered target, or if this is not currently possible, return false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | The ID String passed to [TabIndexManager.addTarget](TabIndexManager.md#classmethod-tabindexmanageraddtarget) when the callback was registered. |

### Returns

`[boolean](../main.md#type-boolean)` — Return true if focus could be successfully moved to the desired target. Returning false indicates the target could not accept focus and will often cause the TabIndexManager to find the next registered target and attempt to shift focus there.

---
## Method: Callbacks.DSCallback

### Description
Callback fired when DataSource methods that send DSRequests complete (such as [DataSource.fetchData](DataSource.md#method-datasourcefetchdata)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | a [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data |
| data | [Any](#type-any) | false | — | data returned to satisfy the DataSource request. See the [DataSource operations](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations) topic for expected results for each type of DataSource operation |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | the [DSRequest](../main_2.md#object-dsrequest) that was sent. You can use [DSRequest.clientContext](DSRequest.md#attr-dsrequestclientcontext) to track state during the server turnaround. |

---
## Method: Callbacks.ExportImageCallback

### Description
Callback for [RPCManager.exportImage](RPCManager.md#classmethod-rpcmanagerexportimage).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| imageData | [String](#type-string) | false | — | image data from the server, in base64 format |

---
## Method: Callbacks.AnimationCallback

### Description
A [Callback](../main.md#type-callback) called when the move completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| earlyFinish | [boolean](../main.md#type-boolean) | false | — | true if the animation was cut short. To quit an animation early, simply call the non-animated version of the same API, so for example call [Canvas.hide](Canvas.md#method-canvashide) to cut short an animation from [Canvas.animateHide](Canvas.md#method-canvasanimatehide) already in progress. |

---
## Method: Callbacks.GetFieldValueCallback

### Description
[Callback](../main.md#type-callback) required for the property [DataSourceField.getFieldValue](DataSourceField.md#attr-datasourcefieldgetfieldvalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Object](../main.md#type-object)|[XMLElement](../main.md#type-xmlelement) | false | — | record object selected from web service response data by [recordXPath](OperationBinding.md#attr-operationbindingrecordxpath) |
| value | [Any](#type-any) | false | — | default value derived by the method described in [DataSourceField.valueXPath](DataSourceField.md#attr-datasourcefieldvaluexpath) |
| field | [DataSourceField](#type-datasourcefield) | false | — | DataSourceField definition |
| fieldName | [FieldName](../main.md#type-fieldname) | false | — | name of the DataSource field |

### Groups

- clientDataIntegration

---
## Method: Callbacks.MockDSExportCallback

### Description
Callback fired upon successful completion of [Reify.getMockDS](Reify.md#classmethod-reifygetmockds) or [Reify.showMockDS](Reify.md#classmethod-reifyshowmockds):

*   Output for all [DataSources](DataSource.md#class-datasource) together is reported as the single string parameter `allDSData`. When using [format](MockDSExportSettings.md#attr-mockdsexportsettingsformat): "reifyCSV", output for separate DataSources is separated by a special marker.
*   Output with each [DataSource](DataSource.md#class-datasource) as a separate string array element is also available as the parameter `perDSData`, ordered to match the `dsNames` parameter in [Reify.getMockDS](Reify.md#classmethod-reifygetmockds) or [Reify.showMockDS](Reify.md#classmethod-reifyshowmockds).

Note that in the case of [Reify.showMockDS](Reify.md#classmethod-reifyshowmockds), the callback is fired after the window is closed, not when it's populated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| allDSData | [String](#type-string) | false | — | concatenated output for all `DataSources` |
| perDSData | [Array of String](#type-array-of-string) | false | — | same output but delivered as a per-DS array |

---
## Method: Callbacks.RemoteWindowBooleanCallback

### Description
Callback reporting the result of a boolean [RemoteWindow](RemoteWindow.md#class-remotewindow) operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| remoteWindow | [RemoteWindow](#type-remotewindow) | false | — | window affected |
| result | [Boolean](#type-boolean) | false | — | result |

---
## Method: Callbacks.AsyncSingleValueGenerationResultCallback

### Description
Callback fired with the result of an asynchronous operation to generate a value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [AsyncSingleValueGenerationResult](#type-asyncsinglevaluegenerationresult) | false | — | The result. |

---
## Method: Callbacks.RPCQueueCallback

### Description
Callback to fire when a queue of requests sent via [RPCManager.sendQueue](RPCManager.md#classmethod-rpcmanagersendqueue) returns.

Note that the Array of RPCResponses passed to this callback will actually be DSResponse objects for any requests that were actually DSRequests.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [Array of RPCResponse](#type-array-of-rpcresponse) | false | — | array of responses returned from the sent queue of requests |

---
## Method: Callbacks.ProcessCallback

### Description
A [Callback](../main.md#type-callback) to evaluate when a Process has been loaded via [Process.loadProcess](Process.md#classmethod-processloadprocess).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| process | [Process](#type-process) | false | — | the loaded Process |

### See Also

- [Process](Process.md#class-process)
- [RPCResponse](RPCResponse.md#class-rpcresponse)

---
## Method: Callbacks.EventErrorCallback

### Description
A [Callback](../main.md#type-callback) called to report [event errors](EventStream.md#attr-eventstreamcaptureeventerrors) from an [active](EventStream.md#method-eventstreamstart) [EventStream](EventStream.md#class-eventstream) to a listener.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [EventStreamData](#type-eventstreamdata) | false | — | A JavaScript object representing the current state of the stream; [events](EventStreamData.md#attr-eventstreamdataevents) will be an array of all retained [EventStreamEvent](../main.md#object-eventstreamevent)s captured by the stream since the last time the callback was invoked, oldest first. The last array element should be the `EventStreamEvent` that triggered this call and have an [errorTrace](EventStreamEvent.md#attr-eventstreameventerrortrace). |
| nEvents | [int](../main.md#type-int) | false | — | The number of events captured by the stream since the last time the callback was invoked. Compare with [EventStreamData.nEvents](EventStreamData.md#attr-eventstreamdatanevents). |

### See Also

- [EventStream.maxSize](EventStream.md#attr-eventstreammaxsize)
- [EventStream.setEventErrorListener](EventStream.md#method-eventstreamseteventerrorlistener)

---
## Method: Callbacks.ShowSectionCallback

### Description
Callback to execute after the section has been shown.

---
## Method: Callbacks.HasFileVersionCallback

### Description
A [Callback](../main.md#type-callback) fired when [DataSource.hasFileVersion](DataSource.md#method-datasourcehasfileversion) completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | A [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data. |
| data | [boolean](../main.md#type-boolean) | false | — | Whether the file version exists. |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The [DSRequest](../main_2.md#object-dsrequest) that was sent. |

### Groups

- fileSource

---
## Method: Callbacks.PaletteNodeCallback

### Description
Callback fired with the [PaletteNodes](../main.md#object-palettenode) obtained asynchronously.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNodes | [Array of PaletteNode](#type-array-of-palettenode) | false | — | an array of PaletteNodes |

---
## Method: Callbacks.HasFileCallback

### Description
A [Callback](../main.md#type-callback) fired when [DataSource.hasFile](DataSource.md#method-datasourcehasfile) completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | A [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data. |
| data | [boolean](../main.md#type-boolean) | false | — | Whether the file exists. |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The [DSRequest](../main_2.md#object-dsrequest) that was sent. |

### Groups

- fileSource

---
## Method: Callbacks.CanPlayCallback

### Description
A [Callback](../main.md#type-callback) fired when [Sound.load](Sound.md#method-soundload) completes.

---
## Method: Callbacks.AskDataQuestionResultCallback

### Description
Callback fired with the result of asking AI to answer a data question.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [DataQuestionResult](#type-dataquestionresult) | false | — | The result. |
| dataQuestion | [DataQuestion](#type-dataquestion) | false | — | The data question. |

### Groups

- answerEngine

---
## Method: Callbacks.GetFileVersionCallback

### Description
Callback fired when [DataSource.getFileVersion](DataSource.md#method-datasourcegetfileversion) completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | A [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data. |
| data | [String](#type-string) | false | — | The file contents, or null if there was an error (such as file not found). |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The [DSRequest](../main_2.md#object-dsrequest) that was sent. |

### Groups

- fileSource

---
## Method: Callbacks.CollapseSectionCallback

### Description
Callback to execute after the section has been collapsed.

---
## Method: Callbacks.LoadProjectCallback

### Description
A [Callback](../main.md#type-callback) to evaluate after [RPCManager.loadProject](RPCManager.md#classmethod-rpcmanagerloadproject) completes.

If [LoadProjectSettings.willHandleError](LoadProjectSettings.md#attr-loadprojectsettingswillhandleerror) is set, the callback will fire even if the requested projects could not be retrieved. You can call [RPCManager.getLoadProjectErrorStatus](RPCManager.md#classmethod-rpcmanagergetloadprojecterrorstatus) or [RPCManager.getLoadProjectErrorMessage](RPCManager.md#classmethod-rpcmanagergetloadprojecterrormessage) in this case for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| project | [Project](#type-project) | false | — | the first project loaded |
| projects | [Array of Project](#type-array-of-project) | false | — | array of all projects loaded |
| rpcResponse | [RPCResponse](#type-rpcresponse) | false | — | server response |

---
## Method: Callbacks.ExpandSectionCallback

### Description
Callback to execute after the section has been expanded.

---
## Method: Callbacks.FormattedTimingDataCallback

### Description
Callback fired after a call to [RPCManager.getFormattedTimingData](RPCManager.md#classmethod-rpcmanagergetformattedtimingdata) to report the formatted timing data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [String](#type-string) | false | — | The formatted timing data. |

---
## Method: Callbacks.TabIndexUpdatedCallback

### Description
A notification [Callback](../main.md#type-callback) fired by the TabIndexManager to allow application code to react to the numeric tab-index of some registered target being modified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | the ID String passed to [TabIndexManager.addTarget](TabIndexManager.md#classmethod-tabindexmanageraddtarget) when the callback was registered. |

---
## Method: Callbacks.DataURLCallback

### Description
Callback for [DrawPane.getDataURL](DrawPane.md#method-drawpanegetdataurl).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataURL | [String](#type-string) | false | — | the data URL |

---
## Method: Callbacks.RemoteWindowCallback

### Description
Callback reporting a change to a [RemoteWindow](RemoteWindow.md#class-remotewindow), such as it moving.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| remoteWindow | [RemoteWindow](#type-remotewindow) | false | — | window affected |

---
## Method: Callbacks.DateRangeCallback

### Description
Callback for [DateRangeDialog.askForRange](DateRangeDialog.md#classmethod-daterangedialogaskforrange).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criterion | [Criterion](#type-criterion) | false | — | criterion representing the selected range |

---
## Method: Callbacks.GetFileCallback

### Description
Callback fired when [DataSource.getFile](DataSource.md#method-datasourcegetfile) completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | A [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data. |
| data | [String](#type-string) | false | — | The file contents, or null if there was an error (such as file not found). |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The [DSRequest](../main_2.md#object-dsrequest) that was sent. |

### Groups

- fileSource

---
## Method: Callbacks.ValidationStatusCallback

### Description
A [Callback](../main.md#type-callback) to evaluate when form validation completes.

The available parameters are:

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errorMap | [Map](#type-map) | false | — | null if validation succeeded for all fields, or an object mapping field names to the associated errors, for those fields that failed validation. |

---
## Method: Callbacks.RemoteWindowErrorCallback

### Description
Callback reporting a failure in a [RemoteWindow](RemoteWindow.md#class-remotewindow) operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| remoteWindow | [RemoteWindow](#type-remotewindow) | false | — | window affected |
| errorMessage | [String](#type-string) | false | — | error message |

---
## Method: Callbacks.ValidatorActionCallback

### Description
[Callback](../main.md#type-callback) required for the property [ValidatorDefinition.action](ValidatorDefinition.md#attr-validatordefinitionaction).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [boolean](../main.md#type-boolean) | false | — | The result of the validator. The value will be null if the validator was skipped because of conditional criteria. |
| item | [DataSourceField](#type-datasourcefield)|[FormItem](#type-formitem) | false | — | FormItem or DataSourceField on which this validator was declared. NOTE: FormItem will not be available during a save performed without a form (eg programmatic save) or if the field is not available in the form. |
| validator | [Validator](#type-validator) | false | — | Validator declaration from eg [DataSourceField.validators](DataSourceField.md#attr-datasourcefieldvalidators). |
| record | [Record](#type-record) | false | — | Record that was validated |
| component | [DataBoundComponent](#type-databoundcomponent) | false | — | The DataBoundComponent holding the item such DynamicForm or ListGrid. |

---
## Method: Callbacks.PrintCanvasCallback

### Description
Callback executed when a [supplied html](PrintCanvas.md#method-printcanvassethtml) is rendered into a printCanvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| printPreview | [PrintCanvas](#type-printcanvas) | false | — | The canvas being printed. |

---
## Method: Callbacks.MessagingCallback

### Description
Callback executed when a message is sent to a channel that you have [subscribed](Messaging.md#classmethod-messagingsubscribe) to.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Any](#type-any) | false | — | data contained in the message |

---
## Method: Callbacks.HideSectionCallback

### Description
Callback to execute after the section has been hidden.

---
## Method: Callbacks.RowCountCallback

### Description
Callback fired when ResultSet.fetchRowCount() completes

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| resultSet | [ResultSet](#type-resultset) | false | — | the [ResultSet](ResultSet.md#class-resultset) resultSet that issued the row-count fetch request. |
| dsResponse | [DSResponse](#type-dsresponse) | false | — | the [DSResponse](DSResponse.md#class-dsresponse) from the fetch request. May be null if the row count fetch was invalidated before the server responded |
| invalidated | [boolean](../main.md#type-boolean) | false | — | boolean indicating whether the rowCountFetch request was invalidated. This parameter will be true if, after the row count fetch request was issued, the criteria were changed, the cache was invalidated or the rowCount status has changed since the fetch was initiated. Calling [ResultSet.fetchRowCount](ResultSet.md#method-resultsetfetchrowcount) before a row count fetch has completed will also invalidate the previous row count fetch. In any of these cases the row count will not be updated by this fetch operation. |

### Groups

- rowRangeDisplay

---
## Method: Callbacks.HiliteViaAIResultCallback

### Description
Callback fired asynchronously with the result of a [hilite-via-AI operation](#method-hiliteviaai).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [HiliteViaAIResult](#type-hiliteviaairesult) | false | — | The result. |

---
## Method: Callbacks.Function

### Description
Generic callback interface.

---
## Method: Callbacks.ClientOnlyDataSourceCallback

### Description
Generic callback interface.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| clientOnly | [DataSource](#type-datasource) | false | — | Client only Data Source. |

---
## Method: Callbacks.SetValueByDisplayValueCallback

### Description
Callback fired when [FormItem.setValueByDisplayValue](FormItem.md#method-formitemsetvaluebydisplayvalue) completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| success | [boolean](../main.md#type-boolean) | false | — | True if the value was successfully set, false otherwise |
| value | [Any](#type-any) | false | — | If success is true, contains the mapped value that was set. If success is false, contains an error message string. |

---
