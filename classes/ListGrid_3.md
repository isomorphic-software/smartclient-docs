# ListGrid Documentation (Part 3 of 3)

[← Back to API Index](../reference.md)

---

## Method: ListGrid.openGroup

### Description
Opens the node represented by the "record" parameter, if it is a folder and is not already open. This method only applies to [grouped](ListGrid_2.md#method-listgridgroupby) ListGrids.

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
Default implementation: If [ListGridField.valueIcons](ListGridField.md#attr-listgridfieldvalueicons) is specified for the title field of this grid (see [ListGrid.getTitleField](ListGrid_2.md#method-listgridgettitlefield)), the appropriate value icon will be displayed. If no appropriate valueIcon can be found, the icon will be derived from [ListGrid.trackerImage](ListGrid_1.md#attr-listgridtrackerimage).  
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
Returns the unmirrored or logical horizontal alignment for the specified cell's contents. The default implementation returns [ListGridField.cellAlign](ListGridField.md#attr-listgridfieldcellalign) if set or else [ListGridField.align](ListGridField.md#attr-listgridfieldalign), and mirrors this alignment in [RTL mode](Page.md#classmethod-pageisrtl) if [ListGrid.reverseRTLAlign](ListGrid_1.md#attr-listgridreversertlalign) is `true`.

This method is an override point. Custom implementations are required to peform their own mirroring if mirroring in RTL mode is desired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | this cell's record |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[Alignment](../reference_2.md#type-alignment)` — Horizontal alignment of cell contents: 'right', 'center', or 'left'

### See Also

- [ListGrid.getCellStyle](ListGrid_2.md#method-listgridgetcellstyle)

---
## Method: ListGrid.recordMarkedAsRemoved

### Description
Returns true if the specified record is marked as removed via a call to [ListGrid.markRecordRemoved](ListGrid_2.md#method-listgridmarkrecordremoved)

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

For a drop from another widget, [ListGrid.transferDragData](ListGrid_2.md#method-listgridtransferdragdata) is called, which depending on the [dragDataAction](ListGrid_1.md#attr-listgriddragdataaction) specified on the source widget, may either remove the source records from the original list (`dragDataAction:"move"`) or just provide a copy to this list (`dragDataAction:"copy"`).

If this grid is databound, the new records will be added to the dataset by calling [DataSource.addData](DataSource_1.md#method-datasourceadddata). Further, if the new records were dragged from another databound component, and [addDropValues](DataBoundComponent.md#attr-databoundcomponentadddropvalues) is true, [getDropValues](DataBoundComponent.md#method-databoundcomponentgetdropvalues) will be called for every item being dropped.

For multi-record drops, Queuing is automatically used to combine all DSRequests into a single HTTP Request (see QuickStart Guide, Server Framework chapter). This allows the server to persist all changes caused by the drop in a single transaction (and this is automatically done when using the built-in server DataSources with Power Edition and above).

Note that reordering records has no effect on a databound grid.

The newly dropped data is then selected automatically.

If these default persistence behaviors are undesirable, return false to cancel them, then and implement your own behavior, typically by using grid.updateData() or addData() to add new records.

**NOTE:** the records you receive in this event are the actual Records from the source component. Use [DataSource.copyRecords](DataSource_1.md#method-datasourcecopyrecords) to create a copy before modifying the records or using them with updateData() or addData().

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

`[Boolean](#type-boolean)` — whether to cancel the event

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

Note: if [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) is true, the criteria returned by this method may not match the values currently displayed in the filter editor, since the user may have entered values which have not yet been applied to our data. [ListGrid.getFilterEditorCriteria](ListGrid_2.md#method-listgridgetfiltereditorcriteria) may be used to retrieve the current criteria displayed in the filterEditor.

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

- [ListGrid.getRecord](ListGrid_2.md#method-listgridgetrecord)
- [ListGrid.getEditedRecord](ListGrid_2.md#method-listgridgeteditedrecord)

**Flags**: A

---
## Method: ListGrid.getEditorValueMap

### Description
Returns the valueMap to display for a field when it is displayed in the editor while editing some record.  
Called when a user starts to edit a field, or whenever the field valueMap is updated via a call to [ListGrid.setValueMap](ListGrid_2.md#method-listgridsetvaluemap) or [ListGrid.setEditorValueMap](#method-listgridseteditorvaluemap). Default implementation will return the `field.editorValueMap` if specified, otherwise `field.valueMap` - can be overridden to provide a different specific valueMap for some field based on the record/field data.

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
Returns the current sort field for this grid. Note that if [ListGrid.setSort](ListGrid_2.md#method-listgridsetsort) has been used to sort by multiple fields, you can call [ListGrid.getSort](ListGrid_2.md#method-listgridgetsort) to retrieve details about the complete sort applied to the grid.

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
Setter for [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth). Enables or disables dynamic autoFitWidth behavior on the specified field. Note if the field is currently autoFitWidth:true, and this method is disabling autoFit, the field will not be resized by default - if you wish to resize to an explicit width, use [ListGrid.resizeField](ListGrid_2.md#method-listgridresizefield).

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
Event handler for when rows in the body are clicked upon. The default implementation handles firing [ListGrid.startEditing](ListGrid_2.md#method-listgridstartediting) if appropriate, and fires [ListGridField.recordClick](ListGridField.md#method-listgridfieldrecordclick) and/or [ListGrid.recordClick](ListGrid_2.md#method-listgridrecordclick) if set. Developers should typically implement recordClick rather than overriding this method.

Note that this method fires in addition to any specified [ListGrid.cellClick](ListGrid_2.md#method-listgridcellclick) handler (even if that method cancels the event as a whole by returning `false`).

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

- [ListGrid.recordClick](ListGrid_2.md#method-listgridrecordclick)

**Flags**: A

---
## Method: ListGrid.editorEnter

### Description
Callback fired when the user starts editing a new cell.

This callback is typically used to establish dynamic default values via [ListGrid.setEditValue](ListGrid_2.md#method-listgridseteditvalue) or [ListGrid.setEditValues](ListGrid_2.md#method-listgridseteditvalues).

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
