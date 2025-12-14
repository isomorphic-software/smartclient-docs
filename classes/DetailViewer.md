# DetailViewer Documentation

[← Back to API Index](../reference.md)

---

## Class: DetailViewer

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
Displays one or more records "horizontally" with one property per line.

---
## Attr: DetailViewer.hiliteIconRightPadding

### Description
How much padding should there be on the right of [hilite icons](#attr-detailviewerhiliteicons) by default? Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DetailViewer.fieldPickerFieldProperties

### Description
Names of properties on [DetailViewerField](../reference.md#object-detailviewerfield) for which the [FieldPicker](FieldPicker.md#class-fieldpicker) should show an editing interface, for convenience.

For example, specify \["decimalPad", "decimalPrecision"\] to allow end users to modify [DetailViewerField.decimalPad](DetailViewerField.md#attr-detailviewerfielddecimalpad) and [DetailViewerField.decimalPrecision](DetailViewerField.md#attr-detailviewerfielddecimalprecision) respectively.

**Flags**: IR

---
## Attr: DetailViewer.fetchRequestProperties

### Description
If [DetailViewer.autoFetchData](#attr-detailviewerautofetchdata) is `true`, this attribute allows the developer to declaratively specify [DSRequest](../reference.md#object-dsrequest) properties for the initial [fetchData()](ListGrid_2.md#method-listgridfetchdata) call.

Note that any properties governing more specific request attributes for the initial fetch (such as [autoFetchTextMatchStyle](#attr-databoundcomponentautofetchtextmatchstyle) and initial sort specifiers) will be applied on top of this properties block.

### Groups

- databinding

**Flags**: IR

---
## Attr: DetailViewer.showDetailFields

### Description
Whether to show fields marked `detail:true` when a DataBoundComponent is given a DataSource but no `component.fields`.

The `detail` property is used on DataSource fields to mark fields that shouldn't appear by default in a view that tries to show many records in a small space.

### Groups

- databinding

**Flags**: IR

---
## Attr: DetailViewer.loadingMessage

### Description
The string to display in the body of a detailViewer which is loading records. Use `"${loadingImage}"` to include [a loading image](Canvas.md#classattr-canvasloadingimagesrc).

### Groups

- emptyMessage

**Flags**: IRW

---
## Attr: DetailViewer.emptyMessageStyle

### Description
CSS style to display this message in

### Groups

- emptyMessage

**Flags**: IRWA

---
## Attr: DetailViewer.valueAlign

### Description
Horizontal alignment of values in this viewer. If unspecified, defaults to `"right"` when in RTL mode and `"left"` otherwise.

### Groups

- values

**Flags**: IRW

---
## Attr: DetailViewer.labelPrefix

### Description
text to put before a label

### Groups

- labels

**Flags**: IRW

---
## Attr: DetailViewer.hiliteIconSize

### Description
Default width and height of [hilite icons](#attr-detailviewerhiliteicons) for this component. Can be overridden at the component level via explicit [hiliteIconWidth](#attr-detailviewerhiliteiconwidth) and [hiliteIconHeight](#attr-detailviewerhiliteiconheight), or at the field level via [hiliteIconSize](ListGridField.md#attr-listgridfieldhiliteiconsize), [hiliteIconWidth](ListGridField.md#attr-listgridfieldhiliteiconwidth) and [hiliteIconHeight](ListGridField.md#attr-listgridfieldhiliteiconheight)

### Groups

- hiliting

### See Also

- [DetailViewer.hiliteIconWidth](#attr-detailviewerhiliteiconwidth)
- [DetailViewer.hiliteIconHeight](#attr-detailviewerhiliteiconheight)
- [DetailViewerField.hiliteIconSize](DetailViewerField.md#attr-detailviewerfieldhiliteiconsize)

**Flags**: IRW

---
## Attr: DetailViewer.showEmptyField

### Description
Whether to show the field when the value is null

### Groups

- appearance

**Flags**: IRWA

---
## Attr: DetailViewer.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: DetailViewer.printHeaderStyle

### Description
Optional CSS style for a header in printable HTML for this component. If unset [DetailViewer.headerStyle](#attr-detailviewerheaderstyle) will be used for printing as well as normal presentation.

### Groups

- printing

**Flags**: IRW

---
## Attr: DetailViewer.hiliteIcons

### Description
Specifies a list of icons that can be used in [hilites](DataBoundComponent.md#method-databoundcomponentedithilites).

`hiliteIcons` should be specified as an Array of [SCImgURL](../reference.md#type-scimgurl). When present, the hilite editing interface shown when [DataBoundComponent.editHilites](DataBoundComponent.md#method-databoundcomponentedithilites) is called will offer the user a drop down for picking one of these icons when defining either a simple or advanced hilite rule.

If the user picks an icon, the created hiliting rule will have [Hilite.icon](Hilite.md#attr-hiliteicon) set to the chosen icon. [DataBoundComponent.hiliteIconPosition](DataBoundComponent.md#attr-databoundcomponenthiliteiconposition) controls where the icon will appear for that field -- the default is that it appears in front of the normal cell content. This can also be overridden at the field level.

### Groups

- hiliting

**Flags**: IR

---
## Attr: DetailViewer.dataArity

### Description
A DetailViewer is a [dataArity](DataBoundComponent.md#attr-databoundcomponentdataarity):either component by default which means data population from [Canvas.dataContext](Canvas.md#attr-canvasdatacontext) will be treated like a DynamicForm (i.e. single). However, by explicitly marking an instance of DetailViewer as `dataArity:multiple`, `dataContext` population will be treated similarly to a ListGrid.

**Flags**: IRWA

---
## Attr: DetailViewer.wrapLabel

### Description
Should the label be allowed to wrap, or be fixed to one line no matter how long

### Groups

- labels

**Flags**: IRW

---
## Attr: DetailViewer.emptyCellValue

### Description
Text to show for an empty cell

### Groups

- appearance

**Flags**: IRWA

---
## Attr: DetailViewer.fieldIdProperty

### Description
Name of the field in the DetailViewerRecord which specifies the data property for that record.

**Deprecated**

**Flags**: R

---
## Attr: DetailViewer.labelStyle

### Description
CSS style for a normal detail label

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.recordsPerBlock

### Description
The number of records to display in a block. A block is a horizontal row on a page containing one or more records, as specified by the value of recordsPerBlock. The height of a block is equal to the height of a single record. The default setting of 1 causes each record to appear by itself in a vertical row. Setting recordsPerBlock to 2 would cause records to appear side by side in groups of two. Use a value of "\*" to indicate all records.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.hiliteIconLeftPadding

### Description
How much padding should there be on the left of [hilite icons](#attr-detailviewerhiliteicons) by default? Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DetailViewer.rowHeight

### Description
Height of rows rendered by the DetailViewer. Acts as a minimum - the DetailViewer never clips values. This attribute can be set as null.

**Flags**: IRW

---
## Attr: DetailViewer.fields

### Description
An array of field objects, specifying the order and type of fields to display in this DetailViewer. In DetailViewers, the fields specify rows.

**Flags**: IRW

---
## Attr: DetailViewer.hiliteIconHeight

### Description
Height for hilite icons for this listGrid. Overrides [hiliteIconSize](#attr-detailviewerhiliteiconsize). Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DetailViewer.styleName

### Description
CSS style for the component as a whole.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria) and related methods.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

**Flags**: IRW

---
## Attr: DetailViewer.labelSuffix

### Description
text to put after a label

### Groups

- labels

**Flags**: IRW

---
## Attr: DetailViewer.cellStyle

### Description
CSS style for a normal value

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.printLabelStyle

### Description
Optional CSS style for a label cell in printable HTML for this component. If unset [DetailViewer.labelStyle](#attr-detailviewerlabelstyle) will be used for printing as well as normal presentation.

### Groups

- printing

**Flags**: IRW

---
## Attr: DetailViewer.dataFetchMode

### Description
DetailViewers do not yet support paging, and will fetch and render all available records.

### Groups

- databinding

**Flags**: IRW

---
## Attr: DetailViewer.fieldPickerWindow

### Description
Instance of [FieldPickerWindow](FieldPickerWindow.md#class-fieldpickerwindow) used if [DetailViewer.canPickFields](#attr-detailviewercanpickfields) is set.

**Flags**: IR

---
## Attr: DetailViewer.showEmptyMessage

### Description
Show [DetailViewer.emptyMessage](#attr-detailvieweremptymessage) when there is no data to display?

### Groups

- emptyMessage

### See Also

- [DetailViewer.emptyMessage](#attr-detailvieweremptymessage)

**Flags**: IRWA

---
## Attr: DetailViewer.datetimeFormatter

### Description
Display format to use for fields specified as type 'datetime'. Default is to use the system-wide default long ("normal") date time format, configured via [DateUtil.setNormalDatetimeDisplayFormat](DateUtil.md#classmethod-dateutilsetnormaldatetimedisplayformat). Specify any valid [DateDisplayFormat](../reference.md#type-datedisplayformat) to change the display format for datetimes used by this viewer. May be specified as a function. If specified as a function, this function will be executed in the scope of the Date and should return the formatted string.

May also be specified at the field level via [DetailViewerField.dateFormatter](DetailViewerField.md#attr-detailviewerfielddateformatter)

### Groups

- appearance

### See Also

- [ListGridField.dateFormatter](ListGridField.md#attr-listgridfielddateformatter)

**Flags**: IRW

---
## Attr: DetailViewer.headerStyle

### Description
CSS style for a header

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.blockStyle

### Description
CSS style for each block (one record's worth of data).

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.separatorStyle

### Description
CSS style for a separator

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.wrapValues

### Description
Whether values should be allowed to wrap by default, or should be shown on one line regardless of length.

### Groups

- labels

**Flags**: IR

---
## Attr: DetailViewer.printCellStyle

### Description
Optional CSS style for a cell in printable HTML for this component. If unset [DetailViewer.cellStyle](#attr-detailviewercellstyle) will be used for printing as well as normal presentation.

### Groups

- printing

**Flags**: IRW

---
## Attr: DetailViewer.emptyMessage

### Description
The string to display in the body of a detailViewer with no records.

### Groups

- emptyMessage

**Flags**: IRW

---
## Attr: DetailViewer.dateFormatter

### Description
How should Date type values be displayed in this DetailViewer by default?

This property specifies the default DateDisplayFormat to apply to Date values displayed in this grid for all fields except those of [type "time"](DetailViewerField.md#attr-detailviewerfieldtype) (See also [DetailViewer.timeFormatter](#attr-detailviewertimeformatter)).  
If [DetailViewer.datetimeFormatter](#attr-detailviewerdatetimeformatter) is specified, that will be applied by default to fields of type `"datetime"`.

Note that if [DetailViewerField.dateFormatter](DetailViewerField.md#attr-detailviewerfielddateformatter) or [DetailViewerField.timeFormatter](DetailViewerField.md#attr-detailviewerfieldtimeformatter) are specified those properties will take precedence over the component level settings.

If unset, date values will be formatted according to the system wide [normal display format](DateUtil.md#classmethod-dateutilsetnormaldisplayformat).

**Flags**: IRW

---
## Attr: DetailViewer.canPickFields

### Description
If set, right-clicking on the DetailViewer will show a context menu that offers to bring up a [FieldPicker](FieldPicker.md#class-fieldpicker) for configuring which fields are displayed and their order.

**Flags**: IR

---
## Attr: DetailViewer.hiliteIconPosition

### Description
When [hiliteIcons](#attr-detailviewerhiliteicons) are present, where the hilite icon will be placed relative to the field value. See [HiliteIconPosition](../reference.md#type-hiliteiconposition). Can be overridden at the field level.

### Groups

- hiliting

**Flags**: IR

---
## Attr: DetailViewer.data

### Description
A single record object or an array of them, specifying data. Note that DetailViewers do not observe changes to the data array (in other words they will not automatically re-draw when the data provided via this property is altered).

### Groups

- basics

**Flags**: IRW

---
## Attr: DetailViewer.labelAlign

### Description
Horizontal alignment of value-labels in this viewer. If unspecified, defaults to `"left"` when in RTL mode and `"right"` otherwise.

### Groups

- labels

**Flags**: IRW

---
## Attr: DetailViewer.blockSeparator

### Description
A string (HTML acceptable) that will be written to a page to separate blocks.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.configureFieldsText

### Description
The title for the Configure Fields menu item.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DetailViewer.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: DetailViewer.initialCriteria

### Description
Criteria to be used when [DetailViewer.autoFetchData](#attr-detailviewerautofetchdata) is set.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

### Groups

- searchCriteria

**Flags**: IR

---
## Attr: DetailViewer.hiliteIconWidth

### Description
Width for hilite icons for this component. Overrides [hiliteIconSize](#attr-detailviewerhiliteiconsize). Can be overridden at the field level.

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DetailViewer.loadingMessageStyle

### Description
CSS style to use for the [DetailViewer.loadingMessage](#attr-detailviewerloadingmessage).

### Groups

- emptyMessage

**Flags**: IRWA

---
## Attr: DetailViewer.timeFormatter

### Description
Display format to use for fields specified as type 'time'. May also be specified at the field level via [DetailViewerField.timeFormatter](DetailViewerField.md#attr-detailviewerfieldtimeformatter).  
If unset, time fields will be formatted based on the system wide [Time.setNormalDisplayFormat](Time.md#classmethod-timesetnormaldisplayformat)

### Groups

- appearance

**Flags**: IRW

---
## Attr: DetailViewer.linkTextProperty

### Description
Property name on a record that will hold the link text for that record.

This property is configurable to avoid possible collision with data values in the record.

Use [DetailViewerField.linkTextProperty](DetailViewerField.md#attr-detailviewerfieldlinktextproperty) if you have more than one link field and the fields' records do not use the same property to store the linkText.

### See Also

- [DetailViewerField.linkText](DetailViewerField.md#attr-detailviewerfieldlinktext)
- [DetailViewerField.linkTextProperty](DetailViewerField.md#attr-detailviewerfieldlinktextproperty)

**Flags**: IRW

---
## Attr: DetailViewer.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [DetailViewer.initialCriteria](#attr-detailviewerinitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle). Additional request properties may be specified using [DetailViewer.fetchRequestProperties](#attr-detailviewerfetchrequestproperties).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_2.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [DetailViewer.initialCriteria](#attr-detailviewerinitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_2.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- databinding

### See Also

- [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata)

**Flags**: IR

---
## Method: DetailViewer.fieldIsVisible

### Description
Check whether a field is currently visible

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [String](#type-string)|[DetailViewerField](#type-detailviewerfield) | false | — | field to be checked |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the field is currently visible, false otherwise.

---
## Method: DetailViewer.getViewState

### Description
Returns a snapshot of the current view state of this DetailViewer.  
This includes the field state of the DetailViewer, returned as a [DetailViewerViewState](../reference.md#type-detailviewerviewstate) object.  
This object can be passed to [DetailViewer.setViewState](#method-detailviewersetviewstate) to reset this detail viewer's view state to the current state (assuming the same data / fields are present in the detail viewer).

### Returns

`[DetailViewerViewState](../reference.md#type-detailviewerviewstate)` — current view state for the detail viewer.

### Groups

- viewState

### See Also

- [DetailViewerViewState](../reference.md#type-detailviewerviewstate)
- [DetailViewer.setViewState](#method-detailviewersetviewstate)

---
## Method: DetailViewer.isExportingClientData

### Description
Returns true if this component is currently [exporting client data](#method-detailviewerexportclientdata). This method can be called from custom cell formatters if you need to return a different formatted value for an export than for a live detailViewer

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if this component is currently exporting client data

### See Also

- [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata)

---
## Method: DetailViewer.getCellStyle

### Description
Return the CSS class for a cell. Default implementation calls [getCellStyle()](DetailViewerField.md#method-detailviewerfieldgetcellstyle) on the field if defined, otherwise returns [this.cellStyle](#attr-detailviewercellstyle)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | actual value of this cell |
| field | [DetailViewerField](#type-detailviewerfield) | false | — | field object for this cell |
| record | [Record](#type-record) | false | — | record object for this cell |
| viewer | [DetailViewer](#type-detailviewer) | false | — | the viewer instance to which this cell belongs |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS style for this cell

### Groups

- appearance

---
## Method: DetailViewer.setViewState

### Description
Reset this detail viewer's view state to match the [DetailViewerViewState](../reference.md#type-detailviewerviewstate) object passed in.  
Used to restore previous state retrieved from the detail viewer by a call to [DetailViewer.getViewState](#method-detailviewergetviewstate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewState | [DetailViewerViewState](../reference.md#type-detailviewerviewstate) | false | — | Object describing the desired view state for the detail viewer |

### Groups

- viewState

### See Also

- [DetailViewer.getViewState](#method-detailviewergetviewstate)

---
## Method: DetailViewer.setData

### Description
Sets the data displayed by this detail viewer.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [Array of DetailViewerRecord[]](#type-array-of-detailviewerrecord)|[Array of Record[]](#type-array-of-record)|[RecordList](#type-recordlist) | false | — | new data to be displayed |

---
## Method: DetailViewer.fetchRelatedData

### Description
Based on the relationship between the DataSource this component is bound to and the DataSource specified as the "schema" argument, call fetchData() to retrieve records in this data set that are related to the passed-in record.

Relationships between DataSources are declared via [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey).

For example, given two related DataSources "orders" and "orderItems", where we want to fetch the "orderItems" that belong to a given "order". "orderItems" should declare a field that is a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) to the "orders" table (for example, it might be named "orderId" with foreignKey="orders.id"). Then, to load the records related to a given "order", call fetchRelatedData() on the component bound to "orderItems", pass the "orders" DataSource as the "schema" and pass a record from the "orders" DataSource as the "record" argument.

**Note:** When you expect a large number of records to be returned it is not recommended to display these in the DetailViewer as it doesn't have the same level of support for large datasets as the [ListGrid](ListGrid_1.md#class-listgrid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | DataSource record |
| schema | [Canvas](#type-canvas)|[DataSource](#type-datasource)|[ID](#type-id) | false | — | schema of the DataSource record, or DataBoundComponent already bound to that schema |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: DetailViewer.exportData

### Description
Sends the current filter criteria and sort direction to the server, then exports data in the requested [exportFormat](DSRequest.md#attr-dsrequestexportas).

A variety of DSRequest settings, such as [exportAs](DSRequest.md#attr-dsrequestexportas) and [DSRequest.exportFilename](DSRequest.md#attr-dsrequestexportfilename), affect the exporting process: see [exportResults](DSRequest.md#attr-dsrequestexportresults) for further detail.

Note that data exported via this method skips client-side fields defined only in the component, excludes any client-side formatting and relies on both the SmartClient server and server-side DataSources. To export client-data including client-only fields and with client-side formatting applied, see [exportClientData](ListGrid_2.md#method-listgridexportclientdata), which still requires the SmartClient server but does not rely on server-side DataSource definitions (.ds.xml files).

For more information on exporting data, see [DataSource.exportData](DataSource.md#method-datasourceexportdata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion. Note that this parameter only applies where [DSRequest.exportToClient](DSRequest.md#attr-dsrequestexporttoclient) is explicitly set to false, because file downloads do not provide ordinary SmartClient callbacks |

### Groups

- dataBoundComponentMethods

### See Also

- [exportFormatting](../kb_topics/exportFormatting.md#kb-topic-exports--formatting)

---
## Method: DetailViewer.viewSelectedData

### Description
Displays the currently selected record(s) of the selectionComponent widget (typically a listGrid) in this component.

For a DynamicForm the first record of the selection is shown after the form is placed into [read-only mode](DynamicForm.md#attr-dynamicformcanedit). A subsequent call to [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) or similar will return the form to editability.

Note that since field-level `canEdit:true` settings override the form-level canEdit setting the automatic change to read-only may not change every field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectionComponent | [ListGrid](#type-listgrid)|[TileGrid](#type-tilegrid)|[ID](#type-id) | false | — | the ListGrid or TileGrid or ID of a [ListGrid](ListGrid_1.md#class-listgrid)/[TileGrid](TileGrid.md#class-tilegrid) whose currently selected record(s) is/are to be viewed |

### Groups

- dataBoundComponentMethods

---
## Method: DetailViewer.exportClientData

### Description
Exports this component's data with client-side formatters applied, so is suitable for direct display to users. See [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata) for details of the general requirements and restrictions when exporting client data.

The following notes apply when exporting client data from DetailViewers:

*   Data is exported in "grid" format, with each record shown in a single row and each column representing a single field. This is quite different from the way DetailViewers display records in the browser

If your detailViewer has custom formatters, formatted values will be exported by default, with HTML normalized to text where possible. Since some levels of HTML normalizing aren't possible, this may result in missing or incorrect export values. In this case, you have two possible approaches:

*   Set [exportRawValues](DetailViewerField.md#attr-detailviewerfieldexportrawvalues) on the field. This will export the raw underlying value of the field; your formatter will not be called
*   Have your formatter call [isExportingClientData()](#method-detailviewerisexportingclientdata) and perform whatever alternative formatting you require if that method returns true

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Request properties for the export. Note that specifying [exportData](DSRequest.md#attr-dsrequestexportdata) on the request properties allows the developer to pass in an explicit data set to export. |
| callback | [RPCCallback](#type-rpccallback) | true | — | Optional callback. If you specify [exportToClient](DSRequest.md#attr-dsrequestexporttoclient): false in the request properties, this callback will fire after export completes. Otherwise the callback will fire right before the download request is made to the server. |

### See Also

- [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata)

---
## Method: DetailViewer.emptyMessageHTML

### Description
Return the message to show if the component has no data. Default implementation returns a centered [DetailViewer.emptyMessage](#attr-detailvieweremptymessage) or "&nbsp;" if showEmptyMessage is false. If the component has no data because the browser is offline, we instead display the [DataBoundComponent.offlineMessage](DataBoundComponent.md#attr-databoundcomponentofflinemessage) or "&nbsp;" if showOfflineMessage is false

### Returns

`[String](#type-string)` — HTML output

**Flags**: A

---
## Method: DetailViewer.getCellCSSText

### Description
Return CSS text for styling this cell, which will be applied in addition to the CSS class for the cell, as overrides.

"CSS text" means semicolon-separated style settings, suitable for inclusion in a CSS stylesheet or in a STYLE attribute of an HTML element.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | actual value of this cell |
| field | [DetailViewerField](#type-detailviewerfield) | false | — | field object for this cell |
| record | [Record](#type-record) | false | — | record object for this cell |
| viewer | [DetailViewer](#type-detailviewer) | false | — | the viewer instance to which this cell belongs |

### Returns

`[CSSText](../reference_2.md#type-csstext)` — CSS text to add to this cell

### Groups

- appearance

---
## Method: DetailViewer.getRecordIndex

### Description
Get the index of the provided record.

Override in subclasses to provide more specific behavior, for instance, when data holds a large number of records

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record whose index is to be retrieved |

### Returns

`[Number](#type-number)` — indexindex of the record, or -1 if not found

---
## Method: DetailViewer.setHilites

### Description
Only supported on ListGrid for now.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hilites | [Array of Hilite](#type-array-of-hilite) | false | — | Array of hilite objects |

### Groups

- hiliting

---
## Method: DetailViewer.formatCellValue

### Description
Optional method to format the value to display for cells in this DetailViewer. Note that if [DetailViewerField.formatCellValue](DetailViewerField.md#method-detailviewerfieldformatcellvalue) is specified this method will not be called for cells within that field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | the raw value of the cell (may be formatted by [DetailViewerField.formatCellValue](DetailViewerField.md#method-detailviewerfieldformatcellvalue) |
| record | [DetailViewerRecord](#type-detailviewerrecord) | false | — | the record being displayed |
| field | [DetailViewerField](#type-detailviewerfield) | false | — | the field being displayed |

---
