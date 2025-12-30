# GridEditProxy Documentation

[← Back to API Index](../reference.md)

---

## Class: GridEditProxy

*Inherits from:* [LayoutEditProxy](../reference.md#class-layouteditproxy)

### Description
[EditProxy](EditProxy.md#class-editproxy) that handles [ListGrid](ListGrid_1.md#class-listgrid) and [TreeGrid](TreeGrid.md#class-treegrid) components when editMode is enabled.

### Groups

- devTools

---
## Attr: GridEditProxy.generateEditableHilites

### Description
Controls whether highlights created while in edit mode are editable by end users at runtime (when the grid is no longer in edit mode). See [Hilite.canEdit](Hilite.md#attr-hilitecanedit).

**Flags**: IR

---
## Attr: GridEditProxy.saveFieldVisibility

### Description
Should changes to grid field visibility be persisted?

Note that changes are saved directly into the ListGridFields not via fieldState or viewState settings. EditNodes will also be introduced for fields as needed if they do not already exist.

Only valid with [SelectedAppearance](../reference_2.md#type-selectedappearance) settings that allow direct interactivity (such as "outlineEdges").

**Flags**: IR

---
## Attr: GridEditProxy.canResizeFields

### Description
Indicates whether fields in this listGrid can be resized by dragging header fields. Overrides [ListGrid.canResizeFields](ListGrid_1.md#attr-listgridcanresizefields) when in edit mode.

**Flags**: IR

---
## Attr: GridEditProxy.saveGroupBy

### Description
Should changes to grid grouping (including both grouping and ungrouping the grid) be persisted?

Only valid with [SelectedAppearance](../reference_2.md#type-selectedappearance) settings that allow direct interactivity (such as "outlineEdges").

**Flags**: IR

---
## Attr: GridEditProxy.generateEditableSummaries

### Description
Controls whether summary fields created while in edit mode are editable by end users at runtime (when the grid is no longer in edit mode). See [ListGridField.canEditSummary](ListGridField.md#attr-listgridfieldcaneditsummary).

**Flags**: IR

---
## Attr: GridEditProxy.canAddFormulaFields

### Description
Can new formula fields be created from header context menu? Overrides [ListGrid.canAddFormulaFields](ListGrid_1.md#attr-listgridcanaddformulafields) when in edit mode.

**Flags**: IR

---
## Attr: GridEditProxy.saveFieldOrder

### Description
Should changes to grid field order be persisted?

Note that changes are saved directly into the ListGridFields not via fieldState or viewState settings. EditNodes will also be introduced for fields as needed if they do not already exist.

Only valid with [SelectedAppearance](../reference_2.md#type-selectedappearance) settings that allow direct interactivity (such as "outlineEdges").

**Flags**: IR

---
## Attr: GridEditProxy.saveFieldFrozenState

### Description
Should changes to which fields are [frozen](ListGridField.md#attr-listgridfieldfrozen) be persisted?

Note that changes are saved directly into the ListGridFields not via fieldState or viewState settings. EditNodes will also be introduced for fields as needed if they do not already exist.

Only valid with [SelectedAppearance](../reference_2.md#type-selectedappearance) settings that allow direct interactivity (such as "outlineEdges").

**Flags**: IR

---
## Attr: GridEditProxy.canReorderFields

### Description
Indicates whether fields in this listGrid can be reordered by dragging and dropping header fields. Overrides [ListGrid.canReorderFields](ListGrid_1.md#attr-listgridcanreorderfields) when in edit mode.

**Flags**: IR

---
## Attr: GridEditProxy.saveFilterCriteria

### Description
Should changes to filter criteria by end user editing of criteria in the [filter editor](ListGrid_1.md#attr-listgridshowfiltereditor) by persisted?

Only valid with [SelectedAppearance](../reference_2.md#type-selectedappearance) settings that allow direct interactivity (such as "outlineEdges").

**Flags**: IR

---
## Attr: GridEditProxy.canAddSummaryFields

### Description
Can new summary fields be created from header context menu? Overrides [ListGrid.canAddSummaryFields](ListGrid_1.md#attr-listgridcanaddsummaryfields) when in edit mode.

**Flags**: IR

---
## Attr: GridEditProxy.canGroupBy

### Description
Can records be grouped from header context menu? Overrides [ListGrid.canGroupBy](ListGrid_1.md#attr-listgridcangroupby) when in edit mode.

**Flags**: IR

---
## Attr: GridEditProxy.saveSort

### Description
Should changes to which fields are sorted be persisted?

Only valid with [SelectedAppearance](../reference_2.md#type-selectedappearance) settings that allow direct interactivity (such as "outlineEdges").

**Flags**: IR

---
## Attr: GridEditProxy.canEditHilites

### Description
Can highlights be edited from header context menu? Overrides [ListGrid.canEditHilites](ListGrid_1.md#attr-listgridcanedithilites) when in edit mode.

**Flags**: IR

---
## Attr: GridEditProxy.generateEditableFormulas

### Description
Controls whether formula fields created while in edit mode are editable by end users at runtime (when the grid is no longer in edit mode). See [ListGridField.canEditFormula](ListGridField.md#attr-listgridfieldcaneditformula).

**Flags**: IR

---
## Method: GridEditProxy.setInlineEditText

### Description
Save the new value into the component's state. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to commit the change.

Updates the grid's data and field configuration.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | the new grid configuration |

---
## Method: GridEditProxy.getInlineEditText

### Description
Returns the text based on the current component state to be edited inline. Called by the [EditProxy.inlineEditForm](EditProxy.md#attr-editproxyinlineeditform) to obtain the starting edit value.

Returns the grid's wiki-style data - see [MockDataSource.mockData](MockDataSource.md#attr-mockdatasourcemockdata) for a description of this format.

---
