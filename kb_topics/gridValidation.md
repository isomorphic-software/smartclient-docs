# gridValidation

[← Back to API Index](../main.md)

---

## KB Topic: gridValidation

### Description
ListGrids support automatic validation of edited cells / records. This group is a collection of APIs related to the validation subsystem.

Default validation occurs in response to the user navigating between edit cells (see [ListGrid.validateByCell](../classes/ListGrid_1.md#attr-listgridvalidatebycell)) or whenever edited values are to be committed to the server for saving. Standard validation can also be triggered for a cell or row programmatically at any time.  
When standard validation occurs, [ListGridField.validators](../classes/ListGridField.md#attr-listgridfieldvalidators) will be run on each cell to be validated.  
In addition to this standard behavior developers can add custom errors to fields via [ListGrid.setFieldError](../classes/ListGrid_2.md#method-listgridsetfielderror) / [ListGrid.setFieldError](../classes/ListGrid_2.md#method-listgridsetfielderror).

### Related

- [ListGrid.validateRow](../classes/ListGrid_2.md#method-listgridvalidaterow)
- [ListGrid.validateCell](../classes/ListGrid_2.md#method-listgridvalidatecell)
- [ListGrid.getRequiredFieldMessage](../classes/ListGrid_2.md#method-listgridgetrequiredfieldmessage)
- [ListGrid.hasErrors](../classes/ListGrid_2.md#method-listgridhaserrors)
- [ListGrid.rowHasErrors](../classes/ListGrid_2.md#method-listgridrowhaserrors)
- [ListGrid.cellHasErrors](../classes/ListGrid_2.md#method-listgridcellhaserrors)
- [ListGrid.getRowErrors](../classes/ListGrid_2.md#method-listgridgetrowerrors)
- [ListGrid.getCellErrors](../classes/ListGrid_2.md#method-listgridgetcellerrors)
- [ListGrid.setFieldError](../classes/ListGrid_2.md#method-listgridsetfielderror)
- [ListGrid.setRowErrors](../classes/ListGrid_2.md#method-listgridsetrowerrors)
- [ListGrid.clearFieldError](../classes/ListGrid_2.md#method-listgridclearfielderror)
- [ListGridField.validators](../classes/ListGridField.md#attr-listgridfieldvalidators)
- [ListGridField.validateOnChange](../classes/ListGridField.md#attr-listgridfieldvalidateonchange)
- [ListGridField.required](../classes/ListGridField.md#attr-listgridfieldrequired)
- [ListGrid.validateByCell](../classes/ListGrid_1.md#attr-listgridvalidatebycell)
- [ListGrid.validateOnChange](../classes/ListGrid_1.md#attr-listgridvalidateonchange)
- [ListGrid.neverValidate](../classes/ListGrid_1.md#attr-listgridnevervalidate)

### See Also

- [editing](editing.md#kb-topic-grid-editing)

---
