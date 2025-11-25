# Exports & Cell Background Color

[← Back to API Index](../main.md)

---

## KB Topic: Exports & Cell Background Color

### Description
Several APIs and settings influence the background color which will be used for spreadsheet cells when exporting to Excel/OpenOffice formats using [ListGrid.exportData](../classes/ListGrid_2.md#method-listgridexportdata) or [ListGrid.exportClientData](../classes/ListGrid_2.md#method-listgridexportclientdata). The following APIs are called in the order shown, so `hilite.backgroundColor` takes precedence over `exportDefaultBGColor`, for example.

1.  [getExportBGColor(rowNum, colNum, record)](../classes/ListGrid_2.md#method-listgridgetexportbgcolor)
2.  [Hilite.backgroundColor](../classes/Hilite.md#attr-hilitebackgroundcolor)
3.  [getExportRowBGColor(rowNum, record)](../classes/ListGrid_2.md#method-listgridgetexportrowbgcolor)
4.  [getExportColumnBGColor(colNum)](../classes/ListGrid_2.md#method-listgridgetexportcolumnbgcolor)
5.  [exportAlternateRowBGColor](../classes/ListGrid_1.md#attr-listgridexportalternaterowbgcolor)
6.  [exportDefaultBGColor](../classes/ListGrid_1.md#attr-listgridexportdefaultbgcolor)

If overriding any of the above methods, return null to allow methods later in the precedence order to influence background color. For example, if you want certain rows to have a special background color but also want to show alternating colors per row, override getExportRowBGColor and return null for all rows that should just show normal alternating colors, and not a special color.

---
