# ListGridRecord Documentation

[← Back to API Index](../reference.md)

---

## Attr: ListGridRecord.embeddedComponent

### Description
A component that should be rendered on top of this record, similar to a [record component](ListGrid_1.md#attr-listgridshowrecordcomponents) but statically defined on the record.

The embedded component will default to covering all fields of the record, but specific fields can be specified via [ListGridRecord.embeddedComponentFields](#attr-listgridrecordembeddedcomponentfields).

By default, the embeddedComponent will fill the entire vertical and horizontal space of the record (or of the specified fields). [ListGridRecord.embeddedComponentPosition](#attr-listgridrecordembeddedcomponentposition) can be set to control exact sizing behavior.

When creating a component to use as an embedded component the component will most likely end up drawing before the record it is due to be embedded within, therefore it is recommended to set [autoDraw](Canvas.md#attr-canvasautodraw) to false on the embedded component.

When a record with an `embeddedComponent` is eliminated from view by filtering or because it is not currently rendered due to [incremental rendering](ListGrid_1.md#attr-listgridshowallrecords), the ListGrid may [Canvas.hide](Canvas.md#method-canvashide) or [Canvas.clear](Canvas.md#method-canvasclear) it.

If the current dataset is completely replaced (by a call to [ListGrid.setData](ListGrid_2.md#method-listgridsetdata) or [ListGrid.setDataSource](ListGrid_1.md#method-listgridsetdatasource), for example), any embedded component is [deparented](Canvas.md#method-canvasdeparent) (which implies being [clear()ed](Canvas.md#method-canvasclear)).

When a ListGrid is [destroyed](Canvas.md#method-canvasdestroy), it will destroy() all embedded components regardless of whether they are currently visible. Use a call to [ListGrid.setData](ListGrid_2.md#method-listgridsetdata) immediately before destroying the ListGrid to avoid this effect when unwanted.

For more advanced control over the lifecycle of components displayed over records, including deferred creation and pooling, use the [record components](ListGrid_1.md#attr-listgridshowrecordcomponents) subsystem.

### Groups

- appearance

**Flags**: IR

---
## Attr: ListGridRecord._canRemove

### Description
Default property name denoting whether this record can be removed. Property name may be modified for the grid via [ListGrid.recordCanRemoveProperty](ListGrid_1.md#attr-listgridrecordcanremoveproperty).

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGridRecord.includeInSummary

### Description
If specified as false this record should be ignored when calculating summary totals to be shown in the [summary row](ListGrid_1.md#attr-listgridshowgridsummary) for this grid.

Note that `includeInSummary` is the default property name for this attribute, but it may be modified via [ListGrid.includeInSummaryProperty](ListGrid_1.md#attr-listgridincludeinsummaryproperty).

**Flags**: IRW

---
## Attr: ListGridRecord.embeddedComponentFields

### Description
Fields where the [ListGridRecord.embeddedComponent](#attr-listgridrecordembeddedcomponent) will be displayed, if specified.

Regardless of the order of fields specified, the component will appear from whichever field is earlier in the current visible order to whichever field is later, inclusive of the specified fields.

To have the component appear in just one field, either specify a single-element Array or specific a two element Array with both fields the same.

If either field is hidden or invalid (no such field), the component will occupy only a single field. If both fields are hidden, the component will be hidden until one or more of the fields are shown.

### Groups

- appearance

**Flags**: IR

---
## Attr: ListGridRecord.backgroundComponent

### Description
Has no effect unless [ListGrid.showBackgroundComponents](ListGrid_1.md#attr-listgridshowbackgroundcomponents) is `true`.

Canvas created and embedded in the body behind a given record. When set, either as a Canvas or Canvas Properties, will be constructed if necessary, combined with the autoChild properties specified for [ListGrid.backgroundComponent](ListGrid_1.md#attr-listgridbackgroundcomponent) and displayed behind this record in the page's z-order, meaning it will only be visible if the cell styling is transparent.

### Groups

- rowEffects

**Flags**: IR

---
## Attr: ListGridRecord.canSelect

### Description
Default property name denoting whether this record can be selected. Property name may be modified for the grid via [ListGrid.recordCanSelectProperty](ListGrid_1.md#attr-listgridrecordcanselectproperty).

**Flags**: IR

---
## Attr: ListGridRecord._baseStyle

### Description
Name of a CSS style to use as the [ListGrid.baseStyle](ListGrid_1.md#attr-listgridbasestyle) for all cells for this particular record.

The styleName specified with have suffixes appended to it as the record changes state ("Over", "Selected" and so forth) as described by [ListGrid.getCellStyle](ListGrid_2.md#method-listgridgetcellstyle). For a single, fixed style for a record, use [ListGridRecord.customStyle](#attr-listgridrecordcustomstyle) instead.

See [ListGrid.getCellStyle](ListGrid_2.md#method-listgridgetcellstyle) for an overview of various ways to customize styling, both declarative and programmatic.

If this property is changed after draw(), to refresh the grid call [ListGrid.refreshRow](ListGrid_2.md#method-listgridrefreshrow) (or [ListGrid.markForRedraw](ListGrid_2.md#method-listgridmarkforredraw) if several rows are being refreshed).

If your application's data uses the "\_baseStyle" attribute for something else, the property name can be changed via [ListGrid.recordBaseStyleProperty](ListGrid_1.md#attr-listgridrecordbasestyleproperty).

**Flags**: IRW

---
## Attr: ListGridRecord.isGridSummary

### Description
This attribute will automatically be set to true for the record representing the grid-level summary row shown if [ListGrid.showGridSummary](ListGrid_1.md#attr-listgridshowgridsummary) is true.

Note that `isGridSummary` is the default property name for this attribute but it may be modified by setting [ListGrid.gridSummaryRecordProperty](ListGrid_1.md#attr-listgridgridsummaryrecordproperty)

**Flags**: IRW

---
## Attr: ListGridRecord._canEdit

### Description
Default property name denoting whether this record can be edited. Property name may be modified for the grid via [ListGrid.recordEditProperty](ListGrid_1.md#attr-listgridrecordeditproperty).

### Groups

- editing

**Flags**: IR

---
## Attr: ListGridRecord.enabled

### Description
Default property name denoting whether this record is enabled. Property name may be modified for some grid via [ListGrid.recordEnabledProperty](ListGrid_1.md#attr-listgridrecordenabledproperty).

**Flags**: IR

---
## Attr: ListGridRecord.isSeparator

### Description
Default property name denoting a separator row.  
When set to `true`, defines a horizontal separator in the listGrid object. Typically this is specified as the only property of a record object, since a record with `isSeparator:true` will not display any values.  
Note: this attribute name is governed by [ListGrid.isSeparatorProperty](ListGrid_1.md#attr-listgridisseparatorproperty).

**Flags**: IR

---
## Attr: ListGridRecord.singleCellValue

### Description
Default property name denoting the single value to display for all fields of this row. If this property is set for some record, the record will be displayed as a single cell spanning every column in the grid, with contents set to the value of this property.  
Note: this attribute name is governed by [ListGrid.singleCellValueProperty](ListGrid_1.md#attr-listgridsinglecellvalueproperty).

**Flags**: IRW

---
## Attr: ListGridRecord.isGroupSummary

### Description
This attribute will automatically be set to true for records representing group-level summary rows shown if [ListGrid.showGroupSummary](ListGrid_1.md#attr-listgridshowgroupsummary) is true.

Note that `isGroupSummary` is the default property name for this attribute but it may be modified by setting [ListGrid.groupSummaryRecordProperty](ListGrid_1.md#attr-listgridgroupsummaryrecordproperty)

**Flags**: IRW

---
## Attr: ListGridRecord.showRollOver

### Description
Set to false to disable rollover for this individual record when [ListGrid.showRollOver](ListGrid_1.md#attr-listgridshowrollover) is true.

Note this property can be renamed to prevent collision with data members - see [ListGrid.recordShowRollOverProperty](ListGrid_1.md#attr-listgridrecordshowrolloverproperty).

### Groups

- appearance

**Flags**: IR

---
## Attr: ListGridRecord.canExpand

### Description
Default property name denoting whether this record can be expanded. Property name may be modified for the grid via [ListGrid.canExpandRecordProperty](ListGrid_1.md#attr-listgridcanexpandrecordproperty).

### Groups

- expansionField

**Flags**: IR

---
## Attr: ListGridRecord.customStyle

### Description
Name of a CSS style to use for all cells for this particular record.

Note that using this property assigns a single, fixed style to the record, so rollover and selection styling are disabled. To provide a series of stateful styles for a record use [ListGridRecord._baseStyle](#attr-listgridrecord_basestyle) instead.

See [ListGrid.getCellStyle](ListGrid_2.md#method-listgridgetcellstyle) for an overview of various ways to customize styling, both declarative and programmatic.

If this property is changed after draw(), to refresh the grid call [ListGrid.refreshRow](ListGrid_2.md#method-listgridrefreshrow) (or [ListGrid.markForRedraw](ListGrid_2.md#method-listgridmarkforredraw) if several rows are being refreshed).

If your application's data uses the "customStyle" attribute for something else, the property name can be changed via [ListGrid.recordCustomStyleProperty](ListGrid_1.md#attr-listgridrecordcustomstyleproperty).

**Flags**: IRW

---
## Attr: ListGridRecord.canAcceptDrop

### Description
When set to `false`, other records cannot be dropped on (i.e., inserted via drag and drop) immediately before this record.

**Flags**: IR

---
## Attr: ListGridRecord.linkText

### Description
The HTML to display in this row for fields with fieldType set to link. This overrides [ListGridField.linkText](ListGridField.md#attr-listgridfieldlinktext).

### Groups

- display_values

### See Also

- [ListGridFieldType](../reference.md#type-listgridfieldtype)
- [FieldType](../reference.md#type-fieldtype)
- [ListGridField.linkText](ListGridField.md#attr-listgridfieldlinktext)
- [ListGrid.linkTextProperty](ListGrid_1.md#attr-listgridlinktextproperty)

**Flags**: IRW

---
## Attr: ListGridRecord.embeddedComponentPosition

### Description
Sizing policy applied to the embedded component. Default behavior if unspecified is the same as [EmbeddedPosition](../reference.md#type-embeddedposition) "within" (fill space allocated to the record, including the ability use percentage sizing and snapTo offset). Use "expand" to have the record expand to accomodate the embedded components' specified sizes instead.

### Groups

- appearance

**Flags**: IR

---
## Attr: ListGridRecord.detailDS

### Description
The default value of [ListGrid.recordDetailDSProperty](ListGrid_1.md#attr-listgridrecorddetaildsproperty).

**Flags**: IRWA

---
## Attr: ListGridRecord.canDrag

### Description
When set to `false`, this record cannot be dragged. If canDrag is false for any record in the current selection, none of the records will be draggable.

**Flags**: IR

---
