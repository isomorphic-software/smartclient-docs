# RecordEditor Documentation

[← Back to API Index](../reference.md)

---

## Class: RecordEditor

*Inherits from:* [ListGrid](ListGrid_1.md#class-listgrid)

### Description
Component for editing a single record.  
RecordEditors are implemented as a subclass of ListGrid, showing no header and a single row always drawn in the editable state, allowing the user to modify the values at any time. The [RecordEditor.actionButton](#attr-recordeditoractionbutton) is automatically shown as a way for the user to act upon the edited values.

The RecordEditor class exists as a helper class for ListGrids, used to provide an interface for editing criteria when [filterEditor](ListGrid_1.md#attr-listgridshowfiltereditor) is set to true.

### See Also

- [ListGrid.showFilterEditor](ListGrid_1.md#attr-listgridshowfiltereditor)
- [ListGrid.filterEditor](ListGrid_1.md#attr-listgridfiltereditor)

---
## Attr: RecordEditor.filterImg

### Description
[Icon](Button.md#attr-buttonicon) to show on the [RecordEditor.actionButton](#attr-recordeditoractionbutton) if this component is being used as a [ListGrid.filterEditor](ListGrid_1.md#attr-listgridfiltereditor).

Note that this [SCImgURL](../reference_2.md#type-scimgurl) will be resolved using the [RecordEditor.skinImgDir](#attr-recordeditorskinimgdir) defined for the RecordEditor.

**Flags**: IR

---
## Attr: RecordEditor.actionButtonProperties

### Description
Properties to apply to the automatically generated [RecordEditor.actionButton](#attr-recordeditoractionbutton).

Note that for a recordEditor being used as a [ListGrid.filterEditor](ListGrid_1.md#attr-listgridfiltereditor), the [ListGrid.filterButtonProperties](ListGrid_1.md#attr-listgridfilterbuttonproperties) can be used to specify actionButton properties directly at the grid level.

**Flags**: IRA

---
## Attr: RecordEditor.baseStyle

### Description
[base cell style](GridRenderer.md#attr-gridrendererbasestyle) for this listGrid. If this property is unset, base style may be derived from [ListGrid.normalBaseStyle](ListGrid_1.md#attr-listgridnormalbasestyle) or [ListGrid.tallBaseStyle](ListGrid_1.md#attr-listgridtallbasestyle) as described in [ListGrid.getBaseStyle](ListGrid_2.md#method-listgridgetbasestyle).

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### Groups

- appearance

**Flags**: IR

---
## Attr: RecordEditor.actionButtonStyle

### Description
[baseStyle](Button.md#attr-buttonbasestyle) for the [RecordEditor.actionButton](#attr-recordeditoractionbutton)

**Flags**: IR

---
## Attr: RecordEditor.recordSummaryBaseStyle

### Description
If showing any record summary fields (IE: fields of [type:"summary"](../reference.md#type-listgridfieldtype)), this attribute specifies a custom base style to apply to cells in the summary field

**Flags**: IR

---
## Attr: RecordEditor.actionButton

### Description
Automatically created Button auto-child shown at the edge of the recordEditor. For a recordEditor acting as a [ListGrid.filterEditor](ListGrid_1.md#attr-listgridfiltereditor), this button will show the [RecordEditor.filterImg](#attr-recordeditorfilterimg) as an [Button.icon](Button.md#attr-buttonicon) by default.

Clicking this button will call [RecordEditor.performAction](#method-recordeditorperformaction) on the editor.

May be customized using the standard [AutoChild](../reference.md#type-autochild) pattern, by overriding [RecordEditor.actionButtonProperties](#attr-recordeditoractionbuttonproperties).

**Flags**: R

---
## Attr: RecordEditor.skinImgDir

### Description
Where do 'skin' images (those provided with the class) live?

**Flags**: IR

---
## Attr: RecordEditor.suppressNullValueFormat

### Description
Should non-editable fields within this record-editor always display the [empty cell value](ListGrid_1.md#attr-listgridemptycellvalue) for null values rather than running any specified [static formatters](ListGridField.md#method-listgridfieldformatcellvalue)?

This setting allows developers to easily account for the fact that a custom formatter for empty cells in a listGrid is often not appropriate to display in the filter editor for a `canFilter:false` field with no specified criterion.

**Flags**: IRA

---
## Method: RecordEditor.performAction

### Description
Fired when the user clicks the [RecordEditor.actionButton](#attr-recordeditoractionbutton) for this RecordEditor. May also be triggered from other user interaction with edit values (for example filter-editor change - see [ListGrid.filterOnKeypress](ListGrid_1.md#attr-listgridfilteronkeypress)).

This is the method which initiates a filter in a listGrid [filter editor](ListGrid_1.md#attr-listgridshowfiltereditor). Note that for custom filtering behavior, developers can use the [ListGrid.filterEditorSubmit](ListGrid_2.md#method-listgridfiltereditorsubmit) notification method rather than overriding this method directly.

---
