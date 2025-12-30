# GridRenderer Documentation

[← Back to API Index](../reference.md)

---

## Class: GridRenderer

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
A flexible, high-speed table that offers consistent cross-platform sizing, clipping, and events.

---
## Attr: GridRenderer.showClippedValuesOnHover

### Description
If true and a cell's value is clipped, then a hover containing the full cell value is enabled.

Note that standard cell hovers override clipped value hovers. Thus, to enable clipped value hovers, [canHover](#attr-gridrenderercanhover) must be unset or null and the corresponding field must have [showHover](ListGridField.md#attr-listgridfieldshowhover) unset or null as well.

### Groups

- events

### See Also

- [GridRenderer.canHover](#attr-gridrenderercanhover)
- [GridRenderer.cellValueHoverHTML](#method-gridrenderercellvaluehoverhtml)

**Flags**: IRWA

---
## Attr: GridRenderer.cellPadding

### Description
The amount of empty space, in pixels, surrounding each value in its cell.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: GridRenderer.baseStyle

### Description
The base name for the CSS class applied to cells. This style will have "Dark", "Over", "Selected", or "Disabled" appended to it according to the state of the cell.

### Groups

- cellStyling

### See Also

- [GridRenderer.getCellStyle](#method-gridrenderergetcellstyle)
- [GridRenderer.getBaseStyle](#method-gridrenderergetbasestyle)

**Flags**: IR

---
## Attr: GridRenderer.emptyCellValue

### Description
Value to show in empty cells (when getCellValue returns null).

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: GridRenderer.emptyMessage

### Description
The string to display in the body of a listGrid with an empty data array, if showEmptyMessage is true.

### Groups

- emptyMessage
- i18nMessages

### See Also

- [GridRenderer.showEmptyMessage](#attr-gridrenderershowemptymessage)
- [GridRenderer.emptyMessageStyle](#attr-gridrendereremptymessagestyle)

**Flags**: IRW

---
## Attr: GridRenderer.showHover

### Description
If true, and canHover is also true, when the user hovers over a cell, hover text will pop up next to the mouse. The contents of the hover is determined by [GridRenderer.cellHoverHTML](#method-gridrenderercellhoverhtml).

### Groups

- events

### See Also

- [GridRenderer.canHover](#attr-gridrenderercanhover)
- [GridRenderer.cellHoverHTML](#method-gridrenderercellhoverhtml)

**Flags**: RW

---
## Attr: GridRenderer.canSelectOnRightMouse

### Description
If true, rightMouseDown events will fire 'selectOnRightMouseDown()' for the appropriate cells.

### Groups

- events

**Flags**: RW

---
## Attr: GridRenderer.showHoverOnDisabledCells

### Description
If [GridRenderer.showHover](#attr-gridrenderershowhover) is true, should cell hover HTML be displayed on disabled cells?

**Flags**: IRWA

---
## Attr: GridRenderer.alternateColumnFrequency

### Description
The number of consecutive columns to draw in the same style before alternating, when [alternateColumnStyles](#attr-gridrendereralternatecolumnstyles) is true.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: GridRenderer.virtualScrolling

### Description
When incremental rendering is switched on and there are variable record heights, the virtual scrolling mechanism manages the differences in scroll height calculations due to the unknown sizes of unrendered rows to make the scrollbar and viewport appear correctly.

virtualScrolling is switched on automatically when fixedRowHeights is false but you should switch it on any time there are variable record heights.

**Flags**: IRA

---
## Attr: GridRenderer.drawAllMaxCells

### Description
If drawing all rows would cause less than `drawAllMaxCells` cells to be rendered, the full dataset will instead be drawn even if [showAllRecords](ListGrid_1.md#attr-listgridshowallrecords) is false and the viewport size and [GridRenderer.drawAheadRatio](#attr-gridrendererdrawaheadratio) setting would normally have caused incremental rendering to be used.

The `drawAllMaxCells` setting prevents incremental rendering from being used in situations where it's really unnecessary, such as a 40 row, 5 column dataset (only 200 cells) which happens to be in a grid with a viewport showing only 20 or so rows. Incremental rendering causes a brief "flash" during scrolling as the visible portion of the dataset is redrawn, and a better scrolling experience can be obtained in this situation by drawing the entire dataset up front, which in this example would have negligible effect on initial draw time.

`drawAllMaxCells:0` disables this features. You may want to disable this feature if performance is an issue and:

*   you are very frequently redraw a grid
*   you do a lot of computation when rendering each cell (eg formulas)
*   you are showing many grids on one screen and the user won't scroll most of them

### Groups

- performance

**Flags**: IRWA

---
## Attr: GridRenderer.alternateColumnStyles

### Description
Whether alternating columns (or blocks of columns, depending on [GridRenderer.alternateColumnFrequency](#attr-gridrendereralternatecolumnfrequency)) should be drawn in alternating styles, in order to create a vertical "ledger" effect for easier reading.

If enabled, the cell style for alternate rows will have the [GridRenderer.alternateColumnSuffix](#attr-gridrendereralternatecolumnsuffix) appended to it. See also [GridRenderer.alternateRowStyles](#attr-gridrendereralternaterowstyles).

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: GridRenderer.instantScrollTrackRedraw

### Description
If true, if the user clicks on the scroll buttons at the end of the track or clicks once on the scroll track, there will be an instant redraw of the grid content so that the user doesn't see any blank space. For drag scrolling or other types of scrolling, the [GridRenderer.scrollRedrawDelay](#attr-gridrendererscrollredrawdelay) applies.

### Groups

- performance

**Flags**: IRW

---
## Attr: GridRenderer.fixedColumnWidths

### Description
Should we horizontally clip cell contents, or allow columns to expand horizontally to show all contents?  
  
If we allow columns to expand, the column width is treated as a minimum.

### Groups

- sizing

**Flags**: IRWA

---
## Attr: GridRenderer.showOfflineMessage

### Description
Indicates whether the text of the offlineMessage property should be displayed if no data is available because we are offline and there is no suitable cached response

### Groups

- emptyMessage
- offlineGroup

### See Also

- [GridRenderer.offlineMessage](#attr-gridrendererofflinemessage)

**Flags**: IRW

---
## Attr: GridRenderer.cellHeight

### Description
The default height of each row in pixels.

### Groups

- cellStyling

### See Also

- [GridRenderer.getRowHeight](#method-gridrenderergetrowheight)

**Flags**: IRW

---
## Attr: GridRenderer.snapToCells

### Description
Should drag-and-drop operations snap the dragged object into line with the nearest cell?

### Groups

- dragdrop

**Flags**: IRW

---
## Attr: GridRenderer.offlineMessageStyle

### Description
The CSS style name applied to the offlineMessage string if displayed.

### Groups

- emptyMessage
- offlineGroup

**Flags**: IRW

---
## Attr: GridRenderer.emptyMessageStyle

### Description
The CSS style name applied to the emptyMessage string if displayed.

### Groups

- emptyMessage

**Flags**: IRW

---
## Attr: GridRenderer.autoFit

### Description
If true, make columns only wide enough to fit content, ignoring any widths specified. Overrides fixedFieldWidths.

### Groups

- sizing

**Flags**: IRWA

---
## Attr: GridRenderer.showAllColumns

### Description
Whether all columns should be drawn all at once, or only columns visible in the viewport.

Drawing all columns causes longer initial rendering time, but allows smoother horizontal scrolling. With a very large number of columns, showAllColumns will become too slow.

### Groups

- performance

**Flags**: IRA

---
## Attr: GridRenderer.scrollRedrawDelay

### Description
While drag scrolling in an incrementally rendered grid, time in milliseconds to wait before redrawing, after the last mouse movement by the user. This delay may be separately customized for mouse-wheel scrolling via [GridRenderer.scrollWheelRedrawDelay](#attr-gridrendererscrollwheelredrawdelay).

See also [GridRenderer.instantScrollTrackRedraw](#attr-gridrendererinstantscrolltrackredraw) for cases where this delay is skipped.

**NOTE:** In [touch browsers](Browser.md#classattr-browseristouch), [touchScrollRedrawDelay](#attr-gridrenderertouchscrollredrawdelay) is used instead.

### Groups

- performance
- scrolling

**Flags**: IRW

---
## Attr: GridRenderer.drawAheadRatio

### Description
How far should we render rows ahead of the currently visible area? This is expressed as a ratio from viewport size to rendered area size.

Tweaking drawAheadRatio allows you to make tradeoffs between continuous scrolling speed vs initial render time and render time when scrolling by large amounts.

NOTE: Only applies when showAllRows is false.

### Groups

- performance

**Flags**: IRWA

---
## Attr: GridRenderer.scrollWheelRedrawDelay

### Description
While scrolling an incrementally rendered grid, using the mouseWheel, time in milliseconds to wait before redrawing, after the last mouseWheel movement by the user. If not specified [GridRenderer.scrollRedrawDelay](#attr-gridrendererscrollredrawdelay) will be used as a default for both drag scrolling and mouseWheel scrolling.

See also [GridRenderer.instantScrollTrackRedraw](#attr-gridrendererinstantscrolltrackredraw) for cases where this delay is skipped.

### Groups

- performance

**Flags**: IRW

---
## Attr: GridRenderer.alternateColumnSuffix

### Description
Suffix to append to [alternate columns](#attr-gridrendereralternatecolumnstyles). Note that if [GridRenderer.alternateRowStyles](#attr-gridrendereralternaterowstyles) is enabled, cells which fall into both an alternate row and column will have both suffixes appended - for example `"cellDarkAltCol"`.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: GridRenderer.showSelectedStyle

### Description
Should the "Selected" style be applied to selected records?

### See Also

- [GridRenderer.getCellStyle](#method-gridrenderergetcellstyle)

**Flags**: IRW

---
## Attr: GridRenderer.alternateRowStyles

### Description
Whether alternating rows (or blocks of rows, depending on [GridRenderer.alternateRowFrequency](#attr-gridrendereralternaterowfrequency)) should be drawn in alternating styles, in order to create a "ledger" effect for easier reading.

If enabled, the cell style for alternate rows will have the [GridRenderer.alternateRowSuffix](#attr-gridrendereralternaterowsuffix) appended to it. See also [GridRenderer.alternateColumnStyles](#attr-gridrendereralternatecolumnstyles).

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: GridRenderer.dragScrollRedrawDelay

### Description
Like [GridRenderer.scrollRedrawDelay](#attr-gridrendererscrollredrawdelay), but applies when the component is being drag-scrolled (via a scrollbar). This value is typically set higher than [GridRenderer.scrollRedrawDelay](#attr-gridrendererscrollredrawdelay) to avoid too many concurrent fetches to the server for [ResultSet](ResultSet.md#class-resultset)-backed components since it's quite easy to induce such a case with a scrollbar and a grid bound to a large databaset.

### Groups

- performance
- scrolling

**Flags**: IRW

---
## Attr: GridRenderer.touchScrollRedrawDelay

### Description
In [touch browsers](Browser.md#classattr-browseristouch), the time in milliseconds to wait after a scroll before redrawing. In non-touch browsers, the [scrollRedrawDelay](#attr-gridrendererscrollredrawdelay) or [scrollWheelRedrawDelay](#attr-gridrendererscrollwheelredrawdelay) is used instead.

### Groups

- performance
- scrolling

**Flags**: IRW

---
## Attr: GridRenderer.quickDrawAheadRatio

### Description
Alternative to [GridRenderer.drawAheadRatio](#attr-gridrendererdrawaheadratio), to be used when the user is rapidly changing the grids viewport (for example drag scrolling through the grid). If unspecified [GridRenderer.drawAheadRatio](#attr-gridrendererdrawaheadratio) will be used in all cases

### Groups

- performance

**Flags**: IRWA

---
## Attr: GridRenderer.snapInsideBorder

### Description
If true, snap-to-cell drops will snap the dropped object inside the selected cell's border. If false, snap-to-cell drops will snap the dropped object to the edge of the selected cell, regardless of borders

### Groups

- dragdrop

### See Also

- [GridRenderer.snapToCells](#attr-gridrenderersnaptocells)

**Flags**: IRW

---
## Attr: GridRenderer.canHover

### Description
If true, cellHover and rowHover events will fire and then a hover will be shown (if not canceled) when the user leaves the mouse over a row / cell unless the corresponding field has [showHover](ListGridField.md#attr-listgridfieldshowhover) set to false. If unset or null, the hover will be shown if the corresponding field has showHover:true. If false, then hovers are disabled.

Note that standard hovers override [clipped value hovers](#attr-gridrenderershowclippedvaluesonhover). Thus, to enable clipped value hovers, canHover must be unset or null and the corresponding field must have showHover unset or null as well.

### Groups

- events

### See Also

- [GridRenderer.cellHover](#method-gridrenderercellhover)
- [GridRenderer.rowHover](#method-gridrendererrowhover)
- [GridRenderer.showHover](#attr-gridrenderershowhover)
- [GridRenderer.showClippedValuesOnHover](#attr-gridrenderershowclippedvaluesonhover)

**Flags**: RW

---
## Attr: GridRenderer.wrapCells

### Description
Should content within cells be allowed to wrap?

### Groups

- cellStyling

**Flags**: IRWA

---
## Attr: GridRenderer.showAllRows

### Description
Whether all rows should be drawn all at once, or only rows visible in the viewport.

Drawing all rows causes longer initial rendering time, but allows smoother vertical scrolling. With a very large number of rows, showAllRows will become too slow.

See also [GridRenderer.drawAheadRatio](#attr-gridrendererdrawaheadratio) and [GridRenderer.drawAllMaxCells](#attr-gridrendererdrawallmaxcells).

### Groups

- performance

**Flags**: IRA

---
## Attr: GridRenderer.showEmptyMessage

### Description
Indicates whether the text of the emptyMessage property should be displayed if no data is available.

### Groups

- emptyMessage

### See Also

- [GridRenderer.emptyMessage](#attr-gridrendereremptymessage)

**Flags**: IRW

---
## Attr: GridRenderer.totalRows

### Description
Total number of rows in the grid.  
  
NOTE: in order to create a valid grid, you must either provide a totalRows value or implement getTotalRows()

### See Also

- [GridRenderer.getTotalRows](#method-gridrenderergettotalrows)

**Flags**: IRW

---
## Attr: GridRenderer.alternateRowSuffix

### Description
Suffix to append to [alternate rows](#attr-gridrendereralternaterowstyles). Note that if [GridRenderer.alternateColumnStyles](#attr-gridrendereralternatecolumnstyles) is enabled, cells which fall into both an alternate row and column will have both suffixes appended - for example `"cellDarkAltCol"`.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: GridRenderer.offlineMessage

### Description
The string to display in the body of a listGrid with an empty data array, if showOfflineMessage is true and the data array is empty because we are offline and there is no suitable cached response

### Groups

- offlineGroup
- emptyMessage
- i18nMessages

### See Also

- [GridRenderer.showOfflineMessage](#attr-gridrenderershowofflinemessage)
- [GridRenderer.offlineMessageStyle](#attr-gridrendererofflinemessagestyle)

**Flags**: IRW

---
## Attr: GridRenderer.emptyMessageTableStyle

### Description
CSS styleName for the table as a whole if we're showing the empty message

### Groups

- emptyMessage

**Flags**: IRW

---
## Attr: GridRenderer.fastCellUpdates

### Description
**Note: This property only has an effect in Internet Explorer**

Advanced property to improve performance for dynamic styling of gridRenderer cells in Internet Explorer, at the expense of slightly slower initial drawing, and some limitations on supported styling options.

`fastCellUpdates` speeds up the dynamic styling system used by rollovers, selections, and custom styling that calls [GridRenderer.refreshCellStyle](#method-gridrendererrefreshcellstyle), at the cost of slightly slower draw() and redraw() times.

Notes:

*   When this property is set, ListGrid cells may be styled using the [ListGrid.tallBaseStyle](ListGrid_1.md#attr-listgridtallbasestyle). See [ListGrid.getBaseStyle](ListGrid_2.md#method-listgridgetbasestyle) for more information.
*   If any cell styles specify a a background image URL, the URL will be resolved relative to the page location rather than the location of the CSS stylesheet. This means cell styles with a background URL should either supply a fully qualified path, or the background image media should be made available at a second location for IE.
*   fastCellUpdates will not work if the styles involved are in an external stylesheet loaded from a remote host. Either the stylesheet containing cell styles needs to be loaded from the same host as the main page, or the cell styles need to be inlined in the html of the bootstrap page.
*   fastCellUpdates will not work if the css styles for cells are defined in a `.css` file loaded via `@import`. Instead the `.css` file should be loaded via a ``<link ...>`` tag.

**Flags**: IRWA

---
## Attr: GridRenderer.alternateRowFrequency

### Description
The number of consecutive rows to draw in the same style before alternating, when [alternateRowStyles](#attr-gridrendereralternaterowstyles) is true.

### Groups

- cellStyling

**Flags**: IRW

---
## Attr: GridRenderer.writeOutCellElementId

### Description
Should this Grid write an ID (obtained via [GridRenderer.getCellElementId](#method-gridrenderergetcellelementid)) into each cell element?

Note that for integration with automated testing tools, we recommend using [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) and [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) to identify specific elements within the DOM wherever possible. These are more robust than simple cell locators as they can identify the DOM element representing a specific data elements using primary key and other approaches rather than relying on the generated DOM structure.

Note that if [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode) is enabled, cell elements will be written out with a generated ID even if this property is false.  
The default generated [WAI-ARIA markup](ListGrid_1.md#attr-listgridariarole) for listGrids makes use of DOM IDs to identify rows and cells in various cases.

**Flags**: IRW

---
## Attr: GridRenderer.recordCustomStyleProperty

### Description
Denotes the name of a property that can be set on records to display a custom style. For example if this property is set to `"customStyle"`, setting `record.customStyle` to a css styleName will cause the record in question to render out with that styling applied to it. Note that this will be a static style - it will not be modified as the state of the record (selected / over etc) changes.

### See Also

- [GridRenderer.getCellStyle](#method-gridrenderergetcellstyle)

**Flags**: IRW

---
## Attr: GridRenderer.fixedRowHeights

### Description
Should we vertically clip cell contents, or allow rows to expand vertically to show all contents?

If we allow rows to expand, the row height as derived from [getRowHeight()](#method-gridrenderergetrowheight) or the default [GridRenderer.cellHeight](#attr-gridrenderercellheight) is treated as a minimum.

### Groups

- cellStyling

**Flags**: IRWA

---
## Attr: GridRenderer.writeOutRowElementId

### Description
Should this Grid write an ID (obtained via [GridRenderer.getRowElementId](#method-gridrenderergetrowelementid)) into each row element?

Note that for integration with automated testing tools, we recommend using [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) and [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) to identify specific elements within the DOM wherever possible. These are more robust than simple cell locators as they can identify the DOM element representing a specific data elements using primary key and other approaches rather than relying on the generated DOM structure.

Note that if [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode) is enabled, row elements will be written out with a generated ID even if this property is false.  
The default generated [WAI-ARIA markup](ListGrid_1.md#attr-listgridariarole) for listGrids makes use of DOM IDs to identify rows and cells in various cases.

**Flags**: IRW

---
## Method: GridRenderer.cellHover

### Description
Called when the mouse hovers over a cell if this.canHover is true. Returning false will suppress the hover text from being shown if this.showHover is true.

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

### See Also

- [GridRenderer.canHover](#attr-gridrenderercanhover)

**Flags**: A

---
## Method: GridRenderer.rowOut

### Description
Called when the mouse pointer leaves a row

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

**Flags**: A

---
## Method: GridRenderer.refreshCellStyle

### Description
Refresh the styling of an individual cell without redrawing the grid.

The cell's CSS class and CSS text will be refreshed, to the current values returned by getCellStyle() and getCellCSSText() respectively.

The cell's contents (as returned by getCellValue()) will **not** be refreshed. To refresh both styling and contents, call refreshCell() instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number of cell to refresh |
| colNum | [number](#type-number) | false | — | column number of cell to refresh |

### Groups

- appearance

### See Also

- [GridRenderer.refreshCell](#method-gridrendererrefreshcell)

---
## Method: GridRenderer.findRowNum

### Description
Given a record displayed in this grid, find and return the rowNum in which the record appears.

As with [GridRenderer.getCellRecord](#method-gridrenderergetcellrecord) implementing this method is optional as a valid grid may be created without any notion of records.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |

### Returns

`[number](#type-number)` — index of the row containing the record or -1 if not found

---
## Method: GridRenderer.getCellElementId

### Description
Get the DOM ID that should be used for a cell element if [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode) is enabled or [GridRenderer.writeOutRowElementId](#attr-gridrendererwriteoutrowelementid) is true.

Note that for integration with automated testing tools, we recommend using [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) and [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) to identify specific elements within the DOM wherever possible. These are more robust than simple cell locators as they can identify the DOM element representing a specific data elements using primary key and other approaches rather than relying on the generated DOM structure.

When using incremental rendering, the `rowNum` and `colNum` params represents virtual coordinates, and the `physicalRowNum` param represents the index that the row/cell will ultimately have in table.rows or row.cells.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | **virtual** row number |
| physicalRowNum | [number](#type-number) | false | — | **physical** row number |
| colNum | [number](#type-number) | false | — | **virtual** col number |
| physicalColNum | [number](#type-number) | false | — | **physical** col number |

### Returns

`[String](#type-string)` — ID for the cell element. This should be unique within the DOM.

**Flags**: A

---
## Method: GridRenderer.getRowHeight

### Description
Return the height this row should be. Default is this.cellHeight. If [GridRenderer.fixedRowHeights](#attr-gridrendererfixedrowheights) is false, the row may be rendered taller than this specified size.

If records will be variable height, you should switch on [virtualScrolling](#attr-gridrenderervirtualscrolling).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number |

### Returns

`[number](#type-number)` — height in pixels

---
## Method: GridRenderer.getNearestRowToEvent

### Description
Returns the nearest row to the event coordinates

### Groups

- events
- selection

---
## Method: GridRenderer.getDrawnRows

### Description
Get the rows that are currently drawn (exist in the DOM), as an array of \[firstRowNum, lastRowNum\].

The drawn rows differ from the [visibleRows](#method-gridrenderergetvisiblerows) because of [drawAhead](#attr-gridrendererdrawaheadratio). The drawn rows are the appropriate range to consider if you need to, eg, using [GridRenderer.refreshCell](#method-gridrendererrefreshcell) to update all the cells in a column.

If the grid is undrawn or the [GridRenderer.emptyMessage](#attr-gridrendereremptymessage) is currently shown, returns \[null,null\];

### Returns

`[Array](#type-array)` — —

---
## Method: GridRenderer.getCellRecord

### Description
Return the record that holds the value for this cell.

Implementing `getCellRecord` is optional: the actual HTML placed into each grid cell comes from `getCellValue`, and a valid grid can be created without any notion of "records" at all.

If you do implement `getCellRecord`, the value you return is passed to you as the "record" parameter in other methods.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[Object](../reference_2.md#type-object)` — record for this cell

---
## Method: GridRenderer.refreshRow

### Description
Refresh an entire row of cells without redrawing the grid.

The cells' values, CSS classes, and CSS text will be refreshed, to the current values returned by getCellValue(), getCellStyle() and getCellCSSText() respectively.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number of cell to refresh |

### Groups

- appearance

### See Also

- [GridRenderer.refreshCellStyle](#method-gridrendererrefreshcellstyle)
- [GridRenderer.refreshCell](#method-gridrendererrefreshcell)

**Flags**: A

---
## Method: GridRenderer.setColumnWidth

### Description
Sets the width of a single column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [number](#type-number) | false | — | the number of the column to resize |
| newWidth | [number](#type-number) | false | — | the new width |

---
## Method: GridRenderer.rowMouseDown

### Description
Called when a row receives a mousedown event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record object returned from 'getCellRecord()' |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.getRowTop

### Description
Returns the top coordinate for a given row number, relative to the top of body content. Use [GridRenderer.getRowPageTop](#method-gridrenderergetrowpagetop) for a page-relative coordinate.

This method is reliable only for rows that are currently drawn, which is generally only rows that are visible in the viewport. If row heights vary (see `fixedRowHeights`), coordinates for rows that are not currently shown are rough approximations.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | — |

### Returns

`[int](../reference.md#type-int)` — Y-coordinate

### Groups

- positioning

**Flags**: A

---
## Method: GridRenderer.setFastCellUpdates

### Description
Setter for [GridRenderer.fastCellUpdates](#attr-gridrendererfastcellupdates). Has no effect in browsers other than Internet Explorer.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fastCellUpdates | [boolean](../reference.md#type-boolean) | false | — | whether to enable fastCellUpdates. |

---
## Method: GridRenderer.getCellValue

### Description
Return the HTML to display in this cell. Implementing this is required to get a non-empty grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[String](#type-string)` — HTML to display in this cell

---
## Method: GridRenderer.getColumnPageLeft

### Description
Return the left coordinate for a given column number as a GLOBAL coordinate

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [Integer](../reference_2.md#type-integer) | false | — | number of the column |

### Returns

`[Integer](../reference_2.md#type-integer)` — page left offset of the passed colNum, or null if undrawn or no such column

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: GridRenderer.cellDoubleClick

### Description
Called when a cell receives a double click event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object returned from getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.rowOver

### Description
Called when the mouse pointer enters a row

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

**Flags**: A

---
## Method: GridRenderer.getEventColumn

### Description
Returns the column number of the most recent mouse event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../reference_2.md#type-integer) | true | — | optional x-coordinate to obtain column number for, in lieu of the x coordinate of the last mouse event |

### Returns

`[int](../reference.md#type-int)` — column number, or -2 if beyond last drawn column

### Groups

- events
- selection

---
## Method: GridRenderer.refreshCell

### Description
Refresh an individual cell without redrawing the grid.

The cell's value, CSS class, and CSS text will be refreshed, to the current values returned by getCellValue(), getCellStyle() and getCellCSSText() respectively.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number of cell to refresh |
| colNum | [number](#type-number) | false | — | column number of cell to refresh |

### Groups

- appearance

### See Also

- [GridRenderer.refreshCellStyle](#method-gridrendererrefreshcellstyle)

**Flags**: A

---
## Method: GridRenderer.getTotalRows

### Description
Return the total number of rows in the grid.  
  
NOTE: in order to create a valid grid, you must either provide a totalRows value or implement getTotalRows()

### Returns

`[number](#type-number)` — —

### See Also

- [GridRenderer.totalRows](#attr-gridrenderertotalrows)

---
## Method: GridRenderer.rowMouseUp

### Description
Called when a row receives a mouseup event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object returned from getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.getCellStyle

### Description
Return the CSS class for a cell. By default this method has the following implementation:  
\- return any custom style for the record ([GridRenderer.recordCustomStyleProperty](#attr-gridrendererrecordcustomstyleproperty)) if defined.  
\- create a style name based on the result of [GridRenderer.getBaseStyle](#method-gridrenderergetbasestyle) and the state of the record using the rules described in [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes).

Cell Styles are customizable by:

*   attaching a custom style to a record by setting `record[this.recordCustomStyleProperty]` to some valid CSS style name.
*   modifying the base style returned by getBaseStyle() \[see that method for further documentation on this\]
*   overriding this function

In addition to this, [getCellCSSText()](#method-gridrenderergetcellcsstext) may be overriden to provide custom cssText to apply on top of the styling attributes derived from the named style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record object for this row and column |
| rowNum | [number](#type-number) | false | — | number of the row |
| colNum | [number](#type-number) | false | — | number of the column |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS style for this cell

### Groups

- appearance

---
## Method: GridRenderer.cellValueHover

### Description
Optional stringMethod to fire when the user hovers over a cell and the value is clipped. If this.showClippedValuesOnHover is true, the default behavior is to show a hover canvas containing the HTML returned by cellValueHoverHTML(). Return false to suppress this default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard hover

### Groups

- events

### See Also

- [GridRenderer.showClippedValuesOnHover](#attr-gridrenderershowclippedvaluesonhover)
- [GridRenderer.cellValueIsClipped](#method-gridrenderercellvalueisclipped)
- [GridRenderer.cellValueHoverHTML](#method-gridrenderercellvaluehoverhtml)

**Flags**: A

---
## Method: GridRenderer.getRowElementId

### Description
Get the DOM ID that should be used for a row element if [screen reader mode](isc.md#staticmethod-iscsetscreenreadermode) is enabled or [GridRenderer.writeOutRowElementId](#attr-gridrendererwriteoutrowelementid) is true.

Note that for integration with automated testing tools, we recommend using [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) and [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) to identify specific elements within the DOM wherever possible. These are more robust than simple cell locators as they can identify the DOM element representing a specific data elements using primary key and other approaches rather than relying on the generated DOM structure.

When using incremental rendering, the `rowNum` param represents the rowNum in virtual coordinates, and the `physicalRowNum` param represents the index that the row will ultimately have in table.rows.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | **virtual** row number |
| physicalRowNum | [number](#type-number) | false | — | **physical** row number |

### Returns

`[String](#type-string)` — ID for the row element. This should be unique within the DOM.

**Flags**: A

---
## Method: GridRenderer.getCellRowSpan

### Description
When using [row spanning](#method-gridrenderergetrowspan), returns the number of cells spanned by the cell at the given coordinates.

If the passed coordinates are in the middle of a series of spanned cells, the row span of the spanning cell is returned. For example, if row 2 col 0 spans 3 cells, calls to `getCellRowSpan()` for row 2 col 0, row 3 col 0, row 4 col 0 will all return 3.

This method returns row span information for the current rendered cells. In contrast, if the grid is about to be redrawn, a call to `getRowSpan()` may return row span values for how the grid is about to be drawn. Also, user-provided getRowSpan() functions are not required to operate properly when called outside of the grid rendering loop.

**Note:** This method is a utility method for developers - it is not called directly by the grid rendering path and therefore is not intended for override. To set up custom row-spanning behavior, override [GridRenderer.getRowSpan](#method-gridrenderergetrowspan) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row number of cell to return the row span for |
| colNum | [int](../reference.md#type-int) | false | — | column number of cell to return the row span for |

### Returns

`[int](../reference.md#type-int)` — number of cells spanned by the cell that spans through these coordinates

---
## Method: GridRenderer.rowClick

### Description
Called when a row receives a click event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object returned from getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.cellIsEnabled

### Description
Whether this cell should be considered enabled. Affects whether events will fire for the cell, and the default styling behavior in getCellStyle.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether this record is enabled or not

### Groups

- selection
- appearance

**Flags**: A

---
## Method: GridRenderer.getBaseStyle

### Description
Return the base stylename for this cell. Default implementation just returns this.baseStyle. See [getCellStyle()](ListGrid_2.md#method-listgridgetcellstyle) for a general discussion of how to style cells.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — CSS class for this cell

### See Also

- [GridRenderer.getCellStyle](#method-gridrenderergetcellstyle)

**Flags**: A

---
## Method: GridRenderer.rowContextClick

### Description
Called when a row receives a contextclick event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.getCellPageRect

### Description
Returns the page offsets and size of the cell at the passed row and column. If auto-sizing is enabled, sizes are not definitive until the grid has finished drawing, so calling this method before drawing completes will return the configured column sizes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row index of the cell |
| colNum | [number](#type-number) | false | — | column index of the cell |

### Returns

`[Array of Integer](#type-array-of-integer)` — the page rect of the passed cell

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: GridRenderer.getColumnLeft

### Description
Return the left coordinate (in local coordinate space) of a particular column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [Integer](../reference_2.md#type-integer) | false | — | number of the column |

### Returns

`[Integer](../reference_2.md#type-integer)` — left coordinate of the passed colNum

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: GridRenderer.cellMouseDown

### Description
Called when a cell receives a mousedown event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.getCellFromDomElement

### Description
Given a pointer to an element in the DOM, this method will check whether this element is contained within a cell of the gridRenderer, and if so return a 2 element array denoting the `[rowNum,colNum]` of the element in question.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [DOMElement](#type-domelement) | false | — | DOM element to test |

### Returns

`[Array](#type-array)` — 2 element array containing rowNum and colNum, or null if the element is not contained in any cell in this gridRenderer

### Groups

- autoTest

**Flags**: A

---
## Method: GridRenderer.getEventRow

### Description
Returns the row number of the most recent mouse event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| y | [Integer](../reference_2.md#type-integer) | true | — | optional y-coordinate to obtain row number, in lieu of the y coordinate of the last mouse event |

### Returns

`[int](../reference.md#type-int)` — row number, or -2 if beyond last drawn row

### Groups

- events
- selection

---
## Method: GridRenderer.getCellHoverComponent

### Description
StringMethod to dynamically create a Canvas-based component to show as a hover window over the appropriate cell/record when this.canHover and this.showHover are both true and when an override of getCellHoverComponent() is present. Called when the mouse hovers over a cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[Canvas](#type-canvas)` — a Canvas to be shown as the hover for this cell

### Groups

- events

### See Also

- [GridRenderer.canHover](#attr-gridrenderercanhover)
- [GridRenderer.showHover](#attr-gridrenderershowhover)

**Flags**: A

---
## Method: GridRenderer.getVisibleRows

### Description
Get the rows that are currently visible in the viewport, as an array of \[firstRowNum, lastRowNum\].

If the grid contains no records, will return \[-1,-1\]. Will also return \[-1,-1\] if called at an invalid time (for example, data is in the process of being fetched - see [ResultSet.lengthIsKnown](ResultSet.md#method-resultsetlengthisknown)).

### Returns

`[Array of int](#type-array-of-int)` — —

---
## Method: GridRenderer.findColNum

### Description
Given a record displayed in this grid, find and return the colNum in which the record appears.

As with [GridRenderer.getCellRecord](#method-gridrenderergetcellrecord) implementing this method is optional as a valid grid may be created without any notion of records, or records may not be displayed in a single column (as with the [ListGrid](ListGrid_1.md#class-listgrid) class where each record is displayed in an entire row.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |

### Returns

`[number](#type-number)` — index of the column containing the record or -1 if not found

---
## Method: GridRenderer.cellMouseUp

### Description
Called when a cell receives a mouseup event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object (retrieved from getCellRecord(rowNum, colNum)) |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.cellHoverHTML

### Description
StringMethod to dynamically assemble an HTML string to show in a hover window over the appropriate cell/record when this.canHover and this.showHover are both true. Called when the mouse hovers over a cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the html to be shown inside the hover for this cell

### Groups

- events

### See Also

- [GridRenderer.canHover](#attr-gridrenderercanhover)
- [GridRenderer.showHover](#attr-gridrenderershowhover)

**Flags**: A

---
## Method: GridRenderer.getCellStartRow

### Description
When using [row spanning](#method-gridrenderergetrowspan), returns the row number where a row-spanning cell starts.

For example, if row 2 col 0 spans 3 cells, `getCellStartRow()` for row 2 col 0, row 3 col 0, row 4 col 0 will all return 2, because that's the row when spanning starts.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | row number of cell for which the start row should be returned |
| colNum | [int](../reference.md#type-int) | false | — | column number of cell for which the start row should be returned |

### Returns

`[int](../reference.md#type-int)` — row number where spanning starts

---
## Method: GridRenderer.cellSelectionChanged

### Description
Called when (cell-based) selection changes within this grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellList | [Array](#type-array) | false | — | Array of cells whos selected state was modified. |

### Returns

`[boolean](../reference.md#type-boolean)` — Returning false will prevent the GridRenderer styling from being updated to reflect the selection change.

### Groups

- selection

**Flags**: A

---
## Method: GridRenderer.cellOver

### Description
Called when the mouse pointer enters a cell

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

**Flags**: A

---
## Method: GridRenderer.getCellCSSText

### Description
Return CSS text for styling this cell, which will be applied in addition to the CSS class for the cell, as overrides.

"CSS text" means semicolon-separated style settings, suitable for inclusion in a CSS stylesheet or in a STYLE attribute of an HTML element.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[String](#type-string)` — CSS text for this cell

### See Also

- [GridRenderer.getCellStyle](#method-gridrenderergetcellstyle)

**Flags**: A

---
## Method: GridRenderer.cellOut

### Description
Called when the mouse pointer leaves a cell

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

**Flags**: A

---
## Method: GridRenderer.getNearestColToEvent

### Description
Returns the nearest column to the event coordinates

### Groups

- events
- selection

---
## Method: GridRenderer.cellValueHoverHTML

### Description
Returns the HTML that is displayed by the default cellValueHover handler. Return null or an empty string to cancel the hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |
| defaultHTML | [HTMLString](../reference.md#type-htmlstring) | false | — | the HTML that would have been displayed by default |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover. If null or an empty string, then the hover is canceled.

### Groups

- events

### See Also

- [GridRenderer.cellValueHover](#method-gridrenderercellvaluehover)

**Flags**: A

---
## Method: GridRenderer.getColumnWidth

### Description
Return the width of a particular column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [number](#type-number) | false | — | number of the column. |

### Returns

`[number](#type-number)` — width

### Groups

- sizing
- positioning

**Flags**: A

---
## Method: GridRenderer.setColumnWidths

### Description
Sets the width of all columns in the grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newWidths | [Array](#type-array) | false | — | array of new widths - one for each column. |

---
## Method: GridRenderer.getRowSpan

### Description
Return how many rows this cell should span. Default is 1.

NOTE: if using horizontal incremental rendering, `getRowSpan()` may be called for a rowNum **in the middle of a spanning cell**, and should return the remaining span from that rowNum onward.

NOTE: if a cell spans multiple rows, getCellRecord/Style/etc will be called with the topmost row coordinates only.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[number](#type-number)` — number of cells to span

**Flags**: A

---
## Method: GridRenderer.cellValueIsClipped

### Description
Is the value in a given cell clipped?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row number of the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[Boolean](#type-boolean)` — null if there is no cell at the given row, column; otherwise, whether the value in the specified cell is clipped.

### See Also

- [GridRenderer.cellValueHover](#method-gridrenderercellvaluehover)

**Flags**: A

---
## Method: GridRenderer.getRowPageTop

### Description
Returns the Y-coordinate for a given row number as a page-relative coordinate. See [GridRenderer.getRowTop](#method-gridrenderergetrowtop).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | — |

### Returns

`[int](../reference.md#type-int)` — Y-coordinate

### Groups

- positioning

**Flags**: A

---
## Method: GridRenderer.rowHover

### Description
Called when the mouse hovers over a row if this.canHover is true. Returning false will suppress the hover text from being shown if this.showHover is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | cell record as returned by getCellRecord |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event (default behavior of showing the hover)

### Groups

- events

### See Also

- [GridRenderer.canHover](#attr-gridrenderercanhover)

**Flags**: A

---
## Method: GridRenderer.rowDoubleClick

### Description
Called when a row receives a double click event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object returned from getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.cellClick

### Description
Called when a cell receives a click event.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | Record object returned from getCellRecord() |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### Groups

- events

**Flags**: A

---
## Method: GridRenderer.selectionChanged

### Description
Called when (row-based) selection changes within this grid. Note this method fires for each record for which selection is modified - so when a user clicks inside a grid this method will typically fire twice (once for the old record being deselected, and once for the new record being selected).

NOTE: For updating other components based on selections or triggering selection-oriented events within an application, see the [selectionUpdated()](DataBoundComponent.md#method-databoundcomponentselectionupdated) event which is likely more suitable. Calls to [getSelection()](Selection.md#method-selectiongetselection) from within this event may not return a valid set of selected records if the event has been triggered by a call to [selectAll()](Selection.md#method-selectionselectall) or [deselectAll()](Selection.md#method-selectiondeselectall) - in this case use the [selectionUpdated()](DataBoundComponent.md#method-databoundcomponentselectionupdated) event instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | record for which selection changed |
| state | [boolean](../reference.md#type-boolean) | false | — | New selection state (true for selected, false for unselected) |

### Groups

- selection

**Flags**: A

---
## Method: GridRenderer.cellContextClick

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

**Flags**: A

---
