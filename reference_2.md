# SmartClient API Reference (13.0) (Part 2 of 2)

[← Back to Part 1](reference.md)

---

## Type: AnimateShowEffectId

### Description
String specifying effect to apply during an animated show or hide.

### Values

| Value | Description |
|-------|-------------|
| "slide" | content slides into or out of view as the widget grows or shrinks |
| "wipe" | content is revealed or wiped as the widget grows or shrinks |
| "fade" | widget's opacity smoothly fades into or out of view |
| "fly" | widget moves into position from offscreen |

---
## Type: Autofit

### Description
Possible values to change the behavior of how data will fill the ListGrid.

### Values

| Value | Description |
|-------|-------------|
| "vertical" | expand vertically to accommodate records. |
| "horizontal" | expand horizontally to accommodate fields. |
| "both" | expand horizontally and vertically to accommodate content. |

### Groups

- autoFitData

---
## Type: AutoFitIconFieldType

### Description
How should fields of [type:"icon"](#type-listgridfieldtype) be sized by default?

### Values

| Value | Description |
|-------|-------------|
| "none" | Apply no special sizing to icon fields - treat them like any other field in the grid |
| "iconWidth" | size the field to accommodate the width of the icon |
| "title" | size the field to accommodate the title (or the width of the icon if it exceeds the width of the title. |

### Groups

- autoFitFields

---
## Type: AutoFitWidthApproach

### Description
How should field width be determined when [ListGridField.autoFitWidth](classes/ListGridField.md#attr-listgridfieldautofitwidth) is true?

### Values

| Value | Description |
|-------|-------------|
| "value" | Size field to fit to the data value(s) contained in the field. |
| "title" | Size field to fit the field title |
| "both" | Size field to fit either the field title or the data values in the field (whichever requires more space). |

### Groups

- autoFitFields

---
## Type: AutoTestLocator

### Description
An autoTestLocator is an xpath-like string used by the AutoTest subsystem to robustly identify DOM elements within a SmartClient application.

Typically AutoTestLocators will not be hand-written - they can be retrieved by a call to [AutoTest.getLocator](classes/AutoTest.md#classmethod-autotestgetlocator), or by clicking on the page after invoking the [AutoTest.installLocatorShortcut](classes/AutoTest.md#classmethod-autotestinstalllocatorshortcut) method.

### Groups

- autoTest

---
## Type: Axis

### Description
An axis or "side" of a table.

### Values

| Value | Description |
|-------|-------------|
| "row" | Row axis |
| "column" | Column axis |

---
## Type: BackgroundRepeat

### Description
Possible values for [Canvas.backgroundRepeat](classes/Canvas.md#attr-canvasbackgroundrepeat).

### Values

| Value | Description |
|-------|-------------|
| Canvas.REPEAT | Tile the background image horizontally and vertically. |
| Canvas.NO_REPEAT | Don't tile the background image at all. |
| Canvas.REPEAT_X | Repeat the background image horizontally but not vertically. |
| Canvas.REPEAT_Y | Repeat the background image vertically but not horizontally. |

### Groups

- appearance

---
## Type: ConnectorStyle

### Description
Supported styles of connector styles.

### Values

| Value | Description |
|-------|-------------|
| "diagonal" | Center segment is drawn diagonally between tail connector segments |
| "rightAngle" | Center segment is drawn perpendicular to tail connector segments |

### Groups

- line

---
## Type: Constant

### Description
A string used to define the value of a class attribute when it's referenced as one of the potential values of an enum type. For example, one documented value of [Overflow](#type-overflow) is [Canvas.HIDDEN](classes/Canvas.md#classattr-canvashidden), which is itself a class attribute with type `Constant` and the value "hidden".

---
## Type: Criteria

### Description
Criteria for selecting only a matching set of records from a DataSource. Criteria can be applied on the client and server. Unless configured otherwise, criteria will generally be applied client-side by [ResultSet](classes/ResultSet.md#class-resultset)s via [ResultSet.applyFilter](classes/ResultSet.md#method-resultsetapplyfilter).

Client- and server-side systems built into SmartClient understand two criteria formats by default: simple key-value pairs (Criteria) or the [AdvancedCriteria](#object-advancedcriteria) format.

Simple key-value Criteria are represented via a JavaScript Object where each property specifies the name and required value for a field. Multiple legal values for a field can be provided as an Array. For example:

```
 var criteria = {
    field1 : "value1",
    field2 : ["value2", "value3"]
 }
 
```
Would select all records where field1 has value "value1" and where field2 has _either_ "value2" or "value3".

Use [DataSource.combineCriteria](classes/DataSource.md#classmethod-datasourcecombinecriteria) to combine two Criteria objects (including Criteria and AdvancedCriteria) or [DataSource.convertCriteria](classes/DataSource.md#classmethod-datasourceconvertcriteria) to convert simple Criteria to the AdvancedCriteria format.

When writing custom client and server-side filtering logic, criteria must be a JavaScript Object but the properties of that Object can contain whatever data you want. When sent to the SmartClient server, the Java representation of the criteria is described [here](classes/RPCRequest.md#attr-rpcrequestdata). When sent to other servers, the [operationBinding.dataProtocol](reference_2.md#type-dsprotocol) affects the format.

### See Also

- [CriteriaPolicy](#type-criteriapolicy)

---
## Type: CriteriaCombineOperator

### Description
The logical operator to use when combining criteria objects with the [DataSource.combineCriteria](classes/DataSource.md#classmethod-datasourcecombinecriteria) method.

### Values

| Value | Description |
|-------|-------------|
| "and" | — |
| "or" | — |

---
## Type: CSSColor

### Description
CSS color specification applied to a specific HTML element on this page.

This is a string matching the syntax as specified in CSS1, and can be formatted in one of the following ways:

*   A keyword color, “white”
*   Six-digit hex notation, “#ffffff”
*   Three-digit hex notation, “#fff”
*   8-bit decimal notation, “rgb(255, 255, 255)”
*   Percentage notation, “rgb(100%, 100%, 100%)”

Note that when working with [FacetChart](classes/FacetChart.md#class-facetchart)s, it's required that colors be specified using the six-digit hex format listed above, rather than any of the others, since the Framework needs to perform math on the subfields. Affected properties include [FacetChart.dataColors](classes/FacetChart.md#attr-facetchartdatacolors), and affected methods include overrides of [FacetChart.getDataColor](classes/FacetChart.md#method-facetchartgetdatacolor) and [FacetChart.getDataLineColor](classes/FacetChart.md#method-facetchartgetdatalinecolor).

### Groups

- appearance

---
## Type: CSSText

### Description
A String of CSS that can be added directly to a `style` attribute.

---
## Type: DataPath

### Description
String specifying a nested data field structure.

**NOTE: the dataPath feature is intended to help certain legacy architectures, such as systems that work in terms of exchanging large messages with several different entity types in one message, and are incapable of providing separate access to each entity type. Don't use dataPath if this is not your situation.**

_If you are not forced by legacy issues to use hierarchical data structures, we recommend:_

_*   If a subobject exists just to bundle several related fields together, and is not a separate entity (cannot be separately created or separately referenced by other objects), "flatten" the fields using features such as [DataSourceField.valueXPath](classes/DataSourceField.md#attr-datasourcefieldvaluexpath).
*   If a subobject is actually a separate entity, make a DataSource for it and use operations on that DataSource to load and modify it.
    
    For example, when representing a sales order with a "deliveryAddress" (consisting of multiple fields), you'd typically want an "orders" dataSource to define the fields for the order as a whole, and an "address" dataSource to define the structure of the deliveryAddress object.
    
    It may seem like a good idea to work with a single hierarchical order object, where the "deliveryAddress" attribute is set to a sub-object that matches the structure defined in the "address" dataSource. DataPaths could be used to extract individual address fields for editing in a form alongside other fields from the order, and edits would be saved via a simple "add" or "update" operation, passing in the modified nested data object.
    
    In fact, this has a number of disadvantages. Since there is no call to the "update" operation on the "address" subobject, the address will be modified without the normal features of a dataSource update. You can't specify [security rules](classes/DataSource.md#attr-datasourcerequiresauthentication), [DMI](kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) logic, [request modifiers](#object-dsrequestmodifier), and no logging or [auditing](classes/DataSource.md#attr-datasourceaudit) will run.  
    The same "bypassing" problem occurs, in perhaps worse form, if a subobject does not yet exist and the framework creates it automatically, skipping a DataSource "add" operation that may have established defaults, not been allowed for the user, etc.
    
    Loading and saving nested data objects as a single hierarchical block also offers no advantages in terms of performance or simplicity.  
    The [queuing](classes/RPCManager.md#classmethod-rpcmanagerstartqueue) system makes it extremely easy to load and save multiple types of entities in a single HTTP request, and takes far less code to implement properly as multiple DataSource operations, with equivalent or better performance.
    
    Loading arrays of related objects (such as all LineItems in an Order) as a hierarchical object has the further drawback that paging cannot be used for the list of related objects, and all such objects will not participate in [automatic cache synchronization](classes/ResultSet.md#class-resultset).
    _

_In short, we do not recommend structuring your data as a hierarchy of nested data objects and using dataPath to navigate these structures unless you are forced to by a legacy system that doesn't allow separate operations on each entity type._

**How to use dataPaths**

Each dataPath string is a slash-delimited set of field identifiers, for example `"id1/id2/id3"`. DataPaths may be applied directly to a [component](classes/Canvas.md#attr-canvasdatapath), and/or to a databound component field specification. A datapath denotes a path to a nested field value in a hierarchical structure, giving developers the opportunity to easily view or edit nested data structures. Specifically:

*   if the component is viewing or editing a record, the value for fields will be derived from a nested structure of records
*   if the component is bound to a dataSource, field attributes may be picked up by following the dataPath to a field definition on another dataSource

**Examples:**  
If a dynamicForm is defined with the following fields:
```
    [
      { name:"name" },
      { name:"street", dataPath:"address/street" }
    ]
 
```
If the `"name"` field is set to _"Joe Smith"_ and the `"street"` field is set to _"1221 High Street"_, when the values for this form are retrieved via a `getValues()` call they will return an object in the following format:
```
    {name:"Joe Smith", address:{street:"1221 High Street"}}
 
```

For databound components, dataPath also provides a way to pick up field attributes from nested dataSources. Given the following dataSource definitions:

```
  isc.DataSource.create({
      ID:"contacts",
      fields:[
          {name:"name"},
          {name:"email"},
          {name:"organization"},
          {name:"phone"},
          {name:"address", type:"Address"}
      ]
  });
 
  isc.DataSource.create({
      ID:"Address",
      fields:[
          {name:"street"},
          {name:"city"},
          {name:"state"},
          {name:"zip"}
      ]
  });
  
```
and a databound component bound to the 'contacts' dataSource, specifying a field with a dataPath of `"address/street"` would ensure the field attributes were derived from the "street" field of the 'Address' dataSource.

dataPaths are also cumulative. In other words if a component has a specified dataPath, the dataPath of any fields it contains will be appended to that component level path when accessing data. For example the following form:

```
 isc.DynamicForm.create({
     dataPath:"contact",
     fields:[
          {dataPath:"address/email"}
     ]
 });
 
```
Might be used to edit a data structure similar to this:
```
{contact:{name:'Ed Jones', address:{state:"CA", email:"ed@ed.jones.com"}}}
```
Nested canvases can also have dataPaths specified, which will similarly be combined. See the [Canvas.dataPath](classes/Canvas.md#attr-canvasdatapath) attribute for more information and examples of this.

### See Also

- [Canvas.ruleScope](classes/Canvas.md#attr-canvasrulescope)

---
## Type: DateFieldLayout

### Description
The direction in which an item should lay out it's fields.

### Values

| Value | Description |
|-------|-------------|
| "horizontal" | fields are placed horizontally |
| "vertical" | fields are placed vertically |

---
## Type: DefaultSampleRecord

### Description
Some interfaces, for example the [FieldPicker](classes/FieldPicker.md#class-fieldpicker) and [HiliteEditor](classes/HiliteEditor.md#class-hiliteeditor) widgets, can use data from an associated DataBoundComponent to express live sample values at runtime.

### Values

| Value | Description |
|-------|-------------|
| "first" | Uses the first record in the DataBoundComponent as sample data |
| "firstOpenLeaf" | Uses the first open leaf-node in the DataBoundComponent as sample data |

---
## Type: Direction

### Description
—

### Values

| Value | Description |
|-------|-------------|
| Canvas.UP | above |
| Canvas.DOWN | below |
| Canvas.LEFT | to the left of |
| Canvas.RIGHT | to the right of |

### Groups

- appearance

---
## Type: DragAppearance

### Description
Different types of effects for showing dragging behavior.

### Values

| Value | Description |
|-------|-------------|
| "none" | No default drag appearance is indicated. Your custom dragging routines should implement some behavior that indicates that the user is in a dragging situation, and where the mouse is. |
| "tracker" | A "drag tracker" object is automatically shown and moved around with the mouse. This is generally set to an icon that represents what is being dragged. The default tracker is a 10 pixel black square, but you can customize this icon. This dragAppearance is not recommended for use with drag resizing or drag moving. |
| "target" | The target object is actually moved, resized, etc. in real time. This is recommended for drag repositioning, but not for drag resizing of complex objects. |
| "outline" | An outline the size of the target object is moved, resized, etc. with the mouse. This is recommended for drag resizing, especially for objects that take a significant amount of time to draw. |

### Groups

- dragdrop

---
## Type: DrawPosition

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "beforeBegin" | insert before the target element |
| "afterBegin" | insert as the target element's first child |
| "beforeEnd" | insert as the target element's last child |
| "afterEnd" | insert after the target element |
| "replace" | replace the target element |

---
## Type: DSCallback

### Description
A [Callback](#type-callback) to evaluate when a DataSource request completes.

The parameters available in the DSCallback expression are:

*   dsResponse: a [DSResponse](classes/DSResponse.md#class-dsresponse) instance with metadata about the returned data
*   data: data returned to satisfy the DataSource request. See the [DataSource operations](kb_topics/dataSourceOperations.md#kb-topic-datasource-operations) topic for expected results for each type of DataSource operation
*   dsRequest: the [DSRequest](#object-dsrequest) that was sent. You can use [DSRequest.clientContext](classes/DSRequest.md#attr-dsrequestclientcontext) to track state during the server turnaround.

For example, if you had a DynamicForm with ID "myForm" and you wanted to retrieve a record from a DataSource "myUsers", where each record has a "userId" field:
```
     myUsers.fetchData({ userId : "fred" }, "myForm.setValues(data)");
 
```
or
```
     myUsers.fetchData({ userId : "fred" }, function (dsResponse, data, dsRequest) {
                                              myForm.setValues(data);
                                            });
 
```

Note that if the request encounters a low-level error (such as 500 server error), by default the callback will **not** be fired, instead, [DataSource.handleError](classes/DataSource.md#method-datasourcehandleerror) is called to invoke the default system-wide error handling. Set [willHandleError](classes/RPCRequest.md#attr-rpcrequestwillhandleerror):true to have your callback invoked regardless of whether there are errors, however, make sure your callback properly handles malformed responses when [DSResponse.status](classes/DSResponse.md#attr-dsresponsestatus) is non-zero.

---
## Type: DSProtocol

### Description
[OperationBinding.dataProtocol](classes/OperationBinding.md#attr-operationbindingdataprotocol) affects how the data in the DSRequest ([DSRequest.data](classes/DSRequest.md#attr-dsrequestdata)) is sent to the [DataSource.dataURL](classes/DataSource.md#attr-datasourcedataurl). Listed below are the valid values for [OperationBinding.dataProtocol](classes/OperationBinding.md#attr-operationbindingdataprotocol) and their behavior.

Note that, when using the SmartClient server, data is automatically translated from JavaScript to Java according to the rules described [here](classes/RPCRequest.md#attr-rpcrequestdata); dataProtocol does not apply and is ignored.

If you are integrating with a [REST](classes/RestDataSource.md#class-restdatasource) server that requires the more obscure [RPCRequest.httpMethod](classes/RPCRequest.md#attr-rpcrequesthttpmethod)s of "PUT", "DELETE" or "HEAD", you can specify these httpMethod settings via [OperationBinding.requestProperties](classes/OperationBinding.md#attr-operationbindingrequestproperties). dataProtocol settings that mention "GET" or "POST" are compatible with these additional HTTP methods as well. Typical [operationBindings](classes/DataSource.md#attr-datasourceoperationbindings) for a REST server that uses "PUT" and "DELETE" are as follows:

```
    operationBindings:[
       {operationType:"fetch", dataProtocol:"getParams"},
       {operationType:"add", dataProtocol:"postParams"},
       {operationType:"remove", dataProtocol:"getParams", requestProperties:{httpMethod:"DELETE"}},
       {operationType:"update", dataProtocol:"postParams", requestProperties:{httpMethod:"PUT"}}
    ],
 
```

### Values

| Value | Description |
|-------|-------------|
| "getParams" | Data is added to the dataURL, with each property in the data becoming an HTTP parameter, eg http://service.com/search?keyword=foo |
| "postParams" | Data is POST'd to the dataURL, with each property becoming an HTTP parameter, exactly as an HTML form would submit them if it had one input field per property in the data. |
| "postJSON" | Data is serialized as a JSON string and POST'd to the dataURL. |
| "postXML" | Data is serialized as XML via [DataSource.xmlSerialize](classes/DataSource.md#method-datasourcexmlserialize) and POST'd as the HTTP request body with contentType "text/xml". |
| "soap" | Data is serialized as XML via [DataSource.xmlSerialize](classes/DataSource.md#method-datasourcexmlserialize), wrapped in a SOAP envelope, and POST'd as the HTTP request body with contentType "text/xml". Generally only used in connection with a [WSDL web service](kb_topics/wsdlBinding.md#kb-topic-wsdl-binding). |
| "postMessage" | dsRequest.data is assumed to be a String set up by [DataSource.transformRequest](classes/DataSource.md#method-datasourcetransformrequest) and is POST'd as the HTTP request body. |
| "clientCustom" | This setting entirely bypasses the SmartClient comm system. Instead of the DataSource sending an HTTP request to a URL, the developer is expected to implement [DataSource.transformRequest](classes/DataSource.md#method-datasourcetransformrequest) to perform their own custom logic, and then call [DataSource.processResponse](classes/DataSource.md#method-datasourceprocessresponse) to handle the results of this action. This `dataProtocol` setting can be used to implement access to in-browser resources such as HTML5 "localStorage", native APIs available to applications [packaged as native applications](kb_topics/mobileDevelopment.md#kb-topic-mobile-application-development), or to implement the [DataSource Facade pattern](kb_topics/dsFacade.md#kb-topic-datasource-facade-pattern). |

### Groups

- clientDataIntegration

### See Also

- [OperationBinding.dataProtocol](classes/OperationBinding.md#attr-operationbindingdataprotocol)

---
## Type: DSServerType

### Description
Indicates what SmartClient Server will do with a DataSource request if you call dsRequest.execute() in server code.

If you use a Java-based persistence layer not provided by SmartClient, such as EJB or your own custom object model, you don't need to set `dataSource.serverType` and should follow the [integration instructions](kb_topics/serverDataIntegration.md#kb-topic-server-datasource-integration).

### Values

| Value | Description |
|-------|-------------|
| "sql" | Use SmartClient's [built-in SQL connectors](kb_topics/sqlDataSource.md#kb-topic-sql-datasources) to talk directly to relational databases. |
| "hibernate" | Use Hibernate, either using a real mapped bean or by automatically generating a Hibernate configuration based on a SmartClient DataSource file (_dataSourceID_.ds.xml). See [hibernateIntegration](kb_topics/hibernateIntegration.md#kb-topic-integration-with-hibernate) for details. |
| "jpa" | Use SmartClient's built-in JPA 2.0 connector. |
| "jpa1" | Use SmartClient's built-in JPA 1.0 connector. |
| "generic" | Requests will be delivered to the server and you are expected to write Java code to create a valid response. Throws an error if the server side method dsRequest.execute() is called. This is appropriate if you intend an entirely custom implementation, and you want an error thrown if there is an attempt to call an operation you have not implemented. |
| "projectFile" | Requests will be delivered to the server and processed as [FileSource operations](kb_topics/fileSource.md#kb-topic-filesource-operations), using directories or other DataSources which you configure via [DataSource.projectFileKey](classes/DataSource.md#attr-datasourceprojectfilekey) or [DataSource.projectFileLocations](classes/DataSource.md#attr-datasourceprojectfilelocations) |

### Groups

- serverDataIntegration

---
## Type: DynamicString

### Description
A [dynamic string](kb_topics/dynamicStrings.md#kb-topic-dynamic-strings).

### Groups

- dynamicStrings

---
## Type: ElementWaitStyle

### Description
How should [AutoTest.waitForElement](classes/AutoTest.md#classmethod-autotestwaitforelement) determine that the application is ready to retrieve the element?

Note: In most cases `"system"` is the appropriate setting. This will wait for standard SmartClient-initiated asychronous actions to complete, including timer-instantiated actions such as [delayed redraws](classes/Canvas.md#method-canvasmarkforredraw) or actions configured through the [Timer class](classes/Timer.md#class-timer), and oustanding [RPC Requests](classes/RPCManager.md#class-rpcmanager). If the locator cannot be resolved to a clickable element after system quiescence, this usually implies that it will not ever resolve, and there's no need to wait for the timeout to complete and slow down your test suite.

The only time you'd want to use `"element"` would be if your application relies on some asynchronous event that isn't tracked by the SmartClient system. Examples might include waiting for asynchronous actions instantiated by a third-party tool on the page, or waiting for a server notification to come in through the [RealtimeMessaging](#realtimemessaging) system.

### Values

| Value | Description |
|-------|-------------|
| "system" | use [AutoTest.waitForSystemDone](classes/AutoTest.md#classmethod-autotestwaitforsystemdone) to wait for actions to complete, then return the result of [AutoTest.getElement](classes/AutoTest.md#classmethod-autotestgetelement), even if this method doesn't resolve to an element. |
| "element" | wait until [AutoTest.getElement](classes/AutoTest.md#classmethod-autotestgetelement) resolves to an element, and the element is [clickable](classes/AutoTest.md#classmethod-autotestiselementclickable). |

---
## Type: EmbeddedPosition

### Description
How a component should be embedded within its record or cell

### Values

| Value | Description |
|-------|-------------|
| "expand" | component should be placed underneath normal record or cell content, expanding the records. Expanding records can result in variable height rows, in which case [virtualScrolling](classes/ListGrid_1.md#attr-listgridvirtualscrolling) should be enabled. |
| "within" | component should be placed within the normal area of the record or cell. Percentage sizes will be treated as percentages of the record and [Canvas.snapTo](classes/Canvas.md#attr-canvassnapto) positioning settings are also allowed and refer to the rectangle of the record or cell. Note that for components embedded within cells, cell align and vAlign will be used if snapTo is unset (so top / left alignment of cell content will map to snapTo of "TL", etc). |

---
## Type: Encoding

### Description
Form encoding types - these translate to Form ENCTYPE parameters.

### Values

| Value | Description |
|-------|-------------|
| DynamicForm.NORMAL | normal form encoding ("application/x-www-form-urlencoded") |
| DynamicForm.MULTIPART | form encoding for forms with INPUT file elements, that is, forms that upload files ("multipart/form-data") |

### Groups

- submitting

---
## Type: EnumTranslateStrategy

### Description
Determines how Java enums are translated to and from Javascript by the SmartClient server.

### Values

| Value | Description |
|-------|-------------|
| "name" | Translates to/from a String matching the constant name. This is the default if not set. |
| "string" | Translates to/from a String matching the `enum.toString()`. |
| "ordinal" | Translates to/from an integer matching the ordinal number of the constant within the enumeration |
| "bean" | Translates to/from a Javascript object containing one property for each property defined within the enum. The constant itself and the ordinal number are included in the JS object. By default they are called "\_constant" and "\_ordinal", but this can be overridden with the [DataSource.enumOrdinalProperty](classes/DataSource.md#attr-datasourceenumordinalproperty) and [DataSource.enumConstantProperty](classes/DataSource.md#attr-datasourceenumconstantproperty) properties |

### See Also

- [DataSource.enumTranslateStrategy](classes/DataSource.md#attr-datasourceenumtranslatestrategy)

---
## Type: ExpansionComponentPoolingMode

### Description
The method of pooling to employ for [expansionComponents](classes/ListGrid_1.md#attr-listgridcanexpandrecords).

### Values

| Value | Description |
|-------|-------------|
| "destroy" | auto-created, built-in components are destroyed when record are [collapsed](classes/ListGrid_2.md#method-listgridcollapserecord). |
| "none" | all expansion components are deparented from the grid when a record is [collapsed](classes/ListGrid_2.md#method-listgridcollapserecord) but are not destroyed. It is the responsibility of the developer to handle component destruction |

---
## Type: ExportDisplay

### Description
Method to use for displaying the exported data.

### Values

| Value | Description |
|-------|-------------|
| "download" | Show the Save As dialog and download the file |
| "window" | Show the data in a new browser window |
| "return" | Return the data for further programmatic processing in the browser |

---
## Type: ExportFormat

### Description
One of the supported formats for data-export. If you are doing a [client export](classes/ListGrid_1.md#method-listgridexportclientdata) to one of the native spreadsheet formats (xls or ooxml), we also export [hilite-based](#object-hilite) coloring. So, if Hilites are causing a particular cell to be rendered as green text on a blue background, the corresponding cell in the exported spreadsheet document will also be colored that way.

### Values

| Value | Description |
|-------|-------------|
| "xml" | Export data as XML records |
| "json" | Export data as JSON objects. Not allowed as a client-side option. |
| "csv" | Export data in comma-separated format |
| "xls" | Export data in native Microsoft Excel 97 format |
| "ooxml" | Export data in native Microsoft Excel 2007 format (also called XLSX) |
| "custom" | Custom server-side logic will do the export |

---
## Type: ExportImageFormat

### Description
One of the supported formats for image export.

### Values

| Value | Description |
|-------|-------------|
| "png" | Export as PNG |
| "jpeg" | Export as JPEG |

---
## Type: FetchMode

### Description
Mode of fetching records from the server.

Generally, "paged" mode should be used unless the maximum number of records is guaranteed to be small.

### Values

| Value | Description |
|-------|-------------|
| "basic" | All records that match the current filter are fetched. Sorting is performed on the client. |
| "paged" | Only requested ranges of records are fetched, with predictive fetch ahead. Sorting is performed on the server. |
| "local" | All records available from the DataSource are fetched. Filtering by search criteria and sorting are both performed on the client. |

### Groups

- fetching

---
## Type: FieldAppearance

### Description
—

### Values

| Value | Description |
|-------|-------------|
| Validator.READONLY | Show in read-only appearance |
| Validator.HIDDEN | Hide field |
| Validator.DISABLED | Disable field |

---
## Type: FieldAuditMode

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "always" | the field value will be saved for all audited adds and updates, regardless of whether it's changed or present in the update |
| "change" | the field value will be saved for all audited adds, and for updates in which the value changed |
| "never" | the field value will never be saved for any DataSource audit operation |

---
## Type: FieldImportStrategy

### Description
Options for how values in the import dataset (for example, the CSV file) are transformed during import if the field is a [foreignKey](classes/DataSourceField.md#attr-datasourcefieldforeignkey) mapped to a [displayField](classes/DataSourceField.md#attr-datasourcefielddisplayfield)

### Values

| Value | Description |
|-------|-------------|
| "key" | The import process expects values in the import dataset to be the real underlying key values, and performs no transformation |
| "display" | The import process expects values in the import dataset to be display values, and it will transform them to the corresponding underlying keys if found |
| "displayRequired" | Same as "display", but results in [validation error](classes/DataSourceField.md#attr-datasourcefieldimportstrategyfailederrormessage) if corresponding underlying keys were not found |
| "auto" | The import process will attempt to discover the best setting to use, based on the values in the first record, and use that setting for every remaining record in the import dataset |

### See Also

- [DataSourceField.importStrategy](classes/DataSourceField.md#attr-datasourcefieldimportstrategy)

---
## Type: FieldState

### Description
An object containing the stored presentation information for the fields of some dataBoundComponent. Information contained in a `FieldState` object includes the visibility and order of the component's fields.  
Note that this object is a JavaScript string, and may be stored (for example) as a blob on the server for state persistence across sessions.

### Groups

- viewState

---
## Type: FieldType

### Description
The types listed below are built-in types that [databound\\n components](#interface-databoundcomponent) understand and treat specially (using type-specific form controls, validators, formatters, sorting logic, etc).

You can declare custom types via [SimpleType.create()](classes/SimpleType.md#class-simpletype), with settings that will influence DataBound components. You can also create your own subclasses of databound components to add further custom, reusable behaviors based on field.type.

`field.type` can also be the ID of another [DataSource](classes/DataSource.md#class-datasource), which allows you to model nested structures such as XML documents (in fact, [XMLTools.loadXMLSchema](classes/XMLTools.md#classmethod-xmltoolsloadxmlschema) models XML schema in this way). Nested DataSource declarations affect how XML and JSON data is deserialized into JavaScript objects in the [client-side integration](kb_topics/clientDataIntegration.md#kb-topic-client-side-data-integration) pipeline, so that you can load complex XML documents and have them deserialized into a correctly typed nested data structure.

Note: to declare related but _separate_ objects, as in an "Account" object that can be related to both a "Contact" object and "Order" objects, use [DataSourceField.foreignKey](classes/DataSourceField.md#attr-datasourcefieldforeignkey), **not** a nested structure declaration.

### Values

| Value | Description |
|-------|-------------|
| "text" | Generic text, e.g. `"John Doe"`. This is the default field type. Use `field.length` to set length. |
| "boolean" | A boolean value, e.g. `true` |
| "integer" | A whole number, e.g. `123` |
| "float" | A floating point (decimal) number, e.g. `1.23` |
| "date" | A logical date, with no time value (such as a holiday or birthday). Represented on the client as a JavaScript `Date` object where time values are ignored. See [dateFormatAndStorage](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more information on date display and serialization formats. |
| "time" | A time of day, with no date. Represented on the client as a JavaScript `Date` object in UTC/GMT by default (see also [dateFormatAndStorage](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) and the [Time](classes/Time.md#class-time) class). |
| "datetime" | A date and time, accurate to the [second](classes/DataSourceField.md#attr-datasourcefieldstoremilliseconds). Represented on the client as a JavaScript `Date` object. See also [dateFormatAndStorage](kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage). |
| "enum" | A text value constrained to a set of legal values specified by the field's [valueMap](classes/DataSourceField.md#attr-datasourcefieldvaluemap), as though a [ValidatorType](#type-validatortype) of "isOneOf" had been declared. |
| "intEnum" | An enum whose values are numeric. |
| "sequence" | If you are using the SmartClient SQL datasource connector, a `sequence` is a unique, increasing whole number, incremented whenever a new record is added. Otherwise, `sequence` behaves identically to `integer`. This type is typically used with `field.primaryKey` to auto-generate unique primary keys. See also [DataSourceField.sequenceName](classes/DataSourceField.md#attr-datasourcefieldsequencename) and [DataSource.sequenceMode](classes/DataSource.md#attr-datasourcesequencemode) |
| "link" | A string representing a well-formed URL. Some components will render this as an HTML link (using an anchor tag for example). |
| "image" | A string representing a well-formed URL that points to an image. Some components will render an IMG tag with the value of this field as the 'src' attribute to render the image. |
| "binary" | Arbitrary binary data. When this field type is present, three additional fields are automatically generated. They are: `<fieldName>`\_filename, `<fieldName>`\_filesize, and `<fieldName>`\_date\_created where `<fieldName>` is the value of the `name` attribute of this field. These fields are marked as [DataSourceField.hidden](classes/DataSourceField.md#attr-datasourcefieldhidden)`:true` to suppress their rendering by default. You can show one or more of these fields by specifying the field with a `hidden:false` override in the fields array of the databound component. _Stream / view file support for custom DataSources_: a custom DataSource or [DMI](classes/DMI.md#class-dmi) must implement the "viewFile" and "downloadFile" operationTypes and return a single Record with a byte\[\] as the field value for the binary field. For more detail see the overview of [Binary Fields](kb_topics/binaryFields.md#kb-topic-binary-fields). |
| "imageFile" | Binary data comprising an image. Causes [ViewFileItem](#class-viewfileitem) to be used when the field is displayed in a form, allowing the image to optionally be displayed inline. |
| "any" | Fields of this type can contain any data value and have no default formatting or validation behavior. This is useful as the [parent type](classes/SimpleType.md#attr-simpletypeinheritsfrom) for SimpleTypes where you do not want any of the standard validation or formatting logic to be inherited from the standard built-in types. |
| "custom" | Synonymous with "any". |
| "modifier" | Fields of this type are automatically populated by the SmartClient Server with the current authenticated userId as part of "add" and "update" operations. By default, fields of this type are hidden and not editable; the server ignores any value that the client sends in a field of this type. Note that the "authenticated user" can be set explicitly on the server-side `RPCManager` using the setUserId() method, or it can come from the servlet API if you are using its built-in authentication scheme. See the server-side Javadocs for `RPCManager`. |
| "modifierTimestamp" | Fields of this type are automatically populated by the SmartClient Server with the current date and time as part of "add" and "update" operations. By default, fields of this type are hidden and not editable; the server ignores any value that the client sends in a field of this type. |
| "creator" | Fields of this type are automatically populated by the SmartClient Server with the current authenticated userId as part of "add" operations. By default, fields of this type are hidden and not editable; the server ignores any value that the client sends in a field of this type. The notes about type "modifier" also apply to fields of this type. |
| "creatorTimestamp" | Fields of this type are automatically populated by the SmartClient Server with the current date and time as part of an "add" operation (when the record is first created). By default, fields of this type are hidden and not editable; the server ignores any value that the client sends in a field of this type. |
| "password" | Same as "text", but causes [PasswordItem](#class-passworditem) to be used by default for editing (hides typed-in value). |
| "ntext" | A special field type specifically for use with Unicode data in conjunction with the Microsoft SQL Server database. Field type "ntext" implies the use of [sqlStorageStrategy](#attr-datasourcefieldsqlstoragestrategy) "ntext"; other than that, this type is identical to "text" |
| "localeInt" | An integer number with locale-based formatting, e.g. `12,345,678`. See [Localized Number Formatting](#kb-topic-localized-number-formatting) for more info. |
| "localeFloat" | A float number with locale-based formatting, e.g. `12,345.67`. See [Localized Number Formatting](#kb-topic-localized-number-formatting) for more info. |
| "localeCurrency" | A float number with locale-based formatting and using currency symbol, e.g. `$12,345.67`. See [Localized Number Formatting](#kb-topic-localized-number-formatting) for more info. |
| "phoneNumber" | A telephone number. Uses [FormItem.browserInputType](classes/FormItem.md#attr-formitembrowserinputtype) "tel" to hint to the device to restrict input. On most mobile devices that have software keyboards, this cause a specialized keyboard to appear which only allows entry of normal phone numbers. When displayed read-only, a "phoneNumber" renders as an HTML link with the "tel:" URL scheme, which will invoke the native phone dialing interface on most mobile devices. In addition, the CSS style "sc\_phoneNumber" is applied.

By default, "phoneNumber" fields do not include validators, however the following validator definition would limit to digits, dashes and the "+" character: xml:

`<validator type="regexp" expression="^(\\(?\\+?\[0-9\]\*\\)?)?\[0-9\_\\- \\(\\)\]\*$" errorMessage="Phone number should be in the correct format e.g. +#(###)###-##-##" />`

or directly in JavaScript:

```
 {type:"regexp", expression:"^(\\(?\\+?[0-9]*\\)?)?[0-9_\\- \\(\\)]*$", 
     errorMessage:"Phone number should be in the correct format e.g. +#(###)###-##-##"}
 
```
and adding "#" and "\*" to the regular expressions above would allow for users to enter special keys sometimes used for extension numbers or pauses |

### See Also

- [ListGridFieldType](#type-listgridfieldtype)
- [FormItemType](#type-formitemtype)

---
## Type: FireStyle

### Description
Flags to set automatic removal of events from the page event registry.

### Values

| Value | Description |
|-------|-------------|
| null | Call the registered handler any time the event occurs |
| Page.FIRE_ONCE | Call the registered handler the first time the event occurs, then unregister the handler as though [Page.clearEvent](classes/Page.md#classmethod-pageclearevent) had been called |

### Groups

- EventRegistry

### See Also

- [Page.setEvent](classes/Page.md#classmethod-pagesetevent)

---
## Type: FormItemClassName

### Description
Name of a SmartClient Class that subclasses [FormItem](classes/FormItem.md#class-formitem). Some values with this type:

*   ["TextItem"](classes/TextItem.md#class-textitem)
*   ["SliderItem"](classes/SliderItem.md#class-slideritem),
*   ["CanvasItem"](classes/CanvasItem.md#class-canvasitem)

---
## Type: GroupTreeChangeType

### Description
Type of change to the [ListGrid.groupTree](classes/ListGrid_1.md#attr-listgridgrouptree).

### Values

| Value | Description |
|-------|-------------|
| ListGrid.GROUP_BY | [ListGrid.groupBy](classes/ListGrid_2.md#method-listgridgroupby) responsible (grouping fields changed) |
| ListGrid.REGROUP | [ListGrid.regroup](classes/ListGrid_2.md#method-listgridregroup) responsible (grid already grouped) |
| ListGrid.INCREMENTAL | incremental regroup of a single record |

### See Also

- [ListGrid.groupTreeChanged](classes/ListGrid_2.md#method-listgridgrouptreechanged)

---
## Type: HoverPersistMode

### Description
Customizes how users can interact with hovers.

### Values

| Value | Description |
|-------|-------------|
| "none" | Hover is dismissed as soon as the mouse moves off the target. This default type of hover cannot offer an interaction because the hover vanishes on mouseOut from the target |
| "underMouse" | the user has a brief window to move the cursor over the hover to prevent it from being dismissed, until mouseOut from the hover, allowing interactive hovers. Note, if you want your hover to disappear as soon as something is clicked (like a link, for example), call [Hover.hide](classes/Hover.md#classmethod-hoverhide) |
| "clickPin" | like "underMouse", but if the user clicks in the hover, it is pinned until the user clicks outside of the hover |
| "autoPin" | like "clickPin", but the hover is pinned as soon as the user places the cursor over the hover, and needs an outside-click to dismiss |

### Groups

- hovers

---
## Type: IconOverTrigger

### Description
Property to govern when the 'over' styling is applied to a formItemIcon.

### Values

| Value | Description |
|-------|-------------|
| "icon" | Show rollover styling and media when the user is over the icon only |
| "textBox" | Show rollover styling and media when the user is over the icon or over the textBox (or control-table, if present) for this icon. Only has an effect when [FormItem.showOver](classes/FormItem.md#attr-formitemshowover) is true. |
| "item" | Show rollover styling and media when the user is over any part of the FormItem, including the entire cell within a DynamicForm table containing the item. |

---
## Type: Integer

### Description
A whole number, for example, 5. Decimal numbers, for example 5.5, are not allowed. Null is allowed.

### See Also

- [int](#type-int)
- [PositiveInteger](#type-positiveinteger)

---
## Type: JSONCircularReferenceMode

### Description
What the [JSONEncoder](classes/JSONEncoder.md#class-jsonencoder) should do when it encounters a circular reference in an object structure.

### Values

| Value | Description |
|-------|-------------|
| "omit" | circular references in Arrays will be represented as a null entry, and objects will have a property with a null value |
| "marker" | leave a string marker, the [JSONEncoder.circularReferenceMarker](classes/JSONEncoder.md#attr-jsonencodercircularreferencemarker), wherever a circular reference is found |
| "path" | leave a string marker _followed by_ the path to the first occurrence of the circular reference from the top of the object tree that was serialized. This potentially allows the original object graph to be reconstructed. |

---
## Type: LabelRotationMode

### Description
Strategy for determining whether and when to rotate certain labels.

### Values

| Value | Description |
|-------|-------------|
| "never" | do not rotate labels |
| "auto" | rotate labels if needed in order to make them legible and non-overlapping |
| "always" | always rotate labels |

---
## Type: LayoutPolicy

### Description
Policy controlling how the Layout will manage member sizes on this axis.

Note that, by default, Layouts do _not_ automatically expand the size of all members to match a member that overflows the layout on the breadth axis. This means that a [DynamicForm](classes/DynamicForm.md#class-dynamicform) or other component that can't shrink beyond a minimum width will "stick out" of the Layout, wider than any other member and wider than automatically generated components like resizeBars or sectionHeaders (in a [SectionStack](classes/SectionStack.md#class-sectionstack)).

This is by design: matching the size of overflowing members would cause expensive redraws of all members in the Layout, and with two or more members potentially overflowing, could turn minor browser size reporting bugs or minor glitches in custom components into infinite resizing loops.

If you run into this situation, you can either:

*   set the overflowing member to [overflow](classes/Canvas.md#attr-canvasoverflow): "auto", so that it scrolls if it needs more space
*   set the Layout as a whole to [overflow](classes/Canvas.md#attr-canvasoverflow):"auto", so that the whole Layout scrolls when the member overflows
*   define a [resized()](classes/Canvas.md#method-canvasresized) handler to manually update the breadth of the layout
*   set [Layout.minBreadthMember](classes/Layout.md#attr-layoutminbreadthmember) to ensure that the available breadth used to expand all (other) members is artificially increased to match the current breadth of the `minBreadthMember` member; the layout will still be overflowed in this case and the reported size from [Canvas.getWidth](classes/Canvas.md#method-canvasgetwidth) or [Canvas.getHeight](classes/Canvas.md#method-canvasgetheight) won't change, but all members should fill the visible width or height along the breadth axis

For the last approach, given the VLayout `myLayout` and a member `myWideMember`, then we could define the following [resized()](classes/Canvas.md#method-canvasresized) handler on `myLayout`:

```
 resized : function () {
     var memberWidth = myWideMember.getVisibleWidth();
     this.setWidth(Math.max(this.getWidth(), memberWidth + offset));
 }
```
where `offset` reflects the difference in width (due to margins, padding, etc.) between the layout and its widest member. In most cases, a fixed offset can be used, but it can also be computed via the calculation:

```
     myLayout.getWidth() - myLayout.getViewportWidth()
 
```
in an override of [draw()](classes/Canvas.md#method-canvasdraw) for `myLayout`. (That calculation is not always valid inside the [resized()](classes/Canvas.md#method-canvasresized) handler itself.)

Note: the HLayout case is similar- just substitute height where width appears above.

See also [Layout.overflow](classes/Layout.md#attr-layoutoverflow).

### Values

| Value | Description |
|-------|-------------|
| Layout.NONE | Layout does not try to size members on the axis at all, merely stacking them (length axis) and leaving them at default breadth. |
| Layout.FILL | Layout sizes members so that they fill the specified size of the layout. The rules are:

*   Any component given an initial pixel size, programmatically resized to a specific pixel size, or drag resized by user action is left at that exact size
*   Any component that [autofits](classes/Button.md#attr-buttonautofit) is given exactly the space it needs, never forced to take up more.
*   All other components split the remaining space equally, or according to their relative percentages.
*   Any component that declares a [Canvas.minWidth](classes/Canvas.md#attr-canvasminwidth) or [Canvas.minHeight](classes/Canvas.md#attr-canvasminheight) will never be sized smaller than that size
*   Any component that declares a [Canvas.maxWidth](classes/Canvas.md#attr-canvasmaxwidth) or [Canvas.maxHeight](classes/Canvas.md#attr-canvasmaxheight) will never be sized larger than that size

In addition, components may declare that they have [adaptive sizing](classes/Canvas.md#attr-canvascanadaptwidth), and may coordinate with the Layout to render at different sizes according to the amount of available space. |

### See Also

- [Layout.minBreadthMember](classes/Layout.md#attr-layoutminbreadthmember)

---
## Type: ListGridFieldState

### Description
An object containing the stored presentation information for the fields of a listGrid. Information contained in a `ListGridFieldState` object includes the visibility and widths of the listGrid's fields.  
Note that this object is a JavaScript string, and may be stored (for example) as a blob on the server for state persistence across sessions.

### Groups

- viewState

---
## Type: ListGridUserCriteriaState

### Description
An object containing the stored criteria as applied by the user. Does not include criteria applied in other ways.

### Groups

- viewState

---
## Type: ListGridViewState

### Description
An object containing the "view state" information for a listGrid.

This object contains state information reflecting the following states in the grid:

*   [field state](reference_2.md#type-listgridfieldstate)
*   [sort state](#type-listgridsortstate)
*   [selected state](#type-listgridselectedstate)
*   [group state](#type-listgridgroupstate)
*   [criteria state](reference_2.md#type-listgridusercriteriastate)
*   hilite state
*   filterEditor visibility state

Note that this object is a JavaScript string, and may be stored (for example) as a blob on the server for state persistence across sessions.

### Groups

- viewState

---
## Type: ListStyleType

### Description
The style of list item marker for a list.

### Values

| Value | Description |
|-------|-------------|
| "disc" | A filled, black dot (•) |
| "circle" | An unfilled circle (◦) |
| "square" | A filled, black square (■) |
| "decimal" | Numbers (1., 2., 3., etc.) |
| "upper-roman" | Uppercase Roman numerals (I., II., III., IV., etc.) |
| "lower-roman" | Lowercase Roman numerals (i., ii., iii., iv., etc.) |
| "upper-alpha" | Uppercase letters (A., B., C., etc.) |
| "lower-alpha" | Lowercase letters (a., b., c., etc.) |
| "custom-image" | An image used in place of a marker. |

---
## Type: LoadProjectErrorStatus

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "timeout" | server has not responded within configured request timeout |
| "noResponseFromURL" | can't reach server at [Reify.serverURL](classes/Reify.md#classattr-reifyserverurl) |
| "badReifyServerURL" | no project loader at [Reify.serverURL](classes/Reify.md#classattr-reifyserverurl) |
| "badCredentials" | invalid [Reify.userName](classes/Reify.md#classattr-reifyusername) or [Reify.password](classes/Reify.md#classattr-reifypassword) |
| "projectNotFound" | none of the requested projects were found |
| "servletError" | — |

---
## Type: LocatorStrategy

### Description
The AutoTest subsystem relies on generating and parsing identifier strings to identify components on the page. A very common pattern is identifying a specific component within a list of possible candidates. There are many many cases where this pattern is used, for example - members in a layout, tabs in a tabset, sections in a section stack.

In order to make these identifiers as robust as possible across minor changes to an application, (such as skin changes, minor layout changes, etc) the system will store multiple pieces of information about a component when generating an identification string to retrieve it from a list of candidates. The system has a default strategy for choosing the order in which to look at these pieces of information but in some cases this can be overridden by setting a `LocatorStrategy`.

By default we use the following strategies in order to identify a component from a list of candidates:

*   `name`: Does not apply in all cases but in cases where a specified `name` attribute has meaning we will use it - for example for [sections in a section stack](classes/SectionStackSection.md#attr-sectionstacksectionname) or [images](classes/Img.md#attr-imgname).
*   `title`: If a title is specified for the component this may be used as a legitimate identifier if it is unique within the component - for example differently titled tabs within a tabset.
*   `index`: Locating by index is typically less robust than by name or title as it is likely to be affected by layout changes on the page.

If an explicit strategy is specified, that will be used to locate the component if possible. If no matching component is found using that strategy, we will continue to try the remaining strategies in order as described above. In other words setting a locatorStrategy to "title" will skip attempting to find a component by name, and instead attempt to find by title - or failing that by index.

In cases where the name is considered definitive, such as for [Tabs](classes/Tab.md#attr-tabname) or [FormItems](classes/FormItem.md#attr-formitemname), no fallback check will occur if a name is provided in the locator but doesn't match a live object - the locator will fail to match anything. Furthermore, in the case of [Tabs](#object-tab), [FormItems](classes/FormItem.md#class-formitem), or collections other than [children of a widget](classes/Canvas.md#attr-canvaschildren), if a title is present in the locator and you haven't specified specified "index" as the strategy, there may be no fallback check using the index if the locator title fails to match.

To avoid the Framework trying to match by name or title where they are assumed definitive and we skip fallback to the remaining locator attributes, you'll need to remove the name or title from the locator in question (or set the locatorStrategy to "index" in the case of the title).

Note that we also support matching by type (see [LocatorTypeStrategy](#type-locatortypestrategy)). Matching by type is used if we were unable to match by name or title or to disambiguate between multiple components with a matching title.

### Values

| Value | Description |
|-------|-------------|
| "name" | Match by name if possible. |
| "title" | Match by title if possible. |
| "index" | Match by index |

### Groups

- autoTest

### See Also

- [ListGrid.locateRowsBy](classes/ListGrid_1.md#attr-listgridlocaterowsby)
- [ListGrid.locateColumnsBy](classes/ListGrid_1.md#attr-listgridlocatecolumnsby)
- [Canvas.locatePeersBy](classes/Canvas.md#attr-canvaslocatepeersby)
- [Canvas.locateChildrenBy](classes/Canvas.md#attr-canvaslocatechildrenby)
- [Layout.locateMembersBy](classes/Layout.md#attr-layoutlocatemembersby)
- [SectionStack.locateSectionsBy](classes/SectionStack.md#attr-sectionstacklocatesectionsby)
- [FormItem.locateItemBy](classes/FormItem.md#attr-formitemlocateitemby)
- [TabSet.locateTabsBy](classes/TabSet.md#attr-tabsetlocatetabsby)

---
## Type: LogicalOperator

### Description
Operators that can evaluate a set of criteria and produce a combined result.

### Values

| Value | Description |
|-------|-------------|
| "and" | true if all criteria are true |
| "or" | true if any criteria are true |
| "not" | true if all criteria are false |

---
## Type: MinimalScrollbarContrastSuffix

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "Light" | suffix to apply to [MinimalScrollbar.trackBaseStyle](classes/MinimalScrollbar.md#attr-minimalscrollbartrackbasestyle) and [MinimalScrollbar.thumbBaseStyle](classes/MinimalScrollbar.md#attr-minimalscrollbarthumbbasestyle) to get a light appearance (appropriate for contrasting against a dark background) |
| "Dark" | suffix to apply to [MinimalScrollbar.trackBaseStyle](classes/MinimalScrollbar.md#attr-minimalscrollbartrackbasestyle) and [MinimalScrollbar.thumbBaseStyle](classes/MinimalScrollbar.md#attr-minimalscrollbarthumbbasestyle) to get a dark appearance (appropriate for contrasting against a light background) |

---
## Type: MockDataFormat

### Description
Specifies the format of the mock data.

### Values

| Value | Description |
|-------|-------------|
| "mock" | Mock data in "balsamiq" format |
| "csv" | Mock data in CSV format |
| "xml" | Mock data in XML format |
| "json" | Mock data in JSON format |

---
## Type: MoveKnobPoint

### Description
Specifies the starting point of a move knob with respect to its draw item. The move knob is positioned relative to the move knob point at the [DrawItem.moveKnobOffset](classes/DrawItem.md#attr-drawitemmoveknoboffset).

### Values

| Value | Description |
|-------|-------------|
| "TL" | Top Left corner |
| "TR" | Top Right corner |
| "BL" | Bottom Left corner |
| "BR" | Bottom Right corner |

---
## Type: MultiComboBoxLayoutStyle

### Description
Specifies the layout of the combo box and buttons in a MultiComboBoxItem.

### Values

| Value | Description |
|-------|-------------|
| "flow" | use a [FlowLayout](#class-flowlayout), showing values first, then the text entry area |
| "flowReverse" | use a FlowLayout, with the text entry first and values shown afterwards |
| "horizontal" | Use a horizontal layout with the combo box on the right |
| "horizontalReverse" | Use a horizontal layout with the combo box on the left |
| "vertical" | Use a vertical layout |
| "verticalReverse" | Use a vertical layout with the combo box at the bottom |

### See Also

- [MultiComboBoxItem.layoutStyle](classes/MultiComboBoxItem.md#attr-multicomboboxitemlayoutstyle)

---
## Type: MultiMessageMode

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "stack" | messages of the same [NotifyType](reference_2.md#type-notifytype) are arranged in a stack |
| "replace" | messages of the same [NotifyType](reference_2.md#type-notifytype) replace each other |

---
## Type: MultiWindowEvent

### Description
Various events triggered by any window in the current application.

Aside from the standard event types listed, other types may be supported depending upon whether OpenFin is in use:

*   With OpenFin, [application event types](https://developer.openfin.co/docs/javascript/stable/tutorial-Application.EventEmitter.html) are allowed.
*   Without OpenFin, [HTML Dom Events](https://www.w3schools.com/jsref/dom_obj_event.asp) supported by [window.addEventListener()](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) are allowed.

### Values

| Value | Description |
|-------|-------------|
| "load" | fires when a window finishes loading |
| "unload" | fires when a window is about to be reloaded or closed |
| "move" | fires when a window is moved |
| "resize" | fires when a window is resized |
| "close" | fires when a window is closed |
| "focus" | fires when a window gets focus |
| "blur" | fires when a window loses focus |
| "activate" | (synonym for "focus") |
| "deactivate" | (synonym for "blur") |

---
## Type: NavigationMethod

### Description
Method of, or reason for, navigation between panes.

### Values

| Value | Description |
|-------|-------------|
| "backClick" | a "back" [NavigationButton](classes/NavigationButton.md#class-navigationbutton) has been clicked |
| "sideClick" | a side panel [NavigationButton](classes/NavigationButton.md#class-navigationbutton) has been clicked |
| "programmatic" | application code called [setCurrentPane()](classes/SplitPane.md#method-splitpanesetcurrentpane), [showNavigationPane()](classes/SplitPane.md#method-splitpaneshownavigationpane), [showListPane()](classes/SplitPane.md#method-splitpaneshowlistpane), [showDetailPane()](classes/SplitPane.md#method-splitpaneshowdetailpane), etc. |
| "navigatePane" | application code directly called [navigatePane()](classes/SplitPane.md#method-splitpanenavigatepane) |
| "selectionChanged" | a seletion change automatically called [navigatePane()](classes/SplitPane.md#method-splitpanenavigatepane) |
| "historyCallback" | browser navigation triggered [SplitPane](classes/SplitPane.md#class-splitpane) navigation |

---
## Type: NotifyType

### Description
An identifier passed to [Notify](classes/Notify.md#class-notify) APIs to group related messages together so that they all use the same behavior and display settings.

### See Also

- [Notify.addMessage](classes/Notify.md#classmethod-notifyaddmessage)
- [Notify.configureMessages](classes/Notify.md#classmethod-notifyconfiguremessages)
- [Notify.dismissMessage](classes/Notify.md#classmethod-notifydismissmessage)

---
## Type: Orientation

### Description
—

### Values

| Value | Description |
|-------|-------------|
| Layout.VERTICAL | members laid out vertically |
| Layout.HORIZONTAL | members laid out horizontally |

### Groups

- orientation

---
## Type: PageEvent

### Description
Events registerable via [Page.setEvent](classes/Page.md#classmethod-pagesetevent)

### Values

| Value | Description |
|-------|-------------|
| "idle" | Fires repeatedly (every 10 ms by default) when the system is idle (i.e., not busy running other scripts) after the page is loaded. |
| "load" | Fires when the page has finished loading. It corresponds to the browser 'load' event normally handled by window.onload. |
| "unload" | Fires when the page is exited or unloaded. It corresponds to the browser 'unload' event normally handled by window.onunload. |
| "resize" | Fires when the browser window is resized by the user. It corresponds to the browser 'resize' event normally handled by window.onresize. |
| "mouseDown" | Fires when the left mouse button is pressed on the Page. |
| "rightMouseDown" | Fires when the right mouse button is pressed on the Page. |
| "mouseMove" | Fires when the mouse moves on the Page. |
| "mouseUp" | Fires when the left mouse button released on the Page. |
| "click" | Fires when the user clicks the mouse on the Page. |
| "doubleClick" | Fires when the uesr double-clicks on the Page. |
| "showContextMenu" | Fires when the right mouse button is clicked on the page. If your event handler for this event returns false, the native browser context menu will be suppressed.  
Note: On the Macintosh platform, `Command+Click` may be used instead of right-button click to trigger a context menu event.  
On the Opera browser, `Ctrl+Shift+Click` should be used instead of right-button click. |
| "keyPress" | Fires when a user presses a key on the keyboard. |
| "orientationChange" | Fires when the [Page.getOrientation](classes/Page.md#classmethod-pagegetorientation) changes due to browser-window resize or rotation of a mobile device. |
| "fontsLoaded" | Fires when the [FontLoader](classes/FontLoader.md#class-fontloader) completes loading custom fonts. |
| "fontLoadingFailed" | Fires after a timeout if the [FontLoader](classes/FontLoader.md#class-fontloader) fails to load all custom fonts. see classMethod:Page.setEvent() see classMethod:Page.clearEvent() |

---
## Type: PanelPlacement

### Description
Possible placements for pop-up choosers, menus, dialogs or other temporary UIs, which may need to expand to take up additional room for smaller screens.

### Values

| Value | Description |
|-------|-------------|
| "nearOrigin" | classic placement for menus, pop-up lists and pickers in desktop interfaces: near the control that was clicked (a search field, [MenuButton](classes/MenuButton.md#class-menubutton), etc). Note: this setting does not apply when there is no originating control (such as a dialog that appears due to session timeout), in which case centering will generally be used |
| "fillPanel" | fill the nearest containing panel managed by a device-aware layout such as [SplitPane](classes/SplitPane.md#class-splitpane), which will generally be equivalent to "fillScreen" for a [handset-sized device](classes/Browser.md#classattr-browserishandset). Note: this setting does not apply if there is no clear container for the component originating the UI, in which case, "fillScreen" will generally be used. |
| "fillScreen" | fill the entire screen |
| "halfScreen" | fill the bottom half of the screen. This is the default behavior on iOS6/7 for plain HTML `<select>`, but note that native apps rarely use this interface for picking from lists and it is not generally recommended. |
| "none" | this setting disables all panelPlacement sizing and positioning logic. Explicitly specified size and positioning will be used. |

---
## Type: PromptStyle

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "dialog" | Displays a centered modal prompt with text specified by [RPCRequest.prompt](classes/RPCRequest.md#attr-rpcrequestprompt) |
| "cursor" | Changes the current cursor to the style specified by [RPCRequest.promptCursor](classes/RPCRequest.md#attr-rpcrequestpromptcursor) |

---
## Type: RecategorizeMode

### Description
Type for controlling when a "recategorize" is applied to records being dropped on a databound component from another databound component.

### Values

| Value | Description |
|-------|-------------|
| "always" | recategorize is always applied |
| "checked" | recategorize if normal checks pass |
| "never" | never recategorize |

---
## Type: RecordComponentPoolingMode

### Description
The method of component-pooling to employ for [recordComponents](classes/ListGrid_1.md#attr-listgridshowrecordcomponents).

### Values

| Value | Description |
|-------|-------------|
| "viewport" | components are destroyed when the record is not being rendered. Best for large datasets where embedded components differ greatly per record. |
| "data" | components are [clear()ed](classes/Canvas.md#method-canvasclear) when not in the viewport, but stay with a record until the record is dropped from cache. Best for guaranteed small datasets. |
| "recycle" | components are pooled and will be passed to [updateRecordComponent()](classes/ListGrid_2.md#method-listgridupdaterecordcomponent) with the `recordChanged` parameter set to true. Best for large datasets where embedded components are uniform across different records and can be efficiently reconfigured to work with a new record |

---
## Type: RecordDropAppearance

### Description
Controls how ListGrid record drop events report their [dropPosition](classes/ListGrid_2.md#method-listgridgetrecorddropposition), and where the drop indicator will be displayed if appropriate.

### Values

| Value | Description |
|-------|-------------|
| ListGrid.OVER | When the user drops onto a record, dropPosition will always be "over" |
| ListGrid.BETWEEN | When the user drops onto a record, dropPosition will be either "before" or "after" depending on whether the mouse was over the top or bottom of the target record |
| ListGrid.BOTH | When the user drops onto a record, if the drop occurs centered over the record, the dropPosition will be reported as "over", otherwise it will be "before" or "after" depending on whether the mouse was over the top or bottom of the target record. |
| ListGrid.BODY | No dropPosition will be reported |

---
## Type: RecordLayout

### Description
Controls the style of TableView record display

### Values

| Value | Description |
|-------|-------------|
| TableView.TITLE_ONLY | Show [title field](classes/TableView.md#attr-tableviewtitlefield) only |
| TableView.TITLE_DESCRIPTION | Show [title](classes/TableView.md#attr-tableviewtitlefield) and [description](classes/TableView.md#attr-tableviewdescriptionfield) fields only |
| TableView.SUMMARY_INFO | Show [title](classes/TableView.md#attr-tableviewtitlefield), [description](classes/TableView.md#attr-tableviewdescriptionfield) and [info](classes/TableView.md#attr-tableviewinfofield) fields only |
| TableView.SUMMARY_DATA | Show [title](classes/TableView.md#attr-tableviewtitlefield), [description](classes/TableView.md#attr-tableviewdescriptionfield) and [data](classes/TableView.md#attr-tableviewdatafield) fields only |
| TableView.SUMMARY_FULL | Show [title](classes/TableView.md#attr-tableviewtitlefield), [description](classes/TableView.md#attr-tableviewdescriptionfield), [info](classes/TableView.md#attr-tableviewinfofield) and [data](classes/TableView.md#attr-tableviewdatafield) fields similar to the iPhoneOS Mail application |

---
## Type: RegressionLineType

### Description
Supported regression algorithms for fitting the data points of a scatter plot.

### Values

| Value | Description |
|-------|-------------|
| "line" | linear regression |
| "polynomial" | polynomial regression |

---
## Type: RelativeDateRangePosition

### Description
When relative dates are specified in a date range, typically in a RelativeDateItem or DateRangeItem, in order to make the range inclusive or exclusive, it is useful to be able to specify whether we're referring to the start or end of the date in question.

### Values

| Value | Description |
|-------|-------------|
| "start" | Indicates this relative date should be treated as the start of the specified logical date. |
| "end" | Indicates this relative date should be treated as the end of the specified logical date. |

---
## Type: RelativeDateString

### Description
A string of known format used to specify a datetime offset. For example, a RelativeDateString that represents "one year from today" is written as `"+1y"`.

RelativeDateStrings are comprised of the following parts:

*   direction: the direction in which the quantity applies - one of + or -
*   quantity: the number of units of time to apply - a number
*   timeUnit: an abbreviated timeUnit to use - one of ms/MS (millisecond), s/S (second), mn/MN (minute), h/H (hour), d/D (day), w/W (week), m/M (month), q/Q (quarter, 3-months), y/Y (year), dc/DC (decade) or c/C (century).  
    The timeUnit is case sensitive. A lowercase timeUnit implies an exact offset, so `+1d` refers to the current date / time increased by exactly 24 hours. If the timeUnit is uppercase, it refers to the start or end boundary of the period of time in question, so `+1D` would refer to the end of the day (23:39:59:999) tomorrow, and `-1D` would refer to the start of the day (00:00:00:000) yesterday.
*   \[qualifier\]: an optional timeUnit encapsulated in square-brackets and used to offset the calculation - eg. if +1d is "plus one day", +1d\[W\] is "plus one day from the end of the current week". You may also specify another complete RelativeDateString as the \[qualifier\], which offers more control - eg, +1d\[+1W\] indicates "plus one day from the end of NEXT week".

This format is very flexible. Here are a few example relative date strings:  
`+0D`: End of today. There are often multiple ways to represent the same time using this system - for example this could also be written as `-1ms[+1D]`  
`-0D`: Beginning of today.  
`+1W`: End of next week.  
`+1w[-0W]`: Beginning of next week.  
`+1w[-0D]`: Beginning of the current day of next week.

### See Also

- [RelativeDateShortcut](#type-relativedateshortcut)

---
## Type: ResizeKnobPoint

### Description
Specifies the position of a resize knob with respect to its draw item.

### Values

| Value | Description |
|-------|-------------|
| "TL" | Top Left corner |
| "TR" | Top Right corner |
| "BL" | Bottom Left corner |
| "BR" | Bottom Right corner |
| "T" | Centered on the top edge |
| "B" | Centered on the bottom edge |
| "R" | Centered on the left edge |
| "L" | Centered on thie right edge |

---
## Type: SavedSearchStoredState

### Description
How should a window be closed?

### Values

| Value | Description |
|-------|-------------|
| "criteria" | only criteria will be stored, even for components that are capable of storing additional viewState. |

---
## Type: ScanMode

### Description
When discovering a tree, the scanMode determines how to scan for the childrenProperty "node": take each node individually "branch": scan direct siblings as a group, looking for best fit "level": scan entire tree levels as a group, looking for best fit

### Values

| Value | Description |
|-------|-------------|
| "node" | take each node individually |
| "branch" | scan direct siblings as a group, looking for best fit |
| "level" | scan entire tree levels as a group, looking for best fit |

---
## Type: SelectionNotificationType

### Description
Enum to indicate selection change notification types. Used by [ListGrid.reselectOnUpdateNotifications](classes/ListGrid_1.md#attr-listgridreselectonupdatenotifications) and [TileGrid.reselectOnUpdateNotifications](classes/TileGrid.md#attr-tilegridreselectonupdatenotifications).

### Values

| Value | Description |
|-------|-------------|
| "none" | No selection change notification should fire |
| "selectionChanged" | [selectionChanged()](classes/ListGrid_2.md#method-listgridselectionchanged) should fire but [selectionUpdated()](classes/ListGrid_2.md#method-listgridselectionupdated) should not fire. |
| "selectionUpdated" | [selectionChanged()](classes/ListGrid_2.md#method-listgridselectionchanged) and [selectionUpdated()](classes/ListGrid_2.md#method-listgridselectionupdated) should both fire. |

---
## Type: SelectItemsMode

### Description
Controls whether and when individual items are selected when clicking on a form in editMode.

### Values

| Value | Description |
|-------|-------------|
| "item" | select an individual item if the item itself it clicked on, but not its title cell |
| "itemOrTitle" | select an individual item if either the item or its title cell is clicked on. NOTE: this mode is not the default because it can be make it difficult to select the form as a whole |
| "never" | never allow selection of an individual item |

---
## Type: SendMethod

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "GET" | GET method (regular URL encoding) |
| "POST" | POST method (form field encoding) |

### Groups

- communication

---
## Type: SettledPromiseStatus

### Description
The eventual state of a settled [Promise](reference_2.md#object-promise).

### Values

| Value | Description |
|-------|-------------|
| "fulfilled" | The `Promise` fulfilled with a value. |
| "rejected" | The `Promise` rejected with a reason. |

---
## Type: SortArrow

### Description
Do we display an arrow for the sorted field ?

### Values

| Value | Description |
|-------|-------------|
| "none" | Don't show a sort arrow at all. |
| "corner" | Display sort arrow in the upper-right corner (above the scrollbar) only. |
| "field" | Display sort arrow above each field header only. |
| "both" | Display sort arrow above each field header AND in corner above scrollbar.BOTH:"both", // NOTE: Canvas establishes this constant |

### Groups

- sorting
- appearance

---
## Type: TieMode

### Description
what to do if there is more than one possible childrenProperty when using scanMode "branch" or "level" "node": continue, but pick childrenProperty on a per-node basis (will detect mixed) "highest": continue, picking the childrenProperty that occurred most as the single choice "stop": if there's a tie, stop at this level (assume no further children)

### Values

| Value | Description |
|-------|-------------|
| "node" | continue, but pick childrenProperty on a per-node basis (will detect mixed) |
| "highest" | continue, picking the childrenProperty that occurred most as the single choice |
| "stop" | if there's a tie, stop at this level (assume no further children) |

---
## Type: TimeUnit

### Description
An enum of time-units available for use with the [RelativeDateItem](classes/RelativeDateItem.md#class-relativedateitem), [TimeItem](classes/TimeItem.md#class-timeitem) and [Calendar](classes/Calendar.md#class-calendar) widgets.

### Values

| Value | Description |
|-------|-------------|
| "millisecond" | a millisecond time-unit |
| "second" | a second time-unit |
| "minute" | a minute time-unit |
| "hour" | an hour time-unit |
| "day" | a day time-unit |
| "week" | a week time-unit |
| "month" | a month time-unit |
| "quarter" | a quarter (3 month) time-unit |
| "year" | a year time-unit |

---
## Type: TreeGridOpenState

### Description
An object containing the open state for a treeGrid. Note that this object is not intended to be interrogated directly, but may be stored (for example) as a blob on the server for state persistence across sessions.

### Groups

- viewState

---
## Type: URL

### Description
A Uniform Resource Locator string, as defined by [https://www.w3.org/Addressing/URL/url-spec.html](https://www.w3.org/Addressing/URL/url-spec.html). For example, "https://www.smartclient.com/product/" is a valid `URL`.

---
## Type: ValueClass

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "general" | Any kind of data. Usually this is textual, but not necessarily always so. An example would be a "2-4 sentence summary". |
| "categorical" | A fixed list of categories or nominal values. |
| "ordinal" | An extension of "categorical", where the categories are also strictly ordered. |
| "interval" | Strictly numerical data. |
| "ratio" | An extension of "interval", where 0 means the absence of something, and ratios between values are meaningful. |

---
## Type: ValueMap

### Description
A ValueMap defines the set of legal values for a field, and optionally allows you to provide a mapping from stored values to values as seen by the end user.

A valueMap can be specified as either an Array of legal values, or as an [Object](#type-object) where each property maps a stored value to a user-displayable value. See [DataSourceField.valueMap](classes/DataSourceField.md#attr-datasourcefieldvaluemap) for how to express a ValueMap in [Component XML](kb_topics/componentXML.md#kb-topic-component-xml).

A ValueMap can be entirely static or entirely dynamic, with many options in between. For example, a ValueMap may be:

*   statically defined in a JavaScript or XML file. Such a valueMap changes only when application code is upgraded.
*   generated dynamically by server code when the application first loads, for example, by generating JavaScript or XML dynamically in a .jsp or .asp file. Such a valueMap may be different for each session and for each user.
*   loaded on demand from a DataSource, via the [optionDataSource](classes/PickList.md#attr-picklistoptiondatasource) property, or via a call to [DataSource.fetchData](classes/DataSource.md#method-datasourcefetchdata) where a valueMap is derived dynamically from the returned data (see [DataSource.fetchData](classes/DataSource.md#method-datasourcefetchdata) for an example). Such a valueMap may be updated at any time, for example, every time the user changes a related field while editing data.

See also the [SmartClient Architecture Overview](kb_topics/smartArchitecture.md#kb-topic-smartclient-architecture) to understand the best architecture from a performance and caching perspective.

---
## Type: VelocityExpression

### Description
An expression in the [Velocity Template Language](http://velocity.apache.org/engine/releases/velocity-1.7/user-guide.html) (VTL). For more information on SmartClient's Velocity support, see [Velocity support](#kb-topic-velocitysupport).

Note that a `VelocityExpression` must often evaluate to a particular type of value to be useful. For example, [DataSource.requires](classes/DataSource.md#attr-datasourcerequires) must evaluate to true or false (Boolean objects or strings containing those two words), and [Mail.messageData](classes/Mail.md#attr-mailmessagedata) must evaluate to a Java `Map` object, or a Java `List` containing only `Map`s.

### Groups

- velocitySupport

---
## Type: Visibility

### Description
—

### Values

| Value | Description |
|-------|-------------|
| Canvas.INHERIT | The widget visibility will match that of its parent (usually visible). |
| Canvas.VISIBLE | The widget will always be visible whether its parent is or not. |
| Canvas.HIDDEN | The widget will always be hidden even when its parent is visible. |

### Groups

- visibility

---
## Type: ZoomStartPosition

### Description
—

### Values

| Value | Description |
|-------|-------------|
| "start" | start at the beginning of the range |
| "end" | start at the end of the range |

### Groups

- zoom

---
## Object: AIFieldRequest

### Description
Settings that configure requests to AI to generate the values for a field.

---
## Object: AIResponse

### Description
Represents a response from AI.

---
## Object: ColorStop

### Description
An object containing properties that is used in Gradient types

---
## Object: Criterion

### Description
An object representing a criterion to apply to a record.

A criterion is part of the definition of an [AdvancedCriteria](#object-advancedcriteria) object, which is used to filter records according to search criteria.

A criterion consists of an [Criterion.operator](classes/Criterion.md#attr-criterionoperator) and typically a [fieldName](classes/DataSourceField.md#attr-datasourcefieldname) from a [Record](#object-record) and a [value](classes/Criterion.md#attr-criterionvalue) to compare to. However some operators either don't require a value (eg, isNull) or act on other criteria rather than directly on a [Record](#object-record)'s fields (eg, the "and" and "or" logical operators).

A shortcut form is also allowed where only `fieldName` and `value` values are provided. In this case the `operator` is assumed to be "equals".

### Groups

- advancedFilter

---
## Object: DataQuestion

### Description
Represents a data question and either the steps taken in attempting to answer it or the result.

### Groups

- answerEngine

---
## Object: DataQuestionResult

### Description
The result of the data question.

---
## Object: DataSourceField

### Description
Metadata about a DataSourceField, including its type and validators.

---
## Object: Date

### Description
Extensions to the Date class, including added static methods on the Date object, and additional instance methods available on all date instances.

---
## Object: DiscoverTreeSettings

### Description
Defines a set of properties that specify how the tree will be explored by [Tree.discoverTree](classes/Tree.md#classmethod-treediscovertree)

---
## Object: DOMElement

### Description
Represents a native DOM element used by the browser.

For example, you can retrieve the DOM element representing the "Set Data" button from ["Empty Grid" Sample](https://www.smartclient.com/smartclient/showcase/?id=emptyGrid) in the SmartClient Feature Explorer using [AutoTest.getElement](classes/AutoTest.md#classmethod-autotestgetelement):

```
 var buttonElement = isc.AutoTest.getElement("scLocator=//testRoot[]/child[Class=IButton||index=1||length=3||classIndex=0||classLength=2||roleIndex=0||roleLength=2||title=Set%20Data||scRole=button]/");
```
This is a more robust way to obtain a DOM element than retreiving it by ID:
```
 var buttonElement = document.getElementById("isc_FZ")
```

### See Also

- [usingSelenium](kb_topics/usingSelenium.md#kb-topic-using-selenium-scripts-selenese)

---
## Object: DrawnValue

### Description
Returns information about how a data value is rendered in a chart.

---
## Object: DSLoadSettings

### Description
Settings to control optional [DataSource loading](classes/DataSource.md#classmethod-datasourceload) features.

### See Also

- [DataSource.load](classes/DataSource.md#classmethod-datasourceload)

---
## Object: Field

### Description
Base type representing a field.

Field container implementations may extend this type with additional attributes and/or methods. For example, [DataSource](classes/DataSource.md#class-datasource) uses [DataSourceField](reference_2.md#object-datasourcefield), [DataBoundComponent](#interface-databoundcomponent) uses [DBCField](#object-dbcfield), and [ListGrid](classes/ListGrid_1.md#class-listgrid) uses [ListGridField](reference_2.md#object-listgridfield) (itself an extension of `DBCField`).

In general, `Field` instances should not be shared with multiple field containers.

---
## Object: FileLoader

### Description
This class enables background (deferred) loading and caching of JS, CSS and Image files. It is designed to work standalone from the rest of the SmartClient framework to provide a lightweight caching and loading mechanism for SmartClient modules as well as user-built application modules/fragments.

The most common usage scenarios are:

*   Caching JS, CSS, Image files in the browser in anticipation of a transition to a page that requires these files. For example, a plain HTML (non-SmartClient) login page or landing page can begin caching SmartClient in the background while allowing the user to login, or giving the user something to read. Normally, loading SmartClient or other large JavaScript files would block page loading and display. By loading SmartClient in the background only after a simple HTML landing page has loaded, you can completely eliminate perceived download time associated with loading a rich UI application, making a much larger difference in user experience than any difference in framework/application size.
*   Loading a multi-phase UI. In this scenario, an initial rendering of a page is done with minimal data transfer to the browser. Then JS, CSS, and Image files are fetched in the background to provide richer UI components. During this time the user can continue to normally interact with the initial page. Once loading is complete, the UI is updated with richer components.

The recommended usage pattern is to use the `loadISC` custom tag provided as part of the SmartClient SDK. You can specify `cacheOnly="true"` to loadISC to cache the SmartClient framework in the background or alternately `defer="true"` to load the SmartClient framework and make it available in the current page. You can specify the `onload` attribute of the tag to provide a JavaScript callback to your code that will be called when the framework loading is complete.

If you're not working in a JSP environment, you can use the [FileLoader.cache](classes/FileLoader.md#classmethod-fileloadercache)/[FileLoader.load](classes/FileLoader.md#classmethod-fileloaderload) APIs to accomplish the same effect as the `loadISC` JSP tag.

Additional APIs are provided for performing dynamic caching and loading of other JS, CSS, and Image files to improve the performance of your application. See below.

**You must set `window.isomorphicDir` before loading and using this module unless the default of '../isomorphic/' is acceptable. E.g. if your html file is in your toplevel webroot directory, then your HTML file should say (note the trailing slash):**

```
 <SCRIPT>window.isomorphicDir='isomorphic/'</SCRIPT>
 <SCRIPT SRC=isomorphic/system/modules/ISC_FileLoader.js></SCRIPT>
 
```
In addition, **if you are using Smart GWT**, you must set [modulesDir](classes/FileLoader.md#classattr-fileloadermodulesdir) to "modules/", as follows:
```
   isc.FileLoader.modulesDir = "modules/";
 
```
This module is usable independent of the rest of SmartClient - you can use it on pages that don't load any other modules. In practice, the general pattern is to use this module on static HTML pages such as a login page to pre-cache SmartClient modules, application logic, skin files, and css so that once the user logs in, there's no latency to load the rich UI.

You can also load the FileLoader itself dynamically - see [FileLoader.ensureLoaded](classes/FileLoader.md#classmethod-fileloaderensureloaded)

Note: You can also reference this class via the alias isc.FL

---
## Object: FiscalYear

### Description
An object representing the start of a given Fiscal Year in the current locale.

See [FiscalCalendar](#object-fiscalcalendar) for more information on how FiscalYears are set up and used.

---
## Object: FormItemEventInfo

### Description
An object containing details for mouse events occurring over a FormItem.

---
## Object: GaugeSector

### Description
Represents a sector on the gauge.

---
## Object: GroupSpecifier

### Description
A Javascript object defining the details of a single group operation. Used by the [MultiGroupDialog](classes/MultiGroupDialog.md#class-multigroupdialog) to edit multi-level grouping scenarios for use by components that support grouping.

### Groups

- grouping

---
## Object: HeaderSpan

### Description
A header span appears as a second level of headers in a ListGrid, spanning one or more ListGrid columns and their associated headers.

See [ListGrid.headerSpans](classes/ListGrid_1.md#attr-listgridheaderspans).

In addition to the properties documented here, all other properties specified on the headerSpan object will be passed to the [create()](classes/Class.md#classmethod-classcreate) method of the [ListGrid.headerSpanConstructor](classes/ListGrid_1.md#attr-listgridheaderspanconstructor). This allows you to set properties such as [Button.baseStyle](classes/Button.md#attr-buttonbasestyle) or [StretchImgButton.src](classes/StretchImgButton.md#attr-stretchimgbuttonsrc) directly in a `headerSpan`.

### Groups

- headerSpan

---
## Object: ListGridField

### Description
An ordinary JavaScript object containing properties that configures the display of and interaction with the columns of a [ListGrid](classes/ListGrid_1.md#class-listgrid).

### See Also

- [ListGrid.fields](classes/ListGrid_1.md#attr-listgridfields)
- [ListGrid.setFields](classes/ListGrid_2.md#method-listgridsetfields)

---
## Object: ListGridRecord

### Description
A ListGridRecord is a JavaScript Object whose properties contain values for each [ListGridField](reference_2.md#object-listgridfield). A ListGridRecord may have additional properties which affect the record's appearance or behavior, or which hold data for use by custom logic or other, related components.

For example a ListGrid that defines the following fields:

```
 fields : [
     {name: "field1"},
     {name: "field2"}
 ],
 
```
Might have the following data:

```
 data : [
     {field1: "foo", field2: "bar", customProperty:5},
     {field1: "field1 value", field2: "field2 value", enabled:false}
 ]
 
```
Each line of code in the `data` array above creates one JavaScript Object via JavaScript [object literal](#type-objectliteral) notation. These JavaScript Objects are used as ListGridRecords.

Both records shown above have properties whose names match the name property of a ListGridField, as well as additional properties. The second record will be disabled due to `enabled:false`; the first record has a property "customProperty" which will have no effect by default but which may be accessed by custom logic.

After a ListGrid is created and has loaded data, records may be accessed via [listGrid.getData()](classes/ListGrid_1.md#attr-listgriddata), for example, listGrid.getData().get(0) retrieves the first record. [ListGrid.data](classes/ListGrid_1.md#attr-listgriddata) may be a [ResultSet](classes/ResultSet.md#class-resultset) if the listGrid is bound to a DataSource. ListGridRecords are also passed to many events, such as [cellClick()](classes/ListGrid_2.md#method-listgridcellclick).

A ListGridRecord is always an ordinary JavaScript Object regardless of how the grid's dataset is loaded (static data, java server, XML web service, etc), and so supports the normal behaviors of JavaScript Objects, including accessing and assigning to properties via dot notation:

```
     var fieldValue = record.fieldName;
     record.fieldName = newValue;
 
```

Note however that simply assigning a value to a record won't cause the display to be automatically refreshed - [ListGrid.refreshCell](classes/ListGrid_2.md#method-listgridrefreshcell) needs to be called. Also, consider [editValues vs saved values](kb_topics/editing.md#kb-topic-grid-editing) when directly modifying ListGridRecords.

See the attributes in the API tab for the full list of special properties on ListGridRecords that will affect the grid's behavior.

---
## Object: LoadProjectSettings

### Description
LoadProjectSettings is the bundle of settings that can be passed to loadProject() as the "settings" argument, including optional http parameters for the request to [ProjectLoaderServlet](kb_topics/servletDetails.md#kb-topic-the-core-and-optional-smartclient-servlets).

There is no need to instantiate an LoadProjectSettings instance. Just pass a normal JavaScript object with the desired properties.

---
## Object: LoadScreenSettings

### Description
This is the bundle of settings that can be passed to [RPCManager.loadScreen](classes/RPCManager.md#classmethod-rpcmanagerloadscreen) as the "settings" argument. Some settings can also be passed as separate arguments; if these are present both as separate arguments and in settings, loadScreen() will use the value from the settings.

There is no need to instantiate a `LoadScreenSettings` instance. Just pass a normal JavaScript object with the desired properties.

---
## Object: MenuItem

### Description
Object specifying an item in a [Menu](classes/Menu.md#class-menu). Each `MenuItem` can have a [title](classes/MenuItem.md#attr-menuitemtitle), [icon](classes/MenuItem.md#attr-menuitemicon), [shortcut\\n keys](classes/MenuItem.md#attr-menuitemkeys), optional [MenuItem.submenu](classes/MenuItem.md#attr-menuitemsubmenu) and various other settings. Alternatively, a `MenuItem` can contain an arbitrary widget via [MenuItem.embeddedComponent](classes/MenuItem.md#attr-menuitemembeddedcomponent). MenuItems are specified as plain [JavaScript Objects](#type-object), usually with [ObjectLiteral](#type-objectliteral) notation. For example:
```
 isc.Menu.create({
     items : [
         {title: "item1", click: "alert(1)"},
         {title: "item2"}
     ]
 });
 
```
Do not use `isc.MenuItem.create()` - this is invalid.

Alternatively, Menus support binding to a [DataSource](classes/Menu.md#attr-menudatasource).

As another option, here's a sample of a Menu in [Component XML](kb_topics/componentXML.md#kb-topic-component-xml):

```
 <Menu>
    <items>
        <MenuItem title="item1" click="alert(1)"/>
        <MenuItem title="item2"/>
    </items>
 </Menu>
 
```

---
## Object: MessageID

### Description
Opaque message identifier for messages shown by the [Notify](classes/Notify.md#class-notify) class

---
## Object: NavigationBarViewState

### Description
Encapsulates state of a [NavigationBar](classes/NavigationBar.md#class-navigationbar)'s view. A `NavigationBarViewState` object is created to pass to [NavigationBar.setViewState](classes/NavigationBar.md#method-navigationbarsetviewstate) so that multiple properties of the `NavigationBar` can be changed at once.

---
## Object: NodeLocator

### Description
An object containing sufficient context to unambiguously identify a single node in the tree. For normal trees, the node itself - or its ID - is sufficient for this purpose, but for [multi-link trees](classes/Tree.md#method-treeismultilinktree), we also need to know the node's parent, and its position within that parent. For cases where we need to propagate change back up the node's parent chain, in order to maintain a given parent node's openList, the node, parent and position are not enough context; for those cases, we need either the node's position in the tree's openList, or a full path to the node. `NodeLocator` objects contain this extra context, and can be passed to APIs such as [Tree.openFolder](classes/Tree.md#method-treeopenfolder), which would ordinarily accept a parameter of type [TreeNode](reference_2.md#object-treenode).

---
## Object: PrintProperties

### Description
Settings for generating printable HTML for components.

### Groups

- printing

---
## Object: Promise

### Description
Extensions to the `Promise` class, or a polyfill of the ES6 `Promise` class if not provided natively by the browser.

---
## Object: PropertyValue

### Description
Identifies a property name and value to be assigned to a component by the [SetPropertiesTask](classes/SetPropertiesTask.md#class-setpropertiestask).

---
## Object: QualityIndicatedLocator

### Description
An object returned from [AutoTest.getLocatorWithIndicators](classes/AutoTest.md#classmethod-autotestgetlocatorwithindicators) that includes the locator and properties that describe the quality of the locator.

### Groups

- autoTest

---
## Object: ServerObject

### Description
The ServerObject tells the ISC server how to find or create a server-side object involved in [DMI](kb_topics/dmiOverview.md#kb-topic-direct-method-invocation) (Direct Method Invocation).

A ServerObject declaration appears in the XML definition of a [DataSource](classes/DataSource.md#class-datasource) (for responding to [DSRequest](#object-dsrequest)s) or in an Application configuration file (.app.xml) for responding to [RPCRequest](#object-rpcrequest)s.

NOTE: Please take note of the points made in [this discussion](kb_topics/serverDataSourceImplementation.md#kb-topic-notes-on-server-side-datasource-implementations) of caching and thread-safety issues in server-side DataSources.

### See Also

- [DMI](classes/DMI.md#class-dmi)

---
## Object: SingleSourceAIRequest

### Description
Represents a request to AI from a single [source](#type-aimessagesource) in some context.

---
## Object: StretchItem

### Description
An object representing one of the image segments displayed by a [StretchImg](classes/StretchImg.md#class-stretchimg). Each item of a StretchImg's [items](classes/StretchImg.md#attr-stretchimgitems) array is a StretchItem.

---
## Object: SystemAIRequest

### Description
Represents a programmer-specified request to AI in some context.

---
## Object: TaskDecision

### Description
Identifies a potential decision (branch) within a [MultiDecisionTask](classes/MultiDecisionTask.md#class-multidecisiontask). Each decision has a criteria and a target ProcessElement ID.

**Deprecated**

---
## Object: TestFunctionResult

### Description
A TestFunctionResult is an ordinary JavaScript Object with properties that indicate the status of an attempt to generate and execute a function for [FormulaBuilder](classes/FormulaBuilder.md#class-formulabuilder) and it's subclasses.

Because TestFunctionResult is always an ordinary JavaScript Object, it supports the normal behaviors of JavaScript Objects, including accessing and assigning to properties via dot notation:

```
     var propValue = testFunctionResult.propName;
     testFunctionResult.propName = newValue;
 
```

### Groups

- formulaFields

---
## Object: TreeNode

### Description
Every node in the tree is represented by a TreeNode object which is an object literal with a set of properties that configure the node.

When a Tree is supplied as [TreeGrid.data](classes/TreeGrid.md#attr-treegriddata) to [TreeGrid](classes/TreeGrid.md#class-treegrid), you can also set properties from [ListGridRecord](reference_2.md#object-listgridrecord) on the TreeNode (e.g. setting [ListGridRecord.enabled](classes/ListGridRecord.md#attr-listgridrecordenabled):`false` on the node).

---
## Object: UISummarySettings

### Description
Settings that control how a widget UI Summary is built.

---
## Object: UserAIRequest

### Description
Represents a user-specified and user-modifiable request to AI in some context. For example, the user's request may be in the context of AI-assisted filtering of a [ListGrid](classes/ListGrid_1.md#class-listgrid); in such a context, the user's request is their description of which records they would like to see.

The user's request is combined with other messages, data, and instructions provided by the framework to create [AIRequest](#object-airequest)s that are sent to the AI engine for the purpose of fulfilling the user's request.

---
## Object: WSRequest

### Description
A WSRequest (or "web service request") is an extended RPCRequest with additional properties applicable to WSDL/SOAP web services.

All properties which are legal on [RPCRequest](#object-rpcrequest) are legal on a WSRequest, in addition to the properties listed here.

### See Also

- [RPCRequest](#object-rpcrequest)

---
## Interface: Chart

### Description
Generic Chart properties and interfaces to be mixed into concrete charting implementations.

Components such as the [ListGrid](classes/ListGrid_2.md#method-listgridchartdata) and [CubeGrid](classes/CubeGrid.md#method-cubegridmakechart) expect this interface and can drive charting engines that support it.

Concrete Chart implementations may expose whatever properties they want for configuration, however, to enable easy switching of charting engines (different engines may be used for different end users based on that user's installed plugins), they should support the properties of this interface to the maximum extent possible.

This interface also provides core data model management (see [getValue()](classes/Chart.md#method-chartgetvalue)) for charting engines.

---
## Interface: PickList

### Description
Interface to show a drop-down list of pickable options. Used by the [SelectItem](classes/SelectItem.md#class-selectitem) and [ComboBoxItem](classes/ComboBoxItem.md#class-comboboxitem) classes. Depending on the value of [PickList.dataSetType](classes/PickList.md#attr-picklistdatasettype), the generated drop down list of options must be an instance of [PickListMenu](classes/PickListMenu.md#class-picklistmenu) or [PickTreeMenu](#class-picktreemenu), or a subclass thereof.

---
