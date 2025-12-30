# Frozen Fields

[← Back to API Index](../reference.md)

---

## KB Topic: Frozen Fields

### Description
Frozen fields are fields that do not scroll horizontally with other fields, remaining on the screen while other fields may be scrolled off. This feature is typically used to allow basic identifying information (like an "accountId") to remain on screen while the user scrolls through a large number of related fields.

Fields can be programmatically frozen via setting [field.frozen](../classes/ListGridField.md#attr-listgridfieldfrozen) to true when the grid is created, or dynamically frozen and unfrozen via [freezeField()](../classes/ListGrid_2.md#method-listgridfreezefield) and [unfreezeField()](../classes/ListGrid_2.md#method-listgridunfreezefield). The setting [canFreezeFields](../classes/ListGrid_1.md#attr-listgridcanfreezefields) enables a user interface to allow end users to dynamically freeze and unfreeze fields.

The frozen fields feature is not compatible with the following features:

*   [autoFitData](../reference.md#kb-topic-autofitdata):"horizontal", as well as headers that autoFit to titles (normally enabled via `field.overflow:"visible"`)
*   the [CubeGrid](../classes/CubeGrid.md#class-cubegrid) subclass of ListGrid
*   nested grids

The frozen fields feature **is** compatible with column resize and reorder, selection and multi-selection, loading data on demand, inline editing, drag and drop and reorder of records, the [TreeGrid](../classes/TreeGrid.md#class-treegrid) subclass of ListGrid, and all dynamic styling-related and formatting-related features.

The [ListGrid.frozenFieldsMaxWidth](../classes/ListGrid_1.md#attr-listgridfrozenfieldsmaxwidth) property may be used to specify a maximum size for the frozen fields. If their combined width exceeds this, a horizontal scrollbar will be displayed, allowing the user to scroll the frozen fields independently of the other fields in the grid.

Troubleshooting tip: If you encounter misalignment between rows in frozen and unfrozen columns, this is likely due to one of the following causes:

*   Inconsistent border/padding: all cells in a row in a table must have the same top and bottom border thickness, and all cells in a column must have the same horizontal border and padding width, or the table is invalid, with no clear rules for rendering it. The HTML/CSS spec doesn't say what to do in this situation, and browser engines behave inconsistently.
*   For grids with [fixedRecordHeights:true](#fixedrecordheights), the cell contents, inclusive of border and padding, needs to be less than your configured [ListGrid.cellHeight](../classes/ListGrid_1.md#attr-listgridcellheight), or you need to set [enforceVClipping](#enforcevclipping) to cause us to clip it as necessary. Breaking this rule can cause misalignment between rows in frozen and unfrozen columns as some fields have cells with taller content. (This does not apply for grids with `fixedRecordHeights` set to false).

### Related

- [ListGridField.getAutoFreezePosition](../classes/ListGridField.md#method-listgridfieldgetautofreezeposition)
- [ListGrid.freezeField](../classes/ListGrid_2.md#method-listgridfreezefield)
- [ListGrid.unfreezeField](../classes/ListGrid_2.md#method-listgridunfreezefield)
- [ListGrid.toggleFrozen](../classes/ListGrid_2.md#method-listgridtogglefrozen)
- [ListGridField.frozen](../classes/ListGridField.md#attr-listgridfieldfrozen)
- [ListGridField.canFreeze](../classes/ListGridField.md#attr-listgridfieldcanfreeze)
- [ListGridField.autoFreeze](../classes/ListGridField.md#attr-listgridfieldautofreeze)
- [ListGrid.frozenBaseStyle](../classes/ListGrid_1.md#attr-listgridfrozenbasestyle)
- [ListGrid.shrinkForFreeze](../classes/ListGrid_1.md#attr-listgridshrinkforfreeze)
- [ListGrid.frozenHeaderBaseStyle](../classes/ListGrid_1.md#attr-listgridfrozenheaderbasestyle)
- [ListGrid.frozenHeaderTitleStyle](../classes/ListGrid_1.md#attr-listgridfrozenheadertitlestyle)
- [ListGrid.canFreezeFields](../classes/ListGrid_1.md#attr-listgridcanfreezefields)

---
