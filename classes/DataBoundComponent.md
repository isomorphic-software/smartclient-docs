# DataBoundComponent Documentation

[← Back to API Index](../reference.md)

---

## Attr: DataBoundComponent.dataFetchMode

### Description
How to fetch and manage records retrieve from the server. See [FetchMode](../reference_2.md#type-fetchmode).

This setting only applies to the [ResultSet](ResultSet.md#class-resultset) automatically created by calling [fetchData()](ListGrid_1.md#method-listgridfetchdata). If a pre-existing ResultSet is passed to setData() instead, it's existing setting for [ResultSet.fetchMode](ResultSet.md#attr-resultsetfetchmode) applies.

### Groups

- databinding

**Flags**: IR

---
## Attr: DataBoundComponent.emptyGeneratedHoverContents

### Description
Hover contents to use when the generated hover contents are empty

### Groups

- pseudoFieldGeneration
- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.descriptionField

### Description
Name of the field that has a long description of the record, or has the primary text data value for a record that represents an email message, SMS, log or similar.

This attribute has the same function as [DataSource.descriptionField](DataSource.md#attr-datasourcedescriptionfield) but can be set for a component with no dataSource, or can be used to override the dataSource setting.

**Flags**: IR

---
## Attr: DataBoundComponent.initialCriteria

### Description
Criteria to be used when [DataBoundComponent.autoFetchData](#attr-databoundcomponentautofetchdata) is set.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

**Flags**: IR

---
## Attr: DataBoundComponent.fieldEditorWindowTitle

### Description
The title for the [Window](#attr-databoundcomponentfieldeditorwindow) used to edit calculated fields.

This is a dynamic string - text within `${...}` are dynamic variables and will be evaluated as JS code whenever the message is displayed.

Two dynamic variables are available - "builderType", either Formula or Summary, and "fieldTitle", which is the title of the calculated field being edited.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: DataBoundComponent.dragTrackerStyle

### Description
CSS Style to apply to the drag tracker when dragging occurs on this component.

**Flags**: IRW

---
## Attr: DataBoundComponent.hiliteState

### Description
Initial hilite state for the grid.

[ListGrid.viewState](ListGrid_1.md#attr-listgridviewstate) can be used to initialize all view properties of the grid. When doing so, `hiliteState` is not needed because `viewState` includes it as well. If both are provided, `hiliteState` has priority for hilite state.

To retrieve current state call [getHiliteState](#method-databoundcomponentgethilitestate).

### Groups

- viewState

**Flags**: IRW

---
## Attr: DataBoundComponent.canEditHilites

### Description
Adds an item to the header context menu allowing users to launch a dialog to define grid hilites using the [HiliteEditor](HiliteEditor.md#class-hiliteeditor).

User-added hilites can be persisted via [DataBoundComponent.getHiliteState](#method-databoundcomponentgethilitestate) and [DataBoundComponent.setHiliteState](#method-databoundcomponentsethilitestate).

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DataBoundComponent.multiSortDialogProperties

### Description
Properties to apply to the [MultiSortDialog](MultiSortDialog.md#class-multisortdialog) which gets automatically generated when [DataBoundComponent.askForSort](#method-databoundcomponentaskforsort) is called.

See also [ListGrid.showHeaderSpanTitlesInSortEditor](ListGrid_1.md#attr-listgridshowheaderspantitlesinsorteditor) and [ListGrid.sortEditorSpanTitleSeparator](ListGrid_1.md#attr-listgridsorteditorspantitleseparator)

**Flags**: IR

---
## Attr: DataBoundComponent.emptyExportMessage

### Description
The message to display to the user if an export of a DataBoundComponent's data is attempted while the DataBoundComponent's data is null or an empty list.

### Groups

- i18nMessages

### See Also

- [ListGrid.exportClientData](ListGrid_1.md#method-listgridexportclientdata)

**Flags**: IRW

---
## Attr: DataBoundComponent.hiliteIcons

### Description
Specifies a list of icons that can be used in [hilites](#method-databoundcomponentedithilites).

`hiliteIcons` should be specified as an Array of [SCImgURL](../reference.md#type-scimgurl). When present, the hilite editing interface shown when [DataBoundComponent.editHilites](#method-databoundcomponentedithilites) is called will offer the user a drop down for picking one of these icons when defining either a simple or advanced hilite rule.

If the user picks an icon, the created hiliting rule will have [Hilite.icon](Hilite.md#attr-hiliteicon) set to the chosen icon. [DataBoundComponent.hiliteIconPosition](#attr-databoundcomponenthiliteiconposition) controls where the icon will appear for that field -- the default is that it appears in front of the normal cell content. This can also be overridden at the field level.

### Groups

- hiliting

**Flags**: IR

---
## Attr: DataBoundComponent.canAddFormulaFields

### Description
Adds an item to the header context menu allowing users to launch a dialog to define a new field based on values present in other fields, using the [FormulaBuilder](FormulaBuilder.md#class-formulabuilder).

User-added formula fields can be persisted via [ListGrid.getFieldState](ListGrid_2.md#method-listgridgetfieldstate) and [ListGrid.setFieldState](ListGrid_2.md#method-listgridsetfieldstate).

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: DataBoundComponent.offlineSaveMessage

### Description
Message to display when this DataBoundComponent attempts to save data while the application is offline.

### Groups

- i18nMessages
- offlineGroup

**Flags**: IRW

---
## Attr: DataBoundComponent.iconField

### Description
Designates a field of [type](../reference_2.md#type-fieldtype):"image" as the field to use when rendering a record as an image, for example, in a [TileGrid](TileGrid.md#class-tilegrid).

This attribute has the same function as [DataSource.iconField](DataSource.md#attr-datasourceiconfield) but can be set for a component with no dataSource, or can be used to override the dataSource setting.

**Flags**: IR

---
## Attr: DataBoundComponent.multiSortDialogDefaults

### Description
Class level defaults to apply to the [MultiSortDialog](MultiSortDialog.md#class-multisortdialog) which gets automatically generated when [DataBoundComponent.askForSort](#method-databoundcomponentaskforsort) is called.

See also [ListGrid.showHeaderSpanTitlesInSortEditor](ListGrid_1.md#attr-listgridshowheaderspantitlesinsorteditor) and [ListGrid.sortEditorSpanTitleSeparator](ListGrid_1.md#attr-listgridsorteditorspantitleseparator)

**Flags**: IR

---
## Attr: DataBoundComponent.noErrorDetailsMessage

### Description
A message to display to the user if server-side validation fails with an error but the server did not provide an error message

### Groups

- validation
- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.hiliteIconHeight

### Description
Height for hilite icons for this listGrid. Overrides [hiliteIconSize](#attr-databoundcomponenthiliteiconsize). Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DataBoundComponent.exportAs

### Description
The format in which the data should be exported if [DataBoundComponent.exportData](#method-databoundcomponentexportdata) is called without specifying a format. Otherwise, the format passed to [DataBoundComponent.exportData](#method-databoundcomponentexportdata) via the requestProperties parameter will be used.

See [ExportFormat](../reference_2.md#type-exportformat) for more information.

**Flags**: IR

---
## Attr: DataBoundComponent.addSummaryFieldText

### Description
Text for a menu item allowing users to add a formula field

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.dragDataAction

### Description
Indicates what to do with data dragged into another DataBoundComponent. See DragDataAction type for details.

### Groups

- dragging

**Flags**: IRW

---
## Attr: DataBoundComponent.offlineMessage

### Description
Message to display when this DataBoundComponent attempts to load data that is not available because the browser is currently offline. Depending on the component, the message is either displayed in the component's body, or in a pop-up warning dialog.

### Groups

- i18nMessages
- offlineGroup

**Flags**: IRW

---
## Attr: DataBoundComponent.canChangeNonFieldValues

### Description
If this attribute is set to false, any attributes in the component's values object that do not map to a [field](../reference_2.md#object-datasourcefield) or [formItem](FormItem.md#class-formitem) will not be tracked when checking for changes. You should only set this flag to false if you know that your code does not store additional, non-field values in the component's data, or if you do store such values, but you don't care that they are not checked for changes. This flag is primarily provided to avoid performance issues in cases where developers are storing large numbers of extra attributes in component data; generally speaking, you should only consider setting it to false if you have a use case like this.

Note, even with this flag set to false, these extra values will still be managed and stored by SmartClient; they just will not be checked when the component's values are inspected to see if they have changed. This may lead to methods like [ListGrid.rowHasChanges](ListGrid_2.md#method-listgridrowhaschanges) returning false when you are expecting it to return true. In this case, either switch this flag back to true (or just do not set it false), or provide a field definition for the affected attribute(s).

**Flags**: IRWA

---
## Attr: DataBoundComponent.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](#attr-databoundcomponentinitialcriteria) and related methods.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

**Flags**: IRW

---
## Attr: DataBoundComponent.titleField

### Description
Best field to use for a user-visible title for an individual record from this component.

This attribute has the same function as [DataSource.iconField](DataSource.md#attr-datasourceiconfield) but can be set for a component with no dataSource, or can be used to override the dataSource setting.

**Flags**: IR

---
## Attr: DataBoundComponent.hiliteEditor

### Description
This component's HiliteEditor instance used to allow the user to create, modify, or delete hilites.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [DataBoundComponent.hiliteIcons](#attr-databoundcomponenthiliteicons) for [HiliteEditor.hiliteIcons](HiliteEditor.md#attr-hiliteeditorhiliteicons)

### Groups

- hiliting

**Flags**: R

---
## Attr: DataBoundComponent.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: DataBoundComponent.fieldNamingStrategy

### Description
The strategy to use when generating names for new fields in this component. The default strategy, "simple", combines the field-type with an index maintained by field-type and component instance. For example, "formulaField1".

**Flags**: IRW

---
## Attr: DataBoundComponent.sparseFieldState

### Description
Should [DataBoundComponent.getFieldState](#method-databoundcomponentgetfieldstate) and [DataBoundComponent.setFieldState](#method-databoundcomponentsetfieldstate) omit state information for hidden fields by default?

**Flags**: IRWA

---
## Attr: DataBoundComponent.logSavedSearchIdWarningOnDSChange

### Description
SavedSearches are associated with a component by an id string value calculated as described in [SavedSearches.getSavedSearchId](SavedSearches.md#method-savedsearchesgetsavedsearchid).

If an application changes the dataSource associated with a component at runtime via [DataBoundComponent.setDataSource](#method-databoundcomponentsetdatasource), if this id is not also modified, any previously created savedSearches will still be associated with the component, but may not be applicable to the new DataSource.

SmartClient has logic to automatically detect this case and log a warning by default. This property may be set to false to suppress this warning - useful for cases where you want to use the same set of stored SavedSearches even after a component's dataSource has been changed.

**Flags**: IRWA

---
## Attr: DataBoundComponent.unknownErrorMessage

### Description
For databound components that support editing, the error message for a failed validator that does not specify its own errorMessage.

### Groups

- validation
- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.dropValues

### Description
When an item is dropped on this component, and [DataBoundComponent.addDropValues](#attr-databoundcomponentadddropvalues) is true and both the source and target widgets are databound, either to the same DataSource or to different DataSources that are related via a foreign key, this object provides the "drop values" that SmartClient will apply to the dropped object before updating it.

If this property is not defined, SmartClient defaults to returning the selection criteria currently in place for this component. Thus, any databound items (for example, rows from other grids bound to the same DataSource) dropped on the grid will, by default, be subjected to an update that makes them conform to the grid's current filter criteria.

### Groups

- dragging

**Flags**: IRWA

---
## Attr: DataBoundComponent.updateOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) this component should use when performing update operations.

### Groups

- operations

**Flags**: IRW

---
## Attr: DataBoundComponent.editSummaryFieldText

### Description
Text for a menu item allowing users to edit the formatter for a field

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.dataPageSize

### Description
When using [data paging](#attr-databoundcomponentdatafetchmode), how many records to fetch at a time. If set to a positive integer, `dataPageSize` will override the default [resultSize](ResultSet.md#attr-resultsetresultsize) for ResultSets automatically created when you call [fetchData()](ListGrid_1.md#method-listgridfetchdata) (and similarly for the [resultSize](ResultTree.md#attr-resulttreeresultsize) of ResultTrees). Leaving `dataPageSize` at its default means to just use the default page size of the data container.

**Note** that regardless of the `dataPageSize` setting, a component will always fetch all of data that it needs to draw. Settings such as [showAllRecords:true](ListGrid_1.md#attr-listgridshowallrecords), [drawAllMaxCells](ListGrid_1.md#attr-listgriddrawallmaxcells) and [drawAheadRatio](ListGrid_1.md#attr-listgriddrawaheadratio) can cause more rows than the configured `dataPageSize` to be fetched.

### Groups

- databinding

### See Also

- [ResultSet.resultSize](ResultSet.md#attr-resultsetresultsize)

**Flags**: IRW

---
## Attr: DataBoundComponent.editHilitesDialogTitle

### Description
The title for the [Hilite Editor](#method-databoundcomponentedithilites) dialog.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DataBoundComponent.fieldEditorWindow

### Description
The [Window](Window.md#class-window) used to edit calculated fields for this component.

**Flags**: R

---
## Attr: DataBoundComponent.fields

### Description
A DataBoundComponent manipulates records with one or more fields, and `component.fields` tells the DataBoundComponent which fields to present, in what order, and how to present each field.

When both `component.fields` and `[component.dataSource](#attr-databoundcomponentdatasource)` are set, any fields in `component.fields` with the same name as a DataSource field inherit properties of the DataSource field. This allows you to centralize data model information in the DataSource, but customize presentation of DataSource fields on a per-component basic. For example, in a ListGrid, a shorter title or format for a field might be chosen to save space.

By default, only fields specified on the component are shown, in the order specified on the component. The [DataBoundComponent.useAllDataSourceFields](#attr-databoundcomponentusealldatasourcefields) flag can be set to show all fields from the DataSource, with `component.fields` acting as field-by-field overrides and/or additional fields.

If a DataBoundComponent is given a DataSource, but no `component.fields`, the "default binding" is used: fields are shown in DataSource order, according to the properties `[DataBoundComponent.showHiddenFields](#attr-databoundcomponentshowhiddenfields)` and `[DataBoundComponent.showDetailFields](#attr-databoundcomponentshowdetailfields)`.

### Groups

- databinding

**Flags**: IRW

---
## Attr: DataBoundComponent.placeholderGeneratedHoverContents

### Description
Default message to display in the hover while the hover contents are being generated

### Groups

- pseudoFieldGeneration
- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.deepCloneNonFieldValuesOnEdit

### Description
When editing values in this DataBoundComponent, should we perform a deep clone of values that are not associated with a field (ie, attributes on the record that do not map to a component field either directly by name, or by [FormItem.dataPath](FormItem.md#attr-formitemdatapath). If this value is not explicitly set, it defaults to the value of [DataSource.deepCloneNonFieldValuesOnEdit](DataSource.md#attr-datasourcedeepclonenonfieldvaluesonedit) if there is a dataSource, or to the value of the static [DataSource.deepCloneNonFieldValuesOnEdit](DataSource.md#classattr-datasourcedeepclonenonfieldvaluesonedit) if there is no dataSource.

Like the other `deepCloneOnEdit` settings, this flag only has an effect if you are editing a values object that contains nested objects or arrays.

### See Also

- [Canvas.dataPath](Canvas.md#attr-canvasdatapath)
- [FormItem.dataPath](FormItem.md#attr-formitemdatapath)
- [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit)
- [DataSource.deepCloneOnEdit](DataSource.md#attr-datasourcedeepcloneonedit)

**Flags**: IRWA

---
## Attr: DataBoundComponent.dataArity

### Description
Does this component represent singular or multiple "records" objects? Options are "multiple", "single" or "either".

This property is used within a [ValuesManager](ValuesManager.md#class-valuesmanager) and also controls how auto-population works if the component is in a [Canvas.dataContext](Canvas.md#attr-canvasdatacontext) and [Canvas.autoPopulateData](Canvas.md#attr-canvasautopopulatedata) is set.

**Flags**: IRWA

---
## Attr: DataBoundComponent.duplicateDragMessage

### Description
Message to show when a user attempts to transfer duplicate records into this component, and [DataBoundComponent.preventDuplicates](#attr-databoundcomponentpreventduplicates) is enabled.

If set to null, duplicates will not be reported and the dragged duplicates will not be saved.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DataBoundComponent.removeFormulaFieldText

### Description
Text for a menu item allowing users to remove a formula field

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.exportOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) this component should use when performing server-driven exports via the exportData() API. If this property is not set, exportData() exports will use the [fetchOperation](#attr-databoundcomponentfetchoperation) instead. If you want to switch off this automatic use of the `fetchOperation` for exportData() exports, specify `exportOperation: ""`

### Groups

- operations

**Flags**: IRW

---
## Attr: DataBoundComponent.useFlatFields

### Description
The `useFlatFields` flag causes all simple type fields anywhere in a nested set of DataSources to be exposed as a flat list for form binding.

`useFlatFields` is typically used with imported metadata, such as [XML Schema](XMLTools.md#classmethod-xmltoolsloadxmlschema) from a [WSDL-described web service](XMLTools.md#classmethod-xmltoolsloadwsdl), as a means of eliminating levels of XML nesting that aren't meaningful in a user interface, without the cumbersome and fragile process of mapping form fields to XML structures.

For example, having called [WebService.getInputDS](WebService.md#method-webservicegetinputds) to retrieve the input message schema for a web service operation whose input message looks like this:

```
 <FindServices>
     <searchFor>search text</searchFor>
     <Options>
         <caseSensitive>false</caseSensitive>
     </Options>
     <IncludeInSearch>
         <serviceName>true</serviceName>
         <documentation>true</documentation>
         <keywords>true</keywords>
     </IncludeInSearch>
 </FindServices>
 
```
Setting `useFlatFields` on a [DynamicForm](DynamicForm.md#class-dynamicform) that is bound to this input message schema would result in 5 [FormItems](FormItem.md#class-formitem) reflecting the 5 simple type fields in the message.

For this form, the result of [form.getValues()](DynamicForm.md#method-dynamicformgetvalues) might look like:

```
{
    searchFor: "search text",
    caseSensitive: false,
    serviceName: true,
    documentation : true,
    keywords : true
 }
```
When contacting a [WSDL web service](WebService.md#class-webservice), these values can be automatically mapped to the structure of the input message for a web service operation by setting [WSRequest.useFlatFields](WSRequest.md#attr-wsrequestuseflatfields) (for use with [WebService.callOperation](WebService.md#method-webservicecalloperation)) or by setting [DSRequest.useFlatFields](DSRequest.md#attr-dsrequestuseflatfields) (for use with a [DataSource](DataSource.md#class-datasource) that is [bound to a WSDL web service](../kb_topics/wsdlBinding.md#kb-topic-wsdl-binding) via [OperationBinding.wsOperation](OperationBinding.md#attr-operationbindingwsoperation)).

Using these two facilities in conjunction (component.useFlatFields and request.useFlatFields) allows gratuitous nesting to be consistently bypassed in both the user presentation and when providing the data for XML messages.

You can also set [OperationBinding.useFlatFields](OperationBinding.md#attr-operationbindinguseflatfields) to automatically enable "flattened" XML serialization (request.useFlatFields) for all DataSource requests of a particular operationType.

Note that `useFlatFields` is not generally recommended for use with structures where multiple simple type fields exist with the same name, however if used with such a structure, the first field to use a given name wins. "first" means the first field encountered in a depth first search. "wins" means only the first field will be present as a field when data binding.

**Flags**: IR

---
## Attr: DataBoundComponent.infoField

### Description
Name of the field that has the second most pertinent piece of textual information in the record, for use when a [DataBoundComponent](../reference.md#interface-databoundcomponent) needs to show a short summary of a record.

This attribute has the same function as [DataSource.infoField](DataSource.md#attr-datasourceinfofield) but can be set for a component with no dataSource, or can be used to override the dataSource setting.

**Flags**: IR

---
## Attr: DataBoundComponent.hilites

### Description
Hilites to be applied to the data for this component. See [hiliting](../kb_topics/hiliting.md#kb-topic-hiliting).

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DataBoundComponent.badFormulaResultValue

### Description
If the result of a formula evaluation is invalid (specifically, if isNaN(result)==true), badFormulaResultValue is displayed instead. The default value is ".".

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: DataBoundComponent.dataField

### Description
Name of the field that has the most pertinent numeric, date, or enum value, for use when a [DataBoundComponent](../reference.md#interface-databoundcomponent) needs to show a short summary of a record.

This attribute has the same function as [DataSource.dataField](DataSource.md#attr-datasourcedatafield) but can be set for a component with no dataSource, or can be used to override the dataSource setting.

**Flags**: IR

---
## Attr: DataBoundComponent.editHilitesText

### Description
Text for a menu item allowing users to edit grid highlights.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.addFormulaFieldText

### Description
Text for a menu item allowing users to add a formula field

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.exportFields

### Description
The list of field-names to export. If provided, the field-list in the exported output is limited and sorted as per the list.

If exportFields is not provided, the exported output includes all visible fields from this component, sorted as they appear.

**Flags**: IRW

---
## Attr: DataBoundComponent.showOfflineMessage

### Description
Indicates whether the text of the offlineMessage property should be displayed if no data is available because we do not have a suitable offline cache

### Groups

- offlineGroup

### See Also

- [DataBoundComponent.offlineMessage](#attr-databoundcomponentofflinemessage)

**Flags**: IRW

---
## Attr: DataBoundComponent.exportDisplay

### Description
Specifies whether the exported data will be downloaded as an attachment or displayed in a new browser window. This option will be used if [DataBoundComponent.exportData](#method-databoundcomponentexportdata) is called without specifying it. Otherwise, the exportDisplay passed to [DataBoundComponent.exportData](#method-databoundcomponentexportdata) via the requestProperties parameter will be used.

See [ExportDisplay](../reference_2.md#type-exportdisplay) for more information.

**Flags**: IR

---
## Attr: DataBoundComponent.useAllDataSourceFields

### Description
If true, the set of fields given by the "default binding" (see [DataBoundComponent.fields](#attr-databoundcomponentfields)) is used, with any fields specified in `component.fields` acting as overrides that can suppress or modify the display of individual fields, without having to list the entire set of fields that should be shown.

If `component.fields` contains fields that are not found in the DataSource, they will be shown after the most recently referred to DataSource field. If the new fields appear first, they will be shown first.

*This example* shows a mixture of component fields and DataSource fields, and how they interact for validation.

This setting may be cleared if a [FieldPicker](FieldPicker.md#class-fieldpicker) is used to edit the component's field order.

### Groups

- databinding

### See Also

- [FieldPicker.dataBoundComponent](FieldPicker.md#attr-fieldpickerdataboundcomponent)

**Flags**: IRW

---
## Attr: DataBoundComponent.preventDuplicates

### Description
If set, detect and prevent duplicate records from being transferred to this component, either via drag and drop or via [DataBoundComponent.transferSelectedData](#method-databoundcomponenttransferselecteddata). When a duplicate transfer is detected, a dialog will appear showing the [DataBoundComponent.duplicateDragMessage](#attr-databoundcomponentduplicatedragmessage).

If the component either does not have a [DataSource](DataSource.md#class-datasource) or has a DataSource with no [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) declared, duplicate checking is off by default. If duplicate checking is enabled, it looks for an existing record in the dataset that has **all** of the properties of the dragged record, and considers that a duplicate.

For [DragDataAction](../reference.md#type-dragdataaction):"copy" where the target DataSource is related to the source DataSource by foreignKey, a duplicate means that the target list, as filtered by the current criteria, already has a record whose value for the foreignKey field matches the primaryKey of the record being transferred.

For example, consider dragging "employees" to "teams", where "teams" has a field "teams.employeeId" which is a foreignKey pointing to "employees.id", and the target grid has search criteria causing it to show all the members of one team. A duplicate - adding an employee to the same team twice - is when the target grid's dataset contains an record with "employeeId" matching the "id" field of the dropped employee.

**Flags**: IR

---
## Attr: DataBoundComponent.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [DataBoundComponent.initialCriteria](#attr-databoundcomponentinitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_1.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [DataBoundComponent.initialCriteria](#attr-databoundcomponentinitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_1.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata)

**Flags**: IR

---
## Attr: DataBoundComponent.removeOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) this component should use when performing remove operations.

### Groups

- operations

**Flags**: IRW

---
## Attr: DataBoundComponent.editFormulaFieldText

### Description
Text for a menu item allowing users to edit a formula field

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.removeSummaryFieldText

### Description
Text for a menu item allowing users to remove a summary field

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.showHiddenFields

### Description
Whether to show fields marked `hidden:true` when a DataBoundComponent is given a DataSource but no `component.fields`.

The `hidden` property is used on DataSource fields to mark fields that are never of meaning to an end user.

### Groups

- databinding

**Flags**: IRW

---
## Attr: DataBoundComponent.exportIncludeSummaries

### Description
If Summary rows exist for this component, whether to include them when exporting client data.

**Flags**: IRW

---
## Attr: DataBoundComponent.hiliteIconSize

### Description
Default width and height of [hilite icons](#attr-databoundcomponenthiliteicons) for this component. Can be overridden at the component level via explicit [hiliteIconWidth](#attr-databoundcomponenthiliteiconwidth) and [hiliteIconHeight](#attr-databoundcomponenthiliteiconheight), or at the field level via [hiliteIconSize](ListGridField.md#attr-listgridfieldhiliteiconsize), [hiliteIconWidth](ListGridField.md#attr-listgridfieldhiliteiconwidth) and [hiliteIconHeight](ListGridField.md#attr-listgridfieldhiliteiconheight)

### Groups

- hiliting

### See Also

- [DataBoundComponent.hiliteIconWidth](#attr-databoundcomponenthiliteiconwidth)
- [DataBoundComponent.hiliteIconHeight](#attr-databoundcomponenthiliteiconheight)
- [ListGridField.hiliteIconSize](ListGridField.md#attr-listgridfieldhiliteiconsize)

**Flags**: IRW

---
## Attr: DataBoundComponent.progressiveLoading

### Description
Indicates whether or not this component will load its data [progressively](DataSource.md#attr-datasourceprogressiveloading).

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading)
- [ResultSet.progressiveLoading](ResultSet.md#attr-resultsetprogressiveloading)

**Flags**: IRW

---
## Attr: DataBoundComponent.deepCloneOnEdit

### Description
Before we start editing values in this DataBoundComponent, should we perform a deep clone of the underlying values. See [DataSource.deepCloneOnEdit](DataSource.md#attr-datasourcedeepcloneonedit) for details of what this means.

If this value is not explicitly set, it defaults to the value of [DataSource.deepCloneOnEdit](DataSource.md#attr-datasourcedeepcloneonedit). This value can be overridden per-field with [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit).

Like the other `deepCloneOnEdit` settings, this flag only has an effect if you are editing a values object that contains nested objects or arrays, using [dataPath](Canvas.md#attr-canvasdatapath)s.

### See Also

- [Canvas.dataPath](Canvas.md#attr-canvasdatapath)
- [FormItem.dataPath](FormItem.md#attr-formitemdatapath)
- [DataSourceField.deepCloneOnEdit](DataSourceField.md#attr-datasourcefielddeepcloneonedit)
- [DataSource.deepCloneOnEdit](DataSource.md#attr-datasourcedeepcloneonedit)

**Flags**: IRWA

---
## Attr: DataBoundComponent.addOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) this component should use when performing add operations.

### Groups

- operations

**Flags**: IRW

---
## Attr: DataBoundComponent.hiliteProperty

### Description
Marker that can be set on a record to flag that record as hilited. Should be set to a value that matches [Hilite.id](Hilite.md#attr-hiliteid) for a hilite defined on this component.

**Flags**: IRW

---
## Attr: DataBoundComponent.fetchOperation

### Description
[operationId](DSRequest.md#attr-dsrequestoperationid) this component should use when performing fetch operations, and export operations where [exportOperation](#attr-databoundcomponentexportoperation) is not set

### Groups

- operations

**Flags**: IRW

---
## Attr: DataBoundComponent.showComplexFields

### Description
Whether to show fields of non-atomic types when a DataBoundComponent is given a DataSource but no `component.fields`.

If true, the component will show fields that declare a complex type, for example, a field 'shippingAddress' that declares type 'Address', where 'Address' is the ID of a DataSource that declares the fields of a shipping address (city, street name, etc).

Such fields may need custom formatters or editors in order to create a usable interface, for example, an Address field in a ListGrid might use a custom formatter to combine the relevant fields of an address into one column, and might use a pop-up dialog for editing.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: DataBoundComponent.missingSummaryFieldValue

### Description
If a summary format string contains an invalid field reference, replace the reference with the missingSummaryFieldValue. The default value is "-".

### Groups

- summaryFields

**Flags**: IRW

---
## Attr: DataBoundComponent.hiliteIconPosition

### Description
When [hiliteIcons](#attr-databoundcomponenthiliteicons) are present, where the hilite icon will be placed relative to the field value. See [HiliteIconPosition](../reference.md#type-hiliteiconposition). Can be overridden at the field level.

### Groups

- hiliting

**Flags**: IR

---
## Attr: DataBoundComponent.dragRecategorize

### Description
Flag controlling when to recategorize records being dropped on a databound component from another databound component.

**Flags**: IRW

---
## Attr: DataBoundComponent.includeHilitesInSummaryFields

### Description
When assembling a value for a [summary field](#attr-databoundcomponentcanaddsummaryfields), if a referenced field is hilited, should the hilite HTML be included in the summary field value?

To control hilites showing in group summaries, see [showHilitesInGroupSummary](ListGrid_1.md#attr-listgridshowhilitesingroupsummary).

### See Also

- [DataBoundComponent.shouldIncludeHiliteInSummaryField](#method-databoundcomponentshouldincludehiliteinsummaryfield)

**Flags**: IRWA

---
## Attr: DataBoundComponent.dataFetchDelay

### Description
Delay in milliseconds before fetching data.

This setting only applies to the [ResultSet](ResultSet.md#class-resultset) automatically created by calling [fetchData()](ListGrid_1.md#method-listgridfetchdata). If a pre-existing ResultSet is passed to setData() instead, it's existing setting for [ResultSet.fetchDelay](ResultSet.md#attr-resultsetfetchdelay) applies.

### Groups

- databinding

### See Also

- [ResultSet.fetchDelay](ResultSet.md#attr-resultsetfetchdelay)

**Flags**: IRWA

---
## Attr: DataBoundComponent.showDetailFields

### Description
Whether to show fields marked `detail:true` when a DataBoundComponent is given a DataSource but no `component.fields`.

The `detail` property is used on DataSource fields to mark fields that shouldn't appear by default in a view that tries to show many records in a small space.

### Groups

- databinding

**Flags**: IRW

---
## Attr: DataBoundComponent.canEditFieldAttribute

### Description
If this component is bound to a dataSource, this attribute may be specified to customize what fields from the dataSource may be edited by default. For example the [SearchForm](SearchForm.md#class-searchform) class has this attribute set to `"canFilter"` which allows search forms to edit dataSource fields marked as `canEdit:false` (but not those marked as `canFilter:false`).

Note that if `canEdit` is explicitly specified on a field in the [DataBoundComponent.fields](#attr-databoundcomponentfields) array, that property will be respected in preference to the canEditAttribute value. (See [FormItem.canEdit](FormItem.md#attr-formitemcanedit), [ListGridField.canEdit](ListGridField.md#attr-listgridfieldcanedit)). Also note that individual dataBoundComponents may have additional logic around whether a field can be edited - for example [ListGrid.canEditCell](ListGrid_2.md#method-listgridcaneditcell) may be overridden.

**Flags**: IRA

---
## Attr: DataBoundComponent.hiliteIconRightPadding

### Description
How much padding should there be on the right of [hilite icons](#attr-databoundcomponenthiliteicons) by default? Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DataBoundComponent.canAddSummaryFields

### Description
Adds an item to the header context menu allowing users to launch a dialog to define a new text field that can contain both user-defined text and the formatted values present in other fields, using the [SummaryBuilder](SummaryBuilder.md#class-summarybuilder).

User-added summary fields can be persisted via [ListGrid.getFieldState](ListGrid_2.md#method-listgridgetfieldstate) and [ListGrid.setFieldState](ListGrid_2.md#method-listgridsetfieldstate).

### Groups

- summaryFields

**Flags**: IRW

---
## Attr: DataBoundComponent.hiliteIconLeftPadding

### Description
How much padding should there be on the left of [hilite icons](#attr-databoundcomponenthiliteicons) by default? Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DataBoundComponent.exportAll

### Description
Setting exportAll to true prevents the component from passing it's list of fields to the export call. The result is the export of all visible fields from [DataSource.fields](DataSource.md#attr-datasourcefields).

If exportAll is false, an export operation will first consider [DataBoundComponent.exportFields](#attr-databoundcomponentexportfields), if it's set, and fall back on all visible fields from [DataSource.fields](DataSource.md#attr-datasourcefields) otherwise.

**Flags**: IRW

---
## Attr: DataBoundComponent.defaultGeneratedHoverAsyncErrorContents

### Description
—

### Groups

- pseudoFieldGeneration
- i18nMessages

**Flags**: IRW

---
## Attr: DataBoundComponent.hiliteIconWidth

### Description
Width for hilite icons for this component. Overrides [hiliteIconSize](#attr-databoundcomponenthiliteiconsize). Can be overridden at the field level.

### Groups

- hiliting

**Flags**: IRW

---
## Attr: DataBoundComponent.addDropValues

### Description
Indicates whether to add "drop values" to items dropped on this component, if both the source and target widgets are databound, either to the same DataSource or to different DataSources that are related via a foreign key. "Drop values" are properties of the dropped item that you wish to change (and persist) as a result of the item being dropped on this grid.

If this value is true and this component is databound, [DataBoundComponent.getDropValues](#method-databoundcomponentgetdropvalues) will be called for every databound item dropped on this grid, and an update performed on the item

### Groups

- dragging

**Flags**: IRW

---
## Attr: DataBoundComponent.savedSearchId

### Description
Optional identifier for saved searches that should be applied to this component.

By default [SavedSearches](SavedSearches.md#class-savedsearches) are associated with a component via a [minimal locator](AutoTest.md#classmethod-autotestgetminimallocator). This property allows developers to override this behavior and explicitly associate a component with a set of saved searches. This can provide a couple of benefits:  
Firstly this ensures that saved searches will be unambiguously associated with the particular component even if the page changes such that a stored minimal locator would no longer applied to the component, without requiring an explicit [Canvas.ID](Canvas.md#attr-canvasid).  
Secondly this allows the same set of saved searches to be applied to more than one component on a page. This may be valueable for cases where the same information from the same dataSource is presented to users in multiple places.

**Flags**: IRWA

---
## Method: DataBoundComponent.getSort

### Description
Return the [SortSpecifier](../reference.md#object-sortspecifier)s representing the current sort configuration of this component.

### Returns

`[Array of SortSpecifier](#type-array-of-sortspecifier)` — sortSpecifiersThe current sort specification for this component

---
## Method: DataBoundComponent.findAll

### Description
This API is equivalent to [List.findAll](List.md#method-listfindall) but searches for a matching record among already-loaded data only. Use [fetchData](ListGrid_1.md#method-listgridfetchdata) to load data from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| advancedCriteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | AdvancedCriteria to use with |

### Returns

`[Array](#type-array)` — all matching Objects or null if none found

---
## Method: DataBoundComponent.getFieldNum

### Description
Find the index of a currently visible field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [FieldName](../reference.md#type-fieldname)|[Field](#type-field) | false | — | field name or field |

### Returns

`[int](../reference.md#type-int)` — index of field within currently visible fields, or -1 if not found.

---
## Method: DataBoundComponent.editHilites

### Description
Shows a [HiliteEditor](HiliteEditor.md#class-hiliteeditor) interface allowing end-users to edit the data-hilites currently in use by this DataBoundComponent.

### Groups

- hiliting

---
## Method: DataBoundComponent.getSelectionLength

### Description
Returns the number of selected records.

### Returns

`[int](../reference.md#type-int)` — number of selected records

### Groups

- selection

---
## Method: DataBoundComponent.addSummaryField

### Description
Convenience method to display a [SummaryBuilder](SummaryBuilder.md#class-summarybuilder) to create a new Summary Field. This is equivalent to calling [editSummaryField()](#method-databoundcomponenteditsummaryfield) with no parameter.

### Groups

- summaryFields

---
## Method: DataBoundComponent.transferSelectedData

### Description
Simulates a drag / drop type transfer of the selected records in some other component to this component, without requiring any user interaction. This method acts on the dropped records exactly as if they had been dropped in an actual drag / drop interaction, including any special databound behavior invoked by calling [getDropValues](#method-databoundcomponentgetdropvalues) for each dropped record.

To transfer **all** data in, for example, a [ListGrid](ListGrid_1.md#class-listgrid), call [ListGrid.selectAllRecords](ListGrid_2.md#method-listgridselectallrecords) first.

Note that drag/drop type transfers of records between components are asynchronous operations: SmartClient may need to perform server turnarounds to establish whether dropped records already exist in the target component. Therefore, it is possible to issue a call to transferSelectedData() and/or the [drop()](ListGrid_2.md#method-listgriddrop) method of a databound component whilst a transfer is still active. When this happens, SmartClient adds the second and subsequent transfer requests to a queue and runs them one after the other. If you want to be notified when a transfer process has actually completed, either provide a callback to this method or implement [DataBoundComponent.dropComplete](#method-databoundcomponentdropcomplete).

See the [dragging](../reference.md#kb-topic-dragging) documentation for an overview of list grid drag/drop data transfer.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| source | [DataBoundComponent](#type-databoundcomponent) | false | — | source component from which the records will be transferred |
| index | [Integer](../reference_2.md#type-integer) | true | — | target index (drop position) of the rows within this grid. |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback to be fired when the transfer process has completed. The callback will be passed a single parameter "records", the list of records actually transferred to this component. |

### Groups

- dragdrop

---
## Method: DataBoundComponent.selectAllRecords

### Description
Select all records

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.setFieldState

### Description
Apply a field state derived from [DataBoundComponent.getFieldState](#method-databoundcomponentgetfieldstate) to this component. This will manage fields' visibility and order if they have been modified, for example via a [FieldPickerWindow](FieldPickerWindow.md#class-fieldpickerwindow).

The optional `isSparse` parameter may be passed to indicate whether the fieldState object is "sparse" - whether it includes explicit state information for hidden fields. In this case any fields defined on the component not explicitly included in the fieldState object will be hidden.  
If `isSparse` is not explicitly passed as a parameter, sparseness will be assumed if [DataBoundComponent.sparseFieldState](#attr-databoundcomponentsparsefieldstate) is true.

Note that this method may be overridden by specific component types to handle more than just field visibility and order. For example ListGrids support extensive customization of fields' appearance and behavior by users and consequently tracks many variables in the field state (see the [documentation for that class](ListGrid_2.md#method-listgridgetfieldstate) for specifics).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldState | [FieldState](../reference_2.md#type-fieldstate) | false | — | field state to apply |
| isSparse | [Boolean](#type-boolean) | true | — | If true, the fieldState passed in is assumed to be "sparse". Any fields defined on this component without explicit field state values will be hidden. |

---
## Method: DataBoundComponent.getTitleFieldValue

### Description
Get the value of the titleField for the passed record

Override in subclasses

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record whose index is to be retrieved |

### Returns

`[String](#type-string)` — valuethe value of the titleField for the passed record

---
## Method: DataBoundComponent.deselectAllRecords

### Description
Deselect all records

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.getHiliteState

### Description
For components that support hiliting, gets the current hilites encoded as a String, for saving.

### Returns

`[String](#type-string)` — hilites state encoded as a String

### Groups

- viewState

---
## Method: DataBoundComponent.getTitleField

### Description
Method to return the fieldName which represents the "title" for records in this Component.  
If this.titleField is explicitly specified it will always be used. Otherwise, default implementation will check [DataSource.titleField](DataSource.md#attr-datasourcetitlefield) for databound compounds.  
For non databound components returns the first defined field name of `"title"`, `"name"`, or `"id"` where the field is visible. If we don't find any field-names that match these titles, the first field in the component will be used instead.

### Returns

`[String](#type-string)` — fieldName for title field for this component.

---
## Method: DataBoundComponent.shouldIncludeHiliteInSummaryField

### Description
When assembling a value for a [summary field](#attr-databoundcomponentcanaddsummaryfields), if a referenced field is hilited, should the hilite HTML be included in the summary field value?

Example use case: Consider a grid containing a numeric field, and a summary field which contains some string value, plus the contents of the numeric field. If a hilite is defined for the grid which turns the numeric field text red when the value is negative, this property will govern whether the number will also be rendered in red within the summary field cells. Any other text in the summary field cells would not be effected by this hilite.

Default implementation returns [includeHilitesInSummaryFields](#attr-databoundcomponentincludehilitesinsummaryfields).

To control hilites showing in group summaries, see [showHilitesInGroupSummary](ListGrid_1.md#attr-listgridshowhilitesingroupsummary).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| summaryFieldName | [String](#type-string) | false | — | name of the summary field |
| usedFieldName | [String](#type-string) | false | — | name of the field referenced by this summary |

### Returns

`[boolean](../reference.md#type-boolean)` — Return true to include hilites from the used field in the generated summary field value.

---
## Method: DataBoundComponent.shouldIncludeTitleInFieldState

### Description
Should the title be included in field state for the field passed in. Default implementation will return true if [canEditTitles](ListGrid_1.md#attr-listgridcanedittitles) is true

This method may be overridden to customize this behavior. For example the following implementation would include titles for fields where an explicitly component-level field-title was set that differed from the [DataSourceField.title](DataSourceField.md#attr-datasourcefieldtitle) for the underlying dataSource field:

```
 shouldIncludeTitleInFieldState : function (field, sparse) {
     var dsField = this.getDataSource().getField(field.name);
     if (dsField != null && dsField.title != field.title) return true;
     return false;
 }
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field to provide field state for |
| sparse | [boolean](../reference.md#type-boolean) | false | — | true if [sparse field state](#method-databoundcomponentgetfieldstate) was requested. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if title should be included in field state

**Flags**: A

---
## Method: DataBoundComponent.findIndex

### Description
This API is equivalent to [List.findIndex](List.md#method-listfindindex) but searches for a matching record among already-loaded data only. Use [fetchData](ListGrid_1.md#method-listgridfetchdata) to load data from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| advancedCriteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | AdvancedCriteria to use with |

### Returns

`[int](../reference.md#type-int)` — index of the first matching Object or -1 if not found

---
## Method: DataBoundComponent.willFetchData

### Description
Compares the specified criteria with the current criteria applied to this component's data object and determines whether the new criteria could be satisfied from the currently cached set of data, or if a new filter/fetch operation will be required.

This is equivalent to calling `this.data.willFetchData(...)`. Always returns true if this component is not showing a set of data from the dataSource.

Note that to predict correctly the decision that will be made by filter/fetch, you'll need to pass the same [TextMatchStyle](../reference.md#type-textmatchstyle) that will be used by the future filter/fetch. Fetching manually (e.g. [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata)) will by default use "exact" while filtering (e.g. [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata)) will by default use "substring". If the component is configured for autofetch (i.e. [ListGrid.autoFetchData](ListGrid_1.md#attr-listgridautofetchdata): true), that will use [ListGrid.autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle), which defaults to "substring". If nothing/null is passed for the style, this method assumes you want the style from the last filter/fetch.

To determine what [TextMatchStyle](../reference.md#type-textmatchstyle) is being used, check the RPC Tab of the [SmartClient Developer Console](../kb_topics/debugging.md#kb-topic-debugging) and check the relevant [DSRequest](../reference.md#object-dsrequest).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | new criteria to test. |
| textMatchStyle | [TextMatchStyle](../reference.md#type-textmatchstyle) | true | — | New text match style. If not passed assumes textMatchStyle will not be modified. |

### Returns

`[Boolean](#type-boolean)` — true if server fetch would be required to satisfy new criteria.

### Groups

- dataBoundComponentMethods

---
## Method: DataBoundComponent.setDragTracker

### Description
Sets the custom tracker HTML to display next to the mouse when the user initiates a drag operation on this component. Default implementation will examine [ListGrid.dragTrackerMode](ListGrid_1.md#attr-listgriddragtrackermode) and set the custom drag tracker to display the appropriate HTML based on the selected record.  
To display custom drag tracker HTML, this method may be overridden - call [EventHandler.setDragTracker](EventHandler.md#classmethod-eventhandlersetdragtracker) to actually update the drag tracker HTML.

### Returns

`[boolean](../reference.md#type-boolean)` — returns false by default to suppress 'setDragTracker' on any ancestors of this component.

### Groups

- dragTracker

---
## Method: DataBoundComponent.selectRecords

### Description
Select/deselect a list of [Record](../reference.md#object-record)s passed in explicitly, or by index.

Note that developers may wish to use [DataBoundComponent.selectRange](#method-databoundcomponentselectrange) to select a single contiguous range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record)|[number](#type-number) | false | — | records (or row numbers) to select |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.getRecordHiliteCSSText

### Description
Return all CSS style declarations associated with the hilites of a record's field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | — |
| cssText | [String](#type-string) | false | — | if set, returned CSS will be appended to this text |
| field | [DBCField](#type-dbcfield) | false | — | field object identifying whose CSS is to be returned |

### Returns

`[String](#type-string)` — valueCSS style declarations for this record and field

---
## Method: DataBoundComponent.enableHilite

### Description
Enable / disable a [hilite](#attr-databoundcomponenthilites)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hiliteID | [String](#type-string) | false | — | ID of hilite to enable |
| enable | [boolean](../reference.md#type-boolean) | true | — | new enabled state to apply - if null, defaults to true |

### Groups

- hiliting

---
## Method: DataBoundComponent.fieldIsEditable

### Description
Can the field be edited? This base method always returns false, but it's overridden by subclasses such as [DynamicForm](DynamicForm.md#class-dynamicform) and [ListGrid](ListGrid_1.md#class-listgrid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [Object](../reference.md#type-object)|[number](#type-number)|[String](#type-string) | false | — | field object or identifier |

### Returns

`[boolean](../reference.md#type-boolean)` — whether field can be edited

### Groups

- editing

### See Also

- [ListGrid.fieldIsEditable](ListGrid_2.md#method-listgridfieldiseditable)
- [DynamicForm.fieldIsEditable](DynamicForm.md#method-dynamicformfieldiseditable)

---
## Method: DataBoundComponent.dropComplete

### Description
This method is invoked whenever a drop operation or [DataBoundComponent.transferSelectedData](#method-databoundcomponenttransferselecteddata) targeting this component completes. A drop is considered to be complete when all the client- side transfer operations have finished. This includes any server turnarounds SmartClient needs to make to check for duplicate records in the target component; it specifically does not include any add or update operations sent to the server for databound components. If you want to be notified when the entire drag operation - including server updates and cache synchronization - has completed, override [dragComplete](#method-databoundcomponentdragcomplete) on the source component.

There is no default implementation of this method; you are intended to override it if you are interested in being notified when drop operations complete.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transferredRecords | [List of Records](#type-list-of-records) | false | — | The list of records actually transferred to this component (note that this is not necessarily the same thing as the list of records dragged out of the source component because it doesn't include records that were excluded because of collisions with existing records) |

### Groups

- dragging

### See Also

- [DataBoundComponent.dragComplete](#method-databoundcomponentdragcomplete)

---
## Method: DataBoundComponent.deselectRange

### Description
Deselect a contiguous range of records by index.

This is a synonym for `selectRange(startRow, endRow, false);`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../reference.md#type-int) | false | — | start of selection range |
| endRow | [int](../reference.md#type-int) | false | — | end of selection range (non-inclusive) |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.find

### Description
This API is equivalent to [List.find](List.md#method-listfind) but searches for a matching record among already-loaded data only. Use [fetchData](ListGrid_1.md#method-listgridfetchdata) to load data from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| advancedCriteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | AdvancedCriteria to use with |

### Returns

`[Object](../reference.md#type-object)` — first matching object or null if not found

---
## Method: DataBoundComponent.disableHiliting

### Description
Disable all hilites.

### Groups

- hiliting

---
## Method: DataBoundComponent.exportData

### Description
Sends the current filter criteria and sort direction to the server, then exports data in the requested [exportFormat](DSRequest.md#attr-dsrequestexportas).

A variety of DSRequest settings, such as [exportAs](DSRequest.md#attr-dsrequestexportas) and [DSRequest.exportFilename](DSRequest.md#attr-dsrequestexportfilename), affect the exporting process: see [exportResults](DSRequest.md#attr-dsrequestexportresults) for further detail.

Note that data exported via this method skips client-side fields defined only in the component, excludes any client-side formatting and relies on both the SmartClient server and server-side DataSources. To export client-data including client-only fields and with client-side formatting applied, see [exportClientData](ListGrid_1.md#method-listgridexportclientdata), which still requires the SmartClient server but does not rely on server-side DataSource definitions (.ds.xml files).

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
## Method: DataBoundComponent.userAddedField

### Description
Notification method fired when a user-generated field is added to this component via [DataBoundComponent.editFormulaField](#method-databoundcomponenteditformulafield) or [DataBoundComponent.editSummaryField](#method-databoundcomponenteditsummaryfield).

Returning false from this method will prevent the field being added at all. Note that this also provides an opportunity to modify the generated field object - any changes made to the field parameter will show up when the field is displayed in the ListGrid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | User generated summary or formula field |

### Returns

`[boolean](../reference.md#type-boolean)` — Return false to cancel the addition of the field

### Groups

- formulaFields
- summaryFields

---
## Method: DataBoundComponent.getImplicitCriteria

### Description
Returns a copy of the [DataBoundComponent.implicitCriteria](#attr-databoundcomponentimplicitcriteria) currently applied to this component.

---
## Method: DataBoundComponent.deselectRecord

### Description
Deselect a [Record](../reference.md#object-record) passed in explicitly, or by index.

Synonym for `selectRecord(record, false)`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record)|[number](#type-number) | false | — | record (or row number) to deselect |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.editFields

### Description
Shows a [FieldPicker](FieldPicker.md#class-fieldpicker) interface allowing end-users to edit the fields currently shown by this DataBoundComponent.

---
## Method: DataBoundComponent.setHiliteState

### Description
For components that support hiliting, sets the current hilites based on a hiliteState String previously returned from [DataBoundComponent.getHiliteState](#method-databoundcomponentgethilitestate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hiliteState | [String](#type-string) | false | — | hilites state encoded as a String |

### Groups

- viewState

---
## Method: DataBoundComponent.enableHiliting

### Description
Enable all hilites.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| enable | [boolean](../reference.md#type-boolean) | true | — | new enabled state to apply - if null, defaults to true |

### Groups

- hiliting

---
## Method: DataBoundComponent.requestsArePending

### Description
Returns whether there are any pending [DSRequest](../reference.md#object-dsrequest)s initiated by this [DataBoundComponent](../reference.md#interface-databoundcomponent). May not include any requests sent by directly calling the [DataSource](DataSource.md#class-datasource) APIs (rather than the DataBoundComponent APIs).

### Returns

`[Boolean](#type-boolean)` — true if one or more requests are pending, false otherwise.

---
## Method: DataBoundComponent.getHilites

### Description
Return the set of hilite-objects currently applied to this DataBoundComponent. These can be serialized for storage and then restored to a component later via [setHilites()](#method-databoundcomponentsethilites).

### Returns

`[Array of Hilite](#type-array-of-hilite)` — Array of hilite objects

### Groups

- hiliting

---
## Method: DataBoundComponent.findByKey

### Description
Attempt to find the record in the resultSet that has a primary key value that matches the passed in parameter value. Only the locally cached data will be searched. Checks only loaded rows and will not trigger a fetch. Returns null if there is no match, data is not loaded, or there is no [dataSource](ResultSet.md#attr-resultsetdatasource).

Note, if you pass a simple value to this method, it will be matched against the first primaryKey field. For DataSources with a composite primary key (multiple primaryKey fields), pass a criteria object containing just your primaryKeys, like this: `{ firstPkField: "value", secondPkField: 25 }`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| keyValue | [Object](../reference.md#type-object) | false | — | primary key value to search for |

### Returns

`[Record](#type-record)` — the record with a matching primary key field, or null if not found

---
## Method: DataBoundComponent.addFormulaField

### Description
Convenience method to display a [FormulaBuilder](FormulaBuilder.md#class-formulabuilder) to create a new Formula Field. This is equivalent to calling [editFormulaField()](#method-databoundcomponenteditformulafield) with no parameter.

### Groups

- formulaFields

---
## Method: DataBoundComponent.getDataPathField

### Description
For a component with a specified [DataSource](DataSource.md#class-datasource), find the associated dataSource field object from a specified [dataPath](../reference_2.md#type-datapath).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataPath | [DataPath](../reference_2.md#type-datapath) | false | — | dataPath for which the field definition should be returned. |

### Returns

`[DataSourceField](#type-datasourcefield)` — the field associated with the passed datapath.

---
## Method: DataBoundComponent.transferRecords

### Description
Transfer a list of [Record](../reference.md#object-record)s from another component (does not have to be a databound component) into this component. This method is only applicable to list-type components, such as [listGrid](ListGrid_1.md#class-listgrid), [treeGrid](TreeGrid.md#class-treegrid) or [tileGrid](TileGrid.md#class-tilegrid)

This method implements the automatic drag-copy and drag-move behaviors of components like [ListGrid](ListGrid_1.md#class-listgrid), and calling it is equivalent to completing a drag and drop of the `dropRecords`.

Note that this method is asynchronous - it may need to perform server turnarounds to prevent duplicates in the target component's data. If you wish to be notified when the transfer process has completed, you can either pass the optional callback to this method or implement the [DataBoundComponent.dropComplete](#method-databoundcomponentdropcomplete) method on this component.

See also [DataBoundComponent.transferSelectedData](#method-databoundcomponenttransferselecteddata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dropRecords | [Array of Record](#type-array-of-record) | false | — | Records to transfer to this component |
| targetRecord | [Record](#type-record) | false | — | The target record (eg, of a drop interaction), for context |
| index | [Integer](../reference_2.md#type-integer) | false | — | Insert point in this component's data for the transferred records |
| sourceWidget | [Canvas](#type-canvas) | false | — | The databound or non-databound component from which the records are to be transferred. |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback to be fired when the transfer process has completed |

### Groups

- dragdrop

---
## Method: DataBoundComponent.editFormulaField

### Description
Method to display a [FormulaBuilder](FormulaBuilder.md#class-formulabuilder) to edit a formula Field. If the function is called without a parameter, a new field will be created when the formula is saved.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DBCField](#type-dbcfield) | false | — | Field to edit or null to add a new formula field |

### Groups

- formulaFields

---
## Method: DataBoundComponent.getField

### Description
Return a field by a field index or field name.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldID | [FieldName](../reference.md#type-fieldname)|[Number](#type-number) | false | — | field index or field.name |

### Returns

`[Object](../reference.md#type-object)` — Field description

---
## Method: DataBoundComponent.setHilites

### Description
Accepts an array of hilite objects and applies them to this DataBoundComponent. See also [getHilites()](#method-databoundcomponentgethilites) for a method of retrieving the hilite array for storage, including hilites manually added by the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hilites | [Array of Hilite](#type-array-of-hilite) | false | — | Array of hilite objects |

### Groups

- hiliting

---
## Method: DataBoundComponent.editSummaryField

### Description
Method to display a [SummaryBuilder](SummaryBuilder.md#class-summarybuilder) to edit a Summary Field. If the function is called without a parameter, a new field will be created when the summary is saved.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DBCField](#type-dbcfield) | false | — | Field to edit or null to add a new summary column |

### Groups

- summaryFields

---
## Method: DataBoundComponent.askForSort

### Description
Show a dialog to configure the sorting of multiple fields on this component. Calls through to [MultiSortDialog.askForSort](MultiSortDialog.md#classmethod-multisortdialogaskforsort), passing this component as the fieldSource and the current [sort-specification](#method-databoundcomponentgetsort) if there is one.

The generated multiSortDialog can be customized via [DataBoundComponent.multiSortDialogDefaults](#attr-databoundcomponentmultisortdialogdefaults), [DataBoundComponent.multiSortDialogProperties](#attr-databoundcomponentmultisortdialogproperties).

---
## Method: DataBoundComponent.deselectRecords

### Description
Deselect a list of [Record](../reference.md#object-record)s passed in explicitly, or by index.

Synonym for `selectRecords(records, false)`

Note that developers may wish to use [DataBoundComponent.deselectRange](#method-databoundcomponentdeselectrange) to select a single contiguous range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record)|[number](#type-number) | false | — | records (or row numbers) to deselect |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.selectRange

### Description
Select a contiguous range of records by index

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../reference.md#type-int) | false | — | start of selection range |
| endRow | [int](../reference.md#type-int) | false | — | end of selection range (non-inclusive) |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.transferDragData

### Description
During a drag-and-drop interaction, this method is called to transfer a set of records that were dropped onto some other component. This method is called after the set of records has been copied to the other component. Whether or not this component's data is modified is determined by the value of [DataBoundComponent.dragDataAction](#attr-databoundcomponentdragdataaction).

With a `dragDataAction` of "move", a databound component will issue "remove" dsRequests against its DataSource to actually remove the data, via [DataSource.removeData](DataSource.md#method-datasourceremovedata).

### Returns

`[Array](#type-array)` — Array of objects that were dragged out of this ListGrid.

### See Also

- [DataBoundComponent.getDragData](#method-databoundcomponentgetdragdata)
- [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop)

**Flags**: A

---
## Method: DataBoundComponent.selectionUpdated

### Description
Called when the selection changes. Note that this method fires exactly once for any given change to the selection unlike the [selectionChanged](ListGrid_2.md#method-listgridselectionchanged) event.

This event is fired once after selection/deselection has completed. The result is one event per mouse-down event. For a drag selection there will be two events fired: one when the first record is selected and one when the range is completed.

This event is also fired when selection is updated by a direct call to one of the `DataBoundComponent` select/deselect methods. Calls on the [Selection](Selection.md#class-selection) object **do not** trigger this event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Object](../reference.md#type-object) | false | — | first selected record in the selection, if any, which may or may not be the first record in sort order if the `DataBoundComponent` is sorted. This parameter is typically used when only one record can be selected at a time. |
| recordList | [Array of Object](#type-array-of-object) | false | — | List of records that are now selected |

### Groups

- selection

---
## Method: DataBoundComponent.setDataSource

### Description
Bind to a new DataSource.

Like passing the "dataSource" property on creation, binding to a DataSource means that the component will use the DataSource to provide default data for its fields.

When binding to a new DataSource, if the component has any existing "fields" or has a dataset, these will be discarded by default, since it is assumed the new DataSource may represent a completely unrelated set of objects. If the old "fields" are still relevant, pass them to setDataSource().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataSource | [GlobalId](../reference.md#type-globalid)|[DataSource](#type-datasource) | false | — | DataSource to bind to |
| fields | [Array of DataSourceField](#type-array-of-datasourcefield) | true | — | optional array of fields to use |

---
## Method: DataBoundComponent.getViewState

### Description
Returns a snapshot of the current view state of this Component.  
The default implementation at the DataBoundComponent level will track [fieldState](#method-databoundcomponentgetfieldstate) only. See documentation on specific component classes for whether additional configuration is included in the viewState.

The viewState subsystem is typically used to store and reapply user preferences, for example after fields are shown or hidden using a [FieldPickerWindow](FieldPickerWindow.md#class-fieldpickerwindow).  
The viewState returned by this method may be stored over page-reloads and then applied to a component at runtime via [DataBoundComponent.setViewState](#method-databoundcomponentsetviewstate).

### Returns

`[ViewState](../reference.md#type-viewstate)` — Current view state of the component

---
## Method: DataBoundComponent.setViewState

### Description
Reset this component's view state to match the [ViewState](../reference.md#type-viewstate) object passed in.  
Used to restore previous state retrieved from the component by a call to [DataBoundComponent.getViewState](#method-databoundcomponentgetviewstate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewState | [ViewState](../reference.md#type-viewstate) | false | — | Object describing the desired view state for the component |

### Groups

- viewState

### See Also

- [DataBoundComponent.getViewState](#method-databoundcomponentgetviewstate)

---
## Method: DataBoundComponent.setSort

### Description
Sort this component by a list of [SortSpecifier](../reference.md#object-sortspecifier)s. If the component's data is not a [ResultSet](ResultSet.md#class-resultset), only the first specifier is applied.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifiers | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | List of [SortSpecifier](../reference.md#object-sortspecifier) objects, one per sort-field and direction |

---
## Method: DataBoundComponent.getSummaryFieldValue

### Description
Get the computed value of a [summary field](#attr-databoundcomponentcanaddsummaryfields).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DBCField](#type-dbcfield) | false | — | field that has a summary format |
| record | [Record](#type-record) | false | — | record to use to compute formula value |

### Returns

`[String](#type-string)` — formula result

---
## Method: DataBoundComponent.isOffline

### Description
Returns true if the component's current data model is marked as offline. This does not necessarily mean that the component has no data; it may have data that was supplied from the [offline cache](Offline.md#class-offline).

### Returns

`[boolean](../reference.md#type-boolean)` — Offline if true

### Groups

- offlineGroup

---
## Method: DataBoundComponent.getDragData

### Description
During a drag-and-drop interaction, this method returns the set of records being dragged out of the component. In the default implementation, this is the list of currently selected records.

This method is consulted by [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop).

NOTE: If this component is a [multi-linked](Tree.md#method-treeismultilinktree) `TreeGrid`, this method returns a list of [NodeLocator](../reference_2.md#object-nodelocator)s rather than a list of records. Each `nodeLocator` contains a pointer to the associated record in its `node` property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| source | [DataBoundComponent](#type-databoundcomponent) | false | — | source component from which the records will be transferred |

### Returns

`[Array of Record](#type-array-of-record)` — Array of [Record](../reference.md#object-record)s that are currently selected.

### Groups

- dragging
- data

**Flags**: A

---
## Method: DataBoundComponent.anySelected

### Description
Whether at least one item is selected

### Returns

`[boolean](../reference.md#type-boolean)` — true == at least one item is selected false == nothing at all is selected

### Groups

- selection

---
## Method: DataBoundComponent.disableHilite

### Description
Disable a hilite

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hiliteID | [String](#type-string) | false | — | ID of hilite to disable |

### Groups

- hiliting

---
## Method: DataBoundComponent.selectRecord

### Description
Select/deselect a [Record](../reference.md#object-record) passed in explicitly, or by index.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record)|[number](#type-number) | false | — | record (or row number) to select |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.setImplicitCriteria

### Description
Setter for the [DataBoundComponent.implicitCriteria](#attr-databoundcomponentimplicitcriteria) attribute, which can be called directly at runtime to update the `implicitCriteria` on this component.

If this component has fetched data before, a fetch will be issued if the new implicit-criteria is less restrictive when re-combined with any additional criteria applied to the component via other means.

If data has never been fetched for this component, this method will not issue an initial fetch unless the `initialFetch` parameter is passed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | non user-editable criteria to apply to this component |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to fire on successful fetch - will not fire if `willFetchData` is false or if an initial fetch is required but `initialFetch` was not passed |
| initialFetch | [Boolean](#type-boolean) | true | — | flag to allow initial fetch if this grid has never fetched data before - default behavior is not to perform an initial fetch |

### Returns

`[Boolean](#type-boolean)` — true if this call resulted in a fetch

---
## Method: DataBoundComponent.dragComplete

### Description
This method is invoked on the source component whenever a drag operation or [DataBoundComponent.transferSelectedData](#method-databoundcomponenttransferselecteddata) completes. This method is called when the entire chain of operations - including, for databound components, server-side updates and subsequent integration of the changes into the client-side cache - has completed.

There is no default implementation of this method; you are intended to override it if you are interested in being notified when drag operations complete.

### Groups

- dragging

### See Also

- [DataBoundComponent.dropComplete](#method-databoundcomponentdropcomplete)

---
## Method: DataBoundComponent.getRecordIndex

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
## Method: DataBoundComponent.getFieldAlignments

### Description
Returns an array of [field alignments](../reference.md#type-alignment) for this grid

### Returns

`[Array of Alignment](#type-array-of-alignment)` — —

---
## Method: DataBoundComponent.getFormulaFieldValue

### Description
Get the computed value of a [formula field](#attr-databoundcomponentcanaddformulafields).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [DBCField](#type-dbcfield) | false | — | field that has a formula |
| record | [Record](#type-record) | false | — | record to use to compute formula value |

### Returns

`[Double](../reference.md#type-double)|[String](#type-string)` — formula result if a valid number or [DataBoundComponent.badFormulaResultValue](#attr-databoundcomponentbadformularesultvalue) if invalid

---
## Method: DataBoundComponent.getDropValues

### Description
Returns the "drop values" to apply to a record dropped on this component prior to update. Only applicable to databound components - see [DataBoundComponent.dropValues](#attr-databoundcomponentdropvalues) for more details. If multiple records are being dropped, this method is called for each of them in turn.

The default implementation of this method returns the following:

*   Nothing, if [DataBoundComponent.addDropValues](#attr-databoundcomponentadddropvalues) is false
*   dropValues, if that property is set. If the component's criteria object is applicable (as explained in the next item), it is merged into dropValues, with properties in dropValues taking precedence.
*   The component's criteria object, if the most recent textMatchStyle for the component was "exact" and it is simple criteria (ie, not an AdvancedCriteria object)
*   Otherwise nothing

You can override this method if you need more complex setting of drop values than can be provided by simply supplying a dropValues object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | record being dropped |
| sourceDS | [DataSource](#type-datasource) | false | — | dataSource the record being dropped is bound to |
| targetRecord | [Record](#type-record) | false | — | record being dropped on |
| index | [int](../reference.md#type-int) | false | — | index of record being dropped on |
| sourceWidget | [Canvas](#type-canvas) | false | — | widget where dragging began |

### Returns

`[Object](../reference.md#type-object)` — dropValues, as described above.

---
## Method: DataBoundComponent.findNextIndex

### Description
This API is equivalent to [List.findNextIndex](List.md#method-listfindnextindex) but searches for a matching record among already-loaded data only. Use [fetchData](ListGrid_1.md#method-listgridfetchdata) to load data from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startIndex | [int](../reference.md#type-int) | false | — | first index to consider |
| advancedCriteria | [AdvancedCriteria](#type-advancedcriteria) | false | — | AdvancedCriteria to use with |
| endIndex | [int](../reference.md#type-int) | true | — | last index to consider |

### Returns

`[int](../reference.md#type-int)` — index of the first matching Object or -1 if not found

---
## Method: DataBoundComponent.selectSingleRecord

### Description
Select a single [Record](../reference.md#object-record) passed in explicitly, or by index, and deselect everything else. When programmatic selection of records is a requirement and [selectionType()](ListGrid_1.md#attr-listgridselectiontype) is "single", use this method rather than [selectRecord()](#method-databoundcomponentselectrecord) to enforce mutually-exclusive record-selection.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record)|[number](#type-number) | false | — | record (or row number) to select |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: DataBoundComponent.getFieldState

### Description
Retrieve a snapshot of current field state for this component. This includes an object for each field, indicating its name, visibility and order, allowing you to track user preferences if they have been modified, for example via a [FieldPickerWindow](FieldPickerWindow.md#class-fieldpickerwindow).

The optional `sparse` parameter governs whether the returned field state should omit state information for hidden fields. If this parameter is not passed explicitly, field state will be sparse if [DataBoundComponent.sparseFieldState](#attr-databoundcomponentsparsefieldstate) is true.  
When applying sparse field state to a component via [DataBoundComponent.setFieldState](#method-databoundcomponentsetfieldstate), any explicitly defined fields on the component that were not captured in the stored state object will be hidden.

Note that this method may be overridden by specific component types to handle more than just field visibility and order. For example ListGrids support extensive customization of fields' appearance and behavior by users and consequently tracks many variables in the field state (see the [documentation for that class](ListGrid_2.md#method-listgridgetfieldstate) for specifics).

Note that, as a shorthand, for fields that are visible but have no other state-variables, only the field-name is included in the field-state array - so this array can contain a mix of strings and objects which are interpreted automatically when the state is reapplied.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sparse | [Boolean](#type-boolean) | true | — | If true, field state will be omitted for hidden fields. |
| return | [FieldState](../reference_2.md#type-fieldstate) | false | — | Current field state |

---
