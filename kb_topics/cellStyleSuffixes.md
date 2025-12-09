# cellStyleSuffixes

[← Back to API Index](../reference.md)

---

## KB Topic: cellStyleSuffixes

### Description
As with [stateful canvases](../classes/StatefulCanvas.md#method-statefulcanvasgetstatesuffix), grid cells support being styled to reflect the current state of the cell by generating a css styleName from the specified [baseStyle](../classes/ListGrid_1.md#attr-listgridbasestyle), plus stateful suffixes.

There are six independent states, which are combined in the order given:

1.  "Disabled" : whether the cell is disabled; enable by setting the "enabled" flag on record returned by getCellRecord
2.  "Selected" : whether cell is selected; enable by passing a Selection object as "selection"
3.  "Over" : mouse is over this cell; enable with showRollovers
4.  [Specified alternateRowSuffix](../classes/GridRenderer.md#attr-gridrendereralternaterowsuffix) ("Dark" by default) : alternating row color bands; enable with alternateRowStyles
5.  [Specified alternateColumnSuffix](../classes/GridRenderer.md#attr-gridrendereralternatecolumnsuffix) ("AltCol" by default) : alternating column color bands; enable with alternateColumnStyles
6.  "Async" or "AsyncError" if the cell's value is being asynchronously computed, or an error occurred during the asynchronous computation; these are enabled with [DataBoundComponent.showAsyncValues](../classes/DataBoundComponent.md#attr-databoundcomponentshowasyncvalues)

This leads to the following set of standard style names:

| CSS Class Applied | Description | Example |
|---|---|---|
| baseStyle | Default css style for the cell | cell |
| baseStyle+alternateRowSuffix | Suffix for alternating color bands when [alternateRowStyles](../classes/GridRenderer.md#attr-gridrendereralternaterowstyles) is true | cellDark |
| baseStyle+alternateColumnSuffix | Suffix for alternating color bands when [alternateColumnStyles](../classes/GridRenderer.md#attr-gridrendereralternatecolumnstyles) is true | cellAltCol |
| baseStyle+Disabled | Whether the cell is disabled; enable by setting the "enabled" flag on record returned by getCellRecord. | cellDisabled |
| baseStyle+Selected | Whether the cell is [selected](../classes/ListGrid_2.md#method-listgridgetselectedrecord). Only applies if [ListGrid.showSelectedStyle](../classes/ListGrid_1.md#attr-listgridshowselectedstyle) is true | cellSelected |
| baseStyle+Over | Mouse is over this record. Only applies if [ListGrid.showRollOver](../classes/ListGrid_1.md#attr-listgridshowrollover) is true | cellOver |
| Combined styles |
| baseStyle+alternateRowSuffix+alternateColumnSuffix | Disabled style applied to cells in both alternate row and column color bands. | cellDarkAltCol |
| baseStyle+Disabled+alternateRowSuffix | Disabled style applied to cells in alternate row color bands. | cellDisabledDark |
| baseStyle+Disabled+alternateColumnSuffix | Disabled style applied to cells in alternate column color bands. | cellDisabledAltCol |
| baseStyle+Disabled++alternateRowSuffix+alternateColumnSuffix | Disabled style applied to cells in both alternate column and row color bands. | cellDisabledDarkAltCol |
| baseStyle+Selected+Over | Style applied to selected cells as the mouse rolls over them. | cellSelectedOver |
| baseStyle+Selected+alternateRowSuffix | Selected style applied to cells in alternate row color bands. | cellSelectedDark |
| baseStyle+Selected+alternateColumnSuffix | Selected style applied to cells in alternate column color bands. | cellSelectedAltCol |
| baseStyle+Selected+alternateRowSuffix+alternateColumnSuffix | Selected style applied to cells in both alternate row and column color bands. | cellSelectedDarkAltCol |
| baseStyle+Over+alternateRowSuffix | Style applied to alternate row color band cells as the mouse rolls over them. | cellOverDark |
| baseStyle+Over+alternateColumnSuffix | Style applied to alternate column color band cells as the mouse rolls over them. | cellOverAltCol |
| baseStyle+Over+alternateRowSuffix+alternateColumnSuffix | Style applied to cells in both alternate row and column color bands as the mouse rolls over them. | cellOverDarkAltCol |
| baseStyle+Selected+Over+alternateRowSuffix | Style applied to selected, alternate row color band cells as the mouse rolls over them. | cellSelectedOverDark |
| baseStyle+Selected+Over+alternateColumnSuffix | Style applied to selected, alternate column color band cells as the mouse rolls over them. | cellSelectedOverAltCol |
| baseStyle+Selected+Over+alternateRowSuffix+alternateColumnSuffix | Style applied to selected, alternate row and column color band cells as the mouse rolls over them. | cellSelectedOverDarkAltCol |

.. to which may be added "Async" or "AsyncError" suffixes.

---
