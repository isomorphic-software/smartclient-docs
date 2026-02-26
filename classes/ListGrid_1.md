# ListGrid Documentation (Part 1 of 2)

[← Back to API Index](../reference.md)

---

# ListGrid Documentation

[← Back to API Index](../reference.md)

---
## Class: ListGrid

*Inherits from:* [VLayout](../reference.md#class-vlayout)

### Description
A ListGrid is a [DataBoundComponent](../reference.md#interface-databoundcomponent) that displays a list of objects in a grid, where each row represents one object and each cell in the row represents one property.

---
## ClassAttr: ListGrid.BOTH

### Description
A declared value of the enum type [RecordDropAppearance](../reference_2.md#type-recorddropappearance).

**Flags**: R

---
## ClassAttr: ListGrid.UP_ARROW_KEYPRESS

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.INCREMENTAL

### Description
A declared value of the enum type [GroupTreeChangeType](../reference_2.md#type-grouptreechangetype)

**Flags**: R

---
## ClassAttr: ListGrid.REGROUP

### Description
A declared value of the enum type [GroupTreeChangeType](../reference_2.md#type-grouptreechangetype)

**Flags**: R

---
## ClassAttr: ListGrid.BODY

### Description
A declared value of the enum type [RecordDropAppearance](../reference_2.md#type-recorddropappearance).

**Flags**: R

---
## ClassAttr: ListGrid.SHIFT_TAB_KEYPRESS

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.CLICK_OUTSIDE

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.ENTER_KEYPRESS

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.CLICK

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.ESCAPE_KEYPRESS

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.OVER

### Description
A declared value of the enum types [RecordDropPosition](../reference.md#type-recorddropposition), [ReorderPosition](../reference.md#type-reorderposition) and [RecordDropAppearance](../reference_2.md#type-recorddropappearance).

**Flags**: R

---
## ClassAttr: ListGrid.DOUBLE_CLICK

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.PROGRAMMATIC

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.BEFORE

### Description
A declared value of the enum types [RecordDropPosition](../reference.md#type-recorddropposition) and [ReorderPosition](../reference.md#type-reorderposition).

**Flags**: R

---
## ClassAttr: ListGrid.GROUP_BY

### Description
A declared value of the enum type [GroupTreeChangeType](../reference_2.md#type-grouptreechangetype)

**Flags**: R

---
## ClassAttr: ListGrid.BETWEEN

### Description
A declared value of the enum type [RecordDropAppearance](../reference_2.md#type-recorddropappearance).

**Flags**: R

---
## ClassAttr: ListGrid.EDIT_FIELD_CHANGE

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.NONE

### Description
A declared value of the enum type [RecordDropPosition](../reference.md#type-recorddropposition).

**Flags**: R

---
## ClassAttr: ListGrid.DOWN_ARROW_KEYPRESS

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## ClassAttr: ListGrid.AFTER

### Description
A declared value of the enum types [RecordDropPosition](../reference.md#type-recorddropposition) and [ReorderPosition](../reference.md#type-reorderposition).

**Flags**: R

---
## ClassAttr: ListGrid.TAB_KEYPRESS

### Description
A declared value of the enum type [EditCompletionEvent](../reference.md#type-editcompletionevent).

**Flags**: R

---
## Attr: ListGrid.clipHeaderTitles

### Description
Whether the ListGrid should manage the clipping of titles of header buttons, showing ellipses if the title is clipped, and potentially showing the full title on [hover](#attr-listgridshowclippedheadertitlesonhover).

In some cases this may be preferable to the button component's default clipping behavior because if a [sort arrow](#attr-listgridshowsortarrow) or sort numeral is displayed for a header, then the button's default clipping behavior may clip the sort arrow/numeral whereas ListGrid-managed title clipping utilizes special HTML which keeps the sort arrow/numeral visible.

This feature is automatically enabled if supported by the browser. The only supported use of this attribute is to _disable_ the feature by setting clipHeaderTitles to false.

Note that this feature is incompatible with [ListGridField.wrap](ListGridField.md#attr-listgridfieldwrap), and will automatically be disabled for wrapping fields.

### Groups

- gridHeader
- appearance

### See Also

- [ListGrid.headerBaseStyle](#attr-listgridheaderbasestyle)

**Flags**: IRA

---
## Attr: ListGrid.hiliteCanReplaceValue

### Description
If set, end users can create advanced hiliting rules that will use the [Hilite.replacementValue](Hilite.md#attr-hilitereplacementvalue) feature to cause values in hilited cells to be replaced with a user-entered value. For example, a user could create a hilite rule that replaces numeric values ranging from 0.5 to 1.0 with the text "LOW".

Specifically, when the "Add Advanced Rule" button is pressed and `hiliteCanReplaceValue` is true, the user will see a text entry field titled "Replace value with" ([ListGrid.hiliteReplaceValueFieldTitle](#attr-listgridhilitereplacevaluefieldtitle)) and if they enter a value, that value will appear in the grid cell in lieu of the cell's original value.

### Groups

- hiliting

**Flags**: IR

---
## Attr: ListGrid.filterByCell

### Description
If we're showing the [filterEditor](#attr-listgridshowfiltereditor), should this list be filtered every time the user changes edit values for particular cells rather than waiting for an Enter keypress or a click on the filterEditor submit button.

Note that by default fields in the filter editor will be set to [changeOnKeypress:false](FormItem.md#attr-formitemchangeonkeypress), so the grid will not filter as the user types in text-based items.  
To enable filtering as the user types in text fields, we recommend the [ListGrid.filterOnKeypress](#attr-listgridfilteronkeypress) attribute. Also note that `filterOnKeypress:true` implies filtering will occur on change to edit values for cells, even if `filterByCell` is not set to true.

### Groups

- filterEditor

### See Also

- [ListGrid.fetchDelay](#attr-listgridfetchdelay)

**Flags**: IRWA

---
## Attr: ListGrid.autoFitExtraRecords

### Description
If [ListGrid.autoFitData](#attr-listgridautofitdata) is set to `"vertical"` or `"both"`, setting this property will cause the ListGrid body to size large enough to accommodate the actual data and also leave this many extra rows' worth of blank space below the last record. If a maximum size is specified via [ListGrid.autoFitMaxHeight](#attr-listgridautofitmaxheight) or [ListGrid.autoFitMaxRecords](#attr-listgridautofitmaxrecords), it will still be respected. Once the data set is large enough to fill or exceed that space, this property no longer has an effect.

### Groups

- autoFitData

**Flags**: IRW

---
## Attr: ListGrid.showGroupSummaryInHeader

### Description
If this grid is [grouped](ListGrid_2.md#method-listgridgroupby), and [ListGrid.showGroupSummary](#attr-listgridshowgroupsummary) is true, setting this property causes field summary values for each group to be displayed directly in the group header node, rather than showing up at the bottom of each expanded group.

Note that this means the group header node will be showing multiple field values rather than the default display of a single cell spanning all columns containing the group title. Developers may specify an explicit [ListGrid.groupTitleField](#attr-listgridgrouptitlefield), or rely on the automatically generated [groupTitleColumn](#attr-listgridshowgrouptitlecolumn) to have group titles be visible as well as the summary values.

Also note that multi-line group summaries are not supported when showing the group summary in the group header. If multiple [field summary functions](ListGridField.md#attr-listgridfieldsummaryfunction) are defined for some field only the first will be displayed when this property is set to true.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IRW

---
## Attr: ListGrid.sorterConstructor

### Description
Widget class for the corner sort button, if showing. This button displays the current sort direction of the primary sort field (either the only sorted field or the first in a [multi-sort](#attr-listgridcanmultisort) grid) and reverses the direction of that field when clicked. For consistent appearance, this is usually set to match [ListGrid.headerButtonConstructor](#attr-listgridheaderbuttonconstructor)

### Groups

- gridHeader
- appearance

**Flags**: IR

---
## Attr: ListGrid.collapseGroupOnRowClick

### Description
If [ListGrid.canCollapseGroup](#attr-listgridcancollapsegroup) is true, will a click anywhere on the group row toggle the group's expanded state? If false, the user must click the [ListGrid.groupIcon](#attr-listgridgroupicon) directly to toggle the group.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IR

---
## Attr: ListGrid.operatorIcon

### Description
Inline icon shown inside [filter editor](#attr-listgridshowfiltereditor) fields when [ListGrid.allowFilterOperators](#attr-listgridallowfilteroperators) is enabled.

**Flags**: I

---
## Attr: ListGrid.headerMenuButton

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, when the user rolls over the header buttons in this grid the headerMenuButton will be shown over the header button in question. When clicked this button will display the standard header context menu (see [ListGrid.displayHeaderContextMenu](ListGrid_2.md#method-listgriddisplayheadercontextmenu)).

[Several properties](../reference.md#kb-topic-headermenubutton) exist to customize the appearance of the headerMenuButton. Also see the [AutoChild](../reference.md#type-autochild) documentation for information on how to make free-form modifications to autoChild widgets

### Groups

- headerMenuButton

**Flags**: RA

---
## Attr: ListGrid.tableRowStyle

### Description
The style to apply to `<TR>` tags in this grid's table. Useful for applying spacing or a custom border between records in the grid.

This is an advanced capability and care should be taken not to use CSS that applies sizes or other settings that could cause sizing/rendering issues when used in conjunction with certain other features, such as [ListGrid.virtualScrolling](#attr-listgridvirtualscrolling). For example, the style should apply _box-sizing: border-box;_ to ensure that settings like border and padding don't change the size of row elements. In some cases, the style will also need to apply _display: inline-block;_ for CSS changes to take effect - this is because the default display setting for `<TR>` elements, _table-row_, has limited styling support.

**Flags**: IRWA

---
## Attr: ListGrid.editPendingMarkerStyle

### Description
The name of a CSS class used to overlay regular cell styles with additional styling when a cell has unsaved edits - these styles are in addition to the styling applied by [ListGrid.editPendingCSSText](#attr-listgrideditpendingcsstext) or [ListGrid.editPendingBaseStyle](#attr-listgrideditpendingbasestyle).

You can use a custom class that overlays styling of your choosing, or use the default _pendingMarker_ class which is present in modern skins and provides a small corner-marker in the top-left of unsaved cells.

Once set, this styleName is automatically appended to the style-list for cells with unsaved edits.

### Groups

- appearance

### See Also

- [ListGrid.baseStyle](#attr-listgridbasestyle)

**Flags**: IRWA

---
## Attr: ListGrid.removeFieldProperties

### Description
Configuration properties for the "remove field" displayed when [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) is enabled. These configuration settings will be overlaid on top of the [ListGrid.removeFieldDefaults](#attr-listgridremovefielddefaults).

**Flags**: IR

---
## Attr: ListGrid.headerMenuButtonSnapOffsetLeft

### Description
Offset of the right edge of a [ListGrid.headerMenuButton](#attr-listgridheadermenubutton) from the right edge of it's parent button.

**Flags**: IRW

---
## Attr: ListGrid.originBaseStyle

### Description
Name of a CSS Style to use as the [ListGrid.baseStyle](#attr-listgridbasestyle) for a cell that is currently a selection origin for shifted incremental cell selection. Only has an effect if [ListGrid.canSelectCells](#attr-listgridcanselectcells) is true.

**Flags**: IRW

---
## Attr: ListGrid.savedSearchStoredState

### Description
Set to "criteria" if you want only criteria to be stored for ListGrids and TreeGrids instead of the full viewState of the component.

### See Also

- [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem)

**Flags**: IR

---
## Attr: ListGrid.fieldPickerShowSampleValues

### Description
When set to false, sample values of the FieldPicker are never shown. This property applies to the entire FieldPicker.

**Flags**: IR

---
## Attr: ListGrid.fullRowRangeDisplayValue

### Description
Dynamic String specifying the format for the [row range summary value](ListGrid_2.md#method-listgridgetrowrangedisplayvalue) when [RowRangeDisplayStyle](../reference_2.md#type-rowrangedisplaystyle) is set to `"full"`.

The following variables are available for evaluation within this string:

*   `rowRange`: the [formatted row range](ListGrid_2.md#method-listgridgetformattedrowrange)
*   `rowCount`: the [formatted row count](ListGrid_2.md#method-listgridgetformattedrowcount)

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.showSelectionCanvas

### Description
If [selectionType](#attr-listgridselectiontype) is set to "single", setting this property to `true` means selection will be displayed to the user with the [selectionCanvas](#attr-listgridselectioncanvas) and/or [selectionUnderCanvas](#attr-listgridselectionundercanvas) rather than with CSS styling.

If `showSelectionCanvas` is set to `true`, then the `selectionUnderCanvas` will automatically be enabled unless [showSelectionUnderCanvas](#attr-listgridshowselectionundercanvas) is set to `false`.

NOTE: It is recommended to use the `selectionUnderCanvas` rather than the `selectionCanvas` if possible because the `selectionCanvas` is stacked on top of the selected record and this may interfere with event handling in rare cases. If no interactive components are shown in the `selectionCanvas` and it simply provides custom styling, then the `selectionUnderCanvas` should be used instead.

With [frozen fields](#attr-listgridcanfreezefields), the `selectionCanvas` is displayed only over the non-frozen fields of the selected row.

### Groups

- rowEffects

### See Also

- [ListGrid.showSelectionUnderCanvas](#attr-listgridshowselectionundercanvas)

**Flags**: IRWA

---
## Attr: ListGrid.rangeRowCountFormat

### Description
Format for the string returned from [ListGrid.getFormattedRowCount](ListGrid_2.md#method-listgridgetformattedrowcount) when [row count status](ListGrid_2.md#method-listgridgetrowcountstatus) is `"range"`.

The following variables are available for evaluation within this string:

*   `minRowCount`: the lower bound of this row count value from [getRowCountRange()\[0\]](ListGrid_2.md#method-listgridgetrowcountrange), as a [locale-formatted number](NumberUtil.md#classmethod-numberutiltolocalizedstring).
*   `minRowCount`: the upper bound of this row count value from [getRowCountRange()\[1\]](ListGrid_2.md#method-listgridgetrowcountrange), as a [locale-formatted number](NumberUtil.md#classmethod-numberutiltolocalizedstring).

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.rowSpanSelectionMode

### Description
Chooses the selection mode when [ListGrid.useRowSpanStyling](#attr-listgriduserowspanstyling) is enabled. See [RowSpanSelectionMode](../reference.md#type-rowspanselectionmode).

**Flags**: IR

---
## Attr: ListGrid.escapeKeyEditAction

### Description
What to do when a user hits escape while editing a cell:

*   "cancel": close the editor and discard the current set of edit values
*   "done": just close the editor (the edit is complete, but the edited values are retained).

Note that if [ListGrid.autoSaveEdits](#attr-listgridautosaveedits) is true, this may cause a save of the current edit values

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.allowFilterOperators

### Description
Causes a menu item titled ["Filter using"](#attr-listgridfilterusingtext) to appear in the [headerContextMenu](#attr-listgridshowheadercontextmenu) that allows the end user to pick an advanced [search operator](../reference.md#type-operatorid) to use for this field.

Once an operator has been chosen, the active operator is indicated by an [ListGrid.operatorIcon](#attr-listgridoperatoricon) placed within the field (you can alternatively cause the icon to [always be present](#attr-listgridalwaysshowoperatoricon)). The `operatorIcon` shows the same textual representation of the search operator as is used by the [FormItem.allowExpressions](FormItem.md#attr-formitemallowexpressions) feature. Clicking on the icon provides a second way to modify the search operator.

This feature is enabled by default if [DataSource.supportsAdvancedCriteria](DataSource.md#method-datasourcesupportsadvancedcriteria) is true, for all fields where it is normally possible to filter by typing in a search string. This excludes field types such as "date" or "boolean" which show specialized filter controls. Use [ListGridField.allowFilterOperators](ListGridField.md#attr-listgridfieldallowfilteroperators) to disable this interface for individual fields, or set [DataSourceField.canFilter](DataSourceField.md#attr-datasourcefieldcanfilter) to false to disallow filtering entirely for a field.

Note that this feature is similar to [ListGrid.allowFilterExpressions](#attr-listgridallowfilterexpressions), which allows the end users to directly type in characters such as ">" to control filtering. `allowFilterOperators` is easier to use and more discoverable than `allowFilterExpressions`, and also avoids the drawback where special characters like ">" cannot be used in filter values. However, `allowFilterExpressions` allows users to make use of certain operators that `allowFilterOperators` does not support, such as using the "betweenInclusive" operator by typing "5...10".

When both `allowfilterExpressions` and `allowFilterOperators` are set, filter expressions entered in to the edit-area are parsed and the operator automatically applied to the [ListGrid.operatorIcon](#attr-listgridoperatoricon).

If [ListGrid.allowFilterWindow](#attr-listgridallowfilterwindow) is enabled another option, ["Advanced Filtering"](#attr-listgridadvancedfilteringtext), is added to the "Filter using" menu.

### See Also

- [ListGrid.allowFilterWindow](#attr-listgridallowfilterwindow)

**Flags**: IR

---
## Attr: ListGrid.dragScrollRedrawDelay

### Description
Like [ListGrid.scrollRedrawDelay](#attr-listgridscrollredrawdelay), but applies when the component is being drag-scrolled (via a scrollbar). This value is typically set higher than [ListGrid.scrollRedrawDelay](#attr-listgridscrollredrawdelay) to avoid too many concurrent fetches to the server for [ResultSet](ResultSet.md#class-resultset)-backed components since it's quite easy to induce such a case with a scrollbar and a grid bound to a large databaset.

### Groups

- performance

**Flags**: IRW

---
## Attr: ListGrid.expansionFieldImageShowSelected

### Description
Should a "\_selected" suffix be added to the [expansionFieldTrueImage](#attr-listgridexpansionfieldtrueimage) and [expansionFieldFalseImage](#attr-listgridexpansionfieldfalseimage) image URLs for selected rows?

This allows developers to provide separate expansion field media for selected rows, in case the selected row style does not contrast well with the standard expansion field image media.

If both this property and [ListGrid.expansionFieldImageShowRTL](#attr-listgridexpansionfieldimageshowrtl) are true, and the grid is in RTL mode, both suffixes will be applied to selected rows' expansion field image (combined as "selected\_rtl")

### Groups

- expansionField

**Flags**: IRA

---
## Attr: ListGrid.valueIconSize

### Description
Default width and height of value icons for this ListGrid. Can be overridden at the listGrid level via explicit [ListGrid.valueIconWidth](#attr-listgridvalueiconwidth) and [ListGrid.valueIconHeight](#attr-listgridvalueiconheight), or at the field level via [ListGridField.valueIconSize](ListGridField.md#attr-listgridfieldvalueiconsize), [ListGridField.valueIconWidth](ListGridField.md#attr-listgridfieldvalueiconwidth) and {ListGridField.valueIconHeight}

### Groups

- imageColumns

### See Also

- [ListGrid.valueIconWidth](#attr-listgridvalueiconwidth)
- [ListGrid.valueIconHeight](#attr-listgridvalueiconheight)
- [ListGridField.valueIconSize](ListGridField.md#attr-listgridfieldvalueiconsize)

**Flags**: IRW

---
## Attr: ListGrid.filterWindowCriteriaIndicator

### Description
Instance of [Canvas](Canvas.md#class-canvas) used to show visual indicator that [ListGrid.filterWindowCriteria](#attr-listgridfilterwindowcriteria) is configured. [ListGrid.showFilterWindowCriteriaIndicator](#attr-listgridshowfilterwindowcriteriaindicator) must be enabled to show indicator.

**Flags**: IR

---
## Attr: ListGrid.clearAllSortingText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, this attribute will be shown as the menu item title to clear any existing sort on all fields. This menu-item is displayed only in the context menu for the sorter button.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.booleanPartialImage

### Description
Image to display for a partially true value in a boolean field (typically selection). The special value "blank" means that no image will be shown.

To turn this off explicitly set [ListGridField.suppressValueIcon](ListGridField.md#attr-listgridfieldsuppressvalueicon) to true.

If this, [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage) and [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage) are unset, this will be set to the default [CheckboxItem.partialSelectedImage](CheckboxItem.md#attr-checkboxitempartialselectedimage).

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string. Alternatively developers can omit this property and instead use CSS directly in the [ListGrid.booleanBaseStyle](#attr-listgridbooleanbasestyle) property to provide a "boolean true" appearance.

### Groups

- imageColumns

### See Also

- [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage)
- [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage)
- [ListGrid.printBooleanPartialImage](#attr-listgridprintbooleanpartialimage)

**Flags**: IRWA

---
## Attr: ListGrid.headerButtonProperties

### Description
Properties to apply to all header buttons. Overrides defaults applied via [ListGrid.headerButtonDefaults](#attr-listgridheaderbuttondefaults).

### Groups

- gridHeader
- appearance

**Flags**: IRA

---
## Attr: ListGrid.aiFilterWindowHint

### Description
The inline hint-text displayed in the user-entry area in the [ListGrid.aiFilterWindow](#attr-listgridaifilterwindow).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.applyFormulaAfterSummary

### Description
If [ListGridField.userFormula](ListGridField.md#attr-listgridfielduserformula) is set for some field, and this grid is showing [group summaries](#attr-listgridshowgroupsummary) or a [grid summary](#attr-listgridshowgridsummary), this property determines what field value should be present in those summary rows. Should the field's user-formula be applied to the calculated summary row (applyFormulaAfterSummary `true`), or should a standard grid or group summary be applied to the user-formula values displayed in the grid (applyFormulaAfterSummary `false`)?

May be overridden at the field level via [ListGridField.applyAfterSummary](ListGridField.md#attr-listgridfieldapplyaftersummary)

**Flags**: IRW

---
## Attr: ListGrid.dataProperties

### Description
For databound ListGrids, this attribute can be used to customize the [ResultSet](ResultSet.md#class-resultset) object created for this grid when data is fetched

### Groups

- databinding

**Flags**: IRWA

---
## Attr: ListGrid.canMultiGroup

### Description
When true, indicates that this ListGrid supports grouping on multiple fields.

**Flags**: IRW

---
## Attr: ListGrid.invalidSummaryValue

### Description
Value to display to the user if showing summary values (through [ListGrid.showGridSummary](#attr-listgridshowgridsummary), [ListGrid.showGroupSummary](#attr-listgridshowgroupsummary) or [listGridFieldType:"summary"](../reference.md#type-listgridfieldtype)), and the summary function returns `"null"` (implying it was unable to calculate a valid summary value). This property will only be used in the default formatting behavior. If an explicit formatter has been specified - via [ListGrid.formatCellValue](ListGrid_2.md#method-listgridformatcellvalue) or [formatGridSummary()](ListGridField.md#attr-listgridfieldformatgridsummary), for example - this property has no effect.

**Flags**: IRWA

---
## Attr: ListGrid.checkboxFieldImageWidth

### Description
If [ListGrid.selectionAppearance](#attr-listgridselectionappearance) is set to `"checkbox"` this property may be set to govern the width of the checkbox image displayed to indicate whether a row is selected. If unset, the checkboxField image will be sized to match the [ListGrid.booleanImageWidth](#attr-listgridbooleanimagewidth) for this grid.

### Groups

- checkboxField

**Flags**: IR

---
## Attr: ListGrid.canEdit

### Description
Can the user edit cells in this listGrid? Can be set for the listGrid, and overridden for individual fields.  
If 'canEdit' is false at the listGrid level, fields can never be edited - in this case the canEdit property on individual fields will be ignored.  
If 'canEdit' is set to true at the listGrid level, setting the 'canEdit' property to false at the field level will prevent the field from being edited inline unless a custom override of [ListGrid.canEditCell](ListGrid_2.md#method-listgridcaneditcell) allows it.  
If 'canEdit' is not set at the listGrid level, setting 'canEdit' to true at the field level enables the field to be edited inline.

For more information on editing, see the [editing overview](../kb_topics/editing.md#kb-topic-grid-editing).

### Groups

- editing

### See Also

- [ListGrid.startEditing](ListGrid_2.md#method-listgridstartediting)
- [ListGridField.canEdit](ListGridField.md#attr-listgridfieldcanedit)
- [ListGrid.recordEditProperty](#attr-listgridrecordeditproperty)
- [ListGrid.canEditCell](ListGrid_2.md#method-listgridcaneditcell)
- [ListGrid.fields](#attr-listgridfields)

**Flags**: IRW

---
## Attr: ListGrid.groupTitleField

### Description
When a list grid is [grouped](ListGrid_2.md#method-listgridgroupby), each group shows under an auto generated header node. By default the title of the group will be shown, with a hanging indent in this node, and will span all columns in the grid. Setting this property causes the titles of auto-generated group nodes to appear as though they were values of the designated field instead of spanning all columns and record values in the designated groupTitleField will appear indented under the group title in a manner similar to how a TreeGrid shows a Tree.

Note if [ListGrid.showGroupSummaryInHeader](#attr-listgridshowgroupsummaryinheader) is true, the header nodes will not show a single spanning title value by default - instead they will show the summary values for each field. In this case, if groupTitleField is unset, a [groupTitleColumn](#attr-listgridshowgrouptitlecolumn) can be automatically generated to show the title for each group.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IR

---
## Attr: ListGrid.aiSortFieldMaxRecordsMessage

### Description
The message to show when a user asks the AI to sort more than the [maximum allowed records](DataBoundComponent.md#attr-databoundcomponentaisortfieldmaxrecords).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.groupSummaryRecordProperty

### Description
If [ListGrid.showGroupSummary](#attr-listgridshowgroupsummary) is true, this attribute will be set to true on each record object representing a group-level summary row.

**Flags**: IRW

---
## Attr: ListGrid.editSelectionType

### Description
If [ListGrid.selectOnEdit](#attr-listgridselectonedit) is true, what should be the edit-selection behavior be?

Default setting of `"single"` will cause the edit row to be automatically selected and any other selection in the grid to be dropped.  
If set to `"multiple"`, selection will be additive (as a record goes into edit mode, it is selected in addition to any pre-existant selection).

If set to `null` behavior is as follows:

*   For grids with [ListGrid.selectionType](#attr-listgridselectiontype) set to `"simple"` edit rows will be selected additively - this is the same behavior as if the `editSelectionType` was `"multiple"`
*   Otherwise edit rows will be selected singly - this is the same behavior as if the `editSelectionType` was `"single"`

**Flags**: IRW

---
## Attr: ListGrid.recordCanSelectProperty

### Description
If set to false on a record, selection of that record is disallowed.

**Flags**: IRA

---
## Attr: ListGrid.showRecordComponents

### Description
When enabled, [ListGrid.createRecordComponent](ListGrid_2.md#method-listgridcreaterecordcomponent) will be called when saved rows are being rendered, and any returned component will be displayed embedded within the row or cell.

recordComponents are not created for newly added rows which have not yet been saved. See the [Handling Unsaved Records overview](../kb_topics/unsavedRecords.md#kb-topic-handling-unsaved-records) for more information.

Depending on the [ListGrid.showRecordComponentsByCell](#attr-listgridshowrecordcomponentsbycell) setting, `createRecordComponent()` will be called either once per row, or once for every cell.

Depending on [ListGrid.recordComponentPosition](#attr-listgridrecordcomponentposition), components can either be placed underneath normal record or cell content ("expand" setting) or placed so that they overlap normal cell content ("within" setting). For the "within" setting, the default is to fill the row or cell, but the component can specify percent size or even use [snapTo-positioning](Canvas.md#attr-canvassnapto) to place itself within the row or cell.

The "expand" setting is incompatible with [frozen columns](#attr-listgridcanfreezefields) _unless_ all `recordComponents` are the same height and they are present in every row, in which case the fixed height of all `recordComponents` can be set via [ListGrid.recordComponentHeight](#attr-listgridrecordcomponentheight) to re-enable frozen fields.

Using `recordComponents` potentially means creating one component for every visible grid row or cell and so can impact performance. Before using this subsystem:

*   consider using [ListGridField.valueIcons](ListGridField.md#attr-listgridfieldvalueicons) (possibly with a specified [ListGridField.valueIconClick](ListGridField.md#method-listgridfieldvalueiconclick) handler) for icons based on field values which may be displayed alone in the cell or alongside standard content (see [ListGridField.showValueIconOnly](ListGridField.md#attr-listgridfieldshowvalueicononly));
*   for clickable icons representing actions that can be taken on a record, also consider using [a field of type "icon"](../reference.md#type-listgridfieldtype), or multiple such fields
*   for controls that only need to appear on rollover, consider [rollOver controls](#attr-listgridshowrollovercanvas)
*   if you are trying to customize the editor for a field, you can provide a custom control via [ListGridField.editorType](ListGridField.md#attr-listgridfieldeditortype), and [FormItem.icons](FormItem.md#attr-formitemicons) are a common way to add clickable buttons. You can also [provide different controls per record](ListGrid_2.md#method-listgridgeteditortype). These options are usually better that using `recordComponents` as custom editors, since you won't have to manage issues like making the `recordComponent` appear only when editing, having changes affect [editValues](../kb_topics/editing.md#kb-topic-grid-editing), triggering saves and handling validation errors, etc.

See [RecordComponentPoolingMode](../reference_2.md#type-recordcomponentpoolingmode) for an overview of how best to optimize use of `recordComponents` for different data sets.

Regardless of the pooling mode, you can explicitly refresh record components via [ListGrid.invalidateRecordComponents](ListGrid_2.md#method-listgridinvalidaterecordcomponents) and [ListGrid.refreshRecordComponent](ListGrid_2.md#method-listgridrefreshrecordcomponent).

_Interaction with [column auto-fit](#attr-listgridautofitfieldwidths)_: per-cell record components are not taken into account when determining the size for column auto fit. The default [ListGrid.getDefaultFieldWidth](ListGrid_2.md#method-listgridgetdefaultfieldwidth) implementation looks at cell content only. We typically recommend that, for fields showing record-components, [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth) and [ListGridField.canAutoFitWidth](ListGridField.md#attr-listgridfieldcanautofitwidth) be disabled, or if the record components are of a predictable size, a [ListGridField.defaultWidth](ListGridField.md#attr-listgridfielddefaultwidth) be specified.  
This is particularly pertinent where [ListGrid.recordComponentPosition](#attr-listgridrecordcomponentposition) is set to "within", in which case cells' content is often empty or completely covered by record-components.

### Groups

- recordComponents

### See Also

- [ListGrid.recordComponentPosition](#attr-listgridrecordcomponentposition)
- [ListGrid.showRecordComponentsByCell](#attr-listgridshowrecordcomponentsbycell)
- [RecordComponentPoolingMode](../reference_2.md#type-recordcomponentpoolingmode)
- [ListGrid.showRecordComponent](ListGrid_2.md#method-listgridshowrecordcomponent)
- [ListGrid.createRecordComponent](ListGrid_2.md#method-listgridcreaterecordcomponent)
- [ListGrid.updateRecordComponent](ListGrid_2.md#method-listgridupdaterecordcomponent)

**Flags**: IRW

---
## Attr: ListGrid.dateInputFormat

### Description
If this is an editable listGrid, this property will specify the [inputFormat](DateItem.md#attr-dateiteminputformat) applied to editors for fields of type `"date"`. May be overridden per field via [ListGridField.inputFormat](ListGridField.md#attr-listgridfieldinputformat).

### See Also

- [ListGrid.dateFormatter](#attr-listgriddateformatter)

**Flags**: IRWA

---
## Attr: ListGrid.showHeaderSpanContextMenu

### Description
Whether to show a context menu on the header span with standard items for showing and hiding fields. Not supported for [CubeGrid](CubeGrid.md#class-cubegrid).

### Groups

- gridHeader

### See Also

- [ListGrid.getHeaderSpanContextMenuItems](#method-listgridgetheaderspancontextmenuitems)

**Flags**: IR

---
## Attr: ListGrid.autoFitMaxRecords

### Description
If [ListGrid.autoFitData](#attr-listgridautofitdata) is set to `"vertical"` or `"both"` this property provides the maximum number of records for which the ListGrid will expand. If more records are present, scrolling will be introduced to reach them as normal. If unset, by default the ListGrid will expand to accommodate as many records as are present.

### Groups

- autoFitData

**Flags**: IRW

---
## Attr: ListGrid.criteriaIndicatorColor

### Description
The color of the [filterWindow criteria indicator](#attr-listgridshowfilterwindowcriteriaindicator).

**Flags**: IR

---
## Attr: ListGrid.exportRawValues

### Description
Dictates whether the data in this grid should be exported raw by [exportClientData()](ListGrid_2.md#method-listgridexportclientdata). If set to true, data will not be processed by field-formatters during exports. Decreases the time taken for large exports. This property can also be set at the [field level](ListGridField.md#attr-listgridfieldexportrawvalues).

**Flags**: IR

---
## Attr: ListGrid.drawAllMaxCells

### Description
If drawing all rows would cause less than `drawAllMaxCells` cells to be rendered, the full dataset will instead be drawn even if [showAllRecords](#attr-listgridshowallrecords) is false and the viewport size and [ListGrid.drawAheadRatio](#attr-listgriddrawaheadratio) setting would normally have caused incremental rendering to be used.

The `drawAllMaxCells` setting prevents incremental rendering from being used in situations where it's really unnecessary, such as a 40 row, 5 column dataset (only 200 cells) which happens to be in a grid with a viewport showing only 20 or so rows. Incremental rendering causes a brief "flash" during scrolling as the visible portion of the dataset is redrawn, and a better scrolling experience can be obtained in this situation by drawing the entire dataset up front, which in this example would have negligible effect on initial draw time.

`drawAllMaxCells:0` disables this features. You may want to disable this feature if performance is an issue and:

*   you are very frequently redraw a grid
*   you do a lot of computation when rendering each cell (eg formulas)
*   you are showing many grids on one screen and the user won't scroll most of them

### Groups

- performance

**Flags**: IRWA

---
## Attr: ListGrid.recordCustomStyleProperty

### Description
Denotes the name of a property that can be set on records to display a custom style. For example if this property is set to `"customStyle"`, setting `record.customStyle` to a css styleName will cause the record in question to render out with that styling applied to it. Note that this will be a static style - it will not be modified as the state of the record (selected / over etc) changes.

### See Also

- [ListGrid.getCellStyle](ListGrid_2.md#method-listgridgetcellstyle)
- [ListGrid.recordBaseStyleProperty](#attr-listgridrecordbasestyleproperty)

**Flags**: IRW

---
## Attr: ListGrid.fastCellUpdates

### Description
**Note: This property only has an effect in Internet Explorer**

Advanced property to improve performance for dynamic styling of gridRenderer cells in Internet Explorer, at the expense of slightly slower initial drawing, and some limitations on supported styling options.

`fastCellUpdates` speeds up the dynamic styling system used by rollovers, selections, and custom styling that calls [GridRenderer.refreshCellStyle](GridRenderer.md#method-gridrendererrefreshcellstyle), at the cost of slightly slower draw() and redraw() times.

Notes:

*   When this property is set, ListGrid cells may be styled using the [ListGrid.tallBaseStyle](#attr-listgridtallbasestyle). See [ListGrid.getBaseStyle](ListGrid_2.md#method-listgridgetbasestyle) for more information.
*   If any cell styles specify a a background image URL, the URL will be resolved relative to the page location rather than the location of the CSS stylesheet. This means cell styles with a background URL should either supply a fully qualified path, or the background image media should be made available at a second location for IE.
*   fastCellUpdates will not work if the styles involved are in an external stylesheet loaded from a remote host. Either the stylesheet containing cell styles needs to be loaded from the same host as the main page, or the cell styles need to be inlined in the html of the bootstrap page.
*   fastCellUpdates will not work if the css styles for cells are defined in a `.css` file loaded via `@import`. Instead the `.css` file should be loaded via a ``<link ...>`` tag.

### Groups

- performance

**Flags**: I

---
## Attr: ListGrid.useAdvancedCriteria

### Description
Should the [filter-editor](#attr-listgridshowfiltereditor) in this grid always produce [AdvancedCriteria](../reference.md#object-advancedcriteria)?

### Groups

- criteriaEditing

**Flags**: IRW

---
## Attr: ListGrid.showExpansionEditorSaveButton

### Description
When [ExpansionMode](../reference_2.md#type-expansionmode) is _editor_, should a Save button be shown below the the expanded editor?

Note that if an expanded-row containing an editor is collapsed while changes are outstanding, changes will be either be automatically updated to the grid, or will first show a confirmation dialog, according to the value of [ListGrid.expansionEditorShowSaveDialog](#attr-listgridexpansioneditorshowsavedialog).

### Groups

- expansionField

**Flags**: RW

---
## Attr: ListGrid.confirmDiscardEditsMessage

### Description
If `this.confirmDiscardEdits` is true, this property can be used to customize the error message string displayed to the user in a dialog with options to cancel the action, or save or discard pending edits in response to sort/filter actions that would otherwise drop unsaved edit values.

### Groups

- editing
- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.groupTitleColumnDefaults

### Description
Default properties for the automatically generated `groupTitleColumn`. Default object includes properties to enable autoFitWidth to group title values.

To modify the behavior or appearance of this column, developers may set [ListGrid.groupTitleColumnProperties](#attr-listgridgrouptitlecolumnproperties) at the instance level, or override this object at the class level. If overriding this object, we recommend using [Class.changeDefaults](Class.md#classmethod-classchangedefaults) rather than replacing this object entirely.

See [ListGrid.showGroupTitleColumn](#attr-listgridshowgrouptitlecolumn) for an overview of the groupTitleColumn.

**Flags**: IR

---
## Attr: ListGrid.dataArity

### Description
A ListGrid is a [dataArity](DataBoundComponent.md#attr-databoundcomponentdataarity):multiple component.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: ListGrid.canFreezeFields

### Description
Whether an interface should be shown to allow user is allowed to dynamically "freeze" or "unfreeze" columns with respect to horizontally scrolling. If unset, this property defaults to `true` unless:

*   [this.fixedRecordHeights](#attr-listgridfixedrecordheights) is `false`
*   [this.bodyOverflow](#attr-listgridbodyoverflow) is `"visible"`
*   [this.autoFitData](#attr-listgridautofitdata) is set to `"horizontal"` or `"both"`
*   Any field has overflow set to `"visible"`

Note that the `canFreezeFields` setting enables or disables the user interface for freezing and unfreezing fields only. Fields can be programmatically frozen via setting [field.frozen](ListGridField.md#attr-listgridfieldfrozen) to true when the grid is created, or dynamically frozen and unfrozen via [ListGrid.freezeField](ListGrid_2.md#method-listgridfreezefield) and [ListGrid.unfreezeField](ListGrid_2.md#method-listgridunfreezefield).

Developers should also be aware that if the cell content for some field exceeds the specified [ListGrid.cellHeight](#attr-listgridcellheight), and [ListGrid.enforceVClipping](#attr-listgridenforcevclipping) is not set to true, this can cause misalignment between rows in frozen and unfrozen columns. See the [Frozen fields overview](../kb_topics/frozenFields.md#kb-topic-frozen-fields) for more on this.

### Groups

- frozenFields

**Flags**: IRW

---
## Attr: ListGrid.booleanTrueImage

### Description
Image to display for a true value in a boolean field. The special value "blank" means that no image will be shown.

To turn this off explicitly set [ListGridField.suppressValueIcon](ListGridField.md#attr-listgridfieldsuppressvalueicon) to true.

If this, [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage) and [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage) are unset, this will be set to the default [CheckboxItem.checkedImage](CheckboxItem.md#attr-checkboxitemcheckedimage).

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string. Alternatively developers can omit this property and instead use CSS directly in the [ListGrid.booleanBaseStyle](#attr-listgridbooleanbasestyle) property to provide a "boolean true" appearance.

### Groups

- imageColumns

### See Also

- [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage)
- [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage)
- [ListGrid.printBooleanTrueImage](#attr-listgridprintbooleantrueimage)

**Flags**: IRWA

---
## Attr: ListGrid.reselectOnUpdate

### Description
If true, when an update operation occurs on a selected record in a [databound](#attr-listgriddatasource) listGrid, ensure the updated record is re-selected when the operation completes. The [ListGrid.reselectOnUpdateNotifications](#attr-listgridreselectonupdatenotifications) attributes governs whether [ListGrid.selectionUpdated](ListGrid_2.md#method-listgridselectionupdated) and [ListGrid.selectionChanged](ListGrid_2.md#method-listgridselectionchanged) will fire when this occurs.

**Flags**: IRA

---
## Attr: ListGrid.editFailedBaseStyle

### Description
A base name for the CSS class applied to cells when editing has failed.  
If this listGrid is editable, this style will be applied to any edited cells for which validation failed.  
As with the default 'baseStyle' property, this style will have "Dark", "Over", "Selected", or "Disabled" appended to it according to the state of the cell.  
If null, cells for which editing has failed will be rendered using the normal base style classNames, but with custom CSSText applied as derived from `this.editFailedCSSText`

### Groups

- appearance

### See Also

- [ListGrid.baseStyle](#attr-listgridbasestyle)
- [ListGrid.editFailedCSSText](#attr-listgrideditfailedcsstext)

**Flags**: IRWA

---
## Attr: ListGrid.autoFitMaxHeight

### Description
If [ListGrid.autoFitData](#attr-listgridautofitdata) is set to `"vertical"` or `"both"` this property provides an upper limit on how far the ListGrid will expand vertically to accommodate its content. If content exceeds this height, scrollbars will be introduced as usual. In addition to this property, [ListGrid.autoFitMaxRecords](#attr-listgridautofitmaxrecords) allows you to limit vertical expansion based on the number of rows to be rendered.

Note: Unlike [ListGrid.autoFitMaxWidth](#attr-listgridautofitmaxwidth), this property cannot be set to a string percentage value; it must be a numeric pixel value or `null`.

### Groups

- autoFitData

**Flags**: IRW

---
## Attr: ListGrid.hilites

### Description
Hilites to be applied to the data for this grid. See [hiliting](../kb_topics/hiliting.md#kb-topic-hiliting).

It is undefined behavior to share the same record objects, or the same [ResultSet](ResultSet.md#class-resultset) instances, among multiple grids if one of the grid's fields specifies a [userFormula](ListGridField.md#attr-listgridfielduserformula), [userSummary](ListGridField.md#attr-listgridfieldusersummary), [aiFieldPrompt](ListGridField.md#attr-listgridfieldaifieldprompt), or [aiHoverRequest](ListGridField.md#attr-listgridfieldaihoverrequest), or if one of the grids has a [Hilite](../reference.md#object-hilite) with an asynchronous filter in the hilite's [criteria](Hilite.md#attr-hilitecriteria).

### Groups

- hiliting

**Flags**: IRW

---
## Attr: ListGrid.errorIconWidth

### Description
Height of the error icon, if we're showing icons when validation errors occur.

### Groups

- errorIcon

**Flags**: IRW

---
## Attr: ListGrid.filterWindowFilter

### Description
Instance of [FilterBuilder](FilterBuilder.md#class-filterbuilder) shown in [ListGrid.filterWindow](#attr-listgridfilterwindow) by [ListGrid.showFilterWindow](#method-listgridshowfilterwindow). See [ListGrid.filterWindow](#attr-listgridfilterwindow) for more information on the filter defaults and changing them.

**Flags**: IR

---
## Attr: ListGrid.useCopyPasteShortcuts

### Description
For ListGrids with [canSelectCells:true](#attr-listgridcanselectcells), enabling this property will cause the listGrid to intercept standard browser copy/paste shortcut keys and perform the following behavior.

*   _ctrl+c_: retrieve selected cell data via a call to [ListGrid.getSelectedCellData](ListGrid_2.md#method-listgridgetselectedcelldata), and temporarily store it in memory in a "clipboard" variable.
*   _ctrl+v_: apply any previously copied data stored in the "clipboard" variable into the current grid selection via [ListGrid.applyCellData](ListGrid_2.md#method-listgridapplycelldata).
*   _ctrl+d_: copy cell values from top row of selected cells down to all rows
*   _ctrl+r_: copy cell values from left column of selected cells right to all columns

**Note:** setting this property to true will disable standard copy and paste behavior to the native Browser or OS-level clipboard. To copy data to and from applications outside of the browser, use the technique shown in the *Grid to Excel* and *Excel to Grid* samples.

If this property is unset, default behavior will enable these shortcuts if [ListGrid.canSelectCells](#attr-listgridcanselectcells) is true, and [ListGrid.canDragSelectText](#attr-listgridcandragselecttext) and [ListGrid.selectCellTextOnClick](#attr-listgridselectcelltextonclick) are both false, so as to minimize the chances of interfering with native copy and paste of cell content.

**Flags**: IRW

---
## Attr: ListGrid.autoFitWidthApproach

### Description
When a user requests column autofitting via the [header context menu](ListGrid_2.md#method-listgridgetheadercontextmenuitems) or via a [mouse gesture](#attr-listgridheaderautofitevent), what autofit approach is used.

For information about auto-fitting specific fields, see [ListGridField.autoFit](ListGridField.md#attr-listgridfieldautofit).

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.cellRole

### Description
Returns the default WAI ARIA role for cells within this listGrid. See [ListGrid.getCellRole](ListGrid_2.md#method-listgridgetcellrole)

**Flags**: IRWA

---
## Attr: ListGrid.selectionCanvas

### Description
AutoChild created and embedded in the grid if [showSelectionCanvas](#attr-listgridshowselectioncanvas) is `true` and the [selectionType](#attr-listgridselectiontype) is "single". This component will be created and displayed above the selected record whenever the selection changes.

NOTE: It is recommended to use the [selectionUnderCanvas](#attr-listgridselectionundercanvas) rather than the `selectionCanvas` if possible because the `selectionCanvas` is stacked on top of the selected record and this may interfere with event handling in rare cases. If no interactive components are shown in the `selectionCanvas` and it simply provides custom styling, then the `selectionUnderCanvas` should be used instead.

The `selectionCanvas` has the following read-only attributes set:  
\- `this.grid` - a pointer to the grid  
\- `this.record` - a pointer to the currently selected record in the grid

### Groups

- rowEffects

### See Also

- [ListGrid.selectionUnderCanvas](#attr-listgridselectionundercanvas)

**Flags**: RA

---
## Attr: ListGrid.canShowFilterEditor

### Description
Should a menu item allowing the user to show or hide the [filter editor](#attr-listgridshowfiltereditor) be displayed in the [headerContextmenu](#attr-listgridheadercontextmenu)?

Note that if this ListGrid is not [bound to a dataSource](#attr-listgriddatasource) it can not be filtered. In this case the context menu option to show the filterEditor will not be displayed even if `canShowFilterEditor` is true.

Enabling [filter via AI](#attr-listgridfilterviaaimode) forces this setting to true.

### Groups

- filterEditor

### See Also

- [ListGrid.showFilterEditorTitle](#attr-listgridshowfiltereditortitle)
- [ListGrid.hideFilterEditorTitle](#attr-listgridhidefiltereditortitle)

**Flags**: IRW

---
## Attr: ListGrid.canSaveSearches

### Description
When enabled (the default), causes a "Saved views >" submenu to appear in the header context menu, last, allowing the user to create new saved searches, select previously saved searches, and edit or copy existing searches.

Note that disabling this feature does not mean that saved searches are disallowed - you can stil implement a separate UI via a [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) that targets this component. But, when disabled, the grid-integrated menu described above will not be shown.

This feature uses the global settings found in [SavedSearches](SavedSearches.md#class-savedsearches). Some aspects can be overridden for this component. See [ListGrid.savedSearchDS](#attr-listgridsavedsearchds), [ListGrid.savedSearchAdminRole](#attr-listgridsavedsearchadminrole).

To avoid leaking local storage, this setting will be disregarded, disabling the feature, unless the grid specifies [savedSearchId](DataBoundComponent.md#attr-databoundcomponentsavedsearchid), or an explicit [local or global ID](Canvas.md#method-canvasgetlocalid) is present.

**Note:** this feature requires [SmartClient Pro](https://www.smartclient.com/product/) or better.

**Flags**: IR

---
## Attr: ListGrid.summaryRowDataSource

### Description
If [ListGrid.showGridSummary](#attr-listgridshowgridsummary) is true, by default summary values are calculated on the client based on the current data-set for the grid (see [ListGrid.getGridSummary](ListGrid_2.md#method-listgridgetgridsummary) and [ListGrid.getGridSummaryFunction](ListGrid_2.md#method-listgridgetgridsummaryfunction)).

In some cases however it may make sense to calculate summary values on the server and retrieve them via a dataSource fetch. If set, this property specifies a dataSource to fetch against for the summary row.

The fetch may be further customized via [ListGrid.summaryRowCriteria](#attr-listgridsummaryrowcriteria) and [ListGrid.summaryRowFetchRequestProperties](#attr-listgridsummaryrowfetchrequestproperties). Note that if [ListGrid.maxSummaryRowRecords](#attr-listgridmaxsummaryrowrecords) is specified this will be passed to the server as the [DSRequest.endRow](DSRequest.md#attr-dsrequestendrow) for the summaryRowFetchRequest. Developers may modify this property in order to display multiple summaryRowRecords from a summaryRowDataSource fetch

Note that specifying a `summaryRowDataSource` completely bypasses the standard client-side grid summary calculation logic.

**Flags**: IRA

---
## Attr: ListGrid.firstCellStyle

### Description
The style to apply to the first cell in each row, when [ListGrid.styledRowEnds](#attr-listgridstyledrowends) is true. Note that this style is additional to the regular cell styling and should not introduce settings that change the layout or size of the cell, such as padding or font-size. The styling will work with any design, and is also applied correctly with or without frozen fields.

If all you want to do is provide rounded-corners for records in this grid, it may be simpler to set [ListGrid.recordRadius](#attr-listgridrecordradius) to a CSS _border-radius_ string that achieves the rounding you want.

**Flags**: IRW

---
## Attr: ListGrid.exportFieldWidths

### Description
When exporting data to Excel/OpenOffice format using [ListGrid.exportData](ListGrid_2.md#method-listgridexportdata) or [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata), whether widths of fields should be replicated in the resulting spreadsheet.

Because Excel's unit of measurement for field widths is based on the default system font, there is no exact way to translate field widths in pixels to Excel column widths. The [ListGrid.exportWidthScale](#attr-listgridexportwidthscale) property can be set to adjust scaling; it's default value errs on the side of making Excel's columns slightly wider than the ListGrid field's actual width to avoid clipping.

Note that you can switch off width export for individual fields with the [ListGridField.exportFieldWidth](ListGridField.md#attr-listgridfieldexportfieldwidth) flag.

### See Also

- [ListGrid.exportHiddenFieldWidth](#attr-listgridexporthiddenfieldwidth)

**Flags**: IRW

---
## Attr: ListGrid.headerMenuButtonIconWidth

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, this property governs the width of the icon shown on the auto-generated `headerMenuButton`

### Groups

- headerMenuButton

**Flags**: IRA

---
## Attr: ListGrid.baseStyle

### Description
[base cell style](GridRenderer.md#attr-gridrendererbasestyle) for this listGrid. If this property is unset, base style may be derived from [ListGrid.normalBaseStyle](#attr-listgridnormalbasestyle) or [ListGrid.tallBaseStyle](#attr-listgridtallbasestyle) as described in [ListGrid.getBaseStyle](ListGrid_2.md#method-listgridgetbasestyle).

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### Groups

- appearance

**Flags**: IR

---
## Attr: ListGrid.dragTrackerStyle

### Description
CSS Style to apply to the drag tracker when dragging occurs on this component.

**Flags**: IRW

---
## Attr: ListGrid.showFilterEditorTitle

### Description
When [canShowFilterEditor](#attr-listgridcanshowfiltereditor) is true, this is the title for the filterEditor show/hide menu-item, in the [headerContextmenu](#attr-listgridheadercontextmenu), when the filterEditor is hidden.

[hideFilterEditorTitle](#attr-listgridhidefiltereditortitle) affects the same menu-item when the filterEditor is visible.

### Groups

- filterEditor
- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.expansionFieldImageStyle

### Description
Custom style to apply to the image in the [ListGrid.expansionField](#attr-listgridexpansionfield) displayed in collapsible rows when [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) is true. Affects the icons provided by [ListGrid.expansionFieldTrueImage](#attr-listgridexpansionfieldtrueimage) and [ListGrid.expansionFieldFalseImage](#attr-listgridexpansionfieldfalseimage).

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.expansionDetailField

### Description
Automatically generated [HTMLFlow](HTMLFlow.md#class-htmlflow) for displaying the contents of [a specified field](#attr-listgriddetailfield) in a record's expanded section when [listGrid.expansionMode](../reference_2.md#type-expansionmode) is `detailField`.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `listGrid.expansionDetailFieldProperties` and `listGrid.expansionDetailFieldDefaults`.

Note, however, that this is a multi-instance component (potentially one per record), so it is created using [createAutoChild()](Class.md#method-classcreateautochild) not [addAutoChild()](Class.md#method-classaddautochild), and no default single instance is created by name on the grid.

### Groups

- expansionField

**Flags**: RA

---
## Attr: ListGrid.confirmCancelEditing

### Description
If this is an editable listGrid, when the user attempts to cancel an edit, should we display a confirmation prompt before discarding the edited values for the record?

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.hiliteIconPosition

### Description
When [hiliteIcons](#attr-listgridhiliteicons) are present, where the hilite icon will be placed relative to the field value. See [HiliteIconPosition](../reference.md#type-hiliteiconposition). Can be overridden at the field level.

### Groups

- hiliting

**Flags**: IR

---
## Attr: ListGrid.sortEditorSpanTitleSeparator

### Description
If this grid has specified [headerSpans](#attr-listgridheaderspans), and [showHeaderSpanTitlesInSortEditor](#attr-listgridshowheaderspantitlesinsorteditor) is true, this string will be inserted between the headerSpan title(s) and the field title in the field chooser grid on the [multi-sort editor](MultiSortDialog.md#class-multisortdialog)

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.sorterDefaults

### Description
Defaults to apply to the corner sort button. To modify this object, use [ListGrid.changeDefaults()](Class.md#classmethod-classchangedefaults) rather than replacing with an entirely new object.

### Groups

- gridHeader
- appearance

**Flags**: IRA

---
## Attr: ListGrid.drawAheadRatio

### Description
How far should we render records ahead of the currently visible area? This is expressed as a ratio from viewport size to rendered area size.

Tweaking drawAheadRatio allows you to make tradeoffs between continuous scrolling speed vs initial render time and render time when scrolling by large amounts.

NOTE: Only applies when showAllRecords is false.

### Groups

- performance

**Flags**: IRW

---
## Attr: ListGrid.headerSpan

### Description
[headerSpans](#attr-listgridheaderspans) are created via the [AutoChild](../reference.md#type-autochild) pattern, hence `headerSpanConstructor`, `headerSpanDefaults` and `headerSpanProperties` are valid.

### Groups

- headerSpan

**Flags**: IR

---
## Attr: ListGrid.useClientFiltering

### Description
Causes this grid to filter its data on the client where possible, eliminating trips to the server when criteria becomes more restrictive, since the filter must apply to data which is already on the client.

This attribute is a shortcut to setting `useClientFiltering` on the grid's [ListGrid.dataProperties](#attr-listgriddataproperties) and overrides any value set there.

While the default value is null, the effective default is true, since `useClientFiltering` is true on [ResultSet](ResultSet.md#attr-resultsetuseclientfiltering).

Note that using client-filtering can avoid up to 90% of the most expensive database requests, so it's critical in most cases to leave it switched on. See the sample [here](https://smartclient.com/smartclient-latest/showcase/?id=adaptiveFilterFS).

In cases where client-filtering alone is not sufficient, note the following:

*   You can easily prevent client-side filtering for a given field by setting [filterOn:"serverOnly"](DataSourceField.md#attr-datasourcefieldfilteron), if you can't replicate the filtering on the client.
*   an override of [ResultSet.compareCriteria](ResultSet.md#method-resultsetcomparecriteria) can be used to handle any other, more complicated differences in client- vs server-side filtering that may arise for a single grid
*   a custom search operator can be used if you want to create custom filtering behavior which applies to a variety of different grids & DataSources

**Flags**: IRW

---
## Attr: ListGrid.hiliteIconLeftPadding

### Description
How much padding should there be on the left of [hilite icons](#attr-listgridhiliteicons) by default? Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: ListGrid.canRemoveRecords

### Description
If set, provide UI for the user to remove records from the grid as an additional field showing the [ListGrid.removeIcon](#attr-listgridremoveicon), which, when clicked, will call [ListGrid.removeRecordClick](ListGrid_2.md#method-listgridremoverecordclick) which removes the row from the data set (or if [ListGrid.deferRemoval](#attr-listgriddeferremoval) is true changes the [ListGrid.markRecordRemoved](ListGrid_2.md#method-listgridmarkrecordremoved) status for the record). Individual records can be marked to prevent removal - see [ListGrid.recordCanRemoveProperty](#attr-listgridrecordcanremoveproperty).

To add a confirmation dialog before a record is removed, set [ListGrid.warnOnRemoval](#attr-listgridwarnonremoval).

If deferring removal, the record will appear marked with the [ListGrid.removedCSSText](#attr-listgridremovedcsstext) until the removal is committed via a call to [ListGrid.saveEdits](ListGrid_2.md#method-listgridsaveedits). Otherwise, the record will disappear from view. If [ListGrid.animateRemoveRecord](#attr-listgridanimateremoverecord) is true, the removed record will appear to shrink out of view when it is removed.

By default the field will display the [ListGrid.removeIcon](#attr-listgridremoveicon) next to each record, and will be rendered as the rightmost column. Two mechanisms exist to further modify this field:

*   To change the position of the remove-field, include an explicitly specified field with the attribute [isRemoveField:true](ListGridField.md#attr-listgridfieldisremovefield) set. This will then be used as the remove field instead of adding a field to the beginning of the set of columns.
*   Additional direct configuration of the remove field may be achieved by modifying [ListGrid.removeFieldProperties](#attr-listgridremovefieldproperties).

If [ListGrid.deferRemoval](#attr-listgriddeferremoval) is true, when a record is marked as removed, the the icon will change to display the [ListGrid.unremoveIcon](#attr-listgridunremoveicon) for this row. Clicking on this icon will call [ListGrid.unmarkRecordRemoved](ListGrid_2.md#method-listgridunmarkrecordremoved) to mark the record as no longer pending deletion.

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.rowLocatorField

### Description
If [ListGrid.locateRowsBy](#attr-listgridlocaterowsby) has been set to "cellValue", this property may be used to specify which field's cell value to use.

If set to an array, cell values from each field will be recorded as part of the locator and used to identify the record.

### Groups

- autoTest

### See Also

- [LocatorStrategy](../reference_2.md#type-locatorstrategy)

**Flags**: IRW

---
## Attr: ListGrid.checkboxFieldPartialImage

### Description
If [ListGrid.selectionAppearance](#attr-listgridselectionappearance) is set to `"checkbox"` this property determines the image to display in the checkbox field for a partially selected row. If unset, the [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage) will be used. Note that the special value "blank" means that no image will be shown.

### Groups

- checkboxField
- printing

### See Also

- [ListGrid.checkboxFieldTrueImage](#attr-listgridcheckboxfieldtrueimage)
- [ListGrid.checkboxFieldImageWidth](#attr-listgridcheckboxfieldimagewidth)
- [ListGrid.checkboxFieldImageHeight](#attr-listgridcheckboxfieldimageheight)
- [ListGrid.printCheckboxFieldPartialImage](#attr-listgridprintcheckboxfieldpartialimage)

**Flags**: IRWA

---
## Attr: ListGrid.spanContextMenu

### Description
The menu displayed when a cell is right clicked on.

### Groups

- gridHeader

**Flags**: R

---
## Attr: ListGrid.ariaRole

### Description
ARIA role for this ListGrid if [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode) is enabled.

The [WAI-Aria standards](https://www.w3.org/WAI/standards-guidelines/aria/) contain a number of roles and related attributes that could apply to data presented in a ListGrid or its subclasses. In order to make screenreader support as straightforward as possible we have built-in support for writing out appropriate aria roles and attributes on the listGrid and its component elements for a couple of standard modes, as well as providing override points allowing developers to explicitly specify the properties that get written out.

The two "standard" ariaRoles supported for ListGrids are ["grid"](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/Grid_Role) and ["list"](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/Roles/List_role).

When _ariaRole_ is set to `"list"` we write out the following standard properties by default:

*   rows have role set to `"listitem"`
*   [ListGrid.getRowAriaState](ListGrid_2.md#method-listgridgetrowariastate) will return aria properties for `setsize`, `posinset`, `selected` (for selected rows) and `expanded` (for [expanded](#attr-listgridcanexpandrecords) rows)
*   Additionally, if [ListGrid.screenReaderWriteRowLabelledBy](#attr-listgridscreenreaderwriterowlabelledby) is true, rows will write out an `aria-labelldby` that will cause ScreenReaders to read the column header and cell / row separators in addition to the cell content for the row

When _ariaRole_ is set to `"grid"` we write out the following standard properties by default:

*   `aria-rowcount` and `aria-colcount` will be specified on the listGrid itself
*   The [header](#attr-listgridheader) will have role `row` and `aria-rowindex` set to 1
*   Column header buttons will have role `columnheader`, and `aria-colindex` set to the appropriate value for the column. Additionally `aria-sort` will be specified to reflect the current sort-state for the field, and if the header menu is enabled, `aria-haspopup` will be `true`
*   Rows within the grid body will have role `row`
*   [ListGrid.getRowAriaState](ListGrid_2.md#method-listgridgetrowariastate) will return aria properties for `rowindex`, `selected` (for selected rows) and `expanded` (for [expanded](#attr-listgridcanexpandrecords) rows)
*   Cells within rows will have role `gridcell`

Developers may configure different ARIA HTML roles and attributes by modifying this attribute (`listGrid.ariaRole`) and implementing custom handling for the following APIs:

| ListGrid | listGrid.ariaRole, [ariaState](Canvas.md#attr-canvasariastate), [ListGrid.getAriaState](ListGrid_2.md#method-listgridgetariastate). |
|---|---|
| header / header buttons | [ListGrid.headerAriaRole](#attr-listgridheaderariarole), [ListGrid.headerButtonAriaRole](#attr-listgridheaderbuttonariarole), [ListGridField.headerButtonAriaRole](ListGridField.md#attr-listgridfieldheaderbuttonariarole) [ListGrid.headerButtonAriaState](#attr-listgridheaderbuttonariastate), [ListGridField.headerButtonAriaState](ListGridField.md#attr-listgridfieldheaderbuttonariastate) |
| rows | [ListGrid.rowRole](#attr-listgridrowrole), [ListGrid.recordRowRoleProperty](#attr-listgridrecordrowroleproperty), [ListGrid.rowAriaState](#attr-listgridrowariastate), [ListGrid.recordRowAriaStateProperty](#attr-listgridrecordrowariastateproperty) , [ListGrid.getRowRole](ListGrid_2.md#method-listgridgetrowrole), [ListGrid.getRowAriaState](ListGrid_2.md#method-listgridgetrowariastate). To update row state at runtime, developers may redraw the grid or its body. |
| cells | [ListGrid.cellRole](#attr-listgridcellrole), [ListGrid.recordCellRoleProperty](#attr-listgridrecordcellroleproperty) , [ListGrid.getCellRole](ListGrid_2.md#method-listgridgetcellrole), [ListGrid.getCellAriaState](ListGrid_2.md#method-listgridgetcellariastate). To update cell state at runtime, developers may redraw the grid or its body. |

### Groups

- accessibility

**Flags**: IRWA

---
## Attr: ListGrid.deferRemoval

### Description
When enabled, the field shown by [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) causes records to be marked for future removal via [ListGrid.markRecordRemoved](ListGrid_2.md#method-listgridmarkrecordremoved) instead of immediately being removed.

When a record has been marked for removal, an icon in the `canRemoveRecords` field allowing it to be unmarked will be displayed.

If not explicitly specified by this property, removal of records will be deferred if [ListGrid.autoSaveEdits](#attr-listgridautosaveedits) is false for the grid.

### Groups

- editing

**Flags**: IR

---
## Attr: ListGrid.showSelectedStyle

### Description
Should the "Selected" style be applied to selected records?

### See Also

- [GridRenderer.getCellStyle](GridRenderer.md#method-gridrenderergetcellstyle)

**Flags**: IRW

---
## Attr: ListGrid.backgroundComponent

### Description
Has no effect unless [ListGrid.showBackgroundComponents](#attr-listgridshowbackgroundcomponents) is `true`.

Canvas created and embedded in the body behind a given record. When [ListGridRecord.backgroundComponent](ListGridRecord.md#attr-listgridrecordbackgroundcomponent) is set, this autoChild canvas will be constructed (if listGridRecord.backgroundComponent is not already a Canvas) and its properties combined with those of listGridRecord.backgroundComponent and then displayed behind a specific record in the page's z-order, meaning it will only be visible if the cell styling is transparent.

### Groups

- rowEffects

**Flags**: IR

---
## Attr: ListGrid.canSort

### Description
Enables or disables interactive sorting behavior for this listGrid. Does not affect sorting by direct calls to the [sort](ListGrid_2.md#method-listgridsort) or [setSort](ListGrid_2.md#method-listgridsetsort) methods.

### Groups

- sorting

**Flags**: IRW

---
## Attr: ListGrid.rowNumberStyle

### Description
The CSS Style name for the [ListGrid.rowNumberField](#attr-listgridrownumberfield).

### Groups

- rowNumberField

**Flags**: IRWA

---
## Attr: ListGrid.canDropInEmptyArea

### Description
If set to false, dropping over an empty part of the grid body is disallowed and the no-drop indicator is displayed.

### Groups

- dragdrop

**Flags**: IRW

---
## Attr: ListGrid.valueIconHeight

### Description
Height for value icons for this listGrid. Overrides [ListGrid.valueIconSize](#attr-listgridvalueiconsize). Can be overridden at the field level

### Groups

- imageColumns

**Flags**: IRW

---
## Attr: ListGrid.body

### Description
GridRenderer used to render the dataset.

Note that this is a multi-instance component when there are frozen fields because in addition to the primary body AutoChild, a "frozen body" AutoChild is created to render the frozen portion of the dataset.

### See Also

- [ListGrid.getBody](ListGrid_2.md#method-listgridgetbody)

**Flags**: R

---
## Attr: ListGrid.errorIconHeight

### Description
Height of the error icon, if we're showing icons when validation errors occur.

### Groups

- errorIcon

**Flags**: IRW

---
## Attr: ListGrid.showGroupTitleInFrozenBody

### Description
If this is [grouped](ListGrid_2.md#method-listgridgroupby) and has [frozen fields](../kb_topics/frozenFields.md#kb-topic-frozen-fields), should the group title show in the frozen or unfrozen body?

Setting this property to false will cause the group title to show in the unfrozen body in this case, meaning it will appear to the right of the frozen fields, and scroll horizontally as the user scrolls the unfrozen fields. This can be useful for grids where there isn't enough available space to show the group title text in the frozen body.

Note that if [ListGrid.groupTitleField](#attr-listgridgrouptitlefield) is explicitly set, or [ListGrid.showGroupSummaryInHeader](#attr-listgridshowgroupsummaryinheader) is true, this property has no effect. In this case rather than the group title showing in a single cell spanning multiple other fields, it will be rendered into a specific column.

**Flags**: IRWA

---
## Attr: ListGrid.headerTitleStyle

### Description
[StretchImgButton.titleStyle](StretchImgButton.md#attr-stretchimgbuttontitlestyle) to apply to the buttons in the header, and the sorter, for this ListGrid. Note that this will typically only have an effect if [ListGrid.headerButtonConstructor](#attr-listgridheaderbuttonconstructor) is set to [StretchImgButton](StretchImgButton.md#class-stretchimgbutton) or a subclass thereof.

### Groups

- gridHeader
- appearance

**Flags**: IR

---
## Attr: ListGrid.formulaBuilderSpanTitleSeparator

### Description
If this grid has specified [headerSpans](#attr-listgridheaderspans), and [showHeaderSpanTitlesInFormulaBuilder](#attr-listgridshowheaderspantitlesinformulabuilder) is true, this string will be inserted between the headerSpan title(s) and the field title in the field chooser grid in the [FormulaBuilder](FormulaBuilder.md#class-formulabuilder) and [SummaryBuilder](SummaryBuilder.md#class-summarybuilder).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.booleanImageHeight

### Description
Height for the [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage), [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage) and [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage). Note: If [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage) is unset, the [CheckboxItem.checkedImage](CheckboxItem.md#attr-checkboxitemcheckedimage) will be used to indicate a true value in a boolean field. In this case this property is ignored in favor of [CheckboxItem.valueIconHeight](CheckboxItem.md#attr-checkboxitemvalueiconheight).

### Groups

- imageColumns

**Flags**: IRWA

---
## Attr: ListGrid.generateClickOnEnter

### Description
If true, when the user navigates to a cell using arrow keys and hits Enter, the cell will respond to a click event.

**Flags**: IRWA

---
## Attr: ListGrid.isGrouped

### Description
True if this listGrid is grouped, false otherwise

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: R

---
## Attr: ListGrid.cellPadding

### Description
The amount of empty space, in pixels, surrounding each value in its cell.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: ListGrid.freezeFieldText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid and [this.canFreezeFields](#attr-listgridcanfreezefields) is true, this string will be shown as the title for the menu item to freeze a currently unfrozen field.

This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `title` available as a variable containing the field title.

Default value returns "Freeze " + the field's summary title.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: ListGrid.shrinkForFreeze

### Description
If this list grid is showing any [frozen](ListGridField.md#attr-listgridfieldfrozen) fields, and a horizontal scrollbar is visible at the bottom of the liquid columns, should an equivalent scrollbar gap be left visible below the frozen columns?  
Note that if set to `true` any backgroundColor or border applied to the ListGrid will show up below the bottom row of the frozen column(s).

### Groups

- frozenFields

**Flags**: IRWA

---
## Attr: ListGrid.canSelectSummaryRows

### Description
Whether to allow selection of the summary row, for example by clicking on the record. The default is to disallow it.

If this property is set, further customization of selection can be made by applying the appropriate selection-related properties to the autochild via [summaryRowProperties](#attr-listgridsummaryrow). The request to fetch the summary row(s) can be customized via [ListGrid.summaryRowFetchRequestProperties](#attr-listgridsummaryrowfetchrequestproperties).

**Flags**: IRA

---
## Attr: ListGrid.rowNumberField

### Description
An automatically generated field that displays the current row number when [showRowNumbers](#attr-listgridshowrownumbers) is true.

### Groups

- rowNumberField

**Flags**: IRWA

---
## Attr: ListGrid.selectOnEdit

### Description
When the user starts editing a row, should the row also be selected?

See [ListGrid.editSelectionType](#attr-listgrideditselectiontype) for how edit-selection behaves.

### Groups

- editing

**Flags**: IRWA

---
## Attr: ListGrid.expansionMode

### Description
The [ExpansionMode](../reference_2.md#type-expansionmode) for records in this grid.

If [canExpandRecords](#attr-listgridcanexpandrecords) is true but `expansionMode` is not set, it defaults to "detailRelated" if [ListGrid.detailDS](#attr-listgriddetailds) is set, or to "details" otherwise.

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.checkboxFieldImageHeight

### Description
If [ListGrid.selectionAppearance](#attr-listgridselectionappearance) is set to `"checkbox"` this property may be set to govern the height of the checkbox image displayed to indicate whether a row is selected. If unset, the checkboxField image will be sized to match the [ListGrid.booleanImageHeight](#attr-listgridbooleanimageheight) for this grid.

### Groups

- checkboxField

**Flags**: IR

---
## Attr: ListGrid.canResizeFields

### Description
Indicates whether fields in this listGrid can be resized by dragging header fields.

### Groups

- dragging

**Flags**: IRW

---
## Attr: ListGrid.alwaysShowOperatorIcon

### Description
When [ListGrid.allowFilterOperators](#attr-listgridallowfilteroperators) is enabled, whether to show the [ListGrid.operatorIcon](#attr-listgridoperatoricon) for all filterable fields, or only for fields where the user has explicitly chosen a search operator different from the default operator for the field.

The default operator for a field is determined by [ListGrid.autoFetchTextMatchStyle](#attr-listgridautofetchtextmatchstyle) or by setting [ListGridField.filterOperator](ListGridField.md#attr-listgridfieldfilteroperator) for a specific field.

**Flags**: IR

---
## Attr: ListGrid.fetchFields

### Description
Fields that will be always requested from the server when the grid fetches data, even if they are not visible - may be either an array of fields or a CSV string.

If `fetchFields` has been set, then aside from the declared `fetchFields`, the full set of requested fields will always include the primary-key fields from the dataSource and any visible fields that are also DataSource fields - so if either a [SavedSearch](SavedSearches.md#class-savedsearches) or the [ListGrid.fields](#attr-listgridfields) configuration includes fields not declared in `fetchFields`, those fields will be requested from the server even if they are not included in `fetchFields`.

In addition, any fields that are referenced by declarative features, such as [UserFormula](../reference.md#object-userformula) or [ListGridField.visibleWhen](ListGridField.md#attr-listgridfieldvisiblewhen), will also be automatically included, even if not listed in `fetchFields`. Also applies to declarative [expansion](../reference_2.md#type-expansionmode) and [hover](../reference.md#type-hovermode) modes, where fields required by those modes are also fetched.

This means you can essentially set `fetchFields` to just fields that always need to be there, whether visible or not - such as fields that are required by custom grid logic (e.g. formatters, or [ListGrid.canEditCell](ListGrid_2.md#method-listgridcaneditcell)) or may be required when other components interact with the data (such as editing a record from the grid in a form via [DynamicForm.editSelectedData](DynamicForm.md#method-dynamicformeditselecteddata)).

To enable the feature of causing just primary-keys, visible and declaratively required fields to be requested, without any specific additional fields, you can set `fetchFields` to the special value "\*visible\*". In order for application code to more easily build a list of fields, you may also include this special value in a compound string, such as _"\*visible\*, field1, field2"_ - in this case, the special value is simply ignored, since visible fields are always requested if `fetchFields` is set to a value.

If `fetchFields` includes fields which do not appear in the dataSource, a warning is logged and those fields will not be requested from the server.

Fields to be retrieved are communicated to the server via [DSRequest.outputs](DSRequest.md#attr-dsrequestoutputs).

If a user dynamically shows additional fields (via the field picking menu, via Saved Search or another mechanism), and such fields are not currently loaded, the ListGrid will automatically invalidate the data cache and issue a new fetch with a different dsRequest.outputs setting in order to fetch the necessary data.

If `fetchFields` has been set and outputs are also set via another mechanism (like [ListGrid.fetchRequestProperties](#attr-listgridfetchrequestproperties)), `fetchFields` wins.

Note that since `fetchFields` ultimately just sets [DSRequest.outputs](DSRequest.md#attr-dsrequestoutputs), [DataSourceField.outputWhen](DataSourceField.md#attr-datasourcefieldoutputwhen) settings will override `fetchFields` settings. This also means that, currently, `fetchFields` is not supported by clientOnly DataSources, because they do not support dsRequest.outputs.

Additionally, if [OperationBinding.outputs](OperationBinding.md#attr-operationbindingoutputs) is specified in a server-side .ds.xml file, `fetchFields` will only be able to request fields listed as valid server outputs. In general, client-specified outputs do not override server-specified outputs; client-specified outputs must be a subset of outputs listed on the server.

### Groups

- databinding

**Flags**: IRW

---
## Attr: ListGrid.selectionProperty

### Description
If specified, the selection object for this list will use this property to mark records as selected. In other words, if this attribute were set to `"isSelected"` any records in the listGrid data where `"isSelected"` is `true` will show up as selected in the grid. Similarly if records are selected within the grid after the grid has been created, this property will be set to true on the selected records.

### Groups

- selection
- appearance

**Flags**: IRA

---
## Attr: ListGrid.frozenRollUnderCanvas

### Description
Automatically generated canvas embedded in the grid's frozen body as a [roll under canvas](#attr-listgridrollundercanvas). This component will be created and displayed above the current rollOver row or cell in the frozen body.

The frozenRollUnderCanvas will be created using the [AutoChild](../reference.md#type-autochild) subsystem, and will derive its configuration from the [ListGrid.rollUnderCanvas](#attr-listgridrollundercanvas) autoChild properties (`"rollUnderCanvasProperties"`, et al).

The `frozenRollUnderCanvas` has the following read-only attributes set:  
\- `this.grid` - a pointer to the grid  
\- `this.record` - a pointer to the current roll over record object in the grid

### Groups

- rowEffects

### See Also

- [ListGrid.rollUnderCanvas](#attr-listgridrollundercanvas)
- [ListGrid.frozenRollOverCanvas](#attr-listgridfrozenrollovercanvas)

**Flags**: RA

---
## Attr: ListGrid.useAdvancedFieldPicker

### Description
If set to true, an advanced field picker based on the [FieldPicker](FieldPicker.md#class-fieldpicker) will be shown instead of the column picker submenu if there are more fields in the grid than [ListGrid.advancedFieldPickerThreshold](#attr-listgridadvancedfieldpickerthreshold).

When there are large numbers of available fields, the FieldPicker-based interface is more usable for both defining visible fields and defining field order.

**Flags**: IR

---
## Attr: ListGrid.showFilterEditor

### Description
Should this listGrid display a filter row. If true, this ListGrid will be drawn with a single editable row, (separate from the body) with a filter button.

Values entered into this row are used as filter criteria to filter this List's data. The [ListGrid.filterByCell](#attr-listgridfilterbycell) and [ListGrid.filterOnKeypress](#attr-listgridfilteronkeypress) attributes allow developers to configure whether filtering occurs automatically on change or requires an enter-keypress or filter button click.  
[ListGrid.autoFetchTextMatchStyle](#attr-listgridautofetchtextmatchstyle) determines the textMatchStyle for the request passed to [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata).

The default [search operator](FormItem.md#attr-formitemoperator) for an item in the filterEditor can be set via [ListGridField.filterOperator](ListGridField.md#attr-listgridfieldfilteroperator). When `field.filterOperator` has been set calls to retrieve the criteria from the grid return [AdvancedCriteria](../reference.md#object-advancedcriteria). See also [ListGrid.allowFilterOperators](#attr-listgridallowfilteroperators) for a UI that allows end users to change the search operator on the fly

Note that if [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata) or [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata) is called directly while the filter editor is showing, the filter editor values will be updated to reflect the new set of criteria. If you wish to retain the user entered filter criteria and modify a subset of field values programmatically, this can be achieved by copying the existing set of criteria and adding other changes - something like this:

```
   var newCriteria = myListGrid.getFilterEditorCriteria();
   isc.DataSource.combineCriteria(newCriteria, {
      field1:"new value1",
      field2:"new value2"
   });
   myListGrid.setCriteria(newCriteria);
 
```
In this example code we're using [ListGrid.getFilterEditorCriteria](ListGrid_2.md#method-listgridgetfiltereditorcriteria) rather than [ListGrid.getCriteria](ListGrid_2.md#method-listgridgetcriteria) - this ensures that if the user has typed a new value into the filter editor, but not yet clicked the filter button, we pick up the value the user entered. This sample code uses [DataSource.combineCriteria](DataSource.md#classmethod-datasourcecombinecriteria) to combine the existing filterEditorCriteria with some new custom criteria. This technique is applicable to both simple and advanced criteria.

If you call `filterData()` and pass in criteria for dataSource fields that are not present in the ListGrid, these criteria will continue to be applied along with the user-visible criteria.

**filterEditor and advanced criteria**: If a developer calls `filterData()` on a ListGrid and passes in [AdvancedCriteria](../reference.md#object-advancedcriteria), expected behavior of the filter editor becomes ambiguous, since AdvancedCriteria has far more complex filter expression support than the ordinary filterEditor can represent.

Default behavior for AdvancedCriteria will combine the AdvancedCriteria with the values in the filter editor as follows:

*   If the top level criteria has operator of type "and":  
    Each field in the top level criteria array for which a 'canFilter' true field is shown in the listGrid will show up if the specified operator matches the default filter behavior (based on the [ListGrid.autoFetchTextMatchStyle](#attr-listgridautofetchtextmatchstyle)).  
    If the user enters values in the filter editor, these will be combined with the existing AdvancedCriteria by either replacing or adding field level criteria at the top level.
*   If the top level criteria is a single field-criteria:  
    If the field shows up in the listGrid and is canFilter:true, it will be displayed to the user (if the operator matches the default filter behavior for the field).  
    If the user enters new filter criteria in the filterEditor, they will be combined with this existing criterion via a top level "and" operator, or if the user modifies the field for which the criterion already existed, it will be replaced.
*   Otherwise, if there are multiple top level criteria combined with an "or" operator, these will not be shown in the filter editor. Any filter parameters the user enters will be added to the existing criteria via an additional top level "and" operator, meaning the user will essentially filter a subset of the existing criteria

### Groups

- filterEditor

**Flags**: IRW

---
## Attr: ListGrid.canSelectCells

### Description
Enables cell-level selection behavior as well as [cell-level rollover](#attr-listgridusecellrollovers).

To query and manipulate cell-level selections, use [ListGrid.getCellSelection](ListGrid_2.md#method-listgridgetcellselection) to retrieve the [CellSelection](CellSelection.md#class-cellselection).

Note that the ListGrid has a data model of one [Record](../reference.md#object-record) per row, unlike the [CubeGrid](CubeGrid.md#class-cubegrid) which supports one [CellRecord](../reference.md#object-cellrecord) per cell. For this reason record-oriented APIs that act on the selection will act on entire Records that have _any_ selected cells (examples include drag and drop and transferSelectedData()).

More generally, `canSelectCells` is primarily intended to enable developers to build Excel-like interactions on local datasets, by using [ListGrid.setData](ListGrid_2.md#method-listgridsetdata) plus [ListGrid.saveLocally](#attr-listgridsavelocally):true rather than record-oriented DataSources and data binding. You can also use `canSelectCells` in conjunction with [SelectionAppearance](../reference.md#type-selectionappearance) set to "checkbox" to complete this experience.

The following keyboard selection behaviors are enabled with this property in addition to standard single-selection Arrow Key navigation:

SHIFT + \[Arrow Key\]: begin or continue incremental selection

SHIFT + CTRL + \[Arrow Key\]: incremental selection to the end of row or column

CTRL + A: select all cells (enabled only with [ListGrid.canSelectAll](#attr-listgridcanselectall))

Incremental selection allows selection of rows and columns of cells via keyboard or mouse provided the shift key is down. Behavior is designed to match Excel. Thus, if a previous selection has begun, cells will be selected from that origin.

Users may also navigate through cells using the _Tab_ and _Shift+Tab_ keypresses if [ListGrid.navigateOnTab](#attr-listgridnavigateontab) is true. When a user tabs to the end of the row, the [ListGrid.rowEndEditAction](#attr-listgridrowendeditaction) is used to determine whether to shift selection to the next row, return to the beginning of the same row, or simply move on through the page's tab order.

**Flags**: IR

---
## Attr: ListGrid.allowFilterWindow

### Description
Adds the ability for a user to define additional criteria above and beyond those expressed in the [filter editor](#attr-listgridshowfiltereditor) via a [FilterBuilder](FilterBuilder.md#class-filterbuilder) which appears in a modal Window over the grid and can be accessed by various menus within the grid or triggered by external controls.

Causes a menu item titled ["Advanced Filtering"](#attr-listgridadvancedfilteringtext) to appear in the ["Filter using"](#attr-listgridfilterusingtext) menu show in the [headerContextMenu](#attr-listgridshowheadercontextmenu) that allows the end user to configure an advanced filter on the grid that can supplement the [filter editor](#attr-listgridshowfiltereditor). Note that the menu option will show even if [filter operators](#attr-listgridallowfilteroperators) is disabled.

To use this feature, the grid must be configured with a [DataSource](DataSource.md#class-datasource). In fact, this feature is enabled by default if the grid has a [DataSource](DataSource.md#class-datasource) and both [DataSource.supportsAdvancedCriteria](DataSource.md#method-datasourcesupportsadvancedcriteria) and [ListGrid.allowFilterOperators](#attr-listgridallowfilteroperators) are true. This default can be disabled by setting `allowFilterWindow` to `false`.

[This example](https://www.smartclient.com/smartclient-latest/showcase/?id=filterWindow) shows the `allowFilterWindow` setting in use.

**Note:** this feature requires [SmartClient Pro](https://www.smartclient.com/product/) or better.

Enabling [filter via AI](#attr-listgridfilterviaaimode) forces this setting to true.

### See Also

- [ListGrid.allowFilterOperators](#attr-listgridallowfilteroperators)

**Flags**: IR

---
## Attr: ListGrid.showNewRecordRow

### Description
If this is an editable ListGrid, setting this property to true causes an extra row with the [ListGrid.newRecordRowMessage](#attr-listgridnewrecordrowmessage) to be displayed below the last record.

Clicking this row will start editing a new record at the end of the data set, as if [ListGrid.startEditingNew](ListGrid_2.md#method-listgridstarteditingnew) had been called.

Note that for [databound grids](#attr-listgriddatasource), the new record row will be suppressed if the grid has not [fetched data](ListGrid_2.md#method-listgridfetchdata), unless [ListGrid.saveLocally](#attr-listgridsavelocally) has been set.

**Flags**: IRW

---
## Attr: ListGrid.multiGroupDialogDefaults

### Description
Class-level defaults to apply to the [MultiGroupDialog](MultiGroupDialog.md#class-multigroupdialog) which gets automatically generated when [ListGrid.configureGrouping](ListGrid_2.md#method-listgridconfiguregrouping) is called.

**Flags**: IR

---
## Attr: ListGrid.exactRowCountFormat

### Description
Format for the string returned from [ListGrid.getFormattedRowCount](ListGrid_2.md#method-listgridgetformattedrowcount) when [row count status](ListGrid_2.md#method-listgridgetrowcountstatus) is `"exact"`.

The variable `rowCount` is available for evaluation within this string and will be set to the [current row count](ListGrid_2.md#method-listgridgetrowcount) as a [locale-formatted number](NumberUtil.md#classmethod-numberutiltolocalizedstring).

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.detailField

### Description
The field whose contents to show in the expanded portion of a record when [canExpandRecords](#attr-listgridcanexpandrecords) is `true` and [listGrid.expansionMode](../reference_2.md#type-expansionmode) is `detailField`.

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.canEditTitles

### Description
If set to true, the [advanced field picker](#attr-listgriduseadvancedfieldpicker) provides an interface allowing users to modify fields' titles.

Note that when enabled, the [field state](ListGrid_2.md#method-listgridgetfieldstate) for this component will include field titles by default (see [DataBoundComponent.shouldIncludeTitleInFieldState](DataBoundComponent.md#method-databoundcomponentshouldincludetitleinfieldstate)).

**Flags**: IRW

---
## Attr: ListGrid.isSeparatorProperty

### Description
If `record[this.isSeparatorProperty]` is set for some record, the record will be displayed as a simple separator row.

**Flags**: IRW

---
## Attr: ListGrid.minimumRowCountFormat

### Description
Format for the string returned from [ListGrid.getFormattedRowCount](ListGrid_2.md#method-listgridgetformattedrowcount) when [row count status](ListGrid_2.md#method-listgridgetrowcountstatus) is `"minimum"`.

The variable `rowCount` is available for evaluation within this string and will be set to the [current row count](ListGrid_2.md#method-listgridgetrowcount) as a [locale-formatted number](NumberUtil.md#classmethod-numberutiltolocalizedstring).

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.printMaxRows

### Description
Advanced property - when generating printHTML for a large ListGrid, rows are printed in batches in order to avoid triggering a native "script is running slowly" browser dialog.

For grids with exceptional numbers of columns or complex formatting logic, this number might need to be adjusted downward.

### Groups

- printing

**Flags**: IRWA

---
## Attr: ListGrid.sortNumeralStyle

### Description
When multiple fields are sorted, the Style to apply to the numeral that appears after the sort-arrows in the header-buttons of sorted fields.

**Flags**: IRWA

---
## Attr: ListGrid.multiSortDialogDefaults

### Description
Class level defaults to apply to the [MultiSortDialog](MultiSortDialog.md#class-multisortdialog) which gets automatically generated when [DataBoundComponent.askForSort](DataBoundComponent.md#method-databoundcomponentaskforsort) is called.

See also [ListGrid.showHeaderSpanTitlesInSortEditor](#attr-listgridshowheaderspantitlesinsorteditor) and [ListGrid.sortEditorSpanTitleSeparator](#attr-listgridsorteditorspantitleseparator)

**Flags**: IR

---
## Attr: ListGrid.fieldPickerWindow

### Description
Instance of [FieldPickerWindow](FieldPickerWindow.md#class-fieldpickerwindow) used if [ListGrid.useAdvancedFieldPicker](#attr-listgriduseadvancedfieldpicker) is set.

**Flags**: IR

---
## Attr: ListGrid.rowCountDisplayPrecision

### Description
When an exact [row count](ListGrid_2.md#method-listgridgetrowcount) is not known due to progressive loading, this attribute allows the formatted row count returned by [ListGrid.getFormattedRowCount](ListGrid_2.md#method-listgridgetformattedrowcount) and ultimately displayed in the [rowRangeDisplay label](#attr-listgridrowrangedisplay) to be rounded to a multiple of the specified value. If not explicitly set, this value defaults to the [page size](ResultSet.md#attr-resultsetresultsize) for the data.

For example if the server reports a [DSResponse.totalRows](DSResponse.md#attr-dsresponsetotalrows) of `320` while progressive loading is active (meaning this is not an exact row count), and `rowCountDisplayPrecision` is set to `150`, the formatted rowCount may display `300+`

The precision will round either up or down depending on the [row count status](ListGrid_2.md#method-listgridgetrowcountstatus).

*   `rowCountStatus:"exact"` - this setting has no effect
*   `rowCountStatus:"minimum"` - the reported row count will be rounded down to the previous multiple of this value.
*   `rowCountStatus:"maximum"` - the reported row count will be rounded up to the next multiple of this value.
*   `rowCountStatus:"approximate"` - the reported row count will be rounded either up or down to the nearest multiple of this value.
*   `rowCountStatus:"range"` - the reported minimum row count will be rounded down to the next multiple of this value, and the reported maximum will be rounded up to the next multiple of this value.

Note the formatted row count will never be rounded down to zero - if the row count is less than the `rowCountDisplayPrecision`, the exact reported row count value will be displayed. This could typically only occur if `rowCountDisplayPrecision` is more than the [page size](ResultSet.md#attr-resultsetresultsize) for the data.

This value may be set to `1` to effectively disable the rounding behavior altogether (the row count will not be displayed exactly as reported).

Note that this is purely a formatting setting for the formatted row count string. It has no impact on the behavior of the grid in terms of the reported [data length](ResultSet.md#method-resultsetgetlength), [totalRows](ListGrid_2.md#method-listgridgettotalrows) or scrollable area.

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.resizeFieldsInRealTime

### Description
If `true`, the grid contents are redrawn in real time as fields are resized. This can be slow with a large grid and/or on some platforms. By default, this is enabled in modern desktop browsers. This is automatically switched off in mobile browsers.

### Groups

- dragging

**Flags**: IRWA

---
## Attr: ListGrid.useMultiSelectForFilterValueMaps

### Description
If [ListGrid.showFilterEditor](#attr-listgridshowfiltereditor) is true, when creating a SelectItem for editing criteria for a field with a ValueMap, should the SelectItem default to [multiple:true](SelectItem.md#attr-selectitemmultiple)?

This overrides [SearchForm.useMultiSelectForValueMaps](SearchForm.md#attr-searchformusemultiselectforvaluemaps) on the filterEditor's edit form.

**Flags**: IRWA

---
## Attr: ListGrid.showAsynchGroupingPrompt

### Description
If set to false, do not show the [ListGrid.asynchGroupingPrompt](#attr-listgridasynchgroupingprompt) dialog during [asynchronous grouping](#attr-listgridgroupbyasyncthreshold).

**Flags**: IR

---
## Attr: ListGrid.briefRowRangeDisplayValue

### Description
Dynamic String specifying the format for the [row range summary value](ListGrid_2.md#method-listgridgetrowrangedisplayvalue) when [RowRangeDisplayStyle](../reference_2.md#type-rowrangedisplaystyle) is set to `"brief"`.

The following variables are available for evaluation within this string:

*   `rowRange`: the [formatted row range](ListGrid_2.md#method-listgridgetformattedrowrange)
*   `rowCount`: the [formatted row count](ListGrid_2.md#method-listgridgetformattedrowcount)

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.expansionEditorCollapseOnSave

### Description
When [ExpansionMode](../reference_2.md#type-expansionmode) is _editor_, should the row be collapsed following a save initiated by the expansion-component's [save button](#attr-listgridexpansioneditorsavebutton).

### Groups

- expansionField

**Flags**: RW

---
## Attr: ListGrid.detailDS

### Description
If [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) is true and [listGrid.expansionMode](../reference_2.md#type-expansionmode) is `"related"`, this property specifies the dataSource for the related records grid to be shown embedded in expanded records.

This property may also be specified on a per-record basis - see [ListGrid.recordDetailDSProperty](#attr-listgridrecorddetaildsproperty)

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.groupStartOpen

### Description
Describes the default state of ListGrid groups when groupBy is called. Possible values are:

*   "all": open all groups
*   "first": open the first group
*   "none": start with all groups closed
*   Array of group values that should be opened

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IRW

---
## Attr: ListGrid.useAllDataSourceFields

### Description
If true, the set of fields given by the "default binding" (see [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields)) is used, with any fields specified in `component.fields` acting as overrides that can suppress or modify the display of individual fields, without having to list the entire set of fields that should be shown.

If `component.fields` contains fields that are not found in the DataSource, they will be shown after the most recently referred to DataSource field. If the new fields appear first, they will be shown first.

*This example* shows a mixture of component fields and DataSource fields, and how they interact for validation.

This setting may be cleared if a [FieldPicker](FieldPicker.md#class-fieldpicker) is used to edit the component's field order.

### Groups

- databinding

### See Also

- [FieldPicker.dataBoundComponent](FieldPicker.md#attr-fieldpickerdataboundcomponent)

**Flags**: IRW

---
## Attr: ListGrid.sortFieldAscendingText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, this attribute will be shown as the menu item title to sort a field in ascending order.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.canTabToHeader

### Description
Should the header be included in the tab-order for the page? If not explicitly specified, the header will be included in the tab order for the page if [isc.setScreenReaderMode()](isc.md#staticmethod-iscsetscreenreadermode) is called.

### Groups

- accessibility

**Flags**: IR

---
## Attr: ListGrid.expansionEditorSaveButtonTitle

### Description
The title for the [ListGrid.expansionEditorSaveButton](#attr-listgridexpansioneditorsavebutton).

### Groups

- expansionField
- i18nMessages

**Flags**: RWA

---
## Attr: ListGrid.recordDropAppearance

### Description
If [ListGrid.canAcceptDroppedRecords](#attr-listgridcanacceptdroppedrecords) is true for this listGrid, this property governs whether the user can drop between, or over records within the grid. This controls what [RecordDropPosition](../reference.md#type-recorddropposition) is passed to the [ListGrid.recordDrop](ListGrid_2.md#method-listgridrecorddrop) event handler.

**Flags**: IRW

---
## Attr: ListGrid.hoverScreen

### Description
Screen to create (via [createScreen()](RPCManager.md#classmethod-rpcmanagercreatescreen)) in lieu of calling [getHoverComponent()](Canvas.md#method-canvasgethovercomponent) or [ListGrid.getCellHoverComponent](ListGrid_2.md#method-listgridgetcellhovercomponent).

If this grid has a [dataSource](DataBoundComponent.md#attr-databoundcomponentdatasource), the created screen is provided with a [Canvas.dataContext](Canvas.md#attr-canvasdatacontext) that includes the record being shown at the row.

### Groups

- hoverComponents

**Flags**: IR

---
## Attr: ListGrid.expansionEditorSaveDialogPrompt

### Description
When [canExpandRecords](#attr-listgridcanexpandrecords) is true and [expansionMode](#attr-listgridexpansionmode) is _editor_, the prompt to display in a dialog when an expanded row is collapsed while it's nested editor has changed values.

### Groups

- expansionField
- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [ListGrid.initialCriteria](#attr-listgridinitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](#attr-listgridautofetchtextmatchstyle). Additional request properties may be specified using [ListGrid.fetchRequestProperties](#attr-listgridfetchrequestproperties).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_2.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [ListGrid.initialCriteria](#attr-listgridinitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_2.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- databinding

### See Also

- [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata)

**Flags**: IR

---
## Attr: ListGrid.hiliteViaAIText

### Description
Title for the menu item displayed in this component's header context menu when [AI-assisted hiliting](#attr-listgridcanhiliteviaai) is allowed.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.animateRemoveTime

### Description
When animating record removal [(see animateRemoveRecord)](#attr-listgridanimateremoverecord), if [ListGrid.animateRemoveSpeed](#attr-listgridanimateremovespeed) is not set, this property designates the duration of the animation in ms.

### Groups

- animation

### See Also

- [ListGrid.animateRemoveRecord](#attr-listgridanimateremoverecord)

**Flags**: IRW

---
## Attr: ListGrid.recordComponentPosition

### Description
if [ListGrid.showRecordComponents](#attr-listgridshowrecordcomponents) is true, how should the component appear within the cell. Valid options are

*   `"within"`: the component will be rendered inside the record / cell. [Canvas.snapTo](Canvas.md#attr-canvassnapto) may be set to specify where the component should render within the row or cell, and [Canvas.snapOffsetTop](Canvas.md#attr-canvassnapoffsettop) / [Canvas.snapOffsetLeft](Canvas.md#attr-canvassnapoffsetleft) may be set to indent recordComponents within their parent cells. Note that if unset, the component will show up at the top/left edge for components embedded within an entire row, or for per-cell components, cell align and valign will be respected. Note also that, when rendering components "within" cells, specified component heights will be respected and will change the height of the row. However, if you want components to completely fill a cell at it's default height, set height: "100%" or rows will render at the default height of the component.
*   `"expand"`: the component will be written into the cell below the normal cell content, causing the cell to expand vertically to accommodate it.
*   `null`: If this attribute is unset, we will default to showing recordComponents with position `"within"` if [ListGrid.showRecordComponentsByCell](#attr-listgridshowrecordcomponentsbycell) is true, otherwise using `"expand"` logic.

### Groups

- recordComponents

### See Also

- [ListGrid.showRecordComponents](#attr-listgridshowrecordcomponents)

**Flags**: IRW

---
## Attr: ListGrid.modalEditing

### Description
If this property is true, any mouse click outside of the open cell editors will end editing mode, hiding the cell editors and saving any changes to those cell values.

### Groups

- editing

**Flags**: IRWA

---
## Attr: ListGrid.animateFolders

### Description
If true, when folders are opened / closed children will be animated into view.

For a ListGrid, this property applies when [grouping](#attr-listgridcangroupby) is enabled.

### Groups

- animation

**Flags**: IRW

---
## Attr: ListGrid.headerSpanConstructor

### Description
[SmartClient Class](../reference.md#type-scclassname) to use for headerSpans. Typically a [Button](Button.md#class-button) or [StretchImgButton](StretchImgButton.md#class-stretchimgbutton) subclass.

If unset, headerSpans will be created using the [ListGrid.headerButtonConstructor](#attr-listgridheaderbuttonconstructor).

### Groups

- headerSpan

**Flags**: IR

---
## Attr: ListGrid.autoFitDateFields

### Description
Should listGrids automatically size date fields to fit their values or titles? If set to `"value"`, fields of type date will be rendered at the size specified by [ListGrid.defaultDateFieldWidth](#attr-listgriddefaultdatefieldwidth), (or [ListGrid.defaultEditableDateFieldWidth](#attr-listgriddefaulteditabledatefieldwidth) for editable fields). This static value is appropriate for dates rendered with the standard short-date formatter. If set to `"title"` or `"both"`, the drawn width of the title will be taken into account when sizing the column.

This is achieved by enabling [autoFitWidth:true](ListGridField.md#attr-listgridfieldautofitwidth) on date fields when this property is set to anything other than `"none"`, setting the [ListGridField.autoFitWidthApproach](ListGridField.md#attr-listgridfieldautofitwidthapproach) to the value specified here and having logic in [ListGrid.getDefaultFieldWidth](ListGrid_2.md#method-listgridgetdefaultfieldwidth) pick up the [ListGrid.defaultDateFieldWidth](#attr-listgriddefaultdatefieldwidth) or [ListGrid.defaultEditableDateFieldWidth](#attr-listgriddefaulteditabledatefieldwidth) if appropriate.

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.autoComplete

### Description
Whether to do inline autoComplete in text fields during inline editing  
Overridden by [ListGridField.autoComplete](ListGridField.md#attr-listgridfieldautocomplete) if specified. If unset picks up the default from the appropriate editor class (subclass of FormItem).

### Groups

- autoComplete

### See Also

- [ListGridField.autoComplete](ListGridField.md#attr-listgridfieldautocomplete)

**Flags**: IRW

---
## Attr: ListGrid.showClippedValuesOnHover

### Description
If true and a cell's value is clipped, then a hover containing the full cell value is enabled.

Note that standard cell hovers override clipped value hovers. Thus, to enable clipped value hovers, [canHover](#attr-listgridcanhover) must be unset or null and the corresponding field must have [showHover](ListGridField.md#attr-listgridfieldshowhover) unset or null as well.

### Groups

- events

### See Also

- [ListGrid.canHover](#attr-listgridcanhover)
- [ListGrid.cellValueHoverHTML](ListGrid_2.md#method-listgridcellvaluehoverhtml)

**Flags**: IRA

---
## Attr: ListGrid.tallBaseStyle

### Description
"Tall" baseStyle for this listGrid. Only applies if [ListGrid.baseStyle](#attr-listgridbasestyle) is set to null.

If `baseStyle` is unset, this property will be used as a base cell style unless the grid is showing fixed height rows with a specified cellHeight that matches [ListGrid.normalCellHeight](#attr-listgridnormalcellheight), in which case [ListGrid.normalBaseStyle](#attr-listgridnormalbasestyle) will be used. Note that in Internet Explorer if [ListGrid.fastCellUpdates](#attr-listgridfastcellupdates) is true, `tallBaseStyle` will also be used even if the cellHeight matches the specified `normalCellHeight` for the grid.

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### See Also

- [ListGrid.getBaseStyle](ListGrid_2.md#method-listgridgetbasestyle)

**Flags**: IR

---
## Attr: ListGrid.showHilitesInGroupSummary

### Description
Determines whether hiliting for any field in this grid is shown in a group summary. This setting affects all fields of the grid.

To suppress hilites for a specific field see [ListGridField.showHilitesInGroupSummary](ListGridField.md#attr-listgridfieldshowhilitesingroupsummary).

Hiliting in summary fields (columns) can be enabled by setting [includeHiliteInSummaryField](#attr-listgridincludehilitesinsummaryfields) to true.

**Flags**: IRW

---
## Attr: ListGrid.headerSpanVAlign

### Description
Default alignment for [headerSpans](#attr-listgridheaderspans) with no [HeaderSpan.valign](HeaderSpan.md#attr-headerspanvalign) specified.

### Groups

- headerSpan

**Flags**: IR

---
## Attr: ListGrid.canMultiSort

### Description
When true, indicates that this ListGrid supports sorting on multiple fields. Note that even when set to true, multi-field sorting may not be available if the grid is databound and the ${isc.DocUtils.linkForRef('attr:DataSource.canMultiSort','DataSource doesn\\'t support multi-sort')}, or if sorting for a field is [client-only](ListGridField.md#attr-listgridfieldcansortclientonly) but not all data is available.

### See Also

- [ListGrid.sortNumeralMenuButtonSpaceOffset](#attr-listgridsortnumeralmenubuttonspaceoffset)

**Flags**: IRW

---
## Attr: ListGrid.discardDataOnSetFetchOperation

### Description
If [ListGrid.setFetchOperation](ListGrid_2.md#method-listgridsetfetchoperation) is invoked while this grid is showing a filtered data-set, should the data set be discarded?

**Flags**: IRA

---
## Attr: ListGrid.showDropLines

### Description
Controls whether to show a drop-indicator during a drag and drop operation.

**Flags**: IRW

---
## Attr: ListGrid.autoFitMaxColumns

### Description
If [ListGrid.autoFitData](#attr-listgridautofitdata) is set to `"horizontal"` or `"both"` this property provides the maximum number of columns for which the ListGrid will expand. If more columns are present, scrolling will be introduced to reach them as normal. If unset the ListGrid will expand to accommodate as many columns as are defined for the grid.

### Groups

- autoFitData

**Flags**: IRW

---
## Attr: ListGrid.blockingRowCountFetch

### Description
If specified, this attribute will be applied to this grid's [data object](ResultSet.md#attr-resultsetblockingrowcountfetch) for dataBound grids.

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.saveLocally

### Description
For grids with a specified [ListGrid.dataSource](#attr-listgriddatasource), this property can be set to `true` to cause the grid directly update its local data set instead of performing an operation against it's configured DataSource.

When using this mode, data must be provided to the grid via [ListGrid.setData](ListGrid_2.md#method-listgridsetdata), and must be provided as a simple Array of Records . Setting `saveLocally` is invalid if either [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata) is called or if a [ResultSet](ResultSet.md#class-resultset) is provided as the data model.

`saveLocally` mode includes changes made via [inline editing](#attr-listgridcanedit), record removal via [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords), as well as programmatic calls to [ListGrid.updateData](ListGrid_2.md#method-listgridupdatedata), [addData()](ListGrid_2.md#method-listgridadddata) and [removeData()](ListGrid_2.md#method-listgridremovedata). This also causes saves to be performed synchronously (unlike normal DataSource operations).

Note that using this mode also disables the automatic cache synchronization provided by the DataSource system - changes made to this grid are saved only to this grid's data set.

See also [ListGrid.filterLocalData](#attr-listgridfilterlocaldata) to allow filtering, such as filtering performed by the [ListGrid.filterEditor](#attr-listgridfiltereditor), to also work only with the local data set.

If saveLocally is unset, and [ListGrid.filterLocalData](#attr-listgridfilterlocaldata) is true, the saveLocally behavior is enabled by default

### Groups

- databinding

### See Also

- [ListGrid.useRemoteValidators](#attr-listgriduseremotevalidators)

**Flags**: IRA

---
## Attr: ListGrid.exportRawNumbers

### Description
Dictates whether numeric values should be exported as raw numbers instead of formatted values when using [exportClientData()](ListGrid_2.md#method-listgridexportclientdata).

This property is only consulted if `exportRawValues` is not set to true at the [grid](#attr-listgridexportrawvalues) or [field](ListGridField.md#attr-listgridfieldexportrawvalues) level. That property causes all values, including numeric values, to be exported unformatted.

This is useful for cases where an explicit ListGrid formatter function simply displays the number as a formatted string for the user (for example "1,234"). Exporting that formatted string rather than the underlying numeric value causes spreadsheet applications such as Excel to lose some functionality.

If this property is not explicitly set, numeric values will be exported as raw numbers for [XLS and OOXML export](DSRequest.md#attr-dsrequestexportas) only.

May be overridden at the field level via [ListGridField.exportRawNumbers](ListGridField.md#attr-listgridfieldexportrawnumbers).

**Flags**: IR

---
## Attr: ListGrid.frozenHeaderTitleStyle

### Description
If this listGrid contains any frozen fields, this property can be used to apply a custom headerTitleStyle to the frozen set of fields. If unset, the standard headerTitleStyle will be used for both frozen and unfrozen cells.

### Groups

- gridHeader
- appearance
- frozenFields

### See Also

- [ListGrid.headerTitleStyle](#attr-listgridheadertitlestyle)
- [ListGridField.frozen](ListGridField.md#attr-listgridfieldfrozen)

**Flags**: IR

---
## Attr: ListGrid.maxExpandedRecords

### Description
When [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) and [ListGrid.canExpandMultipleRecords](#attr-listgridcanexpandmultiplerecords) are both true, this property dictates the number of records which can be expanded simultaneously. If the expanded record count hits the value of this property, further attempts to expand records will result in a popup warning (see [ListGrid.maxExpandedRecordsPrompt](#attr-listgridmaxexpandedrecordsprompt)) and expansion will be cancelled.

The default value is null, meaning there is no limit on the number of expanded records.

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.canAcceptDroppedRecords

### Description
Indicates whether records can be dropped into this listGrid.

### Groups

- dragging

### See Also

- [ListGridRecord.canDrag](ListGridRecord.md#attr-listgridrecordcandrag)
- [ListGridRecord.canAcceptDrop](ListGridRecord.md#attr-listgridrecordcanacceptdrop)

**Flags**: IRW

---
## Attr: ListGrid.showAllRecords

### Description
Whether all records should be drawn all at once, or only records visible in the viewport.

Drawing all records causes longer initial rendering time, but allows smoother vertical scrolling. With a very large number of records, showAllRecords will become too slow.

This setting is incompatible with [ListGrid.dataFetchMode](#attr-listgriddatafetchmode): "paged" as it requires all records matching the criteria to be fetched from the server at once.

### Groups

- performance

### See Also

- [ListGrid.drawAheadRatio](#attr-listgriddrawaheadratio)
- [ListGrid.drawAllMaxCells](#attr-listgriddrawallmaxcells)

**Flags**: IRW

---
## Attr: ListGrid.canDragSelectText

### Description
If this property is true, users can drag the mouse to select text within grid rows, ready to be cliped to clipboard.  
This is mutually exclusive with [rearranging rows or cells by dragging](#attr-listgridcanreorderrecords), and with [drag selection of rows](#attr-listgridcandragselect).

To enable selecting cell text on click, see [ListGrid.selectCellTextOnClick](#attr-listgridselectcelltextonclick).

### Groups

- selection

**Flags**: IRW

---
## Attr: ListGrid.emptyMessage

### Description
The string to display in the body of a listGrid with an empty data array, if showEmptyMessage is true.

### Groups

- emptyMessage
- i18nMessages

### See Also

- [GridRenderer.showEmptyMessage](GridRenderer.md#attr-gridrenderershowemptymessage)
- [GridRenderer.emptyMessageStyle](GridRenderer.md#attr-gridrendereremptymessagestyle)

**Flags**: IRW

---
## Attr: ListGrid.headerRadius

### Description
When set to any valid CSS _border-radius_ string, allows for a rounded header in this grid by applying a corner-radius to the left of the [header](#attr-listgridheader), and to the right of the [corner sort-button](#attr-listgridshowsortarrow) if it's visible, or the right of the `header` otherwise. This styling is applied on top of the regular header styles, so will work with any design, and is also applied correctly with or without frozen fields.

**Flags**: IRW

---
## Attr: ListGrid.showHeaderPartialSelection

### Description
Should partial selection of all records be shown in header with a special icon? The partial icon will show in the header when [ListGrid.canSelectAll](#attr-listgridcanselectall) is enabled and at least one record is selected but all records are not selected. To only show all selected and none selected states, set this attribute to `false`.

### Groups

- selection

**Flags**: IRW

---
## Attr: ListGrid.filterOnKeypress

### Description
When this attribute is true and this component has been assigned a [searchForm](#attr-listgridsearchform) or is showing the [filterEditor](#attr-listgridshowfiltereditor), data will be filtered automatically as users change values in those components.

In the `filterEditor` case, this is equivalent to setting [FormItem.changeOnKeypress](FormItem.md#attr-formitemchangeonkeypress) to true for each text-based field in the [ListGridField.filterEditorProperties](ListGridField.md#attr-listgridfieldfiltereditorproperties) when [ListGrid.filterByCell](#attr-listgridfilterbycell) is true.

### Groups

- filterEditor

### See Also

- [ListGrid.fetchDelay](#attr-listgridfetchdelay)

**Flags**: IRW

---
## Attr: ListGrid.showHeaderSpanTitlesInHiliteEditor

### Description
If this grid has specified [ListGrid.headerSpans](#attr-listgridheaderspans), should field titles be prefixed with the titles of the headerSpans in which they are contained when using the [hilite editor](DataBoundComponent.md#method-databoundcomponentedithilites).

### See Also

- [ListGrid.hiliteEditorSpanTitleSeparator](#attr-listgridhiliteeditorspantitleseparator)

**Flags**: IRW

---
## Attr: ListGrid.headerButtonConstructor

### Description
Widget class for this ListGrid's header buttons. If unset, constructor will be picked up directly from the standard [Toolbar](Toolbar.md#class-toolbar) button constructor.

### Groups

- gridHeader
- appearance

**Flags**: IR

---
## Attr: ListGrid.gridSummaryRecordProperty

### Description
If [ListGrid.showGridSummary](#attr-listgridshowgridsummary) is true, this attribute will be set to true on the record object representing the grid summary row.

**Flags**: IRW

---
## Attr: ListGrid.printAutoFit

### Description
Whether cell contents should wrap during printing. Equivalent to [Autofit](../reference_2.md#type-autofit), but specific to printed output.

### Groups

- printing

**Flags**: IRW

---
## Attr: ListGrid.useRowSpanStyling

### Description
Enables various styling behaviors that potentially make sense when [ListGrid.getRowSpan](ListGrid_2.md#method-listgridgetrowspan) has been overridden to introduce spanning cells, and spanning is largest on the left and smaller as cells go to the right. Specifically:

*   computes [banded styling](#attr-listgridalternaterecordstyles) based on the span of the cell in the left-most column
*   enables [cell-level selection](#attr-listgridcanselectcells), including [cell-level rollover](#attr-listgridusecellrollovers) styling
*   enables row-span-sensitive cell selection. See also [RowSpanSelectionMode](../reference.md#type-rowspanselectionmode) for available behaviors

Because this setting enables [ListGrid.canSelectCells](#attr-listgridcanselectcells), it is incompatible with any APIs that expect a record-oriented data model.

Because this setting only makes sense when row spanning decreases from the first column to the last, it has unspecified behavior with [ListGrid.canReorderFields](#attr-listgridcanreorderfields).

**Flags**: IR

---
## Attr: ListGrid.expansionFieldFalseImage

### Description
If [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) is set to `true`, this property determines the image to display in the expansion field for collapsed rows. If unset, the [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage) will be used.

### Groups

- expansionField

### See Also

- [ListGrid.expansionFieldTrueImage](#attr-listgridexpansionfieldtrueimage)
- [ListGrid.expansionFieldImageWidth](#attr-listgridexpansionfieldimagewidth)
- [ListGrid.expansionFieldImageHeight](#attr-listgridexpansionfieldimageheight)

**Flags**: IRWA

---
## Attr: ListGrid.rowSpanEditMode

### Description
If [ListGrid.allowRowSpanning](#attr-listgridallowrowspanning) is enabled, this property may be used to specify editing behavior for cells that span multiple rows.

**Flags**: IRWA

---
## Attr: ListGrid.showErrorIcons

### Description
If this grid is editable, and an edit has caused validation failure for some cell, should we show an icon to indicate validation failure?

### Groups

- errorIcon

**Flags**: IRW

---
## Attr: ListGrid.sortFieldDescendingText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, this attribute will be shown as the menu item title to sort a field in descending order.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.animateRollOver

### Description
If the [rollOverCanvas](#attr-listgridrollovercanvas) is enabled, setting this property to `true` ensures that when the `rollOverCanvas` is displayed it is animated into view via [Canvas.animateShow](Canvas.md#method-canvasanimateshow). Note that the animation effect may be customized via [Canvas.animateShowEffect](Canvas.md#attr-canvasanimateshoweffect), [Canvas.animateShowTime](Canvas.md#attr-canvasanimateshowtime) and [Canvas.animateShowAcceleration](Canvas.md#attr-canvasanimateshowacceleration) set in `rollOverCanvasProperties`.

### Groups

- rowEffects

**Flags**: IRWA

---
## Attr: ListGrid.saveByCell

### Description
Whether edits should be saved whenever the user moves between cells in the current edit row.

If unset, defaults to [this.editByCell](#attr-listgrideditbycell).

To avoid automatic saving entirely, set [ListGrid.autoSaveEdits](#attr-listgridautosaveedits):false.

### Groups

- editing

### See Also

- [ListGrid.editByCell](#attr-listgrideditbycell)

**Flags**: IRW

---
## Attr: ListGrid.filterWindowCriteria

### Description
Advanced filtering criteria, either [simple](../reference_2.md#type-criteria) or [advanced](../reference.md#object-advancedcriteria), that is combined with the [filter editor criteria](ListGrid_2.md#method-listgridgetfiltereditorcriteria) during filtering.

This criteria is normally configured via [advanced filtering dialog](#method-listgridshowfilterwindow) shown because of the [ListGrid.allowFilterWindow](#attr-listgridallowfilterwindow) option but can be assigned directly as well.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

**Flags**: IRW

---
## Attr: ListGrid.editPendingBaseStyle

### Description
A base name for the CSS class applied to cells containing pending (unsaved) edits  
As with the default 'baseStyle' property, this style will have "Dark", "Over", "Selected", or "Disabled" appended to it according to the state of the cell.

If this property is null (the default setting), cells with pending edits will pick up custom css text to be applied on top of the normal base style from `this.editPendingCSSText`.

### Groups

- appearance

### See Also

- [ListGrid.baseStyle](#attr-listgridbasestyle)

**Flags**: IRA

---
## Attr: ListGrid.showTreeColumnPicker

### Description
When [ListGrid.headerSpans](#attr-listgridheaderspans) are in use, whether to show a hierarchical column picker that includes both headerSpans and normal headers, with normal headers indented under headerSpans similarly to how a [TreeGrid](TreeGrid.md#class-treegrid) displays a Tree.

If `showTreeColumnPicker` is false, no column picker will be shown on the headerSpan itself, and the column picker for a clicked on a normal field header will include only normal fields.

### Groups

- headerSpan

**Flags**: IR

---
## Attr: ListGrid.loadingRowCountDisplayIcoHeight

### Description
Height for the [ListGrid.loadingRowCountDisplayIcon](#attr-listgridloadingrowcountdisplayicon)

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.headerHoverOpacity

### Description
This property may be set to customize the opacity for the hover shown on [ListGrid.headerHover](ListGrid_2.md#method-listgridheaderhover).

**Flags**: IRW

---
## Attr: ListGrid.printBooleanPartialImage

### Description
If set, the [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

If this, [ListGrid.printBooleanTrueImage](#attr-listgridprintbooleantrueimage) and [ListGrid.printBooleanFalseImage](#attr-listgridprintbooleanfalseimage) are unset, this will be set to the default [CheckboxItem.printPartialSelectedImage](CheckboxItem.md#attr-checkboxitemprintpartialselectedimage).

### Groups

- imageColumns
- printing

### See Also

- [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage)

**Flags**: IRWA

---
## Attr: ListGrid.checkboxFieldTrueImage

### Description
If [ListGrid.selectionAppearance](#attr-listgridselectionappearance) is set to `"checkbox"` this property determines the image to display in the checkbox field for a selected row. If unset, the [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage) will be used. Note that the special value "blank" means that no image will be shown.

### Groups

- checkboxField

### See Also

- [ListGrid.checkboxFieldFalseImage](#attr-listgridcheckboxfieldfalseimage)
- [ListGrid.checkboxFieldImageWidth](#attr-listgridcheckboxfieldimagewidth)
- [ListGrid.checkboxFieldImageHeight](#attr-listgridcheckboxfieldimageheight)
- [ListGrid.printCheckboxFieldTrueImage](#attr-listgridprintcheckboxfieldtrueimage)

**Flags**: IRWA

---
## Attr: ListGrid.headerButtonAriaState

### Description
Default [ARIA state](Canvas.md#attr-canvasariastate) for [header buttons](#attr-listgridshowheader). See [ListGrid.getHeaderButtonAriaState](ListGrid_2.md#method-listgridgetheaderbuttonariastate).

**Flags**: IRA

---
## Attr: ListGrid.groupIndentSize

### Description
Default number of pixels by which to indent subgroups relative to parent group.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)
- [ListGrid.getGroupNodeHTML](ListGrid_2.md#method-listgridgetgroupnodehtml)

**Flags**: IRW

---
## Attr: ListGrid.validateOnChange

### Description
If true, validation will be performed on each edited cell when each editor's "change" handler is fired.

### Groups

- gridValidation

### See Also

- [ListGridField.validateOnChange](ListGridField.md#attr-listgridfieldvalidateonchange)

**Flags**: IRW

---
## Attr: ListGrid.checkboxField

### Description
Returns the specially generated checkbox field used when [SelectionAppearance](../reference.md#type-selectionappearance) is "checkbox". Created via the [AutoChild](../reference.md#type-autochild) pattern so that `checkboxFieldDefaults` and `checkboxFieldProperties` are available for skinning purposes. Note that [ListGridField.shouldPrint](ListGridField.md#attr-listgridfieldshouldprint) is `false` for the checkboxField by default - if you want this column to show up in the grid's print view, use `checkboxFieldProperties` to set this property to true.

This field will render an icon to indicate the selected state of each row, which, when clicked will toggle the selection state. The icon src may be configured using [ListGrid.checkboxFieldTrueImage](#attr-listgridcheckboxfieldtrueimage) and [ListGrid.checkboxFieldFalseImage](#attr-listgridcheckboxfieldfalseimage), as well as [ListGrid.checkboxFieldImageWidth](#attr-listgridcheckboxfieldimagewidth) and [ListGrid.checkboxFieldImageHeight](#attr-listgridcheckboxfieldimageheight).

The checkboxField can be detected by calling [ListGrid.isCheckboxField](ListGrid_2.md#method-listgridischeckboxfield) on any ListGridField object.

### Groups

- checkboxField

**Flags**: IR

---
## Attr: ListGrid.screenReaderIncludeFieldTitles

### Description
Should column titles be read along with cell values when screen-readers are reading the content of a row? Only applies when screen-reader mode is enabled, and for ListGrids with [ariaRole:"list"](#attr-listgridariarole).

Has no effect if [ListGrid.showHeader](#attr-listgridshowheader) is false.

See the documentation for [ListGrid.screenReaderCellSeparator](#attr-listgridscreenreadercellseparator) for implementation details on how the header values, cell separators and row separators are picked up by screenreaders in this mode.

For more information on the ARIA attributes generated by ListGrids, see [ListGrid.ariaRole](#attr-listgridariarole).

### Groups

- accessibility

**Flags**: IRA

---
## Attr: ListGrid.autoSaveEdits

### Description
If this ListGrid is editable, should edits be saved out when the user finishes editing a row (or a cell if [ListGrid.saveByCell](#attr-listgridsavebycell) is true).

The default of `true` indicates that edits will be [automatically saved](#attr-listgridsavebycell) as the user navigates through the grid and/or ${isc.DocUtils.linkForRef('type:EnterKeyEditAction','hits \\'Enter\\'')} to end editing. See the [Grid Editing](../kb_topics/editing.md#kb-topic-grid-editing) overview for details.

Setting `autoSaveEdits` false creates a "mass update" / "mass delete" interaction where edits will be retained for all edited cells (across rows if appropriate) until [ListGrid.saveEdits](ListGrid_2.md#method-listgridsaveedits) is called to save a particular row, or [ListGrid.saveAllEdits](ListGrid_2.md#method-listgridsavealledits) is called to save all changes in a batch.

**Note:** when [listGrid grouping](#attr-listgridgroupbyfield) is enabled, or when working with hierarchical data in a [TreeGrid](TreeGrid.md#class-treegrid), users have the option to hide records from view by collapsing the parent folder or group. This, in conjunction with `autoSaveEdits` being set to `false` can lead to a case where a user is unable to save edits due to validation errors on hidden rows. Therefore we recommend developers consider having validators in place such that errors are caught and displayed to the user on change or editor exit rather than being caught only when saving is attempted. If it's not possible for all validation to be performed immediately on row exit, we recommend that a different UI design be used that does not involve `autoSaveEdits` being set to `false`.

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.filterEditorHeight

### Description
Height for the filterEditor, if shown.

### Groups

- filterEditor

**Flags**: IRW

---
## Attr: ListGrid.aiHoverRetryDelay

### Description
Minimum number of milliseconds to wait before retrying to generate hover contents via AI.

The results of [SummarizeValueRequest](../reference_2.md#object-summarizevaluerequest)s generated from a field's [aiHoverRequest](ListGridField.md#attr-listgridfieldaihoverrequest) are cached, whether it was a successful or non-successful result. In the case of a non-successful result, the message therefrom will be displayed to the user for this configurable number of milliseconds before another request is made to try to generate the hover contents.

**Flags**: IRW

---
## Attr: ListGrid.screenReaderRowSeparator

### Description
Special row-separator that may be inserted at the end of the row value when screen-readers are reading the content of a row. Only applies when screen-reader mode is enabled, and for ListGrids with [ariaRole:"list"](#attr-listgridariarole).

See the documentation for [ListGrid.screenReaderCellSeparator](#attr-listgridscreenreadercellseparator) for details on how the header values, cell separators and row separators are picked up by screenreaders in this mode.

For more information on the ARIA attributes generated by ListGrids, see [ListGrid.ariaRole](#attr-listgridariarole).

### Groups

- accessibility

**Flags**: IRA

---
## Attr: ListGrid.animateRollUnder

### Description
If the [rollUnderCanvas](#attr-listgridrollundercanvas) is enabled, setting this property to `true` ensures that when the `rollUnderCanvas` is displayed it is animated into view via [Canvas.animateShow](Canvas.md#method-canvasanimateshow). Note that the animation effect may be customized via [Canvas.animateShowEffect](Canvas.md#attr-canvasanimateshoweffect), [Canvas.animateShowTime](Canvas.md#attr-canvasanimateshowtime) and [Canvas.animateShowAcceleration](Canvas.md#attr-canvasanimateshowacceleration) set in `rollUnderCanvasProperties`.

### Groups

- rowEffects

**Flags**: IRWA

---
## Attr: ListGrid.animateFolderTime

### Description
When animating folder opening / closing, if [TreeGrid.animateFolderSpeed](TreeGrid.md#attr-treegridanimatefolderspeed) is not set, this property designates the duration of the animation in ms.

For a ListGrid, this property applies when [grouping](#attr-listgridcangroupby) is enabled.

### Groups

- animation

### See Also

- [ListGrid.animateFolderSpeed](#attr-listgridanimatefolderspeed)

**Flags**: IRW

---
## Attr: ListGrid.validateByCell

### Description
Whether client-side validation checks should be performed when the user moves between cells in the current edit row. If unset, defaults to [ListGrid.editByCell](#attr-listgrideditbycell).

Note that validation always occurs when a row is to be saved, so setting [ListGrid.saveByCell](#attr-listgridsavebycell):true forces validation on cell transitions. To completely disable automatic validation, set [ListGrid.neverValidate](#attr-listgridnevervalidate):true.

### Groups

- gridValidation

### See Also

- [editing](../kb_topics/editing.md#kb-topic-grid-editing)

**Flags**: IRW

---
## Attr: ListGrid.defaultEditableDateFieldWidth

### Description
Default width for editable date type fields. See [ListGrid.autoFitDateFields](#attr-listgridautofitdatefields) for details on how this property is used.

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.selectedState

### Description
Returns a snapshot of the current selection within this listGrid as a [ListGridSelectedState](../reference_2.md#type-listgridselectedstate) object.  
This object can be passed to [ListGrid.setSelectedState](ListGrid_2.md#method-listgridsetselectedstate) to reset this grid's selection the current state (assuming the same data is present in the grid).

### Groups

- viewState

**Flags**: IRW

---
## Attr: ListGrid.rotateHeaderTitles

### Description
Whether to rotate the field titles so they're rendered vertically from bottom to top. Can be overridden for individual fields by setting [ListGridField.rotateTitle](ListGridField.md#attr-listgridfieldrotatetitle).

Note that you can manually set the header height and field widths as you please when using this feature, but it's not compatible with [ListGrid.autoFitHeaderHeights](#attr-listgridautofitheaderheights) or autofitting of field widths in any [AutoFitWidthApproach](../reference_2.md#type-autofitwidthapproach) other than "value".

You can use [ListGrid.headerTitleVAlign](#attr-listgridheadertitlevalign) or [ListGridField.valign](ListGridField.md#attr-listgridfieldvalign) to control vertical positioning of the titles, and [ListGridField.align](ListGridField.md#attr-listgridfieldalign) to control the horizontal. You may also choose between [clipping](#attr-listgridclipheadertitles) or [wrapping](#attr-listgridwrapheadertitles), and set [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) as you please (which reserves space in each header button for the header menu button).

Note that this feature is incompatible with clipping via [ListGrid.clipHeaderTitles](#attr-listgridclipheadertitles):false, and may not work with older browsers, particular IE versions before IE10. The "TreeFrog" and "Basic" [skins](../kb_topics/skins.md#kb-topic-skins) are not supported for this feature.

### See Also

- [ListGrid.headerTitleVAlign](#attr-listgridheadertitlevalign)
- [ListGridField.valign](ListGridField.md#attr-listgridfieldvalign)
- [ListGridField.rotateTitle](ListGridField.md#attr-listgridfieldrotatetitle)

**Flags**: IR

---
## Attr: ListGrid.headerShadowSoftness

### Description
If [ListGrid.showHeaderShadow](#attr-listgridshowheadershadow) is true, the [Canvas.shadowSoftness](Canvas.md#attr-canvasshadowsoftness) for the header shadow

**Flags**: IRA

---
## Attr: ListGrid.filterLocalData

### Description
Causes filtering to be performed against the local data set, even when a [ListGrid.dataSource](#attr-listgriddatasource) is provided.

When using this mode, data must be provided to the grid via [ListGrid.setData](ListGrid_2.md#method-listgridsetdata), and must be provided as a simple Array of Records .

Note that a [ListGrid.dataSource](#attr-listgriddatasource) must be provided for filtering to occur even when filtering locally.

If this property is set to true, the supplied data is applied as the [complete dataset](ResultSet.md#attr-resultsetallrows) of a [ResultSet](ResultSet.md#class-resultset), which is then filtered according to the specified criteria, and the results displayed. If false, a normal databound fetch will occur, retrieving records that match the specified criteria from this component's [ListGrid.dataSource](#attr-listgriddatasource).

`filterLocalData` includes both calls to [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata) and [ListGrid.filterData](ListGrid_2.md#method-listgridfilterdata) as well as automatic filtering when the [ListGrid.filterEditor](#attr-listgridfiltereditor) is enabled.

If this property is not explicitly set, default behavior will filter against the dataSource unless the grid has a specified [dataPath](../reference_2.md#type-datapath), in which case filtering will occur locally.

See also [ListGrid.saveLocally](#attr-listgridsavelocally) to cause saves to ignore the DataSource and affect the local data set only.

**Flags**: IRA

---
## Attr: ListGrid.showEmptyMessage

### Description
Indicates whether the text of the emptyMessage property should be displayed if no data is available.

### Groups

- emptyMessage

### See Also

- [ListGrid.emptyMessage](#attr-listgridemptymessage)

**Flags**: IRW

---
## Attr: ListGrid.selectOnExpandRecord

### Description
When set to false, clicking a record's [expansion field](#attr-listgridexpansionfield) will not add the record to the current selection.

**Flags**: IRW

---
## Attr: ListGrid.showHoverComponents

### Description
When set to true and canHover is also true, shows a widget hovering at the mouse point.

A number of builtin modes are provided - see [ListGrid.hoverMode](#attr-listgridhovermode). Note, if a `hoverMode` is set but `showHoverComponents` is left null, it will default to true.

Also supported at the [field-level](ListGridField.md#attr-listgridfieldshowhovercomponents).

### Groups

- hoverComponents

**Flags**: IRW

---
## Attr: ListGrid.checkboxFieldFalseImage

### Description
If [ListGrid.selectionAppearance](#attr-listgridselectionappearance) is set to `"checkbox"` this property determines the image to display in the checkbox field for an unselected row. If unset, the [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage) will be used. Note that the special value "blank" means that no image will be shown.

### Groups

- checkboxField

### See Also

- [ListGrid.checkboxFieldTrueImage](#attr-listgridcheckboxfieldtrueimage)
- [ListGrid.checkboxFieldImageWidth](#attr-listgridcheckboxfieldimagewidth)
- [ListGrid.checkboxFieldImageHeight](#attr-listgridcheckboxfieldimageheight)
- [ListGrid.printCheckboxFieldFalseImage](#attr-listgridprintcheckboxfieldfalseimage)

**Flags**: IRWA

---
## Attr: ListGrid.instantScrollTrackRedraw

### Description
If true, if the user clicks on the scroll buttons at the end of the track or clicks once on the scroll track, there will be an instant redraw of the grid content so that the user doesn't see any blank space. For drag scrolling or other types of scrolling, the [ListGrid.scrollRedrawDelay](#attr-listgridscrollredrawdelay) applies.

### Groups

- performance

**Flags**: IRW

---
## Attr: ListGrid.bodyBackgroundColor

### Description
Background color applied to the ListGrid body (that is, the area of the grid where data values are rendered).  
Note that this will typically not be visible to the user unless there are few enough rows that there is visible space in the body below the last row. To style data cells, override [ListGrid.baseStyle](#attr-listgridbasestyle) instead.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.advancedFieldPickerThreshold

### Description
When [ListGrid.useAdvancedFieldPicker](#attr-listgriduseadvancedfieldpicker) is set, total number of available fields that must be present in the grid before the advanced field picker interface is used instead of the normal columns submenu.

Set to 0 to have the advanced picker always used (when useAdvancedFieldPicker is true).

**Flags**: IR

---
## Attr: ListGrid.pendingAsyncCellValue

### Description
The value to display for cells whose value is pending asynchronous computation.

This is the grid-wide setting. [ListGridField.pendingAsyncCellValue](ListGridField.md#attr-listgridfieldpendingasynccellvalue) can override the grid setting for a specific field.

### See Also

- [DataBoundComponent.isValuePendingAsync](DataBoundComponent.md#method-databoundcomponentisvaluependingasync)

**Flags**: IRW

---
## Attr: ListGrid.loadingRowCountDisplayIconWidth

### Description
Width for the [ListGrid.loadingRowCountDisplayIcon](#attr-listgridloadingrowcountdisplayicon)

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.summaryRowStyle

### Description
[ListGrid.baseStyle](#attr-listgridbasestyle) for the [ListGrid.summaryRow](#attr-listgridsummaryrow)

**Flags**: IRWA

---
## Attr: ListGrid.defaultDateFieldWidth

### Description
Default width for date type fields. See [ListGrid.autoFitDateFields](#attr-listgridautofitdatefields) for details on how this property is used.

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.recordCellRoleProperty

### Description
If this property is set on a record it will designate the WAI ARIA role for cells within this records row

**Flags**: IRWA

---
## Attr: ListGrid.advancedFilteringText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, and a [filter-editor](#attr-listgridshowfiltereditor) is visible and [allowFilterWindow](#attr-listgridallowfilterwindow) is enabled, this attribute will be shown as the menu item title to configure advanced filtering. This menu-item is displayed in the context menu for the sorter button and in the [filter using](#attr-listgridallowfilteroperators) operators menu.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.rotatedHeaderMenuButtonWidth

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, this property governs the width of the auto-generated `headerMenuButton` over a [rotated](ListGridField.md#attr-listgridfieldrotatetitle) header button.

### Groups

- headerMenuButton

### See Also

- [ListGrid.headerMenuButtonWidth](#attr-listgridheadermenubuttonwidth)

**Flags**: IRA

---
## Attr: ListGrid.longTextEditorThreshold

### Description
When the length of the field specified by [DataSourceField.length](DataSourceField.md#attr-datasourcefieldlength) exceeds this value, the ListGrid shows an edit field of type [ListGrid.longTextEditorType](#attr-listgridlongtexteditortype) rather than the standard text field when the field enters inline edit mode.

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.saveRequestProperties

### Description
For editable grids with a specified [ListGrid.dataSource](#attr-listgriddatasource), where [ListGrid.saveLocally](#attr-listgridsavelocally) is false, this attribute may be used to specify standard DSRequest properties to apply to all save operations performed by this grid (whether triggered by user interaction, or explicit saveEdits or saveAllEdits call).

An example usage would be to customize the prompt displayed while saving is in progress if [ListGrid.waitForSave](#attr-listgridwaitforsave) is true.

Note that for more advanced customization of save operations, [DataBoundComponent.addOperation](DataBoundComponent.md#attr-databoundcomponentaddoperation) and [DataBoundComponent.updateOperation](DataBoundComponent.md#attr-databoundcomponentupdateoperation) are available to developers, allowing specification of an explicit [OperationBinding](OperationBinding.md#class-operationbinding) for the add / update operation performed on save.

### Groups

- databinding
- editing

**Flags**: IRWA

---
## Attr: ListGrid.aiFilterWindow

### Description
Instance of [AIWindow](../reference.md#class-aiwindow) that allows a user to enter a description of how they would like the AI to filter this grid.

**Flags**: IR

---
## Attr: ListGrid.dragHandleIconSize

### Description
Default width and height of [drag handle icons](#attr-listgriddraghandleicon) for this ListGrid.

### Groups

- dragHandleField

### See Also

- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)

**Flags**: IRW

---
## Attr: ListGrid.normalCellHeight

### Description
If [ListGrid.baseStyle](#attr-listgridbasestyle) is unset, base style will be derived from [ListGrid.normalBaseStyle](#attr-listgridnormalbasestyle) if this grid has fixed row heights and the specified [ListGrid.cellHeight](#attr-listgridcellheight) matches this value. Otherwise [ListGrid.tallBaseStyle](#attr-listgridtallbasestyle) will be used.

**Flags**: IRWA

---
## Attr: ListGrid.summaryRow

### Description
Automatically generated ListGrid for displaying grid summary information (see [ListGrid.showGridSummary](#attr-listgridshowgridsummary)).

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `listGrid.summaryRowProperties` and `listGrid.summaryRowDefaults`.

**Flags**: RA

---
## Attr: ListGrid.showPartialSelection

### Description
Should partially selected parents (in a Tree data set) be shown with special icon? This has an impact in grouped grids where [ListGrid.canSelectGroups](#attr-listgridcanselectgroups) is true. The partial icon will show up for the group header node when a group is partially selected.

### Groups

- selection

**Flags**: IRW

---
## Attr: ListGrid.canHiliteViaAI

### Description
When set to `true` and AI component views are enabled, shows an item in this component's header context menu that allows the user to ask the AI to hilite the records according to a natural language description of which records to hilite.

See [integratingAI](../kb_topics/integratingAI.md#kb-topic-integrating-ai-technology) for the requirements to enable AI component views.

### See Also

- [ListGrid.hiliteViaAIMode](#attr-listgridhiliteviaaimode)

**Flags**: IRW

---
## Attr: ListGrid.expansionField

### Description
The field providing the facility to expand and collapse rows.

### Groups

- expansionField

**Flags**: IRWA

---
## Attr: ListGrid.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: ListGrid.approximateRowCountFormat

### Description
Format for the string returned from [ListGrid.getFormattedRowCount](ListGrid_2.md#method-listgridgetformattedrowcount) when [row count status](ListGrid_2.md#method-listgridgetrowcountstatus) is `"approximate"`.

The variable `rowCount` is available for evaluation within this string and will be set to the [current row count](ListGrid_2.md#method-listgridgetrowcount) as a [locale-formatted number](NumberUtil.md#classmethod-numberutiltolocalizedstring).

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.sortState

### Description
Initial sort state for the grid.

[ListGrid.viewState](#attr-listgridviewstate) can be used to initialize all view properties of the grid. When doing so, `sortState` is not needed because `viewState` includes it as well. If both are provided, `sortState` has priority for sort state.

To retrieve current state call [getSortState](ListGrid_2.md#method-listgridgetsortstate).

### Groups

- viewState

**Flags**: IRW

---
## Attr: ListGrid.autoFetchTextMatchStyle

### Description
When this grid is initially filtered via [ListGrid.autoFetchData](#attr-listgridautofetchdata), or filtered by the user via the [filterEditor](#attr-listgridshowfiltereditor), this attribute can be used to set the `textMatchStyle` on the dsRequest passed to `fetchData()`.

To use a mixture of textMatchStyles, set an appropriate [operator](FormItem.md#attr-formitemoperator) on a field's [filterEditorProperties](ListGridField.md#attr-listgridfieldfiltereditorproperties).

### Groups

- databinding

**Flags**: IR

---
## Attr: ListGrid.emptyRowRangeDisplayValue

### Description
[Row range summary display value](ListGrid_2.md#method-listgridgetrowrangedisplayvalue) when the grid is empty.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.frozenHeaderBaseStyle

### Description
If this listGrid contains any frozen fields, this property can be used to apply a custom headerBaseStyle to the frozen set of fields. If unset, the standard headerBaseStyle will be used for both frozen and unfrozen cells.

### Groups

- gridHeader
- appearance
- frozenFields

### See Also

- [ListGrid.headerBaseStyle](#attr-listgridheaderbasestyle)
- [ListGridField.frozen](ListGridField.md#attr-listgridfieldfrozen)

**Flags**: IR

---
## Attr: ListGrid.saveCriteriaInViewState

### Description
Should the current [filter-criteria](ListGrid_2.md#method-listgridgetfiltereditorcriteria) be included along with other details when saving this grid's [view-state](#attr-listgridviewstate)?

If true, the current criteria will be saved when calling [ListGrid.getViewState](ListGrid_2.md#method-listgridgetviewstate) and will be applied to the grid via a filter when calling [ListGrid.setViewState](ListGrid_2.md#method-listgridsetviewstate).

Notes

*   If this grid has never actually fetched data, criteria will not be included
*   If this flag is set to `false`, [ListGrid.setViewState](ListGrid_2.md#method-listgridsetviewstate) will not modify the grid's filter even if criteria were included when viewState was stored.

### Groups

- viewState

### See Also

- [ListGrid.getUserCriteriaState](ListGrid_2.md#method-listgridgetusercriteriastate)
- [ListGrid.setUserCriteriaState](ListGrid_2.md#method-listgridsetusercriteriastate)

**Flags**: IRW

---
## Attr: ListGrid.touchScrollRedrawDelay

### Description
While scrolling an incrementally rendered grid, using the inertial scrolling, time in milliseconds to wait before redrawing, after the last touchScroll by the user. If not specified [ListGrid.scrollRedrawDelay](#attr-listgridscrollredrawdelay) will be used as a default for both drag scrolling and touch scrolling.

Note that if specified, this value will typically be larger than [ListGrid.scrollRedrawDelay](#attr-listgridscrollredrawdelay).

See also [GridRenderer.instantScrollTrackRedraw](GridRenderer.md#attr-gridrendererinstantscrolltrackredraw) for cases where this delay is skipped.

### Groups

- performance

**Flags**: IRW

---
## Attr: ListGrid.arrowKeyEditAction

### Description
What to do when a user hits arrow key while editing a field?  
If not explicitly specified [ListGrid.getArrowKeyEditAction](ListGrid_2.md#method-listgridgetarrowkeyeditaction) will return an appropriate action depending on the field type.

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.printHeaderStyle

### Description
Style for header cells in printed output. Defaults to [ListGrid.headerBaseStyle](#attr-listgridheaderbasestyle) if null.

### Groups

- printing

**Flags**: IRW

---
## Attr: ListGrid.defaultFilterOperator

### Description
Default [filter operator](../reference.md#type-operatorid) to use for text-based fields in this grid's [filter editor](#attr-listgridfiltereditor), when producing [AdvancedCriteria](../reference.md#object-advancedcriteria). When [allowFilterExpressions](#attr-listgridallowfilterexpressions) or [allowFilterOperators](#attr-listgridallowfilteroperators) are enabled for the grid, the default is ["iContainsPattern"](DataSource.md#attr-datasourcetranslatepatternoperators). Otherwise, the default is "iContains".

Does not apply to special fields where exact match is obviously the right default setting, such as fields of type:"enum", or fields with a [valueMap](FormItem.md#attr-formitemvaluemap) or [optionDataSource](FormItem.md#attr-formitemoptiondatasource).

**Flags**: IR

---
## Attr: ListGrid.showInitialDragHandles

### Description
When set to true, shows the [drag handle field](#attr-listgriddraghandlefield) on initial draw.

### Groups

- dragHandleField

### See Also

- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)
- [ListGrid.hideDragHandles](ListGrid_2.md#method-listgridhidedraghandles)
- [ListGrid.dragHandleField](#attr-listgriddraghandlefield)

**Flags**: IRA

---
## Attr: ListGrid.cancelEditingConfirmationMessage

### Description
If this is an editable listGrid, and `this.confirmCancelEditing` is true this property is used as the message to display in the confirmation dismissal prompt.

### Groups

- editing
- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.checkboxFieldHSpace

### Description
How much horizontal space should the [checkbox field](ListGrid_2.md#method-listgridgetcheckboxfield) leave around the checkbox icon when [ListGrid.selectionAppearance](#attr-listgridselectionappearance) is set to `"checkbox"`?

The automatically generated checkbox field will be sized to the width of the checkbox icon (specified via [ListGrid.checkboxFieldImageWidth](#attr-listgridcheckboxfieldimagewidth) or [ListGrid.booleanImageWidth](#attr-listgridbooleanimagewidth)) plus this value.

### Groups

- checkboxField

**Flags**: IR

---
## Attr: ListGrid.canFocusInEmptyGrid

### Description
If the listGrid is empty, should the user be able to put focus into the grid body by tabbing to it?

Note that if [ListGrid.editOnFocus](#attr-listgrideditonfocus) is true for this grid and [ListGrid.listEndEditAction](#attr-listgridlistendeditaction) is set to next, having this property set to true will allow users to automatically create a new edit row by simply tabbing into the grid.

**Flags**: IRA

---
## Attr: ListGrid.filterWindow

### Description
Instance of [Window](Window.md#class-window) used to [show](#method-listgridshowfilterwindow) the [FilterBuilder](#attr-listgridfilterwindowfilter).

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

By default the `FilterBuilder` shows with the top operator selection as a radio group and allows switching between simple and advanced modes. These defaults can be changed using [autoChild](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) features such as setting [filterWindowFilter](#attr-listgridfilterwindowfilter) properties on a grid instance or globally by changing the `ListGrid` defaults.

For example, in JavaScript, to always use advanced mode on a single grid:

```
 var grid = isc.ListGrid.create({
     ...
     filterWindowFilterProperties: {
         topOperatorAppearance: "bracket",
         showModeSwitcher: false
     }
 });
 
```
or to always use advanced mode:
```
 isc.ListGrid.changeDefaults("filterWindowFilter", {
     topOperatorAppearance: "bracket",
     showModeSwitcher: false
 });
 
```

**Flags**: IR

---
## Attr: ListGrid.showFilterEditorHovers

### Description
When set to false, no hover is shown for the filter editor fields. Otherwise, a hover shows the current field's criteria description along with the [ListGrid.filterWindowCriteria](#attr-listgridfilterwindowcriteria) description if configured.

Hovers can also be disabled for individual fields using [ListGridField.showFilterEditorHovers](ListGridField.md#attr-listgridfieldshowfiltereditorhovers).

The descriptive text for criteria is formatted by [DataSource.getAdvancedCriteriaDescription](DataSource.md#classmethod-datasourcegetadvancedcriteriadescription).

### See Also

- [ListGridField.showFilterEditorHovers](ListGridField.md#attr-listgridfieldshowfiltereditorhovers)

**Flags**: IR

---
## Attr: ListGrid.autoFitAllText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, and [ListGrid.canAutoFitFields](#attr-listgridcanautofitfields) is true, this attribute will be shown as the menu item title for an item to perform a one-time autoFit of all visible fields via the [ListGrid.autoFitField](ListGrid_2.md#method-listgridautofitfield) method.

### Groups

- i18nMessages
- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.originalData

### Description
When grouped, a copy of the original ungrouped data.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: R

---
## Attr: ListGrid.recordRadius

### Description
When set to any valid CSS _border-radius_ string, allows for rounded records in this grid by having [ListGrid.getCellCSSText](ListGrid_2.md#method-listgridgetcellcsstext) apply a corner-radius to the first and last cells in each record. This styling is applied on top of the regular cell styles, so will work with any design, and is also applied correctly with or without frozen fields.

If you need to apply more than just a radius to the ends of each record, you can set [ListGrid.styledRowEnds](#attr-listgridstyledrowends) to true and provide [ListGrid.firstCellStyle](#attr-listgridfirstcellstyle) and [ListGrid.lastCellStyle](#attr-listgridlastcellstyle) classes that achieve the design you need. Note that these two classes should not modify settings which may affect sizing, such as padding or font-sizes.

Note that you can also provide your own implementation of [ListGrid.getCellCSSText](ListGrid_2.md#method-listgridgetcellcsstext) or [ListGrid.getCellStyle](ListGrid_2.md#method-listgridgetcellstyle), if you want to do something more complex, like a gradient fade that spans the end two cells on each side of a record.

**Flags**: IRW

---
## Attr: ListGrid.aiHiliteWindow

### Description
Instance of [AIWindow](../reference.md#class-aiwindow) that allows a user to enter a description of how they would like the AI to filter this grid.

### Groups

- ai

**Flags**: IR

---
## Attr: ListGrid.fetchRequestProperties

### Description
If [ListGrid.autoFetchData](#attr-listgridautofetchdata) is `true`, this attribute allows the developer to declaratively specify [DSRequest](../reference.md#object-dsrequest) properties for the initial [fetchData()](ListGrid_2.md#method-listgridfetchdata) call.

Note that any properties governing more specific request attributes for the initial fetch (such as [ListGrid.autoFetchTextMatchStyle](#attr-listgridautofetchtextmatchstyle) and initial sort specifiers) will be applied on top of this properties block.

### Groups

- databinding

**Flags**: IR

---
## Attr: ListGrid.alternateRecordSuffix

### Description
Suffix to append to [alternate rows](GridRenderer.md#attr-gridrendereralternaterowstyles). Note that if [GridRenderer.alternateColumnStyles](GridRenderer.md#attr-gridrendereralternatecolumnstyles) is enabled, cells which fall into both an alternate row and column will have both suffixes appended - for example `"cellDarkAltCol"`.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: ListGrid.showRollOverInExpansion

### Description
This setting causes the [roll over canvas](#attr-listgridrollovercanvas) to be sized to cover the normal row and the expansion layout. Otherwise the rollOverCanvas is only shown for the un-expanded part of the row.

### Groups

- rowEffects

**Flags**: IRWA

---
## Attr: ListGrid.headerShadowColor

### Description
If [ListGrid.showHeaderShadow](#attr-listgridshowheadershadow) is true, the [Canvas.shadowColor](Canvas.md#attr-canvasshadowcolor) for the header shadow.

**Flags**: IRA

---
## Attr: ListGrid.warnOnRemoval

### Description
If [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) is true, when the user clicks the remove icon for some record, should we show a warning message (defined as [ListGrid.warnOnRemovalMessage](#attr-listgridwarnonremovalmessage)) and allow the user to cancel removal?

**Flags**: IRW

---
## Attr: ListGrid.removedCSSText

### Description
Custom CSS text to be applied to records that have been [marked for removal](ListGrid_2.md#method-listgridmarkrecordremoved).

This CSS text will be applied on top of standard disabled styling for the cell.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: ListGrid.recordSummaryBaseStyle

### Description
If showing any record summary fields (IE: fields of [type:"summary"](../reference.md#type-listgridfieldtype)), this attribute specifies a custom base style to apply to cells in the summary field

**Flags**: IRWA

---
## Attr: ListGrid.preserveFocusStylingOnMouseOut

### Description
If [ListGrid.showRollOver](#attr-listgridshowrollover) or [ListGrid.hiliteRowOnFocus](#attr-listgridhiliterowonfocus) is true the current keyboard focus row for navigation via arrow keys, etc, will be hilighted with `"Over"` styling. This is particularly valuable to indicate which row has keyboard focus where there are multiple selected rows, or where the user is navigating without changing selection (see [ListGrid.arrowKeyAction](#attr-listgridarrowkeyaction)).  
However, note that as the user interacts with the rows using the mouse, the rollover styling will be updated to reflect the mouse position if [ListGrid.showRollOver](#attr-listgridshowrollover) is true.

When the user rolls the mouse off the grid, the default behavior is to re-style the current focus row with `"Over"` styling if the grid has keyboard focus. That way a user has a clear visual indication of where navigation would start. This may be disabled by setting `preserveFocusStylingOnMouseOut` to false.

**Flags**: IRWA

---
## Attr: ListGrid.ungroupText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, and [this.isGrouped](#attr-listgridisgrouped) is true, this attribute will be shown as the title for the menu item to ungroup the grid.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.showSortArrow

### Description
Indicates whether a sorting arrow should appear for the listGrid, and its location. See [SortArrow](../reference_2.md#type-sortarrow) for details.

Clicking the sort arrow reverses the direction of sorting for the current sort column (if any), or sorts the listGrid by its first sortable column. The arrow image on the button indicates the current direction of sorting. If undefined, the sort arrow will show up in the sorted field, and the corner sort button will be displayed if a vertical scrollbar is being displayed

### Groups

- sorting
- appearance

**Flags**: IRW

---
## Attr: ListGrid.badFormulaResultValue

### Description
If the result of a formula evaluation is invalid (specifically, if isNaN(result)==true), badFormulaResultValue is displayed instead. The default value is ".".

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: ListGrid.dragHandleIcon

### Description
Default icon to show in the [drag handle field](#attr-listgriddraghandlefield)..

### Groups

- dragHandleField

### See Also

- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)

**Flags**: IR

---
## Attr: ListGrid.imageSize

### Description
Default size of thumbnails shown for fieldTypes image and imageFile. Overrideable on a per-field basis via [ListGridField.imageSize](ListGridField.md#attr-listgridfieldimagesize) or [ListGridField.imageWidth](ListGridField.md#attr-listgridfieldimagewidth)/[ListGridField.imageHeight](ListGridField.md#attr-listgridfieldimageheight)

### Groups

- imageColumns

**Flags**: IRW

---
## Attr: ListGrid.dataFetchDelay

### Description
Delay in milliseconds before fetching data.

Note: the floor value for this attribute is 1. If you set this value to zero, it will be defaulted to 1 for you instead.

### Groups

- databinding

### See Also

- [DataBoundComponent.dataFetchDelay](DataBoundComponent.md#attr-databoundcomponentdatafetchdelay)
- [ResultSet.fetchDelay](ResultSet.md#attr-resultsetfetchdelay)

**Flags**: IRWA

---
## Attr: ListGrid.warnOnUnmappedValueFieldChange

### Description
If a field has [ListGridField.displayField](ListGridField.md#attr-listgridfielddisplayfield) specified and has no [ListGridField.optionDataSource](ListGridField.md#attr-listgridfieldoptiondatasource), this field will display the value from the `displayField` of each record by default (for more on this behavior see [ListGridField.optionDataSource](ListGridField.md#attr-listgridfieldoptiondatasource)).

If such a field is editable, changing the edit value for the field on some record, without updating the edit value for the associated display field on the same record would mean the user would continue to see the unchanged display field value. Developers can resolve this situation by programmatically setting an edit value for the display field as well as the data field, or avoid it by specifying an optionDataSource and ensuring [ListGrid.autoFetchDisplayMap](#attr-listgridautofetchdisplaymap) is true, or setting an explicit valueMap for the field.

By default, when the edit value on a field with a specified displayField and no optionDataSource is set, we log a warning to notify the developer. This warning may be disabled by setting `warnOnUnmappedValueFieldChange` to `false`.

Note: There are actually a couple of cases in which the system will automatically derive a new display-field value and apply it to the record:

1.  If the edit value was changed by a user actually editing the record (rather than a programmatic call to setEditValue()), and the edit-item had a valueMap or optionDataSource set, we automatically pick up the display value from that item and store it as an edit-value for the displayField of the record
2.  If the listGrid has a loaded record in its data set whose valueField value matches the edit value for the valueField, we automatically apply the displayField value from that record as an edit value for the displayField on the newly edited record.

In either case, the display value for the record is updated automatically (and the warning would not be logged).

**Flags**: IRWA

---
## Attr: ListGrid.autoFitData

### Description
Should this ListGrid automatically expand to accommodate the size of records and fields?

Valid settings are

*   `"vertical"`: expand vertically to accommodate records.
*   `"horizontal"`: expand horizontally to accommodate fields.
*   `"both"`: expand horizontally and vertically to accommodate content.

How far the ListGrid will expand may be limited via the following properties: [ListGrid.autoFitMaxHeight](#attr-listgridautofitmaxheight), [ListGrid.autoFitMaxRecords](#attr-listgridautofitmaxrecords), [ListGrid.autoFitMaxWidth](#attr-listgridautofitmaxwidth), [ListGrid.autoFitMaxColumns](#attr-listgridautofitmaxcolumns).

Note that this property causes the grid as a whole to expand to fit records or fields. To have the fields or records themselves expand to fit cell contents, see [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths) and [ListGrid.fixedRecordHeights](#attr-listgridfixedrecordheights).

### Groups

- autoFitData

**Flags**: IRW

---
## Attr: ListGrid.autoFitFieldText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, and user-driven auto fit of fields is enabled via [ListGridField.canAutoFitWidth](ListGridField.md#attr-listgridfieldcanautofitwidth) or [ListGrid.canAutoFitFields](#attr-listgridcanautofitfields), this attribute will be shown as the menu item title for an item to perform a one-time autoFit of the field to its title or content via a call to [ListGrid.autoFitField](ListGrid_2.md#method-listgridautofitfield).

### Groups

- i18nMessages
- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.configureSortText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, and multi-sorting is enabled, this attribute is used as the title for a menu item that opens a [MultiSortDialog](MultiSortDialog.md#class-multisortdialog) to configure the sort-specification for this grid. This menu-item is displayed only in the context menu for the sorter button.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.sortAscendingImage

### Description
Image to show when sorted in ascending order. Can be either a regular [SCImgURL](../reference.md#type-scimgurl) src, or an [ImgHTMLProperties](../reference_2.md#object-imghtmlproperties) object.

### See Also

- [ListGrid.sortArrowMenuButtonSpaceOffset](#attr-listgridsortarrowmenubuttonspaceoffset)

**Flags**: IRWA

---
## Attr: ListGrid.loadingDataMessage

### Description
The string to display in the body of a listGrid while data is being loaded. Use `"${loadingImage}"` to include [a loading image](Canvas.md#classattr-canvasloadingimagesrc).

### Groups

- emptyMessage
- i18nMessages

### See Also

- [ListGrid.loadingDataMessageStyle](#attr-listgridloadingdatamessagestyle)

**Flags**: IRW

---
## Attr: ListGrid.groupIconStyle

### Description
Custom style to apply to the [ListGrid.groupIcon](#attr-listgridgroupicon) displayed in collapsible rows when [ListGrid.canGroupBy](#attr-listgridcangroupby) is true.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.autoPersistViewState

### Description
Setting this property to a non-null value will enable automatic saving of [view state](ListGrid_2.md#method-listgridgetviewstate) to offline storage. This saved view state will then be restored automatically when the user visits the page again.

_**Note:** [SmartClient Pro users](http://www.smartclient.com/product), may also be interested in the [ListGrid.canSaveSearches](#attr-listgridcansavesearches) feature. This uses the [Saved Search subsystem](SavedSearches.md#class-savedsearches) to allow users to explicitly store and apply multiple named views or "saved searches". Each saved search includes the [full view state](#attr-listgridsavedsearchstoredstate) for the grid by default._

`autoPersistViewState` may be set to a list of [view state](../reference_2.md#type-listgridviewstate) [parts](../reference.md#type-listgridviewstatepart) that should be automatically persisted into offline storage when changed.

This feature saves the derived state whenever the grid's view state changes due to user interaction (see [ListGrid.viewStateChanged](ListGrid_2.md#method-listgridviewstatechanged)), and restores the saved state from offline storage when the grid is drawn.

The state is saved to offline storage using the grid's [locator](../reference_2.md#type-autotestlocator) as the key. See Locator details below.

Note that `autoPersistViewState` should only be set on specific listGrid instances, and never as a default value for the class by changing the ListGrid defaults. Enabling this feature as a default would be an invalid usage as it would apply to listgrids (and subclasses of ListGrid) created and re-used internally by framework features as well as those explicitly created by application code.

The current saved value can be retrieved or cleared by calling [ListGrid.getSavedViewState](ListGrid_2.md#method-listgridgetsavedviewstate) or [ListGrid.clearSavedViewState](ListGrid_2.md#method-listgridclearsavedviewstate) respectively.

**Locator details**

The grid must have a stable locator so that previous state can be retrieved during initial draw and saved back into the same place. If the grid has an explicit [ID](Canvas.md#attr-canvasid) the locator will always be stable. Setting an explicit ID on a known parent of the grid can also lead to a stable ID as described in the [Best Practices section of Using Selenium Scripts](../kb_topics/usingSelenium.md#kb-topic-using-selenium-scripts-selenese).

For purposes of this feature the top-level parent of the grid must have an explicit ID.

Additional details on locators and their use can be found in [AutoTest](AutoTest.md#class-autotest) and [LocatorStrategy](../reference_2.md#type-locatorstrategy).

### Groups

- viewState

### See Also

- [ListGrid.getSavedViewState](ListGrid_2.md#method-listgridgetsavedviewstate)
- [ListGrid.clearSavedViewState](ListGrid_2.md#method-listgridclearsavedviewstate)

**Flags**: IRW

---
## Attr: ListGrid.recordComponentHeight

### Description
If [ListGrid.showRecordComponents](#attr-listgridshowrecordcomponents) is true, this attribute may be used to specify a standard height for record components. If specified every row in the grid will be sized tall enough to accommodate a recordComponent of this size.

Note that if this property is unset, the grid will not be able to know row heights in advance, and [frozen fields](ListGridField.md#attr-listgridfieldfrozen) are not currently supported in this case. If you are putting a recordComponent in every row, and they all have a consistent height, set `recordComponentHeight` and you will then be able to use frozen fields _and_ avoid the whitespace side-effect of virtual scrolling by setting [ListGrid.virtualScrolling](#attr-listgridvirtualscrolling):false.

Similarly, if your recordComponents are never tall enough that they will expand the row beyond the [ListGrid.cellHeight](#attr-listgridcellheight), set [ListGrid.virtualScrolling](#attr-listgridvirtualscrolling):false to avoid the whitespace side-effect of [virtual scrolling](#attr-listgridvirtualscrolling) and to allow [frozen fields](ListGridField.md#attr-listgridfieldfrozen) to be used. In this mode, you can have recordComponents on some rows but not others, and recordComponents of different heights, so long as no recordComponent ever causes a row to grow beyond [ListGrid.cellHeight](#attr-listgridcellheight) (which would happen if the recordComponents height + 2\*[ListGrid.cellPadding](#attr-listgridcellpadding) is larger than [ListGrid.cellHeight](#attr-listgridcellheight)).

### Groups

- recordComponents

### See Also

- [ListGrid.virtualScrolling](#attr-listgridvirtualscrolling)

**Flags**: IRWA

---
## Attr: ListGrid.scrollRedrawDelay

### Description
While drag scrolling in an incrementally rendered grid, time in milliseconds to wait before redrawing, after the last mouse movement by the user. This delay may be separately customized for mouse-wheel scrolling via [ListGrid.scrollWheelRedrawDelay](#attr-listgridscrollwheelredrawdelay).

See also [GridRenderer.instantScrollTrackRedraw](GridRenderer.md#attr-gridrendererinstantscrolltrackredraw) for cases where this delay is skipped.

**NOTE:** In [touch browsers](Browser.md#classattr-browseristouch), [touchScrollRedrawDelay](GridRenderer.md#attr-gridrenderertouchscrollredrawdelay) is used instead.

### Groups

- performance

**Flags**: IRW

---
## Attr: ListGrid.saveDefaultSearch

### Description
Saves the name of the default search to localStorage, under the key "sc\_defaultSearch:" + minimal locator.

See [SavedSearches](SavedSearches.md#class-savedsearches) "Default Searches" for why this is stored separately from the search itself if there is no saved default search, but there is a [SavedSearches.defaultField](SavedSearches.md#attr-savedsearchesdefaultfield), the first user-specfic search marked default will be used, otherwise the first admn search marked default

If [ListGrid.autoFetchData](#attr-listgridautofetchdata) is enabled, the autoFetch will be postponed as needed until a default search can be looked up and applied. If anything fails in the default search lookup, an autoFetch will still be performed (without any saved search information)

**Flags**: IR

---
## Attr: ListGrid.filterEditorProperties

### Description
Properties to apply to the automatically generated [ListGrid.filterEditor](#attr-listgridfiltereditor) if [ListGrid.showFilterEditor](#attr-listgridshowfiltereditor) is true.

**Flags**: IR

---
## Attr: ListGrid.defaultFields

### Description
An array of listGrid field configuration objects. When a listGrid is initialized, if this property is set and there is no value for the `fields` attribute, this.fields will be defaulted to a generated array of field objects duplicated from this array.

This property is useful for cases where a standard set of fields will be displayed in multiple listGrids - for example a subclass of ListGrid intended to display a particular type of data:  
In this example we would not assign a single [ListGrid.fields](#attr-listgridfields) array directly to the class via `addProperties()` as every generated instance of this class would then point to the same fields array object. This would cause unexpected behavior such as changes to the field order in one grid affecting other grids on the page.  
Instead we could use `addProperties()` on our new subclass to set `defaultFields` to a standard array of fields to display. Each generated instance of the subclass would then show up with default fields duplicated from this array.

**Flags**: IRA

---
## Attr: ListGrid.expansionRelated

### Description
Automatically generated [ListGrid](#class-listgrid) for displaying data related to a record in its expanded section when [listGrid.expansionMode](../reference_2.md#type-expansionmode) is `related`. The [DataSource](DataSource.md#class-datasource) containing the related data is provided by [getRelatedDataSource()](ListGrid_2.md#method-listgridgetrelateddatasource) which, by default, returns the DataSource referred to in [ListGridRecord.detailDS](ListGridRecord.md#attr-listgridrecorddetailds).

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `listGrid.expansionRelatedProperties` and `listGrid.expansionRelatedDefaults`.

Note, however, that this is a multi-instance component (potentially one per record), so it is created using [createAutoChild()](Class.md#method-classcreateautochild) not [addAutoChild()](Class.md#method-classaddautochild), and no default single instance is created by name on the grid.

### Groups

- expansionField

**Flags**: RA

---
## Attr: ListGrid.skinImgDir

### Description
Where do 'skin' images (those provided with the class) live?

### Groups

- appearance
- images

**Flags**: IRWA

---
## Attr: ListGrid.aiFilterWindowTitle

### Description
The title for the [AI-driven filter window](#attr-listgridaifilterwindow).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.maximumRowCountFormat

### Description
Format for the string returned from [ListGrid.getFormattedRowCount](ListGrid_2.md#method-listgridgetformattedrowcount) when [row count status](ListGrid_2.md#method-listgridgetrowcountstatus) is `"maximum"`.

The variable `rowCount` is available for evaluation within this string and will be set to the [current row count](ListGrid_2.md#method-listgridgetrowcount) as a [locale-formatted number](NumberUtil.md#classmethod-numberutiltolocalizedstring).

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.expansionEditor

### Description
Automatically generated [DynamicForm](DynamicForm.md#class-dynamicform) for editing the details of a record in its expanded section when [listGrid.expansionMode](../reference_2.md#type-expansionmode) is `editor`. Note that only those fields which do not already appear in the grid will appear in the expanded section.

According to the value of [ListGrid.showExpansionEditorSaveButton](#attr-listgridshowexpansioneditorsavebutton), a save button is shown beneath the editor. You can save the values in the editor by clicking this button

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `listGrid.expansionEditorProperties` and `listGrid.expansionEditorDefaults`.

Note, however, that this is a multi-instance component (potentially one per record), so it is created using [createAutoChild()](Class.md#method-classcreateautochild) not [addAutoChild()](Class.md#method-classaddautochild), and no default single instance is created by name on the grid.

### Groups

- expansionField

**Flags**: RA

---
## Attr: ListGrid.hideEmptySummaryRow

### Description
If true, causes the [summaryRow](#attr-listgridsummaryrow) component to be hidden if it has no data after summaries have been recalculated

**Flags**: IRW

---
## Attr: ListGrid.trackerImage

### Description
Default image to use for the dragTracker when things are dragged within or out of this list. Can be either a regular [SCImgURL](../reference.md#type-scimgurl) src, or an [ImgHTMLProperties](../reference_2.md#object-imghtmlproperties) object.

### Groups

- dragTracker

### See Also

- [ListGrid.dragTrackerMode](#attr-listgriddragtrackermode)
- [ListGrid.getDragTrackerIcon](ListGrid_2.md#method-listgridgetdragtrackericon)

**Flags**: IRWA

---
## Attr: ListGrid.canDragSelect

### Description
If this property is true, users can drag the mouse to select several rows or cells. This is mutually exclusive with rearranging rows or cells by dragging.

**NOTE:** If `canDragSelect` is initially enabled or might be dynamically enabled after the grid is created, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging records/cells selects them rather than starting a scroll. If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag-selection.

### Groups

- selection

**Flags**: IRW

---
## Attr: ListGrid.headerHoverWidth

### Description
Optional default width for the hover shown on [ListGrid.headerHover](ListGrid_2.md#method-listgridheaderhover).

**Flags**: IRW

---
## Attr: ListGrid.loadingRowCountDisplayIcon

### Description
The URL of the icon to display as a [row count value](ListGrid_2.md#method-listgridgetformattedrowcount) when the row count is loading.

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.hiliteIconRightPadding

### Description
How much padding should there be on the right of [hilite icons](#attr-listgridhiliteicons) by default? Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: ListGrid.groupSummaryStyle

### Description
[ListGridRecord.customStyle](ListGridRecord.md#attr-listgridrecordcustomstyle) for the group-level summary row displayed when [ListGrid.showGroupSummary](#attr-listgridshowgroupsummary) is true.

**Flags**: IR

---
## Attr: ListGrid.cellHeight

### Description
Default height for each row in pixels. See [ListGrid.fixedRecordHeights](#attr-listgridfixedrecordheights) and [ListGrid.enforceVClipping](#attr-listgridenforcevclipping) for information on how rows are sized when cell content height exceeds this specified value.

**Flags**: IRW

---
## Attr: ListGrid.embeddedComponentIndent

### Description
This is the pixel-amount by which child components are offset within the grid-body, by default from the left, or from the right when [RTL](Page.md#classmethod-pageisrtl) is in effect. For [expanding rows](#attr-listgridcanexpandrecords), this attribute is overridden by [ListGrid.expansionIndent](#attr-listgridexpansionindent).

This setting overrides the [general margin](#attr-listgridembeddedcomponentmargin) for embedded-components, on the appropriate side.

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.discardEditsSaveButtonTitle

### Description
If [ListGrid.confirmDiscardEdits](#attr-listgridconfirmdiscardedits) is true this is the title for the save button appearing in the lost edits confirmation dialog. Override this for localization if necessary.

### Groups

- editing
- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.iconPadding

### Description
When using [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths), padding in pixels left on each side of fields that show images.

**Flags**: IR

---
## Attr: ListGrid.canGroupBy

### Description
If false, grouping via context menu will be disabled.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IRW

---
## Attr: ListGrid.asyncErrorCellValue

### Description
The value to display for cells when an error occurred during asynchronous computation.

This is the grid-wide setting. [ListGridField.asyncErrorCellValue](ListGridField.md#attr-listgridfieldasyncerrorcellvalue) can override the grid setting for a specific field.

### Groups

- i18nMessages

### See Also

- [DataBoundComponent.isValuePendingAsyncOrAsyncError](DataBoundComponent.md#method-databoundcomponentisvaluependingasyncorasyncerror)

**Flags**: IRW

---
## Attr: ListGrid.dragDataAction

### Description
Indicates what to do with data dragged into another DataBoundComponent. See DragDataAction type for details.

### Groups

- dragging

**Flags**: IRW

---
## Attr: ListGrid.maxSummaryRowRecords

### Description
If [ListGrid.showGridSummary](#attr-listgridshowgridsummary) is true, and summary records are being derived from a fetch against the [ListGrid.summaryRowDataSource](#attr-listgridsummaryrowdatasource), this property may be set to specify the maximum expected number of results from the fetch opeeration. If specified, the [DSRequest.startRow](DSRequest.md#attr-dsrequeststartrow) for the summary row fetch operation will be zero and the [DSRequest.endRow](DSRequest.md#attr-dsrequestendrow) will be this value.

This property has no effect unless summary row records are being retrieved from the [ListGrid.summaryRowDataSource](#attr-listgridsummaryrowdatasource).

**Flags**: IRA

---
## Attr: ListGrid.asyncMissingCellValue

### Description
The value to display for cells whose value was not computed by the previous asynchronous operation to compute it, or will not be computed by an asynchronous operation due to currently being disabled. For example, the previous asynchronous operation may have been canceled, or the grid may be displaying too many values to compute AI-generated values for a field.

This is the grid-wide setting. [ListGridField.asyncMissingCellValue](ListGridField.md#attr-listgridfieldasyncmissingcellvalue) can override the grid setting for a specific field.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.errorIconSrc

### Description
Src of the image to show as an error icon, if we're showing icons when validation errors occur.

### Groups

- errorIcon

**Flags**: IRW

---
## Attr: ListGrid.maxExpandedRecordsPrompt

### Description
This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed. Note that the local variable `count` will be available and set to this.maxExpandedRecords. The string will be executed in the scope of the ListGrid so `this` may also be used to determine other information about this grid.

Default value returns

``_This grid is limited to `[[ListGrid.maxExpandedRecords](#attr-listgridmaxexpandedrecords)]` simultaneously expanded records. Please collapse some expanded records and retry._``

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.clearCriteriaOnFilterEditorHide

### Description
When set to false, this attribute prevents user-criteria in the [filterEditor](#attr-listgridfiltereditor) from being cleared when the user hides it.

### Groups

- filterEditor

**Flags**: IR

---
## Attr: ListGrid.animateRemoveRecord

### Description
When [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) is enabled, should records be animated out of view when they are removed by the user?

**Flags**: IRW

---
## Attr: ListGrid.navigateOnTab

### Description
If [ListGrid.canSelectCells](#attr-listgridcanselectcells) is true, this property allows the user to navigate through the cells of a grid using Tab and Shift+Tab keypresses. When a user tabs to the end of the row, the [ListGrid.rowEndEditAction](#attr-listgridrowendeditaction) is used to determine whether to shift selection to the next row, return to the beginning of the same row, or simply move on through the page's tab order.

Note - if this property is not explicitly set, navigateOnTab behavior will be enabled for grids unless [screenReader mode is on](isc.md#staticmethod-iscsetscreenreadermode) in which case it will be disabled.  
Developers should be aware that setting `navigateOnTab` explicitly to true enabled the behavior even in screenReader mode. This may have an impact on the accessibility of an application - screen reader mode users navigating the application via the keyboard would have to tab through every single data cell in the grid grid before being able to tab to the next component.

**Flags**: IRW

---
## Attr: ListGrid.summaryRowFetchRequestProperties

### Description
If [ListGrid.showGridSummary](#attr-listgridshowgridsummary) is true, and a [ListGrid.summaryRowDataSource](#attr-listgridsummaryrowdatasource) is specified this property may be used to customize the fetch request used when retrieving summary data to show in the summary row. An example use case might be specifying a [DSRequest.operationId](DSRequest.md#attr-dsrequestoperationid) to perform a custom fetch operation which retrieved only summary values based on criteria.

Note that [DSRequest.startRow](DSRequest.md#attr-dsrequeststartrow) and [DSRequest.endRow](DSRequest.md#attr-dsrequestendrow) will be configured to only request the first [ListGrid.maxSummaryRowRecords](#attr-listgridmaxsummaryrowrecords) matches if the criteria matches multiple records - though typically a properly configured summary fetch operation will only return a single record, or an expected fixed number of records if multiple row summary values per field are to be displayed.

### See Also

- [DSRequest.startRow](DSRequest.md#attr-dsrequeststartrow)
- [DSRequest.endRow](DSRequest.md#attr-dsrequestendrow)

**Flags**: IRWA

---
## Attr: ListGrid.showHover

### Description
If true, and [canHover](#attr-listgridcanhover) is also true, shows popup hover text next to the mouse when the user hovers over a cell. The content of the hover is determined by [cellHoverHTML()](ListGrid_2.md#method-listgridcellhoverhtml).

This is the default setting for the grid and can be overridden on a [per-field](ListGridField.md#attr-listgridfieldshowhover) basis.

### Groups

- hovers

### See Also

- [ListGrid.canHover](#attr-listgridcanhover)
- [ListGrid.cellHoverHTML](ListGrid_2.md#method-listgridcellhoverhtml)

**Flags**: IRW

---
## Attr: ListGrid.canCollapseGroup

### Description
Can a group be collapsed/expanded? When true a collapse/expand icon is shown ([groupIcon](#attr-listgridgroupicon)) and the user can collapse or expand the group by clicking either the row as a whole or the opener icon (see [ListGrid.collapseGroupOnRowClick](#attr-listgridcollapsegrouponrowclick)); When false the group icon is not shown and clicking on the row does not change group state. Additionally [groupStartOpen](../reference.md#type-groupstartopen) is initialized to "all".

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IR

---
## Attr: ListGrid.recordRowAriaStateProperty

### Description
If this property is set on a record it will designate a mapping of WAI ARIA attribute names and values for this record's row.

**Flags**: IRWA

---
## Attr: ListGrid.autoFitExpandField

### Description
The field to expand if [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths) and [ListGrid.autoFitFieldsFillViewport](#attr-listgridautofitfieldsfillviewport) are enabled and auto-fitting will not fill all available horizontal space.

If unset, will default to the text field with the longest [DataSourceField.length](DataSourceField.md#attr-datasourcefieldlength) if length is set, otherwise, the first text field with no width specified.

Note that expanding [frozen columns](ListGridField.md#attr-listgridfieldfrozen) is not supported.

### Groups

- autoFitFields

**Flags**: IR

---
## Attr: ListGrid.disabledGroupByPrompt

### Description
Prompt to indicate that grouping is disabled as the data set size exceeds [ListGrid.groupByMaxRecords](#attr-listgridgroupbymaxrecords).

This prompt will be shown as a hover for the disabled [group by menu item](#attr-listgridcangroupby).

See also [ListGrid.groupByMaxRecordsExceededMessage](#attr-listgridgroupbymaxrecordsexceededmessage).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.newRecordRowMessage

### Description
If this listGrid is showing the 'newRecordRow' (used for adding new rows to the end of the data), this property determines what message should be displayed in this row.

### Groups

- editing
- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.singleCellValueProperty

### Description
If `record[this.singleCellValueProperty]` is set for some record, the record will be displayed as a single cell spanning every column in the grid, with contents set to the value of `record[this.singleCellValueProperty]`.

**Flags**: IRW

---
## Attr: ListGrid.booleanImageWidth

### Description
Width for the [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage), [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage) and [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage). Note: If [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage) is unset, the [CheckboxItem.checkedImage](CheckboxItem.md#attr-checkboxitemcheckedimage) will be used to indicate a true value in a boolean field. In this case this property is ignored in favor of [CheckboxItem.valueIconWidth](CheckboxItem.md#attr-checkboxitemvalueiconwidth).

### Groups

- imageColumns

**Flags**: IRWA

---
## Attr: ListGrid.groupIconSize

### Description
Default width and height of group icons for this ListGrid.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IRW

---
## Attr: ListGrid.viewState

### Description
Initial view state may be provided for the listGrid at init time. To set view state at runtime, use [ListGrid.setViewState](ListGrid_2.md#method-listgridsetviewstate).  
See [ListGridViewState](../reference_2.md#type-listgridviewstate) for details of what is included in the viewState for a ListGrid by default.

View state is a composite object containing various more granular states such as [fieldState](../reference_2.md#type-fieldstate), [current filter criteria](#attr-listgridsavecriteriainviewstate), etc. As such it is not necessary to specificify fieldState, etc. in addition to viewState at init time, but if both are provided the specific states (`fieldState`, etc) will have priority.

To retrieve current state call [getViewState](ListGrid_2.md#method-listgridgetviewstate).

**Note:** For [SmartClient Pro users](http://www.smartclient.com/product), the [Saved Search subsystem](SavedSearches.md#class-savedsearches) provides a sophisticated, out of the box set of capabilities and user-interface components for users to store and apply multiple named views or "saved searches". See [ListGrid.canSaveSearches](#attr-listgridcansavesearches) for how to enable menu options to save searches in grids. Note that each saved search includes the [full view state](#attr-listgridsavedsearchstoredstate) for the grid by default.

### Groups

- viewState

**Flags**: IRW

---
## Attr: ListGrid.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: ListGrid.sortByGroupFirst

### Description
If set, whenever grouping is performed by an end user or by a programmatic call to [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby), data is implicitly sorted by all of the grouped columns, in the order they were passed to groupBy. Any user-configured sorting is applied after sorting by grouped columns.

Sorting by grouped fields will be in ascending or descending order according to whether the grid is currently sorted (by any field) in ascending or descending order, defaulting to ascending if the grid is not sorted. Implicit sorting by group can be forced to be always ascending or always descending by setting [ListGrid.groupSortDirection](#attr-listgridgroupsortdirection).

The sorting is "implicit" in the sense that the sorting is not shown in the ListGrid headers, and not shown in the [MultiSortDialog](MultiSortDialog.md#class-multisortdialog) if enabled. An end user cannot currently remove the implicit sorting themselves (except by removing the grouping), though it is possible to override it by providing an explicit sort on the group's column. Clicking on the grouped field's header reveals the usual sort indicators with all the same semantics.

The correct way to remove implicit sorting programmatically is to call [setSortByGroupFirst(false)](ListGrid_2.md#method-listgridsetsortbygroupfirst).

Programmatic calls to [ListGrid.getSort](ListGrid_2.md#method-listgridgetsort) will not include the implicit sort in the list of return sort specifiers, and calls to [ListGrid.setSort](ListGrid_2.md#method-listgridsetsort) will implicitly add the sorting by grouped columns before the specified sort.

Note that directly calling ResultSet.getSort() will include the implicit sort information.

### Groups

- sorting
- grouping

### See Also

- [ListGrid.groupSortDirection](#attr-listgridgroupsortdirection)
- [ListGrid.groupSortNormalizer](ListGrid_2.md#method-listgridgroupsortnormalizer)

**Flags**: IRW

---
## Attr: ListGrid.showRollOverCanvas

### Description
When enabled, when the mouse moves over a row or cell (depending on [ListGrid.useCellRollOvers](#attr-listgridusecellrollovers)), an arbitrary Canvas can be shown layered on top of the row or cell (the [ListGrid.rollOverCanvas](#attr-listgridrollovercanvas)), layered underneath the row or cell (the [ListGrid.rollUnderCanvas](#attr-listgridrollundercanvas)), or both.

This can be used to dynamically show controls or informational displays only on rollover. For example, controls to delete a row might appear only on rollover so they do not clutter the static display, or a "rollUnder" Canvas could be used to display additional information that can appear behind normal cell values (like displaying percent complete via as a bar of color that appears behind text values).

[snapTo positioning](Canvas.md#attr-canvassnapto) can be used to place the rollOver/rollUnderCanvas. With `useCellRollOvers`, positioning is relative to the cell, for row-level rollOver, position is relative to the portion of the row that is scrolled into view (this implies a row-level rollOver/UnderCanvas can never be placed horizontally scrolled out of view, but this is possible for a cell-level rollOver).

`snapTo` positioning makes it easy to do something like place a button at the right edge of the grid, next to the scrollbar: just set snapTo:"R" on the `rollOverCanvas`.

The rollOver/rollUnder Canvas can be a single static component (the same for all cells/rows) configured via the [AutoChild](../reference.md#type-autochild) system, or can instead be provided dynamically by implementing [ListGrid.getRollOverCanvas](ListGrid_2.md#method-listgridgetrollovercanvas) and/or [ListGrid.getRollUnderCanvas](ListGrid_2.md#method-listgridgetrollundercanvas).

The rollOver/rollUnder canvas will be automatically added to the grid's [body](#attr-listgridbody) as an [embedded component](ListGrid_2.md#method-listgridaddembeddedcomponent).  
For grids with [frozen fields](ListGridField.md#attr-listgridfieldfrozen), the behavior is as follows:

*   If [ListGrid.useCellRollOvers](#attr-listgridusecellrollovers) is false (the default), embedded components will be added to both the body and the frozen body
*   Otherwise the component will be added to whichever body contains the cell the user is currently over

The rollOver/rollUnder canvas added to the frozen body will be created by calling the [ListGrid.getFrozenRollOverCanvas](ListGrid_2.md#method-listgridgetfrozenrollovercanvas) or [ListGrid.getFrozenRollUnderCanvas](ListGrid_2.md#method-listgridgetfrozenrollundercanvas) methods. The default implementation for these methods matches their equivalents for non-frozen rollOver / rollUnder canvases - it will use the autoChild subsystem to create a canvas from the [ListGrid.rollOverCanvas](#attr-listgridrollovercanvas) autoChild configuration.

`showRollOverCanvas` has no effect if [ListGrid.showRollOver](#attr-listgridshowrollover) is `false`.

See also [ListGrid.showSelectedRollOverCanvas](#attr-listgridshowselectedrollovercanvas).

### Groups

- rowEffects

### See Also

- [ListGrid.showRollUnderCanvas](#attr-listgridshowrollundercanvas)

**Flags**: IRWA

---
## Attr: ListGrid.hiliteIconHeight

### Description
Height for hilite icons for this listGrid. Overrides [hiliteIconSize](#attr-listgridhiliteiconsize). Can be overridden at the field level

### Groups

- hiliting

**Flags**: IRW

---
## Attr: ListGrid.showAllColumns

### Description
Whether all columns should be drawn all at once, or only columns visible in the viewport.

Drawing all columns causes longer initial rendering time, but allows smoother horizontal scrolling. With a very large number of columns, showAllColumns will become too slow.

### Groups

- performance

**Flags**: IR

---
## Attr: ListGrid.alternateRecordStyles

### Description
Whether alternating rows (or blocks of rows, depending on [GridRenderer.alternateRowFrequency](GridRenderer.md#attr-gridrendereralternaterowfrequency)) should be drawn in alternating styles, in order to create a "ledger" effect for easier reading.

If enabled, the cell style for alternate rows will have the [GridRenderer.alternateRowSuffix](GridRenderer.md#attr-gridrendereralternaterowsuffix) appended to it. See also [GridRenderer.alternateColumnStyles](GridRenderer.md#attr-gridrendereralternatecolumnstyles).

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: ListGrid.emptyMessageStyle

### Description
The CSS style name applied to the [ListGrid.emptyMessage](#attr-listgridemptymessage) if displayed.

### Groups

- emptyMessage

**Flags**: IRW

---
## Attr: ListGrid.autoFetchDisplayMap

### Description
If true, for fields where [ListGridField.optionDataSource](ListGridField.md#attr-listgridfieldoptiondatasource) is specified, a valueMap will be automatically created by making a [DataSource.fetchData](DataSource.md#method-datasourcefetchdata) call against the specified dataSource and extracting a valueMap from the returned records based on the displayField and valueField.

If set to false, valueMaps will not be automatically fetched. In this case, setting field.optionDataSource is effectively a shortcut for setting optionDataSource on the editor via [ListGridField.editorProperties](ListGridField.md#attr-listgridfieldeditorproperties).

Can also be disabled on a per-field basis with [ListGridField.autoFetchDisplayMap](ListGridField.md#attr-listgridfieldautofetchdisplaymap).

### Groups

- display_values

### See Also

- [ListGridField.autoFetchDisplayMap](ListGridField.md#attr-listgridfieldautofetchdisplaymap)
- [ListGridField.optionDataSource](ListGridField.md#attr-listgridfieldoptiondatasource)

**Flags**: IRW

---
## Attr: ListGrid.styledRowEnds

### Description
When set to true, the first and last cells in each row will be styled with an additional CSS class, via the [ListGrid.firstCellStyle](#attr-listgridfirstcellstyle) and [ListGrid.lastCellStyle](#attr-listgridlastcellstyle) attributes. This styling is added as a second style, additional to the cell's regular stateful style, so works with any cell-design and in all states, and is also applied correctly with or without frozen fields.

If all you want to do is provide rounded-corners for records in this grid, it may be simpler to set [ListGrid.recordRadius](#attr-listgridrecordradius) to a CSS _border-radius_ string that achieves the rounding you want.

Note that you can also provide your own implementation of [ListGrid.getCellStyle](ListGrid_2.md#method-listgridgetcellstyle) or [ListGrid.getCellCSSText](ListGrid_2.md#method-listgridgetcellcsstext), if you want to do something more complex, like a gradient fade that spans the end two cells on each side of a record.

**Flags**: IRW

---
## Attr: ListGrid.waitForSave

### Description
If this is an editable listGrid, this property determines whether the user will be able to dismiss the edit form, or navigate to another cell while the save is in process (before the asynchronous server response returns).

### Groups

- editing

**Flags**: IRWA

---
## Attr: ListGrid.alternateFieldStyles

### Description
Whether alternating columns (or blocks of columns, depending on [GridRenderer.alternateColumnFrequency](GridRenderer.md#attr-gridrendereralternatecolumnfrequency)) should be drawn in alternating styles, in order to create a vertical "ledger" effect for easier reading.

If enabled, the cell style for alternate rows will have the [GridRenderer.alternateColumnSuffix](GridRenderer.md#attr-gridrendereralternatecolumnsuffix) appended to it. See also [GridRenderer.alternateRowStyles](GridRenderer.md#attr-gridrendereralternaterowstyles).

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: ListGrid.stopOnErrors

### Description
If this is an editable listGrid, this property determines how failure to save due to validation errors should be displayed to the user.

If this property is true, when validation errors occur the errors will be displayed to the user in an alert, and focus will be returned to the first cell to fail validation.

If false, the cells that failed validation will be silently styled with the editFailedBaseStyle.

**Note:** stopOnErrors being set to true implies that 'waitForSave' is also true. We will not dismiss the editor until save has completed if stopOnErrors is true.

### Groups

- editing

### See Also

- [ListGrid.waitForSave](#attr-listgridwaitforsave)

**Flags**: IRWA

---
## Attr: ListGrid.clearSortFieldText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, this attribute will be shown as the menu item title to clear an existing sort on this field.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.missingSummaryFieldValue

### Description
If a summary format string contains an invalid field reference, replace the reference with the missingSummaryFieldValue. The default value is "-".

### Groups

- summaryFields

**Flags**: IRW

---
## Attr: ListGrid.showEllipsisWhenClipped

### Description
Should ellipses be displayed when cell content is clipped? May be overridden at the field level via [ListGridField.showEllipsisWhenClipped](ListGridField.md#attr-listgridfieldshowellipsiswhenclipped)

**Flags**: IRW

---
## Attr: ListGrid.alternateFieldSuffix

### Description
Suffix to append to [alternate columns](GridRenderer.md#attr-gridrendereralternatecolumnstyles). Note that if [GridRenderer.alternateRowStyles](GridRenderer.md#attr-gridrendereralternaterowstyles) is enabled, cells which fall into both an alternate row and column will have both suffixes appended - for example `"cellDarkAltCol"`.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: ListGrid.fieldCriteriaText

### Description
The field criteria prefix to show in filter editor field hover before the descriptive version of the field's criteria, if any. The descriptive text is formatted by [DataSource.getAdvancedCriteriaDescription](DataSource.md#classmethod-datasourcegetadvancedcriteriadescription).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.frozenBodyStyleName

### Description
CSS style used for the [frozen-body](#attr-listgridcanfreezefields) of this grid. If applying a background-color to the body via a CSS style applied using this property, be sure to set [ListGrid.bodyBackgroundColor](#attr-listgridbodybackgroundcolor) to `null`.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.headerTitleVAlign

### Description
Specifies vertical alignment in the column headers: "top", "center", or "bottom". Can be overridden for individual fields by setting [ListGridField.valign](ListGridField.md#attr-listgridfieldvalign).

When using [rotated titles](#attr-listgridrotateheadertitles), this attribute defaults to "bottom" if it remains unset.

### See Also

- [ListGridField.valign](ListGridField.md#attr-listgridfieldvalign)
- [ListGrid.rotateHeaderTitles](#attr-listgridrotateheadertitles)
- [ListGridField.rotateTitle](ListGridField.md#attr-listgridfieldrotatetitle)

**Flags**: IR

---
## Attr: ListGrid.selectionManager

### Description
The [Selection object](../kb_topics/selection.md#kb-topic-selection) associated with the `ListGrid`.

### Groups

- selection

**Flags**: RA

---
## Attr: ListGrid.hoverStyle

### Description
Style to apply to hovers shown over this grid.

### Groups

- hovers

### See Also

- [ListGrid.showHover](#attr-listgridshowhover)

**Flags**: IRWA

---
## Attr: ListGrid.filterWindowInstructions

### Description
The instruction text to display at the top of the [ListGrid.filterWindow](#attr-listgridfilterwindow).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.showHeaderSpanTitlesInSortEditor

### Description
If this grid has specified [headerSpans](#attr-listgridheaderspans), should field titles be prefixed with the titles of the headerSpans in which they are contained when using the [multi-sort editor](MultiSortDialog.md#class-multisortdialog).

### See Also

- [ListGrid.sortEditorSpanTitleSeparator](#attr-listgridsorteditorspantitleseparator)

**Flags**: IRW

---
## Attr: ListGrid.selectionAppearance

### Description
How selection of rows should be presented to the user.

For `selectionAppearance:"checkbox"` with multiple selection allowed, you would typically use [ListGrid.selectionType](#attr-listgridselectiontype):"simple" (the default). Because `selectionType` and `selectionAppearance` are unrelated, the combination of `selectionAppearance:"checkbox"` and `selectionType:"multiple"` results in a grid where multiple selection can only be achieved via shift-click or ctrl-click.

If using `"checkbox"` for a [ListGrid](#class-listgrid), see also [ListGrid.checkboxField](#attr-listgridcheckboxfield) for customization APIs.

If using `"checkbox"` for a [TreeGrid](TreeGrid.md#class-treegrid), an extra icon, [TreeGrid.getExtraIcon](TreeGrid.md#method-treegridgetextraicon) is not supported. Additionally only [ListGrid.selectionType](#attr-listgridselectiontype):"simple" and "single" are supported. You can also toggle the display of a disabled checkbox on a treeGrid, displayed when the node can't be selected, via [TreeGrid.showDisabledSelectionCheckbox](TreeGrid.md#attr-treegridshowdisabledselectioncheckbox).

Note that the default behavior when you enable checkbox selection is to continue to show the selected style. This can be changed by setting [ListGrid.showSelectedStyle](#attr-listgridshowselectedstyle) to false.

### Groups

- selection

**Flags**: IRW

---
## Attr: ListGrid.wrapHeaderSpanTitles

### Description
If [HeaderSpan.wrap](HeaderSpan.md#attr-headerspanwrap) is not explicitly set, should fields wrap? If autofitting, see the docs on that property for the details of how the minimum width for a field is determined.

### See Also

- [ListGrid.minFieldWidth](#attr-listgridminfieldwidth)

**Flags**: IR

---
## Attr: ListGrid.includeHilitesInSummaryFields

### Description
When assembling a value for a [summary field](#attr-listgridcanaddsummaryfields), if a referenced field is hilited, should the hilite HTML be included in the summary field value?

To control hilites showing in group summaries, see [showHilitesInGroupSummary](#attr-listgridshowhilitesingroupsummary).

### See Also

- [ListGrid.shouldIncludeHiliteInSummaryField](ListGrid_2.md#method-listgridshouldincludehiliteinsummaryfield)

**Flags**: IRWA

---
## Attr: ListGrid.savedSearchText

### Description
Text to show for the saved searches submenu.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.frozenRollOverCanvas

### Description
Automatically generated canvas embedded in the grid's frozen body if [showRollOver](#attr-listgridshowrollover) is `true` and [showRollOverCanvas](#attr-listgridshowrollovercanvas) is `true` or for selected records, if [showSelectedRollOverCanvas](#attr-listgridshowselectedrollovercanvas) is true. This component will be created and displayed above the current rollOver row or cell in the frozen body.

The frozenRollOverCanvas will be created using the [AutoChild](../reference.md#type-autochild) subsystem, and will derive its configuration from the [ListGrid.rollOverCanvas](#attr-listgridrollovercanvas) autoChild properties (`"rollOverCanvasProperties"`, et al).

The `frozenRollOverCanvas` has the following read-only attributes set:  
\- `this.grid` - a pointer to the grid  
\- `this.record` - a pointer to the current roll over record object in the grid

### Groups

- rowEffects

### See Also

- [ListGrid.rollOverCanvas](#attr-listgridrollovercanvas)
- [ListGrid.frozenRollUnderCanvas](#attr-listgridfrozenrollundercanvas)

**Flags**: RA

---
## Attr: ListGrid.expansionFieldImageShowRTL

### Description
If this grid is in RTL mode, should an "\_rtl" suffix be added to the [expansionFieldTrueImage](#attr-listgridexpansionfieldtrueimage) and [expansionFieldFalseImage](#attr-listgridexpansionfieldfalseimage) image URLs? This should only be enabled if RTL media for the true and false expansion field images are available.

If both this property and [ListGrid.expansionFieldImageShowSelected](#attr-listgridexpansionfieldimageshowselected) are true, and the grid is in RTL mode, both suffixes will be applied to selected rows' expansion field images (combined as "selected\_rtl").

### Groups

- RTL
- expansionField

**Flags**: IRA

---
## Attr: ListGrid.booleanBaseStyle

### Description
An optional CSS style to apply to the checkbox image. If supplied, and the checkbox is enabled, the base style is suffixed with "True", "False", or "Partial" if the checkbox is selected, unselected, or partially selected; if the checkbox is disabled, the suffix is "TrueDisabled", "FalseDisabled", or "PartialDisabled".

**NOTE:** This attribute is not supported by [TreeGrid](TreeGrid.md#class-treegrid).

### Groups

- imageColumns

### See Also

- [ListGrid.printBooleanBaseStyle](#attr-listgridprintbooleanbasestyle)

**Flags**: IRA

---
## Attr: ListGrid.groupTitleColumnProperties

### Description
Custom properties for the automatically generated `groupTitleColumn`.

See [ListGrid.showGroupTitleColumn](#attr-listgridshowgrouptitlecolumn) for an overview of the groupTitleColumn.

**Flags**: IR

---
## Attr: ListGrid.showSelectedRollUnderCanvas

### Description
This setting causes the [roll under canvas](#attr-listgridrollundercanvas) to be displayed when the user rolls over selected records in the grid (but not when rolling over other records). This can be useful to display a "Selected Over" appearance which can't be easily achieved via standard cell styling.

As with [ListGrid.showRollUnderCanvas](#attr-listgridshowrollundercanvas), if this property is unset, but the related [ListGrid.showSelectedRollOverCanvas](#attr-listgridshowselectedrollovercanvas) property is true, both the the roll under and roll under canvases will be displayed as the user rolls over selected records.

### Groups

- rowEffects

**Flags**: IRWA

---
## Attr: ListGrid.alwaysShowEditors

### Description
When this attribute is set, editors will be appear to be present in every row of the grid, allowing the user to immediately start editing any cell, rather than showing up in a single record at a time.  
This attribute is only valid when [ListGrid.editByCell](#attr-listgrideditbycell) is false.

This setting has some limitations and is typically only used for simple grids with a limited set of fields and standard editors.

*   Not all formItem types are supported. Default editors for standard data types (text, boolean, date, datetime, integer and float) are all supported, but custom editorType, including CanvasItem based editors are not. Fields with an unsupported editor type will show static values for all rows other than the current edit row, though users can start editing these with a single click
*   `alwaysShowEditors:true` grids do not support showing different editor types for the same field in different rows
*   In some cases there may be visual differences between the editor displayed in the edit row and the editor displayed in other rows.
*   From a design perspective, this mode presents a very "busy-looking" UI, which can made it harder to read the actual data. Functionally having [ListGrid.editEvent](#attr-listgrideditevent) set to "click" provides the same single-click to edit any cell user experience without the busy UI.
*   In some cases there may be a performance penalty for writing out so many controls (editors for every cell of the grid).

Note that in addition to alwaysShowEditors, listGrid support single-click editing via [editEvent:"click"](#attr-listgrideditevent), and, for boolean fields, [ListGridField.canToggle](ListGridField.md#attr-listgridfieldcantoggle)

### Groups

- editing

**Flags**: IRA

---
## Attr: ListGrid.dragTrackerMode

### Description
When records are being dragged from within a ListGrid, what sort of drag-tracker should be displayed?  
Note that if multiple records are being dragged the displayed tracker will be based on the first selected record.

### Groups

- dragTracker

**Flags**: IRA

---
## Attr: ListGrid.dataFetchMode

### Description
How to fetch and manage records retrieve from the server. See [FetchMode](../reference_2.md#type-fetchmode).

This setting only applies to the [ResultSet](ResultSet.md#class-resultset) automatically created by calling [fetchData()](ListGrid_2.md#method-listgridfetchdata). If a pre-existing ResultSet is passed to setData() instead, it's existing setting for [ResultSet.fetchMode](ResultSet.md#attr-resultsetfetchmode) applies.

### Groups

- databinding

### See Also

- [ListGrid.showAllRecords](#attr-listgridshowallrecords)

**Flags**: IR

---
## Attr: ListGrid.hiliteIcons

### Description
Specifies a list of icons that can be used in [hilites](DataBoundComponent.md#method-databoundcomponentedithilites).

`hiliteIcons` should be specified as an Array of [SCImgURL](../reference.md#type-scimgurl). When present, the hilite editing interface shown when [DataBoundComponent.editHilites](DataBoundComponent.md#method-databoundcomponentedithilites) is called will offer the user a drop down for picking one of these icons when defining either a simple or advanced hilite rule.

If the user picks an icon, the created hiliting rule will have [Hilite.icon](Hilite.md#attr-hiliteicon) set to the chosen icon. [DataBoundComponent.hiliteIconPosition](DataBoundComponent.md#attr-databoundcomponenthiliteiconposition) controls where the icon will appear for that field -- the default is that it appears in front of the normal cell content. This can also be overridden at the field level.

### Groups

- hiliting

**Flags**: IR

---
## Attr: ListGrid.sortDescendingImage

### Description
Image to show when sorted in descending order. Can be either a regular [SCImgURL](../reference.md#type-scimgurl) src, or an [ImgHTMLProperties](../reference_2.md#object-imghtmlproperties) object.

### Groups

- appearance

### See Also

- [ListGrid.sortArrowMenuButtonSpaceOffset](#attr-listgridsortarrowmenubuttonspaceoffset)

**Flags**: IRWA

---
## Attr: ListGrid.childExpansionMode

### Description
For [expansionModes](../reference_2.md#type-expansionmode) that show another grid or tree, what the child's expansionMode should be.

Default value `null` means no further expansion.

### Groups

- expansionField

**Flags**: IRWA

---
## Attr: ListGrid.scrollToCellXPosition

### Description
When scrollToCell is called, this is used as defaults if xPosition weren't explicitly passed into the method.

**Flags**: IRW

---
## Attr: ListGrid.showRollUnderCanvas

### Description
If roll overs are enabled, should the [rollUnderCanvas](#attr-listgridrollundercanvas) be displayed?

Use of the `showRollUnderCanvas` is enabled if [showRollOver](#attr-listgridshowrollover) is `true`, and either [showRollOverCanvas](#attr-listgridshowrollovercanvas) is `true` and `showRollUnderCanvas` is unset, or `showRollUnderCanvas` is explicitly set to `true`.

See also [ListGrid.showSelectedRollUnderCanvas](#attr-listgridshowselectedrollundercanvas).

### See Also

- [ListGrid.showRollOverCanvas](#attr-listgridshowrollovercanvas)

**Flags**: IRWA

---
## Attr: ListGrid.groupByMaxRecords

### Description
Maximum number of records to which a groupBy can be applied. If there are more records, grouping will not be available via the default header context menu, and calls to [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby) will be ignored.

The maximum exists because ListGrid grouping is performed in-browser, hence requires loading of all records that match the current filter criteria before records can be grouped. The default maximum represents a number of records which are safe to load in legacy browsers such as Internet Explorer 8 (modern browsers can handle far more), and is also a good upper limit from the perspective of loading data from a database.

Going beyond this limit can cause "script running slowly" errors from legacy browsers (as well as high database load). To build an interface for grouping that handles arbitrary data volume, use a TreeGrid with [TreeGrid.loadDataOnDemand](TreeGrid.md#attr-treegridloaddataondemand) with server-side grouping code.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IRW

---
## Attr: ListGrid.enforceVClipping

### Description
For performance reasons, even when [ListGrid.fixedRecordHeights](#attr-listgridfixedrecordheights) is set, vertical clipping is not enforced by default for some kinds of content (such as images) on all browsers. Set [enforceVClipping:true](#attr-listgridenforcevclipping) to enforce clipping for all types of content on all browsers.

This additional setting is likely to be phased out as browsers improve.

**Flags**: IRW

---
## Attr: ListGrid.expansionDetailRelated

### Description
Automatically generated [HLayout](../reference.md#class-hlayout) appearing in a record's expanded section when [listGrid.expansionMode](../reference_2.md#type-expansionmode) is `detailRelated`. This component contains two other autoChild components, a [DetailViewer](DetailViewer.md#class-detailviewer) for viewing fields from the record which are not already present in the grid and a separate embedded [ListGrid](#class-listgrid) for displaying other data related to this record via record.detailDS. See [ListGrid.expansionDetails](#attr-listgridexpansiondetails) and [ListGrid.expansionRelated](#attr-listgridexpansionrelated) for more information.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `listGrid.expansionDetailRelatedProperties` and `listGrid.expansionDetailRelatedDefaults`.

Note, however, that this is a multi-instance component (potentially one per record), so it is created using [createAutoChild()](Class.md#method-classcreateautochild) not [addAutoChild()](Class.md#method-classaddautochild), and no default single instance is created by name on the grid.

### Groups

- expansionField

**Flags**: RA

---
## Attr: ListGrid.spannedHeaderBaseStyle

### Description
[Button.baseStyle](Button.md#attr-buttonbasestyle) to apply to the field header buttons for this ListGrid when showing header spans. Note that, depending on the [Class](#attr-listgridheaderbuttonconstructor) of the header buttons, you may also need to set [ListGrid.headerTitleStyle](#attr-listgridheadertitlestyle).

### Groups

- gridHeader
- appearance
- headerSpan

**Flags**: IR

---
## Attr: ListGrid.applyRowNumberStyle

### Description
If [ListGrid.showRowNumbers](#attr-listgridshowrownumbers) is true, should we apply the [ListGrid.rowNumberStyle](#attr-listgridrownumberstyle) to the [ListGrid.rowNumberField](#attr-listgridrownumberfield)

### Groups

- rowNumberField

**Flags**: IRWA

---
## Attr: ListGrid.virtualScrolling

### Description
When incremental rendering is switched on and there are variable record heights, the virtual scrolling mechanism manages the differences in scroll height calculations due to the unknown sizes of un-rendered rows to make the scrollbar and viewport appear correctly.

When the `virtualScrolling` system is active, the last scroll position scrolls the last record to the top of the viewport, leaving blank space underneath. This is a necessary and unavoidable consequence of mapping the position of the scrollbar thumb to an unknown amount of remaining space without being able to know the total scrollable area in advance (since record heights vary).

virtualScrolling is switched on automatically when [ListGrid.fixedRecordHeights](#attr-listgridfixedrecordheights) is false and also when using the [recordComponents subsystem](#attr-listgridshowrecordcomponents), as recordComponents expand the rows that contain them. This flag should be manually enabled when calling [ListGrid.addEmbeddedComponent](ListGrid_2.md#method-listgridaddembeddedcomponent) if embedded components can cause record sizes to expand beyond specified cellHeight.

virtualScrolling is also automatically enabled when [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) is true to handle the fact that expanded rows may render at variable heights.

### See Also

- [ListGrid.recordComponentHeight](#attr-listgridrecordcomponentheight)

**Flags**: IRA

---
## Attr: ListGrid.sortField

### Description
Specifies the field by which this grid should be initially sorted. Can be set to either a [field name](ListGridField.md#attr-listgridfieldname) or the index of the field in the fields Array.

ListGrids also support being initialized with multiple-field sort via [ListGrid.initialSort](#attr-listgridinitialsort). If initialSort is specified, it will be used in preference to this property.

To sort the grid after it has been initialized, use [ListGrid.sort](ListGrid_2.md#method-listgridsort) or [ListGrid.setSort](ListGrid_2.md#method-listgridsetsort). Details about the current sort of a live grid can be retrieved by calling [ListGrid.getSortField](ListGrid_2.md#method-listgridgetsortfield) or [ListGrid.getSort](ListGrid_2.md#method-listgridgetsort)

### Groups

- sorting

**Flags**: IR

---
## Attr: ListGrid.canExpandRecords

### Description
When set to true, shows an additional field at the beginning of the field-list (respecting RTL) to allow users to expand and collapse individual records. See [ListGrid.expandRecord](ListGrid_2.md#method-listgridexpandrecord) and [ListGrid.expansionMode](#attr-listgridexpansionmode) for details on record expansion.

[ListGrid.virtualScrolling](#attr-listgridvirtualscrolling) is automatically enabled when canExpandRecords is set to true.

Note that expanded records are not currently supported in conjunction with [frozen fields](ListGridField.md#attr-listgridfieldfrozen).

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.recordSummaryAttributePrefix

### Description
Prefix prepended to the name of a ["summary"](ListGridField.md#attr-listgridfieldrecordsummaryfunction) [type](ListGridField.md#attr-listgridfieldtype) field when accessing its value as record metadata. The Framework may write out this value to make rendering the cell values or calculating a [grid summary row](#attr-listgridshowgridsummary) or [group summary rows](#attr-listgridshowgroupsummary) more efficient.

### See Also

- [ListGridField.type](ListGridField.md#attr-listgridfieldtype)
- [ListGridField.recordSummaryFunction](ListGridField.md#attr-listgridfieldrecordsummaryfunction)

**Flags**: IRA

---
## Attr: ListGrid.hiliteViaAIMode

### Description
When [ListGrid.canHiliteViaAI](#attr-listgridcanhiliteviaai) is `true`, the AI service mode to use.

**Flags**: IR

---
## Attr: ListGrid.titleField

### Description
Best field to use for a user-visible title for an individual record from this grid. If [ListGrid.dataSource](#attr-listgriddatasource) is non null, this property may be specified on the dataSource instead.

If not explicitly set, titleField looks for fields named "title", "name", and "id" in that order. If a field exists with one of those names, it becomes the titleField. If not, then the first field is designated as the titleField.

**Flags**: IRW

---
## Attr: ListGrid.iconCursor

### Description
Default cursor to display when the user rolls over icons within cells of an [type:icon](ListGridField.md#attr-listgridfieldtype) field.

May be overridden by [ListGridField.iconCursor](ListGridField.md#attr-listgridfieldiconcursor).

Note: Unlike the field-level [ListGridField.iconCursor](ListGridField.md#attr-listgridfieldiconcursor) property, listGrid.iconCursor has no effect on the cursor displayed for [valueIcons](ListGridField.md#attr-listgridfieldvalueicons).  
See [ListGrid.getValueIconCursor](ListGrid_2.md#method-listgridgetvalueiconcursor) for more details.

### See Also

- [ListGrid.getIconCursor](ListGrid_2.md#method-listgridgeticoncursor)

**Flags**: IRW

---
## Attr: ListGrid.groupByFieldSummaries

### Description
If this grid is [grouped](#attr-listgridgroupbyfield), and [ListGrid.showGroupSummary](#attr-listgridshowgroupsummary) is true, this attribute may be set to an array of groupBy field names for which group summaries should appear.

This is particularly useful for listGrids grouped by more than one field as it allows developers to display the group summary for a particular nested group without showing a summary for every level of the tree.

### See Also

- [ListGrid.showGroupSummary](#attr-listgridshowgroupsummary)

**Flags**: IRWA

---
## Attr: ListGrid.groupTree

### Description
The data tree that results from a call to [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby). This will be a [ResultTree](ResultTree.md#class-resulttree) if [ListGrid.dataSource](#attr-listgriddatasource) is present, otherwise it will be a [Tree](Tree.md#class-tree).

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: R

---
## Attr: ListGrid.expansionIndent

### Description
When [canExpandRecords](#attr-listgridcanexpandrecords) is true, this is the pixel-amount by which child components are offset within the grid-body, by default from the left, or from the right when [RTL](Page.md#classmethod-pageisrtl) is in effect. If unset, assumes the width of the [expansionField](#attr-listgridexpansionfield), so that child components line up with the following field, according to RTL.

This setting overrides the [general indent](#attr-listgridembeddedcomponentindent) for embedded-components, on the appropriate side.

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.data

### Description
A list of ListGridRecord objects, specifying the data to be used to populate the ListGrid. In ListGrids, the data array specifies rows.

When using a [DataSource](DataSource.md#class-datasource), rather than directly providing `data`, you will typically call [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata) instead, which will automatically establish `data` as a [ResultSet](ResultSet.md#class-resultset) (see the [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata) docs for details).

If you call `fetchData`, any previously supplied `data` is discarded. Also, it is not necessary to call `setData()` after calling [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata).

When calling `setData()`, direct changes to the list using Framework APIs such as [List.add](List.md#method-listadd) or [List.remove](List.md#method-listremove) will be automatically observed and the ListGrid will redraw in response. However, direct changes to individual Records will not be automatically observed and require calls to [ListGrid.refreshCell](ListGrid_2.md#method-listgridrefreshcell) or [ListGrid.refreshRow](ListGrid_2.md#method-listgridrefreshrow) to cause the ListGrid to visually update. Calling methods such as [ListGrid.updateData](ListGrid_2.md#method-listgridupdatedata), [ListGrid.removeData](ListGrid_2.md#method-listgridremovedata) or [ListGrid.addData](ListGrid_2.md#method-listgridadddata) always causes automatic visual refresh.

Note that direct manipulation of the data object without using the [List](../reference_2.md#interface-list) APIs (for example by directly assigning a new Record object to some index or calling non-Framework APIs such as pop(), shift(), etc.) will not be reflected in the grid automatically, but developers can call [List.dataChanged](List.md#method-listdatachanged) directly to notify the grid of changes.

### Groups

- data

### See Also

- [ListGridRecord](../reference_2.md#object-listgridrecord)

**Flags**: IRW

---
## Attr: ListGrid.sorterButtonTitle

### Description
The title for the corner sort button. The title will only [ListGrid.changeDefaults()](Class.md#classmethod-classchangedefaults) rather than replacing with an entirely new object.

### Groups

- i18nMessages
- gridHeader
- appearance

**Flags**: IR

---
## Attr: ListGrid.datetimeFormatter

### Description
Display format to use for fields specified as type 'datetime'. Default is to use the system-wide default date time format, configured via [DateUtil.setShortDatetimeDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdatetimedisplayformat). Specify any valid [DateDisplayFormat](../reference.md#type-datedisplayformat) to change the display format for datetimes used by this grid. May be specified as a function. If specified as a function, this function will be executed in the scope of the Date and should return the formatted string.

May also be specified at the field level via [ListGridField.dateFormatter](ListGridField.md#attr-listgridfielddateformatter)

If this field is editable the dateFormatter will also be passed to the editor created to edit this field as [dateFormatter](DateItem.md#attr-dateitemdateformatter). In this case you may also need to set [ListGrid.dateInputFormat](#attr-listgriddateinputformat).

### Groups

- appearance

### See Also

- [ListGridField.dateFormatter](ListGridField.md#attr-listgridfielddateformatter)

**Flags**: IRW

---
## Attr: ListGrid.animateFolderSpeed

### Description
When animating folder opening / closing, this property designates the speed of the animation in pixels shown (or hidden) per second. Takes precedence over the [TreeGrid.animateFolderTime](TreeGrid.md#attr-treegridanimatefoldertime) property, which allows the developer to specify a duration for the animation rather than a speed.

For a ListGrid, this property applies when [grouping](#attr-listgridcangroupby) is enabled.

### Groups

- animation

### See Also

- [ListGrid.animateFolderTime](#attr-listgridanimatefoldertime)

**Flags**: IRW

---
## Attr: ListGrid.recordDetailDSProperty

### Description
The name of the ListGridRecord property that specifies the DataSource to use when [listGrid.expansionMode](../reference_2.md#type-expansionmode) is "related". The default is [ListGridRecord.detailDS](ListGridRecord.md#attr-listgridrecorddetailds). Note that you can set the [ListGrid.detailDS](#attr-listgriddetailds) at the grid level instead if the same dataSource is to be used for all records.

### Groups

- expansionField

**Flags**: IRWA

---
## Attr: ListGrid.recordRadiusTargets

### Description
Array of [RecordTypes](../reference.md#type-recordtype) that should be rounded when [ListGrid.recordRadius](#attr-listgridrecordradius) is set to a valid CSS _border-radius_ string.

By default, [group-headers](#attr-listgridcangroupby) and records showing [group](#attr-listgridshowgroupsummary) or [grid](#attr-listgridshowgridsummary) summaries are not rounded, because these records typically have a separator line to distinguish them from surrounding records.

**Flags**: IRW

---
## Attr: ListGrid.reverseRTLAlign

### Description
If a page is rendered in [RTL mode](Page.md#classmethod-pageisrtl), should cell alignments specified [ListGridField.cellAlign](ListGridField.md#attr-listgridfieldcellalign) be reversed (so an `align:"right"` field will have content aligned on the left and vice versa)?

This is true by default to match user expectation that text flows from start-to end and is aligned with the start of text flow (left in LTR mode, right in RTL mode) by default. May be set to false to have the specified alignments be taken literally in RTL mode.

### Groups

- RTL

**Flags**: IRW

---
## Attr: ListGrid.loadingMessage

### Description
If you have a databound listGrid and you scroll out of the currently loaded dataset, by default you will see blank rows until the server returns the data for those rows. The loadingMessage attribute allows you to specify arbitrary html that will be shown in each such "blank" record while the data for that record is loading.

### Groups

- emptyMessage
- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.headerBarStyle

### Description
Set the CSS style used for the header as a whole.

### Groups

- gridHeader
- appearance

**Flags**: IR

---
## Attr: ListGrid.showSortNumerals

### Description
When multiple fields are sorted, set this to false to hide the sort-numeral displayed by default after the sort-arrows in the header-buttons of sorted fields.

**Flags**: IRWA

---
## Attr: ListGrid.removeIcon

### Description
When [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) is enabled, default icon to show in the auto-generated field that allows removing records.

**Flags**: IR

---
## Attr: ListGrid.canRequestRowCount

### Description
Depending on whether [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading) is active, the exact count of available rows may not be known, and `canRequestRowCount` controls whether the end user may explicitly request it by clicking the [RowRangeDisplay](RowRangeDisplay.md#class-rowrangedisplay) label.

When this property is set to `true`, the user may request an accurate row count if one is not currently known by [clicking](RowRangeDisplay.md#attr-rowrangedisplaycanrequestrowcount) the [ListGrid.rowRangeDisplay](#attr-listgridrowrangedisplay). To have a row count fetch operation occur automatically when progressive data is loaded instead of requiring a user interaction to initiate the fetch, see [ListGrid.autoFetchRowCount](#attr-listgridautofetchrowcount).

Note: This property also acts as a default for [ResultSet.applyRowCountToLength](ResultSet.md#attr-resultsetapplyrowcounttolength). By default, if set to true, a user may therefore click the rowRangeDisplay label to request a row count query be executed on the server, and when the query is complete they may scroll the listGrid body freely, retrieving records from anywhere within the data set.

If [ListGrid.applyRowCountToLength](#attr-listgridapplyrowcounttolength) is explicitly set it will be applied to the grid's data object instead of using `applyRowCountToLength` as a default. For finer grained control, a developer may set both properties to false and manage behavior by explicitly calling [ListGrid.fetchRowCount](ListGrid_2.md#method-listgridfetchrowcount) and [listGrid.data.setFullLength()](ResultSet.md#method-resultsetsetfulllength) from application code.

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.canEditHilites

### Description
Adds an item to the header context menu allowing users to launch a dialog to define grid hilites using the [HiliteEditor](HiliteEditor.md#class-hiliteeditor).

User-added hilites can be persisted via [DataBoundComponent.getHiliteState](DataBoundComponent.md#method-databoundcomponentgethilitestate) and [DataBoundComponent.setHiliteState](DataBoundComponent.md#method-databoundcomponentsethilitestate).

To avoid undefined behavior, this property must be set to `false` if the same record objects, or the same [ResultSet](ResultSet.md#class-resultset) instances, are shared among multiple [DataBoundComponent](../reference.md#interface-databoundcomponent)s.

### Groups

- hiliting

**Flags**: IRW

---
## Attr: ListGrid.frozenBaseStyle

### Description
If this listGrid contains any frozen fields, this property can be used to apply a custom baseStyle to all cells in those frozen fields. If unset, the standard base style will be used for both frozen and unfrozen cells.

### Groups

- appearance
- frozenFields

### See Also

- [ListGrid.baseStyle](#attr-listgridbasestyle)
- [ListGridField.frozen](ListGridField.md#attr-listgridfieldfrozen)

**Flags**: IRW

---
## Attr: ListGrid.defaultTimeFieldWidth

### Description
Default width for time type fields. See [ListGrid.autoFitDateFields](#attr-listgridautofitdatefields) for details on how this property is used.

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.recordEditProperty

### Description
Property name on a record that should be checked to determine whether the record may be edited.  
This property is configurable to avoid possible collision with data values in record. With the default setting of "\_canEdit", a record can be set non-editable by ensuring record.\_canEdit == false.  
For controlling editability for the entire grid or for a field, set grid.canEdit or field.canEdit.

### Groups

- editing

### See Also

- [ListGrid.canEdit](#attr-listgridcanedit)
- [ListGridField.canEdit](ListGridField.md#attr-listgridfieldcanedit)
- [ListGrid.canEditCell](ListGrid_2.md#method-listgridcaneditcell)

**Flags**: IRWA

---
## Attr: ListGrid.recordBaseStyleProperty

### Description
This attribute allows custom base styles to be displayed on a per-record basis. To specify a custom base-style for some record set `record[listGrid.recordBaseStyleProperty]` to the desired base style name - for example if `recordBaseStyleProperty` is `"_baseStyle"`, set `record._baseStyle` to the custom base style name.

### Groups

- appearance

### See Also

- [ListGrid.baseStyle](#attr-listgridbasestyle)

**Flags**: IRWA

---
## Attr: ListGrid.dragHandleFieldTitle

### Description
The title to use for the [drag handle field](#attr-listgriddraghandlefield).

By default this title is not displayed in the drag column header button as the autochild defaults for the field set [ListGridField.showTitle](ListGridField.md#attr-listgridfieldshowtitle) to `false`.

### Groups

- dragHandleField

### See Also

- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)

**Flags**: IRWA

---
## Attr: ListGrid.overflow

### Description
Since [ListGrid.body](#attr-listgridbody) is configured with overflow: auto by default, no overflow is expected for the [ListGrid](#class-listgrid) itself so by default it has overflow: hidden.

### See Also

- [Layout.overflow](Layout.md#attr-layoutoverflow)

**Flags**: IRW

---
## Attr: ListGrid.emptyAIHoverContents

### Description
Hover contents to use when the AI-generated hover text is empty.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.printBooleanBaseStyle

### Description
If set, the [booleanBaseStyle](#attr-listgridbooleanbasestyle) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- imageColumns
- printing

### See Also

- [ListGrid.booleanBaseStyle](#attr-listgridbooleanbasestyle)

**Flags**: IRA

---
## Attr: ListGrid.scrollToCellYPosition

### Description
When scrollToCell is called, this is used as defaults if yPosition weren't explicitly passed into the method.

**Flags**: IRW

---
## Attr: ListGrid.generateClickOnSpace

### Description
If true, when the user navigates to a cell using arrow keys and hits space, the cell will respond to a click event.

**Flags**: IRWA

---
## Attr: ListGrid.showHeaderMenuButton

### Description
If set to true and [showHeaderContextMenu](#attr-listgridshowheadercontextmenu) is true, the [ListGrid.headerMenuButton](#attr-listgridheadermenubutton) will be displayed when the user rolls over the header buttons in this grid. Not supported for [CubeGrid](CubeGrid.md#class-cubegrid).

### Groups

- headerMenuButton

**Flags**: IR

---
## Attr: ListGrid.longTextEditorType

### Description
When the length of the field specified by [DataSourceField.length](DataSourceField.md#attr-datasourcefieldlength) exceeds `this.longTextEditorThreshold` show an edit field of this type rather than the standard text field when the field enters inline edit mode.

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.skipLineBreaks

### Description
Whether to skip line breaks for all fields by default when [escaping HTML](ListGridField.md#attr-listgridfieldescapehtml). This property can be overridden at the field level by [ListGridField.skipLineBreaks](ListGridField.md#attr-listgridfieldskiplinebreaks).

### See Also

- [ListGridField.escapeHTML](ListGridField.md#attr-listgridfieldescapehtml)

**Flags**: IRW

---
## Attr: ListGrid.autoConfirmSaveEdits

### Description
For editable listGrids, outstanding unsaved edits when the user performs a new filter or sort will be discarded by default. This flag determines whether we should save such edits automatically in this case. See also [ListGrid.confirmDiscardEdits](#attr-listgridconfirmdiscardedits), which allows the user to choose whether to save or discard the unsaved edits.

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.headerMenuButtonHeight

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, this property governs the height of the auto-generated `headerMenuButton`

### Groups

- headerMenuButton

### See Also

- [ListGrid.rotatedHeaderMenuButtonHeight](#attr-listgridrotatedheadermenubuttonheight)

**Flags**: IRA

---
## Attr: ListGrid.unknownRowCountDisplayValue

### Description
Value to return from [ListGrid.getFormattedRowCount](ListGrid_2.md#method-listgridgetformattedrowcount) when the row count is unknown

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.headerMenuButtonIconHeight

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, this property governs the height of the icon shown on the auto-generated `headerMenuButton`

### Groups

- headerMenuButton

**Flags**: IRA

---
## Attr: ListGrid.headerSpanHeight

### Description
Default height for a [headerSpan](#attr-listgridheaderspans) with no height specified.

If `headerSpanHeight` is not specified (the default), headerSpans will be 1/2 of [ListGrid.headerHeight](#attr-listgridheaderheight).

### Groups

- headerSpan

**Flags**: IR

---
## Attr: ListGrid.recordComponentPoolingMode

### Description
The method of [component-pooling](../reference_2.md#type-recordcomponentpoolingmode) to employ for [recordComponents](#attr-listgridshowrecordcomponents).

The default mode is "viewport", which means that recordComponents are destroyed as soon their record is no longer being rendered (scrolled out of the viewport, eliminated by search criteria, etc).

For a large or dynamic data set where the components shown on different rows are similar, switch to "recycle" mode, which pools recordComponents by detaching them from records that are not visible and re-using them in other records. In this mode, you should implement [ListGrid.updateRecordComponent](ListGrid_2.md#method-listgridupdaterecordcomponent) to apply any changes to make reused components applicable to the new record they appear in, if necessary. For example, if you have several controls in your `recordComponents`, and not all of the controls apply to every record, your `updateRecordComponent()` implementation could simply hide or disable inapplicable controls, and this would be much faster than creating a whole new set of controls every time a given record is scrolled into view.

If you are using [per-cell recordComponents](#attr-listgridshowrecordcomponentsbycell), and you have components of different types in different columns and still want to take advantage of component recycling, you can set [ListGrid.poolComponentsPerColumn](#attr-listgridpoolcomponentspercolumn) to ensure that components intended for one column are not recycled for use in another column that should have a different component.

Note that, if different records have distinctly different components embedded in them, or multiple columns in each record embed different components, you should leave the recordComponentPoolingMode at "viewport" if your dataset is very large or use "data" otherwise.

### Groups

- recordComponents

**Flags**: IRWA

---
## Attr: ListGrid.fieldPickerFieldProperties

### Description
Names of properties on [ListGridField](../reference_2.md#object-listgridfield) for which the [FieldPicker](FieldPicker.md#class-fieldpicker) should show an editing interface, for convenience.

For example, specify \["frozen", "decimalPrecision"\] to allow end users to modify [ListGridField.frozen](ListGridField.md#attr-listgridfieldfrozen) and [ListGridField.decimalPrecision](ListGridField.md#attr-listgridfielddecimalprecision) respectively.

**Flags**: IR

---
## Attr: ListGrid.gridComponents

### Description
Array of components that make up this grid. This array controls which standard and/or custom parts will be displayed within this ListGrid.

ListGrid is a subclass of [VLayout](../reference.md#class-vlayout) and consists of a number of member components. The standard set of members are automatically generated by the grid, and include (for example) the header (a Toolbar of buttons for each field) and the body (a GridRenderer displaying the actual data contained in the grid).  
The default value of `gridComponents` is an Array of [ListGridComponent](../reference.md#type-listgridcomponent)s listing the standard components in their default order:

```
    gridComponents : ["filterEditor", "header",
                      "body", "summaryRow"]
 
```
You can override `gridComponents` to change the order of standard components. You can also omit standard components this way, although it more efficient to use the related "show" property if available (eg [ListGrid.showFilterEditor](#attr-listgridshowfiltereditor)). Note that this array must contain an entry for the `"body"` - listGrids with no body showing are unsupported.  
_Advanced note:_ The live components generated for each of these standard [ListGridComponent](../reference.md#type-listgridcomponent) types may differ across different listGrids. For example if this grid has any [frozen fields](ListGridField.md#attr-listgridfieldfrozen), the "body" entry will actually be created as an HLayout containing two GridRenderers (one for frozen fields, and one for unfrozen fields). This is really an implementation detail - the "body" entry in the gridComponents array simply specifies where the UI for the body should render within the ListGrid layout.

By embedding a Canvas directly in this list you can add arbitrary additional components to the listGrid as members, and have them be displayed alongside the standard automatically generated parts of the ListGrid.  
You can also use a [AutoChildShortcut](../reference.md#type-autochildshortcut) to have an [AutoChild](../reference.md#type-autochild) be automatically generated and displayed. Note that this pattern requires that you explicitly set `show_AutoChildName_` to `true` for the grid.

Note that having added controls to gridComponents, you can still call APIs directly on those controls to change their appearance, and you can also show() and hide() them if they should not be shown in some circumstances.

Tip: custom controls need to set layoutAlign:"center" to appear vertically centered.

See [this example](https://smartclient.com/smartgwt/showcase/#grid_appearance_custom_toolbar) of subclassing ListGrid and using gridComponents to add a tool bar with standard functions that you want throughout your application.

**Flags**: IR

---
## Attr: ListGrid.groupSortDirection

### Description
When [ListGrid.sortByGroupFirst](#attr-listgridsortbygroupfirst) is active, the sorting direction applied for implicit sorting by the field(s) used for grouping. Default of null means that sort direction is based on the current direction of user-configured sort, or is "ascending" if the user has not sorted the data.

### Groups

- sorting
- grouping

### See Also

- [ListGrid.sortByGroupFirst](#attr-listgridsortbygroupfirst)
- [ListGrid.groupSortNormalizer](ListGrid_2.md#method-listgridgroupsortnormalizer)
- [SortSpecifier.direction](../reference.md#attr-sortspecifierdirection)

**Flags**: IRW

---
## Attr: ListGrid.autoSizeHeaderSpans

### Description
If this listGrid has specified [ListGrid.headerSpans](#attr-listgridheaderspans), setting this attribute to true will cause spans to expand to accommodate long titles if necessary.

### Groups

- headerSpan
- autoFitFields

**Flags**: IR

---
## Attr: ListGrid.rollOverCanvas

### Description
AutoChild created and embedded in the grid if [showRollOver](#attr-listgridshowrollover) is `true` and [showRollOverCanvas](#attr-listgridshowrollovercanvas) is `true` or for selected records, if [showSelectedRollOverCanvas](#attr-listgridshowselectedrollovercanvas) is true. This component will be created and displayed above the current rollOver row or cell.

Note that if this grid has frozen fields, the [AutoChild](../reference.md#type-autochild) subsystem will use the `rollOverCanvas` configuration settings to create the [ListGrid.frozenRollOverCanvas](#attr-listgridfrozenrollovercanvas) (displayed in the frozen listGrid body).

The `rollOverCanvas` has the following read-only attributes set:  
\- `this.grid` - a pointer to the grid  
\- `this.record` - a pointer to the current roll over record object in the grid

### Groups

- rowEffects

### See Also

- [ListGrid.frozenRollOverCanvas](#attr-listgridfrozenrollovercanvas)
- [ListGrid.rollUnderCanvas](#attr-listgridrollundercanvas)

**Flags**: RA

---
## Attr: ListGrid.useLegacyDefaultFormattedValue

### Description
Controls whether [ListGrid.getDefaultFormattedValue](ListGrid_2.md#method-listgridgetdefaultformattedvalue) uses legacy behavior that omits standard formatting operations.

When `false`, `getDefaultFormattedValue()` applies complete formatting including [ListGridField.valueMap](ListGridField.md#attr-listgridfieldvaluemap) mapping, [ListGridField.displayField](ListGridField.md#attr-listgridfielddisplayfield) substitution, [listGridField.cellValueTemplate](#listgridfieldcellvaluetemplate) evaluation, [ListGridField.format](ListGridField.md#attr-listgridfieldformat) application, and type-specific formatters, matching the behavior of normal cell rendering.

When true `true`, `getDefaultFormattedValue()` returns minimally formatted values without these transformations. This preserves backward compatibility with existing code that relies on the legacy behavior.

**Flags**: IRWA

---
## Attr: ListGrid.initialCriteria

### Description
Criteria to be used when [ListGrid.autoFetchData](#attr-listgridautofetchdata) is set.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

### Groups

- searchCriteria

**Flags**: IR

---
## Attr: ListGrid.printWrapCells

### Description
Whether cell contents should wrap during printing. Equivalent to [ListGrid.wrapCells](#attr-listgridwrapcells), but specific to printed output.

### Groups

- printing

**Flags**: IRW

---
## Attr: ListGrid.selectHeaderOnSort

### Description
If true, show the field-header for the sorted field (or the first field in a [multi-sort](#attr-listgridcanmultisort) grid) in the selected state.

### Groups

- sorting

**Flags**: IRW

---
## Attr: ListGrid.expansionDetails

### Description
Automatically generated [DetailViewer](DetailViewer.md#class-detailviewer) for displaying the details of a record in its expanded section when [listGrid.expansionMode](../reference_2.md#type-expansionmode) is `details`. Note that only those fields which do not already appear in the grid are displayed in the expanded section.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `listGrid.expansionDetailsProperties` and `listGrid.expansionDetailsDefaults`.

Note, however, that this is a multi-instance component (potentially one per record), so it is created using [createAutoChild()](Class.md#method-classcreateautochild) not [addAutoChild()](Class.md#method-classaddautochild), and no default single instance is created by name on the grid.

### Groups

- expansionField

**Flags**: RA

---
## Attr: ListGrid.includeInSummaryProperty

### Description
Property name on a record that will be checked to determine whether a record should be included when calculating totals for the [grid summary](#attr-listgridshowgridsummary).

**Flags**: IRW

---
## Attr: ListGrid.hiliteIconWidth

### Description
Width for hilite icons for this component. Overrides [hiliteIconSize](#attr-listgridhiliteiconsize). Can be overridden at the field level.

### Groups

- hiliting

**Flags**: IRW

---
## Attr: ListGrid.headerButtonAriaRole

### Description
Default [role](Canvas.md#attr-canvasariarole) for [header buttons](#attr-listgridshowheader). See [ListGrid.getHeaderButtonAriaRole](ListGrid_2.md#method-listgridgetheaderbuttonariarole).

**Flags**: IRA

---
## Attr: ListGrid.canAddSummaryFields

### Description
Adds an item to the header context menu allowing users to launch a dialog to define a new text field that can contain both user-defined text and the formatted values present in other fields, using the [SummaryBuilder](SummaryBuilder.md#class-summarybuilder).

User-added summary fields can be persisted via [ListGrid.getFieldState](ListGrid_2.md#method-listgridgetfieldstate) and [ListGrid.setFieldState](ListGrid_2.md#method-listgridsetfieldstate).

To avoid undefined behavior, this property must be set to `false` if the same record objects, or the same [ResultSet](ResultSet.md#class-resultset) instances, are shared among multiple [DataBoundComponent](../reference.md#interface-databoundcomponent)s.

### Groups

- summaryFields

**Flags**: IRW

---
## Attr: ListGrid.showRecordComponentsByCell

### Description
If true, shows [recordComponents](#attr-listgridshowrecordcomponents) in cells, rather than just in records.

### Groups

- recordComponents

**Flags**: IRWA

---
## Attr: ListGrid.headerAriaRole

### Description
[Aria role](Canvas.md#attr-canvasariarole) for this listGrid's [header](#attr-listgridshowheader). See [ListGrid.getHeaderAriaRole](ListGrid_2.md#method-listgridgetheaderariarole)

**Flags**: IRA

---
## Attr: ListGrid.dragHandleField

### Description
An automatically generated field that can be dragged to drag the current selection (where otherwise the grid itself might be scrolled). Visibility is controlled by [ListGrid.showInitialDragHandles](#attr-listgridshowinitialdraghandles), [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles), and [ListGrid.hideDragHandles](ListGrid_2.md#method-listgridhidedraghandles).

### Groups

- dragHandleField

**Flags**: IR

---
## Attr: ListGrid.warnOnRemovalMessage

### Description
Warning message to show the user on a click on the 'remove' icon if [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) is true and [ListGrid.warnOnRemoval](#attr-listgridwarnonremoval) is true.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.rowRangeDisplayStyle

### Description
How should the [ListGrid.getFormattedRowRange](ListGrid_2.md#method-listgridgetformattedrowrange) format the row range and row count for display to the user?

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.aiSortProgressDialog

### Description
Dialog that shows progress after requesting AI-sorting of a field.

**Flags**: IR

---
## Attr: ListGrid.headerShadowVOffset

### Description
If [ListGrid.showHeaderShadow](#attr-listgridshowheadershadow) is true, the [Canvas.shadowVOffset](Canvas.md#attr-canvasshadowvoffset) for the header shadow

**Flags**: IRA

---
## Attr: ListGrid.timeFormatter

### Description
Display format to use for fields specified as type 'time'. May also be specified at the field level via [ListGridField.timeFormatter](ListGridField.md#attr-listgridfieldtimeformatter).  
If unset, time fields will be formatted based on the system wide [Time.shortDisplayFormat](Time.md#classattr-timeshortdisplayformat).  
If this field is editable, the timeFormatter will also be passed to the editor created to edit any time type fields as [TimeItem.timeFormatter](TimeItem.md#attr-timeitemtimeformatter)

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.fixedFieldWidths

### Description
Should we horizontally clip cell contents, or allow columns to expand horizontally to show all contents?

If we allow columns to expand, the column width is treated as a minimum.

NOTE: the header does not automatically respond to expanded field widths. If your grid is showing a header we'd recommend developers consider setting [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths) rather than using this attribute.

### Groups

- cellStyling

**Flags**: IRWA

---
## Attr: ListGrid.screenReaderCellSeparator

### Description
Special cell-separator that may be inserted between cell values when screen-readers are reading the content of a row. Only applies when screen-reader mode is enabled, and for ListGrids with [ariaRole:"list"](#attr-listgridariarole).

When [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode) is enabled, for ListGrids with [ListGrid.ariaRole](#attr-listgridariarole) set to `"list"`, each row in the grid will be rendered as HTML with role `"listItem"`.  
In this mode, the `screenReaderCellSeparator` property, (along with [ListGrid.screenReaderIncludeFieldTitles](#attr-listgridscreenreaderincludefieldtitles) and [ListGrid.screenReaderRowSeparator](#attr-listgridscreenreaderrowseparator)), gives developers a way to customize how screen readers read the row's text value in a way that may be helpful for grids with multiple columns.  
Instead of just picking up the value of each cell in the row strung together, readers will instead pick up the field title, the cell value and then the cellSeparator for each cell, and then the rowSeparator to mark the end of the row. Most screenreaders will also read the row index and total row count - something like "3 of 20".

Note that screen readers vary widely on which punctuation symbols are read aloud, and sometimes it depends on the context of the punctuation. However, the widely-used JAWS, NVDA, and VoiceOver screen readers all read the forward slash '/' as "slash". See [Why Don’t Screen Readers Always Read What’s on the Screen? Part 1: Punctuation and Typographic Symbols](http://www.deque.com/blog/dont-screen-readers-read-whats-screen-part-1-punctuation-typographic-symbols/) for a table of findings on which punctuation symbols are read aloud by JAWS, NVDA, and VoiceOver.

Implementation notes: the generated row HTML makes use of the [aria-labelledby](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-labelledby_attribute) property to achieve this - pointing the screenReader to the title button for the column, the cell content, and a special hidden element containing the cellSeparator.  
Note that this aria-labelledby setting is applied in addition to other aria state specified by [ListGrid.getRowAriaState](ListGrid_2.md#method-listgridgetrowariastate).

To entirely disable this feature, developers may set [ListGrid.screenReaderWriteRowLabelledBy](#attr-listgridscreenreaderwriterowlabelledby) to `false`. In this case other row aria attributes will still be picked up from [ListGrid.getRowAriaState](ListGrid_2.md#method-listgridgetrowariastate), including the `setsize` and `posinset` attributes that tell the screen reader where they currently are in the list.

See [ListGrid.ariaRole](#attr-listgridariarole) for more information on the ARIA attributes generated by ListGrids.

### Groups

- accessibility

**Flags**: IRA

---
## Attr: ListGrid.fieldState

### Description
Initial [field state](../reference_2.md#type-listgridfieldstate) for the grid.

[ViewState](../reference.md#type-viewstate) can be used to initialize all view properties of the grid. When doing so, `fieldState` is not needed because `viewState` includes it as well. If both are provided, `fieldState` has priority for field state.

To retrieve current state call [getFieldState](ListGrid_2.md#method-listgridgetfieldstate).

### Groups

- viewState

**Flags**: IRW

---
## Attr: ListGrid.exportAlternateRowBGColor

### Description
When exporting data to Excel/OpenOffice format using [exportData()](ListGrid_2.md#method-listgridexportdata) or [exportClientData()](ListGrid_2.md#method-listgridexportclientdata), background color to use for even-numbered rows, to create a "banded" or "ledger" effect. Odd-numbered rows will use the [ListGrid.exportDefaultBGColor](#attr-listgridexportdefaultbgcolor).

See [exportBGColor](../kb_topics/exportBGColor.md#kb-topic-exports--cell-background-color) for an overview.

### Groups

- exportBackgroundColor

**Flags**: IR

---
## Attr: ListGrid.hiliteRowOnFocus

### Description
When the grid body gets keyboard focus, should we highlight the current focus row, using the rollover cell style?

This property may be explicitly set to control this behavior independently of [ListGrid.showRollOver](#attr-listgridshowrollover). Otherwise (if this property is null), we will show the roll-over styling for the keyboard focus row if [ListGrid.showRollOver](#attr-listgridshowrollover) is true.

**Flags**: IRW

---
## Attr: ListGrid.printCheckboxFieldPartialImage

### Description
If set, the [ListGrid.checkboxFieldPartialImage](#attr-listgridcheckboxfieldpartialimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- checkboxField
- printing

### See Also

- [ListGrid.checkboxFieldPartialImage](#attr-listgridcheckboxfieldpartialimage)

**Flags**: IRWA

---
## Attr: ListGrid.defaultDateTimeFieldWidth

### Description
Default width for datetime type fields. See [ListGrid.autoFitDateFields](#attr-listgridautofitdatefields) for details on how this property is used.

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.showHeader

### Description
Should we show the header for this ListGrid?

### Groups

- gridHeader
- appearance

**Flags**: IRW

---
## Attr: ListGrid.scrollWheelRedrawDelay

### Description
While scrolling an incrementally rendered grid, using the mouseWheel, time in milliseconds to wait before redrawing, after the last mouseWheel movement by the user. If not specified [ListGrid.scrollRedrawDelay](#attr-listgridscrollredrawdelay) will be used as a default for both drag scrolling and mouseWheel scrolling.

Note that if specified, this value will typically be larger than [ListGrid.scrollRedrawDelay](#attr-listgridscrollredrawdelay). From experimentation, the default setting of `250` is typically enough time for a user to rapidly scroll through a grid (rotating the scroll wheel with repeated flicks), without redrawing between rotations, but this will differ depending on how long the redraw takes. A larger delay may be warranted for grids with large numbers of columns, heavy custom formatting, etc.

See also [GridRenderer.instantScrollTrackRedraw](GridRenderer.md#attr-gridrendererinstantscrolltrackredraw) for cases where this delay is skipped.

### Groups

- performance

**Flags**: IRW

---
## Attr: ListGrid.filterWindowTitle

### Description
The title for the [advanced filtering window](#attr-listgridfilterwindow).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.savedSearchDS

### Description
Override of [SavedSearches.defaultDataSource](SavedSearches.md#attr-savedsearchesdefaultdatasource) for this component.

**Flags**: IR

---
## Attr: ListGrid.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria) and related methods.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

To see implicitCriteria in action, take a look at [this example](https://www.smartclient.com/smartclient-latest/showcase/?id=additiveFilter) of using implicitCriteria to have an external form filter the grid in parallel with the [filterEditor](#attr-listgridshowfiltereditor).

**Flags**: IRW

---
## Attr: ListGrid.showCellContextMenus

### Description
Whether to show a context menu with standard items for all context clicks on rows in the body.

**Flags**: IRW

---
## Attr: ListGrid.multiGroupDialogProperties

### Description
Properties to apply to the [MultiGroupDialog](MultiGroupDialog.md#class-multigroupdialog) which gets automatically generated when [ListGrid.configureGrouping](ListGrid_2.md#method-listgridconfiguregrouping) is called.

**Flags**: IR

---
## Attr: ListGrid.noSavedSearchesText

### Description
Text to show in menu listing saved searches when there are no saved searches.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.recordScreen

### Description
Screen to create (via [createScreen()](RPCManager.md#classmethod-rpcmanagercreatescreen)) in lieu of calling [ListGrid.getRecordComponent](ListGrid_2.md#method-listgridgetrecordcomponent).

If this grid has a [dataSource](#attr-listgriddatasource), the created screen is provided with a [Canvas.dataContext](Canvas.md#attr-canvasdatacontext) that includes the record being shown at the row. Be sure the record screen meets these [requirements](Canvas.md#attr-canvasautopopulatedata) to utilize the `dataContext`.

### Groups

- recordComponents

**Flags**: IR

---
## Attr: ListGrid.frozenFieldsMaxWidth

### Description
Maximum width available for any [frozen fields](../kb_topics/frozenFields.md#kb-topic-frozen-fields) shown in this grid. May be specified as a percentage or numeric pixel value.

If the frozen fields' combined width exceeds this value, a horizontal scrollbar will be shown, allowing the frozen fields to be horizontally scrolled (independently from the unfrozen fields).

**Flags**: IRW

---
## Attr: ListGrid.sortArrowMenuButtonSpaceOffset

### Description
When [ListGrid.leaveHeaderMenuButtonSpace](#attr-listgridleaveheadermenubuttonspace) is true, configures the amount of space beyond the [ListGrid.headerMenuButtonWidth](#attr-listgridheadermenubuttonwidth) on the right side of a ListGrid header button (left for [RTL mode](Page.md#classmethod-pageisrtl)) to reserve for the sort arrow if sorting is active for that field and the arrow will be shown. May be increased for more separation between the sort arrow and the title text, at the expense of a reduced space for the title text.

This value may need to be customized in your skin or if [ListGrid.sortAscendingImage](#attr-listgridsortascendingimage) or [ListGrid.sortDescendingImage](#attr-listgridsortdescendingimage) are changed.

### See Also

- [ListGrid.sortNumeralMenuButtonSpaceOffset](#attr-listgridsortnumeralmenubuttonspaceoffset)

**Flags**: IRW

---
## Attr: ListGrid.rowEndEditAction

### Description
If the user is editing a record in this listGrid, and attempts to navigate to a field beyond the end of the row, via tab (or shift-tab off the first editable field), this property determines what action to take:

*   "next": start editing the next (or previous) record in the list
*   "same": put focus back into the first editable field of the same record.
*   "done": hide the editor
*   "stop": leave focus in the cell being edited
*   "none": no action

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.criteriaIndicatorHeaderColor

### Description
The color of the [filterWindow criteria indicator](#attr-listgridshowfilterwindowcriteriaindicator) when shown on the [sorter button](#attr-listgridsorterconstructor) or the last [header button](#attr-listgridheaderbuttonconstructor) in the grid header. The default is to use [ListGrid.criteriaIndicatorColor](#attr-listgridcriteriaindicatorcolor).

**Flags**: IR

---
## Attr: ListGrid.headerContextMenu

### Description
The context menu displayed for column headers.

### Groups

- gridHeader

**Flags**: R

---
## Attr: ListGrid.showGroupTitleColumn

### Description
If this grid is [grouped](ListGrid_2.md#method-listgridgroupby) and [ListGrid.showGroupSummaryInHeader](#attr-listgridshowgroupsummaryinheader) is true, instead of group header nodes showing up with a single cell value spanning the full set of columns, summaries for each field will show up in the appropriate columns of the header node.

In this case there are 2 options for where the group title will show up. Developers may specify an existing field to put the title values into via [ListGrid.groupTitleField](#attr-listgridgrouptitlefield). If no groupTitleField is specified, this property may be set to `true` which causes a `groupTitleColumn` to be automatically generated. Each group header will show the group title in this column (records within the group will not show a value for this column). The column appears in the leftmost position within the grid (unless [ListGrid.showRowNumbers](#attr-listgridshowrownumbers) is true, in which case this column shows up in the second-leftmost position), and by default will auto-fit to its data.

To customize this field, developers may modify [ListGrid.groupTitleColumnProperties](#attr-listgridgrouptitlecolumnproperties) or [ListGrid.groupTitleColumnDefaults](#attr-listgridgrouptitlecolumndefaults) at the class level.

**Flags**: IR

---
## Attr: ListGrid.animateSelectionUnder

### Description
If the [selectionUnderCanvas](#attr-listgridselectionundercanvas) is enabled, setting this property to `true` ensures that when the `selectionUnderCanvas` is displayed it is animated into view via [Canvas.animateShow](Canvas.md#method-canvasanimateshow). Note that the animation effect may be customized via [Canvas.animateShowEffect](Canvas.md#attr-canvasanimateshoweffect), [Canvas.animateShowTime](Canvas.md#attr-canvasanimateshowtime) and [Canvas.animateShowAcceleration](Canvas.md#attr-canvasanimateshowacceleration) set in `selectionUnderCanvasProperties`.

### Groups

- rowEffects

### See Also

- [ListGrid.animateSelection](#attr-listgridanimateselection)

**Flags**: IRWA

---
## Attr: ListGrid.minFieldWidth

### Description
Minimum size, in pixels, for ListGrid headers.

**Flags**: IRW

---
## Attr: ListGrid.minHeight

### Description
Sets the [minimum height](Canvas.md#attr-canvasminheight) for the entire list (smaller than this doesn't tend to work very well). If not set, this value will be defaulted when [draw()](Canvas.md#method-canvasdraw) is called to something reasonable based on whether we're showing the [filter editor](#attr-listgridshowfiltereditor), [header](#attr-listgridshowheader), [summary rows](#attr-listgridshowgridsummary), and/or the [empty message](#attr-listgridshowemptymessage). Any top or bottom CSS padding specified by [ListGrid.emptyMessageStyle](#attr-listgridemptymessagestyle) will be taken into account, increasing `minHeight` so that the empty message can be shown without overflow.

**Note:** Minimum sizes do not apply to all situations. See [minimum sizing rules](Canvas.md#attr-canvasminwidth) for details.

### Groups

- sizing

### See Also

- [Canvas.minHeight](Canvas.md#attr-canvasminheight)

**Flags**: IRW

---
## Attr: ListGrid.recordRowRoleProperty

### Description
If this property is set on a record it will designate the WAI ARIA role for this record's row.

**Flags**: IRWA

---
## Attr: ListGrid.neverValidate

### Description
If true, validation will not occur as a result of cell editing for this grid.

### Groups

- gridValidation

**Flags**: IRWA

---
## Attr: ListGrid.exportHeaderHeights

### Description
When exporting data to Excel/OpenOffice format using [ListGrid.exportData](ListGrid_2.md#method-listgridexportdata) or [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata), causes the [ListGrid.headerHeight](#attr-listgridheaderheight) and [headerSpan heights](HeaderSpan.md#attr-headerspanheight) to be applied to the corresponding cells in the spreadsheet.

**Flags**: IRW

---
## Attr: ListGrid.showSelectedRollOverCanvas

### Description
This setting causes the [roll over canvas](#attr-listgridrollovercanvas) to be displayed when the user rolls over selected records in the grid (but not when rolling over other records). This can be useful to display a "Selected Over" appearance which can't be easily achieved via standard cell styling.

### Groups

- rowEffects

**Flags**: IRWA

---
## Attr: ListGrid.screenReaderNavigateByCell

### Description
If [screen reader mode is enabled](isc.md#staticmethod-iscsetscreenreadermode), and [ListGrid.canSelectCells](#attr-listgridcanselectcells) is true should the user be able to navigate the grid cell-by-cell, highlighting and focusing on individual cells within the selected row via left and right arrow keypresses?

If [ListGrid.canSelectCells](#attr-listgridcanselectcells) is true, this property will have no effect as all navigation is by cell.

**Flags**: IRW

---
## Attr: ListGrid.canAddAISortFields

### Description
Adds an item to the header context menu allowing users to launch a dialog to define a new field to be sorted by an AI score of the entire record and possibility related records.

AI sort fields can be persisted via [ListGrid.getFieldState](ListGrid_2.md#method-listgridgetfieldstate) and [ListGrid.setFieldState](ListGrid_2.md#method-listgridsetfieldstate).

**Flags**: IRW

---
## Attr: ListGrid.loadingDataMessageStyle

### Description
The CSS style name applied to the loadingDataMessage string if displayed.

### Groups

- emptyMessage

**Flags**: IRW

---
## Attr: ListGrid.canPickFields

### Description
Indicates whether the field picker item and submenu should be present in the header context menu. This menu allows the user to hide visible fields and show hidden fields.

By default only fields explicitly included in the [ListGrid.fields](#attr-listgridfields) array will be available in this menu, unless [ListGrid.canPickOmittedFields](#attr-listgridcanpickomittedfields) is set to true for a databound grid.

A specific field can be omitted from the column picker via [ListGridField.canHide](ListGridField.md#attr-listgridfieldcanhide).

**Flags**: IRW

---
## Attr: ListGrid.unremoveIcon

### Description
When [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) is enabled, this icon will be shown in the auto generated field fro removing records if the record has been marked as removed via [ListGrid.markRecordRemoved](ListGrid_2.md#method-listgridmarkrecordremoved). At this point, clicking on the icon will unmark the record as removed.

**Flags**: IR

---
## Attr: ListGrid.showHoverOnDisabledCells

### Description
If [ListGrid.showHover](#attr-listgridshowhover) is true, should cell hover HTML be displayed on disabled cells?

**Flags**: IRW

---
## Attr: ListGrid.headerHoverStyle

### Description
This property may be set to customize the css style for the hover shown on [ListGrid.headerHover](ListGrid_2.md#method-listgridheaderhover).

**Flags**: IRW

---
## Attr: ListGrid.groupNodeStyle

### Description
The CSS style that [group](ListGrid_2.md#method-listgridgroupby) rows will have.

Note that this is not a [base style](ListGrid_2.md#method-listgridgetbasestyle), so, if this property is set, group nodes will not show stateful styling (different styles for [ListGrid.showRollOver](#attr-listgridshowrollover), [ListGrid.alternateRecordStyles](#attr-listgridalternaterecordstyles), etc). To enable stateful styling for groupNodes, set this property to `null` and specify a [ListGrid.groupNodeBaseStyle](#attr-listgridgroupnodebasestyle)

### Groups

- grouping

### See Also

- [grouping](../reference.md#kb-topic-grouping)

**Flags**: IRW

---
## Attr: ListGrid.allowRowSpanning

### Description
Should cells in this grid be allowed to span multiple rows? If set to `true`, the [ListGrid.getRowSpan](ListGrid_2.md#method-listgridgetrowspan) method will be called for every cell when rendering out the listGrid to determine how many rows the cell should span.

See [ListGrid.getRowSpan](ListGrid_2.md#method-listgridgetrowspan) for more details

**Flags**: IR

---
## Attr: ListGrid.editOnFocus

### Description
Should we start editing when this widget receives focus (if this ListGrid supports editing)?

Note that this property being set to true will cause editing to occur on a single click, even if [ListGrid.editEvent](#attr-listgrideditevent) is `"doubleClick"`, because single clicking the grid will place keyboard focus there automatically.

If this property is set together with [ListGrid.listEndEditAction](#attr-listgridlistendeditaction) being set to "next", users can create a new edit row in an empty grid by simply tabbing into the grid.

### Groups

- editing

**Flags**: IRWA

---
## Attr: ListGrid.summaryRowHeight

### Description
Default height for the [summary row autoChild](#attr-listgridsummaryrow). Note that this height is a minimum - the summary row has [ListGrid.autoFitData](#attr-listgridautofitdata) set to "vertical" so if multiple rows are visible in the grid summary, the summaryRow component will expand to accommodate them.

**Flags**: IR

---
## Attr: ListGrid.savedSearchAdminRole

### Description
Override of [SavedSearches.adminRole](SavedSearches.md#attr-savedsearchesadminrole) for this component.

**Flags**: IR

---
## Attr: ListGrid.rowRole

### Description
Returns the default WAI ARIA role for rows within this listGrid. See [ListGrid.getRowRole](ListGrid_2.md#method-listgridgetrowrole)

**Flags**: IRWA

---
## Attr: ListGrid.hideFilterEditorTitle

### Description
When [canShowFilterEditor](#attr-listgridcanshowfiltereditor) is true, this is the title for the filterEditor show/hide menu-item, in the [headerContextmenu](#attr-listgridheadercontextmenu), when the filterEditor is visible.

[showFilterEditorTitle](#attr-listgridshowfiltereditortitle) affects the same menu-item when the filterEditor is hidden.

### Groups

- filterEditor
- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.header

### Description
A Toolbar used to manager the headers shown for each column of the grid.

### Groups

- gridHeader

**Flags**: R

---
## Attr: ListGrid.editEvent

### Description
Event that will trigger inline editing, see [ListGridEditEvent](../reference.md#type-listgrideditevent) for options.

Note this setting has no effect unless [ListGrid.canEdit](#attr-listgridcanedit) has been set to enable editing.

See also [ListGrid.editOnFocus](#attr-listgrideditonfocus) and [ListGrid.startEditing](ListGrid_2.md#method-listgridstartediting).

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.hiliteReplaceValueFieldTitle

### Description
Title used for the text box shown when [ListGrid.hiliteCanReplaceValue](#attr-listgridhilitecanreplacevalue) is set.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.multiSortDialogProperties

### Description
Properties to apply to the [MultiSortDialog](MultiSortDialog.md#class-multisortdialog) which gets automatically generated when [DataBoundComponent.askForSort](DataBoundComponent.md#method-databoundcomponentaskforsort) is called.

See also [ListGrid.showHeaderSpanTitlesInSortEditor](#attr-listgridshowheaderspantitlesinsorteditor) and [ListGrid.sortEditorSpanTitleSeparator](#attr-listgridsorteditorspantitleseparator)

**Flags**: IR

---
## Attr: ListGrid.editPendingCSSText

### Description
Custom CSS text to be applied to cells with pending edits that have not yet been submitted.  
For further customization of styling for cells with pending edits use `this.editPendingBaseStyle` instead.

### Groups

- appearance

### See Also

- [ListGrid.editFailedBaseStyle](#attr-listgrideditfailedbasestyle)

**Flags**: IRWA

---
## Attr: ListGrid.preserveWhitespace

### Description
Should cells be written out with css that will preserve whitespace?

If true, depending on the value of [ListGrid.wrapCells](#attr-listgridwrapcells), the css generated for cells will use the [white-space](https://www.w3.org/wiki/CSS/Properties/white-space#Values) property values of `pre` or `pre-wrap`. This avoids collapsing sequences of whitespace without requiring special _&nbsp;_ characters.

**Flags**: IRWA

---
## Attr: ListGrid.filterButtonPrompt

### Description
The prompt to show when the mouse hovers over the Filter button in the FilterEditor.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.exportFieldAlignments

### Description
When exporting data to Excel/OpenOffice format using [ListGrid.exportData](ListGrid_2.md#method-listgridexportdata) or [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata), whether field [horizontal header alignments](ListGridField.md#attr-listgridfieldalign) and [data value alignments](ListGridField.md#attr-listgridfieldcellalign) should be replicated in the resulting spreadsheet.

If this attribute is not set, cells will be assigned a default alignment by the spreadsheet, which is typically right-aligned for numeric and date values, and left-aligned for everything else (including dates and numbers that have been exported as strings, as would be the case, for example, if [DSRequest.exportDatesAsFormattedString](DSRequest.md#attr-dsrequestexportdatesasformattedstring) is set)

**Flags**: IRW

---
## Attr: ListGrid.explicitFetchDelay

### Description
If we're showing the filterEditor ([ListGrid.showFilterEditor](#attr-listgridshowfiltereditor) is true), this property determines the delay in kicking off the filter request if the current filter values are submitted by clicking the filter button or hitting return. By default, this property is set to zero so that a filter request is immediately sent.

### Groups

- filterEditor

### See Also

- [ListGrid.fetchDelay](#attr-listgridfetchdelay)

**Flags**: IRWA

---
## Attr: ListGrid.booleanFalseImage

### Description
Image to display for a false value in a boolean field. Default `null` value or the special value "blank" means no image will be displayed.

To turn this off explicitly set [ListGridField.suppressValueIcon](ListGridField.md#attr-listgridfieldsuppressvalueicon) to true

If this, [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage) and [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage) are unset, this will be set to the default [CheckboxItem.uncheckedImage](CheckboxItem.md#attr-checkboxitemuncheckedimage).

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string. Alternatively developers can omit this property and instead use CSS directly in the [ListGrid.booleanBaseStyle](#attr-listgridbooleanbasestyle) property to provide a "boolean false" appearance.

### Groups

- imageColumns

### See Also

- [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage)
- [ListGrid.booleanPartialImage](#attr-listgridbooleanpartialimage)
- [ListGrid.printBooleanFalseImage](#attr-listgridprintbooleanfalseimage)

**Flags**: IRWA

---
## Attr: ListGrid.autoFitMaxWidth

### Description
If [ListGrid.autoFitData](#attr-listgridautofitdata) is set to `"horizontal"` or `"both"` this property provides an upper limit on how far the ListGrid will expand horizontally to accommodate its content. Value may be specified as a numeric pixel value or a percentage value.

If content exceeds this width, scrollbars will be introduced as usual. In addition to this property, [ListGrid.autoFitMaxColumns](#attr-listgridautofitmaxcolumns) allows you to limit horizontal expansion based on the number of columns to be rendered.

### Groups

- autoFitData

**Flags**: IRW

---
## Attr: ListGrid.exportDefaultBGColor

### Description
Default background color to use when exporting data to Excel/OpenOffice format using [exportData()](ListGrid_2.md#method-listgridexportdata) or [exportClientData()](ListGrid_2.md#method-listgridexportclientdata).

If unset (the default), cells that are not provided a background color by more specific APIs will be the default background color used by the spreadsheet program where they are viewed.

See [exportBGColor](../kb_topics/exportBGColor.md#kb-topic-exports--cell-background-color) for an overview.

### Groups

- exportBackgroundColor

**Flags**: IR

---
## Attr: ListGrid.exportHiddenFieldWidth

### Description
Width to size non-visible fields (which may be specified with [exportFields](DataBoundComponent.md#attr-databoundcomponentexportfields) or [DSRequest.exportFields](DSRequest.md#attr-dsrequestexportfields)) during [ListGrid.exportData](ListGrid_2.md#method-listgridexportdata) or [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata), if they have no defined numeric [width](ListGridField.md#attr-listgridfieldwidth).

### See Also

- [exportFormatting](../kb_topics/exportFormatting.md#kb-topic-exports--formatting)
- [ListGrid.exportFieldWidths](#attr-listgridexportfieldwidths)

**Flags**: IRW

---
## Attr: ListGrid.embeddedComponentMargin

### Description
This is the space to apply as margin around child-components embedded in this grid. This value is overridden on one side for [expansion components](#attr-listgridcanexpandrecords) by [expansionIndent](#attr-listgridexpansionindent) and in other scenarios by [ListGrid.embeddedComponentIndent](#attr-listgridembeddedcomponentindent).

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.useCellRollOvers

### Description
Are rollovers cell-level or row-level?

**Flags**: IRW

---
## Attr: ListGrid.animateRemoveSpeed

### Description
When [animating record removal](#attr-listgridanimateremoverecord), this property designates the speed of the animation in pixels per second. Takes precedence over the [ListGrid.animateRemoveTime](#attr-listgridanimateremovetime) property, which allows the developer to specify a duration for the animation rather than a speed.

### Groups

- animation

### See Also

- [ListGrid.animateRemoveRecord](#attr-listgridanimateremoverecord)

**Flags**: IRW

---
## Attr: ListGrid.expansionFieldImageWidth

### Description
If [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) is set to `true`, this property may be set to govern the width of the expansion image displayed to indicate whether a row is expanded. If unset, the expansionField image will be sized to match the [ListGrid.booleanImageWidth](#attr-listgridbooleanimagewidth) for this grid.

### Groups

- expansionField

**Flags**: IR

---
## Attr: ListGrid.emptyCellValue

### Description
The value to display for cells whose value is null or the empty string after applying [formatting](ListGrid_2.md#method-listgridformatcellvalue) and valueMap (if any).

This is the grid-wide attribute. You may also set the [ListGridField.emptyCellValue](ListGridField.md#attr-listgridfieldemptycellvalue) on a per-field basis.

### Groups

- cellStyling

### See Also

- [ListGrid.pendingAsyncCellValue](#attr-listgridpendingasynccellvalue)
- [ListGrid.asyncErrorCellValue](#attr-listgridasyncerrorcellvalue)
- [ListGrid.asyncMissingCellValue](#attr-listgridasyncmissingcellvalue)

**Flags**: IRW

---
## Attr: ListGrid.expansionComponentPoolingMode

### Description
The method of [component-pooling](../reference_2.md#type-recordcomponentpoolingmode) to employ for [expansionComponents](#attr-listgridcanexpandrecords).

The default mode is "destroy", which means that automatically created expansionComponents are destroyed when rows are collapsed.

**Flags**: IRWA

---
## Attr: ListGrid.valueIconRightPadding

### Description
How much padding should there be on the right of valueIcons by default

### Groups

- imageColumns

### See Also

- [ListGridField.valueIcons](ListGridField.md#attr-listgridfieldvalueicons)

**Flags**: IRW

---
## Attr: ListGrid.filterButtonProperties

### Description
If [ListGrid.showFilterEditor](#attr-listgridshowfiltereditor) is true, this attribute may be used to customize the filter button shown to the right of the filterEditor row.

**Flags**: IR

---
## Attr: ListGrid.lastCellStyle

### Description
The style to apply to the last cell in each row, when [ListGrid.styledRowEnds](#attr-listgridstyledrowends) is true. Note that this style is additional to the regular cell styling and should not introduce settings that change the layout or size of the cell, such as padding or font-size, but is ideal for setting a corner-radius or fading gradient. The styling will work with any design, and is also applied correctly with or without frozen fields.

If all you want to do is provide rounded-corners for records in this grid, it may be simpler to set [ListGrid.recordRadius](#attr-listgridrecordradius) to a CSS _border-radius_ string that achieves the rounding you want.

**Flags**: IRW

---
## Attr: ListGrid.headerHoverWrap

### Description
This property may be set to customize the `wrap` attribute for the hover shown on [ListGrid.headerHover](ListGrid_2.md#method-listgridheaderhover).

**Flags**: IRW

---
## Attr: ListGrid.autoFitTimeFields

### Description
Should listGrids automatically size time fields to fit their values or titles? If set to `"value"`, fields of type time will be rendered at the size specified by [ListGrid.defaultTimeFieldWidth](#attr-listgriddefaulttimefieldwidth). This static value is appropriate for dates rendered with the standard time formatter. If set to `"title"` or `"both"`, the drawn width of the title will be taken into account when sizing the column.

This is achieved by enabling [autoFitWidth:true](ListGridField.md#attr-listgridfieldautofitwidth) on date fields when this property is set to anything other than `"none"`, setting the [ListGridField.autoFitWidthApproach](ListGridField.md#attr-listgridfieldautofitwidthapproach) to the value specified here and having logic in [ListGrid.getDefaultFieldWidth](ListGrid_2.md#method-listgridgetdefaultfieldwidth) pick up the [ListGrid.defaultTimeFieldWidth](#attr-listgriddefaulttimefieldwidth) if appropriate.

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.exportWrapHeaderTitles

### Description
When exporting data to Excel/OpenOffice format using [ListGrid.exportData](ListGrid_2.md#method-listgridexportdata) or [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata), whether titles in the [ListGrid header](#attr-listgridheader) and [headerSpans](#attr-listgridheaderspans) should be allowed to wrap.

Excel will wrap at the column boundary automatically; for explicit control over wrapping, insert "`<br>`" tags into your titles.

See also [ListGrid.exportFieldWidths](#attr-listgridexportfieldwidths) for replicating the widths of fields in the exported spreadsheet.

**Flags**: IRW

---
## Attr: ListGrid.showHeaderContextMenu

### Description
Whether to show a context menu on the header with standard items for showing and hiding fields. Not supported for [CubeGrid](CubeGrid.md#class-cubegrid).

### Groups

- gridHeader

### See Also

- [ListGrid.displayHeaderContextMenu](ListGrid_2.md#method-listgriddisplayheadercontextmenu)
- [ListGrid.getHeaderContextMenuItems](ListGrid_2.md#method-listgridgetheadercontextmenuitems)

**Flags**: IR

---
## Attr: ListGrid.rowNumberStart

### Description
The number to start the row-count from - default value is 1.

### Groups

- rowNumberField

**Flags**: IRWA

---
## Attr: ListGrid.placeholderAIHoverContents

### Description
Message to show in the hover while AI-generated hover text is being retrieved for fields specifying an [aiHoverRequest](ListGridField.md#attr-listgridfieldaihoverrequest).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.deselectOnPartialCheckboxClick

### Description
Should partially selected checkbox be deselected or selected on click? This setting affects [header selection checkbox](#attr-listgridcanselectall), [group\\n checkboxes](#attr-listgridcanselectgroups) and folder checkbox selection in a Tree data set.

By default clicking a partially selected checkbox selects it.

### Groups

- selection

**Flags**: IRW

---
## Attr: ListGrid.rollUnderCanvas

### Description
AutoChild created and embedded in the grid if [showRollOver](#attr-listgridshowrollover) is `true`, and either [showRollOverCanvas](#attr-listgridshowrollovercanvas) is `true` and [showRollUnderCanvas](#attr-listgridshowrollundercanvas) is unset, or `showRollUnderCanvas` is explicitly set to `true`. This component will be created and displayed behind the current rollOver row or cell in the page's z-order, meaning that it will only be visible if the cell styling is transparent.

Note that if this grid has frozen fields, the [AutoChild](../reference.md#type-autochild) subsystem will use the `rollUnderCanvas` configuration settings to create the [ListGrid.frozenRollUnderCanvas](#attr-listgridfrozenrollundercanvas) (displayed in the frozen listGrid body).

The `rollUnderCanvas` has the following read-only attributes set:  
\- `this.grid` - a pointer to the grid  
\- `this.record` - a pointer to the current roll over record object in the grid

### Groups

- rowEffects

**Flags**: RA

---
## Attr: ListGrid.groupNodeBaseStyle

### Description
[Base style](ListGrid_2.md#method-listgridgetbasestyle) for [group](ListGrid_2.md#method-listgridgroupby) rows.

Note that this property has no effect if [ListGrid.groupNodeStyle](#attr-listgridgroupnodestyle) is non null.

### Groups

- grouping

### See Also

- [grouping](../reference.md#kb-topic-grouping)

**Flags**: IRW

---
## Attr: ListGrid.animateSelection

### Description
If the [selectionCanvas](#attr-listgridselectioncanvas) is enabled, setting this property to `true` ensures that when the `selectionCanvas` is displayed it is animated into view via [Canvas.animateShow](Canvas.md#method-canvasanimateshow). Note that the animation effect may be customized via [Canvas.animateShowEffect](Canvas.md#attr-canvasanimateshoweffect), [Canvas.animateShowTime](Canvas.md#attr-canvasanimateshowtime) and [Canvas.animateShowAcceleration](Canvas.md#attr-canvasanimateshowacceleration) set in `selectionCanvasProperties`.

### Groups

- rowEffects

### See Also

- [ListGrid.animateSelectionUnder](#attr-listgridanimateselectionunder)

**Flags**: IRWA

---
## Attr: ListGrid.removeFieldTitle

### Description
The title to use for the [remove field](#attr-listgridremovefielddefaults).

By default this title is not displayed in the remove column header button as the [ListGrid.removeFieldDefaults](#attr-listgridremovefielddefaults) sets [ListGridField.showTitle](ListGridField.md#attr-listgridfieldshowtitle) to `false`.

**Flags**: IRWA

---
## Attr: ListGrid.alternateFieldFrequency

### Description
The number of consecutive columns to draw in the same style before alternating, when [alternateColumnStyles](GridRenderer.md#attr-gridrendereralternatecolumnstyles) is true.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: ListGrid.editByCell

### Description
Determines whether when the user edits a cell in this listGrid the entire row becomes editable, or just the cell that received the edit event.

No effect if this.canEdit is false or null.

### Groups

- editing

### See Also

- [ListGrid.canEdit](#attr-listgridcanedit)

**Flags**: IRW

---
## Attr: ListGrid.headerHoverVAlign

### Description
This property may be set to customize the vertical alignment for the hover shown on [ListGrid.headerHover](ListGrid_2.md#method-listgridheaderhover).

**Flags**: IRW

---
## Attr: ListGrid.filterViaAIMode

### Description
If filtering of the grid is enabled and AI [is enabled](AI.md#classmethod-aiisenabled), filtering-via-AI can be enabled by setting the [AIServiceMode](../reference.md#type-aiservicemode) to use.

**Flags**: IR

---
## Attr: ListGrid.headerMenuButtonConstructor

### Description
Constructor for the [ListGrid.headerMenuButton](#attr-listgridheadermenubutton). If unset a standard "Button" will be rendered out. Note that this property may be overridden by different skins.

### Groups

- headerMenuButton

**Flags**: IRA

---
## Attr: ListGrid.expansionLayout

### Description
Automatically generated [VLayout](../reference.md#class-vlayout) which fills a record's expanded section and contains other builtin [expansion-components](../reference_2.md#type-expansionmode). You can also override [getExpansionComponent()](ListGrid_2.md#method-listgridgetexpansioncomponent) to provide components of your own specification.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `listGrid.expansionLayoutProperties` and `listGrid.expansionLayoutDefaults`.

Note, however, that this is a multi-instance component (potentially one per record), so it is created using [createAutoChild()](Class.md#method-classcreateautochild) not [addAutoChild()](Class.md#method-classaddautochild), and no default single instance is created by name on the grid.

### Groups

- expansionField

**Flags**: RA

---
## Attr: ListGrid.rowRangeFormat

### Description
Dynamic String specifying the format for the [visible row range](ListGrid_2.md#method-listgridgetformattedrowrange).

The following variables are available for evaluation within this string:

*   `startRow`: first visible row in the viewport as a [formatted string](NumberUtil.md#classmethod-numberutiltolocalizedstring)
*   `endRow`: last visible row in the viewport as a [formatted string](NumberUtil.md#classmethod-numberutiltolocalizedstring)

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.clearFilterViaAIText

### Description
Title for the menu-item displayed in this component's header context-menu when [AI-assisted filtering](#attr-listgridfilterviaaimode) is allowed and an AI filter in already in effect.

### Groups

- ai
- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.defaultFilterOperatorSuffix

### Description
Text to show after the name of the default filterOperator in the [headerContextMenu](#attr-listgridshowheadercontextmenu) when [ListGrid.allowFilterOperators](#attr-listgridallowfilteroperators) is enabled.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.headerHoverAlign

### Description
This property may be set to customize the alignment for the hover shown on [ListGrid.headerHover](ListGrid_2.md#method-listgridheaderhover).

**Flags**: IRW

---
## Attr: ListGrid.showGridSummary

### Description
Should this ListGrid show a summary row beneath the last record of the grid. This summary row will contain per-field summary information. See [ListGridField.showGridSummary](ListGridField.md#attr-listgridfieldshowgridsummary) and [ListGrid.getGridSummaryFunction](ListGrid_2.md#method-listgridgetgridsummaryfunction) for details on how the summary value to be displayed for each column will be calculated.

Note that the [summaryRow autoChild](#attr-listgridsummaryrow) will be created to actually display the summary row.

**Flags**: IRW

---
## Attr: ListGrid.sortDirection

### Description
Sorting direction of this ListGrid. If specified when the ListGrid is initialized, this property will be the default sorting direction for the [ListGrid.sortField](#attr-listgridsortfield). May be overridden by specifying [ListGridField.sortDirection](ListGridField.md#attr-listgridfieldsortdirection).

After initialization, this property will be updated on [ListGrid.sort](ListGrid_2.md#method-listgridsort) or [ListGrid.setSort](ListGrid_2.md#method-listgridsetsort) to reflect the current sort direction of the grid. When this grid is sorted by multiple fields, the grid's sortDirection reflects the sort direction of the primary sort field.

Note: A side effect of [ListGrid.setSort](ListGrid_2.md#method-listgridsetsort) is that it updates the grid's `sortDirection` to the direction of the first sort. In particular, if there is an [ListGrid.initialSort](#attr-listgridinitialsort) or [ListGrid.sortField](#attr-listgridsortfield), then `sortDirection` will be updated during initialization to the direction of the first sort.

### Groups

- sorting

### See Also

- [SortDirection](../reference_2.md#type-sortdirection)

**Flags**: IRW

---
## Attr: ListGrid.canSelectGroups

### Description
Controls whether a checkbox for selecting [groups](ListGrid_2.md#method-listgridgroupby) appears in the group node if [SelectionAppearance](../reference.md#type-selectionappearance) is set to `"checkbox"`

### Groups

- selection

**Flags**: IRW

---
## Attr: ListGrid.canTabToSorter

### Description
Should the [corner sort button](#attr-listgridsorterconstructor) be included in the tab-order for the page?

### Groups

- accessibility

**Flags**: IR

---
## Attr: ListGrid.configureGroupingText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, and multi-grouping is enabled, this attribute is used as the title for a menu item that opens a [MultiGroupDialog](MultiGroupDialog.md#class-multigroupdialog) to configure the grouping for this grid.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.fields

### Description
An array of field objects, specifying the order, layout, formatting, and sorting behavior of each field in the listGrid object. In ListGrids, the fields array specifies columns. Each field in the fields array is a ListGridField object. Any listGrid that will display data should have at least one visible field.

If [ListGrid.dataSource](#attr-listgriddatasource) is also set, this value acts as a set of overrides as explained in [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields).

Note: grids with [useAllDataSourceFields:true](#attr-listgridusealldatasourcefields) will render the full set of dataSource fields in the order in which they are defined in the dataSource - in this usage the component fields array is just a way to customize the appearance of individual fields.

Grids with [canPickOmittedFields:true](#attr-listgridcanpickomittedfields) will only show the explicitly specified set of fields, but will similarly show them in the order in which they're defined within the dataSource.

### Groups

- databinding

### See Also

- [ListGridField](../reference_2.md#object-listgridfield)
- [ListGrid.setFields](ListGrid_2.md#method-listgridsetfields)

**Flags**: IRW

---
## Attr: ListGrid.animateFolderMaxRows

### Description
If [ListGrid.animateFolders](#attr-listgridanimatefolders) is true for this grid, this number can be set to designate the maximum number of rows to animate at a time when opening / closing a folder.

For a ListGrid, this property applies when [grouping](#attr-listgridcangroupby) is enabled.

### Groups

- animation

### See Also

- [TreeGrid.getAnimateFolderMaxRows](TreeGrid.md#method-treegridgetanimatefoldermaxrows)

**Flags**: IRW

---
## Attr: ListGrid.wrapHeaderTitles

### Description
If [ListGridField.wrap](ListGridField.md#attr-listgridfieldwrap) is not explicitly set, should fields wrap? If autofitting, see the docs on that property for the details of how the minimum width for a field is determined.

### See Also

- [ListGrid.minFieldWidth](#attr-listgridminfieldwidth)
- [ListGrid.headerBaseStyle](#attr-listgridheaderbasestyle)

**Flags**: IR

---
## Attr: ListGrid.canReorderFields

### Description
Indicates whether fields in this listGrid can be reordered by dragging and dropping header fields. If true, can be overridden at the field level via [ListGridField.canReorder](ListGridField.md#attr-listgridfieldcanreorder).

### Groups

- dragging

**Flags**: IRW

---
## Attr: ListGrid.filterViaAIPanelInstructions

### Description
The instruction text to display above the "Filter via AI" text box.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.groupByField

### Description
List of fields to group grid records. If only a single field is used, that field may be specified as a string. After initialization, use [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby) to update the grouping field list, instead of modifying groupByField directly.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IR

---
## Attr: ListGrid.bodyOverflow

### Description
Overflow setting for the "body", that is, the area of the grid where data values are rendered.

**This is a very advanced setting** which is typically only changed by subclasses of ListGrid which never show a header. To achieve auto-fitting, instead use properties such as [ListGrid.autoFitData](#attr-listgridautofitdata), [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths) and [ListGrid.fixedRecordHeights](#attr-listgridfixedrecordheights).

### Groups

- sizing

**Flags**: IRWA

---
## Attr: ListGrid.leaveScrollbarGap

### Description
Whether to leave a gap for the vertical scrollbar, even when it's not present.

Note that if leaveScrollbarGap is false and vertical scrolling is introduced, fields will be resized to fit the smaller body area if possible, in order to avoid horizontal scrolling also being required.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.enumCriteriaAsInitialValues

### Description
In a ListGrid that has a DataSource and has filter criteria that include values for fields declared as [type "enum"](../reference_2.md#type-fieldtype) in the DataSource, by default a newly edited row will use those filter criteria as initial values.

For example, if a ListGrid is showing all Accounts that have status:"Active" and a new row is created, the new row will default to status:"Active" unless this flag is set to false.

### Groups

- editing

**Flags**: IR

---
## Attr: ListGrid.headerHeight

### Description
The height of this listGrid's header, in pixels.

### Groups

- gridHeader
- sizing

**Flags**: IRW

---
## Attr: ListGrid.canPickOmittedFields

### Description
If true, the [field picker menu](#attr-listgridcanpickfields) will include entries for all dataSource fields, including those not included in the specified [fields array](#attr-listgridfields).

This property only applies to grids with a specified [ListGrid.dataSource](#attr-listgriddatasource), where [ListGrid.fields](#attr-listgridfields) is explicitly set and [ListGrid.useAllDataSourceFields](#attr-listgridusealldatasourcefields) is false. The [ListGrid.canPickFields](#attr-listgridcanpickfields) property must also be set to true to allow the user to view the field picker menu.

**Note: grids with `canPickOmittedFields:true`, like those with [useAllDataSourceFields:true](#attr-listgridusealldatasourcefields) will render fields in the order in which they are defined in the dataSource rather than the order in which they're defined in the [listGrid fields array](#attr-listgridfields).**

**Flags**: IR

---
## Attr: ListGrid.applyRowCountToLength

### Description
This property allows developers to explicitly set [ResultSet.applyRowCountToLength](ResultSet.md#attr-resultsetapplyrowcounttolength) for this grid's data object.

If not explicitly specified this will be derived from [ListGrid.canRequestRowCount](#attr-listgridcanrequestrowcount)

### Groups

- rowRangeDisplay

**Flags**: IRW

---
## Attr: ListGrid.chartType

### Description
Default type of chart to plot.

**Flags**: IRW

---
## Attr: ListGrid.headerSpans

### Description
Header spans are a second level of headers that appear above the normal ListGrid headers, spanning one or more listGrid fields in a manner similar to a column-spanning cell in an HTML table.

A header span can be created by simply naming the fields the header should span. The example below creates a headerSpan that spans the first two fields of the ListGrid.

```
    isc.ListGrid.create({
        headerHeight:40,
        fields : [
            { name:"field1" },
            { name:"field2" },
            { name:"field3" }
        ],
        headerSpans : [
            {
                fields: ["field1", "field2"],
                title: "Field 1 and 2"
            }
        ]
    });
 
```
Header spans can be nested, allowing fields to be grouped by multiple levels of granularity. See [HeaderSpan.spans](HeaderSpan.md#attr-headerspanspans) for further information on nesting spans.

Header spans will automatically react to resizing of the headers they span, and will be hidden automatically when all of the spanned fields are hidden.

Header spans appear in the [header](#attr-listgridheader) area of the ListGrid, sharing space with the existing headers, so it's typical to set [ListGrid.headerHeight](#attr-listgridheaderheight) to approximately double its normal height when using headerSpans, or if using nested header spans, the default header height multiplied by the number of levels of header spans to be shown.

See [HeaderSpan](../reference_2.md#object-headerspan) for many properties that allow the control of the appearance of headerSpans. Note that headerSpans are created via the [AutoChild](../reference.md#type-autochild) pattern, hence you can change the SmartClient component being used, or any of its properties.

Neither headerSpans themselves nor the fields within them may be drag reordered, but other unspanned headers may be.

A span can only span adjacent fields - if a span is defined and the spanned fields don't sit next to each other in the specified fields array, the fields array will be automatically reordered to match the order specified in the span's [HeaderSpan.fields](HeaderSpan.md#attr-headerspanfields) array.

Note that headerSpans primarily provide a visual cue for grouping multiple headers together. If you have an OLAP, data "cube" or multi-dimensional data model, the [CubeGrid](CubeGrid.md#class-cubegrid) component is the right choice.

### Groups

- headerSpan

**Flags**: IRW

---
## Attr: ListGrid.filterViaAIText

### Description
Title for the menu-item displayed in this component's header context-menu when [AI-assisted filtering](#attr-listgridfilterviaaimode) is allowed.

### Groups

- ai
- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.filterUsingText

### Description
Text for the menu item shown in the [headerContextMenu](#attr-listgridshowheadercontextmenu) when [ListGrid.allowFilterOperators](#attr-listgridallowfilteroperators) is enabled.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.savedSearchAdminSeparator

### Description
Properties for the separator record between locally saved and admin searches.

**Flags**: IR

---
## Attr: ListGrid.showDetailFields

### Description
Whether to include fields marked `detail:true` from this component's `DataSource`.

When this property is `true`, the `ListGrid` will include all detail fields unless fields have been specifically declared using the [ListGrid.fields](#attr-listgridfields) array.

Any field which has been included directly in the `fields` array will be included regardless of the fields `detail` attribute.

Detail fields included will initially be hidden but the user may show these fields via the default header context menu ([ListGrid.showHeaderContextMenu](#attr-listgridshowheadercontextmenu)).

The field's visibility can also be overridden programatically using the standard [ListGrid.showField](ListGrid_2.md#method-listgridshowfield), [ListGrid.hideField](ListGrid_2.md#method-listgridhidefield) and [ListGridField.showIf](ListGridField.md#method-listgridfieldshowif) APIs, for example, set showIf:"true" to show a detail field initially.

Setting this property to false will completely exclude all detail fields from the list grid's fields array, such that they cannot be shown by the user or programmatically.

### Groups

- databinding

**Flags**: IR

---
## Attr: ListGrid.showBackgroundComponents

### Description
If `true` this grid will create and show per-row backgroundComponents as detailed [here](#attr-listgridbackgroundcomponent).

**Flags**: IRW

---
## Attr: ListGrid.autoFetchRowCount

### Description
Depending on whether [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading) is active, the exact count of available rows may not be available as part of the standard data fetch response - setting `autoFetchRowCount:true` will cause a fetch for an accurate row count to be issued as soon as data arrives (from a [progressive dataSource response](DSResponse.md#attr-dsresponseprogressiveloading)) without an accurate row count. This value will then be available for display in the [RowRangeDisplay](RowRangeDisplay.md#class-rowrangedisplay) label.

To allow users to request an accurate row count by clicking the [RowRangeDisplay](RowRangeDisplay.md#class-rowrangedisplay) instead of kicking off a row count fetch automatically, use [ListGrid.canRequestRowCount](#attr-listgridcanrequestrowcount).

The `autoFetchRowCount` value will be passed through to the [ResultSet data object](ResultSet.md#attr-resultsetautofetchrowcount) which is responsible for issuing the row count fetch(es) at appropriate times.

### Groups

- rowCountDisplay

**Flags**: IRW

---
## Attr: ListGrid.poolComponentsPerColumn

### Description
Should recycled [record components](#attr-listgridshowrecordcomponents), be pooled per column or per record. Only applies if [ListGrid.showRecordComponentsByCell](#attr-listgridshowrecordcomponentsbycell) is true.

When [ListGrid.recordComponentPoolingMode](#attr-listgridrecordcomponentpoolingmode) is "recycle" and you have components of different types in different columns, set this property to true to ensure that components intended for one column are not recycled for use in another column that should have a different component.

If no components applicable to a particular column are available in the pool, the system calls [createRecordComponent](ListGrid_2.md#method-listgridcreaterecordcomponent).

### Groups

- recordComponents

**Flags**: IRW

---
## Attr: ListGrid.locateRowsBy

### Description
When [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) is used to parse locator strings generated by [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) for a cell in this grid, how should the row be identified?  
Note that getLocator() will actually store all available information about the row in the generated string -- this attribute effects how a stored string will be parsed only.

Valid options area:

*   `"primaryKey"` Only applies to databound grids: If the cell in question has a primary key cell value, use it to identify cells in autoTest locator strings.
*   `"titleField"` If the cell in question has a value for the [titleField](ListGrid_2.md#method-listgridgettitlefield), use it to identify cells in autoTest locator strings
*   `"targetCellValue"` Identify rows by storing the cell value for the target row / field in autoTest locator strings
*   `"cellValue"` Use the value of a specific cell to identify the row. The [ListGrid.rowLocatorField](#attr-listgridrowlocatorfield) attribute may be used to specify the field from which the cellValue should be retrieved.
*   `"index"`The rowNum will be used to identify the row.

If unset, default behavior depends on what information is available in the locator passed to [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement).

If a primaryKey value was recorded (and this grid has a primary key field), it will be used to identify the target row. Otherwise the system will back off to use the titleField (if present in the locator), then the cell value (if present in the locator), and lastly the recorded index.

### Groups

- autoTest

### See Also

- [LocatorStrategy](../reference_2.md#type-locatorstrategy)

**Flags**: IRW

---
## Attr: ListGrid.editOnF2Keypress

### Description
Should we start editing when the widget has focus and the user presses the "f2" key (if this ListGrid supports editing)?

Note that if [ListGrid.editEvent](#attr-listgrideditevent) is set to `"click"` or `"doubleClick"`, the `Space` or `Enter` key may also be used to start editing, depending on the value for [ListGrid.generateClickOnSpace](#attr-listgridgenerateclickonspace), [ListGrid.generateDoubleClickOnSpace](#attr-listgridgeneratedoubleclickonspace), [ListGrid.generateClickOnEnter](#attr-listgridgenerateclickonenter) and [ListGrid.generateDoubleClickOnEnter](#attr-listgridgeneratedoubleclickonenter).

If [ListGrid.canEdit](#attr-listgridcanedit) is false, or [ListGrid.editEvent](#attr-listgrideditevent) is set to "none" this property has no effect.

### Groups

- editing

**Flags**: IRWA

---
## Attr: ListGrid.quickDrawAheadRatio

### Description
Alternative to [ListGrid.drawAheadRatio](#attr-listgriddrawaheadratio), to be used when the user is rapidly changing the grids viewport (for example drag scrolling through the grid). If unspecified [ListGrid.drawAheadRatio](#attr-listgriddrawaheadratio) will be used in all cases

### Groups

- performance

**Flags**: IRW

---
## Attr: ListGrid.recordCanRemoveProperty

### Description
If set to false on a record and [canRemoveRecords](#attr-listgridcanremoverecords) is true, removal of that record is disallowed in the UI. The icon in the remove field is not shown.

### Groups

- editing

**Flags**: IRA

---
## Attr: ListGrid.alternateRecordFrequency

### Description
The number of consecutive rows to draw in the same style before alternating, when [alternateRowStyles](GridRenderer.md#attr-gridrendereralternaterowstyles) is true.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: ListGrid.selection

### Description
The [Selection object](../kb_topics/selection.md#kb-topic-selection) associated with the `ListGrid`.

### Groups

- selection

**Deprecated**

**Flags**: RA

---
## Attr: ListGrid.nullGroupTitle

### Description
Default alias to use for groups with no value

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IRW

---
## Attr: ListGrid.showHeaderSpanTitlesInFormulaBuilder

### Description
If this grid has specified [headerSpans](#attr-listgridheaderspans), should field titles be prefixed with the titles of the headerSpans in which they are contained when using the [FormulaBuilder](FormulaBuilder.md#class-formulabuilder) or [SummaryBuilder](SummaryBuilder.md#class-summarybuilder).

### See Also

- [ListGrid.formulaBuilderSpanTitleSeparator](#attr-listgridformulabuilderspantitleseparator)

**Flags**: IRW

---
## Attr: ListGrid.dataPageSize

### Description
When using [data paging](#attr-listgriddatafetchmode), how many records to fetch at a time. If set to a positive integer, `dataPageSize` will override the default [resultSize](ResultSet.md#attr-resultsetresultsize) for ResultSets automatically created when you call [fetchData()](ListGrid_2.md#method-listgridfetchdata) (and similarly for the [resultSize](ResultTree.md#attr-resulttreeresultsize) of ResultTrees). Leaving `dataPageSize` at its default means to just use the default page size of the data container.

**Note** that regardless of the `dataPageSize` setting, a component will always fetch all of data that it needs to draw. Settings such as [showAllRecords:true](#attr-listgridshowallrecords), [drawAllMaxCells](#attr-listgriddrawallmaxcells) and [drawAheadRatio](#attr-listgriddrawaheadratio) can cause more rows than the configured `dataPageSize` to be fetched.

### Groups

- performance

### See Also

- [ResultSet.resultSize](ResultSet.md#attr-resultsetresultsize)

**Flags**: IRW

---
## Attr: ListGrid.screenReaderWriteRowLabelledBy

### Description
When [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode) is enabled, for grids with [ListGrid.ariaRole](#attr-listgridariarole) set to `"list"`, should a custom [aria-labelledby](https://developer.mozilla.org/en-US/docs/Web/Accessibility/ARIA/ARIA_Techniques/Using_the_aria-labelledby_attribute) attribute be written out in addition to any other [row aria properties](ListGrid_2.md#method-listgridgetrowariastate) to ensure the [column titles](#attr-listgridscreenreaderincludefieldtitles), [ListGrid.screenReaderCellSeparator](#attr-listgridscreenreadercellseparator) and [ListGrid.screenReaderRowSeparator](#attr-listgridscreenreaderrowseparator) are read out along with cell content when reading rows?

Setting this property to false will disable the writing out of this `labelled-by` attribute. See the documentation for [ListGrid.screenReaderCellSeparator](#attr-listgridscreenreadercellseparator) for more on how the header values, cell separators and row separators are picked up by screenreaders in this mode.

For more information on the ARIA attributes generated by ListGrids, see [ListGrid.ariaRole](#attr-listgridariarole).

### Groups

- accessibility

**Flags**: IRA

---
## Attr: ListGrid.showClippedHeaderTitlesOnHover

### Description
If true and a header button's title is clipped, then a hover containing the full field title is enabled.

### Groups

- hovers

### See Also

- [ListGrid.headerTitleClipped](ListGrid_2.md#method-listgridheadertitleclipped)
- [ListGrid.headerHoverHTML](ListGrid_2.md#method-listgridheaderhoverhtml)

**Flags**: IRA

---
## Attr: ListGrid.expansionFieldImageHeight

### Description
If [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) is set to `true`, this property may be set to govern the height of the expansion image displayed to indicate whether a row is expanded. If unset, the expansionField image will be sized to match the [ListGrid.booleanImageHeight](#attr-listgridbooleanimageheight) for this grid.

### Groups

- expansionField

**Flags**: IR

---
## Attr: ListGrid.recordShowRollOverProperty

### Description
Name of the property that can be set on a per-record basis to disabled rollover for an individual record when [ListGrid.showRollOver](#attr-listgridshowrollover) is true.

### Groups

- appearance

**Flags**: IR

---
## Attr: ListGrid.expansionCanEdit

### Description
For [expansionModes](../reference_2.md#type-expansionmode) that show another grid or tree, is that component editable?

The default value for this property is `false`.

### Groups

- expansionField

**Flags**: IRWA

---
## Attr: ListGrid.unspannedHeaderVAlign

### Description
When [headerSpans](#attr-listgridheaderspans) are in use, this property sets the default vertical alignment for fields which do **not** have a headerSpan.

### Groups

- headerSpan

**Flags**: IR

---
## Attr: ListGrid.aiHoverContentsPrefix

### Description
Optional prefix for the AI-generated hover text displayed when hovering over fields specifying an [aiHoverRequest](ListGridField.md#attr-listgridfieldaihoverrequest).

This can be overridden per-field by [ListGridField.aiHoverContentsPrefix](ListGridField.md#attr-listgridfieldaihovercontentsprefix).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.canExpandRecordProperty

### Description
Property name on a record that will be checked to determine whether a record can be expanded.

### Groups

- expansionField

### See Also

- [ListGridRecord.canExpand](ListGridRecord.md#attr-listgridrecordcanexpand)

**Flags**: IR

---
## Attr: ListGrid.unfreezeFieldText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid and [this.canFreezeFields](#attr-listgridcanfreezefields) is true, this string will be shown as the title for the menu item to unfreeze a currently frozen field.

This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `title` available as a variable containing the field title.

Default value returns "Unfreeze " + the field's summary title.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: ListGrid.selectionType

### Description
Defines a listGrid's clickable-selection behavior.

The default selection appearance is governed by [ListGrid.selectionAppearance](#attr-listgridselectionappearance): if selectionAppearance is "checkbox", this will be "simple", otherwise, this will be "multiple".

### Groups

- selection
- appearance

### See Also

- [SelectionStyle](../reference.md#type-selectionstyle)

**Flags**: IRW

---
## Attr: ListGrid.groupState

### Description
Initial group state for the grid.

[ListGrid.viewState](#attr-listgridviewstate) can be used to initialize all view properties of the grid. When doing so, `groupState` is not needed because `viewState` includes it as well. If both are provided, `groupState` has priority for group state.

To retrieve current state call [getGroupState](ListGrid_2.md#method-listgridgetgroupstate).

### Groups

- viewState

**Flags**: IRW

---
## Attr: ListGrid.minimumCellHeight

### Description
Minimum height for ListGrid cells, settable by the skin, based on the size of the checkbox media used for boolean fields plus minimal surrounding padding. `minimumCellHeight` is used by [Canvas.resizeControls](Canvas.md#classmethod-canvasresizecontrols) to avoid shrinking ListGrid rows so much that correct display is impossible. Do not set minimumCellHeight on a per-instance basis - it's only for use in custom skins.

**Flags**: IR

---
## Attr: ListGrid.hiliteHTMLAfterFormat

### Description
If set to true, custom HTML applied as part of hiliting will be applied after [formatting](ListGrid_2.md#method-listgridformatcellvalue) for each cell. If false, hilite HTML will be applied before formatting.

This applies to the following hilite properties:

*   [Hilite.replacementValue](Hilite.md#attr-hilitereplacementvalue)
*   [Hilite.htmlBefore](Hilite.md#attr-hilitehtmlbefore)
*   [Hilite.htmlAfter](Hilite.md#attr-hilitehtmlafter)
*   [Hilite.htmlValue](Hilite.md#attr-hilitehtmlvalue)

May be overridden per field via [ListGridField.hiliteHTMLAfterFormat](ListGridField.md#attr-listgridfieldhilitehtmlafterformat)

**Flags**: IR

---
## Attr: ListGrid.bodyStyleName

### Description
CSS style used for the body of this grid. If applying a background-color to the body via a CSS style applied using this property, be sure to set [ListGrid.bodyBackgroundColor](#attr-listgridbodybackgroundcolor) to `null`.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.defaultEditableDateTimeFieldWidth

### Description
Default width for editable datetime type fields. See [ListGrid.autoFitDateFields](#attr-listgridautofitdatefields) for details on how this property is used.

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.editFailedCSSText

### Description
Custom CSS text to be applied to cells when editing has failed.  
If this listGrid is editable, this css text will be applied to any edited cells for which validation failed, on top of the base style for the cell.  
For further customization of styling for cells that failed editing validation, use `this.editFailedBaseStyle` instead.

### Groups

- appearance

### See Also

- [ListGrid.editFailedBaseStyle](#attr-listgrideditfailedbasestyle)

**Flags**: IRWA

---
## Attr: ListGrid.separatorRowStyle

### Description
CSS class to apply to rows marked as [separators](#attr-listgridisseparatorproperty) in this grid. The default behavior is to draw a line by rendering an `<HR>` tag, and the class applied to this attribute may be used to style that tag, for example by applying a _border-top_ setting.

**Flags**: IRW

---
## Attr: ListGrid.gridAdditionalCriteriaText

### Description
The additional criteria prefix to show in filter editor field hover, the filter action button or the sorter button before the descriptive version of the [ListGrid.filterWindowCriteria](#attr-listgridfilterwindowcriteria), if any. The descriptive text is formatted by [DataSource.getAdvancedCriteriaDescription](DataSource.md#classmethod-datasourcegetadvancedcriteriadescription).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.headerMenuButtonIcon

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, this property governs the icon shown on the auto-generated `headerMenuButton`

### Groups

- headerMenuButton

**Flags**: IRA

---
## Attr: ListGrid.selectionUnderCanvas

### Description
AutoChild created and embedded in the grid if [showSelectionCanvas](#attr-listgridshowselectioncanvas) is `true` and [showSelectionUnderCanvas](#attr-listgridshowselectionundercanvas) is unset, or `showSelectionUnderCanvas` is explicitly set to `true`, and the [selectionType](#attr-listgridselectiontype) is "single". This component will be created and displayed behind the selected record whenever the selection changes.

The `selectionUnderCanvas` has the following read-only attributes set:  
\- `this.grid` - a pointer to the grid  
\- `this.record` - a pointer to the currently selected record object in the grid

### Groups

- rowEffects

### See Also

- [ListGrid.selectionCanvas](#attr-listgridselectioncanvas)

**Flags**: RA

---
## Attr: ListGrid.autoFitIconFields

### Description
SmartClient listGrids have special logic to automatically size fields that are displayed as an icon - that is fields with [type:"icon"](../reference.md#type-listgridfieldtype), fields displaying only [value icons](ListGridField.md#attr-listgridfieldshowvalueicononly), and boolean fields (which are rendered as a checkmark type icon by default.

This attribute controls this behavior - governing whether icon fields should be sized to fit their content (icon), title, or whether to disable this behavior. Setting this value to `"title"` or `"iconWidth"` will cause [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth) to be enabled by default for all icon fields with the [ListGridField.autoFitWidthApproach](ListGridField.md#attr-listgridfieldautofitwidthapproach) set to `"value"` or `"both"` as appropriate. Note that the width required for the icons is calculated by [ListGrid.getDefaultFieldWidth](ListGrid_2.md#method-listgridgetdefaultfieldwidth) which performs a simple calculation based on the specified icon width for these types of fields.

This setting governs default behavior for icon fields - for specific fields within a grid, this default behavior can be overridden by setting an explicit [ListGridField.width](ListGridField.md#attr-listgridfieldwidth) or explicitly enabling [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth) and setting [ListGridField.autoFitWidthApproach](ListGridField.md#attr-listgridfieldautofitwidthapproach) on the field in question.

### Groups

- autoFitFields

### See Also

- [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths)

**Flags**: IRW

---
## Attr: ListGrid.confirmDiscardEdits

### Description
For editable listGrids, outstanding unsaved edits when the user performs a new filter or sort will be discarded. This flag determines whether we should display a confirmation dialog with options to save or discard the edits, or cancel the action in this case.

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.canDragRecordsOut

### Description
Indicates whether records can be dragged from this listGrid and dropped elsewhere.

**NOTE:** If `canDragRecordsOut` is initially enabled or might be dynamically enabled after the grid is created, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging a record starts a drag operation rather than a scroll, but see the discussion of [drag handles](ListGrid_2.md#method-listgridshowdraghandles). If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag and drop of records out of the grid.

### Groups

- dragging

### See Also

- [ListGridRecord.canDrag](ListGridRecord.md#attr-listgridrecordcandrag)
- [ListGridRecord.canAcceptDrop](ListGridRecord.md#attr-listgridrecordcanacceptdrop)
- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)

**Flags**: IRW

---
## Attr: ListGrid.headerHoverHeight

### Description
Optional default height for the hover shown on [ListGrid.headerHover](ListGrid_2.md#method-listgridheaderhover).

**Flags**: IRW

---
## Attr: ListGrid.removeIconSize

### Description
Default width and height of [remove icons](#attr-listgridremoveicon) for this ListGrid.

**Flags**: IRW

---
## Attr: ListGrid.valueIconWidth

### Description
Width for value icons for this listGrid. Overrides [ListGrid.valueIconSize](#attr-listgridvalueiconsize). Can be overridden at the field level

### Groups

- imageColumns

**Flags**: IRW

---
## Attr: ListGrid.canAutoFitFields

### Description
Can the user perform one-time autofit for specific columns in this grid?

If set to true, the default header menu will include options to auto fit [all fields](#attr-listgridautofitalltext) such that they fit their content or titles as specified via [ListGridField.autoFitWidthApproach](ListGridField.md#attr-listgridfieldautofitwidthapproach).  
Autofitting of individual fields via a [header context menu item](#attr-listgridautofitfieldtext), or the [ListGrid.headerAutoFitEvent](#attr-listgridheaderautofitevent) will also be enabled when this property is set unless [ListGridField.canAutoFitWidth](ListGridField.md#attr-listgridfieldcanautofitwidth) is explicitly set to false

Note that the ability to perform one-time autofitting of fields via this subsystem is separate from the programmatic autofit behavior enabled via [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths).

This subsystem is requires canResizeFields be enabled and will be disabled if that property is set to false

### Groups

- autoFitFields

**Flags**: IRW

---
## Attr: ListGrid.sortNumeralMenuButtonSpaceOffset

### Description
When [ListGrid.leaveHeaderMenuButtonSpace](#attr-listgridleaveheadermenubuttonspace) is true, configures the amount of space beyond the [ListGrid.headerMenuButtonWidth](#attr-listgridheadermenubuttonwidth) on the right side of a ListGrid header button (left for [RTL mode](Page.md#classmethod-pageisrtl)) to reserve for the sort numeral if [multi-sorting](#attr-listgridcanmultisort) is active for that field and the numeral will be shown. May be increased for more separation between the title text and the sort arrow when multi-sorting.

Note that larger values may required if 10 or more fields are sorted at once, as the numeral will occupy more space. This value may need to be customized in your skin or if [ListGrid.sortAscendingImage](#attr-listgridsortascendingimage) or [ListGrid.sortDescendingImage](#attr-listgridsortdescendingimage) are changed.

### See Also

- [ListGrid.sortArrowMenuButtonSpaceOffset](#attr-listgridsortarrowmenubuttonspaceoffset)

**Flags**: IRW

---
## Attr: ListGrid.asynchGroupingPrompt

### Description
The prompt to display while interactivity is blocked during [asynchronous grouping](#attr-listgridgroupbyasyncthreshold).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.wrapCells

### Description
Should content within cells be allowed to wrap?

Even if content is allowed to wrap, if [ListGrid.fixedRecordHeights](#attr-listgridfixedrecordheights) is set, the content will be clipped off at the cell boundary. Either set a larger, fixed [ListGrid.cellHeight](#attr-listgridcellheight) to reveal more content, or set [ListGrid.fixedRecordHeights](#attr-listgridfixedrecordheights) to false to allow auto-sizing.

**Flags**: IRWA

---
## Attr: ListGrid.showHeaderShadow

### Description
Should the header show a drop-shadow? Shadow will be applied to the header, or for a grid with frozen columns, the header layout.

Header shadow will only be displayed if [css shadows](Canvas.md#attr-canvasusecssshadow) are being used.

### See Also

- [ListGrid.headerShadowVOffset](#attr-listgridheadershadowvoffset)
- [ListGrid.headerShadowHOffset](#attr-listgridheadershadowhoffset)
- [ListGrid.headerShadowSoftness](#attr-listgridheadershadowsoftness)
- [ListGrid.headerShadowColor](#attr-listgridheadershadowcolor)

**Flags**: IRW

---
## Attr: ListGrid.normalBaseStyle

### Description
"Normal" baseStyle for this listGrid. Only applies if [ListGrid.baseStyle](#attr-listgridbasestyle) is set to null.

If `baseStyle` is unset, this property will be used as a base cell style if the grid is showing fixed height rows, and the specified cellHeight matches [ListGrid.normalCellHeight](#attr-listgridnormalcellheight) (and in Internet Explorer, [ListGrid.fastCellUpdates](#attr-listgridfastcellupdates) is false). Otherwise [ListGrid.tallBaseStyle](#attr-listgridtallbasestyle) will be used.

Having separate styles defined for fixed vs. variable height rows allows the developer to specify css which is designed to render at a specific height (typically using background images, which won't scale), without breaking support for styling rows of variable height.

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### See Also

- [ListGrid.getBaseStyle](ListGrid_2.md#method-listgridgetbasestyle)

**Flags**: IR

---
## Attr: ListGrid.listEndEditAction

### Description
If the user is editing the last record in this listGrid, and attempts to navigate beyond the last row either by tabbing off the last editable field, or using the down arrow key, this property determines what action to take:

*   "next": start editing a new record at the end of the list.
*   "done": hide the editor
*   "stop": leave focus in the cell being edited
*   "none": no action

See the [Grid Editing overview](../kb_topics/editing.md#kb-topic-grid-editing) and also the [Editing Unsaved Records overview](../kb_topics/unsavedRecords.md#kb-topic-handling-unsaved-records) for context about how newly added records behave.

### Groups

- editing

**Flags**: IRW

---
## Attr: ListGrid.printCheckboxFieldTrueImage

### Description
If set, the [ListGrid.checkboxFieldTrueImage](#attr-listgridcheckboxfieldtrueimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- checkboxField
- printing

### See Also

- [ListGrid.checkboxFieldTrueImage](#attr-listgridcheckboxfieldtrueimage)

**Flags**: IRWA

---
## Attr: ListGrid.groupLeadingIndent

### Description
Default number of pixels by which to indent all groups.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)
- [ListGrid.getGroupNodeHTML](ListGrid_2.md#method-listgridgetgroupnodehtml)

**Flags**: IRW

---
## Attr: ListGrid.linkTextProperty

### Description
Property name on a record that will hold the link text for that record.

This property is configurable to avoid possible collision with data values in the record.

Use [ListGridField.linkTextProperty](ListGridField.md#attr-listgridfieldlinktextproperty) if you have more than one link field and

### Groups

- display_values

### See Also

- [ListGridFieldType](../reference.md#type-listgridfieldtype)
- [FieldType](../reference_2.md#type-fieldtype)
- [ListGridField.linkText](ListGridField.md#attr-listgridfieldlinktext)
- [ListGridField.linkTextProperty](ListGridField.md#attr-listgridfieldlinktextproperty)

**Flags**: IRW

---
## Attr: ListGrid.discardEditsOnHideField

### Description
If a user is editing a [canEdit:true](#attr-listgridcanedit) listGrid, and they hide a field while the editor is showing, should we discard any edits in the edit row for the field being hidden?

Default behavior is to discard the edits - set this flag to false to preserve edits

**Flags**: IRW

---
## Attr: ListGrid.arrowKeyAction

### Description
Action to perform when the listGrid has keyboard focus (but not editing focus) and a user presses the arrow keys to navigate around the grid.

If [ListGrid.canSelectCells](#attr-listgridcanselectcells) is true, navigation occurs by cell - the user can move to a new cell in any direction.  
If [ListGrid.canSelectCells](#attr-listgridcanselectcells) is false, navigation typically occurs by row - the user can move up or down through the rows in the grid.

For actions that fire events (click or doubleClick), both cell and record level events are fired (for example for arrowKeyAction `"activate"`, [ListGrid.cellDoubleClick](ListGrid_2.md#method-listgridcelldoubleclick) and [ListGrid.recordDoubleClick](ListGrid_2.md#method-listgridrecorddoubleclick) are fired for the new position.  
Note that if [ListGrid.canSelectCells](#attr-listgridcanselectcells) is false, the events will be fired as if a click or double click had occurred on the first cell where [ListGridField.ignoreKeyboardClicks](ListGridField.md#attr-listgridfieldignorekeyboardclicks) is not true.

Possible actions are:

*   `"select"` : select the next row or cell in the grid and call click handlers.
*   `"selectOnly"` : select the next row or cell in the grid without firing click handlers.
*   `"focus"` : move focus to the next row or cell in the grid without changing the selection or calling click handlers.
*   `"activate"` : select and activate the next row or cell in the list (calls `recordDoubleClick` handler)
*   `"none"` : no action
*   `null` : if [ListGrid.selectionAppearance](#attr-listgridselectionappearance) is "checkbox", behaves as if set to "focus"; otherwise, behaves as if set to "select"

Note: If this grid is editable, behavior while editing is governed by the result of [ListGrid.getArrowKeyEditAction](ListGrid_2.md#method-listgridgetarrowkeyeditaction).

See also [ListGrid.generateClickOnEnter](#attr-listgridgenerateclickonenter), [ListGrid.generateClickOnSpace](#attr-listgridgenerateclickonspace), [ListGrid.generateDoubleClickOnEnter](#attr-listgridgeneratedoubleclickonenter) and [ListGrid.generateDoubleClickOnSpace](#attr-listgridgeneratedoubleclickonspace)

### Groups

- events

**Flags**: IRWA

---
## Attr: ListGrid.fixedRecordHeights

### Description
Should we vertically clip cell contents, or allow rows to expand vertically to show all contents?

If we allow rows to expand, the row height as derived from [getRowHeight()](GridRenderer.md#method-gridrenderergetrowheight) or the default [ListGrid.cellHeight](#attr-listgridcellheight) is treated as a minimum.

Setting `fixedRecordHeights` to false enables the [ListGrid.virtualScrolling](#attr-listgridvirtualscrolling) system.

**NOTE:**

*   Setting fixedRecordHeights to false for [CubeGrid](CubeGrid.md#class-cubegrid) is not supported, though a similar option for the row headers is available as [CubeGrid.autoSizeHeaders](CubeGrid.md#attr-cubegridautosizeheaders).
*   By default, for performance reasons, clipping is not enforced for some kinds of content (such as images) on all browsers. Set [enforceVClipping:true](#attr-listgridenforcevclipping) to enforce clipping for all types of content on all browsers.

### Groups

- cellStyling

**Flags**: IRWA

---
## Attr: ListGrid.canHover

### Description
If true, cellHover and rowHover events will fire and then a hover will be shown (if not canceled) when the user leaves the mouse over a row / cell unless the corresponding field has [showHover](ListGridField.md#attr-listgridfieldshowhover) set to false. If unset or null, the hover will be shown if the corresponding field has showHover:true. If false, then hovers are disabled.

Note that standard hovers override [clipped value hovers](#attr-listgridshowclippedvaluesonhover). Thus, to enable clipped value hovers, canHover must be unset or null and the corresponding field must have showHover unset or null as well.

### Groups

- hovers

### See Also

- [ListGrid.showHover](#attr-listgridshowhover)
- [ListGridField.showHover](ListGridField.md#attr-listgridfieldshowhover)

**Flags**: IRW

---
## Attr: ListGrid.chartConstructor

### Description
Name of the SmartClient Class to be used when creating charts. Must support the [Chart](../reference_2.md#interface-chart) interface.

**Flags**: IR

---
## Attr: ListGrid.cellContextMenu

### Description
The menu displayed when a cell is right clicked on.

**Flags**: R

---
## Attr: ListGrid.headerBackgroundColor

### Description
BackgroundColor for the header toolbar. Typically this is set to match the color of the header buttons.

### Groups

- gridHeader
- appearance

**Flags**: IRW

---
## Attr: ListGrid.expansionEditorSaveButton

### Description
Automatically generated [IButton](../reference.md#class-ibutton) for saving the values in the expanded portion of a ListGrid row.

This component is an [AutoChild](../reference.md#type-autochild) and as such may be customized via `listGrid.expansionEditorSaveButtonProperties` and `listGrid.expansionEditorSaveButtonDefaults`.

Note, however, that this is a multi-instance component (potentially one per record), so it is created using [createAutoChild()](Class.md#method-classcreateautochild) not [addAutoChild()](Class.md#method-classaddautochild), and no default single instance is created by name on the grid.

### Groups

- expansionField

**Flags**: RA

---
## Attr: ListGrid.headerAutoFitEvent

### Description
Event on a ListGrid header that triggers auto fitting to data and/or title.

Note that if sorting is enabled for the field and the headerAutoFitEvent is "click", both sorting and autofit occur on a click.

Only has an impact when [ListGrid.canAutoFitFields](#attr-listgridcanautofitfields) or [ListGridField.canAutoFitWidth](ListGridField.md#attr-listgridfieldcanautofitwidth) is set to `true`.

### Groups

- autoFitFields

**Flags**: IR

---
## Attr: ListGrid.rowAriaState

### Description
Returns a mapping of default WAI ARIA attributes for rows within this listGrid. See [ListGrid.getRowAriaState](ListGrid_2.md#method-listgridgetrowariastate)

**Flags**: IRWA

---
## Attr: ListGrid.canAddFormulaFields

### Description
Adds an item to the header context menu allowing users to launch a dialog to define a new field based on values present in other fields, using the [FormulaBuilder](FormulaBuilder.md#class-formulabuilder).

User-added formula fields can be persisted via [ListGrid.getFieldState](ListGrid_2.md#method-listgridgetfieldstate) and [ListGrid.setFieldState](ListGrid_2.md#method-listgridsetfieldstate).

To avoid undefined behavior, this property must be set to `false` if the same record objects, or the same [ResultSet](ResultSet.md#class-resultset) instances, are shared among multiple [DataBoundComponent](../reference.md#interface-databoundcomponent)s.

### Groups

- formulaFields

**Flags**: IRW

---
## Attr: ListGrid.aiFilterWindowInstructions

### Description
The descriptive text displayed above the user-entry area in the [ListGrid.aiFilterWindow](#attr-listgridaifilterwindow).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.autoFitFieldWidths

### Description
Should ListGrid fields autofit their widths to titles or content? This property may be overridden on a per-field basis via [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth). Developers may wish to consider disabling autoFit for fields known to have exceptionally long content as this can lead to large horizontal scrollbars and unwieldy UI.

The [ListGrid.autoFitWidthApproach](#attr-listgridautofitwidthapproach) controls whether fitting is to values, titles or both. This property may also be overridden on a per field basis.

If [field.width](ListGridField.md#attr-listgridfieldwidth) is also set on the field, it will be taken as a minimum width. [ListGrid.minFieldWidth](#attr-listgridminfieldwidth) will also be respected.

By default, the entire available width of the grid will still be used, by allocating any "extra" space to specific columns - see [ListGrid.autoFitFieldsFillViewport](#attr-listgridautofitfieldsfillviewport) for details on controlling this behavior.

When this feature is enabled, autofitting is active on an ongoing basis. Autofitting will be performed:

*   whenever the dataset is completely changed or rows are added or removed
*   whenever a field which is autofitting is changed
*   on a manual call to [ListGrid.autoFitField](ListGrid_2.md#method-listgridautofitfield) or [ListGrid.autoFitFields](ListGrid_2.md#method-listgridautofitfields)

Auto-fitting behavior continues until the user resizes the field manually, at which point it stops. The user can also perform a one-time auto-fit of fields via the header context menu if [ListGrid.canAutoFitFields](#attr-listgridcanautofitfields) is enabled.

When autofitting to column values, [ListGrid.getDefaultFieldWidth](ListGrid_2.md#method-listgridgetdefaultfieldwidth) will be called to determine the space required for a field's values. This method uses values from the rendered set of rows to calculate the required column width, which means the field width may still be smaller than values from non-rendered rows. See [ListGrid.showAllRecords](#attr-listgridshowallrecords) and [ListGrid.drawAheadRatio](#attr-listgriddrawaheadratio)) to control incremental rendering of rows.

Note that for `icon` type fields, the [ListGrid.autoFitIconFields](#attr-listgridautofiticonfields) property setting may turn on auto-fit-width behavior for specific fields by default, even if `autoFitFieldWidths` is false for the grid as a whole.

Using this feature has a performance penalty roughly comparable to always rendering one additional field per field where autofitting is enabled. Specifically, enabling it for all fields would be comparable to _both_ doubling the number of fields _and_ disabling [horizontal incremental rendering](#attr-listgridshowallcolumns). In a grid where only half the fields are normally visible and hence only half are normally rendered, this would be roughly 4 times slower overall.

This performance penalty is a result of [ListGrid.getDefaultFieldWidth](ListGrid_2.md#method-listgridgetdefaultfieldwidth) having to render out the data set offscreen and measure the rendered content - it does not apply for cases where this method can return a simple fixed values (as with icon fields).

Which fields are currently autofitting is saved as part of the [view state](ListGrid_2.md#method-listgridgetviewstate) of the ListGrid.

Interaction with wrapping: If [wrapping of cell values](#attr-listgridwrapcells) is enabled, autoFit behavior based on [cell content](#attr-listgridautofitwidthapproach) will render fields wide enough to contain the _unwrapped_ cell values. If [wrapping of field titles](ListGridField.md#attr-listgridfieldwrap) is enabled, when fitting to a title, a field will render wide enough to accommodate the _wrapped_ title without clipping (so wide enough for the natural wrap-point / longest word or unwrappable string).

Note that, if you just want to autofit specific fields, rather than trying to achieve cascading from grid-level settings with specific field overrides, the quick, single setting to use is [ListGridField.autoFit](ListGridField.md#attr-listgridfieldautofit).

### Groups

- autoFitFields

**Flags**: IR

---
## Attr: ListGrid.dateFormatter

### Description
How should Date type values be displayed in this ListGrid by default?

This property specifies the default DateDisplayFormat to apply to Date values displayed in this grid for all fields except those of [type "time"](ListGridField.md#attr-listgridfieldtype) (See also [ListGrid.timeFormatter](#attr-listgridtimeformatter)).  
If [ListGrid.datetimeFormatter](#attr-listgriddatetimeformatter) is specified, that will be applied by default to fields of type `"datetime"`.

Note that if [ListGridField.dateFormatter](ListGridField.md#attr-listgridfielddateformatter) or [ListGridField.timeFormatter](ListGridField.md#attr-listgridfieldtimeformatter) are specified those properties will take precedence over the component level settings.

If unset, date values will be formatted according to the system wide [short display format](DateUtil.md#classmethod-dateutilsetshortdisplayformat) or [short datetime display format](DateUtil.md#classmethod-dateutilsetshortdatetimedisplayformat) for datetime type fields.

If this field is editable the dateFormatter will also be passed to the editor created to edit this field as [dateFormatter](DateItem.md#attr-dateitemdateformatter). In this case you may also need to set [ListGrid.dateInputFormat](#attr-listgriddateinputformat).

**Flags**: IRW

---
## Attr: ListGrid.hiliteEditorSpanTitleSeparator

### Description
If this grid has specified [ListGrid.headerSpans](#attr-listgridheaderspans), and [ListGrid.showHeaderSpanTitlesInHiliteEditor](#attr-listgridshowheaderspantitlesinhiliteeditor) is true, this string will be inserted between the headerSpan title and the field title in the hiliteEditor field chooser grid.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.autoFitHeaderHeights

### Description
If this property is set to true, header buttons for either [fields](#attr-listgridfields) or [header spans](#attr-listgridheaderspans) will automatically expand to accommodate their titles vertically. This means if you have a "tall" title - typically a long string where [ListGridField.wrap](ListGridField.md#attr-listgridfieldwrap) is set to true such that you end up with several lines of text - the button will render large enough to accommodate it. If necessary this will cause the header for the grid as a whole to expand beyond the specified [ListGrid.headerHeight](#attr-listgridheaderheight).

Note that you need not set [HeaderSpan.height](HeaderSpan.md#attr-headerspanheight) or [ListGrid.headerSpanHeight](#attr-listgridheaderspanheight) if you set this property, but if you do, they will be used as minimum values.

**Flags**: IR

---
## Attr: ListGrid.printBaseStyle

### Description
Style for non-header cells in printed output. Defaults to [ListGrid.baseStyle](#attr-listgridbasestyle) if null.

### Groups

- printing

**Flags**: IRW

---
## Attr: ListGrid.useRemoteValidators

### Description
If [ListGrid.saveLocally](#attr-listgridsavelocally) is specified, but this grid is bound to a DataSource which includes remote field validators, by default edits will be saved synchronously and these validators will not be executed.  
Set this property to `true` to ensure these remote validators are called when saving edits in saveLocally mode. Note that since these remote validators need to run on the server, saving with this property set is asynchronous, even though the data that ultimately gets updated is already present on the client.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: ListGrid.filterEditor

### Description
If [ListGrid.showFilterEditor](#attr-listgridshowfiltereditor) is set to true, the `filterEditor` is automatically created as an AutoChild.

The filterEditor autoChild is a [RecordEditor](RecordEditor.md#class-recordeditor) - essentially it is a specialized listGrid in edit mode for editing a single set of values to be used as criteria. Once created, developers may access it and use standard listGrid APIs to interact with it. For example, given a listGrid _`myListGrid`_, live edit items could be accessed via  
`myListGrid.filterEditor.getEditFormItem(someFieldName);`

Developers may configure the AutoChild using [ListGrid.filterEditorProperties](#attr-listgridfiltereditorproperties).

### Groups

- filterEditor

### See Also

- [ListGrid.filterEditorSubmit](ListGrid_2.md#method-listgridfiltereditorsubmit)
- [ListGrid.filterOnKeypress](#attr-listgridfilteronkeypress)
- [ListGrid.filterByCell](#attr-listgridfilterbycell)

**Flags**: R

---
## Attr: ListGrid.fetchDelay

### Description
If we're showing the filterEditor ([ListGrid.showFilterEditor](#attr-listgridshowfiltereditor) is true), and [ListGrid.filterByCell](#attr-listgridfilterbycell) or [ListGrid.filterOnKeypress](#attr-listgridfilteronkeypress) are enabled, this property is the delay in milliseconds between the user changing the filter and the filter request being sent to the server. If multiple changes are made to the filter within this fetch delay, only the most recent will actually cause a re-filter

### Groups

- filterEditor

### See Also

- [ListGrid.explicitFetchDelay](#attr-listgridexplicitfetchdelay)

**Flags**: IRWA

---
## Attr: ListGrid.autoFitClipFields

### Description
If [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths) is enabled and the calculated field sizes are wide enough that horizontal scrolling would be introduced, this attribute may be set to an array of fieldNames, causing those fields to be clipped rather than forcing horizontal scrollbars to appear.

Note: If any [frozen columns](ListGridField.md#attr-listgridfieldfrozen) are included in this list they will not be clipped.

### Groups

- autoFitFields

**Flags**: IR

---
## Attr: ListGrid.showFilterWindowCriteriaIndicator

### Description
Should an indicator be shown to indicate that [ListGrid.filterWindowCriteria](#attr-listgridfilterwindowcriteria) is configured? The indicator is a small triangle shown in the top-right of the grid header or filter.

**Flags**: IR

---
## Attr: ListGrid.expansionFieldTrueImage

### Description
If [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) is set to `true`, this property determines the image to display in the expansion field for expanded rows. If unset, the [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage) will be used.

### Groups

- expansionField

### See Also

- [ListGrid.expansionFieldFalseImage](#attr-listgridexpansionfieldfalseimage)
- [ListGrid.expansionFieldImageWidth](#attr-listgridexpansionfieldimagewidth)
- [ListGrid.expansionFieldImageHeight](#attr-listgridexpansionfieldimageheight)

**Flags**: IRWA

---
## Attr: ListGrid.alternateBodyStyleName

### Description
Optional css style to apply to the body if [ListGrid.alternateRecordStyles](#attr-listgridalternaterecordstyles) is true for this grid. If unset [ListGrid.bodyStyleName](#attr-listgridbodystylename) will be used to style the body regardless of the [alternateRecordStyles](#attr-listgridalternaterecordstyles) setting.

**Flags**: IRWA

---
## Attr: ListGrid.hiliteIconSize

### Description
Default width and height of [hilite icons](#attr-listgridhiliteicons) for this component. Can be overridden at the component level via explicit [hiliteIconWidth](#attr-listgridhiliteiconwidth) and [hiliteIconHeight](#attr-listgridhiliteiconheight), or at the field level via [hiliteIconSize](ListGridField.md#attr-listgridfieldhiliteiconsize), [hiliteIconWidth](ListGridField.md#attr-listgridfieldhiliteiconwidth) and [hiliteIconHeight](ListGridField.md#attr-listgridfieldhiliteiconheight)

### Groups

- hiliting

### See Also

- [ListGrid.hiliteIconWidth](#attr-listgridhiliteiconwidth)
- [ListGrid.hiliteIconHeight](#attr-listgridhiliteiconheight)
- [ListGridField.hiliteIconSize](ListGridField.md#attr-listgridfieldhiliteiconsize)

**Flags**: IRW

---
## Attr: ListGrid.generateDoubleClickOnEnter

### Description
If true, when the user navigates to a cell using arrow keys and hits Enter, the cell will respond to a double click event.

**Flags**: IRWA

---
## Attr: ListGrid.groupByText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid and [this.canGroupBy](#attr-listgridcangroupby) is true, this string will be shown as the title for the menu item to toggle the group by setting for a field.

This is a dynamic string - text within `${...}` will be evaluated as JS code when the message is displayed, with `title` available as a variable containing the field title.

Default value returns "Group by " + the field's summary title.

### Groups

- i18nMessages

**Flags**: IRWA

---
## Attr: ListGrid.showCollapsedGroupSummary

### Description
Should group summaries be visible when the group is collapsed?

This property only applies to [grouped](ListGrid_2.md#method-listgridgroupby) grids showing [group summary rows](#attr-listgridshowgroupsummary). When set to true, the group summary row(s) for each group will show up under the group header nodes when the group is collapsed, or at then end of the grouped set of data if the group is expanded.

This property has no effect if [ListGrid.showGroupSummaryInHeader](#attr-listgridshowgroupsummaryinheader) is true.

### Groups

- grouping

### See Also

- [ListGrid.groupBy](ListGrid_2.md#method-listgridgroupby)

**Flags**: IRW

---
## Attr: ListGrid.printCheckboxFieldFalseImage

### Description
If set, the [ListGrid.checkboxFieldFalseImage](#attr-listgridcheckboxfieldfalseimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- checkboxField
- printing

### See Also

- [ListGrid.checkboxFieldFalseImage](#attr-listgridcheckboxfieldfalseimage)

**Flags**: IRWA

---
## Attr: ListGrid.clearFilterText

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, and a [filter-editor](#attr-listgridshowfiltereditor) is visible, this attribute will be shown as the menu item title to clear any existing filter. This menu-item is displayed only in the context menu for the sorter button.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.generateDoubleClickOnSpace

### Description
If true, when the user navigates to a cell using arrow keys and hits Space, the cell will respond to a double click event.

**Flags**: IRWA

---
## Attr: ListGrid.recordEnabledProperty

### Description
Property name on a record that will be checked to determine whether a record is enabled.

Setting this property on a record will effect the visual style and interactivity of the record. If set to `false` the record (row in a [ListGrid](#class-listgrid) or [TreeGrid](TreeGrid.md#class-treegrid)) will not highlight when the mouse moves over it, nor will it respond to mouse clicks.

### See Also

- [ListGridRecord.enabled](ListGridRecord.md#attr-listgridrecordenabled)

**Flags**: IR

---
## Attr: ListGrid.headerShadowHOffset

### Description
If [ListGrid.showHeaderShadow](#attr-listgridshowheadershadow) is true, the [Canvas.shadowHOffset](Canvas.md#attr-canvasshadowhoffset) for the header shadow

**Flags**: IRA

---
## Attr: ListGrid.searchForm

### Description
When declared, the specified form is automatically used as a search form for this grid, that is, [form.getValuesAsCriteria()](DynamicForm.md#method-dynamicformgetvaluesascriteria) is called and the criteria returned are additive with any criteria present in the [FilterEditor](#attr-listgridfiltereditor) or [Filter Window](#attr-listgridallowfilterwindow).

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

This is similar to the effect of adding a [ListGrid.filterEditorSubmit](ListGrid_2.md#method-listgridfiltereditorsubmit) override that pulls in criteria from the external form, and having the external form call [ListGrid.filterByEditor](ListGrid_2.md#method-listgridfilterbyeditor) instead of [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata), as shown in the +exampleLink{additiveFilter} example.

In particular, the grid will automatically filter when the [search()](SearchForm.md#method-searchformsearch) or [submit()](DynamicForm.md#method-dynamicformsubmit) events fire on the form (happens if a [SubmitItem](../reference.md#class-submititem) is present and is pressed), and will automatically trigger filtering if Enter is pressed in the form, as though [searchOnEnter](SearchForm.md#attr-searchformsearchonenter) or [saveOnEnter](DynamicForm.md#attr-dynamicformsaveonenter) had been set.

If the FilterEditor is enabled and listGrid.filterOnKeypress is set, the grid will automatically watch for [SearchForm.criteriaChanged](SearchForm.md#method-searchformcriteriachanged), and filter whenever that method fires. For the purposes of this behavior, the FilterEditor is considered to be enabled even if it is not currently visible but [ListGrid.canShowFilterEditor](#attr-listgridcanshowfiltereditor) is true (as otherwise filtering behavior in the form would change when the FilterEditor appears).

The criteria from the specified `searchForm` will only be shown and edited in the external form; they will neither be shown nor editable in the FilterEditor, even if the FilterEditor also allows criteria on the same fields. That is, they are treated much like [ListGrid.implicitCriteria](#attr-listgridimplicitcriteria).

Note: when using `listGrid.searchForm` don't add your own logic to call fetchData() or the criteria you specify will appear in the FilterEditor and be editable there, potentially creating user confusion, especially if some of the criteria in your form cannot be displayed and edited in the FilterEditor.

### Groups

- searchCriteria

**Flags**: IRW

---
## Attr: ListGrid.allowFilterExpressions

### Description
For use with [ListGrid.showFilterEditor](#attr-listgridshowfiltereditor):true, allows simple search expressions to be entered into filter fields, as though [DynamicForm.allowExpressions](DynamicForm.md#attr-dynamicformallowexpressions) were true.

This attribute can also be set at the [field level](ListGridField.md#attr-listgridfieldallowfilterexpressions).

### Groups

- advancedFilter

**Flags**: IR

---
## Attr: ListGrid.headerBaseStyle

### Description
[Button.baseStyle](Button.md#attr-buttonbasestyle) to apply to the buttons in the header, and the sorter, for this ListGrid. Note that, depending on the [Class](#attr-listgridheaderbuttonconstructor) of the header buttons, you may also need to set [ListGrid.headerTitleStyle](#attr-listgridheadertitlestyle).

### Groups

- gridHeader
- appearance

### See Also

- [skins](../kb_topics/skins.md#kb-topic-skins)
- [ListGrid.clipHeaderTitles](#attr-listgridclipheadertitles)
- [ListGrid.wrapHeaderTitles](#attr-listgridwrapheadertitles)

**Flags**: IR

---
## Attr: ListGrid.showSelectionUnderCanvas

### Description
If [selectionType](#attr-listgridselectiontype) is set to "single", and either [showSelectionCanvas](#attr-listgridshowselectioncanvas) is `true` and `showSelectionUnderCanvas` is unset, or `showSelectionUnderCanvas` is explicitly set to `true`, then selection will be displayed to the user with the [selectionCanvas](#attr-listgridselectioncanvas) and/or [selectionUnderCanvas](#attr-listgridselectionundercanvas) rather than with CSS styling. Setting `showSelectionUnderCanvas` to `false` will disable the use of the `selectionUnderCanvas`.

With [frozen fields](#attr-listgridcanfreezefields), the `selectionUnderCanvas` is displayed only behind the non-frozen fields of the selected row.

### Groups

- rowEffects

### See Also

- [ListGrid.showSelectionCanvas](#attr-listgridshowselectioncanvas)

**Flags**: IRWA

---
## Attr: ListGrid.autoFitFieldsFillViewport

### Description
If [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths) is enabled, and extra space is available after autofitting all fields, should the grid automatically expand one field to fill the extra space.

When enabled, the field to expand may be specified via [ListGrid.autoFitExpandField](#attr-listgridautofitexpandfield).

Note this logic will not expand a [frozen column](ListGridField.md#attr-listgridfieldfrozen).

### Groups

- autoFitFields

**Flags**: IR

---
## Attr: ListGrid.canSelectAll

### Description
Controls whether a checkbox for selecting all records appears in the header with [selectionAppearance](#attr-listgridselectionappearance) set to "checkbox"

### Groups

- selection

**Flags**: IRW

---
## Attr: ListGrid.styleName

### Description
Default CSS class for the ListGrid as a whole.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.fieldVisibilitySubmenuTitle

### Description
If we're showing a [headerContextMenu](#attr-listgridshowheadercontextmenu) for this grid, and [this.canPickFields](#attr-listgridcanpickfields) is true, this attribute will be shown as the title for the menu item which contains a submenu with items allowing the user to show and hide fields in the grid.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.removeIconStyle

### Description
Custom style to apply to the image in the [removeField](#attr-listgridremovefieldproperties) displayed in rows when [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) is true. Affects the icons provided by [ListGrid.removeIcon](#attr-listgridremoveicon) and [ListGrid.unremoveIcon](#attr-listgridunremoveicon).

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.rotatedHeaderMenuButtonHeight

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, this property governs the height of the auto-generated `headerMenuButton` over a [rotated](ListGridField.md#attr-listgridfieldrotatetitle) header button.

### Groups

- headerMenuButton

### See Also

- [ListGrid.headerMenuButtonHeight](#attr-listgridheadermenubuttonheight)

**Flags**: IRA

---
## Attr: ListGrid.sortBinaryByFileName

### Description
For any fields of [type "binary"](../reference_2.md#type-fieldtype), should sorting be performed against the fileName of the value for the field? For SmartClient server backed dataSources, this is applied to the record automatically as described in the [binaryFields](../kb_topics/binaryFields.md#kb-topic-binary-fields) overview.

If set to false, binary fields will be sorted against the record value for the field in question. Client-side sorting does not support this, so developers who actually want to support a sort against the binary itself would typically set [ResultSet.useClientSorting](ResultSet.md#attr-resultsetuseclientsorting) to false on the [ListGrid.dataProperties](#attr-listgriddataproperties) block for this grid.

Note that this setting will have no effect if [DataSourceField.sortByField](DataSourceField.md#attr-datasourcefieldsortbyfield) is specified

### Groups

- sorting

**Flags**: IRW

---
## Attr: ListGrid.printBooleanFalseImage

### Description
If set, the [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

If this, [ListGrid.printBooleanTrueImage](#attr-listgridprintbooleantrueimage) and [ListGrid.printBooleanPartialImage](#attr-listgridprintbooleanpartialimage) are unset, this will be set to the default [CheckboxItem.printUncheckedImage](CheckboxItem.md#attr-checkboxitemprintuncheckedimage).

### Groups

- imageColumns
- printing

### See Also

- [ListGrid.booleanFalseImage](#attr-listgridbooleanfalseimage)

**Flags**: IRWA

---
## Attr: ListGrid.reselectOnUpdateNotifications

### Description
if [ListGrid.reselectOnUpdate](#attr-listgridreselectonupdate) is true, this property governs what selection changed notifications should be triggered when a selected record is edited then automatically reselected when the edited data is merged into the data set.

**Flags**: IRWA

---
## Attr: ListGrid.hoverMode

### Description
When [showHoverComponents](#attr-listgridshowhovercomponents) is true, the builtin mode to use when automatically creating a hover component for rows in this grid.

A number of builtin modes are provided - see [HoverMode](../reference.md#type-hovermode). You can also override [getCellHoverComponent()](ListGrid_2.md#method-listgridgetcellhovercomponent) to provide a custom hover widget - in that case, this attribute is ignored.

If `showHoverComponents` is true but `hoverMode` is not set, it defaults to "detailRelated" if [ListGrid.detailDS](#attr-listgriddetailds) is set, or to "details" otherwise. If `showHoverComponents` is not set (ie, is null) and `hoverMode` _is_ set, `showHoverComponents` defaults to true.

### Groups

- hoverComponents

**Flags**: IRW

---
## Attr: ListGrid.newSearchText

### Description
Text to show for saving the current view as a new "saved search".

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ListGrid.summaryRowCriteria

### Description
If [ListGrid.showGridSummary](#attr-listgridshowgridsummary) is true, and a [ListGrid.summaryRowDataSource](#attr-listgridsummaryrowdatasource) is specified this property may be used to specify fetch criteria to apply when retrieving summary data to show in the summary row. If unset, and any filter criteria have been specified for the grid, they will be used.

If this property is set, the [textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) will default to "exact". Otherwise [ListGrid.autoFetchTextMatchStyle](#attr-listgridautofetchtextmatchstyle) will be used. This can be overridden via [ListGrid.summaryRowFetchRequestProperties](#attr-listgridsummaryrowfetchrequestproperties).

**Flags**: IRWA

---
## Attr: ListGrid.groupByAsyncThreshold

### Description
When grouping is requested with this number of records or more, an asynchronous approach is used to avoid the browser showing a "script is running slowly.." message prompting the user to stop execution of JavaScript.

Note that [ListGrid.groupByMaxRecords](#attr-listgridgroupbymaxrecords) must be set at least as high as [ListGrid.groupByAsyncThreshold](#attr-listgridgroupbyasyncthreshold) or asynchronous grouping will never be used.

During async grouping, interactivity is blocked and the [ListGrid.asynchGroupingPrompt](#attr-listgridasynchgroupingprompt) is shown to the user, then hidden when grouping completes; [ListGrid.groupByComplete](ListGrid_2.md#method-listgridgroupbycomplete) then fires.

Note that this async processing covers grouping **only** - it does not cover whole grid or per-group summaries, client-side sort or filter, or other operations that may cause the browser to show the "script is running slowly" prompt when working with very large sets of records in a grid.

At this time, there is no generally effective way to avoid this warning dialog appearing with very large datasets in Microsoft's Internet Explorer (IE). IE's severely flawed detection algorithm for runaway scripts has been shown to interrupt computations after only 0.2 seconds elapsed time even if the computation would have finished in 0.3 seconds. Optimizations that reduce execution time can sometimes trigger the "script running slowly" dialog sooner. Since not every operation can reasonably be made asynchronous, the current recommendation is to avoid working with overly large datasets until the affected versions of IE are obsoleted.

**Flags**: IRW

---
## Attr: ListGrid.printBooleanTrueImage

### Description
If set, the [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

If this, [ListGrid.printBooleanFalseImage](#attr-listgridprintbooleanfalseimage) and [ListGrid.printBooleanPartialImage](#attr-listgridprintbooleanpartialimage) are unset, this will be set to the default [CheckboxItem.printCheckedImage](CheckboxItem.md#attr-checkboxitemprintcheckedimage).

### Groups

- imageColumns
- printing

### See Also

- [ListGrid.booleanTrueImage](#attr-listgridbooleantrueimage)

**Flags**: IRWA

---
## Attr: ListGrid.groupByMaxRecordsExceededMessage

### Description
Warning shown to the user when a grouping attempt failed as the data set length exceeds [ListGrid.groupByMaxRecords](#attr-listgridgroupbymaxrecords).

If defined, this prompt will be shown to the user in a [warning dialog](isc.md#staticmethod-iscwarn) when the user attempts to group a data set that exceeds the [ListGrid.groupByMaxRecords](#attr-listgridgroupbymaxrecords) threshold.

This can occur if an already-grouped grid's filter criteria are modified such that a new set of records is loaded from the DataSource which exceeds the [ListGrid.groupByMaxRecords](#attr-listgridgroupbymaxrecords) threshold.

It can also occur when a user attempts to group a grid with a partially loaded data set where the true size of the data set is not known due to [progressiveLoading](DataBoundComponent.md#attr-databoundcomponentprogressiveloading). In this case, the grouping logic will attempt to retrieve all the records in the data set and may get back a new total row count from the DataSource which exceeds [ListGrid.groupByMaxRecords](#attr-listgridgroupbymaxrecords).

In either case the warning will be displayed to the user and the [group by menu item](#attr-listgridcangroupby) will be disabled.

See also [ListGrid.disabledGroupByPrompt](#attr-listgriddisabledgroupbyprompt).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ListGrid.updateSummariesDuringEditing

### Description
Should the [summary row](#attr-listgridshowgridsummary) or [group summaries](#attr-listgridshowgroupsummary) be updated during editing of grid records? This can be set false to improve performance when a large number of [ListGridFields](../reference_2.md#object-listgridfield) or [DataSourceFields](../reference_2.md#object-datasourcefield) are present for the grid.

Note that summaries will always be updated when the edits are saved, so to avoid recalculation overhead when a row or cell edit is completed, you must also set [ListGrid.autoSaveEdits](#attr-listgridautosaveedits): false. Summaries will then be updated upon your manual save, such as [ListGrid.saveAllEdits](ListGrid_2.md#method-listgridsavealledits).

### See Also

- [ListGrid.recalculateSummaries](ListGrid_2.md#method-listgridrecalculatesummaries)

**Flags**: IRW

---
## Attr: ListGrid.locateColumnsBy

### Description
When [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) is used to parse locator strings generated by [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) for a cell in this grid, how should the column be identified?  
Note that getLocator() will actually store all available information about the column in the generated string -- this attribute effects how a stored string will be parsed only.

Valid options area:

*   `"fieldName"` Attempt to identify by fieldName.
*   `"index"` Attempt to identify by colNum (index in the fields array).

If unset, default behavior is to identify by fieldName (if available), otherwise by index.

### Groups

- autoTest

### See Also

- [LocatorStrategy](../reference_2.md#type-locatorstrategy)

**Flags**: IRW

---
## Attr: ListGrid.headerButtonDefaults

### Description
Defaults to apply to all header buttons. To modify this object, use [ListGrid.changeDefaults()](Class.md#classmethod-classchangedefaults) rather than replacing with an entirely new object.

### Groups

- gridHeader
- appearance

**Flags**: IRA

---
## Attr: ListGrid.exportWidthScale

### Description
Scaling factor to translate from ListGrid field widths in pixels to Excel/OpenOffice units for field width, which are 1/256th of the width of the widest digit character in the default font for the spreadsheet. See [ListGrid.exportFieldWidths](#attr-listgridexportfieldwidths) for where this is used.

**Flags**: IRW

---
## Attr: ListGrid.offlineMessageStyle

### Description
The CSS style name applied to the [offlineMessage](DataBoundComponent.md#attr-databoundcomponentofflinemessage) if displayed.

### Groups

- offlineGroup

**Flags**: IRW

---
## Attr: ListGrid.expansionEditorShowSaveDialog

### Description
When [canExpandRecords](#attr-listgridcanexpandrecords) is true and [expansionMode](#attr-listgridexpansionmode) is _editor_, whether a dialog should be displayed when an expanded row is collapsed while it's nested editor has changed values.

### Groups

- expansionField

**Flags**: IR

---
## Attr: ListGrid.sorterProperties

### Description
Properties to apply to the sorter button. Overrides defaults applied via [ListGrid.sorterDefaults](#attr-listgridsorterdefaults).

### Groups

- gridHeader
- appearance

**Flags**: IRA

---
## Attr: ListGrid.removeFieldDefaults

### Description
Default configuration properties for the "remove field" displayed when [ListGrid.canRemoveRecords](#attr-listgridcanremoverecords) is enabled. [Class.changeDefaults](Class.md#classmethod-classchangedefaults) should be used when modifying this object.

The default configuration includes a [ListGridField.recordClick](ListGridField.md#method-listgridfieldrecordclick) handler which calls [ListGrid.removeData](ListGrid_2.md#method-listgridremovedata) to actually perform the data removal.

**Flags**: IR

---
## Attr: ListGrid.showRowNumbers

### Description
When set to true, shows an additional field at the beginning of the field-list (respecting RTL) that displays the current rowNum for each record.

### Groups

- rowNumberField

**Flags**: IRWA

---
## Attr: ListGrid.expansionScreen

### Description
Screen to create (via [createScreen()](RPCManager.md#classmethod-rpcmanagercreatescreen)) in lieu of calling [ListGrid.getExpansionComponent](ListGrid_2.md#method-listgridgetexpansioncomponent).

If this grid has a [dataSource](#attr-listgriddatasource), the created screen is provided with a [Canvas.dataContext](Canvas.md#attr-canvasdatacontext) that includes the record being expanded. Be sure the expansion screen meets these [requirements](Canvas.md#attr-canvasautopopulatedata) to utilize the `dataContext`.

### Groups

- expansionField

**Flags**: IR

---
## Attr: ListGrid.leaveHeaderMenuButtonSpace

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, when auto-fitting fields to the title width via [ListGrid.autoFitFieldWidths](#attr-listgridautofitfieldwidths) or [ListGridField.autoFitWidth](ListGridField.md#attr-listgridfieldautofitwidth), should the button be sized such that there is enough space for the header menu button to show without covering the field title?

May be explicitly specified at the [field level](ListGridField.md#attr-listgridfieldleaveheadermenubuttonspace) or at the [grid level](#attr-listgridleaveheadermenubuttonspace). If not explicitly specified space will be left for fields with [ListGridField.align](ListGridField.md#attr-listgridfieldalign) set to `"left"` or `"right"`, but not for fields with align set to `"center"`.

### Groups

- headerMenuButton

### See Also

- [ListGrid.sortArrowMenuButtonSpaceOffset](#attr-listgridsortarrowmenubuttonspaceoffset)
- [ListGrid.sortNumeralMenuButtonSpaceOffset](#attr-listgridsortnumeralmenubuttonspaceoffset)

**Flags**: IWA

---
## Attr: ListGrid.selectCellTextOnClick

### Description
If this property is set to true, clicking on a cell will natively select the cell's content, ready to be copied to the browser clipboard.

For control of this behavior at the field level, [ListGridField.selectCellTextOnClick](ListGridField.md#attr-listgridfieldselectcelltextonclick) may be used. These properties interact as follows:

| listGrid.selectCellTextOnClick value | listGridField.selectCellTextOnClick value | Behavior |
|---|---|---|
| true | unset or true | Cell contents will be natively selected on click. |
| false | Cell contents will not be natively selected on click. |
| unset | true | Cell contents will be natively selected on click. |
| unset or false | Cell contents will not be natively selected on click. |
| false | true, false or unset | Cell contents will not be natively selected on click. |

This is related to the [ListGrid.canDragSelectText](#attr-listgridcandragselecttext) attribute which enables native text selection of grid content by standard browser interactions (drag selecting or double-click selecting).

Note that developers may also be interested in the related formItem properties [FormItem.selectOnClick](FormItem.md#attr-formitemselectonclick) and [FormItem.selectOnFocus](FormItem.md#attr-formitemselectonfocus).

**Flags**: IRW

---
## Attr: ListGrid.groupIcon

### Description
The URL of the base icon for the group icons in this listGrid. Default value may be overridden by the [current skin](../kb_topics/skinning.md#kb-topic-skinning--theming).

### Groups

- grouping

### See Also

- [grouping](../reference.md#kb-topic-grouping)

**Flags**: IRW

---
## Attr: ListGrid.initialSort

### Description
An array of [SortSpecifier](../reference.md#object-sortspecifier) objects used to set up the initial sort configuration for this grid. If specified, this will be used instead of any [ListGrid.sortField](#attr-listgridsortfield) specified.

### Groups

- sorting

**Flags**: IR

---
## Attr: ListGrid.canReorderRecords

### Description
Indicates whether records can be reordered by dragging within this `ListGrid`.

**NOTE:** If `canReorderRecords` is initially enabled or might be [dynamically enabled](ListGrid_2.md#method-listgridsetcanreorderrecords) after the grid is created, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging a record starts a reorder operation rather than a scroll, but see the discussion of [drag handles](ListGrid_2.md#method-listgridshowdraghandles). If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag-reordering of records.

### Groups

- dragging

### See Also

- [ListGridRecord.canDrag](ListGridRecord.md#attr-listgridrecordcandrag)
- [ListGridRecord.canAcceptDrop](ListGridRecord.md#attr-listgridrecordcanacceptdrop)
- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)

**Flags**: IRW

---
## Attr: ListGrid.canExpandMultipleRecords

### Description
When [ListGrid.canExpandRecords](#attr-listgridcanexpandrecords) is true, this property indicates whether multiple records can be expanded simultaneously. If set to false, expanding a record will automatically collapse any record which is already expanded. The default value is `true`.

### Groups

- expansionField

**Flags**: IRW

---
## Attr: ListGrid.valueIconLeftPadding

### Description
How much padding should there be on the left of valueIcons by default Can be overridden at the field level

### Groups

- imageColumns

### See Also

- [ListGridField.valueIcons](ListGridField.md#attr-listgridfieldvalueicons)

**Flags**: IRW

---
## Attr: ListGrid.headerMenuButtonWidth

### Description
If [ListGrid.showHeaderMenuButton](#attr-listgridshowheadermenubutton) is true, this property governs the width of the auto-generated `headerMenuButton`

### Groups

- headerMenuButton

### See Also

- [ListGrid.rotatedHeaderMenuButtonWidth](#attr-listgridrotatedheadermenubuttonwidth)

**Flags**: IRA

---
## Attr: ListGrid.animateFolderEffect

### Description
When animating folder opening / closing, this property can be set to apply an animated acceleration effect. This allows the animation speed to be "weighted", for example expanding or collapsing at a faster rate toward the beginning of the animation than at the end.

For a ListGrid, this property applies when [grouping](#attr-listgridcangroupby) is enabled.

### Groups

- animation

**Flags**: IRW

---
## Attr: ListGrid.showRollOver

### Description
Should we show different styling for the cell the mouse is over?

If true, the cell style will have the suffix "Over" appended.

Can be overridden on a per-record basis via [ListGridRecord.showRollOver](ListGridRecord.md#attr-listgridrecordshowrollover).

### Groups

- appearance

**Flags**: IRW

---
## Attr: ListGrid.rowRangeDisplay

### Description
[RowRangeDisplay](RowRangeDisplay.md#class-rowrangedisplay) autoChild, which may be retrieved by calling [ListGrid.getRowRangeDisplay](ListGrid_2.md#method-listgridgetrowrangedisplay).

### Groups

- rowRangeDisplay

**Flags**: R

---
## Attr: ListGrid.showGroupSummary

### Description
If this listGrid supports [grouping](#attr-listgridcangroupby), setting this property will cause the grid to render an extra row at the end of each group when grouped, containing summary information for the fields. Summary information will be calculated by the [ListGridField.getGroupSummary](ListGridField.md#method-listgridfieldgetgroupsummary) method if specified, otherwise via the specified [ListGridField.summaryFunction](ListGridField.md#attr-listgridfieldsummaryfunction).

### See Also

- [ListGrid.groupByFieldSummaries](#attr-listgridgroupbyfieldsummaries)

**Flags**: IRW

---
## Attr: ListGrid.enterKeyEditAction

### Description
What to do when a user hits enter while editing a cell:

*   "nextCell": start editing the next editable cell in this record (or the first editable cell in the next record if focus is in the last editable cell in the row)
*   "nextRow": start editing the same field in the next row (skipping any rows where that would be a non-editable cell.
*   "nextRowStart": start editing the first editable cell in the next row.
*   "done": hide the editor (editing is complete)

Note that if this.autoSaveEdits is true, this may cause a save of the current edit values

### Groups

- editing

**Flags**: IRW

---
## Method: ListGrid.cellErrorIconOver

### Description
Optional stringMethod to fire when the mouse moves over the error icon of a cell with validation errors.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the default behavior (show a standard error message hover)

### Groups

- events

### See Also

- [ListGrid.showErrorIcons](#attr-listgridshowerroricons)

**Flags**: A

---
## Method: ListGrid.getDefaultFormattedFieldValue

### Description
Get a field value for some record with default field formatters applied.

This method differs from [ListGrid.getDefaultFormattedValue](ListGrid_2.md#method-listgridgetdefaultformattedvalue) in that this method does not rely on the rowNum and colNum parameters to find the record and field in the grid. Also, unlike [ListGrid.getDefaultFormattedValue](ListGrid_2.md#method-listgridgetdefaultformattedvalue), this method _will_ call any [field-level formatter](ListGridField.md#method-listgridfieldformatcellvalue) if one is defined on the field (though it will not call a [grid-level formatter](ListGrid_2.md#method-listgridformatcellvalue) if one exists).

This method is typically called from within a grid-level [formatCellValue()](ListGrid_2.md#method-listgridformatcellvalue) override when the developer wants to conditionally customize formatting for some fields while allowing other fields to use their standard formatting (including any field-level formatters). This avoids infinite recursion since the grid-level formatter is not called.

This method applies standard formatting such as [ListGridField.valueMap](ListGridField.md#attr-listgridfieldvaluemap) mapping, [ListGridField.displayField](ListGridField.md#attr-listgridfielddisplayfield) substitution, [ListGridField.format](ListGridField.md#attr-listgridfieldformat) application, and type-specific formatters. If a field-level formatter is present, it is called and other declarative formatting is skipped. The [ListGrid.useLegacyDefaultFormattedValue](#attr-listgriduselegacydefaultformattedvalue) flag can be used to revert to legacy behavior where these formatting steps were not applied when no field-level formatter is present.

The `rowNum` and `colNum` parameters are passed through to the field-level formatter if one exists. If not explicitly provided, these are defaulted to -1.

For other use cases, see also:

*   [ListGrid.getDefaultFormattedValue](ListGrid_2.md#method-listgridgetdefaultformattedvalue) - get formatted value without any custom formatters
*   [ListGrid.getFormattedValue](ListGrid_2.md#method-listgridgetformattedvalue) - get fully formatted value including all custom formatters

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | the record object |
| field | [ListGridField](#type-listgridfield) | false | — | the field object |
| rowNum | [int](../reference.md#type-int) | true | — | rowNum (passed to field-level formatter if present) |
| colNum | [int](../reference.md#type-int) | true | — | colNum (passed to field-level formatter if present) |

### Returns

`[String](#type-string)` — Formatted value

### See Also

- [ListGridField.formatCellValue](ListGridField.md#method-listgridfieldformatcellvalue)
- [ListGrid.formatCellValue](ListGrid_2.md#method-listgridformatcellvalue)
- [ListGrid.getDefaultFormattedValue](ListGrid_2.md#method-listgridgetdefaultformattedvalue)
- [ListGrid.getFormattedValue](ListGrid_2.md#method-listgridgetformattedvalue)

**Flags**: A

---
## Method: ListGrid.getHeaderSpanContextMenuItems

### Description
Return the menus items that should be shown in a menu triggered from a [headerSpan](#attr-listgridheaderspans). The default implementation returns the parent element's context menu, unless [ListGrid.showHeaderSpanContextMenu](#attr-listgridshowheaderspancontextmenu) is `true`, in which case it returns standard items for showing / hiding fields and freezing / unfreezing header spans. Note that no column picker will be shown unless [ListGrid.showTreeColumnPicker](#attr-listgridshowtreecolumnpicker) is `true`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| headerSpan | [HeaderSpan](#type-headerspan) | false | — | the component representing the headerSpan. This component will have all the properties specified via [ListGrid.headerSpans](#attr-listgridheaderspans). |

### Returns

`[Array of MenuItem](#type-array-of-menuitem)` — return false instead to avoid showing any menu

### Groups

- headerSpan

---
## Method: ListGrid.anySelected

### Description
Whether at least one item is selected

### Returns

`[boolean](../reference.md#type-boolean)` — true == at least one item is selected false == nothing at all is selected

### Groups

- selection

---
## Method: ListGrid.editFailed

### Description
Called when an attempt to save inline edits fails, due to a validation error or other server error.

The default implementation of editFailed does nothing for normal validation errors, which are displayed before editFailed() is called. For any other errors, the default implementation will call [RPCManager.handleError](RPCManager.md#classmethod-rpcmanagerhandleerror), which by default will result in a warning dialog.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | current index of the row we attempted to save |
| colNum | [number](#type-number) | false | — | index of the column where the edit failed, if applicable |
| newValues | [Object](../reference.md#type-object)|[Record](#type-record) | false | — | new values that we attempted to save |
| oldValues | [Record](#type-record) | false | — | the complete original values from before the save occurred |
| editCompletionEvent | [EditCompletionEvent](../reference.md#type-editcompletionevent) | false | — | Edit completion event that led to the save attempt |
| dsResponse | [DSResponse](#type-dsresponse) | true | — | DSResponse, for saves through a DataSource |

### Groups

- editing

---
## Method: ListGrid.cellContextClick

### Description
Called when a cell receives a contextclick event.

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
## Method: ListGrid.showFields

### Description
Force an array of fields to be shown. This method does not add new fields to the grid, it simply changes field visibility. If a field.showIf expression exists, it will be destroyed.

Note: for showing multiple fields it is more efficient to call this method than to call [ListGrid.showField](ListGrid_2.md#method-listgridshowfield) repeatedly.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| field | [Array of String](#type-array-of-string)|[Array of ListGridField](#type-array-of-listgridfield) | false | — | Fields to show. |
| suppressRelayout | [boolean](../reference.md#type-boolean) | true | — | If passed, don't resize non-explicitly sized columns to fill the available space. |

---
## Method: ListGrid.showFilterWindow

### Description
Shows the dialog for [ListGrid.filterWindowCriteria](#attr-listgridfilterwindowcriteria) allowing end-users to edit the advanced filter. This method can be called directly but it is also used to show the dialog when [ListGrid.allowFilterWindow](#attr-listgridallowfilterwindow) is enabled and the user chooses the ["Advanced Filtering"](#attr-listgridadvancedfilteringtext) menu option.

**Note:** this feature requires [SmartClient Pro](https://www.smartclient.com/product/) or better.

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
