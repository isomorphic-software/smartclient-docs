# ListGrid Documentation (Part 3 of 3)

[← Back to API Index](../reference.md)

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
Called when a user starts to edit a field, or whenever the field valueMap is updated via a call to [ListGrid.setValueMap](ListGrid_2.md#method-listgridsetvaluemap) or [ListGrid.setEditorValueMap](ListGrid_2.md#method-listgridseteditorvaluemap). Default implementation will return the `field.editorValueMap` if specified, otherwise `field.valueMap` - can be overridden to provide a different specific valueMap for some field based on the record/field data.

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
