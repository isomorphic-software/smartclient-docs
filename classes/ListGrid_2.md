# ListGrid Documentation (Part 2 of 2)

[← Back to API Index](../reference.md)

---

## Method: ListGrid.getDrawnRowHeight

### Description
Get the drawn height of a row.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | — |

### Returns

`[number](#type-number)` — height

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: ListGrid.getFormattedValue

### Description
Get the fully formatted value for a cell, including all formatting applied by custom formatters and declarative formatting settings.

This method returns the complete formatted value exactly as it would appear in the grid cell, applying all of the following in order:

*   [ListGridField.valueMap](ListGridField.md#attr-listgridfieldvaluemap) mapping
*   [ListGridField.displayField](ListGridField.md#attr-listgridfielddisplayfield) substitution
*   Custom formatters ([ListGridField.formatCellValue](ListGridField.md#method-listgridfieldformatcellvalue) and [ListGrid.formatCellValue](#method-listgridformatcellvalue))
*   [listGridField.cellValueTemplate](#listgridfieldcellvaluetemplate) evaluation
*   [ListGridField.format](ListGridField.md#attr-listgridfieldformat) application
*   Type-specific formatters
*   Final string formatting and HTML escaping

This method is useful when you want to display a grid cell's value elsewhere in your UI with the exact same formatting that appears in the grid itself.

Unlike [ListGrid.getDefaultFormattedValue](#method-listgridgetdefaultformattedvalue), this method _will_ call any custom formatter methods that have been defined on the field or grid, so it returns the complete formatted value exactly as it would appear in the grid.

For other use cases, see also:

*   [ListGrid.getDefaultFormattedValue](#method-listgridgetdefaultformattedvalue) - get formatted value without any custom formatters
*   [ListGrid.getDefaultFormattedFieldValue](ListGrid_1.md#method-listgridgetdefaultformattedfieldvalue) - get formatted value with field-level formatters only

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record containing the value to format |
| fieldName | [String](#type-string) | false | — | the name of the field to format |
| value | [Any](#type-any) | false | — | optional value to format; if not provided, the value will be extracted from the record |

### Returns

`[String](#type-string)` — the fully formatted cell value

### See Also

- [ListGrid.getDefaultFormattedValue](#method-listgridgetdefaultformattedvalue)
- [ListGrid.getDefaultFormattedFieldValue](ListGrid_1.md#method-listgridgetdefaultformattedfieldvalue)

**Flags**: A

---
## Method: ListGrid.getRowCountStatus

### Description
This method indicates whether [ListGrid.getRowCount](#method-listgridgetrowcount) reflects an accurate row-count for this listGrid. An accurate row count may not currently be available if [progressiveLoading](DataSource.md#attr-datasourceprogressiveloading) is active.

See [RowCountStatus](../reference.md#type-rowcountstatus) for further details.

### Returns

`[RowCountStatus](../reference.md#type-rowcountstatus)` — Current row-count status for this grid

### Groups

- rowRangeDisplay

---
## Method: ListGrid.cellErrorIconOut

### Description
Optional stringMethod to fire when the mouse moves off the error icon of a cell with validation errors.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard behavior (clear the standard error message hover if it is showing)

### Groups

- events

### See Also

- [ListGrid.showErrorIcons](ListGrid_1.md#attr-listgridshowerroricons)

**Flags**: A

---
## Method: ListGrid.setHeaderSpans

### Description
Update the headerSpans configuration on the grid dynamically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| headerSpans | [Array of HeaderSpan](#type-array-of-headerspan) | false | — | same configuration block as that passed to [ListGrid.headerSpans](ListGrid_1.md#attr-listgridheaderspans). |

### Groups

- headerSpan

---
## Method: ListGrid.setFieldIcon

### Description
Change the [ListGridField.icon](ListGridField.md#attr-listgridfieldicon) for a field after the grid is created

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to update |
| icon | [SCImgURL](../reference.md#type-scimgurl) | false | — | icon for the field |

---
## Method: ListGrid.setCanRemoveRecords

### Description
Updates the [ListGrid.canRemoveRecords](ListGrid_1.md#attr-listgridcanremoverecords) property for this listGrid at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canRemove | [boolean](../reference.md#type-boolean) | false | — | new canRemoveRecords value |

---
## Method: ListGrid.hilitesChanged

### Description
Notification method executed whenever the end user uses the HiliteEditor to change the set of hilites applied to this grid. This method will not be called after a purely programmatic change to the hilites made with a call to [setHilites()](DataBoundComponent.md#method-databoundcomponentsethilites). The array of currently applied hilite objects is accessible via [getHilites()](DataBoundComponent.md#method-databoundcomponentgethilites).

### Groups

- hiliting

---
## Method: ListGrid.getDataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference_2.md#object-dsrequest).

### Returns

`[DataSource](#type-datasource)` — Datasource object for this ListGrid instance.

---
## Method: ListGrid.getSummaryTitle

### Description
Return the summary title of particular field. This is the title of the field to be used in the show / hide fields context menu. Default implementation will use [ListGridField.getSummaryTitle](ListGridField.md#method-listgridfieldgetsummarytitle) or [ListGridField.summaryTitle](ListGridField.md#attr-listgridfieldsummarytitle) if specified, otherwise [ListGridField.title](ListGridField.md#attr-listgridfieldtitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field for which we're returning the title |

### Returns

`[String](#type-string)` — Field summary title.

### Groups

- i18nMessages
- display

**Flags**: A

---
## Method: ListGrid.hideDragHandles

### Description
Hides the [drag handle field](ListGrid_1.md#attr-listgriddraghandlefield), if currently shown.

### Groups

- dragHandleField

### See Also

- [ListGrid.showDragHandles](#method-listgridshowdraghandles)

---
## Method: ListGrid.headerHover

### Description
Handle a hover over a button in the header.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [number](#type-number) | false | — | field number for the header that was hovered |

### Groups

- events
- gridHeader
- hovers

### See Also

- [ListGrid.headerHoverHTML](#method-listgridheaderhoverhtml)

**Flags**: A

---
## Method: ListGrid.getHeaderContextMenuItems

### Description
If [ListGrid.showHeaderContextMenu](ListGrid_1.md#attr-listgridshowheadercontextmenu) is `true` this method returns the menu items to be displayed in the default header context menu.

This method is called at various times, including during redraws, as the mouse moves over a ListGrid header button and each time the menu is actually displayed - this allows for dynamic content depending on the current state of the grid and its fields.

Consequently, this method should not instantiate any classes, because they'll be re-created on each call, resulting in a leak - your implementation should return an array of menuItem config-blocks only, so you shouldn't instantiate actual Menu instances to apply as the [submenu](MenuItem.md#attr-menuitemsubmenu) of items - instead, set submenu to a simple array of menuItems. If your use-case necessitates that class instances are created, because specific submenus have a different Menu class, for example, you should keep a reference to them and either, if their content is dynamic, destroy and recreate them with the new items, or just return the existing instances otherwise.

The default set of menu items includes items for built-in ListGrid features like showing and hiding fields, freezing fields or grouping by them, and other functions.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [Integer](../reference_2.md#type-integer) | true | — | Index of the field the user clicked in the [fields](ListGrid_1.md#attr-listgridfields) array. **Note:** if the user right-clicked the sorter button this parameter will be `null`. |

### Returns

`[Array of MenuItem](#type-array-of-menuitem)` — —

### Groups

- gridHeader

---
## Method: ListGrid.saveAllEdits

### Description
Save a number of outstanding edits for this ListGrid. If no rows are specified, all outstanding edits will be saved.

Note that if [ListGrid.saveRequestProperties](ListGrid_1.md#attr-listgridsaverequestproperties) is specified and the grid is performing a databound save, these properties will be applied to each generated DSRequest.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rows | [Array of Number](#type-array-of-number) | true | — | optionally specify which rows to save |
| saveCallback | [Callback](../reference.md#type-callback) | true | — | If specified this callback will be fired on a successful save of the specified rows. Note that if there are no pending edits to be saved this callback will not fire - you can check for this condition using [ListGrid.hasChanges](#method-listgridhaschanges) or [ListGrid.rowHasChanges](#method-listgridrowhaschanges). Use [ListGrid.editFailed](ListGrid_1.md#method-listgrideditfailed) to find out about failures encountered during saving (on a per-row basis). |

### Returns

`[boolean](../reference.md#type-boolean)` — true if a save has been initiated (at least one row had changes, passed client-side validation, and a save has been attempted). False otherwise

### Groups

- editing

---
## Method: ListGrid.setHideOnTablet

### Description
Updates the [ListGridField.hideOnTablet](ListGridField.md#attr-listgridfieldhideontablet) attribute at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[String](#type-string) | false | — | field or field name to update |
| hideOnTablet | [Boolean](#type-boolean) | false | — | new setting for hideOnTablet property |

---
## Method: ListGrid.setSortState

### Description
Reset this grid's sort state (sort field and direction or list of [SortSpecifier](../reference_2.md#object-sortspecifier)s) to match the [ListGridSortState](../reference.md#type-listgridsortstate) object passed in.  
Used to restore previous state retrieved from the grid by a call to [ListGrid.getSortState](#method-listgridgetsortstate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortState | [ListGridSortState](../reference.md#type-listgridsortstate) | false | — | Object describing the desired sort state for the grid. |

### Groups

- viewState

### See Also

- [ListGrid.getSortState](#method-listgridgetsortstate)

---
## Method: ListGrid.setDataSource

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
## Method: ListGrid.getUserCriteriaState

### Description
Returns a snapshot of the current user-provided criteria for this ListGrid.

This object can be passed to [ListGrid.setUserCriteriaState](#method-listgridsetusercriteriastate) to reset this grid's user-criteria to the current state.

### Returns

`[ListGridUserCriteriaState](../reference_2.md#type-listgridusercriteriastate)` — current criteria state for the grid.

### Groups

- viewState

### See Also

- [ListGridUserCriteriaState](../reference_2.md#type-listgridusercriteriastate)
- [ListGrid.setUserCriteriaState](#method-listgridsetusercriteriastate)

---
## Method: ListGrid.formatInactiveCellValue

### Description
Formatter for inactive content.

If present, this method will be invoked instead of [ListGrid.formatCellValue](#method-listgridformatcellvalue) in cases where the grid is rendering non-interactive content outside. Examples of cases where this can happen include:

*   dragTracker HTML for a row when [ListGrid.dragTrackerMode](ListGrid_1.md#attr-listgriddragtrackermode) is set to "record"
*   measurement HTML used for sizing columns during autoFit
*   measurement HTML used for sizing rows when [ListGrid.fixedRecordHeights](ListGrid_1.md#attr-listgridfixedrecordheights) is false and the grid has both frozen and unfrozen fields

May also be overridden at the [field level](ListGridField.md#method-listgridfieldformatinactivecellvalue).

This is useful for cases where it would not be appropriate to render the standard formatted cell value outside of the body of the grid. An example might be if the formatted value contains a DOM element with a specified ID - an approach sometimes used for integrating third party components into SmartClient listGrid cells. In this case developers will wish to avoid having the framework render an element with the same ID outside of the grid, and should instead return HTML that would render at the same size, with an appropriate appearance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value for the cell being |
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object for the cell. Note: If this is a new row that has not been saved, in an editable grid, it has no associated record object. In this case the edit values will be passed in as this parameter. |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number for the cell. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — formatted value to display in the cell.

### See Also

- [ListGrid.formatCellValue](#method-listgridformatcellvalue)
- [ListGridField.formatInactiveCellValue](ListGridField.md#method-listgridfieldformatinactivecellvalue)

---
## Method: ListGrid.unsort

### Description
Turn sorting off, typically because data has changed and is no longer sorted.

Calling `unsort()` disables visual indication of which columns are sorted, and calls `unsort()` on the underlying dataset if supported.

Note that a grid viewing a paged dataset may not be able to support [ResultSet.unsort](ResultSet.md#method-resultsetunsort) because the sort order is what establishes the row numbering that allows data to be fetched in batches. In this case the dataset will be explicitly sorted to an empty array which may cause the cache to be invalidated and a new fetch.

`unsort()` is automatically called in response to edits or changes to the data set that would cause records to be reordered. See [editing](../kb_topics/editing.md#kb-topic-grid-editing) for further details on editing records in a sorted ListGrid.

### Groups

- sorting

---
## Method: ListGrid.exportClientData

### Description
Exports this component's data with client-side formatters applied, so is suitable for direct display to users, using the specified [export format](DSRequest.md#attr-dsrequestexportas).

A variety of DSRequest settings, such as [exportAs](DSRequest.md#attr-dsrequestexportas) and [DSRequest.exportFilename](DSRequest.md#attr-dsrequestexportfilename), affect the exporting process: see [exportResults](DSRequest.md#attr-dsrequestexportresults) for further detail.

If this component is [databound](DataBoundComponent.md#method-databoundcomponentsetdatasource) and not all records that match the current [filter-criteria](#method-listgridgetcriteria) have [been loaded](ResultSet.md#method-resultsetallmatchingrowscached), you can call [ListGrid.loadAllRecords](#method-listgridloadallrecords) - this method accepts a callback which is fired when all necessary data has arrived. When that callback fires, a call to `exportClientData` will have access to the full dataset for the filter.

This feature requires the SmartClient server.

If your ListGrid has custom formatters, formatted values will be exported by default, with HTML normalized to text where possible. Since some levels of HTML normalizing aren't possible, this may result in missing or incorrect export values. In this case, you have three options:

*   Set [exportRawValues](ListGridField.md#attr-listgridfieldexportrawvalues) on the field. This will export the raw underlying value of the field; your formatter will not be called
*   Have your formatter call [isExportingClientData()](#method-listgridisexportingclientdata) and perform whatever alternative formatting you require if that method returns true
*   Set [exportRawNumbers](ListGridField.md#attr-listgridfieldexportrawnumbers) on the field. This will export the raw underlying number of the field; your formatter will not be called

Note that during export, the [ListGridField.escapeHTML](ListGridField.md#attr-listgridfieldescapehtml) setting on a field determines how escaped and unescaped HTML values are handled. In particular, if `escapeHTML` is not set for a field, a value like "`<FOO>`" will be exported as the empty string, and you'd need the escaped value "&lt;FOO&gt;" to end up exporting "`<FOO>`".

Ordinarily, calls to this method go through the static classMethod [DataSource.exportClientData](DataSource.md#classmethod-datasourceexportclientdata). In this case, no server-side DataSources are required. However, if this component is [databound](DataBoundComponent.md#method-databoundcomponentsetdatasource) and you specify a valid [operationId](DSRequest.md#attr-dsrequestoperationid) in the properties passed to this method, the call will go through the instance method [DataSource.exportClientData](DataSource.md#method-datasourceexportclientdata) instead. As the documentation for that method explains, this allows you more control on the server side. This approach requires both the SmartClient server and server-side DataSource definitions.

To export data from this component's dataSource, see [exportData](DataBoundComponent.md#method-databoundcomponentexportdata), which does not include client-side formatters, but **does** include formatters declared in the `.ds.xml` file. `exportData()` relies on both the SmartClient server and server-side DataSources.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Request properties for the export. Note that specifying [exportData](DSRequest.md#attr-dsrequestexportdata) on the request properties allows the developer to pass in an explicit data set to export. |
| callback | [RPCCallback](#type-rpccallback) | true | — | Optional callback. If you specify [exportToClient](DSRequest.md#attr-dsrequestexporttoclient): false in the request properties, this callback will fire after export completes. Otherwise the callback will fire right before the download request is made to the server. |

### See Also

- [DataSource.exportClientData](DataSource.md#method-datasourceexportclientdata)
- [exportFormatting](../kb_topics/exportFormatting.md#kb-topic-exports--formatting)

---
## Method: ListGrid.setBodyStyleName

### Description
Update the [bodyStyleName](ListGrid_1.md#attr-listgridbodystylename) for this listGrid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| styleName | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new body style name |

---
## Method: ListGrid.getEditedRecord

### Description
Returns the combination of unsaved edits (if any) and original values (if any) for a given row being edited.

The returned value is never null, and can be freely modified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valuesID | [number](#type-number)|[Object](../reference.md#type-object) | false | — | rowNum of the record being edited, or an Object containing values for all the record's primary keys |

### Returns

`[Object](../reference.md#type-object)` — A copy of the record with unsaved edits included

### Groups

- editing

---
## Method: ListGrid.hasChanges

### Description
Whether the grid as a whole has any unsaved edits, in any row. Note that this method will return true if any rows are [marked as removed](#method-listgridmarkrecordremoved) in addition to any rows that have unsaved edits.

Note that if this grid is bound to a [dataSource](ListGrid_1.md#attr-listgriddatasource), and an asynchronous save has been submitted, this method will compare the local edit values against the submitted values by default, returning false (no changes), if they match. This is useful for detecting whether the user is actively editing values and hasn't yet committed them.

The `ignorePendingValues` parameter may be used by developers who want to ignore this case and simply compare edit values against the record in the local data set.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ignorePendingValues | [Boolean](#type-boolean) | true | — | If true, this method will compare the current edit values against the underlying records in the dataset, not taking pending edit values into account |

### Returns

`[Boolean](#type-boolean)` — returns true of any unsaved edits are present

### Groups

- editing

---
## Method: ListGrid.fetchRowCount

### Description
For databound grids, method will fall through to [ResultSet.fetchRowCount](ResultSet.md#method-resultsetfetchrowcount), allowing developers to request an accurate row count from the dataSource when [progressive loading is active](DataSource.md#attr-datasourceprogressiveloading).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [RowCountCallback](#type-rowcountcallback) | true | — | Callback to fire when the fetch request completes. To retrieve details of the row-count that was retrieved from the server, use the `getRowCount()` and `getRowCountStatus()` methods. |
| dsRequest | [DSRequest Properties](#type-dsrequest-properties) | true | — | Custom properties for the row count fetch request |

### Groups

- rowRangeDisplay

---
## Method: ListGrid.rowOver

### Description
Called when the mouse pointer enters a row

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.getGroupMembers

### Description
For a [grouped](ListGrid_1.md#attr-listgridgroupbyfield) grid, returns all the direct children of the supplied node in the [ListGrid.groupTree](ListGrid_1.md#attr-listgridgrouptree) if `recordsOnly` false. Otherwise, if `recordsOnly` is true, returns instead a list of all descendants under the supplied node that are actual records from the grid's original data - i.e. that are not other group nodes (for multi-grouping) or summary records.

Note that null may be returned if the grid is not currently grouped or the supplied node is not a valid [GroupNode](../reference.md#object-groupnode).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [GroupNode](#type-groupnode) | false | — | node from [ListGrid.groupTree](ListGrid_1.md#attr-listgridgrouptree) |
| recordsOnly | [boolean](../reference.md#type-boolean) | false | — | `true` to return all descendants that are actual records from the grid's original data, or `false` to return all immediate children of the supplied group node |

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — records under the supplied node, as specified above, or null if we're not grouping or the node isn't a group node

### Groups

- grouping

---
## Method: ListGrid.setAutoFitFieldWidths

### Description
Setter for [ListGrid.autoFitFieldWidths](ListGrid_1.md#attr-listgridautofitfieldwidths). Modifies the default auto-fit-width behavior for fields in this grid. Note that this may be overridden at the field level via [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoFit | [boolean](../reference.md#type-boolean) | false | — | New value for autoFitFieldWidths |
| dontResetWidths | [boolean](../reference.md#type-boolean) | true | — | If autoFitFieldWidths was true, and is being set to false, should fields be resized to their originally specified size? Pass in this parameter to suppress this behavior. |

---
## Method: ListGrid.showRecordComponent

### Description
When [ListGrid.showRecordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents) is true, return false from this method to prevent the recordComponent system from processing the passed record or cell.

**If [showRecordComponentsByCell](ListGrid_1.md#attr-listgridshowrecordcomponentsbycell) is true, it is important to implement this method** - especially if the grid has many fields - otherwise, the internal automatic detection will process every visible cell, checking, for example, whether a component already exists for that cell, before eventually running [ListGrid.createRecordComponent](#method-listgridcreaterecordcomponent) to check if one is required. Implementing this method avoids all that processing for cells that aren't expected to have components.

The second parameter is only applicable if [ListGrid.showRecordComponentsByCell](ListGrid_1.md#attr-listgridshowrecordcomponentsbycell) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record being processed |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | column index of the cell in which the record component may be shown. Will be null unless showRecordComponentsByCell is true. |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel showRecordComponent behavior

### Groups

- recordComponents

---
## Method: ListGrid.hideFields

### Description
Force an array of fields to be hidden.

NOTE: If a field.showIf expression exists, it will be destroyed.

When hiding multiple fields, this method should be called rather than calling [ListGrid.hideField](#method-listgridhidefield) repeatedly for each field to hide.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fields | [Array of String](#type-array-of-string)|[Array of ListGridField](#type-array-of-listgridfield) | false | — | fields to hide |
| suppressRelayout | [boolean](../reference.md#type-boolean) | true | — | if passed, don't relayout non-explicit sized fields to fit the available space |

---
## Method: ListGrid.sorterClick

### Description
Notification method fired when the user clicks on the corner [sort button](ListGrid_1.md#attr-listgridsorterconstructor). Return false to suppress the sort.

### Returns

`[boolean](../reference.md#type-boolean)` — return false to suppress the sort

### Groups

- events
- sorting

**Flags**: A

---
## Method: ListGrid.getExpansionComponent

### Description
When [ListGrid.canExpandRecords](ListGrid_1.md#attr-listgridcanexpandrecords) is true, gets the embedded-component to show as a given record's expansionComponent. This component is then housed in [a VLayout](ListGrid_1.md#attr-listgridexpansionlayout) and embedded into a record's row.

By default, this method returns one of a set of built-in components, according to the value of [listGrid.expansionMode](../reference_2.md#type-expansionmode). You can override this method to return any component you wish to provide as an expansionComponent.

As long as the record is expanded, this component may be retrieved via a call to [ListGrid.getCurrentExpansionComponent](#method-listgridgetcurrentexpansioncomponent).

When an expanded record is collapsed, the component is disassociated from the record and may or may not be automatically destroyed. By default, built-in components will be destroyed on unembed according to the [pooling mode](ListGrid_1.md#attr-listgridexpansioncomponentpoolingmode) being used. Custom expansion components, created via an override of getExpansionComponents(), will **_not_** be auto-destroyed - developers should override [ListGrid.collapseRecord](#method-listgridcollapserecord) to take care of clean-up for such components.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to get the expansionComponent for |

### Returns

`[Canvas](#type-canvas)|[Canvas Properties](#type-canvas-properties)` — the component to embed

### Groups

- expansionField

### See Also

- [ListGrid.expansionScreen](ListGrid_1.md#attr-listgridexpansionscreen)

---
## Method: ListGrid.setSelectionAppearance

### Description
Changes selectionAppearance on the fly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectionAppearance | [SelectionAppearance](../reference.md#type-selectionappearance) | false | — | new selection appearance |

---
## Method: ListGrid.getFields

### Description
Get the array of all **currently visible** fields for this ListGrid.

This list fields is only valid once the ListGrid has been [drawn](Canvas.md#method-canvasdraw) or once [ListGrid.setFields](#method-listgridsetfields) has been called explicitly. If called earlier, only the list of directly specified fields will be returned (the Array passed to create()).

This Array should be treated as **read-only**. To modify the set of visible fields, use [ListGrid.showField](#method-listgridshowfield), [ListGrid.hideField](#method-listgridhidefield) and related APIs. To update properties of individual fields, use [ListGrid.setFieldProperties](#method-listgridsetfieldproperties) or more specific APIs such as [ListGrid.setFieldTitle](#method-listgridsetfieldtitle).

To get the Array of all fields, including fields that are not currently visible or were specified implicitly, use [ListGrid.getAllFields](#method-listgridgetallfields).

### Returns

`[Array of ListGridField](#type-array-of-listgridfield)` — Array of all currently visible fields

---
## Method: ListGrid.setUserAIFilterRequest

### Description
If filter-via-AI is enabled (see [ListGrid.filterViaAIMode](ListGrid_1.md#attr-listgridfilterviaaimode)), this utility method first calls [AI.buildCriterion](AI.md#classmethod-aibuildcriterion) to build [AdvancedCriteria](../reference.md#object-advancedcriteria) for the user's request, then sets this grid's filter criteria.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| userAIFilterRequest | [UserAIRequest](#type-userairequest) | false | — | the user's natural language description of a filter. |
| buildRequestProperties | [BuildCriterionRequest Properties](#type-buildcriterionrequest-properties) | true | — | request properties to use. Note that [userAIRequest](../reference.md#attr-buildcriterionrequestuserairequest) will be overridden by `userAIFilterRequest`, [dataSource](../reference.md#attr-buildcriterionrequestdatasource) will be overridden by this grid's [DataSource](DataSource.md#class-datasource), and [mode](../reference.md#attr-buildcriterionrequestmode) will be overridden by [ListGrid.filterViaAIMode](ListGrid_1.md#attr-listgridfilterviaaimode). |
| callback | [BuildCriterionResponseCallback](#type-buildcriterionresponsecallback) | true | — | optional callback to fire. |

---
## Method: ListGrid.setBodyOverflow

### Description
Update the [bodyOverflow](ListGrid_1.md#attr-listgridbodyoverflow) for this listGrid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| overflow | [Overflow](../reference.md#type-overflow) | false | — | new overflow setting for the body |

**Flags**: A

---
## Method: ListGrid.hideField

### Description
Force a field to be hidden.  
  
NOTE: If a field.showIf expression exists, it will be destroyed.

Note also that if multiple fields are to be hidden it is more efficient to call [ListGrid.hideFields](#method-listgridhidefields) passing in the array of fields to hide rather than to call this method repeatedly. In particular, this will ensure [ListGrid.recalculateSummaries](#method-listgridrecalculatesummaries) is only run once.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [String](#type-string)|[ListGridField](#type-listgridfield) | false | — | field to hide |
| suppressRelayout | [boolean](../reference.md#type-boolean) | true | — | if passed, don't relayout non-explicit sized fields to fit the available space |

---
## Method: ListGrid.cellSelectionChanged

### Description
Called when (cell-based) selection changes within this grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellList | [Array](#type-array) | false | — | Array of cells whos selected state was modified. |

### Returns

`[boolean](../reference.md#type-boolean)` — Returning false will prevent the GridRenderer styling from being updated to reflect the selection change.

### Groups

- selection

**Flags**: A

---
## Method: ListGrid.setFixedRecordHeights

### Description
Setter for [ListGrid.fixedRecordHeights](ListGrid_1.md#attr-listgridfixedrecordheights)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fixedRecordHeights | [boolean](../reference.md#type-boolean) | false | — | New fixedRecordHeights value |

---
## Method: ListGrid.drawAreaChanged

### Description
Notification method that fires when the drawArea changes due to scrolling. Receives the previous drawArea co-ordinates as parameters. Call [ListGrid.getDrawArea](#method-listgridgetdrawarea) to get the new drawArea co-ordinates.

Note that if this grid is showing any [frozen fields](ListGridField.md#attr-listgridfieldfrozen), they will not be included in the `oldStartCol`, `oldEndCol` range reported by this method. Frozen fields are assumed never to be scrolled out of view.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| oldStartRow | [number](#type-number) | false | — | the startRow from before the drawArea changed |
| oldEndRow | [number](#type-number) | false | — | the endRow from before the drawArea changed |
| oldStartCol | [number](#type-number) | false | — | the startCol from before the drawArea changed |
| oldEndCol | [number](#type-number) | false | — | the endCol from before the drawArea changed |

**Flags**: A

---
## Method: ListGrid.createRecordComponent

### Description
When [ListGrid.showRecordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents) is true, this method is called to create per-row or per-cell embedded components to display in the grid.

The colNum parameter is applicable only when [ListGrid.showRecordComponentsByCell](ListGrid_1.md#attr-listgridshowrecordcomponentsbycell) is true.

If this row should not have a `recordComponent`, return null.

This method should create and return a new component for the record passed in every time it is called and never return the same Canvas instance twice. To re-use components with different rows, set [RecordComponentPoolingMode](../reference_2.md#type-recordcomponentpoolingmode) to "recycle". In this mode, in addition to implementing this method, developers should also implement [ListGrid.updateRecordComponent](#method-listgridupdaterecordcomponent) which allows already created components to be altered for re-use in new records. See the [ListGrid.showRecordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents) overview for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to create a component for |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | cell to which the component applies |

### Returns

`[Canvas](#type-canvas)` — return the component to embed in the passed record

### Groups

- recordComponents

---
## Method: ListGrid.redrawHeader

### Description
Redraw just the [grid header](ListGrid_1.md#attr-listgridheader)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rightNow | [boolean](../reference.md#type-boolean) | false | — | If true, redraw the grid header with a direct inline call to its redraw() method. Otherwise, [mark the header for redraw](Canvas.md#method-canvasmarkforredraw) |

---
## Method: ListGrid.getValueIcon

### Description
Returns the appropriate valueIcon for a cell based on the field and the data value for the cell. Default implementation returns null if [ListGridField.suppressValueIcon](ListGridField.md#attr-listgridfieldsuppressvalueicon) is true otherwise looks at [ListGridField.valueIcons](ListGridField.md#attr-listgridfieldvalueicons).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field associated with the cell |
| value | [Any](#type-any) | false | — | data value for the cell's record in this field. |
| record | [ListGridRecord](#type-listgridrecord) | false | — | record associated with this cell |

### Returns

`[SCImgURL](../reference.md#type-scimgurl)` — url for the icon

### Groups

- imageColumns

---
## Method: ListGrid.updateData

### Description
Perform a DataSource "update" operation to update existing records in this component's DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| updatedRecord | [Record](#type-record) | false | — | updated record |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | method to call on operation completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: ListGrid.fetchData

### Description
Retrieves data from the DataSource that matches the specified criteria.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

When `fetchData()` is first called, if data has not already been provided via [setData()](#method-listgridsetdata), this method will create a [ResultSet](ResultSet.md#class-resultset), which will be configured based on component settings such as [DataBoundComponent.fetchOperation](DataBoundComponent.md#attr-databoundcomponentfetchoperation) and [DataBoundComponent.dataPageSize](DataBoundComponent.md#attr-databoundcomponentdatapagesize), as well as the general purpose [ListGrid.dataProperties](ListGrid_1.md#attr-listgriddataproperties). The created ResultSet will automatically send a DSRequest to retrieve data from [listGrid.dataSource](ListGrid_1.md#attr-listgriddatasource), and from then on will automatically manage paging through large datasets, as well as performing filtering and sorting operations inside the browser when possible - see the [ResultSet](ResultSet.md#class-resultset) docs for details.

**NOTE:** do not use **both** [autoFetchData:true](DataBoundComponent.md#attr-databoundcomponentautofetchdata) **and** a call to `fetchData()` - this may result in two DSRequests to fetch data. Use either [autoFetchData](DataBoundComponent.md#attr-databoundcomponentautofetchdata) and [Criteria](../reference_2.md#type-criteria) **or** a manual call to fetchData() passing criteria.

Whether a ResultSet was automatically created or provided via [setData()](#method-listgridsetdata), subsequent calls to fetchData() will simply call [ResultSet.setCriteria](ResultSet.md#method-resultsetsetcriteria).

Changes to criteria may or may not result in a DSRequest to the server due to [client-side filtering](ResultSet.md#attr-resultsetuseclientfiltering). You can call [willFetchData(criteria)](DataBoundComponent.md#method-databoundcomponentwillfetchdata) to determine if new criteria will result in a server fetch.

If you need to force data to be re-fetched, you can call [invalidateCache()](#method-listgridinvalidatecache) and new data will automatically be fetched from the server using the current criteria and sort direction. **NOTE:** when using `invalidateCache()` there is no need to **also** call `fetchData()` and in fact this could produce unexpected results.

This method takes an optional callback parameter (set to a [DSCallback](../reference_2.md#type-dscallback)) to fire when the fetch completes. Note that this callback will not fire if no server fetch is performed. In this case the data is updated synchronously, so as soon as this method completes you can interact with the new data. If necessary, you can use [willFetchData()](DataBoundComponent.md#method-databoundcomponentwillfetchdata) to determine whether or not a server fetch will occur when `fetchData()` is called with new criteria.

In addition to the callback parameter for this method, developers can use [dataArrived()](#method-listgriddataarrived) to be notified every time data is loaded.

By default, this method assumes a [TextMatchStyle](../reference_2.md#type-textmatchstyle) of "exact"; that can be overridden by supplying a different value in the requestProperties parameter. See [DataBoundComponent.willFetchData](DataBoundComponent.md#method-databoundcomponentwillfetchdata);

**Changing the request properties**

Changes to [TextMatchStyle](../reference_2.md#type-textmatchstyle) made via `requestProperties` will be honored in combination with the fetch criteria, possibly invalidating cache and triggering a server request if needed, as documented for [willFetchData()](DataBoundComponent.md#method-databoundcomponentwillfetchdata). In contrast, changes to [operationId](DSRequest.md#attr-dsrequestoperationid) in the request properties will cause the [ResultSet](ResultSet.md#class-resultset) or [ResultTree](ResultTree.md#class-resulttree) to be rebuilt, always refetching from the server. However, changes to other request properties after the initial fetch won't be detected, and no fetch will get triggered based on that new request context.

To pick up such changes, we recommend that you call [setData(\[\])](#method-listgridsetdata) (passing an empty array to ensure the data model is cleared), and then call this method to fetch again. If you try to do it by calling [invalidateCache()](#method-listgridinvalidatecache), you may see duplicate fetches if you haven't already updated the data context by calling this method with the new request properties, and fail to do so before the component is [redrawn](Canvas.md#method-canvasredraw).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | Search criteria. If a [DynamicForm](DynamicForm.md#class-dynamicform) is passed in as this argument instead of a raw criteria object, will be derived by calling [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke when a fetch is complete. Fires only if server contact was required |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.refreshData](#method-listgridrefreshdata)

---
## Method: ListGrid.getFieldState

### Description
Returns a snapshot of the current presentation of this listGrid's fields as a [ListGridFieldState](../reference_2.md#type-listgridfieldstate) object.

This object can later be passed to [ListGrid.setFieldState](#method-listgridsetfieldstate) to reset this grid's fields to the current state.

Note that the information stored includes the current width and visibility of each of this grid's fields, as well as any [formula](ListGrid_1.md#attr-listgridcanaddformulafields) or [summary fields](ListGrid_1.md#attr-listgridcanaddsummaryfields) added by the user.

The optional `sparse` parameter governs whether the returned field state should omit state information for hidden fields. If this parameter is not passed explicitly, field state will be sparse if [DataBoundComponent.sparseFieldState](DataBoundComponent.md#attr-databoundcomponentsparsefieldstate) is true.  
When applying sparse field state to a component via [ListGrid.setFieldState](#method-listgridsetfieldstate), any explicitly defined fields on the component that were not captured in the stored state object will be hidden.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sparse | [Boolean](#type-boolean) | true | — | If true, field state will be ommitted for hidden fields. |

### Returns

`[ListGridFieldState](../reference_2.md#type-listgridfieldstate)` — current state of this grid's fields.

### Groups

- viewState

### See Also

- [ListGrid.setFieldState](#method-listgridsetfieldstate)

---
## Method: ListGrid.getColumnPageLeft

### Description
Return the left coordinate for a given column number as a GLOBAL coordinate

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [Integer](../reference_2.md#type-integer) | false | — | number of the column |

### Returns

`[Integer](../reference_2.md#type-integer)` — page left offset of the passed colNum, or null if undrawn or no such column

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: ListGrid.getEventColumn

### Description
Returns the column number of the provided X-coordinate, or the most recent mouse event if an X-coordinate is not provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../reference_2.md#type-integer) | true | — | X-coordinate relative to the left edge of the content to obtain the column number for. If not provided, then [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx) will be used. |

### Returns

`[int](../reference.md#type-int)` — column number, or -2 if beyond last drawn column

### Groups

- events

---
## Method: ListGrid.setFieldHeaderTitleStyle

### Description
Update the [ListGridField.headerTitleStyle](ListGridField.md#attr-listgridfieldheadertitlestyle) for a field within the grid at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | name of the field. |
| newStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new titleTyle for the field header |

---
## Method: ListGrid.getEditValues

### Description
Returns the current set of unsaved edits for a given row being edited.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valuesID | [number](#type-number)|[Object](../reference.md#type-object) | false | — | rowNum of the record being edited, or an Object containing values for all the record's primary keys |

### Returns

`[Object](../reference.md#type-object)` — Current editValues object for the row. This contains the current edit values in {fieldName1:value1, fieldName2:value2} format.

### Groups

- editing

---
## Method: ListGrid.focusInCell

### Description
Puts keyboard focus into the specified cell, showing a highlighted (roll-over style) appearance, and ensuring that arrow-key navigation will start from the specified cell.

Only applies where [ListGrid.canSelectCells](ListGrid_1.md#attr-listgridcanselectcells) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| row | [Integer](../reference_2.md#type-integer) | false | — | Index of target row |
| col | [Integer](../reference_2.md#type-integer) | false | — | Index of target col |

### See Also

- [ListGrid.focusInRow](#method-listgridfocusinrow)

---
## Method: ListGrid.selectionChanged

### Description
Called when (row-based) selection changes within this grid. Note this method fires for each record for which selection is modified - so when a user clicks inside a grid this method will typically fire twice (once for the old record being deselected, and once for the new record being selected).

NOTE: For updating other components based on selections or triggering selection-oriented events within an application, see the [selectionUpdated()](DataBoundComponent.md#method-databoundcomponentselectionupdated) event which is likely more suitable. Calls to [getSelection()](#method-listgridgetselection) from within this event may not return a valid set of selected records if the event has been triggered by a call to [selectAllRecords()](DataBoundComponent.md#method-databoundcomponentselectallrecords) or [deselectAllRecords()](DataBoundComponent.md#method-databoundcomponentdeselectallrecords) - in this case use the [selectionUpdated()](DataBoundComponent.md#method-databoundcomponentselectionupdated) event instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for which selection changed |
| state | [boolean](../reference.md#type-boolean) | false | — | New selection state (true for selected, false for unselected) |

### Groups

- selection

---
## Method: ListGrid.canExpandRecord

### Description
Indicates whether a given record or rowNum can be expanded. The default implementation checks the value of [ListGrid.canExpandRecords](ListGrid_1.md#attr-listgridcanexpandrecords) and `record[[ListGrid.canExpandRecordProperty](ListGrid_1.md#attr-listgridcanexpandrecordproperty)]`.

Override this method for more specific control over individual record expansion.

**Note:** Rows with no underlying record in the data array - for example newly added edit rows that have not yet been saved - cannot be expanded.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to work with |
| rowNum | [Number](#type-number) | false | — | rowNum of the record to work with |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the record can be expanded

### Groups

- expansionField

---
## Method: ListGrid.displaySort

### Description
Modify the grid UI to reflect the parameter sortSpecifiers. For a single sortSpecifier, this consists of marking the field with a directional arrow in its header button (if it visible).

If multiple fields are sorted, those that are visible show a directional icon and a small [sort-numeral](ListGrid_1.md#attr-listgridsortnumeralstyle) indicating that field's index in the sort configuration.

See [addSort()](#method-listgridaddsort) and [toggleSort()](#method-listgridtogglesort) APIs for information on making changes to the current sort configuration.

**NOTE:** This method is primarily used by [ListGrid.setSort](#method-listgridsetsort); it is not intended to be called by user code, unless you are implementing a custom [setSortHandler](#method-listgridsetsorthandler)). For the normal use case, calling this method directly will fail to execute vital pre-steps. If you are not implementing a custom handler as described above, do not call this method directly - call `setSort()` instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifiers | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | Array of [SortSpecifier](../reference_2.md#object-sortspecifier) objects |

**Flags**: A

---
## Method: ListGrid.cellHasErrors

### Description
Given a rowNum and a colNum or fieldName, determine whether we currently have stored validation errors for the record/field in question.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | index of row to check for validation errors |
| fieldID | [String](#type-string)|[number](#type-number) | false | — | name of field, or index of column to check for validation errors |

### Returns

`[Boolean](#type-boolean)` — true if we have validation errors for the row/col in question

### Groups

- gridValidation

### See Also

- [ListGrid.hasErrors](#method-listgridhaserrors)
- [ListGrid.rowHasErrors](#method-listgridrowhaserrors)

---
## Method: ListGrid.getFieldNum

### Description
Given a field or field id, return it's index in the fields array

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldID | [String](#type-string)|[number](#type-number) | false | — | field number or field.name |

### Returns

`[int](../reference.md#type-int)` — index of the field within this.fields

### Groups

- display

**Flags**: A

---
## Method: ListGrid.getFieldContentWidth

### Description
Returns the pixel width of the content of a visible field in this grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field to test |

### Returns

`[Integer](../reference_2.md#type-integer)` — drawn width of this fields content

---
## Method: ListGrid.setRecordRadius

### Description
Setter for [ListGrid.recordRadius](ListGrid_1.md#attr-listgridrecordradius), which provides rounded corners for rows in this grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recordRadius | [String](#type-string) | false | — | any CSS border-radius string, with 1 to 4 space-separated sizes |

---
## Method: ListGrid.setCanExpandRecords

### Description
Setter for [ListGrid.canExpandRecords](ListGrid_1.md#attr-listgridcanexpandrecords)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canExpand | [boolean](../reference.md#type-boolean) | false | — | new value for listGrid.canExpandRecords. |

---
## Method: ListGrid.getAriaState

### Description
Dynamically retrieves the aria properties to write out for this listGrid in [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode).

If [ListGrid.ariaRole](ListGrid_1.md#attr-listgridariarole) is set to `"grid"` this will return an object with `rowcount` and `colcount` attributes populated to indicate this size of the grid and its data.

If a static [ariaState](Canvas.md#attr-canvasariastate) has been specified, the default implementation will apply these dynamically derived properties in addition to any properties specified on the static object.

Note that [redrawing](Canvas.md#method-canvasredraw) the grid will re-evaluate this method and apply the result to the handle.

### Returns

`[Object](../reference.md#type-object)` — object containing aria attribute names and values to apply to this grid's handle

**Flags**: A

---
## Method: ListGrid.setHeaderSpanTitle

### Description
Update the title of a [headerSpan](ListGrid_1.md#attr-listgridheaderspans) dynamically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | name of the headerSpan, as specified via [HeaderSpan.name](HeaderSpan.md#attr-headerspanname). |
| newTitle | [String](#type-string) | false | — | new title for the headerSpan |

### Groups

- headerSpan

---
## Method: ListGrid.getCellRole

### Description
Returns the WAI ARIA role for cells within this listGrid.

If the record has a value for the [ListGrid.recordCellRoleProperty](ListGrid_1.md#attr-listgridrecordcellroleproperty), this will be respected.  
Otherwise if [ListGrid.cellRole](ListGrid_1.md#attr-listgridcellrole) is specified, it will be used.

If neither property is set, the default implementation will return `"gridcell"` if this listGrid has [role:"grid"](ListGrid_1.md#attr-listgridariarole), otherwise `null`, meaning no role will be written out for cells.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | row index of the cell |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | column index of the cell |
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record for the cell in question |

### Returns

`[String](#type-string)` — role for cells within this grid

### Groups

- accessibility

**Flags**: A

---
## Method: ListGrid.getRequiredFieldMessage

### Description
Returns the message to display when a user attempts to save a required field with an empty value. By default returns [Validator.requiredField](Validator.md#classattr-validatorrequiredfield).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [Object](../reference.md#type-object) | false | — | definition of the field being edited |
| record | [Object](../reference.md#type-object) | false | — | record object being edited |

### Returns

`[String](#type-string)` — "Field is required"

### Groups

- i18nMessages
- gridValidation

---
## Method: ListGrid.cellDoubleClick

### Description
Called when a cell receives a double click event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object returned from getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.dataArrived

### Description
Notification method fired when new data arrives from the [DataSource](ListGrid_1.md#attr-listgriddatasource) to be displayed in this ListGrid, (for example in response to the user scrolling a new set of rows into view). Only applies to databound listGrids where the [data](ListGrid_1.md#attr-listgriddata) attribute is a [ResultSet](ResultSet.md#class-resultset). This ResultSet may have been created manually and applied to the grid via a call to [ListGrid.setData](#method-listgridsetdata) or may have been created and automatically assigned if [ListGrid.fetchData](#method-listgridfetchdata) was used to populate the grid. This method is fired directly in response to [dataArrived()](ResultSet.md#method-resultsetdataarrived) firing on the data object.

Note that `dataArrived()`, unlike [ListGrid.dataChanged](#method-listgriddatachanged), only fires in limited circumstances - when data for a [ResultSet](ResultSet.md#class-resultset) arrives from the DataSource due to a fetch or cache invalidation, or as a result of [filtering](ListGrid_1.md#attr-listgridfilterlocaldata). If you want to catch all data changes, you should instead react to [ListGrid.dataChanged](#method-listgriddatachanged).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../reference.md#type-int) | false | — | starting index of the newly loaded set of rows |
| endRow | [int](../reference.md#type-int) | false | — | ending index of the newly loaded set of rows (non inclusive). |

### See Also

- [ListGrid.dataChanged](#method-listgriddatachanged)

**Flags**: A

---
## Method: ListGrid.groupTreeChanged

### Description
Callback fired when a [grouping](ListGrid_1.md#attr-listgridgroupbyfield) operation completes, whether it started as a direct call to [ListGrid.groupBy](#method-listgridgroupby) or [ListGrid.regroup](#method-listgridregroup) or data changing, including incremental changes.

If `changeType` is "groupBy", [ListGrid.handleGroupBy](#method-listgridhandlegroupby) should have been called at the beginning of the operation, and [ListGrid.groupByComplete](#method-listgridgroupbycomplete) will be called immediately before this method. If `changeType` is "regroup", then [ListGrid.handleRegroup](#method-listgridhandleregroup) should have been called at the beginning of the operation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| changeType | [GroupTreeChangeType](../reference_2.md#type-grouptreechangetype) | false | — | did the change originate from [ListGrid.groupBy](#method-listgridgroupby), [ListGrid.regroup](#method-listgridregroup). or an incremental data change? |
| success | [boolean](../reference.md#type-boolean) | false | — | did the operation complete successfully? |

### Groups

- grouping

### See Also

- [ListGrid.handleRegroup](#method-listgridhandleregroup)
- [ListGrid.groupByComplete](#method-listgridgroupbycomplete)

---
## Method: ListGrid.cellChanged

### Description
Fires after user edits have been successfully saved to the server, only for cells where the value was actually modified.

If you want immediate notification of a changes **before** changes has been saved to the server, implement [field.change()](ListGridField.md#method-listgridfieldchange) or [field.changed()](ListGridField.md#method-listgridfieldchanged) instead.

You can alternatively use [ListGridField.cellChanged](ListGridField.md#method-listgridfieldcellchanged) to get notification only of saved changes for a specific field. If both a listGridField and the containing listGrid have a handler for this event, only the handler defined on the field is called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for the cell being changed |
| newValue | [Any](#type-any) | false | — | new value for the cell |
| oldValue | [Any](#type-any) | false | — | old value for the cell |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |
| grid | [ListGrid](#type-listgrid) | false | — | grid where cell was changed. Also available as "this" |

### Groups

- editing

### See Also

- [ListGridField.cellChanged](ListGridField.md#method-listgridfieldcellchanged)

---
## Method: ListGrid.getRecordSummary

### Description
Provides access to the summary (see [summary-type](../reference.md#type-listgridfieldtype) fields) value of the record for other fields when called from inside the body of [ListGridField.getRecordSummary](ListGridField.md#method-listgridfieldgetrecordsummary) (since they're not available directly off the record). The behavior is unspecified if not called from inside the [ListGridField.getRecordSummary](ListGridField.md#method-listgridfieldgetrecordsummary) method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for which a summary is being generated |
| field | [ListGridField](#type-listgridfield)|[int](../reference.md#type-int)|[ID](#type-id) | false | — | field, or its number or id |

### Returns

`[Any](#type-any)` — summary value to display

**Flags**: A

---
## Method: ListGrid.selectRecord

### Description
Select/deselect a [Record](../reference.md#object-record) passed in explicitly, or by index.

Note that this method selects records unconditionally, allowing multiple selected records, even when [ListGrid.selectionType](ListGrid_1.md#attr-listgridselectiontype) is "single". To enforce mutually-exclusive record-selection, use [ListGrid.selectSingleRecord](#method-listgridselectsinglerecord).

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
## Method: ListGrid.setHideOnPhone

### Description
Updates the [ListGridField.hideOnPhone](ListGridField.md#attr-listgridfieldhideonphone) attribute at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[String](#type-string) | false | — | field or field name to update |
| hideOnPhone | [Boolean](#type-boolean) | false | — | new setting for hideOnPhone property |

---
## Method: ListGrid.displayHeaderContextMenu

### Description
If [ListGrid.showHeaderContextMenu](ListGrid_1.md#attr-listgridshowheadercontextmenu) is `true` this method is fired when the user right-clicks on the header for this grid.  
Default implementation will display a menu with entries derived from [ListGrid.getHeaderContextMenuItems](#method-listgridgetheadercontextmenuitems) for the appropriate column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas) | false | — | which button in the header received the right-click event (may be the sorter button or header menu button) |
| position | [Array](#type-array) | true | — | Optional 2-element array specifying position at which the menu should be shown. If this is not passed in the menu will be shown at the mouseEvent position (default context menu behavior). |

### Groups

- gridHeader

### See Also

- [ListGrid.showHeaderContextMenu](ListGrid_1.md#attr-listgridshowheadercontextmenu)

---
## Method: ListGrid.fetchRelatedData

### Description
Based on the relationship between the DataSource this component is bound to and the DataSource specified as the "schema" argument, call fetchData() to retrieve records in this grid that are related to the passed-in record.

Relationships between DataSources are declared via [DataSourceField.foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey).

For example, given two related DataSources "orders" and "orderItems", where we want to fetch the "orderItems" that belong to a given "order". "orderItems" should declare a field that is a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) to the "orders" table (for example, it might be named "orderId" with foreignKey="orders.id"). Then, to load the records related to a given "order", call fetchRelatedData() on the component bound to "orderItems", pass the "orders" DataSource as the "schema" and pass a record from the "orders" DataSource as the "record" argument.

Note that multiple foreign keys into the schema are supported by this method.

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
## Method: ListGrid.setEditValues

### Description
This method sets up a set of editValues for some row / cell. It differs from 'setEditValue()' in that:  
 - it takes values for multiple fields  
 - it clears out any previous edit values for the record

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | Row number for the record being edited |
| values | [Object](../reference.md#type-object) | false | — | New values for the row |

---
## Method: ListGrid.transferSelectedData

### Description
Simulates a drag / drop type transfer of the selected records in some other component to this component, without requiring any user interaction. This method acts on the dropped records exactly as if they had been dropped in an actual drag / drop interaction, including any special databound behavior invoked by calling [getDropValues](DataBoundComponent.md#method-databoundcomponentgetdropvalues) for each dropped record.

To transfer **all** data in, for example, a [ListGrid](ListGrid_1.md#class-listgrid), call [ListGrid.selectAllRecords](#method-listgridselectallrecords) first.

Note that drag/drop type transfers of records between components are asynchronous operations: SmartClient may need to perform server turnarounds to establish whether dropped records already exist in the target component. Therefore, it is possible to issue a call to transferSelectedData() and/or the [drop()](#method-listgriddrop) method of a databound component whilst a transfer is still active. When this happens, SmartClient adds the second and subsequent transfer requests to a queue and runs them one after the other. If you want to be notified when a transfer process has actually completed, either provide a callback to this method or implement [DataBoundComponent.dropComplete](DataBoundComponent.md#method-databoundcomponentdropcomplete).

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
## Method: ListGrid.cellValueHoverHTML

### Description
Returns the HTML that is displayed by the default cellValueHover handler. Return null or an empty string to cancel the hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |
| defaultHTML | [HTMLString](../reference.md#type-htmlstring) | false | — | the HTML that would have been displayed by default |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover. If null or an empty string, then the hover is canceled.

### Groups

- events

### See Also

- [ListGrid.cellValueHover](#method-listgridcellvaluehover)

---
## Method: ListGrid.getGroupByText

### Description
If we're showing a [headerContextMenu](ListGrid_1.md#attr-listgridshowheadercontextmenu) for this grid and [this.canGroupBy](ListGrid_1.md#attr-listgridcangroupby) is true, this string will be shown as the title for the menu item to toggle the group by setting for a field.  
Default implementation evaluates and returns the dynamic [ListGrid.groupByText](ListGrid_1.md#attr-listgridgroupbytext) string.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field to get the menu item title for |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — Title to show in the menu item

### Groups

- i18nMessages

---
## Method: ListGrid.getFilterWindowCriteria

### Description
Returns the current [ListGrid.filterWindowCriteria](ListGrid_1.md#attr-listgridfilterwindowcriteria).

### Returns

`[Criteria](../reference_2.md#type-criteria)` — a copy of the current filter window criteria

---
## Method: ListGrid.keyPress

### Description
Handle a keyPress event on the ListGrid as a whole.

Note that the majority of keyboard handling for a ListGrid is performed by [ListGrid.bodyKeyPress](#method-listgridbodykeypress) and most overrides are better performed there.

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel

---
## Method: ListGrid.editComplete

### Description
Callback fired when inline edits have been successfully saved.

No default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | current index of the row that was saved |
| colNum | [number](#type-number) | false | — | index of the column that was saved, if applicable |
| newValues | [Object](../reference.md#type-object)|[Record](#type-record) | false | — | new values that were saved |
| oldValues | [Record](#type-record) | false | — | the complete original values from before the save occurred |
| editCompletionEvent | [EditCompletionEvent](../reference.md#type-editcompletionevent) | false | — | Event that led to the save |
| dsResponse | [DSResponse](#type-dsresponse) | true | — | for DataSource saves, DSResponse object returned |

### Groups

- editing

---
## Method: ListGrid.getHeaderAriaRole

### Description
Returns the [role](Canvas.md#attr-canvasariarole) for this listGrid's [header](ListGrid_1.md#attr-listgridshowheader).

If [ListGrid.headerAriaRole](ListGrid_1.md#attr-listgridheaderariarole) is explicitly provided, it will be used.  
Otherwise default implementation returns `"row"` if [ListGrid.ariaRole](ListGrid_1.md#attr-listgridariarole) is set to `"grid"`

### Returns

`[String](#type-string)` — role for the header

**Flags**: A

---
## Method: ListGrid.getCellStartRow

### Description
When using [row spanning](#method-listgridgetrowspan), returns the row number where a row-spanning cell starts.

For example, if row 2 col 0 spans 3 cells, `getCellStartRow()` for row 2 col 0, row 3 col 0, row 4 col 0 will all return 2, because that's the row when spanning starts.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row number of cell for which the start row should be returned |
| colNum | [int](../reference.md#type-int) | false | — | column number of cell for which the start row should be returned |

### Returns

`[int](../reference.md#type-int)` — row number where spanning starts

---
## Method: ListGrid.formatCellValue

### Description
Formatter to apply to values displayed within cells.

The value passed to this method is either the field value found in the cell record or, if there are unsaved edits, the current user-entered value for the cell. **NOTE:** unsaved user edits may contain nulls, bad values or values of the wrong type, so formatters used for editable data should be bulletproof. For example, if you have a function "myNumberFormatter" that should only be passed actual Numbers, you might define formatCellValue like so:

```
     isc.isA.Number(parseInt(value)) ?
            myNumberFormatter(parseInt(value)) : value
 
```
Note that this formatter will not be applied to the value displayed within editors for cells - use `formatEditorValue` to achieve this.

If `formatCellValue` is defined at the field level for some cell being edited, the field level method will be used to format the edit value and this method will not be called for that cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value for the cell being |
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object for the cell. Note: If this is a new row that has not been saved, in an editable grid, it has no associated record object. In this case the edit values will be passed in as this parameter. |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number for the cell. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — formatted value to display in the cell.

### Groups

- display_values

### See Also

- [ListGridField.formatCellValue](ListGridField.md#method-listgridfieldformatcellvalue)
- [ListGrid.formatEditorValue](#method-listgridformateditorvalue)

---
## Method: ListGrid.setAutoFitMaxHeight

### Description
Setter for [ListGrid.autoFitMaxHeight](ListGrid_1.md#attr-listgridautofitmaxheight).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Integer](../reference_2.md#type-integer) | false | — | Maximum height in px we'll expand to accommodate if [auto fit](ListGrid_1.md#attr-listgridautofitdata) is enabled vertically. |

### Groups

- autoFitData

---
## Method: ListGrid.rowOut

### Description
Called when the mouse pointer leaves a row

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.setAutoFitExtraRecords

### Description
Setter for [ListGrid.autoFitExtraRecords](ListGrid_1.md#attr-listgridautofitextrarecords).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| extraRecords | [Integer](../reference_2.md#type-integer) | false | — | Number of extra rows beyond the data-size we'll expand to accommodate if [auto fit](ListGrid_1.md#attr-listgridautofitdata) is enabled vertically. |

### Groups

- autoFitData

---
## Method: ListGrid.setCanResizeFields

### Description
Setter method for updating [ListGrid.canResizeFields](ListGrid_1.md#attr-listgridcanresizefields) at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canResize | [boolean](../reference.md#type-boolean) | false | — | new value for this.canResizeFields |

---
## Method: ListGrid.setCanFreezeFields

### Description
Setter method for [ListGrid.canFreezeFields](ListGrid_1.md#attr-listgridcanfreezefields)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canFreeze | [boolean](../reference.md#type-boolean) | false | — | New value for `listGrid.canFreezeFields` |

---
## Method: ListGrid.chartRow

### Description
Chart a single row of data, with each cell value labeled by the column header.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Number](#type-number) | false | — | row to chart |
| dataFields | [Array of String](#type-array-of-string) | true | — | optional list of fields to use as labels. By default, all fields are used. |
| chartProperties | [Chart Properties](#type-chart-properties) | true | — | properties to pass to the created chart |

### Returns

`[Chart](#type-chart)` — created Chart instance

---
## Method: ListGrid.getRowPageTop

### Description
Returns the Y-coordinate for a given row number as a page-relative coordinate. See [ListGrid.getRowTop](#method-listgridgetrowtop).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | — |

### Returns

`[int](../reference.md#type-int)` — Y-coordinate

### Groups

- positioning

---
## Method: ListGrid.setHeaderSpanTitleStyle

### Description
Update the [HeaderSpan.headerTitleStyle](HeaderSpan.md#attr-headerspanheadertitlestyle) for a span within the grid at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | name of the headerSpan, as specified via [HeaderSpan.name](HeaderSpan.md#attr-headerspanname). |
| newTitle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new titleStyle for the headerSpan |

---
## Method: ListGrid.getEventRow

### Description
Returns the row number of the provided Y-coordinate, or the most recent mouse event if a Y-coordinate is not provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| y | [Integer](../reference_2.md#type-integer) | true | — | Y-coordinate relative to the top edge of the content to obtain the row number for. If not provided, then [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety) will be used. |

### Returns

`[int](../reference.md#type-int)` — row number, or -2 if beyond last drawn row

### Groups

- events

---
## Method: ListGrid.setMinFieldWidth

### Description
Updates [ListGrid.minFieldWidth](ListGrid_1.md#attr-listgridminfieldwidth) and redraws any columns as needed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [int](../reference.md#type-int) | false | — | — |

### See Also

- [ListGrid.minFieldWidth](ListGrid_1.md#attr-listgridminfieldwidth)

---
## Method: ListGrid.saveEdits

### Description
Validates and saves edits within the row currently being edited (or another row with unsaved edits, if indicated).

This method can be called to manually trigger saves if the default mechanisms of [cell by cell](ListGrid_1.md#attr-listgridsavebycell) or row by row saving are not suitable.

The 'callback' parameter provides a notification when the save attempt completes, which is likely to be asynchronous for databound grids. Cases under which the callback will fire are:

*   Save completed successfully
*   No changes to the edited row, so save not required
*   Validation failure occurred on the client or on the server

Note that if this method was unable to determine the row to be saved, the callback will NOT fire - in this case, the method is a no-op.

Other, standard callbacks such as [ListGrid.editComplete](#method-listgrideditcomplete), [ListGrid.editFailed](ListGrid_1.md#method-listgrideditfailed) and [ListGrid.cellChanged](#method-listgridcellchanged) will fire normally.

Note this method does not hide the inline editors if they are showing - to explicitly save and end editing, use the method 'endEditing()'

If this method is called for a row which has been marked for deletion (see [ListGrid.markRecordRemoved](#method-listgridmarkrecordremoved)) it will cause the record to be removed from the data-set.

For more information on editing, see the [editing overview](../kb_topics/editing.md#kb-topic-grid-editing).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editCompletionEvent | [EditCompletionEvent](../reference.md#type-editcompletionevent) | true | — | Event used to complete cell editing. Optional, and defaults to `"programmatic"`. Can be used by the `callback` method to perform custom actions such as navigation when the save completes. |
| callback | [Callback](../reference.md#type-callback) | true | — | Callback to fire on completion of the saving process. If no edits were made or client-side validation fails the callback will be fired synchronously at the end of this method.  
Takes the following parameters:  
\- rowNum _(Number) edited row number_  
\- colNum _(Number) edited column number_  
\- editCompletionEvent _(EditCompletionEvent) event passed in (defaults to `"programmatic"`)_  
\- success _(boolean) false if the save was unable to complete due to a validation failure or server-side error._ |
| rowNum | [number](#type-number) | true | — | Which row should be saved. If unspecified the current edit row is saved by default. Note that if there is no current edit row this method will no op. |

### Groups

- editing

### See Also

- [ListGrid.endEditing](#method-listgridendediting)

**Flags**: A

---
## Method: ListGrid.rowContextClick

### Description
Called when a row receives a contextclick event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.getSelectedCellData

### Description
Returns the selected cells as a series of Records where each field value is stored under it's offset from the top-left of the selection. For example, a 2x2 cell selection starting from the first column would return two Records, each with two values stored under the names "0" and "1".

If [ListGrid.canSelectCells](ListGrid_1.md#attr-listgridcanselectcells) is not enabled, this API always returns null.

### Returns

`[RecordList](#type-recordlist)` — list of Records as described above

---
## Method: ListGrid.editExistingRecord

### Description
Start inline editing at a record identified by criteria. If the criteria matches more than one record, the first matched record is edited. Additionally, if the record to be edited is not visible, the record will be scrolled into view.

Note that the record to be matched must already be loaded in the grid - no fetch will be performed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | Criteria identifying the existing row to edit |

### Groups

- editing

### See Also

- [ListGrid.startEditing](#method-listgridstartediting)

**Flags**: A

---
## Method: ListGrid.headerClick

### Description
Handle a click in the list header.

By default, calls [ListGrid.sort](#method-listgridsort) to sort by the field that was clicked, if [sorting is enabled](ListGrid_1.md#attr-listgridcansort), and calls [ListGrid.autoFitField](#method-listgridautofitfield) if [ListGrid.canAutoFitFields](ListGrid_1.md#attr-listgridcanautofitfields) is true and [ListGrid.headerAutoFitEvent](ListGrid_1.md#attr-listgridheaderautofitevent) is set to `"click"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [number](#type-number) | false | — | field number for the header that was clicked |

### Groups

- sorting
- events
- gridHeader

**Flags**: A

---
## Method: ListGrid.applyRecordData

### Description
Applies a list of Records as changes to the current selection.

Values found in each of the passed records will be applied to the same-named fields in the Records starting from the top-left of the current selection, in order.

Will only modify cells in the grid which are editable, and changes will be applied as editValues, exactly as though the user had typed the values in (see [Grid Editing Overview](../kb_topics/editing.md#kb-topic-grid-editing)).

See also [ListGrid.applyCellData](#method-listgridapplycelldata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recordData | [RecordList](#type-recordlist) | false | — | list of Records as described above |

---
## Method: ListGrid.clearCriteria

### Description
Clear the current criteria used to filter data. This method clears filter-values from fields in the [ListGrid.filterEditor](ListGrid_1.md#attr-listgridfiltereditor) but will not change their current [operator](ListGridField.md#attr-listgridfieldfilteroperator) or clear associated [operator-icons](ListGrid_1.md#attr-listgridallowfilteroperators). See [ListGrid.clearAllCriteria](#method-listgridclearallcriteria) for a means of doing that.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.fetchData](#method-listgridfetchdata)

---
## Method: ListGrid.fieldIsEditable

### Description
Can the field be edited? This method looks at [ListGrid.canEdit](ListGrid_1.md#attr-listgridcanedit) for the grid as well as the [ListGridField.canEdit](ListGridField.md#attr-listgridfieldcanedit) value, to determine whether editing is allowed. This method's return value is not authoritative for editibility since [ListGrid.canEditCell](#method-listgridcaneditcell) could return a more specific value.

For a detailed discussion, see the documentation at [ListGrid.canEdit](ListGrid_1.md#attr-listgridcanedit).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[number](#type-number)|[FieldName](../reference.md#type-fieldname) | false | — | field object, number, or name |

### Returns

`[boolean](../reference.md#type-boolean)` — whether field can be edited

### Groups

- editing

---
## Method: ListGrid.setFrozenFieldsMaxWidth

### Description
Setter for the [ListGrid.frozenFieldsMaxWidth](ListGrid_1.md#attr-listgridfrozenfieldsmaxwidth) attribute

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [String](#type-string)|[Integer](../reference_2.md#type-integer) | false | — | new maximum width for frozen fields |

---
## Method: ListGrid.canSelectCell

### Description
If [ListGrid.canSelectCells](ListGrid_1.md#attr-listgridcanselectcells) is set to `true` then, whenever an end-user or programmatic cell-selection is attempted, this method is called for each cell in the selection. If it returns false, the cell will not be selected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | rowNum being selected |
| colNum | [int](../reference.md#type-int) | false | — | colNum being selected |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to disallow selection

**Flags**: A

---
## Method: ListGrid.getHeaderButtonAriaState

### Description
Returns a map of [WAI ARIA state attribute values](Canvas.md#attr-canvasariastate) to be written into header buttons for this grid.

Default implementation returns an object with combined properties from any specified [header button aria state default object](ListGrid_1.md#attr-listgridheaderbuttonariastate), overlaid with any [ListGridField.headerButtonAriaState](ListGridField.md#attr-listgridfieldheaderbuttonariastate) properties specified on the field itself, plus the following attributes:

*   `haspopup` - true if the button should show the header context menu
*   `colindex` - index of the column if [ListGrid.ariaRole](ListGrid_1.md#attr-listgridariarole) is `"grid"`
*   `sort` - "ascending", "descending" or "none" depending on the sort-state of the field

Also, if an explicit property is set in ariaState, it will be respected and will take precedence over the calculated property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| button | [Button](#type-button) | false | — | The live ListGrid column header button. Note that the `"name"` attribute of the button will be set to the field name for the column. |

### Returns

`[Object](../reference.md#type-object)` — Object containing aria property names and values to write into the button's handle

### Groups

- accessibility

**Flags**: A

---
## Method: ListGrid.chartData

### Description
Chart the data in this listGrid as a multi-series chart.

Each row provides a series of data. Each series of data is labeled by a value from one column, called the `labelField`.

For example, cell values are sales figures, and fields are "Product", "August", "September", "October". In this case each row gives a series: sales figures for each of 3 months. The `labelField` in this case is the "Product" field, meaning each row represents sales figures for each of 3 months for a particular product. This dataset can be charted via any multi-series chart: stacked or clustered bar or column chart, line chart with multiple lines, or area chart (stacked lines).

By default, all visible fields other than the label field are assumed to be labels for series values, but an explicit list of fields can be provided as `dataFields`.

By default, all data is charted if all data is loaded, otherwise, data visible in the viewport is charted. An explicit set of rows can be provided via `dataRows`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| labelField | [String](#type-string) | false | — | name of the field |
| dataFields | [Array of String](#type-array-of-string) | true | — | optional list of fields to use as labels. By default, all fields are used. |
| dataRows | [Array of ListGridRecord](#type-array-of-listgridrecord) | true | — | set of records to chart. Can be obtained by eg [grid.data.getRange()](ResultSet.md#method-resultsetgetrange). |
| chartProperties | [FacetChart Properties](#type-facetchart-properties) | true | — | properties to pass to the created chart |
| labelFieldFirst | [boolean](../reference.md#type-boolean) | true | — | if true, use the labelField as the "first" set of labels, for example, as the bar labels in a stacked bar chart, whereas the second set of labels would appear as the legend. |

### Returns

`[FacetChart](#type-facetchart)` — created Chart instance

---
## Method: ListGrid.setUserSummary

### Description
Updates the [userSummary](ListGridField.md#attr-listgridfieldusersummary) of the specified field. This method is preferred over setting the 'userSummary' property of the field directly because it also updates any component dependencies and recomputes the field. If the summary is not passed or is `undefined`, it is assumed that the summary has already been updated and only the dependency propagation logic will run.

Known component dependencies are:

*   the cached record values of the summary for this field
*   any generated field that references the field's computed summaries

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[String](#type-string) | false | — | field owning the summary |
| userSummary | [UserSummary](#type-usersummary) | true | — | optional summary to install |

### See Also

- [ListGridField.userSummary](ListGridField.md#attr-listgridfieldusersummary)

---
## Method: ListGrid.getAllEditRows

### Description
Returns an array of every rowNum for which we have pending (unsubmitted) edits. This will return records that have been marked as removed (see [ListGrid.markRecordRemoved](#method-listgridmarkrecordremoved) as well as records with unsaved changes to field values.

### Returns

`[Array of int](#type-array-of-int)` — Array of rowNums for rows with edit values pending submission.

### Groups

- editing

---
## Method: ListGrid.isExpanded

### Description
Whether a given [record](../reference_2.md#object-listgridrecord) is expanded or collapsed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record in question |

### Returns

`[Boolean](#type-boolean)` — true if the node is expanded

### Groups

- expansionField

---
## Method: ListGrid.scrollToColumn

### Description
Scroll the grid to specified column such that the row appears near the center of the viewport.

See [ListGrid.scrollToCell](#method-listgridscrolltocell) for a full description of how this method interacts with incremental loading and rendering of data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [number](#type-number) | false | — | Index of the column to scroll into view |
| xPosition | [Alignment](../reference_2.md#type-alignment) | true | — | Horizontal position of scrolled column (optional) |

### Groups

- scrolling

---
## Method: ListGrid.groupBy

### Description
Display the current set of records grouped by their values for the given field or fields. With no arguments, disables all grouping.

Grouping transforms the current dataset into a Tree on the fly, then provides a familiar tree interface for exploring the grouped data. Note that for performance reasons grouping is only available for dataSets with less than [ListGrid.groupByMaxRecords](ListGrid_1.md#attr-listgridgroupbymaxrecords) entries.

Grouping works automatically with any dataset, providing simple default grouping based on each field's declared type - see [SimpleType.groupingModes](SimpleType.md#attr-simpletypegroupingmodes) for more information. Additionally, you can use [field.getGroupValue()](ListGridField.md#method-listgridfieldgetgroupvalue) to control how records are grouped, and [field.getGroupTitle()](ListGridField.md#method-listgridfieldgetgrouptitle) to control how groups are titled. You can affect multiple fields of the same data-type via the same-named APIs on an appropriate custom [SimpleType](SimpleType.md#method-simpletypegetgroupvalue).

Grouping can be performed programmatically via this API, or you can set [grid.canGroupBy:true](ListGrid_1.md#attr-listgridcangroupby) to enable menus that allow the user to perform grouping. To group a grid automatically, instantiate the grid with a [ListGrid.groupByField](ListGrid_1.md#attr-listgridgroupbyfield) setting. To take action when an end use requests grouping, see [ListGrid.handleGroupBy](#method-listgridhandlegroupby).

While grouped, the automatically created Tree is available as [grid.groupTree](ListGrid_1.md#attr-listgridgrouptree) and the original dataset is available as [grid.originalData](ListGrid_1.md#attr-listgridoriginaldata).

#### Data Requirements

Before grouping can be performed, all records that match current [criteria](#method-listgridfetchdata) must be loaded. If [data paging](ListGrid_1.md#attr-listgriddatafetchmode) is in use, not all matching records are cached, and the [total rows available from the server](ResultSet.md#method-resultsetgetlength) is less than [ListGrid.groupByMaxRecords](ListGrid_1.md#attr-listgridgroupbymaxrecords), the grid will automatically request all unloaded records from the server, then perform grouping once they arrive.

If the total number of rows available from the server exceeds [ListGrid.groupByMaxRecords](ListGrid_1.md#attr-listgridgroupbymaxrecords), calling `groupBy` will have no effect, and menu items for grouping will appear disabled.

#### Grouping Notification

Grouping is often an asynchronous operation, both because of automatic loading of remaining rows, and because asynchronous processing is required to work around bugs in some browsers related to misdetection of "hung" scripts (see [ListGrid.groupByAsyncThreshold](ListGrid_1.md#attr-listgridgroupbyasyncthreshold)). Define a [ListGrid.handleGroupBy](#method-listgridhandlegroupby) method to be called when grouping is about to start (potentially canceling it), and define a [ListGrid.groupByComplete](#method-listgridgroupbycomplete) method to be notified when it's done.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Array of String](#type-array-of-string) | true | — | name of fields to group by |

### Groups

- grouping

---
## Method: ListGrid.getEditRow

### Description
Returns the index of the row being edited or null if there is no current edit row.

### Returns

`[int](../reference.md#type-int)` — index of the current edit row

### Groups

- editing

---
## Method: ListGrid.getRollUnderCanvas

### Description
This method is called to retrieve the [ListGrid.rollUnderCanvas](ListGrid_1.md#attr-listgridrollundercanvas) when the user moves over a new row or cell if [showing a rollUnder canvas](ListGrid_1.md#attr-listgridshowrollundercanvas) or showing a [rollUnder canvas for the selected record](ListGrid_1.md#attr-listgridshowselectedrollundercanvas).

The default implementation uses the [AutoChild](../reference.md#type-autochild) subystem to create the [ListGrid.rollUnderCanvas](ListGrid_1.md#attr-listgridrollundercanvas) auto child. It may be overridden for custom behavior.

Note that for efficiency this should not typically create a new Canvas every time that it is called. Instead usually a single rollOver canvas should be created and updated to reflect the current rollOver row if necessary.

Return null to avoid showing a `rollUnderCanvas` for this row.

See also [ListGrid.getFrozenRollUnderCanvas](#method-listgridgetfrozenrollundercanvas).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | index of the current rollOver row. |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | index of the current rollOver column. This parameter will be null unless [useCellRollOvers](ListGrid_1.md#attr-listgridusecellrollovers) is true for the grid. |

### Returns

`[Canvas](#type-canvas)` — the embedded component

### Groups

- hoverComponents

---
## Method: ListGrid.setFieldProperties

### Description
Dynamically set properties for a particular field. This method will update the fields header-button without having to explicitly reset the fields in the grid.

NOTE: Where explicit setters exist for field properties (such as [ListGrid.resizeField](#method-listgridresizefield), [ListGrid.setFieldTitle](#method-listgridsetfieldtitle), [ListGrid.setFieldIcon](#method-listgridsetfieldicon), etc.) these should be used instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [number](#type-number)|[String](#type-string) | false | — | name of the field, or index. |
| properties | [ListGridField Properties](#type-listgridfield-properties) | false | — | properties to apply to the header |

---
## Method: ListGrid.getFieldSearchOperator

### Description
Returns the current search-operator applied to criteria for a given field in this grid's [filter row](ListGrid_1.md#attr-listgridfiltereditor). Typically, this will be the operator most recently selected by the user, or applied by a call to [ListGrid.setCriteria](#method-listgridsetcriteria) or similar..

If no operator has been applied by the user, the result is the default provided [by the developer](ListGridField.md#attr-listgridfieldfilteroperator), or null, indicating a default operator according to data-type.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | name of the field to get the search operator for |

---
## Method: ListGrid.filterData

### Description
Retrieves data that matches the provided criteria and displays the matching data in this component.

This method behaves exactly like [ListGrid.fetchData](#method-listgridfetchdata) except that [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) is automatically set to "substring" so that String-valued fields are matched by case-insensitive substring comparison.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | Search criteria. If a [DynamicForm](DynamicForm.md#class-dynamicform) is passed in as this argument instead of a raw criteria object, will be derived by calling [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke when a fetch is complete. Fires only if server contact was required; see [fetchData()](#method-listgridfetchdata) for details |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | for databound components only - optional additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [DataBoundComponent.willFetchData](DataBoundComponent.md#method-databoundcomponentwillfetchdata)

---
## Method: ListGrid.getRecord

### Description
Return the pointer to a particular record by record number. Synonym for [ListGrid.getCellRecord](#method-listgridgetcellrecord).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recordNum | [number](#type-number) | false | — | row index of record to return. |

### Returns

`[ListGridRecord](#type-listgridrecord)` — Record object for the row.

### See Also

- [ListGrid.getCellRecord](#method-listgridgetcellrecord)
- [ListGrid.getEditedRecord](#method-listgridgeteditedrecord)

**Flags**: A

---
## Method: ListGrid.cellHoverHTML

### Description
StringMethod to dynamically assemble an HTML string to show in a hover window over the appropriate cell/record when this.canHover and this.showHover are both true. Called when the mouse hovers over a cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the html to be shown inside the hover for this cell

### Groups

- events

### See Also

- [ListGrid.canHover](ListGrid_1.md#attr-listgridcanhover)
- [ListGrid.showHover](ListGrid_1.md#attr-listgridshowhover)

---
## Method: ListGrid.setSelectionType

### Description
Changes selectionType on the fly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectionType | [SelectionStyle](../reference.md#type-selectionstyle) | false | — | New selection style. |

**Flags**: A

---
## Method: ListGrid.setSortByGroupFirst

### Description
—

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortByGroupFirst | [Boolean](#type-boolean) | false | — | — |

**Flags**: A

---
## Method: ListGrid.cellOut

### Description
Called when the mouse pointer leaves a cell

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.resort

### Description
If a list has become unsorted due to data modification or a call to [ListGrid.unsort](#method-listgridunsort), this method will resort the list by the previous [sort-specifier](#method-listgridsetsort) array, if there is one, or by the previous sort-field and -direction.

### Groups

- sorting

---
## Method: ListGrid.getRowHeight

### Description
Return the height this row should be. Default is this.cellHeight. If [ListGrid.fixedRecordHeights](ListGrid_1.md#attr-listgridfixedrecordheights) is false, the row may be rendered taller than this specified size.

If records will be variable height, you should switch on [virtualScrolling](ListGrid_1.md#attr-listgridvirtualscrolling).

Note if [row spanning](ListGrid_1.md#attr-listgridallowrowspanning) is enabled, this method should return the height of a single row (with rowSpan set to 1).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number |

### Returns

`[number](#type-number)` — height in pixels

---
## Method: ListGrid.isSummaryRecord

### Description
Returns whether the supplied record is a group or grid summary record. Useful in conjunction with [ListGrid.getGroupMembers](#method-listgridgetgroupmembers) for determining which records are group summary records.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object such as from [ListGrid.getGroupMembers](#method-listgridgetgroupmembers) |

### Returns

`[boolean](../reference.md#type-boolean)` — whether record is summary

---
## Method: ListGrid.getCellHoverComponent

### Description
When [ListGrid.showHoverComponents](ListGrid_1.md#attr-listgridshowhovercomponents) is set, this method is called to get the component to show as a hover for the current cell.

By default, this method returns one of a set of builtin components, according to the value of [listGrid.hoverMode](../reference.md#type-hovermode). You can override this method to return any component you wish to provide as a hoverComponent, or invoke the superclass method to have the default hover component generated, then further customize it.

By default, components returned by `getCellHoverComponent()` will be automatically destroyed when the hover is hidden. To prevent this, set [Canvas.hoverAutoDestroy](Canvas.md#attr-canvashoverautodestroy) to false on the returned component.

If you return a component that fetches data or loads content dynamically:

1.  set rpcRequest.promptStyle to "cursor" or set rpcRequest.showPrompt to false on any network requests, or the default masking that blocks the screen during network requests will dismiss the hover
2.  as covered above, your component may have been automatically destroyed by the time your content has been loaded. Check [Canvas.destroyed](Canvas.md#attr-canvasdestroyed) before taking action in an asynchronous callback
3.  if your component grows in size after data is loaded, and it would then be rendered partially off-screen, it will be automatically re-positioned to keep it on-screen. However this will not automatically happen in cases where you provide HTML content that changes size after initial render, in which case a call to [Canvas.adjustForContent](Canvas.md#method-canvasadjustforcontent) will be required. See that API for details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | record to get the hoverComponent for |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | row number for the cell |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | column number of the cell |

### Returns

`[Canvas](#type-canvas)|[Canvas Properties](#type-canvas-properties)` — the component to show as a hover

### Groups

- hoverComponents

---
## Method: ListGrid.getHeaderButtonAriaRole

### Description
Returns the [role](Canvas.md#attr-canvasariarole) for this listGrid's [header buttons](ListGrid_1.md#attr-listgridshowheader).

If [ListGridField.headerButtonAriaRole](ListGridField.md#attr-listgridfieldheaderbuttonariarole) or [ListGrid.headerButtonAriaRole](ListGrid_1.md#attr-listgridheaderbuttonariarole) is set, it will be used.  
Othewise, the default implementation returns `"columnheader"` if [ListGrid.ariaRole](ListGrid_1.md#attr-listgridariarole) is set to `"grid"`, `"button"` otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | header button field object |

### Returns

`[String](#type-string)` — role for the header button

**Flags**: A

---
## Method: ListGrid.transferDragData

### Description
During a drag-and-drop interaction, this method is called to transfer a set of records that were dropped onto some other component. This method is called after the set of records has been copied to the other component. Whether or not this component's data is modified is determined by the value of [DataBoundComponent.dragDataAction](DataBoundComponent.md#attr-databoundcomponentdragdataaction).

With a `dragDataAction` of "move", a databound component will issue "remove" dsRequests against its DataSource to actually remove the data, via [DataSource.removeData](DataSource.md#method-datasourceremovedata).

### Returns

`[Array](#type-array)` — Array of objects that were dragged out of this ListGrid.

### See Also

- [DataBoundComponent.getDragData](DataBoundComponent.md#method-databoundcomponentgetdragdata)
- [ListGrid.willAcceptDrop](#method-listgridwillacceptdrop)

**Flags**: A

---
## Method: ListGrid.fieldIsVisible

### Description
Check whether a field is currently visible

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [String](#type-string)|[ListGridField](#type-listgridfield) | false | — | field to be checked |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the field is currently visible, false otherwise.

---
## Method: ListGrid.getExportRowBGColor

### Description
When exporting data to Excel/OpenOffice format using [exportData()](#method-listgridexportdata) or [exportClientData()](#method-listgridexportclientdata), background color to use for the given rowNum.

See [exportBGColor](../kb_topics/exportBGColor.md#kb-topic-exports--cell-background-color) for an overview.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row number |
| record | [Record](#type-record) | false | — | the record object behind the row being exported |

### Returns

`[CSSColor](../reference_2.md#type-csscolor)` — background color to use for the row, or null to use the default background color

### Groups

- exportBackgroundColor

---
## Method: ListGrid.getFieldByName

### Description
Given a field name, return the appropriate field definition. Unlike [getField()](#method-listgridgetfield), this method will return the field definition even if it's not visible in the grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | name of the field to retrieve |

### Returns

`[ListGridField](#type-listgridfield)` — field definition

---
## Method: ListGrid.cellValueHover

### Description
Optional stringMethod to fire when the user hovers over a cell and the value is clipped. If this.showClippedValuesOnHover is true, the default behavior is to show a hover canvas containing the HTML returned by cellValueHoverHTML(). Return false to suppress this default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard hover

### Groups

- events

### See Also

- [ListGrid.showClippedValuesOnHover](ListGrid_1.md#attr-listgridshowclippedvaluesonhover)
- [ListGrid.cellValueIsClipped](#method-listgridcellvalueisclipped)
- [ListGrid.cellValueHoverHTML](#method-listgridcellvaluehoverhtml)

**Flags**: A

---
## Method: ListGrid.getGroupState

### Description
Returns a snapshot of the current grouping state of this ListGrid.  
This object can be passed to [ListGrid.setGroupState](#method-listgridsetgroupstate) to reset this grid's grouping to the current state (assuming the same data / fields are present in the grid).

### Returns

`[ListGridGroupState](../reference.md#type-listgridgroupstate)` — current view state for the grid.

### Groups

- viewState

### See Also

- [ListGridGroupState](../reference.md#type-listgridgroupstate)
- [ListGrid.setGroupState](#method-listgridsetgroupstate)

---
## Method: ListGrid.getSortSpecifier

### Description
Returns the [SortSpecifier](../reference_2.md#object-sortspecifier) for the passed fieldName, or null if the field is not sorted.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | The name of a field, visible, hidden or existing only in the dataSource |

### Returns

`[SortSpecifier](#type-sortspecifier)` — for the passed fieldName, or null if the field is not sorted.

**Flags**: A

---
## Method: ListGrid.clearSavedViewState

### Description
Clear this grid's auto-saved [view state](../reference_2.md#type-listgridviewstate) as described in [ListGrid.autoPersistViewState](ListGrid_1.md#attr-listgridautopersistviewstate).

### Groups

- viewState

### See Also

- [ListGrid.autoPersistViewState](ListGrid_1.md#attr-listgridautopersistviewstate)
- [ListGrid.getSavedViewState](#method-listgridgetsavedviewstate)

---
## Method: ListGrid.findNextEditCell

### Description
Method to find the next editable cell given a starting row/col, and a direction, either iterating through fields within each row, or checking the same field in each row.

Note, this is potentially an expensive method. For example, consider a listGrid where the user can add rows but not edit any existing rows; in this case, `canEditCell()` would inspect and reject every row in the dataSet before returning true for the last row. Consider this before making use of this method on grids with large dataSets

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Number](#type-number) | false | — | Index of starting row |
| colNum | [Number](#type-number) | false | — | Index of starting column |
| direction | [Number](#type-number) | false | — | +1 if searching forward for the next edit cell, -1 if searching backwards |
| stepThroughFields | [boolean](../reference.md#type-boolean) | false | — | true if we should check every field in each row - false if we should check the same field in each row. |
| checkStartingCell | [boolean](../reference.md#type-boolean) | true | — | Should we check whether the cell passed in is editable? Default behavior WILL check that cell - pass false to suppress checking that cell. |

### Returns

`[Array](#type-array)` — 2 element array specifying next editable rowNum, colNum, or null if this method fails to find an editable cell.

### Groups

- editing

---
## Method: ListGrid.getAriaStateDefaults

### Description
Retrieves dynamically calculated default [ARIA state mapping](Canvas.md#attr-canvasariastate) properties for this listGrid. These will be combined with explicitly specified aria state as described in [ListGrid.getAriaState](#method-listgridgetariastate).

Overridden by ListGrid to pick up aria-rowcount and aria-colcount.

### Returns

`[Object](../reference.md#type-object)` — dynamically calculated default aria state properties

**Flags**: A

---
## Method: ListGrid.getRecordDropPosition

### Description
Returns the [RecordDropPosition](../reference.md#type-recorddropposition) for some record drop operation. This value is passed to the [ListGrid.recordDrop](#method-listgridrecorddrop) event notification method.

Default implementation determines the position to return based on the specified [ListGrid.recordDropAppearance](ListGrid_1.md#attr-listgridrecorddropappearance) for the grid and the [y-coordinate of the drop event](EventHandler.md#classmethod-eventhandlergety).

### Returns

`[RecordDropPosition](../reference.md#type-recorddropposition)` — record drop position.

---
## Method: ListGrid.setDontAutoDestroyComponent

### Description
If [ListGrid.showRecordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents) is true, by default any created record components are destroyed once they are no longer in use (for example, if the ListGrid as a whole is destroyed). This method may be used to suppress this behavior for some component. Typical usage might call this method as part of [ListGrid.createRecordComponent](#method-listgridcreaterecordcomponent) to suppress this behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| component | [Canvas](#type-canvas) | false | — | component in question. |
| dontAutoDestroy | [boolean](../reference.md#type-boolean) | false | — | If true, the component will not be destroyed automatically when the grid is destroyed |

---
## Method: ListGrid.getDragTrackerTitle

### Description
Return "title" HTML to display as a drag tracker when the user drags some record.  
Default implementation will display the cell value for the title field (see [ListGrid.getTitleField](#method-listgridgettitlefield)) for the record(s) being dragged (including any icons / custom formatting / styling, etc).

Note: Only called if [ListGrid.dragTrackerMode](ListGrid_1.md#attr-listgriddragtrackermode) is set to `"title"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | First selected record being dragged |
| rowNum | [number](#type-number) | false | — | row index of first record being dragged |

### Returns

`[String](#type-string)` — Title for the row. Default implementation looks at the value of the title-field cell for the row.

### Groups

- dragTracker

---
## Method: ListGrid.unfreezeField

### Description
Unfreeze a frozen field, so that it will now scroll along with other fields when horizontal scrolling occurs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[Integer](../reference_2.md#type-integer)|[String](#type-string)|[Array](#type-array) | false | — | field or fields to unfreeze. fields may be specified as ListGridField objects, field names or colNum. |

### Groups

- frozenFields

---
## Method: ListGrid.getCellValue

### Description
Obtains the display value for a specific cell according to the given input parameters.  
To format the value displayed in the cell, make use of the [formatting](#method-listgridformatcellvalue) methods rather than overriding this method directly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Object](../reference.md#type-object) | false | — | the current record object |
| recordNum | [number](#type-number) | false | — | number of the record in the current set of displayed record (e.g. 0 for the first displayed record) |
| fieldNum | [number](#type-number) | false | — | number of the field in the listGrid.fields array |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — display value for this cell

### Groups

- data

### See Also

- [ListGrid.formatCellValue](#method-listgridformatcellvalue)

**Flags**: A

---
## Method: ListGrid.getRowCountRange

### Description
Retrieves the [row count range](ResultSet.md#method-resultsetgetrowcountrange) for listGrids where [progressive loading](DataSource.md#attr-datasourceprogressiveloading) is active and the row count has been specified as a [range](ResultSet.md#method-resultsetgetrowcountstatus).

The returned value will be a two element array, containing the min and max bounds for the row-count. Note that if the row count has not been recorded as a range, the first element in the array will be the [row count](#method-listgridgetrowcount), and the second element will be null.

### Returns

`[Array of Integer](#type-array-of-integer)` — minimum and maximum bounds for the row count

### Groups

- rowRangeDisplay

---
## Method: ListGrid.getRowTop

### Description
Returns the top coordinate for a given row number, relative to the top of body content. Use [ListGrid.getRowPageTop](#method-listgridgetrowpagetop) for a page-relative coordinate.

This method is reliable only for rows that are currently drawn, which is generally only rows that are visible in the viewport. If row heights vary (see `fixedRowHeights`), coordinates for rows that are not currently shown are rough approximations.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | — |

### Returns

`[int](../reference.md#type-int)` — Y-coordinate

### Groups

- positioning

---
## Method: ListGrid.exportData

### Description
Sends the current filter criteria and sort direction to the server, then exports data in the requested [exportFormat](DSRequest.md#attr-dsrequestexportas).

A variety of DSRequest settings, such as [exportAs](DSRequest.md#attr-dsrequestexportas) and [DSRequest.exportFilename](DSRequest.md#attr-dsrequestexportfilename), affect the exporting process: see [exportResults](DSRequest.md#attr-dsrequestexportresults) for further detail.

Note that data exported via this method skips client-side fields defined only in the component, excludes any client-side formatting and relies on both the SmartClient server and server-side DataSources. To export client-data including client-only fields and with client-side formatting applied, see [exportClientData](#method-listgridexportclientdata), which still requires the SmartClient server but does not rely on server-side DataSource definitions (.ds.xml files).

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
## Method: ListGrid.setAutoFitMaxColumns

### Description
Setter for [ListGrid.autoFitMaxColumns](ListGrid_1.md#attr-listgridautofitmaxcolumns).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| maxColumns | [int](../reference.md#type-int) | false | — | Maximum number of fields we'll expand to accommodate if [auto fit](ListGrid_1.md#attr-listgridautofitdata) is enabled horizontally. |

### Groups

- autoFitData

---
## Method: ListGrid.cellHover

### Description
Called when the mouse hovers over a cell if `this.canHover` is `true`. Returning `false` will suppress the hover text from being shown if `showHover` is `true` for `this` or the field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

### See Also

- [ListGrid.canHover](ListGrid_1.md#attr-listgridcanhover)

---
## Method: ListGrid.recalculateGridSummary

### Description
Refresh the [grid summary](ListGrid_1.md#attr-listgridshowgridsummary), by either re-calculating from already-loaded data or doing a new fetch from the [ListGrid.summaryRowDataSource](ListGrid_1.md#attr-listgridsummaryrowdatasource).

Note unlike [ListGrid.recalculateSummaries](#method-listgridrecalculatesummaries), this method will not force a refresh of field-level summaries (see [ListGridField.recordSummaryFunction](ListGridField.md#attr-listgridfieldrecordsummaryfunction)) or group level summaries (see [ListGrid.showGroupSummary](ListGrid_1.md#attr-listgridshowgroupsummary)).

---
## Method: ListGrid.userSelectAllRecords

### Description
Selects every user-selectable record in the grid. Unlike [ListGrid.selectAllRecords](#method-listgridselectallrecords), if a record is [unselectable](#method-listgridcanselectrecord), this method will not attempt to select it.

---
## Method: ListGrid.autoFitFields

### Description
Perform a one-time horizontal auto-fit of the fields passed. Fields will be sized to match their contents or title (as specified in [ListGrid.autoFitWidthApproach](ListGrid_1.md#attr-listgridautofitwidthapproach)) Does not establish permanent auto-fitting - use [ListGrid.setAutoFitWidth](#method-listgridsetautofitwidth) to do so.

Note that unlike the ongoing autoFit set up by [ListGrid.autoFitFieldWidths](ListGrid_1.md#attr-listgridautofitfieldwidths) or [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth), any specified [ListGridField.width](ListGridField.md#attr-listgridfieldwidth) will not be taken as a minimum width - the field(s) may shrink below the current specified width when this method is run. However, [ListGridField.minWidth](ListGridField.md#attr-listgridfieldminwidth) will be respected.

For information about auto-fitting specific fields, see [ListGridField.autoFit](ListGridField.md#attr-listgridfieldautofit).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fields | [Array of ListGridField](#type-array-of-listgridfield) | true | — | Array of fields to auto fit. If this parameter is not passed, autoFitting will occur on all visible fields. |

### Groups

- autoFitFields

---
## Method: ListGrid.setFilterEditorCriteria

### Description
If [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) is true, this method will update the criteria shown in the `filterEditor` without performing a filter.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria) | false | — | New criteria to show |

---
## Method: ListGrid.getGroupTreeSelection

### Description
If this grid [is grouped](ListGrid_1.md#attr-listgridisgrouped), this method will return the current selection. Unlike the standard [getSelection method](#method-listgridgetselection), this method will return [group nodes](#method-listgridisgroupnode) in addition to standard [ListGridRecord](../reference_2.md#object-listgridrecord)s within the grid's data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| excludePartialSelection | [boolean](../reference.md#type-boolean) | true | — | By default a group header node is considered selected if any members of the group are selected. If this flag is passed in, only header nodes where **all** members of the group are selected will be included in the returned results. |
| groupNodesOnly | [boolean](../reference.md#type-boolean) | true | — | If this parameter is passed as `true`, this method will return just the group header nodes from the group tree. If omitted or false, both header nodes and data records will be returned. |

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — Selected group header nodes and record data objects. If this grid is not grouped, standard [listGrid selection](#method-listgridgetselection) will be returned.

---
## Method: ListGrid.discardEdits

### Description
Cancel outstanding edits for the specified rows, discarding edit values, and hiding editors if appropriate.

Note that if this method is called on a new edit row (created via [ListGrid.startEditingNew](#method-listgridstarteditingnew) for example), which has not yet been saved, this method will remove the row entirely.

Also note that this method will clear the [removed](#method-listgridmarkrecordremoved) state of records that have been marked as removed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | Row to cancel |
| colNum | [int](../reference.md#type-int) | false | — | Column to cancel. Note that this parameter is ignored in ListGrids but may be required in subclasses of ListGrid where each cell represents one record in the data set (EG CubeGrid) |
| dontHideEditor | [Boolean](#type-boolean) | true | — | By default this method will hide the editor if it is currently showing for the row in question. Passing in this parameter will leave the editor visible (and just reset the edit values underneath the editor). |

### Groups

- editing

**Flags**: A

---
## Method: ListGrid.setSelectedState

### Description
Reset this grid's selection to match the [ListGridSelectedState](../reference_2.md#type-listgridselectedstate) object passed in.  
Used to restore previous state retrieved from the grid by a call to [ListGrid.getSelectedState](#method-listgridgetselectedstate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectedState | [ListGridSelectedState](../reference_2.md#type-listgridselectedstate) | false | — | Object describing the desired selection state of the grid |

### Groups

- viewState

### See Also

- [ListGrid.getSelectedState](#method-listgridgetselectedstate)

---
## Method: ListGrid.getSummaryFieldValue

### Description
Get the computed value of a [summary field](ListGrid_1.md#attr-listgridcanaddsummaryfields).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field that has a summary format |
| record | [Record](#type-record) | false | — | record to use to compute formula value |

### Returns

`[String](#type-string)` — formula result

---
## Method: ListGrid.toggleFrozen

### Description
Freeze or unfreeze the indicated field according to whether it is currently frozen.

Called when the ListGrid freezes or unfreezes fields by user action.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[Integer](../reference_2.md#type-integer)|[String](#type-string)|[Array](#type-array) | false | — | field or fields to freeze. fields may be specified as ListGridField objects, field names or colNum. |

### Groups

- frozenFields

---
## Method: ListGrid.getCurrentFieldWidths

### Description
Returns an array of widths of the visible fields in this `ListGrid`, in px. This method is implemented by calling [getFieldWidth()](#method-listgridgetfieldwidth) for each field. If field widths cannot be determined, the returned array will contain nulls.

### Returns

`[Array of Integer](#type-array-of-integer)` — field widths in px

---
## Method: ListGrid.getColumnLeft

### Description
Return the left offset (in local coordinate space) of a particular column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [Integer](../reference_2.md#type-integer) | false | — | number of the column |

### Returns

`[Integer](../reference_2.md#type-integer)` — left offset of the passed colNum, or null if not yet drawn or no such column

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: ListGrid.invalidateCache

### Description
Invalidate the current data cache for this databound component via a call to the dataset's `invalidateCache()` method, for example, [ResultSet.invalidateCache](ResultSet.md#method-resultsetinvalidatecache).

**NOTE:** there is no need to call `invalidateCache()` when a save operation is performed on a DataSource. Automatic cache synchronization features will automatically update caches - see [ResultSet](ResultSet.md#class-resultset) for details. If automatic cache synchronization isn't working, troubleshoot the problem using the steps suggested [in the FAQ](http://forums.smartclient.com/showthread.php?t=8159#aGrid) rather than just calling invalidateCache(). Calling `invalidateCache()` unnecessarily causes extra server load and added code complexity.

Calling `invalidateCache()` will automatically cause a new fetch to be performed with the current set of criteria if data had been previously fetched and the component is currently drawn with data visible - there is no need to manually call fetchData() after invalidateCache() and this could result in duplicate fetches.

While data is being re-loaded after a call to `invalidateCache()`, the widget is in a state similar to initial data load - it doesn't know the total length of the dataset and any APIs that act on records or row indices will necessarily fail and should not be called. To detect that the widget is in this state, call [ResultSet.lengthIsKnown](ResultSet.md#method-resultsetlengthisknown).

`invalidateCache()` only has an effect if this components dataset is a data manager class that manages a cache (eg ResultSet or ResultTree). If data was provided as a simple Array or List, invalidateCache() does nothing.

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.refreshData](#method-listgridrefreshdata)

---
## Method: ListGrid.setFieldError

### Description
Set a validation error for some cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row index of cell to add validation error for |
| fieldName | [String](#type-string)|[number](#type-number) | false | — | col index or field name of cell to add validation error for |
| errorMessage | [String](#type-string)|[Array of String](#type-array-of-string) | false | — | validation error/errors for the cell. |

### Groups

- gridValidation

### See Also

- [ListGrid.getCellErrors](#method-listgridgetcellerrors)
- [ListGrid.setRowErrors](#method-listgridsetrowerrors)

---
## Method: ListGrid.setFastCellUpdates

### Description
Setter for [GridRenderer.fastCellUpdates](GridRenderer.md#attr-gridrendererfastcellupdates). Has no effect in browsers other than Internet Explorer.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fastCellUpdates | [boolean](../reference.md#type-boolean) | false | — | whether to enable fastCellUpdates. |

---
## Method: ListGrid.markRecordsRemoved

### Description
Marks an array of records deleted such that a later call to [ListGrid.saveEdits](#method-listgridsaveedits) or [ListGrid.saveAllEdits](#method-listgridsavealledits) will cause a "remove" [DSRequest](../reference_2.md#object-dsrequest) to be submitted.

This method is similar to [ListGrid.markRecordRemoved](#method-listgridmarkrecordremoved) but should be more efficient in avoiding unneeded duplicate refreshes due to the multiple records getting marked.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of ListGridRecord](#type-array-of-listgridrecord)|[number](#type-number) | false | — | records or indices to mark removed |

### Groups

- editing

### See Also

- [ListGrid.markRecordRemoved](#method-listgridmarkrecordremoved)

---
## Method: ListGrid.getCellErrors

### Description
Returns the current set of errors for this cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | index of row to check for validation errors. |
| fieldName | [String](#type-string)|[number](#type-number) | false | — | field to check for validation errors - can be fieldName or index of the column. |

### Returns

`[Array of String](#type-array-of-string)` — array of error messages (strings) for the specified cell. If no validation errors are present, returns null.

### Groups

- gridValidation

---
## Method: ListGrid.clearFieldSearchOperator

### Description
Clears the current search operator from a field in the grid's [filter row](ListGrid_1.md#attr-listgridfiltereditor). This will reset the field to its [default operator](ListGridField.md#attr-listgridfieldfilteroperator) and, unless [ListGrid.alwaysShowOperatorIcon](ListGrid_1.md#attr-listgridalwaysshowoperatoricon) is true, hide the field's operatorIcon.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

If [ListGrid.filterOnKeypress](ListGrid_1.md#attr-listgridfilteronkeypress) is true, a fetch may be issued when the operator is cleared - see [ListGrid.setFieldSearchOperator](#method-listgridsetfieldsearchoperator) for details. To prevent this fetch, pass the _suppressFilter_ parameter.

To retrieve a field's current search operator, use [ListGrid.getFieldSearchOperator](#method-listgridgetfieldsearchoperator). To programmatically modify a field's current search operator, use [ListGrid.setFieldSearchOperator](#method-listgridsetfieldsearchoperator).

This method has no effect if no specific operator has been set on the field, either by the user or as a result of other criteria applied by [ListGrid.setCriteria](#method-listgridsetcriteria) or similar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | name of the field to clear the search operator from |
| suppressFilter | [Boolean](#type-boolean) | false | — | prevent this call from causing a filter as a result of operator change - clearing, eg, "isNull" criteria will cause a refilter |

---
## Method: ListGrid.setSort

### Description
Sort the grid on one or more fields.

Pass in an array of [SortSpecifier](../reference_2.md#object-sortspecifier)s to have the grid's data sorted by the fields in each [specifier.property](../reference.md#attr-sortspecifierproperty) and in the directions specified. The grid can be sorted by any combination of fields, including fields specified in the fields array, whether visible or hidden, and [unused fields from the\\n underlying dataSource](DataSource.md#attr-datasourcefields), if there is one.

If multiple fields are sorted, those that are visible show a directional icon and a small [sort-numeral](ListGrid_1.md#attr-listgridsortnumeralstyle) indicating that field's index in the sort configuration.

See [addSort()](#method-listgridaddsort) and [toggleSort()](#method-listgridtogglesort) APIs for information on making changes to the current sort configuration.

Note that for editable grids, sorting is performed by underlying data values, not for unsaved [pending edit values](#method-listgridgeteditvalues).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifiers | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | Array of [SortSpecifier](../reference_2.md#object-sortspecifier) objects |

**Flags**: A

---
## Method: ListGrid.getViewState

### Description
Returns a snapshot of the current view state of this ListGrid.  
This includes the field, sort, hilite, group, and selected state of the grid, its criteria and, when canShowFilterEditor is true, whether the filter-editor is visible, returned as a string representation of a [ListGridViewState](../reference_2.md#type-listgridviewstate) object.  
This string can be stored over page-reloads (for example, in [browser local storage](Offline.md#classmethod-offlineput) or as field value in a record stored to a [DataSource](DataSource.md#class-datasource)) and then reapplied to the grid via [ListGrid.setViewState](#method-listgridsetviewstate) later to reset the grid to to the current state (assuming the same data / fields are present).

To detect when view state changes, developers may use the [viewStateChanged event](#method-listgridviewstatechanged).

Note that the [ListGrid.autoPersistViewState](ListGrid_1.md#attr-listgridautopersistviewstate) feature will automatically persist the view state to Offline storage and reapply when the grid is reloaded, without the need to invoke this method explicitly.

### Returns

`[ListGridViewState](../reference_2.md#type-listgridviewstate)` — current view state for the grid.

### Groups

- viewState

### See Also

- [ListGridViewState](../reference_2.md#type-listgridviewstate)
- [ListGrid.setViewState](#method-listgridsetviewstate)

---
## Method: ListGrid.deselectRange

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
## Method: ListGrid.getArrowKeyEditAction

### Description
How should "Up" and "Down" arrow keypresses be handled when the user is editing an item in the grid.

Returning "none" will cause the grid to take no action and allow default up/down arrow key behavior within the editor to proceed. Returning "editNext" will create an appropriate [EditCompletionEvent](../reference.md#type-editcompletionevent) (_"arrow\_up"_ or _"arrow\_down"_ and cause the grid to start editing the previous or next row).

Default behavior varies by item type. For items where up and down arrows have significant functionality to the editor this method returns _"none"_, allowing that standard behavior to proceed. This includes:  
\- Multi line editors (such as TextAreaItems)  
\- SelectItems  
\- SpinnerItems  
For other items, the default return value will be _"edit\_next"_

To override these defaults, developers may specify an explicit arrowKeyEditAction at the [grid](ListGrid_1.md#attr-listgridarrowkeyeditaction), or [field](ListGridField.md#attr-listgridfieldarrowkeyeditaction) level.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [FormItem](#type-formitem) | false | — | Edit item receiving the up or down arrow keypress event |
| keyName | [KeyName](../reference_2.md#type-keyname) | false | — | Key pressed (one of "Arrow\_Up" or "Arrow\_Down") |

### Returns

`[ArrowKeyEditAction](../reference.md#type-arrowkeyeditaction)` — action to take

---
## Method: ListGrid.cellMouseDown

### Description
Called when a cell receives a mousedown event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.getBaseStyle

### Description
Return the base styleName for this cell. Has the following implementation by default:

*   If [this.editFailedBaseStyle](ListGrid_1.md#attr-listgrideditfailedbasestyle) is defined, and the cell is displaying a validation error return this value.
*   If [this.editFailedPendingStyle](ListGrid_1.md#attr-listgrideditpendingbasestyle) is defined, and the cell is displaying an edit value that has not yet been saved (see [ListGrid.autoSaveEdits](ListGrid_1.md#attr-listgridautosaveedits)) return this value.
*   Otherwise return [record\[listGrid.recordBaseStyleProperty\]](ListGrid_1.md#attr-listgridrecordbasestyleproperty), if defined, otherwise [field.baseStyle](ListGridField.md#attr-listgridfieldbasestyle).

If no custom style is found for the cell as described above, the default baseStyle will be returned. If [ListGrid.baseStyle](ListGrid_1.md#attr-listgridbasestyle) is specified this will be used. Otherwise for grids showing fixed height rows which match [ListGrid.normalCellHeight](ListGrid_1.md#attr-listgridnormalcellheight) [ListGrid.normalBaseStyle](ListGrid_1.md#attr-listgridnormalbasestyle) will be used. For grids with variable, or modified cell heights, [ListGrid.tallBaseStyle](ListGrid_1.md#attr-listgridtallbasestyle) will be used.

Note also that enabling [ListGrid.fastCellUpdates](ListGrid_1.md#attr-listgridfastcellupdates) will cause the `tallBaseStyle` to be used rather than [ListGrid.normalBaseStyle](ListGrid_1.md#attr-listgridnormalbasestyle).

As noted under [ListGrid.enforceVClipping](ListGrid_1.md#attr-listgridenforcevclipping), cell content which renders taller than the available space within a cell may cause rows to expand even if [ListGrid.fixedRecordHeights](ListGrid_1.md#attr-listgridfixedrecordheights) is true. This can lead to misaligned rows when frozen columns are used. Developers should be aware that changing cell styling such that there is increased borders or padding will reduce the available space for content within the specified cell height, making this scenario more common. To fix this, specify a larger cellHeight, or set enforceVClipping to true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record associated with this cell. May be `null` for a new edit row at the end of this grid's data set. |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS class for this cell

### See Also

- [ListGrid.getCellStyle](#method-listgridgetcellstyle)

---
## Method: ListGrid.getFilterEditorType

### Description
If we're showing the filter (query-by-example) row for this ListGrid, this method is used to determine the type of form item to display in the filter edit row for this field. Default implementation will return the field.filterEditorType if specified, or the result of [form.getEditorType()](DynamicForm.md#method-dynamicformgeteditortype) otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field definition to get the editorType for |

### Returns

`[String](#type-string)` — the editorType to use in the filterEditor for the passed field

### Groups

- filterEditor

**Flags**: A

---
## Method: ListGrid.getDrawnRows

### Description
Get the rows that are currently drawn (exist in the DOM), as an array of \[firstRowNum, lastRowNum\].

The drawn rows differ from the [visibleRows](#method-listgridgetvisiblerows) because of [drawAhead](ListGrid_1.md#attr-listgriddrawaheadratio). The drawn rows are the appropriate range to consider if you need to, eg, using [ListGrid.refreshCell](#method-listgridrefreshcell) to update all the cells in a column.

If the grid is undrawn or the [ListGrid.emptyMessage](ListGrid_1.md#attr-listgridemptymessage) is currently shown, returns \[null,null\];

### Returns

`[Array](#type-array)` — —

---
## Method: ListGrid.getEditValue

### Description
Returns the current temporary locally stored edit value for some field within a record being edited.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | index of the row for which the editValue should be returned |
| colNum | [number](#type-number)|[String](#type-string) | false | — | index of the field, or fieldName, for which value should be returned |

### Returns

`[Any](#type-any)` — edit value for the field in question

### Groups

- editing

---
## Method: ListGrid.getDropIndex

### Description
Return the drop-index for a given row and reorderPosition.

When there are no rows in the grid, getDropIndex() returns zero.

If parameter _recordNum_ is not passed, the current event row is used, see [ListGrid.getEventRow](#method-listgridgeteventrow).

Parameter [reorderPosition](../reference.md#type-reorderposition) indicates where the drop-item should appear in relation to the row at index _recordNum_. If no reorderPosition is provided, it is calculated based on the physical position of the mouse in the drop-target row when the drop occurs; if the mouse is in the top half of a row, the drop-index is before _recordNum_. Otherwise, the drop-index is after _recordNum_.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recordNum | [number](#type-number) | true | — | Index of the record to drop onto |
| reorderPosition | [ReorderPosition](../reference.md#type-reorderposition) | true | — | Where to drop in relation to _recordNum_ |

### Returns

`[number](#type-number)` — The calculated drop-index

---
## Method: ListGrid.setFields

### Description
Sets the fields array and/or field widths to newFields and sizes, respectively.

If newFields is specified, it is assumed that the new fields may have nothing in common with the old fields, and the component is substantially rebuilt. Furthermore, it's invalid to modify any of the existing [ListGridField](../reference_2.md#object-listgridfield)s after they've been passed to this function. Consider the following methods for more efficient, more incremental changes: [ListGrid.resizeField](#method-listgridresizefield), [ListGrid.reorderField](#method-listgridreorderfield), [ListGrid.showField](#method-listgridshowfield), [ListGrid.hideField](#method-listgridhidefield), or [ListGrid.setFieldProperties](#method-listgridsetfieldproperties).

Two specific values of newFields have explicit meanings:

*   null - a newFields value of `null` indicates there are no field overrides. All current fields are removed and, if the grid is bound to a [DataSource](DataSource.md#class-datasource), the "default binding" is used. (see [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields)).
*   empty array (\[\]) - providing an empty array for the newFields indicates that no fields are desired even if a dataSource is provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newFields | [Array of ListGridField](#type-array-of-listgridfield) | true | — | array of fields to draw |

**Flags**: A

---
## Method: ListGrid.getDragData

### Description
During a drag-and-drop interaction, this method returns the set of records being dragged out of the component. In the default implementation, this is the list of currently selected records.

This method is consulted by [ListGrid.willAcceptDrop](#method-listgridwillacceptdrop).

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

---
## Method: ListGrid.getSelection

### Description
Returns all selected records in this grid. If this grid is [grouped](ListGrid_1.md#attr-listgridisgrouped), group header nodes will not be included in the returned array. Developers can make use of [ListGrid.getGroupTreeSelection](#method-listgridgetgrouptreeselection) to get the selection including the selected group header nodes.

**NOTE:** Records in the returned array should be treated as read-only and not modified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| excludePartialSelections | [Boolean](#type-boolean) | true | — | When true, partially selected records will not be returned. Otherwise, both fully and partially selected records are returned. |

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — array of selected records, which will be empty if no record is selected.

### Groups

- selection

---
## Method: ListGrid.getToggleFreezeText

### Description
If we're showing a [headerContextMenu](ListGrid_1.md#attr-listgridshowheadercontextmenu) for this grid and [this.canFreezeFields](ListGrid_1.md#attr-listgridcanfreezefields) is true, this string will be shown as the title for the menu item to toggle whether a field is frozen or unfrozen.

Default implementation evaluates and returns [ListGrid.freezeFieldText](ListGrid_1.md#attr-listgridfreezefieldtext) or [ListGrid.unfreezeFieldText](ListGrid_1.md#attr-listgridunfreezefieldtext) depending on whether the field is currently frozen.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field to get the menu item title for |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — Title to show in the menu item

### Groups

- i18nMessages

---
## Method: ListGrid.getColumnWidth

### Description
Return the width of a particular column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [number](#type-number) | false | — | number of the column |

### Returns

`[Integer](../reference_2.md#type-integer)` — width of the column, or `null` if undrawn or no such column.

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: ListGrid.getSelectedRecords

### Description
Returns all selected records in this grid.

**NOTE:** Records in the returned array should be treated as read-only and not modified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| excludePartialSelections | [boolean](../reference.md#type-boolean) | true | — | When true, partially selected records will not be returned. Otherwise, both fully and partially selected records are returned. |

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — array of selected records, which will be empty if no record is selected.

### Groups

- selection

---
## Method: ListGrid.getDrawArea

### Description
Returns the extents of the rows and columns currently visible in this grid's viewport.

Note: if there are any [frozen fields](ListGridField.md#attr-listgridfieldfrozen), they are not included in the draw area range returned by this method. Frozen fields are assumed to never be scrolled out of view. The column coordinates returned by this method will only include unfrozen columns.

### Returns

`[Array of Integer](#type-array-of-integer)` — The row/col co-ordinates currently visible in the viewport as \[startRow, endRow, startCol, endCol\].

**Flags**: A

---
## Method: ListGrid.sortChanged

### Description
Notification method executed when the [sort specifiers](#method-listgridsetsort) change for this grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifiers | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | new sort specifiers - may be empty indicating the grid was unsorted |

---
## Method: ListGrid.getExpandedRecords

### Description
Returns the list of [records](../reference_2.md#object-listgridrecord) from this ListGrid that are [expanded](#method-listgridexpandrecord)

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — All expanded records in the grid

### Groups

- expansionField

---
## Method: ListGrid.getCellContextMenuItems

### Description
If [ListGrid.showCellContextMenus](ListGrid_1.md#attr-listgridshowcellcontextmenus) is `true` this method returns the menu items to be displayed in the default cell context menu.

This method is called at various times, so this method should not instantiate any classes, because they'll be re-created on each call, resulting in a leak - your implementation should return an array of menuItem config-blocks only, so you shouldn't instantiate actual Menu instances to apply as the [submenu](MenuItem.md#attr-menuitemsubmenu) of items - instead, set submenu to a simple array of menuItems. If your use-case necessitates that class instances are created, because specific submenus have a different Menu class, for example, you should keep a reference to them and either, if their content is dynamic, destroy and recreate them with the new items, or just return the existing instances otherwise.

The default set of menu items includes items for built-in ListGrid features, like showing or hiding an inline edit form, or removing records.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Integer](../reference_2.md#type-integer) | false | — | The record the user clicked in |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | Index of the record the user clicked in |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | Index of the column the user clicked in |

### Returns

`[Array of MenuItem](#type-array-of-menuitem)` — —

---
## Method: ListGrid.getCellPageRect

### Description
Returns the page offsets and size of the cell at the passed row and column. If auto-sizing is enabled, sizes are not definitive until the grid has finished drawing, so calling this method before drawing completes will return the configured column sizes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row index of the cell |
| colNum | [number](#type-number) | false | — | column index of the cell |

### Returns

`[Array of Integer](#type-array-of-integer)` — the page rect of the passed cell, or null if undrawn

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: ListGrid.showDragHandles

### Description
Shows an additional field near the beginning of the field list (after any [row number](ListGrid_1.md#attr-listgridshowrownumbers) field) that can be dragged to drag the current selection. This feature is useful in [touch environments](Browser.md#classattr-browseristouch) where both touch scrolling and dragging are needed on the same grid, and allows scrolling to be triggered on the other fields so that both operations are available. Targeted touch environments include both mobile devices, and Windows hardware that supports [Dual Input Mode](Browser.md#classattr-browsersupportsdualinput) such as Microsoft Surface.

Note that the [drag handle field](ListGrid_1.md#attr-listgriddraghandlefield) will never be shown unless [ListGrid.canReorderRecords](ListGrid_1.md#attr-listgridcanreorderrecords) or [ListGrid.canDragRecordsOut](ListGrid_1.md#attr-listgridcandragrecordsout) are true.

In IE11 or Microsoft Edge, dragging a record in a grid may not be possible using a touch device without enabling drag handles, or disabling native touch scrolling by setting  `window.isc_useNativeTouchScrolling = false`  before SmartClient is loaded.

#### Background

One alternative to adding a drag handle field would be to use long touch to start a drag (with normal touch triggering scrolling). However, this is unsupportable in IE11 or Edge on Microsoft Surface (with native scrolling) because native scrolling cannot be canceled on the fly using Event.preventDefault(), but instead must be disabled by applying the appropriate CSS at rendering time. (Such limitations are not present elsewhere, such as on Android or IPhone browsers.)

For more details, some links are provided below. Note that while IE10 is mentioned in some of the links, the reasoning is still relevant now for IE11 and Edge as the limitations remain:

*   [Cross-browser support of touchMove](https://quirksmode.org/mobile/default.html)
*   [preventDefault() doesn't work in IE11 on MS Surface](https://stackoverflow.com/questions/26218146/pointer-events-ie11-surface)
*   [preventDefault() doesn't work in Edge on MS Surface](https://stackoverflow.com/questions/49299496/html5-pointermove-touchmove-not-working-in-microsoft-edge)
*   [preventDefault() failure reported to Microsoft against IE10](https://web.archive.org/web/20160309214328/https://connect.microsoft.com/IE/feedback/details/767646/ms-touch-action-does-not-allow-a-way-to-programmatically-prevent-default-touch-behavior)

### Groups

- dragHandleField

### See Also

- [ListGrid.hideDragHandles](#method-listgridhidedraghandles)
- [ListGrid.dragHandleField](ListGrid_1.md#attr-listgriddraghandlefield)
- [ListGrid.dragHandleIcon](ListGrid_1.md#attr-listgriddraghandleicon)
- [ListGrid.dragHandleIconSize](ListGrid_1.md#attr-listgriddraghandleiconsize)

---
## Method: ListGrid.cellErrorIconHover

### Description
Optional stringMethod to fire when the user hovers over the error icon of a cell with validation errors. The default behavior is to show a hover canvas containing the validation error message text. Return false to suppress this default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard error message hover

### Groups

- events

### See Also

- [ListGrid.showErrorIcons](ListGrid_1.md#attr-listgridshowerroricons)

**Flags**: A

---
## Method: ListGrid.expandRecords

### Description
Expands the passed list of [records](../reference_2.md#object-listgridrecord) by creating a subcomponent for each record and inserting them it in to the record's grid-row. Calls [expandRecord](#method-listgridexpandrecord) for each passed record, but only marks the grid for redraw once, after all expansions are complete.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of ListGridRecord](#type-array-of-listgridrecord) | false | — | records to expand |

### Groups

- expansionField

---
## Method: ListGrid.setUserFormula

### Description
Updates the [userFormula](ListGridField.md#attr-listgridfielduserformula) of the specified field. This method is preferred over setting the the 'userFormula' property of the field directly because it also updates any component dependencies and recalculates the field. If the formula is not passed or is `undefined`, it is assumed that the formula has already been updated and only the dependency propagation logic will run.

Known component dependencies are:

*   the cached record values of the formula for this field
*   the common formula variable => field name map maintained by the component for calls to the [FormulaBuilder](FormulaBuilder.md#class-formulabuilder)
*   any generated field that references the field's calculated values

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[String](#type-string) | false | — | field owning the formula |
| userFormula | [UserFormula](#type-userformula) | true | — | optional formula to install |

### See Also

- [ListGridField.userFormula](ListGridField.md#attr-listgridfielduserformula)

---
## Method: ListGrid.rowHover

### Description
Called when the mouse hovers over a row if this.canHover is true. Returning false will suppress the hover text from being shown if this.showHover is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event (default behavior of showing the hover)

### Groups

- events

### See Also

- [ListGrid.canHover](ListGrid_1.md#attr-listgridcanhover)

---
## Method: ListGrid.validateRow

### Description
Validate the current set of edit values for the row in question.

Called when the user moves to a new edit row, or when an edited record is to be saved if client side validation is enabled for this grid.

This method may also be called directly to perform row level validation at any time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | index of row to be validated. |

### Returns

`[Boolean](#type-boolean)` — returns true if validation was successful (no errors encountered), false otherwise.

### Groups

- gridValidation

---
## Method: ListGrid.getExportBGColor

### Description
When exporting data to Excel/OpenOffice format using [exportData()](#method-listgridexportdata) or [exportClientData()](#method-listgridexportclientdata), background color to use for the cell at the given rowNum and colNum.

See [exportBGColor](../kb_topics/exportBGColor.md#kb-topic-exports--cell-background-color) for an overview.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row number of cell |
| colNum | [int](../reference.md#type-int) | false | — | column number of cell |
| record | [Record](#type-record) | false | — | the record object behind the row being exported |

### Returns

`[CSSColor](../reference_2.md#type-csscolor)` — background color to use for the cell, or null to use the default background color

### Groups

- exportBackgroundColor

---
## Method: ListGrid.setShowGridSummary

### Description
Setter for the [ListGrid.showGridSummary](ListGrid_1.md#attr-listgridshowgridsummary) attribute

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showGridSummary | [boolean](../reference.md#type-boolean) | false | — | new value for this.showGridSummary |

---
## Method: ListGrid.getRowSpan

### Description
Return how many rows this cell should span. Default is 1.

This method will only be called if [ListGrid.allowRowSpanning](ListGrid_1.md#attr-listgridallowrowspanning) is set to `true`

When using row spanning, consider setting [ListGrid.useRowSpanStyling](ListGrid_1.md#attr-listgriduserowspanstyling) to enable row-span-sensitive styling behaviors.

Note that the standard implementation assumes that the number of rows spanned by cells decreases or stays the same, starting with the first (leftmost) column in the grid and moving rightwards.

When using row spanning:

*   APIs that allow modifying the contents of cells (such as [ListGrid.getCellStyle](#method-listgridgetcellstyle) or [ListGridField.formatCellValue](ListGridField.md#method-listgridfieldformatcellvalue)) will be called only once per row-spanning cell
*   when using [cell-based selection](ListGrid_1.md#attr-listgridcanselectcells), only the spanning cell is considered selected, and not any of the cells spanned through. For example, if the cell at row 2 column 0 spans 2 cells, [CellSelection.isSelected()](CellSelection.md#class-cellselection) will be true for 2,0 but false for 3,0.
*   if using incremental rendering (either horizontal or vertical), `getRowSpan()` may be called for a rowNum **in the middle of a spanning cell**, and should return the remaining span from that rowNum onward.
*   cell-level events such as [ListGrid.recordClick](#method-listgridrecordclick) will report the logical rowNum for spanned cells. In other words if a cell spans two rows, a different rowNum parameter will be passed to the recordClick handler depending on whether the user clicks at the top of the spanning cell or the bottom. Developers can normalize this to the starting cell via the [ListGrid.getCellStartRow](#method-listgridgetcellstartrow) API.
*   for cells that span multiple records, editing behavior may be controlled by the [rowSpanEditMode](../reference.md#type-rowspaneditmode) attribute.
*   rowSpanning can be used in conjunction with [recordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents). If record component are enabled on a grid with row-spanning cells the behavior is as follows:
    *   Having [ListGrid.recordComponentPosition](ListGrid_1.md#attr-listgridrecordcomponentposition) set to "expand" is not currently supported for grids that render out spanning cells.
    *   The method to retrieve / create record components will not be run for cells that are "spanned". In other words if the first row in a grid spans 2 rows for some field, the second logical row is "spanned" for that field - that cell doesn't render any content and won't attempt to create a recordComponent.
    *   If [ListGrid.showRecordComponentsByCell](ListGrid_1.md#attr-listgridshowrecordcomponentsbycell) is false, the method to create record components will be called for every non-spanned cell in the first column of the grid.
    *   Percentage sizing of record components spanning multiple cells will be calculated relative to the set of spanned cells.

More generally, the ListGrid has a data model of one [Record](../reference.md#object-record) per row, and spanning cells doesn't fit well with this model, meaning that many ListGrid features are incompatible with rowSpanning.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[number](#type-number)` — number of cells to span

---
## Method: ListGrid.getCurrentExpansionComponent

### Description
Returns the expansion component derived from [ListGrid.getExpansionComponent](#method-listgridgetexpansioncomponent) currently visible in some record, or null if the specified record is not showing an expansion component.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Integer](../reference_2.md#type-integer)|[ListGridRecord](#type-listgridrecord) | false | — | rowNum or record to get the expansionComponent for |

### Returns

`[Canvas](#type-canvas)` — the currently visible expansion component for the expanded row.

### Groups

- expansionField

---
## Method: ListGrid.getFrozenRollUnderCanvas

### Description
For grids with frozen columns, this method is called to retrieve the [ListGrid.frozenRollUnderCanvas](ListGrid_1.md#attr-listgridfrozenrollundercanvas) when [showing a rollUnder canvas](ListGrid_1.md#attr-listgridshowrollundercanvas) or showing a [rollUnder canvas for the selected record](ListGrid_1.md#attr-listgridshowselectedrollundercanvas).

The default implementation uses the [AutoChild](../reference.md#type-autochild) subystem to create the [ListGrid.rollUnderCanvas](ListGrid_1.md#attr-listgridrollundercanvas) auto child. It may be overridden for custom behavior.

Note that for efficiency this should not typically create a new Canvas every time that it is called. Instead usually a single rollOver canvas should be created and updated to reflect the current rollOver row if necessary.

Return null to avoid showing a `rollUnderCanvas` for frozen fields for this row.

See also [ListGrid.getRollUnderCanvas](#method-listgridgetrollundercanvas).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | index of the current rollOver row. |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | index of the current rollOver column. This parameter will be null unless [useCellRollOvers](ListGrid_1.md#attr-listgridusecellrollovers) is true for the grid. |

### Returns

`[Canvas](#type-canvas)` — the embedded component

### Groups

- hoverComponents

---
## Method: ListGrid.isGroupNode

### Description
If this listGrid is [grouped](#method-listgridgroupby), is the record passed in a group header node.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to test |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if the record passed in is a group header node

---
## Method: ListGrid.cellClick

### Description
Called when a cell receives a click event.

Note that returning false from this method will not prevent any specified [ListGrid.rowClick](#method-listgridrowclick) handler from firing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object returned from getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.getRowAriaState

### Description
Returns a map of [WAI ARIA state attribute values](Canvas.md#attr-canvasariastate) to be written into rows within this grid.

Default implementation returns an object with combined properties from any specified [row aria state default object](ListGrid_1.md#attr-listgridrowariastate), overlaid with any [ListGrid.recordRowAriaStateProperty](ListGrid_1.md#attr-listgridrecordrowariastateproperty) properties specified on the record itself, plus the following attributes:

*   `setsize` - total row count for the grid if [ListGrid.ariaRole](ListGrid_1.md#attr-listgridariarole) is set to `"list"`
*   `posinset` - index of the row if [ListGrid.ariaRole](ListGrid_1.md#attr-listgridariarole) is set to `"list"`
*   `rowindex` - index of the row if [ListGrid.ariaRole](ListGrid_1.md#attr-listgridariarole) is set to `"grid"`
*   `selected` - true if the record is [selected](#method-listgridgetselection)
*   `expanded` - true for [expanded records](ListGrid_1.md#attr-listgridcanexpandrecords) or [open folders](Tree.md#method-treeisopen)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | row index |
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for the row in question |
| role | [String](#type-string) | false | — | ARIA role for the cell as returned by [ListGrid.getRowRole](#method-listgridgetrowrole) |

### Returns

`[Object](../reference.md#type-object)` — Object containing aria property names and values to write into the cell's HTML

### Groups

- accessibility

**Flags**: A

---
## Method: ListGrid.setWrapCells

### Description
Setter for [ListGrid.wrapCells](ListGrid_1.md#attr-listgridwrapcells)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| wrapCells | [boolean](../reference.md#type-boolean) | false | — | New wrapCells value |

---
## Method: ListGrid.viewStateChanged

### Description
Notification method executed whenever the viewState of this grid changes. View state is accessible via [ListGrid.getViewState](#method-listgridgetviewstate), and contains field state information, sort information, selection information, hiliting information and grouping information.

### See Also

- [ListGrid.fieldStateChanged](#method-listgridfieldstatechanged)

---
## Method: ListGrid.cellOver

### Description
Called when the mouse pointer enters a cell

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.hasErrors

### Description
Does this grid currently have errors associated with editValues for any row in the grid.

### Returns

`[Boolean](#type-boolean)` — true if there are unresolved errors, false otherwise

### Groups

- gridValidation

### See Also

- [ListGrid.rowHasErrors](#method-listgridrowhaserrors)
- [ListGrid.cellHasErrors](#method-listgridcellhaserrors)

---
## Method: ListGrid.willAcceptDrop

### Description
This method overrides [Canvas.willAcceptDrop](Canvas.md#method-canvaswillacceptdrop) and works as follows:  

*   If [Canvas.willAcceptDrop](Canvas.md#method-canvaswillacceptdrop) (the superclass definition) returns false, this method always returns false. This allows [Canvas.dragType](Canvas.md#attr-canvasdragtype) and [Canvas.dropTypes](Canvas.md#attr-canvasdroptypes) to be used to configure eligibility for drop. By default, a ListGrid has no dropTypes configured and so this check will not prevent a drop.
*   If this is a self-drop, that is, the user is dragging a record within this list, this is an attempted drag-reorder. If [ListGrid.canReorderRecords](ListGrid_1.md#attr-listgridcanreorderrecords) is false, this method returns false.
*   If the [dragTarget](EventHandler.md#classmethod-eventhandlergetdragtarget) is another widget, if [ListGrid.canAcceptDroppedRecords](ListGrid_1.md#attr-listgridcanacceptdroppedrecords) is false this method returns false.
*   If a call to [ListGrid.getDragData](#method-listgridgetdragdata) on the `dragTarget` fails to return an record object or an array of records, this method returns null.
*   If the drop target record is disabled or has [ListGridRecord.canAcceptDrop](ListGridRecord.md#attr-listgridrecordcanacceptdrop) set to false, return false.

Note that this method may be called repeatedly during a drag-drop interaction to update the UI and notify the user as to when they may validly drop data.

### Returns

`[boolean](../reference.md#type-boolean)` — true if this component will accept a drop of the dragData, otherwise false, or null if the drop() should be bubbled to parent elements

### Groups

- events
- dragging

### See Also

- [ListGridRecord.canAcceptDrop](ListGridRecord.md#attr-listgridrecordcanacceptdrop)
- [ListGrid.getDragData](#method-listgridgetdragdata)

**Flags**: A

---
## Method: ListGrid.getExpansionField

### Description
Returns the specially generated expansion field used when [ListGrid.canExpandRecords](ListGrid_1.md#attr-listgridcanexpandrecords) is true.

Called during [ListGrid.setFields](#method-listgridsetfields), this method can be overridden to add advanced dynamic defaults to the expansion field (call Super, modify the default field returned by Super, return the modified field). Normal customization can be handled by just setting [AutoChild](../reference.md#type-autochild) properties, as mentioned under the docs for [ListGrid.expansionField](ListGrid_1.md#attr-listgridexpansionfield).

### Returns

`[ListGridField](#type-listgridfield)` — —

### Groups

- expansionField

---
## Method: ListGrid.getGroupByFields

### Description
Get the current grouping of this listGrid as an array of fieldNames.

This method returns an array containing the names of the field(s) by which this grid is grouped (either from [ListGrid.groupByField](ListGrid_1.md#attr-listgridgroupbyfield) having been explicitly set or from a call to [ListGrid.groupBy](#method-listgridgroupby)). If this grid is not currently grouped, this method will return null.

### Returns

`[Array of String](#type-array-of-string)` — Current grouping for this grid. If grouped by a single field an array with a single element will be returned.

---
## Method: ListGrid.setEditValue

### Description
Modifies a field value being tracked as an unsaved user edit.

Use for suggested or reformatted values for edits that remain unsaved.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | Row number (or edit values ID) |
| colNum | [number](#type-number)|[String](#type-string) | false | — | Column number of cell, or name of field having editValue updated |
| value | [Any](#type-any) | false | — | New value for the appropriate field. |

### Groups

- editing

**Flags**: A

---
## Method: ListGrid.getAllFields

### Description
Get the complete array of fields for this ListGrid, including fields that are not currently visible or were specified implicitly via [ListGrid.dataSource](ListGrid_1.md#attr-listgriddatasource).

This list of fields is only valid once the ListGrid has been [drawn](Canvas.md#method-canvasdraw) or once [ListGrid.setFields](#method-listgridsetfields) has been called explicitly. If called earlier, only the list of directly specified fields will be returned (the Array passed to create()).

This Array should be treated as **read-only**. To modify the set of visible fields, use [ListGrid.showField](#method-listgridshowfield), [ListGrid.hideField](#method-listgridhidefield) and related APIs. To update properties of individual fields, use [ListGrid.setFieldProperties](#method-listgridsetfieldproperties) or more specific APIs such as [ListGrid.setFieldTitle](#method-listgridsetfieldtitle).

### Returns

`[Array of ListGridField](#type-array-of-listgridfield)` — Array of all fields in the ListGrid

---
## Method: ListGrid.cellValueIsClipped

### Description
Is the value in a given cell clipped?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number of the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[Boolean](#type-boolean)` — null if there is no cell at the given row, column; otherwise, whether the value in the specified cell is clipped.

### See Also

- [ListGrid.cellValueHover](#method-listgridcellvaluehover)

---
## Method: ListGrid.reorderFields

### Description
Reorder a set of adjacent fields, from start to end exclusive at the end, by distance moveDelta.  
  
NOTE: start and end coordinates are in terms of the currently visible fields, not the full set of fields.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | Start of the range of fields to move, inclusive |
| end | [number](#type-number) | false | — | End of the range of fields to move, non-inclusive |
| moveDelta | [number](#type-number) | false | — | Distance to move by |

**Flags**: A

---
## Method: ListGrid.reorderField

### Description
Reorder a particular field

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [number](#type-number) | false | — | Number of the field to reorder |
| moveToPosition | [number](#type-number) | false | — | New position for that field |

**Flags**: A

---
## Method: ListGrid.filterByEditor

### Description
If the filter editor ([ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor)) is visible for this grid, this method will perform a filter based on the current values in the editor.

### Groups

- filterEditor

---
## Method: ListGrid.recordClick

### Description
Executed when the listGrid receives a 'click' event on an enabled, non-separator record. The default implementation does nothing -- override to perform some action when any record or field is clicked.  
A record event handler can be specified either as a function to execute, or as a string of script to evaluate. If the handler is defined as a string of script, all the parameters below will be available as variables for use in the script.  
To do something specific if a particular field is clicked, add a recordClick method or string of script to that field (same parameters) when you're setting up the list.  
**Notes:**

*   This will not be called if the click is below the last item of the list.
*   This method is called from the default implementation of [ListGrid.rowClick](#method-listgridrowclick), so if that method is overridden this method may not be fired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [ListGrid](#type-listgrid) | false | — | the listGrid that contains the click event |
| record | [ListGridRecord](#type-listgridrecord) | false | — | the record that was clicked on |
| recordNum | [number](#type-number) | false | — | number of the record clicked on in the current set of displayed records (starts with 0) |
| field | [ListGridField](#type-listgridfield) | false | — | the field that was clicked on (field definition) |
| fieldNum | [number](#type-number) | false | — | number of the field clicked on in the listGrid.fields array |
| value | [Any](#type-any) | false | — | value of the cell (after valueMap, etc. applied) |
| rawValue | [Any](#type-any) | false | — | raw value of the cell (before valueMap, etc applied) |
| editedRecord | [ListGridRecord](#type-listgridrecord) | false | — | the clicked record with any unsaved edit values overlaid (see `listGrid.getEditedRecord()`). |

### Returns

`[Boolean](#type-boolean)` — return false to cancel default behavior

### Groups

- events

### See Also

- [ListGrid.rowClick](#method-listgridrowclick)

---
## Method: ListGrid.getRelatedDataSource

### Description
Returns the [DataSource](DataSource.md#class-datasource) containing data related to the passed record. Used when [ListGrid.canExpandRecords](ListGrid_1.md#attr-listgridcanexpandrecords) is true and [ExpansionMode](../reference_2.md#type-expansionmode) is "related". The default implementation returns the DataSource specified in [ListGridRecord.detailDS](ListGridRecord.md#attr-listgridrecorddetailds) if set, otherwise [ListGrid.detailDS](ListGrid_1.md#attr-listgriddetailds).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | The record to get the Related dataSource for. |

### Returns

`[DataSource](#type-datasource)` — The related DataSource for the "record" param

---
## Method: ListGrid.setFilterWindowCriteria

### Description
Setter for [ListGrid.filterWindowCriteria](ListGrid_1.md#attr-listgridfilterwindowcriteria).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | criteria for advanced filtering |

---
## Method: ListGrid.getTitleField

### Description
Method to return the fieldName which represents the "title" for records in this Component.  
If this.titleField is explicitly specified it will always be used. Otherwise, default implementation will check [DataSource.titleField](DataSource.md#attr-datasourcetitlefield) for databound compounds.  
For non databound components returns the first defined field name of `"title"`, `"name"`, or `"id"` where the field is visible. If we don't find any field-names that match these titles, the first field in the component will be used instead.

### Returns

`[String](#type-string)` — fieldName for title field for this component.

---
## Method: ListGrid.getDisplayValue

### Description
Given a field with a specified [ListGridField.valueMap](ListGridField.md#attr-listgridfieldvaluemap) or [ListGridField.displayField](ListGridField.md#attr-listgridfielddisplayfield) this method will return the display value for any underlying data value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldID | [String](#type-string)|[number](#type-number)|[ListGridField](#type-listgridfield) | false | — | Field or field identifier with valueMap |
| valueFieldValue | [Any](#type-any) | false | — | Data value for this field |
| record | [Record](#type-record) | false | — | The record containing the data values to be inspected |

### Returns

`[String](#type-string)` — Display value associated with the specified valueFieldValue

---
## Method: ListGrid.setDragTracker

### Description
Sets the custom tracker HTML to display next to the mouse when the user initiates a drag operation on this component. Default implementation will examine [ListGrid.dragTrackerMode](ListGrid_1.md#attr-listgriddragtrackermode) and set the custom drag tracker to display the appropriate HTML based on the selected record.  
To display custom drag tracker HTML, this method may be overridden - call [EventHandler.setDragTracker](EventHandler.md#classmethod-eventhandlersetdragtracker) to actually update the drag tracker HTML.

### Returns

`[boolean](../reference.md#type-boolean)` — returns false by default to suppress 'setDragTracker' on any ancestors of this component.

### Groups

- dragTracker

---
## Method: ListGrid.setShowGroupSummaryInHeader

### Description
Setter for [ListGrid.showGroupSummaryInHeader](ListGrid_1.md#attr-listgridshowgroupsummaryinheader)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showGroupSummaryInHeader | [boolean](../reference.md#type-boolean) | false | — | new showGroupSummaryInHeader state |

---
## Method: ListGrid.addSort

### Description
Adds another [SortSpecifier](../reference_2.md#object-sortspecifier) to this grid's sort configuration and resorts.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifier | [SortSpecifier](#type-sortspecifier) | false | — | A SortSpecifier object indicating an additional field and direction to sort by |

**Flags**: A

---
## Method: ListGrid.getRecordIndex

### Description
Get the index of the provided record.

This is essentially the same as calling listGrid.data.indexOf(record), except that the currently visible range of records is checked first. This is important for responsiveness in functions that respond to user actions when the user is working near the end of a very large dataset (eg 500k records).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | the record whose index is to be retrieved |

### Returns

`[int](../reference.md#type-int)` — index of the record, or -1 if not found

---
## Method: ListGrid.getGridSummaryFunction

### Description
Determines the [SummaryFunction](../reference_2.md#type-summaryfunction) to use when calculating per-field summary values describing multiple records in this grid. Used to determine the summary function to use for both [ListGrid.showGridSummary](ListGrid_1.md#attr-listgridshowgridsummary) and [ListGrid.showGroupSummary](ListGrid_1.md#attr-listgridshowgroupsummary).

Default implementation picks up [ListGridField.summaryFunction](ListGridField.md#attr-listgridfieldsummaryfunction) if explicitly specified, otherwise checks for a default summary function based on field type (see [SimpleType.setDefaultSummaryFunction](SimpleType.md#classmethod-simpletypesetdefaultsummaryfunction)). Note that a default summary function will not be supplied if the field represents a [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) or [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey), since it would likely not be meaningful.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field to check for summary function |

### Returns

`[SummaryFunction](../reference_2.md#type-summaryfunction)` — summary function for the field in question

**Flags**: A

---
## Method: ListGrid.scrollToCell

### Description
Will scroll the listGrid body such that the specified cell is visible close to the center of the viewport.

This method has no effect if the cell is already visible in the viewport.

When scrolling vertically, this will cause data to be automatically loaded if [paging is active](ListGrid_1.md#attr-listgriddatafetchmode) and you scroll into an area of the data that isn't loaded. Only rows around the target row will be loaded, not all intervening rows. See also [ResultSet](ResultSet.md#class-resultset).

Scrolling into an undrawn area will cause the body area of the grid to redraw, but this won't happen synchronously unless you explicitly call redraw(). Scrolling into an area of the data that is not yet loaded will never synchronously draw new rows, even if you call redraw() - wait for [ListGrid.dataArrived](#method-listgriddataarrived) to be notified when new rows have been loaded.

Calling this method with a row index larger than the current dataset will clamp to the end of the dataset (similarly horizontal scrolling will clamp to the last column).

If a call to this method is made while data is still loading, such that the last row of the dataset is not yet known the grid will attempt to compensate by scrolling the record into view when data arrives, if it is valid. For better control over scrolling, developers should consider calling `scrollToRow()` or `scrollToCell` from [ListGrid.dataArrived](#method-listgriddataarrived) if data is still loading.

With mixed-height rows it will only reliably work if virtualScrolling is enabled.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | Row index of the cell to scroll into view |
| colNum | [int](../reference.md#type-int) | false | — | Column index of the cell to scroll into view |
| xPosition | [Alignment](../reference_2.md#type-alignment) | true | — | Horizontal position of scrolled cell (optional) |
| yPosition | [VerticalAlignment](../reference.md#type-verticalalignment) | true | — | Vertical position of scrolled cell (optional) |

### Groups

- scrolling

**Flags**: A

---
## Method: ListGrid.criteriaChanged

### Description
Callback fired when the end-user changes criteria. This occurs via the +{FilterEditor} or +{showFilterWindow,advanced filtering} interface. It does not fire when a change is made via [ListGrid.setCriteria](#method-listgridsetcriteria), [ListGrid.fetchData](#method-listgridfetchdata), [ListGrid.setFilterWindowCriteria](#method-listgridsetfilterwindowcriteria) or other APIs are called to change the criteria.

---
## Method: ListGrid.dataChangedComplete

### Description
Notification method fired when the [grid data has changed](#method-listgriddatachanged).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationType | [String](#type-string) | true | — | optionally passed operation causing the change |

---
## Method: ListGrid.getGroupedRecordIndex

### Description
Returns the true row index for a grouped record excluding group and summary records. Records in closed groups are included in number.

Function is not applicable for non-grouped grids and will return -1 if called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to number |

### Returns

`[int](../reference.md#type-int)` — row index for record or -1 for group or summary records

### Groups

- rowNumberField

---
## Method: ListGrid.setFieldCellIcon

### Description
Change the [ListGridField.cellIcon](ListGridField.md#attr-listgridfieldcellicon) for a field after the grid is created

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to update |
| cellIcon | [SCImgURL](../reference.md#type-scimgurl) | false | — | new cellIcon for the field |

---
## Method: ListGrid.getExportTextColor

### Description
When exporting data to Excel/OpenOffice format using [exportData()](#method-listgridexportdata) or [exportClientData()](#method-listgridexportclientdata), text color to use for the cell at the given rowNum and colNum.

Return null (the default function behavior) to allow [hilite color](Hilite.md#attr-hilitetextcolor), if any, to determine the text color.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row number of cell |
| colNum | [int](../reference.md#type-int) | false | — | column number of cell |
| record | [Record](#type-record) | false | — | the record object behind the row being exported |

### Returns

`[CSSColor](../reference_2.md#type-csscolor)` — text color to use for the cell, or null to use the default text color

### Groups

- exportBackgroundColor

---
## Method: ListGrid.isSelected

### Description
Returns true if the record is selected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to check |

### Returns

`[Boolean](#type-boolean)` — true if record is selected; false otherwise

### Groups

- selection

---
## Method: ListGrid.groupStateChanged

### Description
Notification method executed whenever the groupState of this grid changes. Group state is accessible via [ListGrid.getGroupState](#method-listgridgetgroupstate), and contains group state information.

---
## Method: ListGrid.refreshData

### Description
Unlike [invalidateCache](#method-listgridinvalidatecache) this will perform an asynchronous (background) refresh of this component's data and then call the provided callback method on completion. A grid needs to have a [DataSource](DataSource.md#class-datasource) associated with it to use this method.

If `refreshData()` is called while the grid is waiting for a response from [ListGrid.fetchData](#method-listgridfetchdata) the `refreshData()` call will be aborted. This is because the fetch has higher priority.

If [ListGrid.fetchData](#method-listgridfetchdata) is called while the grid is waiting for a response from `refreshData()` and the `fetchData()` call has altered the criteria or sort specifiers, the `refreshData()` call will be aborted.

If data is being edited or has been edited without being saved when `refreshData()` is called, the data will be retained so you can save it after the refresh is complete. If you however want to throw away your edited but unsaved data when calling `refreshData()` you first need to call [ListGrid.discardAllEdits](#method-listgriddiscardalledits) which will discard any unsaved edited data.

Note that for a TreeGrid with [TreeGrid.loadDataOnDemand](TreeGrid.md#attr-treegridloaddataondemand): true, all currently opened parent nodes will be re-fetched, except for [paged](TreeGrid.md#attr-treegriddatafetchmode) TreeGrids, for which only opened parent nodes that are _visible_ or contain _visible_ children are re-fetched. We do this in a single queued batch of fetches to maximize efficiency.

Except for changes to the dataset length, [dataChanged()](#method-listgriddatachanged) is not fired after `refreshData()`, as the Framework is not in a position to know for sure if data has actually changed (which would require traversing the entire dataset to determine) and whether criteria, sort or other specifiers of the dataset also have not changed. Applications that need to take action on `refreshData()` should use the callback to do so.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback method to run once the refresh completes. |

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.fetchData](#method-listgridfetchdata)
- [ListGrid.invalidateCache](#method-listgridinvalidatecache)

---
## Method: ListGrid.getIconCursor

### Description
Returns the cursor to display when the mouse pointer is over an [icon](ListGridField.md#attr-listgridfieldicon) in an `"icon"` type field.

Default behavior will display the [ListGridField.iconCursor](ListGridField.md#attr-listgridfieldiconcursor) if specified, otherwise the component level [ListGrid.iconCursor](ListGrid_1.md#attr-listgridiconcursor).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field displaying the icon |

### Returns

`[Cursor](../reference.md#type-cursor)` — cursor to display when the user rolls over icons in this field's cells

---
## Method: ListGrid.updateRecordComponent

### Description
When [ListGrid.showRecordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents) is true, this method is called to update components created by [ListGrid.createRecordComponent](#method-listgridcreaterecordcomponent) when they are to be applied to a different record in the grid. See the [record components overview](ListGrid_1.md#attr-listgridshowrecordcomponents) for more information on recordComponents.

The colNum parameter is applicable only when [ListGrid.showRecordComponentsByCell](ListGrid_1.md#attr-listgridshowrecordcomponentsbycell) is true. Note that if [ListGrid.poolComponentsPerColumn](ListGrid_1.md#attr-listgridpoolcomponentspercolumn) is set to false, the component may have been generated by a [ListGrid.createRecordComponent](#method-listgridcreaterecordcomponent) call applied to a different field.

Return null to avoid re-adding the component to the row or cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to which the passed component applies |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | cell to which the passed component applies |
| component | [Canvas](#type-canvas) | false | — | the component to update |
| recordChanged | [boolean](../reference.md#type-boolean) | false | — | was the passed component previously embedded in a different record? |

### Returns

`[Canvas](#type-canvas)` — return the component to embed in the passed record

### Groups

- recordComponents

---
## Method: ListGrid.setShowGroupSummary

### Description
Setter for the [ListGrid.showGroupSummary](ListGrid_1.md#attr-listgridshowgroupsummary) attribute

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showGroupSummary | [boolean](../reference.md#type-boolean) | false | — | new value for this.showGroupSummary |

---
## Method: ListGrid.isExportingClientData

### Description
Returns true if this component is currently [exporting client data](#method-listgridexportclientdata). This method can be called from custom cell formatters if you need to return a different formatted value for an export than for a live ListGrid

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if this component is currently exporting client data

### See Also

- [ListGrid.exportClientData](#method-listgridexportclientdata)

---
## Method: ListGrid.askForSort

### Description
Show a dialog to configure the sorting of multiple fields on this component. Calls through to [MultiSortDialog.askForSort](MultiSortDialog.md#classmethod-multisortdialogaskforsort), passing this component as the fieldSource and the current [sort-specification](DataBoundComponent.md#method-databoundcomponentgetsort) if there is one.

The generated multiSortDialog can be customized via [ListGrid.multiSortDialogDefaults](ListGrid_1.md#attr-listgridmultisortdialogdefaults), [ListGrid.multiSortDialogProperties](ListGrid_1.md#attr-listgridmultisortdialogproperties).

---
## Method: ListGrid.setFieldHeaderBaseStyle

### Description
Update the [ListGridField.headerBaseStyle](ListGridField.md#attr-listgridfieldheaderbasestyle) for a field within the grid at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | name of the field. |
| newStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new baseStyle for the field header |

---
## Method: ListGrid.getGroupSummaryData

### Description
If this grid is [grouped](ListGrid_1.md#attr-listgridgroupbyfield), and [ListGrid.showGroupSummary](ListGrid_1.md#attr-listgridshowgroupsummary) is true, this method will be called for each group to return the group summary data to display at the end of the group.

By default this will call [ListGridField.getGroupSummary](ListGridField.md#method-listgridfieldgetgroupsummary) if defined for each field and generate an array of records containing the resulting values. If no explicit per-field getGroupSummary method is present, this method will fall back to calling the appropriate [ListGridField.summaryFunction](ListGridField.md#attr-listgridfieldsummaryfunction).

This method may be overridden for custom group-summary display, and may return multiple records if more than one summary row per group is desired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record) | false | — | the records in the group, for which the summary values are being calculated |
| groupNode | [Record](#type-record) | false | — | object with specified groupValue and groupName for this group |
| recalculate | [Boolean](#type-boolean) | true | — | if set to false and the node has existing summary data, returns the stored summary data, rather than recalculating |

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — summary record(s)

---
## Method: ListGrid.setAutoFitWidthApproach

### Description
Setter for the [ListGrid.autoFitWidthApproach](ListGrid_1.md#attr-listgridautofitwidthapproach).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| approach | [AutoFitWidthApproach](../reference_2.md#type-autofitwidthapproach) | false | — | new AutoFitWidth approach |

---
## Method: ListGrid.formulaUpdated

### Description
Notification fired when a user either creates a new formula field or edits an existing formula field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | the formula field |
| formula | [UserFormula](#type-userformula) | false | — | the new or updated formula definition |

---
## Method: ListGrid.setHeaderSpanBaseStyle

### Description
Update the [HeaderSpan.headerBaseStyle](HeaderSpan.md#attr-headerspanheaderbasestyle) for a span within the grid at runtime.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | name of the headerSpan, as specified via [HeaderSpan.name](HeaderSpan.md#attr-headerspanname). |
| newStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new baseStyle for the headerSpan |

---
## Method: ListGrid.clearSort

### Description
This method clears any existing sort on this grid by calling [ListGrid.setSort](#method-listgridsetsort) with a null parameter. The internal list of [SortSpecifier](../reference_2.md#object-sortspecifier)s is removed and the grid is unsorted.

**Flags**: A

---
## Method: ListGrid.setRecordComponentHeight

### Description
Setter for the [ListGrid.recordComponentHeight](ListGrid_1.md#attr-listgridrecordcomponentheight)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Integer](../reference_2.md#type-integer) | false | — | recordComponent height |

### Groups

- recordComponents

---
## Method: ListGrid.handleRegroup

### Description
Callback fired when a regroup operation is begun, either from a direct call to [ListGrid.regroup](#method-listgridregroup), or because of [data arriving from the server](#method-listgriddatachanged) when the grid is already [grouped](#method-listgridgroupby).

After this call, the Framework should eventually call [ListGrid.groupTreeChanged](#method-listgridgrouptreechanged).

### Groups

- grouping

### See Also

- [ListGrid.handleGroupBy](#method-listgridhandlegroupby)
- [ListGrid.groupTreeChanged](#method-listgridgrouptreechanged)

---
## Method: ListGrid.rowHasErrors

### Description
Does the specified row have unresolved errors?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | rowNum to check for errors |

### Returns

`[Boolean](#type-boolean)` — true if there are unresolved errors, false otherwise

### Groups

- gridValidation

### See Also

- [ListGrid.hasErrors](#method-listgridhaserrors)
- [ListGrid.cellHasErrors](#method-listgridcellhaserrors)

---
## Method: ListGrid.willFetchData

### Description
Compares the specified criteria with the current criteria applied to this component's data object and determines whether the new criteria could be satisfied from the currently cached set of data, or if a new filter/fetch operation will be required.

This is equivalent to calling `this.data.willFetchData(...)`. Always returns true if this component is not showing a set of data from the dataSource.

Note that to predict correctly the decision that will be made by filter/fetch, you'll need to pass the same [TextMatchStyle](../reference_2.md#type-textmatchstyle) that will be used by the future filter/fetch. Fetching manually (e.g. [ListGrid.fetchData](#method-listgridfetchdata)) will by default use "exact" while filtering (e.g. [ListGrid.filterData](#method-listgridfilterdata)) will by default use "substring". If the component is configured for autofetch (i.e. [ListGrid.autoFetchData](ListGrid_1.md#attr-listgridautofetchdata): true), that will use [ListGrid.autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle), which defaults to "substring". If nothing/null is passed for the style, this method assumes you want the style from the last filter/fetch.

To determine what [TextMatchStyle](../reference_2.md#type-textmatchstyle) is being used, check the RPC Tab of the [SmartClient Developer Console](../kb_topics/debugging.md#kb-topic-debugging) and check the relevant [DSRequest](../reference_2.md#object-dsrequest).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | new criteria to test. |
| textMatchStyle | [TextMatchStyle](../reference_2.md#type-textmatchstyle) | true | — | New text match style. If not passed assumes textMatchStyle will not be modified. |

### Returns

`[Boolean](#type-boolean)` — true if server fetch would be required to satisfy new criteria.

### Groups

- dataBoundComponentMethods

---
## Method: ListGrid.clearAllCriteria

### Description
This method, the equivalent of the builtin [Clear Filter menu-item](ListGrid_1.md#attr-listgridclearfiltertext), clears all user-visible criteria applied to this grid, including values and filter-operators in the [filter-row](ListGrid_1.md#attr-listgridshowfiltereditor) and criteria in the [advanced filter window](ListGrid_1.md#attr-listgridallowfilterwindow), and issues a re-filter.

---
## Method: ListGrid.getFocusRow

### Description
Get the row that currently has keyboard focus. Arrow key navigation moves relative to this row.

### Returns

`[Integer](../reference_2.md#type-integer)` — rowNum of the current focus row

**Flags**: A

---
## Method: ListGrid.refreshCell

### Description
Refresh an individual cell without redrawing the grid.

The cell's value, CSS class, and CSS text will be refreshed, to the current values returned by getCellValue(), getCellStyle(), and getCellCSSText(), respectively. Also, if displaying a standard hover (not a hover component), re-checks to see if the hover should continue to be displayed, hiding the hover if not, or updating the hover if so.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number of cell to refresh |
| colNum | [number](#type-number) | false | — | column number of cell to refresh |

### Groups

- appearance

### See Also

- [ListGrid.refreshCellStyle](#method-listgridrefreshcellstyle)

---
## Method: ListGrid.canSelectRecord

### Description
If [ListGrid.selectionType](ListGrid_1.md#attr-listgridselectiontype) is not set to `"none"`, This method will be called for each record the user attempts to select. If it returns false, the record will not be selected.

The default implementation will return true for any records where [ListGrid.recordCanSelectProperty](ListGrid_1.md#attr-listgridrecordcanselectproperty) is not explicitly set to false, and false if this method was called by a click on the [expansion field](ListGrid_1.md#attr-listgridexpansionfield) and [selectOnExpandRecord](ListGrid_1.md#attr-listgridselectonexpandrecord) is set to false.

Note this method will not be called at all if [ListGrid.canSelectCells](ListGrid_1.md#attr-listgridcanselectcells) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record being selected |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to disallow selection

---
## Method: ListGrid.getSortFieldCount

### Description
Returns the number of fields involved in this grid's current sort configuration.

### Returns

`[Number](#type-number)` — the number of fields this grid is currently sorted on.

**Flags**: A

---
## Method: ListGrid.setCriteria

### Description
Sets this component's filter criteria. Default implementation calls this.data.setCriteria().

Note: if [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) is true, the [ListGrid.setFilterEditorCriteria](#method-listgridsetfiltereditorcriteria) method may be used to update the values displayed in the filter editor without effecting the data object.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria) | false | — | new criteria to show |

### Groups

- dataBoundComponentMethods

---
## Method: ListGrid.getCheckboxField

### Description
Returns the specially generated checkbox field used when [SelectionAppearance](../reference.md#type-selectionappearance) is "checkbox".

Called during [ListGrid.setFields](#method-listgridsetfields), this method can be overridden to add advanced dynamic defaults to the checkbox field (call Super, modify the default field returned by Super, return the modified field). Normal customization can be handled by just setting [AutoChild](../reference.md#type-autochild) properties, as mentioned under the docs for [ListGrid.checkboxField](ListGrid_1.md#attr-listgridcheckboxfield).

### Returns

`[ListGridField](#type-listgridfield)` — —

### Groups

- checkboxField

---
## Method: ListGrid.refreshRecordComponent

### Description
Discards any [recordComponent](ListGrid_1.md#attr-listgridshowrecordcomponents) currently assigned to the specified record (or cell) and gets a fresh one, according to the [ListGrid.recordComponentPoolingMode](ListGrid_1.md#attr-listgridrecordcomponentpoolingmode)

See also [ListGrid.invalidateRecordComponents](#method-listgridinvalidaterecordcomponents) which allows you to refresh all record components that are currently visible in the grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | Row to refresh |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column to refresh. This parameter should be passed if [ListGrid.showRecordComponentsByCell](ListGrid_1.md#attr-listgridshowrecordcomponentsbycell) is true. |

### Groups

- recordComponents

---
## Method: ListGrid.setUserCriteriaState

### Description
Reset this grid's user-criteria to match the [ListGridUserCriteriaState](../reference_2.md#type-listgridusercriteriastate) object passed in.

Used to restore previous state retrieved from the grid by a call to [ListGrid.getUserCriteriaState](#method-listgridgetusercriteriastate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| userCriteriaState | [ListGridUserCriteriaState](../reference_2.md#type-listgridusercriteriastate) | false | — | Object describing the desired criteria |

### Groups

- viewState

### See Also

- [ListGrid.getUserCriteriaState](#method-listgridgetusercriteriastate)

---
## Method: ListGrid.getSortNumeralHTML

### Description
When multiple fields are sorted, this method returns the HTML for the sort-numeral that appears after the sort-arrows in the header-buttons of sorted fields. If you don't want sort-numerals in the header-buttons, you can override this method to return null or an empty string, or set [ListGrid.showSortNumerals](ListGrid_1.md#attr-listgridshowsortnumerals) to false.

Note that the sortIndex passed in is zero based. The default implementation of this method returns an HTML element with the [ListGrid.sortNumeralStyle](ListGrid_1.md#attr-listgridsortnumeralstyle) applied to it, containing the specified sortIndex incremented by 1 (therefore showing the more user-friendly 1-based numbering system).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | The name of a sort-field to get the [sortNumeral](ListGrid_1.md#attr-listgridsortnumeralstyle) HTML for. |
| sortIndex | [int](../reference.md#type-int) | false | — | The sort index for the field. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — The HTML for this field's sortNumeral

---
## Method: ListGrid.rowMouseUp

### Description
Called when a row receives a mouseup event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object returned from getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.setHeaderSpanButtonProperties

### Description
Method to update properties on a headerSpan's header button at runtime. This property allows customization of any settable properties on the HeaderSpan's header button after it has been generated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | [name](HeaderSpan.md#attr-headerspanname) of span to update |
| properties | [Canvas Properties](#type-canvas-properties) | false | — | new properties to apply to the header button |

---
## Method: ListGrid.getGroupNodeHTML

### Description
Returns the HTML code necessary to render a group node, including icon, title, and padding. The amount of the padding is at least [ListGrid.groupLeadingIndent](ListGrid_1.md#attr-listgridgroupleadingindent) pixels, and an additional [ListGrid.groupIndentSize](ListGrid_1.md#attr-listgridgroupindentsize) pixels for each increasing level of the node.

The result of this method will be displayed to the user for the appropriate row, either in a single cell which spans multiple columns, or in the [ListGrid.groupTitleField](ListGrid_1.md#attr-listgridgrouptitlefield). For the case where group titles are displayed in a cell spanning multiple columns, if this grid has frozen fields, this method may be run for both the frozen and unfrozen body. This method will return the html described above for the frozen body, and an empty string for the unfrozen body (or vice versa depending on [ListGrid.showGroupTitleInFrozenBody](ListGrid_1.md#attr-listgridshowgrouptitleinfrozenbody)). This ensures the groupNodeHTML is not displayed twice.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [Object](../reference.md#type-object) | false | — | Specified group node |
| gridBody | [GridRenderer](#type-gridrenderer) | true | — | The body in which the returned value will be displayed. This parameter allows the default implementation to return an empty string if appropriate for the case where there is both a frozen and unfrozen body. Note that if this parameter may be empty. If not passed, the full group node HTML will be returned. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — The HTML to be displayed in the appropriate row.

---
## Method: ListGrid.getFilterEditorCriteria

### Description
If [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) is true, this method will return the criteria currently displayed in the `filterEditor`. Note that these values may differ from the criteria returned by [ListGrid.getCriteria](#method-listgridgetcriteria) if the filter editor values have been modified without performing an actual filter.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| omitHiddenFields | [Boolean](#type-boolean) | true | — | By default this method will include criteria applied to fields, including criteria that are not actually visible/editable in the filterEditor for the grid. Pass in this parameter to get only values for visible fields returned. |

### Returns

`[Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria)` — criteria currently displayed in the filterEditor

---
## Method: ListGrid.getCellRowSpan

### Description
When using [row spanning](#method-listgridgetrowspan), returns the number of cells spanned by the cell at the given coordinates.

If the passed coordinates are in the middle of a series of spanned cells, the row span of the spanning cell is returned. For example, if row 2 col 0 spans 3 cells, calls to `getCellRowSpan()` for row 2 col 0, row 3 col 0, row 4 col 0 will all return 3.

This method returns row span information for the current rendered cells. In contrast, if the grid is about to be redrawn, a call to `getRowSpan()` may return row span values for how the grid is about to be drawn. Also, user-provided getRowSpan() functions are not required to operate properly when called outside of the grid rendering loop.

**Note:** This method is a utility method for developers - it is not called directly by the grid rendering path and therefore is not intended for override. To set up custom row-spanning behavior, override [ListGrid.getRowSpan](#method-listgridgetrowspan) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row number of cell to return the row span for |
| colNum | [int](../reference.md#type-int) | false | — | column number of cell to return the row span for |

### Returns

`[int](../reference.md#type-int)` — number of cells spanned by the cell that spans through these coordinates

---
## Method: ListGrid.setGroupState

### Description
Reset this grid's grouping to match the [ListGridGroupState](../reference.md#type-listgridgroupstate) object passed in.  
Used to restore previous state retrieved from the grid by a call to [ListGrid.getGroupState](#method-listgridgetgroupstate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupState | [ListGridGroupState](../reference.md#type-listgridgroupstate) | false | — | Object describing the desired grouping state of the grid |

### Groups

- viewState

### See Also

- [ListGrid.getGroupState](#method-listgridgetgroupstate)

---
## Method: ListGrid.getRowRangeDisplayValue

### Description
This method will return a row range summary display value containing the currently visible row range and row count for the data set.

The [RowRangeDisplay](RowRangeDisplay.md#class-rowrangedisplay) label autoChild shows this value as its contents.

The format of the display value is governed by the [RowRangeDisplayStyle](../reference_2.md#type-rowrangedisplaystyle)

### Returns

`[String](#type-string)` — formatted row range summary value

### Groups

- rowRangeDisplay

---
## Method: ListGrid.cellHasChanges

### Description
If this listGrid can be edited, this method will return true if the cell passed in has been edited, but the edits have not yet been saved to the ListGrid's data object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | index of row to check for changes |
| colNum | [int](../reference.md#type-int) | false | — | index of the col to check for changes |

### Returns

`[Boolean](#type-boolean)` — returns true if the cell has unsaved edits

### Groups

- editing

---
## Method: ListGrid.drop

### Description
Handle a drop event. Default implementation supports moving data within this grid or transferring data into the grid from some other component.

Developers wishing to implement custom listGrid record drag and drop behavior should typically use the [ListGrid.recordDrop](#method-listgridrecorddrop) method rather than overriding this method directly.

### Returns

`[boolean](../reference.md#type-boolean)` — true for completion of a successful drag/drop interaction

### Groups

- events
- dragging

### See Also

- [ListGrid.willAcceptDrop](#method-listgridwillacceptdrop)
- [ListGrid.transferDragData](#method-listgridtransferdragdata)

**Flags**: A

---
## Method: ListGrid.setShowRecordComponents

### Description
Setter for the [ListGrid.showRecordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents) attribute

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showRecordComponents | [boolean](../reference.md#type-boolean) | false | — | new value for `this.showRecordComponents` |

### Groups

- recordComponents

---
## Method: ListGrid.refreshCellStyle

### Description
Refresh the styling of an individual cell without redrawing the grid.

The cell's CSS class and CSS text will be refreshed, to the current values returned by getCellStyle() and getCellCSSText() respectively.

The cell's contents (as returned by getCellValue()) will **not** be refreshed. To refresh both styling and contents, call refreshCell() instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number of cell to refresh |
| colNum | [number](#type-number) | false | — | column number of cell to refresh |

### Groups

- appearance

### See Also

- [ListGrid.refreshCell](#method-listgridrefreshcell)

---
## Method: ListGrid.getCellSelection

### Description
When [ListGrid.canSelectCells](ListGrid_1.md#attr-listgridcanselectcells) is active, returns the [CellSelection](CellSelection.md#class-cellselection) object that tracks and manages the current selection. Returns null if [ListGrid.canSelectCells](ListGrid_1.md#attr-listgridcanselectcells) is false.

### Returns

`[CellSelection](#type-cellselection)` — current cellSelection

---
## Method: ListGrid.summaryUpdated

### Description
Notification fired when a user either creates a new summary field or edits an existing summary field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | the summary field |
| summary | [UserSummary](#type-usersummary) | false | — | the new or updated summary definition |

---
## Method: ListGrid.setAutoFitMaxRecords

### Description
Setter for [ListGrid.autoFitMaxRecords](ListGrid_1.md#attr-listgridautofitmaxrecords).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| maxRecords | [int](../reference.md#type-int) | false | — | Maximum number of rows we'll expand to accommodate if [auto fit](ListGrid_1.md#attr-listgridautofitdata) is enabled vertically. |

### Groups

- autoFitData

---
## Method: ListGrid.expandRecord

### Description
Expands a given [record](../reference_2.md#object-listgridrecord) by creating a subcomponent and inserting it in to the record's grid-row. A number of built-in [expansionModes](../reference_2.md#type-expansionmode) are supported by the default implementation of [getExpansionComponent()](#method-listgridgetexpansioncomponent) and you can override that method to provide your own expansion behavior.

Once a record has been expanded, the currently visible expansion component may be retrieved via [ListGrid.getCurrentExpansionComponent](#method-listgridgetcurrentexpansioncomponent).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to expand |

### Groups

- expansionField

---
## Method: ListGrid.deselectRecords

### Description
Deselect a list of [Record](../reference.md#object-record)s passed in explicitly, or by index.

Synonym for `selectRecords(records, false)`

Note that developers may wish to use [ListGrid.deselectRange](#method-listgriddeselectrange) to select a single contiguous range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record)|[number](#type-number) | false | — | records (or row numbers) to deselect |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: ListGrid.refreshFields

### Description
Re-evaluates [ListGridField.showIf](ListGridField.md#method-listgridfieldshowif) for each field, dynamically showing and hiding the appropriate set of fields

---
## Method: ListGrid.isSortField

### Description
Returns `true` if the passed fieldName is in the current sort-specification.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | The name of a field, which may be visible, hidden or existing only in the dataSource |

### Returns

`[Boolean](#type-boolean)` — `true` if the component is sorted by the specified field; `false` otherwise.

**Flags**: A

---
## Method: ListGrid.setCanReorderRecords

### Description
Setter for the [ListGrid.canReorderRecords](ListGrid_1.md#attr-listgridcanreorderrecords) attribute.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canReorderRecords | [boolean](../reference.md#type-boolean) | false | — | new value for `this.canReorderRecords` |

---
## Method: ListGrid.getRowNum

### Description
Synonym of [getRecordIndex()](#method-listgridgetrecordindex).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | the record whose index is to be retrieved |

### Returns

`[int](../reference.md#type-int)` — index of the record, or -1 if not found

---
## Method: ListGrid.removeRecordClick

### Description
Method fired when the user clicks the "remove" icon if [ListGrid.canRemoveRecords](ListGrid_1.md#attr-listgridcanremoverecords) is true. Default behavior will remove the record from the data set, or if we're [deferring removal](ListGrid_1.md#attr-listgriddeferremoval) mark record as removed \[or for records already marked as removed, clear this removed marker\].

If [ListGrid.warnOnRemoval](ListGrid_1.md#attr-listgridwarnonremoval) is set, this method will also show a warning dialog to users allowing them to cancel the removal.

This method may be called directly to cause a record to be removed or marked for removal as if the user had hit the "remove" icon.

May be overridden to perform custom logic on remove click.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | Row on which the icon was clicked |

---
## Method: ListGrid.selectAllRecords

### Description
Select all records.

Note that this method will select records even if [ListGrid.canSelectRecord](#method-listgridcanselectrecord) returns false for the record in question. See also [ListGrid.userSelectAllRecords](#method-listgriduserselectallrecords)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| visibleNodesOnly | [boolean](../reference.md#type-boolean) | true | — | For TreeGrids, or listGrids showing hierarchical [group data](ListGrid_1.md#attr-listgridisgrouped), if `true` is passed for this parameter, only visible nodes will be selected. Nodes embedded in a closed parent folder (and thus hidden from the user) will not be selected. |

---
## Method: ListGrid.getBody

### Description
Returns the primary [body](ListGrid_1.md#attr-listgridbody), which, when there are frozen fields, is the [GridRenderer](GridRenderer.md#class-gridrenderer) used to render the non-frozen portion of the dataset; otherwise, the primary body (the only body) is the GridRenderer used to render the entire dataset.

### Returns

`[GridRenderer](#type-gridrenderer)` — the primary body or null if this ListGrid has not been drawn yet.

---
## Method: ListGrid.getFormattedRowCount

### Description
Returns the [current total row count](#method-listgridgetrowcount) for this grid as a formatted string.

Due to [progressiveLoading](DataSource.md#attr-datasourceprogressiveloading), an exact total row count may not be available. Depending on the current [rowCount status](#method-listgridgetrowcountstatus), this method will return a value in one of the following formats. Note that if the row count is not exact, the numeric value will be rounded to the nearest multiple of [ListGrid.rowCountDisplayPrecision](ListGrid_1.md#attr-listgridrowcountdisplayprecision).

*   `"exact"`: The row count will be formatted using [ListGrid.exactRowCountFormat](ListGrid_1.md#attr-listgridexactrowcountformat)
*   `"minimum"`: The row count will be formatted using [ListGrid.minimumRowCountFormat](ListGrid_1.md#attr-listgridminimumrowcountformat)
*   `"approximate"`: The row count will be formatted using [ListGrid.approximateRowCountFormat](ListGrid_1.md#attr-listgridapproximaterowcountformat)
*   `"maximum"`: The row count will be formatted using [ListGrid.maximumRowCountFormat](ListGrid_1.md#attr-listgridmaximumrowcountformat)
*   `"range"`: The row count range will be formatted using [ListGrid.rangeRowCountFormat](ListGrid_1.md#attr-listgridrangerowcountformat)
*   `"unknown"`: The [ListGrid.unknownRowCountDisplayValue](ListGrid_1.md#attr-listgridunknownrowcountdisplayvalue) will be displayed
*   `"loading"`: The [ListGrid.loadingRowCountDisplayIcon](ListGrid_1.md#attr-listgridloadingrowcountdisplayicon) will be displayed

See also [ListGrid.getRowRangeDisplayValue](#method-listgridgetrowrangedisplayvalue).

### Returns

`[String](#type-string)` — the formatted rowCount display value

### Groups

- rowRangeDisplay

---
## Method: ListGrid.deselectRecord

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
## Method: ListGrid.getFieldName

### Description
Given a column number or field id, return the field name of a field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [number](#type-number)|[ID](#type-id) | false | — | number or id of the field. |

### Returns

`[String](#type-string)` — Name of the field.

### Groups

- display

**Flags**: A

---
## Method: ListGrid.getSavedViewState

### Description
Returns the [view state](../reference_2.md#type-listgridviewstate) for this ListGrid as last saved by the [ListGrid.autoPersistViewState](ListGrid_1.md#attr-listgridautopersistviewstate) setting.

### Returns

`[ListGridViewState](../reference_2.md#type-listgridviewstate)` — last auto-saved view state for the grid.

### Groups

- viewState

### See Also

- [ListGrid.autoPersistViewState](ListGrid_1.md#attr-listgridautopersistviewstate)
- [ListGrid.clearSavedViewState](#method-listgridclearsavedviewstate)

---
## Method: ListGrid.getRollOverCanvas

### Description
This method is called to retrieve the [ListGrid.rollOverCanvas](ListGrid_1.md#attr-listgridrollovercanvas) when the user moves over a new row or cell if [ListGrid.showRollOverCanvas](ListGrid_1.md#attr-listgridshowrollovercanvas) is true, or when the user moves over the selected record if [ListGrid.showSelectedRollOverCanvas](ListGrid_1.md#attr-listgridshowselectedrollovercanvas) is true.

The default implementation uses the [AutoChild](../reference.md#type-autochild) subystem to create the [ListGrid.rollOverCanvas](ListGrid_1.md#attr-listgridrollovercanvas) auto child. It may be overridden for custom behavior.

Note that for efficiency this should not typically create a new Canvas every time that it is called. Instead usually a single rollOver canvas should be created and updated to reflect the current rollOver row if necessary.

Return null to avoid showing a `rollOverCanvas` for this row.

See also [ListGrid.getFrozenRollOverCanvas](#method-listgridgetfrozenrollovercanvas).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | index of the current rollOver row. |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | index of the current rollOver column. This parameter will be null unless [useCellRollOvers](ListGrid_1.md#attr-listgridusecellrollovers) is true for the grid. |

### Returns

`[Canvas](#type-canvas)` — the embedded component

### Groups

- hoverComponents

---
## Method: ListGrid.formatEditorValue

### Description
Formatter to apply to values displayed within editors while a cell is being edited. The value passed to this method is the raw value for the cell.  
If `formatEditorValue` is defined at the field level for some cell being edited, the field level method will be used to format the edit value and this method will not be called for that cell.  
To convert the formatted value displayed within an editor back to a raw value, the `parseEditorValue` method is used.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | raw value for the cell being edited |
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object for the cell. Note: If this is a new row that has not been saved, it has no associated record object. In this case the edit values will be passed in as this parameter. |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number for the cell. |

### Returns

`[Any](#type-any)` — formatted value to display in the editor

### Groups

- editing

### See Also

- [ListGridField.formatEditorValue](ListGridField.md#method-listgridfieldformateditorvalue)
- [ListGrid.parseEditorValue](#method-listgridparseeditorvalue)

---
## Method: ListGrid.shouldIncludeHiliteInSummaryField

### Description
When assembling a value for a [summary field](ListGrid_1.md#attr-listgridcanaddsummaryfields), if a referenced field is hilited, should the hilite HTML be included in the summary field value?

Example use case: Consider a grid containing a numeric field, and a summary field which contains some string value, plus the contents of the numeric field. If a hilite is defined for the grid which turns the numeric field text red when the value is negative, this property will govern whether the number will also be rendered in red within the summary field cells. Any other text in the summary field cells would not be effected by this hilite.

Default implementation returns [includeHilitesInSummaryFields](DataBoundComponent.md#attr-databoundcomponentincludehilitesinsummaryfields).

To control hilites showing in group summaries, see [showHilitesInGroupSummary](ListGrid_1.md#attr-listgridshowhilitesingroupsummary).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| summaryFieldName | [String](#type-string) | false | — | name of the summary field |
| usedFieldName | [String](#type-string) | false | — | name of the field referenced by this summary |

### Returns

`[boolean](../reference.md#type-boolean)` — Return true to include hilites from the used field in the generated summary field value.

---
## Method: ListGrid.setFieldSearchOperator

### Description
Applies a new [search operator](../reference.md#type-operatorid) to a field in the grid's [filter row](ListGrid_1.md#attr-listgridfiltereditor), and updates it's operatorIcon.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

Depending on the field's current filter-value and operator, calls to this method may result in the current filter-value being cleared, and/or a fetch being issued if [filterByCell](ListGrid_1.md#attr-listgridfilterbycell) or [filterOnKeypress](ListGrid_1.md#attr-listgridfilteronkeypress) are set.

In general, if the field has a current filter-value, it will be cleared if

*   the new operator does not require a value (operator-type [none](../reference_2.md#type-operatorvaluetype) - [isBlank](../reference.md#type-operatorid), for example)
*   the current and new operators have different [value-types](../reference_2.md#type-operatorvaluetype) and [ListGrid.allowFilterExpressions](ListGrid_1.md#attr-listgridallowfilterexpressions) is false
*   the item has an [optionDataSource](FormItem.md#attr-formitemoptiondatasource) or valueMap which no longer includes the current value

If `filterOnKeypress` is true, a fetch will be issued if

*   the value was just cleared, in one of the ways listed above
*   the operator changes while there is a current value
*   the new operator does not require a value and the old one did

If passed null, the field's operator will be cleared, reverting it to its [default operator](ListGridField.md#attr-listgridfieldfilteroperator) and, if [ListGrid.alwaysShowOperatorIcon](ListGrid_1.md#attr-listgridalwaysshowoperatoricon) is false, the operatorIcon is hidden. See [ListGrid.clearFieldSearchOperator](#method-listgridclearfieldsearchoperator) for an alternative way to clear a field's operator.

To retrieve a field's current search operator, use [ListGrid.getFieldSearchOperator](#method-listgridgetfieldsearchoperator).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | name of the field to apply a new search operator to |
| operator | [OperatorId](../reference.md#type-operatorid) | false | — | id of the search operator to apply |

---
## Method: ListGrid.editorExit

### Description
Callback fired when the user attempts to navigate away from the current edit cell, or complete the current edit.

Return false from this method to cancel the default behavior (Saving / cancelling the current edit / moving to the next edit cell).

This callback is typically used to dynamically update values or value maps for related fields (via [ListGrid.setEditValue](#method-listgridseteditvalue) and [ListGrid.setEditorValueMap](#method-listgridseteditorvaluemap) respectively, or to implement custom navigation (via [startEditing(rowNum,colNum)](#method-listgridstartediting).

Can be overridden at the field level as field.editorExit.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editCompletionEvent | [EditCompletionEvent](../reference.md#type-editcompletionevent) | false | — | How was the edit completion fired? |
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for the cell being edited |
| newValue | [Any](#type-any) | false | — | new edit value for the cell being edited. Note that if the user has not made any changes this will be undefined |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — Returning false from this method will cancel the default behavior (for example saving the row) and leave the editor visible and focus in this edit cell.

### Groups

- editing

### See Also

- [ListGridField.editorExit](ListGridField.md#method-listgridfieldeditorexit)

---
## Method: ListGrid.getEditField

### Description
Returns the field object associated with cell currently being edited

### Returns

`[Object](../reference.md#type-object)` — Field object definition

### Groups

- editing

---
## Method: ListGrid.clearFilterWindowCriteria

### Description
Clears criteria applied to this grid via the [advanced filter window](ListGrid_1.md#attr-listgridallowfilterwindow) and issues a re-filter.

To clear all user-editable criteria, see [ListGrid.clearAllCriteria](#method-listgridclearallcriteria).

---
## Method: ListGrid.groupByComplete

### Description
Callback fired when the listGrid is grouped or ungrouped.

Unlike [ListGrid.handleGroupBy](#method-listgridhandlegroupby), this notification will fire when grouping is complete, and the [ListGrid.data](ListGrid_1.md#attr-listgriddata) object has been updated. On successful grouping the `fields` argument will list the new grouping and the [ListGrid.groupTree](ListGrid_1.md#attr-listgridgrouptree) will have been updated to reflect the grouped data.

Note that the `fields` argument may be an empty array if the data is not grouped. This implies that a user or developer explicitly ungrouped the grid, or that a groupBy attempt failed due to the data length exceeding [ListGrid.groupByMaxRecords](ListGrid_1.md#attr-listgridgroupbymaxrecords).

By design, this method is not called when the data is regrouped, either [programmatically](#method-listgridregroup), or in response to new data arriving from the server. You can use the callback [ListGrid.groupTreeChanged](#method-listgridgrouptreechanged) to be notified in that situation.

If you monitor only this method and call [ListGrid.groupBy](#method-listgridgroupby) before data is fetched, the notification that you'll receive will be for grouping the initial (perhaps empty) data set only. To have this method actually trigger when grouping of the fetched data is done, you should avoid calling [ListGrid.groupBy](#method-listgridgroupby) before the initial fetch, and instead do it in the the [fetch callback](#method-listgridfetchdata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fields | [Array of String](#type-array-of-string) | false | — | ListGrid field names by which the grid is now grouped. If the grid is currently not grouped, this parameter will be an empty array. |

### Groups

- grouping

### See Also

- [ListGrid.handleGroupBy](#method-listgridhandlegroupby)
- [ListGrid.groupTreeChanged](#method-listgridgrouptreechanged)

---
## Method: ListGrid.filterEditorSubmit

### Description
Optional notification fired when the user performs a filter using the [Filter Editor](ListGrid_1.md#attr-listgridshowfiltereditor). Useful for applying additional criteria not available in the filterEditor. Note that it is often easiest to do this with the [SearchForm](SearchForm.md#class-searchform) attribute, which requires no code.

May fire as criteria values are being edited if [ListGrid.filterByCell](ListGrid_1.md#attr-listgridfilterbycell) or [ListGrid.filterOnKeypress](ListGrid_1.md#attr-listgridfilteronkeypress) is true, otherwise will fire when the user clicks the filter button or presses the Enter key while focus is in the Filter Editor.

Return false to cancel the default behavior - you **must** cancel the default behavior if your code is going to call [ListGrid.filterData](#method-listgridfilterdata), [ListGrid.setCriteria](#method-listgridsetcriteria) or any other API that affects the criteria applied to the grid.

The `criteria` parameter contains the current criteria applied to the grid including edits the user has just made using the Filter Editor and those applied with the [advanced filtering dialog](ListGrid_1.md#method-listgridshowfilterwindow). A call to [ListGrid.getFilterEditorCriteria](#method-listgridgetfiltereditorcriteria) does not include the [advanced filtering criteria](#method-listgridgetfilterwindowcriteria).

If you wish to access the `criteria` applied to the grid without picking up any edits to the Filter Editor, use [ListGrid.getCriteria](#method-listgridgetcriteria) instead.

Developers may wish to perform a filter using the Filter Editor values from code running outside the standard filterEditorSubmit flow. For example, if you wanted a confirmation dialog to be shown before filtering was performed, you would cancel the default behavior as described above, but then need to replicate the default behavior once the user confirms that they want to proceed. To replicate the default behavior, just call:

```
  grid.filterData(grid.getFilterEditorCriteria());
 
```
or, to ensure the specified [ListGrid.autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle) is picked up
```
  grid.filterData(grid.getFilterEditorCriteria(), 
          null, {textMatchStyle:grid.autoFetchTextMatchStyle});
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | criteria derived from the filter editor values |

### Returns

`[boolean](../reference.md#type-boolean)` — returning false will suppress the filter from occurring

### See Also

- [ListGrid.criteriaChanged](#method-listgridcriteriachanged)

---
## Method: ListGrid.showField

### Description
Force a field to be shown. This method does not add new fields to the grid, it simply changes field visibility. If a field.showIf expression exists, it will be destroyed.

Note: for showing multiple fields it is more efficient to call [ListGrid.showFields](ListGrid_1.md#method-listgridshowfields) than to call this method repeatedly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [String](#type-string)|[ListGridField](#type-listgridfield) | false | — | field to show |
| suppressRelayout | [boolean](../reference.md#type-boolean) | true | — | If passed, don't resize non-explicitly sized columns to fill the available space. |

---
## Method: ListGrid.getGridSummaryData

### Description
This method returns the data to be displayed in the [ListGrid.summaryRow](ListGrid_1.md#attr-listgridsummaryrow) when [ListGrid.showGridSummary](ListGrid_1.md#attr-listgridshowgridsummary) is true.

By default this will call [ListGrid.getGridSummary](#method-listgridgetgridsummary) for each field and generate an array of records containing the resulting values.

This method may be overridden for custom grid-summary display, and may return multiple records if more than one summary row is desired.

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — summary record(s)

---
## Method: ListGrid.getGridSummary

### Description
When [ListGrid.showGridSummary](ListGrid_1.md#attr-listgridshowgridsummary) is `true` this method is called for each field which will show a grid summary value (as described in [ListGridField.showGridSummary](ListGridField.md#attr-listgridfieldshowgridsummary)) to get the summary value to display below the relevant column.

The default implementation is as follows:

*   If this is a databound grid and not all data is loaded, returns null for every field
*   Otherwise if [ListGridField.getGridSummary](ListGridField.md#method-listgridfieldgetgridsummary) is defined, calls that method passing in the current data set for the grid
*   If [ListGridField.getGridSummary](ListGridField.md#method-listgridfieldgetgridsummary) is undefined, makes use of the [standard summary function](#method-listgridgetgridsummaryfunction) for the field to calculate the summary based on the current data set

This method may return an array of values. This implies that the grid summary should show multiple rows. Note that if a field has more than one summaryFunction specified, this method will pick up values from each summary function and return them in an array, meaning these summaries will show up on multiple rows in the grid.

This method may be overridden to completely customize the summary value displayed for columns in this grid. An example use case would be when summary information is available on the client and does not need to be calculated directly from the data.

If you update this method after the grid has been drawn so that new summaries will be generated from the same data, the changes won't be reflected in any [redraws](Canvas.md#method-canvasredraw) or other interaction until the next [data change](#method-listgriddatachanged), unless you call [ListGrid.recalculateGridSummary](#method-listgridrecalculategridsummary).

**Note:** this method will not be called if [ListGrid.summaryRowDataSource](ListGrid_1.md#attr-listgridsummaryrowdatasource) is specified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field for which the summary value should be returned |

### Returns

`[Any](#type-any)` — summary value to display for the specified field.

**Flags**: A

---
## Method: ListGrid.startEditing

### Description
Start inline editing at the provided coordinates.

Invoked when a cell is editable and the `editEvent` occurs on that cell. Can also be invoked explicitly.

If this method is called while editing is already in progress, the value from the current editCell will either be stored locally as a temporary edit value, or saved via 'saveEdits()' depending on `this.saveByCell`, and the position of the new edit cell.  
Will update the UI to show the editor for the new cell, and put focus in it unless explicitly suppressed by the optional `suppressFocus` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | true | — | Row number of the cell to edit. Defaults to first editable row |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column number of the cell to edit. Defaults to first editable column |
| suppressFocus | [Boolean](#type-boolean) | true | — | If passed this parameter suppresses the default behavior of focusing in the edit form item when the editor is shown. |

### Returns

`[Boolean](#type-boolean)` — true if we are editing the cell, false if not editing for some reason

### Groups

- editing

### See Also

- [ListGrid.canEditCell](#method-listgridcaneditcell)
- [ListGrid.editEvent](ListGrid_1.md#attr-listgrideditevent)

**Flags**: A

---
## Method: ListGrid.recalculateSummaries

### Description
Recalculates values for fields with [summary-functions](ListGridField.md#attr-listgridfieldrecordsummaryfunction) or [user formulae](ListGridField.md#attr-listgridfielduserformula) defined and for values displayed in the [grid summary](ListGrid_1.md#attr-listgridshowgridsummary) and [group summary rows](ListGrid_1.md#attr-listgridshowgroupsummary).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record) | true | — | Optional array of records to recalculate summaries for, or null for all records |
| fields | [Array of ListGridField](#type-array-of-listgridfield) | true | — | Optional array of fields to recalculate summaries for, or null for all fields

Note that the records should be from [ListGrid.data](ListGrid_1.md#attr-listgriddata); thus, if the grid is grouped, the records should be from the grouped data rather than [ListGrid.originalData](ListGrid_1.md#attr-listgridoriginaldata). |

---
## Method: ListGrid.configureGrouping

### Description
Open a MultiGroupDialog to configure the fields used for grouping.

---
## Method: ListGrid.invalidateRecordComponents

### Description
Invalidates the currently visible set of [recordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents) and gets fresh ones for the visible rows in the grid according to the [ListGrid.recordComponentPoolingMode](ListGrid_1.md#attr-listgridrecordcomponentpoolingmode)

See also [ListGrid.refreshRecordComponent](#method-listgridrefreshrecordcomponent) which allows you to refresh a specific recordComponent

### Groups

- recordComponents

---
## Method: ListGrid.getFormattedRowRange

### Description
Uses the [ListGrid.rowRangeFormat](ListGrid_1.md#attr-listgridrowrangeformat) to return a formatted display value showing the currently visible set of rows in the listGrid viewport.

If this listGrid has never been drawn, so has no meaningful "viewport", this method will return an empty string.

See also [ListGrid.getRowRangeDisplayValue](#method-listgridgetrowrangedisplayvalue)

### Returns

`[String](#type-string)` — formatted row range value

---
## Method: ListGrid.getOriginalData

### Description
Returns the original, ungrouped data in the grid. If the grid is ungrouped, returns [ListGrid.data](ListGrid_1.md#attr-listgriddata).

### Returns

`[Object](../reference.md#type-object)` — The ungrouped data that is being displayed and observed

### Groups

- grouping

---
## Method: ListGrid.getTotalRows

### Description
Return the total number of rows in the grid.

Note that, when creating new rows via inline editing, this can be more than the total number of rows in the dataset (that is, grid.data.getLength())

### Returns

`[int](../reference.md#type-int)` — total number of rows in the grid

---
## Method: ListGrid.isRowNumberField

### Description
Identifies whether the passed-in field is the specially generated [rowNumberField](ListGrid_1.md#attr-listgridrownumberfield) used when [ListGrid.showRowNumbers](ListGrid_1.md#attr-listgridshowrownumbers) is true. Use this method in your custom event handlers to avoid inappropriately performing actions when the rowNumberField is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field to test |

### Returns

`[Boolean](#type-boolean)` — whether the provided field is the rowNumberField

### Groups

- rowNumberField

---
## Method: ListGrid.getRecordComponent

### Description
Retrieve the [recordComponent](ListGrid_1.md#attr-listgridshowrecordcomponents) currently being shown at the given coordinates.

`recordComponents` are dynamically assigned to row/cell coordinates and, depending on the [ListGrid.recordComponentPoolingMode](ListGrid_1.md#attr-listgridrecordcomponentpoolingmode), any kind of redraw of the containing ListGrid (due to sort change, scrolling, editing etc) may cause a `recordComponent` to be assigned to another row, [clear()ed](Canvas.md#method-canvasclear) or permanently [destroy()ed](Canvas.md#method-canvasdestroy).

Hence you should always call `getRecordComponent()` right before taking action on the `recordComponent` - don't cache the component associated with row/cell coordinate. Similarly, it's invalid to call `getRecordComponent()` during a redraw (for example, from [formatting](ListGridField.md#method-listgridfieldformatcellvalue) code).

It's always invalid to try to use a `recordComponent` outside of a ListGrid (by eg adding it to some other layout).

If [ListGrid.showRecordComponentsByCell](ListGrid_1.md#attr-listgridshowrecordcomponentsbycell) is true and the colNum parameter is not passed, the call will return the first component in the passed rowNum.

Returns null if there is no component at the specified coordinates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row number to get record component for |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | optional column number to get the record component for |

### Returns

`[Canvas](#type-canvas)` — record component, or null if none is shown at these coordintes

### Groups

- recordComponents

### See Also

- [ListGrid.recordScreen](ListGrid_1.md#attr-listgridrecordscreen)

---
## Method: ListGrid.rowMouseDown

### Description
Called when a row receives a mousedown event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record object returned from 'getCellRecord()' |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.addEmbeddedComponent

### Description
Attaches the component to the provided record. If `position` is specified as `"within"` [Canvas.snapTo](Canvas.md#attr-canvassnapto) and [Canvas.snapOffsetLeft](Canvas.md#attr-canvassnapoffsetleft), [Canvas.snapOffsetTop](Canvas.md#attr-canvassnapoffsettop) may be set to specify where the component will render within the cell or record. If unset, for components embedded within a record we will default to embedding at the top/left coordinate, and for components embedded within a cell, we will respect the align / valign properties for the cell in question. Any percentage sizing will be interpreted as percentage of row size.

Otherwise it will appear to be embedded within the record, underneath the field values.

Embedded components become children of the grid and will stay attached to a record through scrolling, sorting and other operations that cause records to shift position.

If `position` is set to `"expand"`, embedded components may offer a resize interface, eg, by setting [canDragResize](ListGridField.md#attr-listgridfieldcandragresize):true, and the grid will react accordingly, growing or shrinking the record to match the embedded component's new extents.

Embedded components can be explicitly removed with [ListGrid.removeEmbeddedComponent](#method-listgridremoveembeddedcomponent).

If a record is removed from the dataset or is replaced in the dataset, for example, it is eliminated through filtering (removes record) or is successfully edited in a databound grid (replaces record), the component is cleared but not logically removed from the grid. It is the responsibility of code that sets up the embedded component to remove it if the record is removed from the dataSet.

When embedding components will result in variable height records, you should switch on [virtualScrolling](ListGrid_1.md#attr-listgridvirtualscrolling).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| component | [Canvas](#type-canvas) | false | — | component to embed |
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to attach the component to |
| rowNum | [Integer](../reference_2.md#type-integer) | true | — | rowNum of the record to attach the component to |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | colNum in which to embed the component |
| position | [EmbeddedPosition](../reference_2.md#type-embeddedposition) | true | — | positioning with respect to the record or cell (Defaults to "expand"). |

**Flags**: A

---
## Method: ListGrid.clearFieldError

### Description
Clears any validation errors for some cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row index of cell to add validation error for |
| fieldName | [number](#type-number)|[String](#type-string) | false | — | col index or field name of cell to add validation error for |

### Groups

- gridValidation

### See Also

- [ListGrid.setFieldError](#method-listgridsetfielderror)

---
## Method: ListGrid.selectionUpdated

### Description
Called when the selection changes. Note that this method fires exactly once for any given change to the selection unlike the [selectionChanged](#method-listgridselectionchanged) event.

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
## Method: ListGrid.setHeaderSpanHeaderTitle

### Description
Update the headerTitle of a [headerSpan](ListGrid_1.md#attr-listgridheaderspans) dynamically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | name of the headerSpan, as specified via [HeaderSpan.name](HeaderSpan.md#attr-headerspanname). |
| newTitle | [String](#type-string) | false | — | new headerTitle for the headerSpan |

### Groups

- headerSpan

---
## Method: ListGrid.setHeaderRadius

### Description
Setter for [ListGrid.headerRadius](ListGrid_1.md#attr-listgridheaderradius), which provides rounded corners for this grid's [header area](ListGrid_1.md#attr-listgridshowheader).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| headerRadius | [String](#type-string) | false | — | any CSS border-radius string, with 1 to 4 space-separated sizes |

---
## Method: ListGrid.setFieldTitle

### Description
Change the title of a field after the grid is created.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [int](../reference.md#type-int)|[String](#type-string) | false | — | name of the field, or index. |
| title | [String](#type-string) | false | — | new title |

---
## Method: ListGrid.ungroup

### Description
Removes the grouping from the listGrid, restoring its original data

---
## Method: ListGrid.markForRedraw

### Description
Marks the widget as "dirty" so that it will be added to a queue for redraw. Redraw of dirty components is handled by a looping timer and will after a very short delay (typically less than 100ms). In most cases it is recommended that developers use `markForRedraw()` instead of calling [Canvas.redraw](Canvas.md#method-canvasredraw) directly. Since this method queues the redraw, multiple calls to markForRedraw() within a single thread of execution will only lead to a single DOM manipulation which greatly improves application performance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [String](#type-string) | true | "no reason provided" | reason for performing the redraw |

### Groups

- drawing

---
## Method: ListGrid.recordDoubleClick

### Description
Executed when the listGrid receives a 'doubleClick' event on an enabled, non-separator record. The default implementation does nothing -- override to perform some action when any record or field is double clicked.  
A record event handler can be specified either as a function to execute, or as a string of script to evaluate. If the handler is defined as a string of script, all the parameters below will be available as variables for use in the script.  
To do something specific if a particular field is double clicked, add a recordDoubleClick method or string of script to that field (same parameters) when you're setting up the list.  
**Notes:**

*   This will not be called if the click is below the last item of the list.
*   This method is called from the default implementation of [ListGrid.rowDoubleClick](#method-listgridrowdoubleclick), so if that method is overridden this method may not be fired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [ListGrid](#type-listgrid) | false | — | the listGrid that contains the doubleclick event |
| record | [ListGridRecord](#type-listgridrecord) | false | — | the record that was double-clicked |
| recordNum | [number](#type-number) | false | — | number of the record clicked on in the current set of displayed records (starts with 0) |
| field | [ListGridField](#type-listgridfield) | false | — | the field that was clicked on (field definition) |
| fieldNum | [number](#type-number) | false | — | number of the field clicked on in the listGrid.fields array |
| value | [Object](../reference.md#type-object) | false | — | value of the cell (after valueMap, etc. applied) |
| rawValue | [Object](../reference.md#type-object) | false | — | raw value of the cell (before valueMap, etc applied) |
| editedRecord | [ListGridRecord](#type-listgridrecord) | false | — | the clicked record with any unsaved edit values overlaid (see `listGrid.getEditedRecord()`). |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel event bubbling

### Groups

- events

### See Also

- [ListGrid.rowDoubleClick](#method-listgridrowdoubleclick)

---
## Method: ListGrid.getRowRangeDisplay

### Description
This method will create and return a [RowRangeDisplay](RowRangeDisplay.md#class-rowrangedisplay) autoChild with [RowRangeDisplay.sourceGrid](RowRangeDisplay.md#attr-rowrangedisplaysourcegrid) set to this listGrid.

Note that this method will only create one rowRangeDisplay instance. Calling it repeatedly will return the same canvas.

### Returns

`[RowRangeDisplay](#type-rowrangedisplay)` — RowRangeDisplay component

### Groups

- rowRangeDisplay

---
## Method: ListGrid.loadAllRecords

### Description
Loads all records that match this grid's current filter-criteria, optionally firing a callback when the data arrives.

If the length of the data is [not known](ResultSet.md#method-resultsetlengthisknown), or is greater than the passed _maxRecords_, this call returns false. No fetch is issued and the _callback_, if passed, is not fired.

If all data is [already loaded](ResultSet.md#method-resultsetallmatchingrowscached), no fetch is issued and this call returns true. The _callback_, if passed, will be fired, but its parameters will be null, since there was no fetch to provide the values from.

In all other cases, this call returns true and a fetch is issued for all necessary records. When the data arrives, the _callback_ is fired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| maxRecords | [Integer](../reference_2.md#type-integer) | true | — | optional maximum record count - if passed, no fetch takes place if maxRecords is below the known length of the data |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to fire if a fetch is issued - if all data was already loaded, the callback is fired with no parameters |

### Returns

`[Boolean](#type-boolean)` — true if a fetch was made or was not needed - false otherwise

---
## Method: ListGrid.getSelectedState

### Description
For components bound to a [dataSource](ListGrid_1.md#attr-listgriddatasource) with records identified by unique [primaryKeys](DataSourceField.md#attr-datasourcefieldprimarykey), this method returns a snapshot of the component's current selection, as a [ListGridSelectedState](../reference_2.md#type-listgridselectedstate) object.  
This object can be passed to [ListGrid.setSelectedState](#method-listgridsetselectedstate) to reset this grid's current selection state (assuming the same data is present in the grid).  
Selected state is not supported if the component has no dataSource, or the dataSource has no primaryKey fields.

### Returns

`[ListGridSelectedState](../reference_2.md#type-listgridselectedstate)` — current state of this grid's selection

### Groups

- viewState

### See Also

- [ListGrid.setSelectedState](#method-listgridsetselectedstate)

---
## Method: ListGrid.getSortByGroupFirst

### Description
—

### See Also

- [ListGrid.sortByGroupFirst](ListGrid_1.md#attr-listgridsortbygroupfirst)

**Flags**: A

---
## Method: ListGrid.getRowCount

### Description
Retrieves the [row count](ResultSet.md#method-resultsetgetrowcount) for the grid, which may differ from the reported [data length](ResultSet.md#method-resultsetgetlength) if [progressive loading](DataSource.md#attr-datasourceprogressiveloading) is enabled.

See also [ListGrid.getRowCountStatus](#method-listgridgetrowcountstatus)

### Returns

`[Integer](../reference_2.md#type-integer)` — current row count for the grid

### Groups

- rowRangeDisplay

---
## Method: ListGrid.getEditorValueIcons

### Description
Returns the valueIcons for a field when it is displayed in the editor while editing some record. Default implementation will return [ListGridField.editorValueIcons](ListGridField.md#attr-listgridfieldeditorvalueicons) if specified otherwise [ListGridField.valueIcons](ListGridField.md#attr-listgridfieldvalueicons)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [Object](../reference.md#type-object) | false | — | field definition |
| values | [Object](../reference.md#type-object) | false | — | current edit values for the record |

### Returns

`[Object](../reference.md#type-object)` — valueIcons for the editor

### Groups

- imageColumns

---
## Method: ListGrid.removeSelectedData

### Description
Remove the currently selected records from this component. If this is a databound grid, the records will be removed directly from the DataSource. The grid will automatically be updated if the record deletion succeeds.

If no records are selected, no action is taken and neither callback will be called.

For a grid with no DataSource or where `saveLocally` is true, the data removal is performed on the client and both callbacks will fire with no arguments.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to fire when each record has been removed |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |
| queueCallback | [RPCQueueCallback](#type-rpcqueuecallback) | true | — | callback to fire after all selected data has been removed |

### Groups

- dataBoundComponentMethods

---
## Method: ListGrid.fieldStateChanged

### Description
Notification method executed when columns are resized or reordered, or fields are shown or hidden, frozen or unfrozen. Has no default implementation.

### Groups

- fieldState

### See Also

- [ListGrid.viewStateChanged](#method-listgridviewstatechanged)

---
## Method: ListGrid.getVisibleRows

### Description
Get the rows that are currently visible in the viewport, as an array of \[firstRowNum, lastRowNum\].

If the grid contains no records, will return \[-1,-1\]. Will also return \[-1,-1\] if called at an invalid time (for example, data is in the process of being fetched - see [ResultSet.lengthIsKnown](ResultSet.md#method-resultsetlengthisknown)).

### Returns

`[Array of Integer](#type-array-of-integer)` — —

---
## Method: ListGrid.setShowHeader

### Description
Show or hide the ListGrid header.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../reference.md#type-boolean) | false | — | true to show the header, false to hide it. |

### Groups

- gridHeader

---
## Method: ListGrid.getRowErrors

### Description
Returns any currently stored validation errors for this row in the following format:  
  `{fieldName:[array of error messages], ...}`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | index of row to check for validation errors. |

### Returns

`[Object](../reference.md#type-object)` — object showing validation error arrays by field for the row passed in - if no validation errors stored for the row, null is returned.

### Groups

- gridValidation

### See Also

- [ListGrid.getCellErrors](#method-listgridgetcellerrors)

---
## Method: ListGrid.getEditedCell

### Description
Returns the current value of a cell. If the cell has an outstanding edit value, this will be returned, otherwise the underlying value of the record will be returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [number](#type-number)|[Object](../reference.md#type-object) | false | — | rowNum of the record being edited, or an Object containing values for all the record's primary keys |
| field | [number](#type-number)|[String](#type-string) | false | — | colNum or fieldName of the cell |

### Returns

`[Any](#type-any)` — Current edit value, or underlying value for the cell

### Groups

- editing

---
## Method: ListGrid.parseEditorValue

### Description
Method used to convert the value displayed in an editor for some cell being edited into a raw value for saving.  
If `parseEditorValue` is defined at the field level for some cell being edited, the field level method will be used to parse the edit value and this method will not be called for that cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value displayed in the editor for the cell |
| record | [ListGridRecord](#type-listgridrecord) | false | — | record object for the row being edited. May be null if this is a new row being added to the end of the list. |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number for the cell. |

### Returns

`[Any](#type-any)` — value in raw format

### Groups

- editing

### See Also

- [ListGridField.parseEditorValue](ListGridField.md#method-listgridfieldparseeditorvalue)
- [ListGrid.formatEditorValue](#method-listgridformateditorvalue)

---
## Method: ListGrid.regroup

### Description
Programmatically regroup the grid according to the current grouping configuration.

### See Also

- [ListGrid.groupBy](#method-listgridgroupby)

---
## Method: ListGrid.applyCellData

### Description
Applies a set of Records containing coordinate-based data as returned by [ListGrid.getSelectedCellData](#method-listgridgetselectedcelldata) and applies the data at the current selection.

For consistency with Excel, given a record in the cellData, after the data value with the most negative column index is found, the rest of the values in the record are applied contiguously to the right of it, using the positional data for ordering only.

Will only modify cells in the grid which are editable, and changes will be applied as editValues, exactly as though the user had typed the values in (see [Grid Editing Overview](../kb_topics/editing.md#kb-topic-grid-editing)).

See also [ListGrid.applyRecordData](#method-listgridapplyrecorddata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellData | [RecordList](#type-recordlist) | false | — | list of Records as described above |

---
## Method: ListGrid.selectSingleRecord

### Description
Select a single [Record](../reference.md#object-record) passed in explicitly, or by index, and deselect everything else. When programmatic selection of records is a requirement and [selectionType()](ListGrid_1.md#attr-listgridselectiontype) is "single", use this method rather than [selectRecord()](DataBoundComponent.md#method-databoundcomponentselectrecord) to enforce mutually-exclusive record-selection.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record)|[number](#type-number) | false | — | record (or row number) to select |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: ListGrid.headerDoubleClick

### Description
Handle a double click in the list header.

By default, calls [ListGrid.autoFitField](#method-listgridautofitfield) if [ListGrid.canAutoFitFields](ListGrid_1.md#attr-listgridcanautofitfields) is true and [ListGrid.headerAutoFitEvent](ListGrid_1.md#attr-listgridheaderautofitevent) is `"doubleClick"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [number](#type-number) | false | — | field number for the header that was clicked |

### Groups

- events
- gridHeader

**Flags**: A

---
## Method: ListGrid.setAlternateBodyStyleName

### Description
Update the [alternateBodyStyleName](ListGrid_1.md#attr-listgridalternatebodystylename) for this listGrid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| styleName | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new body style name when showing alternateRecordStyles |

---
## Method: ListGrid.getDefaultFormattedValue

### Description
Get the value for some cell with default formatters applied, but without calling any custom [ListGridField.formatCellValue](ListGridField.md#method-listgridfieldformatcellvalue) or [ListGrid.formatCellValue](#method-listgridformatcellvalue) methods.

This method is useful for cases where a developer wishes to conditionally customize a cell's formatting, but needs to see what the default formatted value would be.

For example - a developer might wish to apply a custom [formatter](ListGridField.md#method-listgridfieldformatcellvalue) to some `link` type field, and be able to return the default active link HTML in some cases. In this case a formatter could check for the conditions in which custom formatting should be applied and run appropriate custom logic to generate a value for display - otherwise return the result of this method to leave the standard formatted-value intact.

This method applies standard formatting such as [ListGridField.valueMap](ListGridField.md#attr-listgridfieldvaluemap) mapping, [ListGridField.displayField](ListGridField.md#attr-listgridfielddisplayfield) substitution, [ListGridField.format](ListGridField.md#attr-listgridfieldformat) application, and type-specific formatters. The [ListGrid.useLegacyDefaultFormattedValue](ListGrid_1.md#attr-listgriduselegacydefaultformattedvalue) flag can be used to revert to legacy behavior where these formatting steps were not applied.

For other use cases, see also:

*   [ListGrid.getFormattedValue](#method-listgridgetformattedvalue) - get fully formatted value including all custom formatters
*   [ListGrid.getDefaultFormattedFieldValue](ListGrid_1.md#method-listgridgetdefaultformattedfieldvalue) - get formatted value with field-level formatters only

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the cell's record object |
| rowNum | [int](../reference.md#type-int) | false | — | rowNum for the cell |
| colNum | [int](../reference.md#type-int) | false | — | colNum for the cell |

### Returns

`[String](#type-string)` — Cell value with default formatters applied

### See Also

- [ListGrid.getFormattedValue](#method-listgridgetformattedvalue)
- [ListGridField.formatCellValue](ListGridField.md#method-listgridfieldformatcellvalue)

**Flags**: A

---
## Method: ListGrid.showAIHiliteWindow

### Description
Shows the [ListGrid.aiFilterWindow](ListGrid_1.md#attr-listgridaifilterwindow), which allows the user to ask the AI to filter data by describing which records should be included.

---
## Method: ListGrid.removeData

### Description
Remove a record from this ListGrid.

If this grid is bound to a DataSource, it will perform a DataSource "remove" operation to remove records from this component's DataSource.

Otherwise the data will be removed from the grid's [data](ListGrid_1.md#attr-listgriddata) object.

To make changes to the local data object even when a DataSource is present, use [ListGrid.saveLocally](ListGrid_1.md#attr-listgridsavelocally).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Record](#type-record) | false | — | listGrid record, or primary key values of record to delete. |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | method to call on operation completion. Note that if this is method does not trigger a dataSource remove operation, the callback will still be fired when the data has been removed, but the `dsResponse` parameter will be null. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on any DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: ListGrid.showAIFilterWindow

### Description
Shows the [ListGrid.aiFilterWindow](ListGrid_1.md#attr-listgridaifilterwindow), which allows the user to ask the AI to filter data by describing which records should be included.

---
## Method: ListGrid.getAutoFitMaxWidth

### Description
Returns the [ListGrid.autoFitMaxWidth](ListGrid_1.md#attr-listgridautofitmaxwidth). Note that this method always returns an integer value - autoFitMaxWidth specified as a percentage will be resolved to a pixel value before being returned.

### Returns

`[Integer](../reference_2.md#type-integer)` — autoFitMaxWidth pixel value

### Groups

- autoFitData

---
## Method: ListGrid.setAutoFitData

### Description
Setter for [ListGrid.autoFitData](ListGrid_1.md#attr-listgridautofitdata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoFitData | [Autofit](../reference_2.md#type-autofit) | false | — | One of `"vertical"`, `"horizontal"` or `"both"`. To disable auto fit behavior, pass in `null`. |

### Groups

- autoFitData

---
## Method: ListGrid.refreshRow

### Description
Refresh an entire row of cells without redrawing the grid.

The cells' values, CSS classes, and CSS text will be refreshed, to the current values returned by getCellValue(), getCellStyle() and getCellCSSText(), respectively. Also, if displaying a standard hover (not a hover component), re-checks to see if the hover should continue to be displayed, hiding the hover if not, or updating the hover if so.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number of cell to refresh |

### Groups

- appearance

### See Also

- [ListGrid.refreshCellStyle](#method-listgridrefreshcellstyle)
- [ListGrid.refreshCell](#method-listgridrefreshcell)

---
## Method: ListGrid.setUserFormulaText

### Description
Updates the [UserFormula.text](UserFormula.md#attr-userformulatext) of the specified field. This method is preferred over setting the 'text' property directly because it also updates any component dependencies and recalculates the field. If the formula text is not passed or is `undefined`, it is assumed that the formula has already been updated and only the dependency propagation logic will run.

Known component dependencies are:

*   the cached record values of the formula for this field
*   the common formula variable => field name map maintained by the component for calls to the [FormulaBuilder](FormulaBuilder.md#class-formulabuilder)
*   any generated field that references the field's calculated values

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[String](#type-string) | false | — | field owning the formula |
| text | [String](#type-string) | true | — | optional formula text to install |

### See Also

- [ListGridField.userFormula](ListGridField.md#attr-listgridfielduserformula)

---
## Method: ListGrid.addData

### Description
Perform a DataSource "add" operation to add new records to this component's DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newRecord | [Record](#type-record) | false | — | new record |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | method to call on operation completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: ListGrid.scrollToRow

### Description
Scroll the grid to specified row such that the row appears near the center of the viewport, loading data if necessary.

See [ListGrid.scrollToCell](#method-listgridscrolltocell) for a full description of how this method interacts with incremental loading and rendering of data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | Row index of the cell to scroll into view |
| yPosition | [VerticalAlignment](../reference.md#type-verticalalignment) | true | — | Vertical position of scrolled row (optional) |

### Groups

- scrolling

---
## Method: ListGrid.setGroupByFieldSummaries

### Description
Setter for the [ListGrid.groupByFieldSummaries](ListGrid_1.md#attr-listgridgroupbyfieldsummaries) attribute

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupByFieldSummaries | [Array of String](#type-array-of-string) | false | — | new value for this.groupByFieldSummaries |

---
## Method: ListGrid.setAlternateRecordStyles

### Description
Setter for [ListGrid.alternateRecordStyles](ListGrid_1.md#attr-listgridalternaterecordstyles)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| alternateStyles | [boolean](../reference.md#type-boolean) | false | — | New value for `this.alternateRecordStyles` |

---
## Method: ListGrid.getEditorType

### Description
Returns the form item type (Class Name) to display for a field when it is displayed in the editor while editing some record.  
Default implementation will return field.editorType if specified. If not specified, the default form item for the appropriate data type will be displayed - can be overridden to provide a different specific form item type for some field based on the record/field data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field definition field for which we need a valueMap |
| values | [Object](../reference.md#type-object) | false | — | current edit values for the record (may be null, if editing a new record) |

### Returns

`[String](#type-string)` — form item type for the edit field

### Groups

- editing

### See Also

- [ListGrid.getEditorProperties](#method-listgridgeteditorproperties)

**Flags**: A

---
## Method: ListGrid.getCellStyle

### Description
Return the CSS class for a cell. By default this method has the following implementation:  
\- return any custom style for the record ([GridRenderer.recordCustomStyleProperty](GridRenderer.md#attr-gridrendererrecordcustomstyleproperty)) if defined.  
\- create a style name based on the result of [GridRenderer.getBaseStyle](GridRenderer.md#method-gridrenderergetbasestyle) and the state of the record using the rules described in [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes).

Cell Styles are customizable by:

*   attaching a custom style to a record by setting `record[this.recordCustomStyleProperty]` to some valid CSS style name.
*   modifying the base style returned by getBaseStyle() \[see that method for further documentation on this\]
*   overriding this function

In addition to this, [getCellCSSText()](GridRenderer.md#method-gridrenderergetcellcsstext) may be overriden to provide custom cssText to apply on top of the styling attributes derived from the named style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record object for this row and column |
| rowNum | [number](#type-number) | false | — | number of the row |
| colNum | [number](#type-number) | false | — | number of the column |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS style for this cell

### Groups

- appearance

### See Also

- [ListGrid.getBaseStyle](#method-listgridgetbasestyle)

---
## Method: ListGrid.setData

### Description
Provides a new data set to the ListGrid after the grid has been created or drawn. The ListGrid will redraw to show the new data automatically.

Note that passing null will not clear [ListGrid.data](ListGrid_1.md#attr-listgriddata), but will regroup it and reapply the current sort, highlighting, and summaries to the grid. Size will be recalculated for fields marked as [autofitWidth](ListGridField.md#attr-listgridfieldautofitwidth):true and a [selection manager](ListGrid_1.md#attr-listgridselectionmanager) will be created if none exists. To clear the grid instead, pass \[\].

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [List of ListGridRecord](#type-list-of-listgridrecord) | false | — | data to show in the list |

### Groups

- data

---
## Method: ListGrid.rowDoubleClick

### Description
Event handler for when a body record is double-clicked.

Default implementation fires 'editCell' if appropriate, and handles firing 'recordDoubleClick' stringMethod if defined at the field or LG level (That method has a different signature from this one)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record object returned from getCellRecord() |
| recordNum | [number](#type-number) | false | — | index of the row where the click occurred |
| fieldNum | [number](#type-number) | false | — | index of the col where the click occurred |
| keyboardGenerated | [boolean](../reference.md#type-boolean) | true | — | indicates whether this was a synthesized record doubleclick in response to a keyboard event |

### Returns

`[boolean](../reference.md#type-boolean)` — false if first click not on same record; true otherwise

### Groups

- events

### See Also

- [ListGrid.recordDoubleClick](#method-listgridrecorddoubleclick)

**Flags**: A

---
## Method: ListGrid.validateCell

### Description
Validate the current edit value for the cell in question. Called when the user moves to a new edit cell if [ListGrid.validateByCell](ListGrid_1.md#attr-listgridvalidatebycell) is true.  
This method may also be called directly to perform cell level validation at any time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | index of row to be validated. |
| fieldName | [String](#type-string)|[number](#type-number) | false | — | field name (or column index) of field to be validated |

### Returns

`[Boolean](#type-boolean)` — returns true if validation was successful (no errors encountered), false otherwise.

### Groups

- gridValidation

---
## Method: ListGrid.setFieldState

### Description
Sets some presentation properties (visibility, width, userFormula and userSummary) of the listGrid fields based on the [ListGridFieldState](../reference_2.md#type-listgridfieldstate) object passed in.  
Used to restore previous state retrieved from the grid by a call to [ListGrid.getFieldState](#method-listgridgetfieldstate).

The optional `isSparse` parameter may be passed to indicate whether the fieldState object is "sparse" - whether it includes explicit state information for hidden fields. In this case any fields defined on the component not explicitly included in the fieldState object will be hidden.  
If `isSparse` is not explicitly passed as a parameter, sparseness will be assumed if [DataBoundComponent.sparseFieldState](DataBoundComponent.md#attr-databoundcomponentsparsefieldstate) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldState | [ListGridFieldState](../reference_2.md#type-listgridfieldstate) | false | — | state to apply to the listGrid's fields. |
| isSparse | [Boolean](#type-boolean) | true | — | If true, the fieldState passed in is assumed to be "sparse". Any fields defined on this component without explicit field state values will be hidden. |

### Groups

- viewState

### See Also

- [ListGrid.getFieldState](#method-listgridgetfieldstate)

---
## Method: ListGrid.setUserSummaryText

### Description
Updates the [UserSummary.text](UserSummary.md#attr-usersummarytext) of the specified field. This method is preferred over setting the 'text' property directly because it also updates any component dependencies and recomputes the field. If the summary text is not passed or is `undefined`, it is assumed that the summary has already been updated and only the dependency propagation logic will run.

Known component dependencies are:

*   the cached record values of the formula for this field
*   any generated field that references the field's computed values

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[String](#type-string) | false | — | field owning the summary |
| text | [String](#type-string) | true | — | optional summary text to install |

### See Also

- [ListGridField.userSummary](ListGridField.md#attr-listgridfieldusersummary)

---
## Method: ListGrid.getFieldTitle

### Description
Return the title of a field, specified by name or index.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldId | [String](#type-string)|[Number](#type-number) | false | — | name or index of the field |

### Returns

`[String](#type-string)` — Field title.

**Flags**: A

---
## Method: ListGrid.getFormulaFieldValue

### Description
Get the computed value of a [formula field](ListGrid_1.md#attr-listgridcanaddformulafields).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field that has a formula |
| record | [Record](#type-record) | false | — | record to use to compute formula value |

### Returns

`[Double](../reference.md#type-double)|[String](#type-string)` — formula result if a valid number or [DataBoundComponent.badFormulaResultValue](DataBoundComponent.md#attr-databoundcomponentbadformularesultvalue) if invalid

---
## Method: ListGrid.setFieldMaxWidth

### Description
Updates [ListGridField.maxWidth](ListGridField.md#attr-listgridfieldmaxwidth) for the specified field and redraws the associated column if required.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [int](../reference.md#type-int)|[String](#type-string) | false | — | name of the field, or index. |
| width | [Number](#type-number) | false | — | — |

### See Also

- [ListGridField.maxWidth](ListGridField.md#attr-listgridfieldmaxwidth)

---
## Method: ListGrid.setRowErrors

### Description
Set the validation errors for some row (replacing any pre-existent validation errors)

Note that in the case of a [grouped listGrid](ListGrid_1.md#attr-listgridgroupbyfield), or a [TreeGrid](TreeGrid.md#class-treegrid), some records may be hidden form view (part of a collapsed group or parent folder). In this case there is no meaningful row number associated with a record. This method cannot be called on such rows - developers should make the row visible first. This is by design - users should always be able to see errors.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row to add validation error for |
| errors | [Any](#type-any) | false | — | validation errors for the row in the format `{fieldName:errorMessage, ...}`  
or  
`{fieldName:[errorMessage1, errorMessage2], ...}` |

### Groups

- gridValidation

### See Also

- [ListGrid.getRowErrors](#method-listgridgetrowerrors)
- [ListGrid.setFieldError](#method-listgridsetfielderror)

---
## Method: ListGrid.stopHover

### Description
Notification that the user is no longer hovering over some cell. Hides the current hover canvas if one is showing.

---
## Method: ListGrid.setHeaderHeight

### Description
Modify the height of a listGrid. To hide the header set height to zero.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [number](#type-number) | false | — | new height for the header |

### Groups

- sizing
- gridHeader

---
## Method: ListGrid.getFrozenRollOverCanvas

### Description
For grids with frozen columns, this method is called to retrieve the [ListGrid.frozenRollOverCanvas](ListGrid_1.md#attr-listgridfrozenrollovercanvas) when the user moves over a new row or cell if [ListGrid.showRollOverCanvas](ListGrid_1.md#attr-listgridshowrollovercanvas) is true, or when the user moves over the selected record if [ListGrid.showSelectedRollOverCanvas](ListGrid_1.md#attr-listgridshowselectedrollovercanvas) is true.

The default implementation uses the [AutoChild](../reference.md#type-autochild) subystem to create the [ListGrid.frozenRollOverCanvas](ListGrid_1.md#attr-listgridfrozenrollovercanvas) based on the `rollOverCanvas` auto child settings. It may be overridden for custom behavior.

Note that for efficiency this should not typically create a new Canvas every time that it is called. Instead usually a single rollOver canvas should be created and updated to reflect the current rollOver row if necessary.

Return null to avoid showing a `rollOverCanvas` for this row.

See also [ListGrid.getRollOverCanvas](#method-listgridgetrollovercanvas).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | index of the current rollOver row. |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | index of the current rollOver column. This parameter will be null unless [useCellRollOvers](ListGrid_1.md#attr-listgridusecellrollovers) is true for the grid. |

### Returns

`[Canvas](#type-canvas)` — the embedded component

### Groups

- hoverComponents

---
## Method: ListGrid.getSort

### Description
Returns the current [SortSpecifiers](../reference_2.md#object-sortspecifier) for this ListGrid. Will return null if this grid has never been sorted (and has no specified [ListGrid.initialSort](ListGrid_1.md#attr-listgridinitialsort) or [ListGrid.sortField](ListGrid_1.md#attr-listgridsortfield)).

Note that if sorting was applied via [ListGrid.sort](#method-listgridsort) \[rather than [ListGrid.setSort](#method-listgridsetsort)\] the sortSpecifiers returned will have been created based on the specified sort field / direction passed into [ListGrid.sort](#method-listgridsort).

### Returns

`[Array of SortSpecifier](#type-array-of-sortspecifier)` — current sort specifiers for this grid (may be null if this grid is unsorted).

### Groups

- sorting

---
## Method: ListGrid.rowEditorExit

### Description
Callback fired when the user attempts to navigate away from the current edit row, or complete the current edit.

Return false from this method to cancel the default behavior (Saving / cancelling the current edit / moving to the next edit cell).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editCompletionEvent | [EditCompletionEvent](../reference.md#type-editcompletionevent) | false | — | How was the edit completion fired? |
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for the cell being edited |
| newValues | [Object](../reference.md#type-object) | false | — | new values for the record \[Note that fields that have not been edited will not be included in this object\] |
| rowNum | [number](#type-number) | false | — | row number for the row being left |

### Returns

`[boolean](../reference.md#type-boolean)` — Returning false from this method will cancel the default behavior (for example saving the row) and leave the editor visible and focus in this edit cell.

### Groups

- editing

### See Also

- [ListGridField.editorExit](ListGridField.md#method-listgridfieldeditorexit)

---
## Method: ListGrid.handleGroupBy

### Description
Callback fired when the user attempts to group or ungroup the listGrid, or when [ListGrid.groupBy](#method-listgridgroupby) is called programmatically. Return false to cancel grouping.

This notification is fired before the [data](ListGrid_1.md#attr-listgridgrouptree) is updated to reflect the grouping. See also [ListGrid.groupByComplete](#method-listgridgroupbycomplete).

Note that this method is not called when the data is regrouped, either [programmatically](#method-listgridregroup), or in response to new data arriving from the server, and such regrouping can't be canceled - instead use callback [ListGrid.handleRegroup](#method-listgridhandleregroup).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fields | [Array of String](#type-array-of-string) | false | — | the list of ListGrid field-names by which the grid is about to be grouped. If the grid is being ungrouped, this param will be an empty array |
| specifiers | [Array of GroupSpecifier](#type-array-of-groupspecifier) | false | — | list of GroupSpecifier objects detailing grouping specifics for each grouped field |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel grouping on the passed specification

### Groups

- grouping

### See Also

- [ListGrid.handleRegroup](#method-listgridhandleregroup)
- [ListGrid.groupByComplete](#method-listgridgroupbycomplete)

---
## Method: ListGrid.isExpansionField

### Description
Identifies whether the passed-in field is the specially generated [expansionField](ListGrid_1.md#attr-listgridexpansionfield) used when [ListGrid.canExpandRecords](ListGrid_1.md#attr-listgridcanexpandrecords) is true. Use this method in your custom event handlers to avoid inappropriately performing actions when the expansionField is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field to test |

### Returns

`[Boolean](#type-boolean)` — whether the provided field is the expansion field

### Groups

- expansionField

---
## Method: ListGrid.setShowCollapsedGroupSummary

### Description
Setter for [ListGrid.showCollapsedGroupSummary](ListGrid_1.md#attr-listgridshowcollapsedgroupsummary)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showCollapsedGroupSummary | [boolean](../reference.md#type-boolean) | false | — | new showCollapsedGroupSummary value |

---
## Method: ListGrid.focusInFilterEditor

### Description
If the filter editor ([ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor)) is visible for this grid, this method will explicitly put focus into the specified field in the filter editor.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | true | — | Name of the field to put focus into. If unspecified focus will go to the first field in the editor |

### Groups

- filterEditor

---
## Method: ListGrid.collapseRecord

### Description
Collapses a given [record](../reference_2.md#object-listgridrecord) which has been previously expanded using [ListGrid.expandRecord](#method-listgridexpandrecord).

Depending on the [pooling mode](ListGrid_1.md#attr-listgridexpansioncomponentpoolingmode), this method may automatically destroy expansionComponents. By default, components created automatically by the ListGrid will be auto-destroyed. This behavior can be changed by setting a different pooling mode.

Note that components created via an override to [ListGrid.getExpansionComponent](#method-listgridgetexpansioncomponent) will **_not_** be auto-destroyed - developers should override `collapseRecord` to take care of clean-up for such components.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to collapse |

### Groups

- expansionField

---
## Method: ListGrid.endEditing

### Description
Complete the current edit by storing the value and hiding the inline editor. Note that if [ListGrid.autoSaveEdits](ListGrid_1.md#attr-listgridautosaveedits) is true, the value will be saved to the server.

### Groups

- editing

### See Also

- [ListGrid.startEditing](#method-listgridstartediting)

---
## Method: ListGrid.autoFitField

### Description
Programmatically cause a field to auto-fit horizontally to it's contents or title.

Does not establish permanent auto-fitting - use [ListGrid.setAutoFitWidth](#method-listgridsetautofitwidth) or [ListGrid.setAutoFitFieldWidths](#method-listgridsetautofitfieldwidths) to do so.

Note that unlike the ongoing autoFit set up by [ListGrid.autoFitFieldWidths](ListGrid_1.md#attr-listgridautofitfieldwidths) or [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth), any specified [ListGridField.width](ListGridField.md#attr-listgridfieldwidth) will not be taken as a minimum width - the field may shrink below the current specified width when this method is run. However, [ListGridField.minWidth](ListGridField.md#attr-listgridfieldminwidth) will be respected.

As with [ListGrid.autoFitFieldWidths](ListGrid_1.md#attr-listgridautofitfieldwidths), the auto-fit sizing is determined via the [ListGrid.autoFitWidthApproach](ListGrid_1.md#attr-listgridautofitwidthapproach).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | — |

### Returns

`[int](../reference.md#type-int)` — new width in pixels

### Groups

- autoFitFields

---
## Method: ListGrid.getEditFormItem

### Description
Method to retrieve a live edit form item for an [editable](ListGrid_1.md#attr-listgridcanedit) ListGrid. This is the automatically generated editor displayed in a cell while editing the grid.

Note that this is an advanced method and developers should be aware of the following issues:

*   Edit form items are created automatically as necessary and their lifecycle is managed by the grid. Items may be created or destroyed as a result of fields being shown and hidden, horizontal scrolling with [incremental rendering](ListGrid_1.md#attr-listgridshowallcolumns), row or cell transitions, configuration changes, and other circumstances. This method will return null when an item is not present.  
    Developers should therefore be aware that:
    *   There may not be a live item for a field while a cell is not currently editable and visible to the user.
    *   The item returned from a call to `getEditItem()` can become invalid as the user interacts with a grid. Even if the user is currently editing the field in question, this method may return a different live item if invoked later in the application flow. Therefore application code should avoid holding onto references to the items returned by this method, and instead invoke the method directly to dynamically retrieve the current edit item as required.
    *   If you change configuration of an edit item created by the grid, your changes will be lost if the item is destroyed and re-created
*   EditFormItems can be thought of as [autoChildren](../kb_topics/autoChildren.md#kb-topic-autochildren). They should be configured via [ListGridField.editorProperties](ListGridField.md#attr-listgridfieldeditorproperties) (or [ListGridField.editorProperties](ListGridField.md#attr-listgridfieldeditorproperties) for the [filter editor](ListGrid_1.md#attr-listgridshowfiltereditor) edit items), rather than by setting properties on the live items directly.
*   The items' values are managed by the ListGrid through the edit-values subsystem. If you want to change an edit value for a field, call [ListGrid.setEditValue](#method-listgridseteditvalue) and the grid will handle updating the value in the live item if necessary. You should not need to call `setValue();` directly on the item and doing so will not always update the edit value for the grid.

In general - bear in mind that this is an advanced usage and if there is an equivalent API available on the ListGrid it is always preferable to use that.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [String](#type-string)|[Integer](../reference_2.md#type-integer) | false | — | fieldName or colNum to get the edit item for. |

### Returns

`[FormItem](#type-formitem)` — the live edit item for the current edit row and specified field, or null if the grid is not currently showing any editors.

**Flags**: A

---
## Method: ListGrid.setSortHandler

### Description
Optional notification fired when either user or framework code calls [setSort()](#method-listgridsetsort). This notification fires before the default behavior; return false from the handler to cancel the default behavior. Note, the notification is fired before the default functionality, but _after_ prechecks have completed; your method will only be called if the default behavior would have been called. For example, if there are pending edits and the user does not confirm that these should be saved, normal sorting would not have gone ahead, so equally your handler will not be called.

The default `setSort()` method does two things to reflect the set of [sortSpecifier](../reference_2.md#object-sortspecifier)s passed to it:

*   Change the grid UI (show directional arrows, numerals to indicate sort priority, etc)
*   Actually sort the grid data

If your reason for implementing a custom `setSortHandler()` is to inhibit or replace one of those behaviors, you should cancel the default behavior and directly invoke just that part of it you require. The following implementation will replicate the default behavior:
```
   setSortHandler : function(sortSpecifiers) {
       this.displaySort(sortSpecifiers);
       this.applySortToData(sortSpecifiers);
       return false;  // Prevent the framework from running its own default impl
   }
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifiers | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | Array of [SortSpecifier](../reference_2.md#object-sortspecifier) objects |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel the default setSort() behavior

**Flags**: A

---
## Method: ListGrid.isPartiallySelected

### Description
When using tree-oriented selection modes like [TreeGrid.cascadeSelection](TreeGrid.md#attr-treegridcascadeselection), returns true if the record is considered partially selected because only some of it's children are selected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to check |

### Returns

`[Boolean](#type-boolean)` — true if record is partially selected; false otherwise

### Groups

- selection

---
## Method: ListGrid.headerTitleClipped

### Description
Is the field title for the specified field clipped?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [number](#type-number) | false | — | field number for the header button title to test |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the field title for the specified field is clipped

### Groups

- gridHeader

### See Also

- [ListGrid.clipHeaderTitles](ListGrid_1.md#attr-listgridclipheadertitles)

**Flags**: A

---
## Method: ListGrid.closeGroup

### Description
Closes the node represented by the "record" parameter, if it is a folder and is not already closed. This method only applies to [grouped](#method-listgridgroupby) ListGrids.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | node to close |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the node was closed, false if it was not (either because it is not a folder, or because it was already closed)

---
## Method: ListGrid.getFieldWidth

### Description
Returns a numeric value for the width of some field within this `ListGrid`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [int](../reference.md#type-int)|[FieldName](../reference.md#type-fieldname) | false | — | Index or name of the field for which the width is to be determined. |

### Returns

`[Integer](../reference_2.md#type-integer)` — width of the field in px, or `null` if the width can't be determined.

---
## Method: ListGrid.focusInRow

### Description
Puts keyboard focus into the specified row, showing a highlighted (roll-over style) appearance, and ensuring that arrow-key navigation will start from the specified row.

Only applies where [ListGrid.canSelectCells](ListGrid_1.md#attr-listgridcanselectcells) is false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| row | [Integer](../reference_2.md#type-integer) | false | — | Index of target row |

### See Also

- [ListGrid.focusInCell](#method-listgridfocusincell)

---
## Method: ListGrid.chartColumn

### Description
Chart a single column of data, with each cell value labeled by a value from another column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataColumn | [String](#type-string) | false | — | name of the ListGridField to use as a data |
| labelColumn | [String](#type-string) | false | — | name of the ListGridField to use as labels for data |
| chartProperties | [Chart Properties](#type-chart-properties) | true | — | properties to pass to the created chart |

### Returns

`[Chart](#type-chart)` — created Chart instance

---
## Method: ListGrid.getCellCSSText

### Description
Return CSS text for styling this cell, which will be applied in addition to the CSS class for the cell, as overrides.

"CSS text" means semicolon-separated style settings, suitable for inclusion in a CSS stylesheet or in a STYLE attribute of an HTML element.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[String](#type-string)` — CSS text for this cell

### See Also

- [ListGrid.getCellStyle](#method-listgridgetcellstyle)

---
## Method: ListGrid.getEditorProperties

### Description
Get the default properties for editor form items displayed while editing some field. Overriding this method allows developers to dynamically customize the form item displayed in an editable grid, based on the cell being edited.

Note: you should set [editorType](FormItem.md#attr-formitemeditortype) in the returned properties to control the type of form item that is used.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field whose properties are needed |

### Returns

`[Object](../reference.md#type-object)` — default properties for the field

### See Also

- [ListGrid.getEditorType](#method-listgridgeteditortype)

---
## Method: ListGrid.setViewState

### Description
Reset this grid's view state to match the [ListGridViewState](../reference_2.md#type-listgridviewstate) object passed in.  
Used to restore previous state retrieved from the grid by a call to [ListGrid.getViewState](#method-listgridgetviewstate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewState | [ListGridViewState](../reference_2.md#type-listgridviewstate) | false | — | Object describing the desired view state for the grid |

### Groups

- viewState

### See Also

- [ListGrid.getViewState](#method-listgridgetviewstate)

---
## Method: ListGrid.dataChanged

### Description
Method invoked when changes to the listGrid's data occur. This method will perform the necessary actions to ensure the changes to the data are reflected in the user interface, and then invoked the [ListGrid.dataChangedComplete](#method-listgriddatachangedcomplete) notification method.

May be invoked by any of the following:

*   a call to [ListGrid.addData](#method-listgridadddata), [ListGrid.updateData](#method-listgridupdatedata), or [ListGrid.removeData](#method-listgridremovedata)
*   [DataSource](DataSource.md#class-datasource) updates from the server for [ResultSet](ResultSet.md#class-resultset) data (triggered by record editing, etc.)
*   fetches arriving back from the server for [ResultSet](ResultSet.md#class-resultset) data
*   changes to array data if made through APIs such as [Array.set](Array.md#method-arrayset), [Array.add](Array.md#method-arrayadd), etc.
*   cache invalidation
*   filtering

Calling [ListGrid.setData](#method-listgridsetdata) will not call this method directly, but it may fire if one of the above listed events is triggered (e.g. a server fetch for [ResultSet](ResultSet.md#class-resultset) data).

Note that the `operationType` parameter is optional and will be passed and contain the operation (e.g. "update") if this notification was triggered by a fetch, an [ListGrid.addData](#method-listgridadddata), [ListGrid.updateData](#method-listgridupdatedata), or [ListGrid.removeData](#method-listgridremovedata), or a [DataSource](DataSource.md#class-datasource) update for [ResultSet](ResultSet.md#class-resultset) data (the first three reasons listed above) but otherwise will be undefined.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationType | [String](#type-string) | true | — | optionally passed operation causing the change |

### See Also

- [ListGrid.dataArrived](#method-listgriddataarrived)

**Flags**: A

---
## Method: ListGrid.clearEditValue

### Description
Clear a field value being tracked as an unsaved user edit.

The saved record value will be displayed in the the appropriate cell instead. Will also discard any validation errors for the specified field / row.

Note that for edits to an existing record, clearing all edit values will drop the edit session for the row altogether (it will no longer be returned by [ListGrid.getAllEditRows](#method-listgridgetalleditrows)). This is the not the case for unsaved [new edit rows](#method-listgridstarteditingnew) - for these rows edit values will be retained even if they are empty. To explicitly discard a new edit row, use [ListGrid.discardEdits](#method-listgriddiscardedits) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editValuesID | [number](#type-number)|[Object](../reference.md#type-object) | false | — | Row number, primary keys object for the record, or editValues object |
| colNum | [number](#type-number)|[String](#type-string) | false | — | Column number, or Name of field for which the value is to be cleared |

### Groups

- editing

**Flags**: A

---
## Method: ListGrid.bodyKeyPress

### Description
Handle a keyPress event on the body.

Default implementation handles navigating between records with arrow keys, and activating records with space and enter.

### Returns

`[boolean](../reference.md#type-boolean)` — return false to cancel

---
## Method: ListGrid.groupSortNormalizer

### Description
When [ListGrid.sortByGroupFirst](ListGrid_1.md#attr-listgridsortbygroupfirst) is active, the sorting [normalizer](../reference.md#attr-sortspecifiernormalizer) applied for implicit sorting by the field(s) used for grouping.

No default implementation.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record to normalize |
| fieldName | [FieldName](../reference.md#type-fieldname) | false | — | name of the field on which sorting occurred |
| context | [ListGrid](#type-listgrid) | false | — | the grid is passed to allow property and method access |

### Returns

`[Any](#type-any)` — normalized value for sorting

### Groups

- sorting
- grouping

### See Also

- [ListGrid.sortByGroupFirst](ListGrid_1.md#attr-listgridsortbygroupfirst)
- [ListGrid.groupSortDirection](ListGrid_1.md#attr-listgridgroupsortdirection)
- [SortSpecifier.normalizer](../reference.md#attr-sortspecifiernormalizer)

---
## Method: ListGrid.collapseRecords

### Description
Collapses the passed list of expanded [records](../reference_2.md#object-listgridrecord). Calls [collapseRecord](#method-listgridcollapserecord) for each passed record, but only marks the grid for redraw once, after all records have been collapsed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of ListGridRecord](#type-array-of-listgridrecord) | false | — | records to collapse |

### Groups

- expansionField

---
## Method: ListGrid.isCheckboxField

### Description
Identifies whether the passed-in field is the specially generated [checkboxField](ListGrid_1.md#attr-listgridcheckboxfield) used when [SelectionAppearance](../reference.md#type-selectionappearance) is "checkbox". Use this method in your custom event handlers to avoid inappropriately performing actions when the checkboxField is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field to test |

### Returns

`[Boolean](#type-boolean)` — whether the provided field is the checkbox field

### Groups

- checkboxField

---
## Method: ListGrid.getEditCol

### Description
Returns the index of the column being edited or null if there is no current edit column.

### Returns

`[int](../reference.md#type-int)` — index of the current edit column

### Groups

- editing

---
## Method: ListGrid.setFetchOperation

### Description
Update the [fetchOperation](DataBoundComponent.md#attr-databoundcomponentfetchoperation) at runtime.

If this grid is currently showing a filtered data set it will be discarded by default. Developers may issue a new [fetch](#method-listgridfetchdata) to fetch a new set of data using the new operation. Set [ListGrid.discardDataOnSetFetchOperation](ListGrid_1.md#attr-listgriddiscarddataonsetfetchoperation) to false to avoid dropping the existing set of data automatically. In this case if you want to clear the existing data you should call [ListGrid.setData](#method-listgridsetdata) and pass in an empty array in application code.

Developers should be aware changing the fetch operation at runtime can lead to a bad user experience in some cases.

For example if a fetch operation does not provide data for fields that are visible (or fails to provide hidden data used in formula fields, etc), this may lead to missing values in the grid.

Similarly, any smart behaviors based on the operationBinding definition, such as special treatment of operationBindings that involve Server Summaries, or any automated behavior around picking visible fields, or determining which fields are editable, will not be recalculated in response to `setFetchOperation()`

If you need such ground-up recalculation, consider re-creating the grid as a whole instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationId | [String](#type-string) | false | — | new fetch operation ID. |

### Returns

`[ListGrid](#type-listgrid)` — this grid

---
## Method: ListGrid.toggleSort

### Description
Toggles the sort-direction of the field with the passed name and resorts the grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | The name of a field, visible, hidden or existing only in the dataSource |

### Groups

- sorting

**Flags**: A

---
## Method: ListGrid.getCellVAlign

### Description
Return the vertical alignment for cell contents. Expected values are: 'top', 'center', or 'bottom'

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListgridRecord](#type-listgridrecord) | false | — | this cell's record |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[VerticalAlignment](../reference.md#type-verticalalignment)` — Vertical alignment of cell contents: 'top', 'center', or 'bottom'

### See Also

- [ListGrid.getCellStyle](#method-listgridgetcellstyle)

---
## Method: ListGrid.getFilterEditorValueMap

### Description
If we're showing the filter (query-by-example) row for this ListGrid, this method is used to determine the valueMap to display in the filter row for this field. Default implementation will return the field.filterEditorValueMap if specified, or field.valueMap.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field definition field for which we need a valueMap |

### Returns

`[ValueMap](../reference_2.md#type-valuemap)` — ValueMap for the edit field (or null if no valueMap required)

### Groups

- filterEditor

**Flags**: A

---
## Method: ListGrid.getExportColumnBGColor

### Description
When exporting data to Excel/OpenOffice format using [exportData()](#method-listgridexportdata) or [exportClientData()](#method-listgridexportclientdata), background color to use for the given colNum.

See [exportBGColor](../kb_topics/exportBGColor.md#kb-topic-exports--cell-background-color) for an overview.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [int](../reference.md#type-int) | false | — | column number |

### Returns

`[CSSColor](../reference_2.md#type-csscolor)` — background color to use for the column, or null to use the default background color

### Groups

- exportBackgroundColor

---
## Method: ListGrid.setValueMap

### Description
Set the [valueMap](ListGridField.md#attr-listgridfieldvaluemap) for a field. See also the [setEditorValueMap()](#method-listgridseteditorvaluemap) and [getEditorValueMap()](#method-listgridgeteditorvaluemap) methods which allow further customization of the valueMap displayed while the field is in edit mode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldID | [String](#type-string)|[int](../reference.md#type-int) | false | — | Name or index of field to update |
| map | [Object](../reference.md#type-object) | false | — | ValueMap for the passed field |

---
## Method: ListGrid.sorterContextClick

### Description
Notification method fired when the user right-clicks on the corner [sort button](ListGrid_1.md#attr-listgridsorterconstructor). Return false to suppress the default behavior of showing the sorter's context menu.

### Returns

`[boolean](../reference.md#type-boolean)` — return false to suppress the context menu

### Groups

- events
- sorting

**Flags**: A

---
## Method: ListGrid.setShowFilterEditor

### Description
Setter for the [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) property. Allows the filter editor to be shown or hidden at runtime.

By default, hiding the `filterEditor` will also clear any user-criteria it specified and refetch the data. To prevent this behavior, you can set [clearCriteriaOnFilterEditorHide](ListGrid_1.md#attr-listgridclearcriteriaonfiltereditorhide) to false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [boolean](../reference.md#type-boolean) | false | — | true if the filter editor should be shown, false if it should be hidden |

### Groups

- filterEditor

---
## Method: ListGrid.getField

### Description
Given a column number or field name, return the field definition of a field which is visible in the grid. To retrieve the definition of _any_ field, including hidden ones, use [getFieldByName()](#method-listgridgetfieldbyname).

When using [DataBinding](DataBoundComponent.md#attr-databoundcomponentfields), the field definition may be a mix of information derived from [ListGrid.fields](ListGrid_1.md#attr-listgridfields) and [ListGrid.dataSource](ListGrid_1.md#attr-listgriddatasource).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [int](../reference.md#type-int)|[FieldName](../reference.md#type-fieldname) | false | — | number or name of the field |

### Returns

`[ListGridField](#type-listgridfield)` — field definition

---
## Method: ListGrid.getDefaultFieldWidth

### Description
Method to calculate and return the default width of a field. This method is called to calculate the size of each field's content as part of the [field auto fit](ListGrid_1.md#attr-listgridautofitfieldwidths) behavior. Note that this method returns a size for _content_, so will not be consulted if [autoFitWidthApproach](ListGridField.md#attr-listgridfieldautofitwidthapproach) is set to `"title"`.

If [ListGridField.defaultWidth](ListGridField.md#attr-listgridfielddefaultwidth) is specified, this will be returned.

Otherwise, the default implementation varies by [field type](../reference.md#type-listgridfieldtype). For fields of type `"icon"`, or fields which show only a [valueIcon](ListGridField.md#attr-listgridfieldvalueicons) as a value, and for boolean fields which show a checkbox value, the width will be calculated based on the icon size and [ListGrid.iconPadding](ListGrid_1.md#attr-listgridiconpadding). For other fields the [ListGrid.getFieldContentWidth](#method-listgridgetfieldcontentwidth) method will be used to calculate a width based on the rendered width of content. Note that for `"image"` type fields, this method will rely on the [ListGridField.imageWidth](ListGridField.md#attr-listgridfieldimagewidth) being specified.

Note that this width is the default width of "content" - it does not take into account the rendered size of the field title.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | Field for which the size should be determined |

### Returns

`[int](../reference.md#type-int)` — default size required for the field's content.

---
## Method: ListGrid.clearRowErrors

### Description
Clear any stored validation errors for some row

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | index of row to clear validation error for |

### Groups

- validation

### See Also

- [ListGrid.setRowErrors](#method-listgridsetrowerrors)

---
## Method: ListGrid.getSelectedRecord

### Description
Returns the first selected record in this grid.

This method is appropriate if the [selectionType](ListGrid_1.md#attr-listgridselectiontype) is "single", or if you only care about the first selected record in a multiple-record selection. To access all selected records, use [ListGrid.getSelection](#method-listgridgetselection) instead.

**NOTE:** If a record is returned, it should be treated as read-only and not modified.

### Returns

`[ListGridRecord](#type-listgridrecord)` — the first selected record, or null if no record is selected.

### Groups

- selection

---
## Method: ListGrid.unmarkRecordRemoved

### Description
Reverses a previous call to [ListGrid.markRecordRemoved](#method-listgridmarkrecordremoved).

Note that a record that is marked for removal and then un-marked retains any uncommitted edits from before it was marked for removal. These can be discarded with [ListGrid.discardEdits](#method-listgriddiscardedits).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | index of record to clear the 'removed' |

### Groups

- editing

---
## Method: ListGrid.startEditingNew

### Description
Start editing a new row, after the last pre-existing record in the current set of data.

This new row will be saved via the "add" [DataSource\\n operation](../kb_topics/dataSourceOperations.md#kb-topic-datasource-operations).

See the [Grid Editing overview](../kb_topics/editing.md#kb-topic-grid-editing) and also the [Editing Unsaved Records overview](../kb_topics/unsavedRecords.md#kb-topic-handling-unsaved-records) for context about how unsaved records behave.

You can optionally pass `newValues` which are the initial values for the newly added record. See also [ListGridField.defaultValue](ListGridField.md#attr-listgridfielddefaultvalue) as a means of setting default values every time the user begins editing a new record, for instance, by pressing downArrow on the last normal record in the grid when [ListGrid.listEndEditAction](ListGrid_1.md#attr-listgridlistendeditaction) is "next".

If editing is already underway elsewhere in the grid, startEditingNew() behaves just like [ListGrid.startEditing](#method-listgridstartediting).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValues | [Map](#type-map)|[Record](#type-record) | true | — | Optional initial set of properties for the new record |
| suppressFocus | [Boolean](#type-boolean) | true | — | Whether to suppress the default behavior of moving focus to the newly shown editor. |

### Groups

- editing

### See Also

- [ListGrid.startEditing](#method-listgridstartediting)

**Flags**: A

---
## Method: ListGrid.selectRecords

### Description
Select/deselect a list of [Record](../reference.md#object-record)s passed in explicitly, or by index.

Note that developers may wish to use [ListGrid.selectRange](#method-listgridselectrange) to select a single contiguous range.

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
## Method: ListGrid.freezeField

### Description
Freeze the indicated field, so that it remains in place and visible when horizontal scrolling occurs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield)|[Integer](../reference_2.md#type-integer)|[String](#type-string)|[Array](#type-array) | false | — | field or fields to freeze. fields may be specified as ListGridField objects, field names or colNum. |

### Groups

- frozenFields

---
## Method: ListGrid.getValueIconCursor

### Description
Returns the cursor to display when the mouse pointer is over a [valueIcon](ListGridField.md#attr-listgridfieldvalueicons) in a a cell.

Default behavior will display the [ListGridField.iconCursor](ListGridField.md#attr-listgridfieldiconcursor) if specified, otherwise the `"pointer"` cursor if a [ListGridField.valueIconClick](ListGridField.md#method-listgridfieldvalueiconclick) hander is present. (If no valueIconClick handler is defined this method will return null and the cursor will be unchanged when the user rolls over the value icon image).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field displaying the valueIcon |
| record | [ListGridRecord](#type-listgridrecord) | false | — | record being rolled over |
| value | [Any](#type-any) | false | — | value of this cell |

### Returns

`[Cursor](../reference.md#type-cursor)` — cursor to display when the user rolls over icons in this field's cells. May be null indicating no special cursor to display.

---
## Method: ListGrid.resizeField

### Description
Resize a particular field to a new width. Note that this method will also set [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth) to false if it was previously true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [number](#type-number) | false | — | Number of the field to resize |
| newWidth | [number](#type-number) | false | — | New width of the field |

**Flags**: A

---
## Method: ListGrid.discardAllEdits

### Description
Cancel outstanding edits, discarding edit values, and hiding editors for the record\[s\] passed in if appropriate.

If no rows are passed in, all outstanding edit values will be dropped. This will **not** automatically end editing; call [ListGrid.endEditing](#method-listgridendediting) **before** calling discardAllEdits() if you also want to end editing.

Note that this also clears the [removed](#method-listgridmarkrecordremoved) state of any records that have been marked as removed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rows | [Array of Number](#type-array-of-number) | true | — | allows you to specify which row(s) to drop edits for |
| dontHideEditor | [boolean](../reference.md#type-boolean) | true | — | By default this method will hide the editor if it is currently showing for any row in the grid. Passing in this parameter will leave the editor visible (and just reset the edit values underneath the editor). |

### Groups

- editing

**Flags**: A

---
## Method: ListGrid.markSelectionRemoved

### Description
Marks the currently selected records as removed, as though [ListGrid.markRecordRemoved](#method-listgridmarkrecordremoved) had been called.

### Groups

- editing

---
## Method: ListGrid.canEditCell

### Description
Can this cell be edited?

The default implementation of `canEditCell()` respects the various property settings affecting editability:

*   [field.canEdit](ListGridField.md#attr-listgridfieldcanedit) can be set to disable editing for a field
*   If the grid is bound to a dataSource, the [ListGrid.canEditFieldAttribute](ListGrid_1.md#attr-listgridcaneditfieldattribute) value on the dataSource field may enable / disable editing
*   a record with the [recordEditProperty](ListGrid_1.md#attr-listgridrecordeditproperty) set to false is not editable
*   disabled records are not editable

You can override this method to control editability on a cell-by-cell basis. For example, if you had a grid that allows editing of "orders", and you had a field "shipDate" that is normally editable, but should not be editable if the order is already "complete", you might implement `canEditCell()` as follows:

```
   isc.ListGrid.create({
       ...
       canEditCell : function (rowNum, colNum) {
           var record = this.getRecord(rowNum),
               fieldName = this.getFieldName(colNum);
           if (fieldName == "shipDate" &&
               record.orderStatus == "complete")
           {
               return false;
           }
           // use default rules for all other fields
           return this.Super("canEditCell", arguments);
       }
   });
 
```

Notes on providing custom implementations:

*   In order to allow complete control over editing, `canEditCell()` is called very frequently. If you see delays on row to row navigation, check that your implementation is efficient
*   If you change the editability of a cell on the fly, for example, during [ListGrid.editorExit](#method-listgrideditorexit) on another cell, call refreshCell() to show or hide the editor
*   If this ListGrid allows new records to be created, `canEditCell()` may be called when there is no record available, in which case getRecord() will return null. The values input so far by the user are available via [ListGrid.getEditValues](#method-listgridgeteditvalues).

For more information on editing, see the [editing overview](../kb_topics/editing.md#kb-topic-grid-editing).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — Whether to allow editing this cell

### Groups

- editing

**Flags**: A

---
## Method: ListGrid.cancelEditing

### Description
Cancel the current edit without saving.

### Groups

- editing

---
## Method: ListGrid.deselectAllRecords

### Description
Deselect all records

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: ListGrid.getCellAriaState

### Description
Returns a map of [WAI ARIA state attribute values](Canvas.md#attr-canvasariastate) to be written into cells within this grid. Default implementation return null, meaning no per-cell aria state is written out

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | row index of the cell |
| colNum | [Integer](../reference_2.md#type-integer) | false | — | column index of the cell |
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for the cell in question |
| role | [String](#type-string) | false | — | ARIA role for the cell as returned by [ListGrid.getCellRole](#method-listgridgetcellrole) |

### Returns

`[Object](../reference.md#type-object)` — Object containing aria property names and values to write into the cell's HTML

### Groups

- accessibility

**Flags**: A

---
## Method: ListGrid.applySortToData

### Description
Sort the grid's data to reflect the parameter sortSpecifiers.

**NOTE:** This method is primarily used by [ListGrid.setSort](#method-listgridsetsort); it is not intended to be called by user code, unless you are implementing a custom [setSortHandler](#method-listgridsetsorthandler)). For the normal use case, calling this method directly will fail to execute vital pre-steps. If you are not implementing a custom handler as described above, do not call this method directly - call `setSort()` instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortSpecifiers | [Array of SortSpecifier](#type-array-of-sortspecifier) | false | — | Array of [SortSpecifier](../reference_2.md#object-sortspecifier) objects |

**Flags**: A

---
## Method: ListGrid.getSortState

### Description
Returns a snapshot of the current sort state within this listGrid as a [ListGridSortState](../reference.md#type-listgridsortstate) object.  
This object can be passed to [ListGrid.setSortState](#method-listgridsetsortstate) to reset this grid's sort to the current state (assuming the same fields are present in the grid).

### Returns

`[ListGridSortState](../reference.md#type-listgridsortstate)` — current sort state for the grid.

### Groups

- viewState

### See Also

- [ListGrid.setSortState](#method-listgridsetsortstate)

---
## Method: ListGrid.getRowRole

### Description
Returns the WAI ARIA role for rows within this listGrid.

If the record has a value for the [ListGrid.recordRowRoleProperty](ListGrid_1.md#attr-listgridrecordrowroleproperty), this will be respected.  
Otherwise if [ListGrid.rowRole](ListGrid_1.md#attr-listgridrowrole) is specified, it will be used.

If the property is not explicitly set, default implementation will return `"separator"` for separator rows, `"listitem"` for data rows if this listGrid has [role:"list"](ListGrid_1.md#attr-listgridariarole), or `"row"` for data rows if this listGrid has `ariaRole:"grid"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | row index |
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record for the row in question |

### Returns

`[String](#type-string)` — role for rows within this grid

### Groups

- accessibility

**Flags**: A

---
## Method: ListGrid.sort

### Description
Sort this grid's data, with the option to explicitly specify a single field to sort by and sort direction.

If sortField is not provided and listGrid.sortField is undefined, the data will be sorted by the first sortable column according to [ListGridField.sortDirection](ListGridField.md#attr-listgridfieldsortdirection) if specified, or [ListGrid.sortDirection](ListGrid_1.md#attr-listgridsortdirection).

ListGrids also support multiple-field sorting. See [ListGrid.setSort](#method-listgridsetsort) for details.

Note that for editable grids, sorting is performed by underlying data values, not for unsaved [pending edit values](#method-listgridgeteditvalues). When the user saves edits in a sorted grid, the grid will automatically be [unsorted](#method-listgridunsort). See [editing](../kb_topics/editing.md#kb-topic-grid-editing) for further details.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortField | [String](#type-string)|[number](#type-number) | true | — | the field name or column number to sort by |
| sortDirection | [SortDirection](../reference_2.md#type-sortdirection) | true | — | the direction to sort in |

### Returns

`[Boolean](#type-boolean)` — sorting worked

### Groups

- sorting

### See Also

- [SortDirection](../reference_2.md#type-sortdirection)

---
## Method: ListGrid.removeEmbeddedComponent

### Description
Removes an embedded component previously associated with the provided record. If a Canvas is passed as the `record` parameter, it is assumed to be a component and the record is detected automatically from it. If `destroyOnUnEmbed` is `true` for the component, it will also be destroyed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord)|[Canvas](#type-canvas) | false | — | record that the component was previously attached to or the component itself |
| component | [Integer](../reference_2.md#type-integer)|[Canvas](#type-canvas) | true | — | component to unembed, or the colNum in which it appears |

**Flags**: A

---
## Method: ListGrid.headerHoverHTML

### Description
Returns the HTML that is displayed by the default [headerHover](#method-listgridheaderhover) handler. Return null or an empty string to cancel the hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [number](#type-number) | false | — | field number for the header that was hovered |
| defaultHTML | [HTMLString](../reference.md#type-htmlstring) | false | — | the HTML that would have been displayed by default |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover. If null or an empty string, then the hover is canceled.

### Groups

- hovers
- gridHeader

### See Also

- [ListGrid.showClippedHeaderTitlesOnHover](ListGrid_1.md#attr-listgridshowclippedheadertitlesonhover)
- [ListGrid.clipHeaderTitles](ListGrid_1.md#attr-listgridclipheadertitles)

**Flags**: A

---
## Method: ListGrid.rowEditorEnter

### Description
Callback fired when the user starts editing a new row.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridField](#type-listgridfield) | false | — | record for the cell being edited |
| editValues | [Object](../reference.md#type-object) | false | — | edit values for the current row |
| rowNum | [number](#type-number) | false | — | row number for the cell |

### Groups

- editing

### See Also

- [ListGrid.editorEnter](#method-listgrideditorenter)

---
## Method: ListGrid.markRecordRemoved

### Description
Marks a record deleted such that a later call to [ListGrid.saveEdits](#method-listgridsaveedits) or [ListGrid.saveAllEdits](#method-listgridsavealledits) will cause a "remove" [DSRequest](../reference_2.md#object-dsrequest) to be submitted.

A removed record is disabled and non-editable, and uses [ListGrid.removedCSSText](ListGrid_1.md#attr-listgridremovedcsstext) for its CSS style, which by default will show strikethrough text.

Contrast this method with removeSelectedData(), which immediately submits a DSRequest to remove the selected records from the dataset.

Records that have been marked for removal using this method may be 'unmarked' via a call to [ListGrid.unmarkRecordRemoved](#method-listgridunmarkrecordremoved), or by discarding edit values ([ListGrid.discardEdits](#method-listgriddiscardedits)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number for the record to mark |

### Groups

- editing

---
## Method: ListGrid.rowHasChanges

### Description
If this listGrid can be edited, this method will return true if the row passed in has been edited, but the edits have not yet been saved to the ListGrid's data object.

Note this method will not return true if a record has been marked as [removed](#method-listgridmarkrecordremoved), but has no other changes. Developers can use [ListGrid.recordMarkedAsRemoved](#method-listgridrecordmarkedasremoved) to check for this case.

Note that if this grid is bound to a [dataSource](ListGrid_1.md#attr-listgriddatasource), and an asynchronous save has been submitted, this method will compare the local edit values against the submitted values by default, returning false (no changes), if they match. This is useful for detecting whether the user is actively editing values and hasn't yet committed them.

The `ignorePendingValues` parameter may be used by developers who want to ignore this case and simply compare edit values against the record in the local data set.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | index of row to check for changes |
| ignorePendingValues | [Boolean](#type-boolean) | true | — | If true, this method will compare the current edit values against the underlying record in the dataset, not taking pending edit values into account |

### Returns

`[Boolean](#type-boolean)` — true if the row has changes.

### Groups

- editing

---
## Method: ListGrid.openGroup

### Description
Opens the node represented by the "record" parameter, if it is a folder and is not already open. This method only applies to [grouped](#method-listgridgroupby) ListGrids.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | node to open |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the node was opened, false if it was not (either because it is not a folder, or because it was already open)

---
## Method: ListGrid.getDragTrackerIcon

### Description
Return an icon to display as a drag tracker when the user drags some record.  
Default implementation: If [ListGridField.valueIcons](ListGridField.md#attr-listgridfieldvalueicons) is specified for the title field of this grid (see [ListGrid.getTitleField](#method-listgridgettitlefield)), the appropriate value icon will be displayed. If no appropriate valueIcon can be found, the icon will be derived from [ListGrid.trackerImage](ListGrid_1.md#attr-listgridtrackerimage).  
If multiple records are selected, only the first record is examined for valueIcons.

Note: Only called if [ListGrid.dragTrackerMode](ListGrid_1.md#attr-listgriddragtrackermode) is set to `"icon"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of ListGridRecord](#type-array-of-listgridrecord) | false | — | Records being dragged |

### Returns

`[String](#type-string)` — Image URL of icon to display

### Groups

- dragTracker

---
## Method: ListGrid.getCellAlign

### Description
Return the horizontal alignment for cell contents. Default implementation returns [ListGridField.cellAlign](ListGridField.md#attr-listgridfieldcellalign) if specified, otherwise [ListGridField.align](ListGridField.md#attr-listgridfieldalign).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | this cell's record |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[Alignment](../reference_2.md#type-alignment)` — Horizontal alignment of cell contents: 'right', 'center', or 'left'

### See Also

- [ListGrid.getCellStyle](#method-listgridgetcellstyle)

---
## Method: ListGrid.recordMarkedAsRemoved

### Description
Returns true if the specified record is marked as removed via a call to [ListGrid.markRecordRemoved](#method-listgridmarkrecordremoved)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | index of row to verify |

### Returns

`[Boolean](#type-boolean)` — true if the specified record has been marked for removal

### Groups

- editing

---
## Method: ListGrid.recordDrop

### Description
Process a drop of one or more records on a ListGrid record.

This method can be overridden to provide custom drop behaviors, and is a more appropriate override point than the lower level [Canvas.drop](Canvas.md#method-canvasdrop) handler.

If this is a self-drop, records are simply reordered.

For a drop from another widget, [ListGrid.transferDragData](#method-listgridtransferdragdata) is called, which depending on the [dragDataAction](ListGrid_1.md#attr-listgriddragdataaction) specified on the source widget, may either remove the source records from the original list (`dragDataAction:"move"`) or just provide a copy to this list (`dragDataAction:"copy"`).

If this grid is databound, the new records will be added to the dataset by calling [DataSource.addData](DataSource.md#method-datasourceadddata). Further, if the new records were dragged from another databound component, and [addDropValues](DataBoundComponent.md#attr-databoundcomponentadddropvalues) is true, [getDropValues](DataBoundComponent.md#method-databoundcomponentgetdropvalues) will be called for every item being dropped.

For multi-record drops, Queuing is automatically used to combine all DSRequests into a single HTTP Request (see QuickStart Guide, Server Framework chapter). This allows the server to persist all changes caused by the drop in a single transaction (and this is automatically done when using the built-in server DataSources with Power Edition and above).

Note that reordering records has no effect on a databound grid.

The newly dropped data is then selected automatically.

If these default persistence behaviors are undesirable, return false to cancel them, then and implement your own behavior, typically by using grid.updateData() or addData() to add new records.

**NOTE:** the records you receive in this event are the actual Records from the source component. Use [DataSource.copyRecords](DataSource.md#method-datasourcecopyrecords) to create a copy before modifying the records or using them with updateData() or addData().

NOTE: for a drop beyond the last visible record of a ListGrid, `targetRecord` will be null and the `index` will be one higher than the last record. This includes a drop into an empty ListGrid, where `index` will be 0.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dropRecords | [Array of ListGridRecord](#type-array-of-listgridrecord)[] | false | — | records being dropped |
| targetRecord | [ListGridRecord](#type-listgridrecord) | false | — | record being dropped on. May be null |
| index | [int](../reference.md#type-int) | false | — | index of record being dropped on |
| sourceWidget | [Canvas](#type-canvas) | false | — | widget where dragging began |

---
## Method: ListGrid.setEditorValueMap

### Description
Set a valueMap to display for this field while editing.  
This method sets the [field.editorValueMap](ListGridField.md#attr-listgridfieldeditorvaluemap) property - note that if [ListGrid.getEditorValueMap](#method-listgridgeteditorvaluemap) has been overridden it may not make use of this property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldID | [Object](../reference.md#type-object)|[number](#type-number)|[FieldName](../reference.md#type-fieldname) | false | — | field object, number, or name |
| map | [Object](../reference.md#type-object) | false | — | ValueMap to apply to the field |

### Groups

- editing

**Flags**: A

---
## Method: ListGrid.cellMouseUp

### Description
Called when a cell receives a mouseup event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object (retrieved from getCellRecord(rowNum, colNum)) |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

---
## Method: ListGrid.setFieldButtonProperties

### Description
Method to update properties on a field's header button at runtime. This property allows customization of any settable properties on the ListGridField's header button after it has been generated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| name | [String](#type-string) | false | — | Field to update |
| properties | [Canvas Properties](#type-canvas-properties) | false | — | new properties to apply to the header button |

---
## Method: ListGrid.selectRange

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
## Method: ListGrid.getCriteria

### Description
Retrieves a copy of the explicit criteria currently applied to this component, including criteria provided by a grid's [ListGrid.filterWindow](ListGrid_1.md#attr-listgridfilterwindow) or [ListGrid.searchForm](ListGrid_1.md#attr-listgridsearchform), but not criteria applied [implicitly](DataBoundComponent.md#attr-databoundcomponentimplicitcriteria). May return null.

Note: if [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) is true, the criteria returned by this method may not match the values currently displayed in the filter editor, since the user may have entered values which have not yet been applied to our data. [ListGrid.getFilterEditorCriteria](#method-listgridgetfiltereditorcriteria) may be used to retrieve the current criteria displayed in the filterEditor.

### Returns

`[Criteria](../reference_2.md#type-criteria)` — current filter criteria

### Groups

- dataBoundComponentMethods

---
## Method: ListGrid.getCellRecord

### Description
Return the pointer to a particular record by record number.  
Notes:  
\- If this is a databound grid, and the record for some row has not yet been loaded, returns the [loading marker](ResultSet.md#classmethod-resultsetgetloadingmarker), and a fetch will be initialized to retrieve the record from the server.  
\- If this is a new row in an editable ListGrid, and has not yet been saved, this method will return null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recordNum | [number](#type-number) | false | — | row index of record to return. |

### Returns

`[ListGridRecord](#type-listgridrecord)` — Record object for the row.

### See Also

- [ListGrid.getRecord](#method-listgridgetrecord)
- [ListGrid.getEditedRecord](#method-listgridgeteditedrecord)

**Flags**: A

---
## Method: ListGrid.getEditorValueMap

### Description
Returns the valueMap to display for a field when it is displayed in the editor while editing some record.  
Called when a user starts to edit a field, or whenever the field valueMap is updated via a call to [ListGrid.setValueMap](#method-listgridsetvaluemap) or [ListGrid.setEditorValueMap](#method-listgridseteditorvaluemap). Default implementation will return the `field.editorValueMap` if specified, otherwise `field.valueMap` - can be overridden to provide a different specific valueMap for some field based on the record/field data.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [ListGridField](#type-listgridfield) | false | — | field definition field for which we need a valueMap |
| values | [Object](../reference.md#type-object) | false | — | Field values for record being edited. Note that this will include the current edit values for fields that have not yet been saved. May be null, if editing a new record. |

### Returns

`[ValueMap](../reference_2.md#type-valuemap)` — ValueMap for the edit field (or null if no valueMap required)

### Groups

- editing

**Flags**: A

---
## Method: ListGrid.getSortField

### Description
Returns the current sort field for this grid. Note that if [ListGrid.setSort](#method-listgridsetsort) has been used to sort by multiple fields, you can call [ListGrid.getSort](#method-listgridgetsort) to retrieve details about the complete sort applied to the grid.

### Returns

`[String](#type-string)` — sort field name

### Groups

- sorting

---
## Method: ListGrid.setAutoFitMaxWidth

### Description
Setter for [ListGrid.autoFitMaxWidth](ListGrid_1.md#attr-listgridautofitmaxwidth).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Integer](../reference_2.md#type-integer)|[String](#type-string) | false | — | Width we'll expand to accommodate if [auto fit](ListGrid_1.md#attr-listgridautofitdata) is enabled horizontally. |

### Groups

- autoFitData

---
## Method: ListGrid.setFieldMinWidth

### Description
Updates [ListGridField.minWidth](ListGridField.md#attr-listgridfieldminwidth) for the specified field and redraws the associated column if required.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNum | [int](../reference.md#type-int)|[String](#type-string) | false | — | name of the field, or index. |
| width | [Number](#type-number) | false | — | — |

### See Also

- [ListGridField.minWidth](ListGridField.md#attr-listgridfieldminwidth)

---
## Method: ListGrid.setAutoFitWidth

### Description
Setter for [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth). Enables or disables dynamic autoFitWidth behavior on the specified field. Note if the field is currently autoFitWidth:true, and this method is disabling autoFit, the field will not be resized by default - if you wish to resize to an explicit width, use [ListGrid.resizeField](#method-listgridresizefield).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | field to auto-fit |
| autoFit | [boolean](../reference.md#type-boolean) | false | — | Should autoFitWidth be enabled or disabled? |

### Groups

- autoFitFields

---
## Method: ListGrid.getFilterEditorCriterion

### Description
Extracts and returns the criteria for the passed field from the [filterEditor](ListGrid_1.md#attr-listgridshowfiltereditor). The result can be an [AdvancedCriteria](../reference.md#object-advancedcriteria), if the field in question produces more than one restriction, such as separate `greaterThan` and `lessThan` criteria for a range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldName | [String](#type-string) | false | — | name of the field to get the criteria for |

### Returns

`[Criterion](#type-criterion)` — the passed field's filterEditor criterion

---
## Method: ListGrid.rowClick

### Description
Event handler for when rows in the body are clicked upon. The default implementation handles firing [ListGrid.startEditing](#method-listgridstartediting) if appropriate, and fires [ListGridField.recordClick](ListGridField.md#method-listgridfieldrecordclick) and/or [ListGrid.recordClick](#method-listgridrecordclick) if set. Developers should typically implement recordClick rather than overriding this method.

Note that this method fires in addition to any specified [ListGrid.cellClick](#method-listgridcellclick) handler (even if that method cancels the event as a whole by returning `false`).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record object returned from getCellRecord() |
| recordNum | [int](../reference.md#type-int) | false | — | index of the row where the click occurred |
| fieldNum | [int](../reference.md#type-int) | false | — | index of the col where the click occurred |
| keyboardGenerated | [boolean](../reference.md#type-boolean) | true | — | indicates whether this was a synthesized record click in response to a keyboard event |

### Returns

`[Boolean](#type-boolean)` — —

### Groups

- events
- events

### See Also

- [ListGrid.recordClick](#method-listgridrecordclick)

**Flags**: A

---
## Method: ListGrid.editorEnter

### Description
Callback fired when the user starts editing a new cell.

This callback is typically used to establish dynamic default values via [ListGrid.setEditValue](#method-listgridseteditvalue) or [ListGrid.setEditValues](#method-listgridseteditvalues).

Can also be overridden on a per-field basis via [field.editorEnter](ListGridField.md#method-listgridfieldeditorenter).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for the cell being edited. **Will be null** for a new, unsaved record. |
| value | [Any](#type-any) | false | — | value for the cell being edited |
| rowNum | [int](../reference.md#type-int) | false | — | row number for the cell |
| colNum | [int](../reference.md#type-int) | false | — | column number of the cell |

### Groups

- editing

### See Also

- [ListGridField.editorEnter](ListGridField.md#method-listgridfieldeditorenter)

---
