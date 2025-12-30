# Callbacks Documentation

[← Back to API Index](../reference.md)

---

## Class: Callbacks

### Description
This object cannot be used; it exists for documentation purposes only as a place to put documentation for callback methods, such as the callback for [DataSource.fetchData()](#method-callbacksdscallback).

---
## Method: Callbacks.HasFileVersionCallback

### Description
A [Callback](../reference.md#type-callback) fired when [DataSource.hasFileVersion](DataSource.md#method-datasourcehasfileversion) completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | A [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data. |
| data | [boolean](../reference.md#type-boolean) | false | — | Whether the file version exists. |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The [DSRequest](../reference.md#object-dsrequest) that was sent. |

### Groups

- fileSource

---
## Method: Callbacks.LoadScreenCallback

### Description
A [Callback](../reference.md#type-callback) to evaluate when a screen is loaded via [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| screen | [Canvas](#type-canvas) | true | — | The last top-level component loaded |
| rpcResponse | [RPCResponse](#type-rpcresponse) | true | — | — |
| suppressedGlobals | [Map](#type-map) | true | — | A collection of suppressed globals. |

---
## Method: Callbacks.PaletteNodeCallback

### Description
Callback fired with the [PaletteNodes](../reference_2.md#object-palettenode) obtained asynchronously.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNodes | [Array of PaletteNode](#type-array-of-palettenode) | false | — | an array of PaletteNodes |

---
## Method: Callbacks.HasFileCallback

### Description
A [Callback](../reference.md#type-callback) fired when [DataSource.hasFile](DataSource.md#method-datasourcehasfile) completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | A [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data. |
| data | [boolean](../reference.md#type-boolean) | false | — | Whether the file exists. |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The [DSRequest](../reference.md#object-dsrequest) that was sent. |

### Groups

- fileSource

---
## Method: Callbacks.CanPlayCallback

### Description
A [Callback](../reference.md#type-callback) fired when [Sound.load](Sound.md#method-soundload) completes.

---
## Method: Callbacks.GetFileVersionCallback

### Description
Callback fired when [DataSource.getFileVersion](DataSource.md#method-datasourcegetfileversion) completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | A [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data. |
| data | [String](#type-string) | false | — | The file contents, or null if there was an error (such as file not found). |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The [DSRequest](../reference.md#object-dsrequest) that was sent. |

### Groups

- fileSource

---
## Method: Callbacks.RPCCallback

### Description
A [Callback](../reference.md#type-callback) to evaluate when an RPCRequest completes.

Parameters passed to this callback are:

*   rpcResponse: an [RPCResponse](RPCResponse.md#class-rpcresponse) encapsulating the server response to your request
*   data: just the "data" property from the RPCResponse, for convenience
*   rpcRequest: the [RPCRequest](../reference.md#object-rpcrequest) that was sent. You can use [RPCRequest.clientContext](RPCRequest.md#attr-rpcrequestclientcontext) to track state during the server turnaround.

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

- [RPCRequest](../reference.md#object-rpcrequest)
- [RPCResponse](RPCResponse.md#class-rpcresponse)

---
## Method: Callbacks.CollapseSectionCallback

### Description
Callback to execute after the section has been collapsed.

---
## Method: Callbacks.PlaybackCompleteCallback

### Description
A [Callback](../reference.md#type-callback) fired when [Sound.play](Sound.md#method-soundplay) completes.

---
## Method: Callbacks.ExpandSectionCallback

### Description
Callback to execute after the section has been expanded.

---
## Method: Callbacks.TabIndexUpdatedCallback

### Description
A notification [Callback](../reference.md#type-callback) fired by the TabIndexManager to allow application code to react to the numeric tab-index of some registered target being modified.

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
## Method: Callbacks.ValidatorConditionCallback

### Description
[Callback](../reference.md#type-callback) required for the property [Validator.condition](Validator.md#attr-validatorcondition) and [ValidatorDefinition.condition](ValidatorDefinition.md#attr-validatordefinitioncondition).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [DataSourceField](#type-datasourcefield)|[ListGridField](#type-listgridfield)|[FormItem](#type-formitem) | false | — | FormItem, DataSourceField or ListGridField on which this validator was declared. NOTE: FormItem will not be available during a save performed without a form (eg programmatic save) or if the field is not available in the form. |
| validator | [Validator](#type-validator) | false | — | Validator declaration from eg [DataSourceField.validators](DataSourceField.md#attr-datasourcefieldvalidators). |
| value | [Any](#type-any) | false | — | value to validate |
| record | [Object](../reference_2.md#type-object) | false | — | Field values for record being validated. |
| additionalContext | [Object](../reference_2.md#type-object) | false | — | Object containing extra context which may be useful to the condition function. Contains the following properties:  
component: the DynamicForm or ListGrid being validated  
rowNum: the row number of the cell being validated (only if component is a ListGrid)  
colNum: the column number of the cell being validated (only if component is a ListGrid) |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the value passed validation. True for passed, false for fail.

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
| dsRequest | [DSRequest](#type-dsrequest) | false | — | The [DSRequest](../reference.md#object-dsrequest) that was sent. |

### Groups

- fileSource

---
## Method: Callbacks.ValidationStatusCallback

### Description
A [Callback](../reference.md#type-callback) to evaluate when form validation completes.

The available parameters are:

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| errorMap | [Map](#type-map) | false | — | null if validation succeeded for all fields, or an object mapping field names to the associated errors, for those fields that failed validation. |

---
## Method: Callbacks.ShiftFocusCallback

### Description
A [Callback](../reference.md#type-callback) fired by the TabIndexManager when application code or user action attempts to synthetically shift focus to some registered target. See [TabIndexManager.shiftFocus](TabIndexManager.md#classmethod-tabindexmanagershiftfocus).

A typical implementation will shift focus to some native element associated with the registered target, or if this is not currently possible, return false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | The ID String passed to [TabIndexManager.addTarget](TabIndexManager.md#classmethod-tabindexmanageraddtarget) when the callback was registered. |

### Returns

`[boolean](../reference.md#type-boolean)` — Return true if focus could be successfully moved to the desired target. Returning false indicates the target could not accept focus and will often cause the TabIndexManager to find the next registered target and attempt to shift focus there.

---
## Method: Callbacks.DSCallback

### Description
Callback fired when DataSource methods that send DSRequests complete (such as [DataSource.fetchData](DataSource.md#method-datasourcefetchdata)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | a [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data |
| data | [Any](#type-any) | false | — | data returned to satisfy the DataSource request. See the [DataSource operations](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations) topic for expected results for each type of DataSource operation |
| dsRequest | [DSRequest](#type-dsrequest) | false | — | the [DSRequest](../reference.md#object-dsrequest) that was sent. You can use [DSRequest.clientContext](DSRequest.md#attr-dsrequestclientcontext) to track state during the server turnaround. |

---
## Method: Callbacks.ExportImageCallback

### Description
Callback for [RPCManager.exportImage](RPCManager.md#classmethod-rpcmanagerexportimage).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| imageData | [String](#type-string) | false | — | image data from the server, in base64 format |

---
## Method: Callbacks.ValidatorActionCallback

### Description
[Callback](../reference.md#type-callback) required for the property [ValidatorDefinition.action](ValidatorDefinition.md#attr-validatordefinitionaction).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| result | [boolean](../reference.md#type-boolean) | false | — | The result of the validator. The value will be null if the validator was skipped because of conditional criteria. |
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
## Method: Callbacks.AnimationCallback

### Description
A [Callback](../reference.md#type-callback) called when the move completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| earlyFinish | [boolean](../reference.md#type-boolean) | false | — | true if the animation was cut short. To quit an animation early, simply call the non-animated version of the same API, so for example call [Canvas.hide](Canvas.md#method-canvashide) to cut short an animation from [Canvas.animateHide](Canvas.md#method-canvasanimatehide) already in progress. |

---
## Method: Callbacks.GetFieldValueCallback

### Description
[Callback](../reference.md#type-callback) required for the property [DataSourceField.getFieldValue](DataSourceField.md#attr-datasourcefieldgetfieldvalue).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Object](../reference_2.md#type-object)|[XMLElement](../reference.md#type-xmlelement) | false | — | record object selected from web service response data by [recordXPath](OperationBinding.md#attr-operationbindingrecordxpath) |
| value | [Any](#type-any) | false | — | default value derived by the method described in [DataSourceField.valueXPath](DataSourceField.md#attr-datasourcefieldvaluexpath) |
| field | [DataSourceField](#type-datasourcefield) | false | — | DataSourceField definition |
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | name of the DataSource field |

### Groups

- clientDataIntegration

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
## Method: Callbacks.RPCQueueCallback

### Description
Callback to fire when a queue of requests sent via {@link com.smartgwt.client.rpc.RPCManager#sendQueue(RPCQueueCallback)} returns.

Note that the Array of RPCResponses passed to this callback will actually be DSResponse objects for any requests that were actually DSRequests.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| response | [Array of RPCResponse](#type-array-of-rpcresponse) | false | — | array of responses returned from the sent queue of requests |

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
## Method: Callbacks.ProcessCallback

### Description
A [Callback](../reference.md#type-callback) to evaluate when an {Process.loadProcess} method completes.

Loaded process passed as a parameter to this callback are:

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dsResponse | [DSResponse](#type-dsresponse) | false | — | a [DSResponse](DSResponse.md#class-dsresponse) instance with metadata about the returned data |
| process | [Process](#type-process) | false | — | — |

### See Also

- [Process](Process.md#class-process)
- [RPCResponse](RPCResponse.md#class-rpcresponse)

---
## Method: Callbacks.ShowSectionCallback

### Description
Callback to execute after the section has been shown.

---
