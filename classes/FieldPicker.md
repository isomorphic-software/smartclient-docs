# FieldPicker Documentation

[← Back to API Index](../reference.md)

---

## Class: FieldPicker

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
FieldPicker provides a configuration dialog that displays, side-by-side, the available and currently-displayed fields of a [DataBoundComponent](../reference.md#interface-databoundcomponent). It allows for easy customization of the order in which the fields of a [DataBoundComponent](../reference.md#interface-databoundcomponent) are displayed, and of which are visible. If so configured, it also allows for convenient launching of the HiliteEditor, FormulaBuilder, and SummaryBuilder. A FieldPicker instance runs in its own window, a [FieldPickerWindow](FieldPickerWindow.md#class-fieldpickerwindow)

---
## Attr: FieldPicker.instructionLabel

### Description
A [label](Label.md#class-label) displaying the text assigned as the FieldPicker's [instructions](#attr-fieldpickerinstructions). Shown across the top of the widget.

**Flags**: IR

---
## Attr: FieldPicker.confirmText

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.removeText

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.cancelChangesButton

### Description
An AutoChild [button](../reference.md#class-ibutton) that saves the current field-set and exits the Field Picker.

**Flags**: IR

---
## Attr: FieldPicker.showFieldOrderButtons

### Description
When set to false, hides the right-most set of buttons, used for re-ordering fields in the Visible Fields list.

**Flags**: IR

---
## Attr: FieldPicker.currentFieldsGrid

### Description
A [ListGrid](ListGrid_1.md#class-listgrid) showing the list of currently selected fields.

**Flags**: IR

---
## Attr: FieldPicker.availableFieldsHeaderControls

### Description
Provides a set of controls to appear as [section header controls](SectionHeader.md#attr-sectionheadercontrols) above the available fields grid.

**Flags**: IR

---
## Attr: FieldPicker.saveAndExitButton

### Description
An AutoChild [button](../reference.md#class-ibutton) that saves the current field-set and exits the Field Picker.

**Flags**: IR

---
## Attr: FieldPicker.hilitesText

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.availableFieldsGrid

### Description
A [ListGrid](ListGrid_1.md#class-listgrid) showing the list of available fields.

**Flags**: IR

---
## Attr: FieldPicker.availableFieldsTitle

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.showHilitesButton

### Description
Shows a "Highlights..." button that shows an interface for editing hilites in the attached DataBoundComponent.

**Flags**: IR

---
## Attr: FieldPicker.addCustomFieldsButtonTitle

### Description
The title displayed for the Add Custom Fields Button

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.availableTitleTitle

### Description
The title displayed for the title property of the available fields

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.currentFieldsTitle

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.emptyTitleHint

### Description
The hint shown when editing a field with no title defined.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.dataSource

### Description
An optional DataSource that is used to create a disposable [FieldPicker.dataBoundComponent](#attr-fieldpickerdataboundcomponent) if none is provided. Has no effect if a [FieldPicker.dataBoundComponent](#attr-fieldpickerdataboundcomponent) is specified.

**Flags**: IR

---
## Attr: FieldPicker.sampleValueTitle

### Description
The title displayed for the sample value property of the current fields

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.saveAndExitButtonTitle

### Description
The title shown on the Save and Exit button

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.buttonLayout

### Description
A [horizontal layout](../reference.md#class-hlayout) used to show the [Save](#attr-fieldpickersaveandexitbutton) and [Cancel](#attr-fieldpickercancelchangesbutton) buttons.

**Flags**: IR

---
## Attr: FieldPicker.currentTitleTitle

### Description
The title displayed for the title property of the current fields

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.canFilterSampleValue

### Description
Whether the current fields' filter row allows the sample value column to be filtered.

### See Also

- [FieldPicker.sampleValueTitle](#attr-fieldpickersamplevaluetitle)
- [FieldPicker.sampleRecord](#attr-fieldpickersamplerecord)

**Flags**: IR

---
## Attr: FieldPicker.instructions

### Description
—

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.cancelButtonTitle

### Description
The title shown on the Cancel button

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.removeItemTitle

### Description
The title shown on the 'Visible Fields' grid's context menu item, whose click handler puts the selected item back in the 'Available Fields' collection.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: FieldPicker.sampleRecord

### Description
If a `sampleRecord` is provided, the FieldPicker will show a second column in the Current Fields dialog showing the cell value that will appear for that field given the provided sample record.  
A value of "first" means the first record. If the underlying [FieldPicker.dataBoundComponent](#attr-fieldpickerdataboundcomponent) is a [TreeGrid](TreeGrid.md#class-treegrid), you can specify "firstOpenLeaf" to use the first open leaf as the sampleRecord (this is often desirable in trees where the first record may be a folder that's used for organizational purposes only and hence would have no actual data for columns other than the tree column).

**Flags**: IR

---
## Attr: FieldPicker.dataBoundComponent

### Description
The component whose fields should be edited.

Note that if [DataBoundComponent.useAllDataSourceFields](DataBoundComponent.md#attr-databoundcomponentusealldatasourcefields) is set on the component, it will be cleared when the FieldPicker applies the requested ordering since that setting imposes a fixed ordering on the fields.

**Flags**: IR

---
## Method: FieldPicker.callback

### Description
Callback invoked when picker changes are committed, if a disposable [DataBoundComponent](../reference.md#interface-databoundcomponent) is present.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fields | [Array of ListGridField](#type-array-of-listgridfield) | false | — | committed fields from disposable component |
| hilites | [Array of Hilite](#type-array-of-hilite) | false | — | Array of hilite objects |

### See Also

- [FieldPicker.dataSource](#attr-fieldpickerdatasource)

---
## Method: FieldPicker.setAvailableFields

### Description
Provides a new set of available fields.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newFields | [Array of DataSourceField](#type-array-of-datasourcefield) | false | — | — |

---
