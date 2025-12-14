# CubeGrid Documentation

[← Back to API Index](../reference.md)

---

## Class: CubeGrid

*Inherits from:* [ListGrid](ListGrid_1.md#class-listgrid)

### Description
The CubeGrid is an interactive grid component that presents very large, multi-dimensional data sets (also known as data cubes) for reporting or analytic applications.

CubeGrids are often called crosstabs, for their cross-tabular display of data dimensions in stacked/nested rows and columns, or pivot tables, for their ability to "pivot" dimensions between rows and columns to view a data cube from different perspectives. They are typically used in the querying and reporting front-ends of data warehousing, decision support, OLAP, and business intelligence systems.

For example, CubeGrids can be connected to Pentaho Mondrian, Jasper Reports, Microsoft Analysis Services and any other OLAP technology that supports the XMLA standard - the Isomorphic public wiki has [examples](http://wiki.smartclient.com/pages/viewpage.action?pageId=1441839). of such integration.

**NOTE:** you must load the Analytics [Optional Module](../kb_topics/loadingOptionalModules.md#kb-topic-loading-optional-modules) before you can use CubeGrid.

**Multi-Dimensional Data Terminology**

The CubeGrid refers to the dimensions of a data cube as facets, to the possible values in each facet as facet values, and to the values within the data cube as data values or cell values. Equivalent terms that are commonly used in data warehousing or business intelligence systems include:  
**facet:** dimension, attribute, feature  
**facet value:** dimension member, attribute value, feature value  
**cell value:** data value, metric value, measure

**Visual Structure**

Like the ListGrid and TreeGrid components, the CubeGrid displays data values in a tabular "body" with adjacent "headers". While the ListGrid and TreeGrid display rows of records with field values, the CubeGrid displays a body of individual cell values, each associated with a combination of facet values. The facet values for a cell are displayed in the column headers above the cell and row headers to the left of the cell. CubeGrids can display an arbitrary number of facets, by stacking multiple levels of row and/or column headers.

Except for the innermost column facet, each facet in a CubeGrid has a facet label adjacent to its row or column headers. The facet labels serve two main purposes: they display the titles of the facets, and they provide drag-and-drop reordering or pivoting of facets within the CubeGrid. The row facet labels also provide interactive selection, resizing, and other operations on the columns of row facet values.

The innermost column headers provide special behaviors and controls for manipulating the columns of data in a CubeGrid. End users may select, resize, reorder, minimize, maximize, or auto-fit the columns of data via mouse interactions with these headers. Customizable indicators and controls may be included at the top of each innermost column header.

If a CubeGrid is not large enough to display all of its cell values, horizontal and/or vertical scrollbars will appear below and to the right of the body. The body of the CubeGrid may be scrolled on either axis. The headers are "frozen" from scrolling on one axis - row headers only scroll vertically, while column headers only scroll horizontally - so the facet values for the visible cells are always displayed.

**Data Loading**

Data can be provided to the Cube via [CubeGrid.data](#attr-cubegriddata) as an Array of [CellRecords](../reference.md#object-cellrecord), each representing the data for one cell.

For large datasets, [provide a DataSource](#attr-cubegriddatasource) with one field per facetId, and the CubeGrid will load data on demand to fill the visible area, including lazily loading data for expanding/collapsing tree facets and when facetValues are made visible programmatically or via menus.

**Picking Facets**

By "facet" we mean an aspect of the data which is orthogonal to other aspects of the data, that is, combining values from any two "facets" should make sense.

For example, in sales data, two facets might be "quarter" and "region" - it makes sense to combine any quarter and region, although for some combinations, there may not be data available.

An example of two aspects that would **not** be independent facets are "state" and "city" - it's senseless to combine arbitrary states with arbitrary cities - most combinations are invalid. Consider instead a [tree facet](Facet.md#attr-facetistree) that combines "city" and "state" values.

Note that if "city" and "state" are represented as facets, they may look correct if they are both on the same axis of the grid and [hideEmptyFacetValues](#attr-cubegridhideemptyfacetvalues) is used to trim nonsense combinations, but if the data is [pivoted](#attr-cubegridcanmovefacets) such that "state" and "city" are on opposing axes, there will be a roughly diagonal "stripe" of data for combinations of "state" and "city" that make sense, and all other space will be blank. This is a strong indication that two facets should be represented as a single tree facet instead.

### See Also

- [Facet](Facet.md#class-facet)
- [FacetValue](../reference.md#object-facetvalue)

---
## ClassAttr: CubeGrid.ASCENDING

### Description
A declared value of the enum type [FacetIndentDirection](../reference.md#type-facetindentdirection).

**Flags**: R

---
## ClassAttr: CubeGrid.DESCENDING

### Description
A declared value of the enum type [FacetIndentDirection](../reference.md#type-facetindentdirection).

**Flags**: R

---
## Attr: CubeGrid.valueFormat

### Description
[FormatString](../reference.md#type-formatstring) for numeric or date formatting. See [DataSourceField.format](DataSourceField.md#attr-datasourcefieldformat).

### Groups

- exportFormatting

**Flags**: IR

---
## Attr: CubeGrid.editByCell

### Description
CubeGrids only support editing by cell.

### Groups

- cellEditing

**Flags**: R

---
## Attr: CubeGrid.hideEmptyFacetValues

### Description
This causes the headers for any combination of facetValues for which there are no cellRecords to be suppressed.

To use this feature, either:

*   all must be provided via [setData()](ListGrid_2.md#method-listgridsetdata) before the CubeGrid is first drawn, OR
*   all data must be returned by the first DataSource fetch, OR
*   [CubeGrid.hideEmptyAxis](#attr-cubegridhideemptyaxis) must be set to either "row" or "column" so that empty values are only automatically hidden for one axis

This last point is required because there is no way to determine whether a row is empty unless data for all columns of the row has been loaded (and vice-versa). For this reason if you set hideEmptyFacetValues but do not set hideEmptyAxis, the default behavior of [loading only visible data](DataSource.md#class-datasource) is automatically disabled and only [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues) will be sent as criteria.

### Groups

- facetLayout

**Flags**: IR

---
## Attr: CubeGrid.indentVTreeFacets

### Description
Turns on indenting of any [hierarchical](Facet.md#attr-facetistree) column facets. This can be overridden at the facet level via [Facet.indentVTree](Facet.md#attr-facetindentvtree). Setting this property also ensures that the header is sized tall enough to accommodate the fully expanded facet.

The amount of indenting per level can be set with [CubeGrid.vTreeFacetIndent](#attr-cubegridvtreefacetindent), and the direction of the indenting specified with [CubeGrid.vTreeFacetIndentDirection](#attr-cubegridvtreefacetindentdirection).

Note that if you specify an explicit height for such a fscet, such as by setting [Facet.height](Facet.md#attr-facetheight) or [Facet.labelHeight](Facet.md#attr-facetlabelheight), then the greater of that or the space required to accommodate the fully expanded facet will determine the actual height used.

### See Also

- [Facet.indentVTree](Facet.md#attr-facetindentvtree)
- [CubeGrid.vTreeFacetIndent](#attr-cubegridvtreefacetindent)
- [CubeGrid.vTreeFacetIndentDirection](#attr-cubegridvtreefacetindentdirection)

**Flags**: IR

---
## Attr: CubeGrid.canSelectHeaders

### Description
Determines whether row or column facetValue headers can be selected.

**Flags**: IRW

---
## Attr: CubeGrid.showHoverTipsTitle

### Description
Title for the show hover tips menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.dataSource

### Description
DataSource to use to fetch CubeGrid data.

The DataSource should have a field named after each facetId. The CubeGrid will submit requests for data as DataSource "fetch" operations that request [cellRecords](../reference.md#object-cellrecord) only for currently visible area (including [drawAheadRatio](ListGrid_1.md#attr-listgriddrawaheadratio)). The [Criteria](../reference_2.md#type-criteria) passed in each fetch operation will be a [FacetValueMap](../reference.md#object-facetvaluemap) that corresponds to a rectangular swath of cells the CubeGrid needs data for, for example:

```
      { region:"west", product:["chair", "table"], timePeriod:"Q1 2004" }
 
```
Note that in the criteria above, the Array value for the "product" facet indicates the CubeGrid needs cellRecords for both the "chair" and "table" facetValues.

[CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues), if any, are always sent in each "fetch" operation.

Scrolling, expanding/collapsing tree facets, pivoting, and changing the currently visible facets may all trigger data requests.

The CubeGrid will generally attempt to fetch a minimal set of data to fill the viewport, sending multiple fetch operations in a batch (via [queueing](RPCManager.md#classmethod-rpcmanagerstartqueue)) which minimally describe newly revealed areas without specifying each individual cell. The CubeGrid will automatically handle being provided _more_ data than was asked for, so server-side fetch-ahead policies can be implemented without any client-side customization.

Note that the [SQL connector](DataSource.md#attr-datasourceservertype) shipped with the SmartClient SDK is capable of responding to the CubeGrid's data requests without writing any custom server code.

**Flags**: IR

---
## Attr: CubeGrid.bodyMinWidth

### Description
Minimum width for the body of this cubeGrid.

### Groups

- gridLayout

**Flags**: IRWA

---
## Attr: CubeGrid.rowFacets

### Description
The list of [ids](Facet.md#attr-facetid) for facets that will appear to the left of the body.

### Groups

- facetLayout

### See Also

- [CubeGrid.rowHeaderGridMode](#attr-cubegridrowheadergridmode)

**Flags**: IR

---
## Attr: CubeGrid.valueProperty

### Description
Name of the property in a cell record that holds the cell value.

**Flags**: IR

---
## Attr: CubeGrid.canResizeColumns

### Description
If true, body columns can be resized via the innermost column headers.

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.vTreeFacetIndent

### Description
Determines how many pixels to move for each level when [hierarchical](Facet.md#attr-facetistree) column facets are being [indented](#attr-cubegridindentvtreefacets).

### See Also

- [CubeGrid.indentVTreeFacets](#attr-cubegridindentvtreefacets)

**Flags**: IR

---
## Attr: CubeGrid.chartItemTitle

### Description
Title for the Chart menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.showAllHighlightsTitle

### Description
Title for the show all highlights menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.colHeaderLabelBaseStyle

### Description
[baseStyle](Button.md#attr-buttonbasestyle) for the facet-label buttons above this grid's column headers.

### Groups

- appearance

**Flags**: IR

---
## Attr: CubeGrid.autoSelectValues

### Description
Whether to select cells in the body when row or column headers are selected.

**Flags**: IR

---
## Attr: CubeGrid.maximizeColumnTitle

### Description
Title for the maximize-column menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.canMoveFacets

### Description
Whether row and column facets can be rearranged by the user, by dragging and dropping the facet labels.

### Groups

- facetLayout

**Flags**: IRW

---
## Attr: CubeGrid.exportColumnFacetTextColor

### Description
Sets the text color for the column headers of the cube.

**Flags**: IR

---
## Attr: CubeGrid.facetLabelHoverAlign

### Description
Allows the developer to override the horizontal text alignment of hover tips shown for facetLabels. If unspecified the hover canvas content alignment will be set by `this.hoverAlign` if specified.

### Groups

- hoverTips

### See Also

- [Canvas.hoverAlign](Canvas.md#attr-canvashoveralign)

**Flags**: IRWA

---
## Attr: CubeGrid.chartTypeTitle

### Description
Title for the chart-type control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.styleName

### Description
CSS class for the CubeGrid as a whole

### Groups

- appearance

**Flags**: IRW

---
## Attr: CubeGrid.highlightCellTitle

### Description
Title for the cell highlight menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.facetLabelHoverVAlign

### Description
Allows the developer to override the vertical text alignment of hover tips shown for facetLabels. If unspecified the hover canvas content alignment will be set by `this.hoverVAlign` if specified.

### Groups

- hoverTips

### See Also

- [Canvas.hoverVAlign](Canvas.md#attr-canvashovervalign)

**Flags**: IRWA

---
## Attr: CubeGrid.renameFacetValueTitle

### Description
Title for the Rename menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.noHighlightsTitle

### Description
Title for the menu item that clears highlights.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.saveByCell

### Description
CubeGrids only support editing by cell.

### Groups

- cellEditing

**Flags**: R

---
## Attr: CubeGrid.highlightTitle

### Description
Title for the highlight menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.canSortFacets

### Description
If true, sort controls will be shown on FacetHeaders.

When clicked, sort controls call [CubeGrid.sortByFacetId](#method-cubegridsortbyfacetid).

**Flags**: IRW

---
## Attr: CubeGrid.exportFacetBGColor

### Description
Sets the background color for the row and column headers of the cube, if not otherwise set by a more specific property. (see [exportRowFacetBGColor()](#attr-cubegridexportrowfacetbgcolor) and [exportColumnFacetBGColor()](#attr-cubegridexportcolumnfacetbgcolor)). See also [exportBGColor](../kb_topics/exportBGColor.md#kb-topic-exports--cell-background-color).

**Flags**: IR

---
## Attr: CubeGrid.controlReorderHandleTitle

### Description
Title for the resizeHandle control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.chartDialogTitle

### Description
Title for the Chart dialog.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.valueTitle

### Description
A label for the data values shown in cells, such as "Sales in Thousands", typically used when the CubeGrid must generate a description for a cell value or set of cell values.

For example, in a CubeGrid showing "Revenue" by region and product, a cell with a CellRecord like:

```
 
 {product:"chairs", region:"northwest", _value:"$5k"}
 
```
Should be described as "Revenue for Chairs for Northwest Region", not "Chairs for Revenue for Northwest Region".

For CubeGrids that show multiple types of values at once (eg both "Revenue" and "Income") see [CubeGrid.metricFacetId](#attr-cubegridmetricfacetid).

**Flags**: IR

---
## Attr: CubeGrid.exportRowFacetBGColor

### Description
Sets the background color for the row headers of the cube. See also [exportBGColor](../kb_topics/exportBGColor.md#kb-topic-exports--cell-background-color).

**Flags**: IR

---
## Attr: CubeGrid.facetValueContextItems

### Description
Array of MenuItem to replace the default menu. Call [CubeGrid.getDefaultFacetValueContextItems](#method-cubegridgetdefaultfacetvaluecontextitems) to get a default set of items to start with.

**Flags**: IRW

---
## Attr: CubeGrid.facetValueHoverVAlign

### Description
Allows the developer to override the vertical text alignment of hover tips shown for facet values. If unspecified the hover canvas content alignment will be set by `this.hoverVAlign` if specified.

### Groups

- hoverTips

### See Also

- [Canvas.hoverVAlign](Canvas.md#attr-canvashovervalign)

**Flags**: IRWA

---
## Attr: CubeGrid.canReorderColumns

### Description
If true, body columns can be reordered via the innermost column headers.

### Groups

- facetLayout

**Flags**: IRW

---
## Attr: CubeGrid.autoFitFieldWidths

### Description
This property is not supported for `CubeGrid`.

Consider setting explicit widths via [FacetValue.width](FacetValue.md#attr-facetvaluewidth) or [CubeGrid.defaultFacetWidth](#attr-cubegriddefaultfacetwidth).

### Groups

- autoFitFields

**Flags**: IR

---
## Attr: CubeGrid.exportFacetSeparatorString

### Description
Default separator string used by [CubeGrid.exportClientData](#method-cubegridexportclientdata) to separate column and row facet value titles.

**Flags**: IRWA

---
## Attr: CubeGrid.chartType

### Description
Default type of chart to plot.

**Flags**: IRW

---
## Attr: CubeGrid.data

### Description
An array of "cellRecords", each of which represents data for one cell of the body area.

### See Also

- [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues)

**Flags**: IRW

---
## Attr: CubeGrid.controlMaximizeTitle

### Description
Title for the maximize control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.canSortData

### Description
If true, sort controls will be shown on facet values.

When clicked, sort controls call [CubeGrid.sortByFacetValues](#method-cubegridsortbyfacetvalues).

**Flags**: IRW

---
## Attr: CubeGrid.hideEmptyAxis

### Description
With [CubeGrid.hideEmptyFacetValues](#attr-cubegridhideemptyfacetvalues), controls on which axis hiding of empty values is applied, "row" (only empty rows are hidden), "column" (only empty columns are hidden) or both (the default).

### Groups

- facetLayout

**Flags**: IR

---
## Attr: CubeGrid.hilites

### Description
Hilites to be applied to the data for this component. See [hiliting](../kb_topics/hiliting.md#kb-topic-hiliting).

### Groups

- hiliting

**Flags**: IRW

---
## Attr: CubeGrid.renameFacetValueMessage

### Description
Message displayed when renaming a facet value.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.canMinimizeFacets

### Description
If true, when multiple facets are shown on a side, all facetValues in the second level of headers or higher will show controls to "minimize" the values of the next facet. Minimizing means showing only one, or very few, of the next facet's values.

Set [FacetValue.isMinimizeValue](FacetValue.md#attr-facetvalueisminimizevalue) to indicate which facetValues should be shown when a facet is minimized.

### Groups

- facetExpansion

**Flags**: IRW

---
## Attr: CubeGrid.vTreeFacetIndentDirection

### Description
Determines layout of facet value titles in each column facet being [indented](#attr-cubegridindentvtreefacets).

### See Also

- [CubeGrid.indentVTreeFacets](#attr-cubegridindentvtreefacets)

**Flags**: IRW

---
## Attr: CubeGrid.rollupValue

### Description
facetValueId of the default rollupValue for each facet. Can be overridden per facet via facet.rollupValue.

**Flags**: IR

---
## Attr: CubeGrid.showHighlightsTitle

### Description
Title for the show highlights menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.autoFitColumnTitle

### Description
Title for the auto-fit column menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.canEdit

### Description
Whether cells can be edited in this grid. Can be overridden on a per-facetValue basis.

### Groups

- cellEditing

**Flags**: IRW

---
## Attr: CubeGrid.rowHeaderGridMode

### Description
If enabled row headers for this cubeGrid will be rendered using a [GridRenderer](GridRenderer.md#class-gridrenderer) component. This improves performance for very large cubeGrids.

Note that this attribute must be set for hierarchical row facets to be indented properly.

### See Also

- [CubeGrid.rowFacets](#attr-cubegridrowfacets)
- [CubeGrid.canCollapseFacets](#attr-cubegridcancollapsefacets)

**Flags**: IRA

---
## Attr: CubeGrid.controlSortDownTitle

### Description
Title for the sort-down control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.sortDirection

### Description
Direction of sorting if sortedFacet or sortedFacetValues is specified.

**Flags**: IRW

---
## Attr: CubeGrid.facetValueAlign

### Description
Default alignment for facet values (in headers).

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.valueExportFormat

### Description
[FormatString](../reference.md#type-formatstring) used during exports for numeric or date formatting. See [DataSourceField.exportFormat](DataSourceField.md#attr-datasourcefieldexportformat).

### Groups

- exportFormatting

**Flags**: IR

---
## Attr: CubeGrid.facetTitleAlign

### Description
Default alignment for facet labels.

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.exportFacetTextColor

### Description
Sets the text color for the row and column headers of the cube, if not otherwise set by a more specific property. (see [exportRowFacetTextColor()](#attr-cubegridexportrowfacettextcolor) and [exportColumnFacetTextColor()](#attr-cubegridexportcolumnfacettextcolor)).

**Flags**: IR

---
## Attr: CubeGrid.controlCloseTitle

### Description
Title for the close control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.autoSelectHeaders

### Description
If true, when multiple facets appear on one side in a nested headers presentation, the selection state of parent/child headers are automatically kept in sync.

**Flags**: IRW

---
## Attr: CubeGrid.facets

### Description
Facet definitions for this CubeGrid. Facets, also called "dimensions", are orthogonal aspects of the data model.

For example, you can look at profit by the facets "plant and product" or by "product and plant" and it's the same number, because the facets - plant and product - are the same. What would change the profit numbers would be to remove a facet, called "summarizing", or add a new facet, called "drilling down". For example, showing profit by plant and product, you could "drill down" by adding the region facet, which would divide profit among each region. Or you could remove the "plant" facet, showing total profit for each "product", summed across all plants.

This property need not be set and will automatically be constructed during widget initialization if data is provided up front and [CubeGrid.rowFacets](#attr-cubegridrowfacets) and [CubeGrid.columnFacets](#attr-cubegridcolumnfacets) have been set. If [CubeGrid.facets](#attr-cubegridfacets) is not set and there is no initial data but a DataSource is present, drawing the grid will automatically issue a fetch to allow [CubeGrid.facets](#attr-cubegridfacets) to be resolved.

### See Also

- [CubeGrid.getFacet](#method-cubegridgetfacet)
- [Facet](Facet.md#class-facet)
- [CubeGrid.getFacetValue](#method-cubegridgetfacetvalue)
- [FacetValue](../reference.md#object-facetvalue)

**Flags**: I

---
## Attr: CubeGrid.metricFacetId

### Description
In a CubeGrid that displays values of different types (eg "Revenue" and "Income"), the different types of values on display are enumerated as the facet values of the "metric facet".

The metric facet is treated identically to any other facet by the CubeGrid: it can be represented as row or column headers, can be innermost or have other facets under it, can be moved around, etc. However when a metric facet is used, [CubeGrid.metricFacetId](#attr-cubegridmetricfacetid) must be set to allow the CubeGrid to generate meaningful descriptions of values shown in cells for use in hovers and other situations; see [CubeGrid.valueTitle](#attr-cubegridvaluetitle) for a full explanation.

**Flags**: IR

---
## Attr: CubeGrid.canCollapseFacets

### Description
If true, hierarchical facets will show expand/collapse controls to allow the user to expand and collapse the tree of facetValues for that facet.

### Groups

- facetExpansion

### See Also

- [CubeGrid.rowHeaderGridMode](#attr-cubegridrowheadergridmode)

**Flags**: IRW

---
## Attr: CubeGrid.innerHeaderBaseStyle

### Description
[baseStyle](Button.md#attr-buttonbasestyle) for the buttons in the innermost column header for this cubeGrid.

### Groups

- appearance

**Flags**: IR

---
## Attr: CubeGrid.rowHeaderBaseStyle

### Description
[baseStyle](Button.md#attr-buttonbasestyle) for the buttons in this grid's row headers.

### Groups

- appearance

**Flags**: IR

---
## Attr: CubeGrid.cellAlign

### Description
Default align for cell values (in body).

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.simpleDeselect

### Description
If true, clicking on the existing selection causes it to be entirely deselected.

**Flags**: IRW

---
## Attr: CubeGrid.wrapFacetTitles

### Description
Whether to allow text wrapping on facet titles.

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.bodyStyleName

### Description
CSS class for the CubeGrid body

### Groups

- appearance

**Flags**: IRW

---
## Attr: CubeGrid.canMinimizeColumns

### Description
If true, allow columns in the grid body to be minimized (reduced to the width of the minimize control) by clicking on a minimize control in the innermost column headers.

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.showFacetContextMenus

### Description
If true, show facet label context menus with some built-in operations. Otherwise, use generic context menu handling.

**Flags**: IRW

---
## Attr: CubeGrid.controlMinimizeTitle

### Description
Title for the minimize control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.hideAllHighlightsTitle

### Description
Title for the hide all highlights menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.colHeaderBaseStyle

### Description
[baseStyle](Button.md#attr-buttonbasestyle) for the buttons in this grid's column headers.

Exception: The innermost column header will always be styled using [CubeGrid.innerHeaderBaseStyle](#attr-cubegridinnerheaderbasestyle).

### Groups

- appearance

**Flags**: IR

---
## Attr: CubeGrid.exportColumnFacetBGColor

### Description
Sets the background color for the column headers of the cube. See also [exportBGColor](../kb_topics/exportBGColor.md#kb-topic-exports--cell-background-color).

**Flags**: IR

---
## Attr: CubeGrid.defaultFacetWidth

### Description
Default width of inner column headers.

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.cellIdProperty

### Description
Name of the property in a cell record that holds it's unique ID. Note cell record IDs are optional.

**Flags**: IR

---
## Attr: CubeGrid.bodyMinHeight

### Description
Minimum height for the body of this cubeGrid.

### Groups

- gridLayout

**Flags**: IRWA

---
## Attr: CubeGrid.chartStackedTitle

### Description
Title for the stacked chart item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.facetValueHoverAlign

### Description
Allows the developer to override the horizontal text alignment of hover tips shown for facet values. If unspecified the hover canvas content alignment will be set by `this.hoverAlign` if specified.

### Groups

- hoverTips

### See Also

- [Canvas.hoverAlign](Canvas.md#attr-canvashoveralign)

**Flags**: IRWA

---
## Attr: CubeGrid.alternateRecordStyles

### Description
Whether alternating rows should be drawn in alternating styles, in order to create a "ledger" effect for easier reading. If enabled, the cell style for alternate rows will have "Dark" appended to it.

### Groups

- appearance

**Flags**: IRW

---
## Attr: CubeGrid.padTitles

### Description
Whether to pad titles so they aren't flush with header borders.

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.exportRowFacetTextColor

### Description
Sets the text color for the row headers of the cube.

**Flags**: IR

---
## Attr: CubeGrid.rotateHeaderTitles

### Description
This property is not supported for `CubeGrid`.

**Flags**: IR

---
## Attr: CubeGrid.wrapFacetValueTitles

### Description
Whether to allow text wrapping on facet value titles.

Note that this property is incompatible with [indented](#attr-cubegridindentvtreefacets) column facets.

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.canDragSelect

### Description
For [touch browsers](Browser.md#classattr-browseristouch), `canDragSelect` defaults to false so that touch scrolling can be used to navigate scrollable CubeGrids. In all other browsers it defaults to true.

**NOTE:** If `canDragSelect` is enabled, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging cells of the CubeGrid selects them rather than starting a scroll. If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag-selection.

**Flags**: IR

---
## Attr: CubeGrid.canSelectValues

### Description
Determines whether cell values in the body can be selected.

**Flags**: IRW

---
## Attr: CubeGrid.autoFetchTextMatchStyle

### Description
If [CubeGrid.autoFetchData](#attr-cubegridautofetchdata) is `true`, this attribute allows the developer to specify a textMatchStyle for the initial [fetchData()](ListGrid_1.md#method-listgridfetchdata) call.

### Groups

- databinding

**Flags**: IR

---
## Attr: CubeGrid.columnFacets

### Description
The list of [ids](Facet.md#attr-facetid) for facets that will appear on top of the body.

### Groups

- facetLayout

**Flags**: IR

---
## Attr: CubeGrid.controlSortUpTitle

### Description
Title for the sort-up control.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.showFacetValueContextMenus

### Description
If true, show facet value context menus with some built-in operations. Otherwise, use generic context menu handling. Use this in place of [ListGrid.showHeaderContextMenu](ListGrid_1.md#attr-listgridshowheadercontextmenu) and [ListGrid.showHeaderMenuButton](ListGrid_1.md#attr-listgridshowheadermenubutton) for CubeGrids.

**Flags**: IRW

---
## Attr: CubeGrid.facetValueHoverWidth

### Description
If specified and `this.showHover` is true, this is the default width to apply to hover tips shown for facetValues. If unset, the hover canvas will be sized to `this.hoverWidth` if specified instead.

### Groups

- hoverTips

### See Also

- [Canvas.hoverWidth](Canvas.md#attr-canvashoverwidth)

**Flags**: IRWA

---
## Attr: CubeGrid.chartConstructor

### Description
Name of the SmartClient Class to be used when creating charts. Must support the [Chart](../reference_2.md#interface-chart) interface.

**Flags**: IR

---
## Attr: CubeGrid.facetLabelHoverHeight

### Description
If specified and `this.showHover` is true, this is the default height to apply to hover tips shown for facetLabels. If unset, the hover canvas will be sized to `this.hoverHeight` if specified instead.

### Groups

- hoverTips

### See Also

- [Canvas.hoverHeight](Canvas.md#attr-canvashoverheight)

**Flags**: IRWA

---
## Attr: CubeGrid.highlightSelectionTitle

### Description
Title for the selection highlight menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.facetLabelHoverWidth

### Description
If specified and `this.showHover` is true, this is the default width to apply to hover tips shown for facetLabels. If unset, the hover canvas will be sized to `this.hoverWidth` if specified instead.

### Groups

- hoverTips

### See Also

- [Canvas.hoverWidth](Canvas.md#attr-canvashoverwidth)

**Flags**: IRWA

---
## Attr: CubeGrid.fieldVisibilitySubmenuTitle

### Description
Title for the Field-visibility submenu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.enableCharting

### Description
If set to true, context menu items will be included on the cells and headers providing the user with an option to create a chart of the cubeGrid's data set. See [CubeGrid.makeChart](#method-cubegridmakechart) for more information.

**Flags**: IRW

---
## Attr: CubeGrid.rowHeaderLabelBaseStyle

### Description
[baseStyle](Button.md#attr-buttonbasestyle) for the facet-label buttons above the grid's row headers.

### Groups

- appearance

**Flags**: IR

---
## Attr: CubeGrid.facetValueHoverHeight

### Description
If specified and `this.showHover` is true, this is the default height to apply to hover tips shown for facetValues. If unset, the hover canvas will be sized to `this.hoverHeight` if specified instead.

### Groups

- hoverTips

### See Also

- [Canvas.hoverHeight](Canvas.md#attr-canvashoverheight)

**Flags**: IRWA

---
## Attr: CubeGrid.skinImgDir

### Description
Default directory for skin images (those defined by the class), relative to the Page-wide [skinDir](Page.md#classmethod-pagegetskindir).

### Groups

- images

**Flags**: IR

---
## Attr: CubeGrid.fixedFacetValues

### Description
A [FacetValueMap](../reference.md#object-facetvaluemap) describing the set of facet values that should be regarded as "fixed" in this cubeGrid. These are used as fixed criteria for load on demand, and also allow using a dataset with more facets in it than are currently shown in the grid.

### See Also

- [CubeGrid.addFacet](#method-cubegridaddfacet)
- [CubeGrid.removeFacet](#method-cubegridremovefacet)

**Flags**: IR

---
## Attr: CubeGrid.minimizeColumnTitle

### Description
Title for the minimize-column menu item.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: CubeGrid.facetValueHoverStyle

### Description
Allows the developer to override the css class applied to hover tips shown for facet values. If unspecified, and `this.hoverStyle` is not null, that css class will be applied to facet value hovers instead.

### Groups

- hoverTips

### See Also

- [Canvas.hoverStyle](Canvas.md#attr-canvashoverstyle)

**Flags**: IRWA

---
## Attr: CubeGrid.facetLabelHoverStyle

### Description
Allows the developer to override the css class applied to hover tips shown for facet labels. If unspecified, and `this.hoverStyle` is not null, that css class will be applied to facet label hovers instead.

### Groups

- hoverTips

### See Also

- [Canvas.hoverStyle](Canvas.md#attr-canvashoverstyle)

**Flags**: IRWA

---
## Attr: CubeGrid.sortedFacetValues

### Description
[FacetValueMap](../reference.md#object-facetvaluemap) of facet values representing a set of facetValues by which the cubeGrid data is sorted.

**Flags**: IRW

---
## Attr: CubeGrid.chartConfirmThreshold

### Description
If [CubeGrid.makeChart](#method-cubegridmakechart) is called with a chart specification that will show more than `chartConfirmThreshold` data elements, the user will be presented with a [confirmation dialog](isc.md#staticmethod-iscconfirm).

Set to 0 to disable this confirmation.

**Flags**: IR

---
## Attr: CubeGrid.baseStyle

### Description
[base cell style](GridRenderer.md#attr-gridrendererbasestyle) for this listGrid. If this property is unset, base style may be derived from [ListGrid.normalBaseStyle](ListGrid_1.md#attr-listgridnormalbasestyle) or [ListGrid.tallBaseStyle](ListGrid_1.md#attr-listgridtallbasestyle) as described in [ListGrid.getBaseStyle](ListGrid_2.md#method-listgridgetbasestyle).

See [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) for details on how stateful suffixes are combined with the base style to generate stateful cell styles.

### Groups

- appearance

**Flags**: IR

---
## Attr: CubeGrid.autoSizeHeaders

### Description
Automatically size row headers to fit wrapped text.

### Groups

- gridLayout

**Flags**: IRW

---
## Attr: CubeGrid.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [initialCriteria](ListGrid_1.md#attr-listgridinitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_1.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [initialCriteria](ListGrid_1.md#attr-listgridinitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_1.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- databinding

### See Also

- [ListGrid.fetchData](ListGrid_1.md#method-listgridfetchdata)

**Flags**: IR

---
## Method: CubeGrid.collapseField

### Description
Collapses the specified field. No-ops if it's not showing, or it it's already collapsed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValueMap | [FacetValueMap](#type-facetvaluemap) | false | — | field specified as a facetValueMap |

### Returns

`[Boolean](#type-boolean)` — whether specified field was actually collapsed

---
## Method: CubeGrid.facetLabelClick

### Description
Method handler fired when the user clicks on a facet label.

### Groups

- events

---
## Method: CubeGrid.getSelectedCells

### Description
Returns an array of the selected cell records.  
_methodType_ getter

### Returns

`[Array of CellRecord](#type-array-of-cellrecord)` — array of the selected cell records

### Groups

- selection

---
## Method: CubeGrid.recordHasChanges

### Description
If this cubeGrid can be edited, this method will return true if the record passed in has been edited, but the edits have not yet been saved to the CubeGrid's data object.

Note that if this grid is bound to a [dataSource](ListGrid_1.md#attr-listgriddatasource), and an asynchronous save has been submitted, this method will compare the local edit values against the submitted values by default, returning false (no changes), if they match. This is useful for detecting whether the user is actively editing values and hasn't yet committed them.

The `ignorePendingValues` parameter may be used by developers who want to ignore this case and simply compare edit values against the record in the local data set.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row index of record to check for changes |
| colNum | [number](#type-number) | false | — | column index of the record to check for changes |
| ignorePendingValues | [Boolean](#type-boolean) | true | — | If true, this method will compare the current edit values against the underlying records in the dataset, not taking pending edit values into account |

### Returns

`[Boolean](#type-boolean)` — true if the record has been edited but not yet saved

### Groups

- editing

---
## Method: CubeGrid.setFacetTitle

### Description
Set the title of a facet (appears in facet label).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facet to update |
| newTitle | [String](#type-string) | false | — | title for the facet |

### Groups

- metadata

---
## Method: CubeGrid.selectFacetValue

### Description
Select/deselect the header for a given facet value.  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of facet |
| facetValueId | [String](#type-string) | false | — | ID of facetValue to select |
| newState | [Boolean](#type-boolean) | true | — | new selection state - if null defaults to true |

### Groups

- selection

---
## Method: CubeGrid.getRowHeaderFacetValues

### Description
Return a [FacetValueMap](../reference.md#object-facetvaluemap) of the facet values for the row field at the specified level containing the requested row number. Note that outer row fields may span several grid rows.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [int](../reference.md#type-int) | false | — | 0-based index into the grid rows (and inner row header fields) |
| level | [int](../reference.md#type-int) | false | — | target header level; 0 represents the outer row header |

### Returns

`[FacetValueMap](#type-facetvaluemap)` — facet values for the targeted row header field

---
## Method: CubeGrid.exportClientData

### Description
Exports this component's data with client-side formatters applied, so is suitable for direct display to users. This feature requires the SmartClient server.

The export format will combine the column facet value titles, generating a single row of column headers at the top with titles such as "All Years - Budget" if Time and Scenario were column facets. The row facet value titles for separate facets won't be combined, so that each row facet will have a separate column, with the facet titles at the top in the "column header" row, and the row facet value titles below their corresponding facet title. Data values each get their own row and column position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [Object](../reference.md#type-object) | false | — | contains configuration settings for the export, including:

*   facetSeparatorString (String) - if specified, the separator to use in favor of [CubeGrid.exportFacetSeparatorString](#attr-cubegridexportfacetseparatorstring) when combining titles from multiple facet values. |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Request properties for the export. |
| callback | [RPCCallback](#type-rpccallback) | true | — | Optional callback. If you specify [exportToClient](DSRequest.md#attr-dsrequestexporttoclient): false in the request properties, this callback will fire after export completes. Otherwise the callback will fire right before the download request is made to the server. |

### See Also

- [ListGrid.exportClientData](ListGrid_1.md#method-listgridexportclientdata)

---
## Method: CubeGrid.facetValueHover

### Description
StringMethod handler fired when mouse hovers over a facetValue button in a header.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | FacetValueMap for the appropriate header button |

### Groups

- events

---
## Method: CubeGrid.expandField

### Description
Expands the specified field. No-ops if it's not showing, or if it's already expanded.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValueMap | [FacetValueMap](#type-facetvaluemap) | false | — | field specified as a facetValueMap |

### Returns

`[Boolean](#type-boolean)` — whether specified field was actually expanded

---
## Method: CubeGrid.getRollupValue

### Description
Get the facetValue definition for the facetValue to show when this facet is "rolled up" under another facet, during a breakout.  
  
A facet is not required to have a rollup value, and if it does not have one, then rollups will simply be blank rows. The facetValueId of the rollup value can be declared as cubeGrid.rollupValue or facet.rollupValue.

### Returns

`[String](#type-string)` — rolled up facet value definition

### See Also

- [CubeGrid.rollupValue](#attr-cubegridrollupvalue)

---
## Method: CubeGrid.removeFacet

### Description
Remove a facet from the current view, using a fixed value from that facet. For example, remove the "months" facet from the view, collapsing to just January, or total for all months.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facetId to remove |
| fixedFacetValueId | [Identifier](../reference.md#type-identifier) | true | — | New fixed value for the facet, to be added to [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues). Default is the rollup value for the facet. |

### Groups

- facetLayout

### See Also

- [CubeGrid.addFacet](#method-cubegridaddfacet)
- [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues)

---
## Method: CubeGrid.hiliteFacetValue

### Description
Apply a hilite to all cells corresponding to a facetValue.  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetID | [String](#type-string) | false | — | facet ID |
| facetValueID | [String](#type-string) | false | — | facet value ID |
| hiliteID | [String](#type-string) | false | — | hilite ID |

### Returns

`[Boolean](#type-boolean)` — true if the cells were successfully hilited.

### Groups

- hiliting

---
## Method: CubeGrid.getFacetValuesRow

### Description
Get the index of the first row in the grid that matches the specified FacetValueMap.

The facetValues passed in should contain values for at least one row facet. It may contain properties other than row facets, which will be ignored. If values are sparse (values not specified for every row facet), the first row matching the specified facet values will be returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facet values to find |

### Returns

`[int](../reference.md#type-int)` — index of first row in the grid that matches the facet values passed in, or -1 if not found

---
## Method: CubeGrid.getRowFacetValues

### Description
Return a [FacetValueMap](../reference.md#object-facetvaluemap) indicating the facet values for a specific row in the grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | index of the row |

### Returns

`[FacetValueMap](#type-facetvaluemap)` — facet values for the specified row. Returns null if the specified row is not present in the grid.

---
## Method: CubeGrid.getCellCoordinates

### Description
Given a record in this grid, this method returns the coordinates of the cell in which the record is displayed as a 2 element array.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [CellRecord](#type-cellrecord) | false | — | record to find coordinates for |

### Returns

`[Array](#type-array)` — 2 element array containing `[rowNum,colNum]` for the cell, or `null` if the record is not found.

---
## Method: CubeGrid.getBaseStyle

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

- [CubeGrid.getCellStyle](#method-cubegridgetcellstyle)

---
## Method: CubeGrid.facetValueReordered

### Description
Notification fired when a facet or facetValueGroup is reordered

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupId | [String](#type-string) | false | — | facetValueGroupId or facetId |

### Groups

- facetLayout

---
## Method: CubeGrid.facetValuesSelected

### Description
Return whether the header indicated by the set of facetValues is selected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facetValues to test |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the header is selected

### Groups

- selection

---
## Method: CubeGrid.sortByFacetValues

### Description
Called when a sort control is clicked on a FacetValueHeader. Does nothing by default.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facetValues to sort |
| sortDirection | [boolean](../reference.md#type-boolean) | false | — | true for ascending |

### Groups

- columnControls

---
## Method: CubeGrid.getEditValues

### Description
Returns the current set of unsaved edits for a given row being edited.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valuesID | [number](#type-number)|[Object](../reference.md#type-object) | false | — | rowNum of the record being edited, or an Object containing values for all the record's primary keys |
| colNum | [number](#type-number) | false | — | colNum of the record being edited. Only required if valuesID is passed in as a rowNum. |

### Returns

`[Object](../reference.md#type-object)` — Current editValues object for the row. This contains the current edit values in {fieldName1:value1, fieldName2:value2} format.

### Groups

- editing

---
## Method: CubeGrid.deselectCells

### Description
Deselect cells that match a [FacetValueMap](../reference.md#object-facetvaluemap). Also supports an explicit list of CellRecords or cell IDs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellList | [Array of CellRecord[]](#type-array-of-cellrecord)|[FacetValueMap](#type-facetvaluemap)|[Array of ID](#type-array-of-id) | false | — | cells to deselect |

### Groups

- selection

---
## Method: CubeGrid.getEventRow

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
## Method: CubeGrid.getFacetValueLayout

### Description
Get the current visual order and width for the facet values of a facet or facetValueGroup as an object of the form:
```
 [ {id:facetValueId, width:currentWidth }, ... ]
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [FacetValueGroupId](#type-facetvaluegroupid)|[FacetId](#type-facetid) | false | — | Which facet do we want details for? |

### Returns

`[Array](#type-array)` — array of {id:facetValueId, width:width} objects

### Groups

- facetLayout

---
## Method: CubeGrid.fixedFacetValueChanged

### Description
Notification fired when a fixed facet value is set for some facet.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | facetId |
| facetValueId | [String](#type-string) | false | — | new fixed facet value |

### See Also

- [CubeGrid.setFixedFacetValue](#method-cubegridsetfixedfacetvalue)

---
## Method: CubeGrid.addFacet

### Description
Add a facet to the view, into the row or column facets (intoRows true or false), at index "index". Handles the facet already being in the view (does a pivot).

The facet being added should currently have a fixed facet value (unless it's already part of the view), which will be removed from cubeGrid.fixedFacetValues.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facetId to add. Definition must have been provided at init time. |
| intoRows | [Boolean](#type-boolean) | true | true | whether to add facet as a row facet |
| index | [Integer](../reference_2.md#type-integer) | true | — | index to add the facet at. 0 = outermost (default innermost) |

### See Also

- [CubeGrid.removeFacet](#method-cubegridremovefacet)
- [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues)

---
## Method: CubeGrid.getFacetsHavingSelection

### Description
Return the list of facets that have any selection in their headers.  
_methodType_ getter

### Returns

`[Array of String](#type-array-of-string)` — list of facets that have any selection in their headers

### Groups

- selection

---
## Method: CubeGrid.selectAllFacetValues

### Description
Select/deselect all headers in a headerBar (specified by facetId) or all headerBars (if no facetId).  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | true | — | ID of facet - if null, selects all headerbars' headers |
| newState | [Boolean](#type-boolean) | true | — | new selection state - if null defaults to true |

### Groups

- selection

---
## Method: CubeGrid.facetMoved

### Description
Notification fired when a facet is moved.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | facetId which moved |

### Groups

- facetLayout

### See Also

- [CubeGrid.facetRemoved](#method-cubegridfacetremoved)
- [CubeGrid.facetAdded](#method-cubegridfacetadded)

---
## Method: CubeGrid.isFieldOpen

### Description
Return whether the specified CubeGrid field is open, taking into account both [collapsing](Facet.md#attr-facetcancollapse) and [minimizing](Facet.md#attr-facetcanminimize).

Note that if you don't already have a [FacetValueMap](../reference.md#object-facetvaluemap) to the field in question, you can get one by calling [CubeGrid.getRowHeaderFacetValues](#method-cubegridgetrowheaderfacetvalues) or [CubeGrid.getColumnHeaderFacetValues](#method-cubegridgetcolumnheaderfacetvalues),

You can also construct a [FacetValueMap](../reference.md#object-facetvaluemap) on your own by using the [Facet.id](Facet.md#attr-facetid)s from [CubeGrid.rowFacets](#attr-cubegridrowfacets) or [CubeGrid.columnFacets](#attr-cubegridcolumnfacets) together with the [FacetValue.id](FacetValue.md#attr-facetvalueid)s of the [Facet.values](Facet.md#attr-facetvalues) for the row or column that you want to query. Given a [Facet.id](Facet.md#attr-facetid), you can use [CubeGrid.getFacet](#method-cubegridgetfacet) to obtain the correponding [Facet](Facet.md#class-facet).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValueMap | [FacetValueMap](#type-facetvaluemap) | false | — | field specified as a facetValueMap |

### Returns

`[Boolean](#type-boolean)` — whether field is open

---
## Method: CubeGrid.facetValueContextClick

### Description
StringMethod handler fired when context click occurs over a facetValue button in a header.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | FacetValueMap describing the appropriate header button |

### Groups

- events

---
## Method: CubeGrid.getRowFacetLayout

### Description
Get the current widths of the row facets, as an object of the form:
```
 [ {facetId:facetId, width:currentWidth }, ... ]
 
```

### Returns

`[Array](#type-array)` — array of {facetId:facetId, width:width} objects

### Groups

- facetLayout

---
## Method: CubeGrid.setEditValues

### Description
Set the temporary edit values for some cell in the cubeGrid.  
Note that only the [this.valueProperty](#attr-cubegridvalueproperty) of the object passed in will be displayed in the cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cell | [Array of number](#type-array-of-number) | false | — | 2 element array of the form `[rowNum,colNum]` indicating the record being edited |
| values | [Object](../reference.md#type-object) | false | — | New values for the record |

---
## Method: CubeGrid.setFacetValueTitle

### Description
Set the title for a facet value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facet to update |
| facetValueId | [Identifier](../reference.md#type-identifier) | false | — | facetValue to update |
| newTitle | [String](#type-string) | false | — | title for the facet |

### Groups

- metadata

---
## Method: CubeGrid.getEditedCell

### Description
Returns the current value of a cell. If the cell has an outstanding edit value, this will be returned, otherwise the underlying value of the record will be returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [number](#type-number)|[Object](../reference.md#type-object) | false | — | rowNum of the record being edited, or an Object containing values for all the record's primary keys |
| colNum | [number](#type-number) | false | — | colNum of the cell. Only required if the first parameter is a rowNum |

### Returns

`[Any](#type-any)` — Current edit value, or underlying value for the cell.

### Groups

- editing

---
## Method: CubeGrid.getEventColumn

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
## Method: CubeGrid.getEditedRecord

### Description
Returns the combination of unsaved edits (if any) and original values (if any) for a given cell being edited.

The returned value is never null, and can be freely modified.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| valuesID | [number](#type-number)|[Object](../reference.md#type-object) | false | — | rowNum of the record being edited, or an Object containing values for all the record's primary keys |
| colNum | [number](#type-number) | true | — | colNum of the record being edited. Only required if the records rowNum is passed in as the first parameter |

### Returns

`[Object](../reference.md#type-object)` — A copy of the record with unsaved edits included

### Groups

- editing

---
## Method: CubeGrid.deselectAll

### Description
Deselect all cells and facetValues.  
_methodType_ action

### Groups

- selection

---
## Method: CubeGrid.deselectFacetValues

### Description
Deselect the header showing a given set of facet values.  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facetValues to deselect |

### Groups

- selection

---
## Method: CubeGrid.getSelectedFacetValues

### Description
Returns an array of facetValues objects indicating the headers that are selected in the headerBar for this facet. If facetId is not passed, returns selection for all facets.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | true | — | id for facet for which we are getting selected facetValues |

### Returns

`[Array of FacetValueMap](#type-array-of-facetvaluemap)` — selected facetValues

### Groups

- selection

---
## Method: CubeGrid.setEditValue

### Description
Set the edit value for some cell in the cube grid.

Note that cubeGrids display one record per cell - the value passed in should be the desired edit value for the [CubeGrid.valueProperty](#attr-cubegridvalueproperty) of the record.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | Row number |
| colNum | [number](#type-number) | false | — | Column number |
| value | [Any](#type-any) | false | — | New value for the record |

### Groups

- editing

**Flags**: A

---
## Method: CubeGrid.cellIsSelected

### Description
Determine whether the cell passed in is selected in this cubeGrid.  
_methodType_ tester

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cell | [CellRecord](#type-cellrecord) | false | — | cell to test |

### Returns

`[Boolean](#type-boolean)` — true if any cells are selected

### Groups

- selection

---
## Method: CubeGrid.facetLabelHover

### Description
StringMethod handler fired from hover over a facet label

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of the appropriate facet |

### Groups

- events

---
## Method: CubeGrid.getPrintHTML

### Description
Note that CubeGrid does not support a WYSIWYG print view by default(also used when [exporting to pdf](RPCManager.md#classmethod-rpcmanagerexportcontent)). Instead we recommend [exporting to excel or csv format](DataSource.md#method-datasourceexportclientdata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| printProperties | [PrintProperties](#type-printproperties) | true | — | properties to configure printing behavior - may be null. |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback. This is required to handle cases where HTML generation is asynchronous - if a method generates HTML asynchronously, it should return null, and fire the specified callback on completion of HTML generation. The first parameter `HTML` should contain the generated print HTML. The callback is only called if null is returned. Furthermore, the default getPrintHTML() implementation always returns null and fires the callback when a callback is provided. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — null if the print HTML is being generated asynchronously and/or a callback is provided; otherwise, the direct print HTML for this component (but note that returning direct print HTML is a deprecated feature).

### Groups

- printing

---
## Method: CubeGrid.selectCells

### Description
Select/deselect cells that match a [FacetValueMap](../reference.md#object-facetvaluemap). Also supports an explicit list of CellRecords or cell IDs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellList | [Array of CellRecord[]](#type-array-of-cellrecord)|[FacetValueMap](#type-facetvaluemap)|[Array of ID](#type-array-of-id) | false | — | cells to select |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |

### Groups

- selection

---
## Method: CubeGrid.getFacetValuesColumn

### Description
Get the index of the first column in the grid that matches the specified FacetValueMap.

The facetValues passed in should contain values for at least one column facet. It may contain properties other than column facets, which will be ignored. If values are sparse (values not specified for every column facet), the first column matching the specified facet values will be returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facet values to find |

### Returns

`[int](../reference.md#type-int)` — index of first column in the grid that matches the facet values passed in, or -1 if not found

---
## Method: CubeGrid.deselectFacetValue

### Description
Deselect the header for a given facet value.  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of facet |
| facetValueId | [String](#type-string) | false | — | ID of facetValue to select |

### Groups

- selection

---
## Method: CubeGrid.makeChart

### Description
Chart the portion of the dataset indicated by `fixedFacetValues`, for all values of the `variableFacets`. Note that the current [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues) of the CubeGrid will be implicitly added to whatever you pass as `fixedFacetValues`, since the idea is that this chart should be taken from data available in the CubeGrid.

One, two or more variableFacets may be passed. Two variable facets for a column chart will result in [stacking](Chart.md#attr-chartstacked) or clustering. Three facets or more may be supported by some [chartTypes](#attr-cubegridcharttype) or [charting engines](#attr-cubegridchartconstructor).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fixedFacetValues | [FacetValueMap](#type-facetvaluemap) | false | — | set of facet values to hold constant. Pass null to chart the entire dataset. |
| variableFacets | [Array of FacetId](#type-array-of-facetid) | false | — | set of facets to be charted |
| chartProperties | [Chart Properties](#type-chart-properties) | false | — | properties to pass through to the created [Chart](../reference_2.md#interface-chart) |

### Returns

`[Chart](#type-chart)` — created chart instance

---
## Method: CubeGrid.selectFacetValues

### Description
Select/deselect the header showing a given set of facet values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facetValues to select the header of |
| newState | [Boolean](#type-boolean) | true | — | new selection state - if null defaults to true |

### Groups

- selection

---
## Method: CubeGrid.facetValueOut

### Description
StringMethod handler fired when mouseout occurs for a facetValues header button

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | FacetValueMap for the appropriate header button |

### Groups

- events

---
## Method: CubeGrid.deselectCell

### Description
Deselect a single cell - accepts cell ID or cell record.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cell | [CellRecord](#type-cellrecord)|[ID](#type-id) | false | — | cell to deselect |

### Groups

- selection

---
## Method: CubeGrid.getCellStyle

### Description
Return the CSS class for a cell. By default this method has the following implementation:  
\- return any custom style for the record ([GridRenderer.recordCustomStyleProperty](GridRenderer.md#attr-gridrendererrecordcustomstyleproperty)) if defined.  
\- create a style name based on the result of [GridRenderer.getBaseStyle](GridRenderer.md#method-gridrenderergetbasestyle) and the state of the record using the rules described in [cellStyleSuffixes](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes).

Cell Styles are customizable by:

*   attaching a custom style to a record by setting `record[this.recordCustomStyleProperty]` to some valid CSS style name.
*   modifying the base style returned by getBaseStyle() \[see that method for further documentation on this\]
*   overriding this function

In addition to this, [getCellCSSText()](GridRenderer.md#method-gridrenderergetcellcsstext) may be overriden to provide custom cssText to apply on top of the styling attributes derived from the named style.

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
## Method: CubeGrid.facetValueOver

### Description
StringMethod handler fired when mouseover occurs over a facetValues header button

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | FacetValueMap for the appropriate header button |

### Groups

- events

---
## Method: CubeGrid.getCellFacetValues

### Description
Given a cell coordinate within this CubeGrid return a [FacetValueMap](../reference.md#object-facetvaluemap) indicating the facet values for the cell.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row index of the cell |
| colNum | [number](#type-number) | false | — | column index of the cell |

### Returns

`[FacetValueMap](#type-facetvaluemap)` — facet values for the specified cell. Returns null if the specified cell is not present in the grid.

---
## Method: CubeGrid.resizeFacetValue

### Description
Resizes all columns for the provided facetValueId, which must be a facetValueId from the innermost column facet.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValueId | [Identifier](../reference.md#type-identifier) | false | — | facetValueId of columns to be resized |
| newWidth | [number](#type-number) | false | — | column's new width |

---
## Method: CubeGrid.facetHasSelection

### Description
Return whether any facet value for this facet is selected in headers. If no facetId passed, return whether any facet has a selection.  
_methodType_ tester

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | Id for facet to test |

### Returns

`[Boolean](#type-boolean)` — true if any facet value in this header is selected

### Groups

- selection

---
## Method: CubeGrid.getColumnFacetValues

### Description
Return a [FacetValueMap](../reference.md#object-facetvaluemap) indicating the facet values for a specific column in the grid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [number](#type-number) | false | — | index of the column |

### Returns

`[FacetValueMap](#type-facetvaluemap)` — facet values for the specified column. Returns null if the specified column is not present in the grid.

---
## Method: CubeGrid.getCellRow

### Description
Given a record in this grid, this method returns the rowNum on which the record is displayed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellRecord | [CellRecord](#type-cellrecord) | false | — | record to find coordinates for |

### Returns

`[int](../reference.md#type-int)` — Row number for the record. Returns -1 if the record is not found.

---
## Method: CubeGrid.closeFacet

### Description
Handler fired when facet is closed  
_methodType_ handler

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of facet that was closed |

### Groups

- columnControls

---
## Method: CubeGrid.facetValueHoverHTML

### Description
Get the HTML for the facetValue button hover. Default implementation returns null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facetValues object for the button |

### Groups

- hoverTips

---
## Method: CubeGrid.getViewState

### Description
**Note**: This is a ListGrid feature which is inapplicable on this class.

### Returns

`[ListGridViewState](../reference_2.md#type-listgridviewstate)` — current view state for the grid.

### Groups

- viewState

### See Also

- [ListGridViewState](../reference_2.md#type-listgridviewstate)
- [ListGrid.setViewState](ListGrid_2.md#method-listgridsetviewstate)

---
## Method: CubeGrid.autoSizeFacet

### Description
auto-size the header facet horizontally

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of facet to resize. |

---
## Method: CubeGrid.getFacet

### Description
Get a facet definition by facetId. Constant time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | the id of the facet to retrieve |

### Returns

`[Facet](#type-facet)` — the Facet if found, or null

### See Also

- [Facet](Facet.md#class-facet)

---
## Method: CubeGrid.closeColumn

### Description
Handler fired when column is closed  
_methodType_ handler

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| headerFacetValues | [FacetValue Object](#type-facetvalue-object) | false | — | FacetValues for the appropriate col. |

### Groups

- columnControls

---
## Method: CubeGrid.getCellColumn

### Description
Given a record in this grid, this method returns the colNum in which the record is displayed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellRecord | [CellRecord](#type-cellrecord) | false | — | record to find coordinates for |

### Returns

`[int](../reference.md#type-int)` — Column number for the record. Returns -1 if the record is not found.

---
## Method: CubeGrid.hasChanges

### Description
Determines whether any cells in this cubeGrid have been edited but not yet saved to the underlying data set. Note that for asynchronous saves, this method will return false if the current edit values match any submitted (but not yet saved) values. This behavior can be turned off with the `ignorePendingValues` parameter.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ignorePendingValues | [Boolean](#type-boolean) | true | — | If true, this method will compare the current edit values against the underlying records in the dataset, not taking pending edit values into account |

### Returns

`[Boolean](#type-boolean)` — true if any record in the grid has been edited but not yet saved

### Groups

- editing

---
## Method: CubeGrid.setHilites

### Description
Only supported on ListGrid for now.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hilites | [Array of Hilite](#type-array-of-hilite) | false | — | Array of hilite objects |

### Groups

- hiliting

---
## Method: CubeGrid.setViewState

### Description
**Note**: This is a ListGrid feature which is inapplicable on this class.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewState | [ListGridViewState](../reference_2.md#type-listgridviewstate) | false | — | Object describing the desired view state for the grid |

### Groups

- viewState

### See Also

- [ListGrid.getViewState](ListGrid_2.md#method-listgridgetviewstate)

---
## Method: CubeGrid.facetLabelOut

### Description
StringMethod handler fired when mouseout occurs over a facet label

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of the appropriate facet |

### Groups

- events

---
## Method: CubeGrid.saveEdits

### Description
Validates and saves edits for some cell. If rowNum and colNum are not passed in, the current edit cell will be saved.

The 'callback' parameter provides a notification when the save attempt completes. Cases under which the callback will fire are:

*   Save completed successfully
*   No changes to the edited cell, so save not required
*   Validation failure occurred on the client or on the server

Note that if no rowNum/colNum were passed in and the editor is not showing for the cell, the callback will NOT fire - in this case, the method is a no-op.

Other, standard callbacks such as [editComplete()](ListGrid_2.md#method-listgrideditcomplete), [editFailed()](ListGrid_1.md#method-listgrideditfailed) and [cellChanged()](ListGrid_2.md#method-listgridcellchanged) will fire normally.

Note this method does not hide the inline editors if they are showing - to explicitly save and end editing, use the method 'endEditing()'

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editCompletionEvent | [EditCompletionEvent](../reference.md#type-editcompletionevent) | true | — | Event used to complete cell editing. Optional, and defaults to `"programmatic"`. Can be used by the `callback` method to perform custom actions such as navigation when the save completes. |
| callback | [Callback](../reference.md#type-callback) | true | — | Callback to fire on completion of the saving process. If no edits were made or client-side validation fails the callback will be fired synchronously at the end of this method.  
Takes the following parameters:  
\- rowNum _(Number) edited row number_  
\- colNum _(Number) edited column number_  
\- editCompletionEvent _(EditCompletionEvent) event passed in (defaults to `"programmatic"`)_  
\- success _(boolean) false if the save was unable to complete due to a validation failure or server-side error._ |
| rowNum | [number](#type-number) | true | — | Which row should be saved. If unspecified the current edit row is saved by default. Note that if there is no current edit cell this method will no op. |
| colNum | [number](#type-number) | true | — | Which row should be saved. If unspecified the current edit column is saved by default. Note that if there is no current edit cell this method will no op. |

### Groups

- editing

### See Also

- [ListGrid.endEditing](ListGrid_2.md#method-listgridendediting)

**Flags**: A

---
## Method: CubeGrid.setFacetTitleAlign

### Description
Set the align of a facet title (appears in facet label).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facet to update |
| align | [Alignment](../reference.md#type-alignment) | false | — | new alignment for facet title |

### Groups

- gridLayout

---
## Method: CubeGrid.dataArrived

### Description
Notification method fired when new data arrives from the server to be displayed in this CubeGrid. For example in response to the user openng a collapsed facet, or as a result of an initial fetch request for all data from a CubeGrid where [CubeGrid.facets](#attr-cubegridfacets) is not set and there is no initial data. Only applies to databound CubeGrids.

**Flags**: A

---
## Method: CubeGrid.getColumnHeaderFacetValues

### Description
Return a [FacetValueMap](../reference.md#object-facetvaluemap) of the facet values for the column field at the specified level containing the requested column number. Note that outer column fields may span several grid columns.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [int](../reference.md#type-int) | false | — | 0-based index into the grid columns (and inner column header fields) |
| level | [int](../reference.md#type-int) | false | — | target header level; 0 represents the outer column header |

### Returns

`[FacetValueMap](#type-facetvaluemap)` — facet values for the targeted column header field

---
## Method: CubeGrid.toggleFieldOpenState

### Description
Toggles the open state of the specified field. No-ops if it's not showing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValueMap | [FacetValueMap](#type-facetvaluemap) | false | — | field specified as a facetValueMap |

### Returns

`[Boolean](#type-boolean)` — whether specified field's open state was toggled

---
## Method: CubeGrid.getDefaultFacetValueContextItems

### Description
Returns a default set of items, which can be updated/modified, and then assigned to [CubeGrid.facetValueContextItems](#attr-cubegridfacetvaluecontextitems) to be used in the context menu of the appropriate header button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | FacetValueMap for the appropriate header button |

### Returns

`[Array of MenuItem](#type-array-of-menuitem)` — Return standard context menu items for these facet values.

---
## Method: CubeGrid.getColumnFacetLayout

### Description
Get the current heights of the column facets, as an object of the form:
```
 [ {facetId:facetId, height:currentHeight}, ... ]
 
```

### Returns

`[Array](#type-array)` — array of {facetId:facetId, height:height} objects

### Groups

- facetLayout

---
## Method: CubeGrid.selectAllCells

### Description
Select all cells.

### Groups

- selection

---
## Method: CubeGrid.hiliteCellList

### Description
Apply a hilite to an array of cells.  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellObjList | [Array of Cell Object](#type-array-of-cell-object) | false | — | cells to hilite |
| hiliteID | [String](#type-string) | false | — | ID of hilite to apply to cells |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the cells were successfully hilited.

### Groups

- hiliting

---
## Method: CubeGrid.setFacetValueTitleAlign

### Description
Set the align for the title for a facet value.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facet to update |
| facetValueId | [Identifier](../reference.md#type-identifier) | false | — | facetValue to update |
| align | [Alignment](../reference.md#type-alignment) | false | — | new alignment for facet value title |

### Groups

- gridLayout

---
## Method: CubeGrid.facetRemoved

### Description
Notification fired when a facet is removed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | facetId that was removed |

### Groups

- facetLayout

### See Also

- [CubeGrid.facetAdded](#method-cubegridfacetadded)

---
## Method: CubeGrid.anyCellSelected

### Description
Determine whether any cells are selected in this cubeGrid.  
_methodType_ tester

### Returns

`[Boolean](#type-boolean)` — true if any cells are selected

### Groups

- selection

---
## Method: CubeGrid.getCellRecord

### Description
Return the pointer to a particular record by record and column number.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | row index of record to return. |
| colNum | [number](#type-number) | false | — | column index of record to return. |

### Returns

`[ListGridRecord](#type-listgridrecord)` — Record object for the row.

### See Also

- [ListGrid.getRecord](ListGrid_2.md#method-listgridgetrecord)
- [ListGrid.getEditedRecord](ListGrid_1.md#method-listgridgeteditedrecord)

**Flags**: A

---
## Method: CubeGrid.discardAllEdits

### Description
—

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Array of int](#type-array-of-array-of-int) | true | — | allows you to specify which cell(s) to drop edits for. Each record should be identified as an array containing `[rowNum,colNum]` |
| dontHideEditor | [boolean](../reference.md#type-boolean) | true | — | By default this method will hide the editor if it is currently showing for any row in the grid. Passing in this parameter will leave the editor visible (and just reset the edit values underneath the editor). |

### Groups

- editing

**Flags**: A

---
## Method: CubeGrid.deselectAllCells

### Description
Deselect all cells.

### Groups

- selection

---
## Method: CubeGrid.showFacetValues

### Description
Shows the specified field if it was previsouly hidden. No-ops if it's already showing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValueMap | [FacetValueMap](#type-facetvaluemap) | false | — | field specified as a facetValueMap |

### Returns

`[boolean](../reference.md#type-boolean)` — whether specified field was actually shown

---
## Method: CubeGrid.getEditValue

### Description
Returns the current temporary locally stored edit value for a cell being edited. Note this is the [valueProperty](#attr-cubegridvalueproperty) that will be saved for the cell in question.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rowNum | [number](#type-number) | false | — | index of the row for which the editValue should be returned |
| colNum | [number](#type-number) | false | — | index of the column for which value should be returned |

### Returns

`[Any](#type-any)` — edit value for the cell

### Groups

- editing

---
## Method: CubeGrid.deselectAllFacetValues

### Description
Deselect all headers in a headerBar (specified by facetId) or all headerBars (if no facetId).  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | true | — | ID of facet - if null, selects all headerbars' headers |

### Groups

- selection

---
## Method: CubeGrid.addRowFacet

### Description
Add a row facet to the view at index "index". Handles the facet already being in the view (does a pivot).  
  
The facet being added should currently have a fixed facet value (unless it's already part of the view), which will be removed from cubeGrid.fixedFacetValues.  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facetId to add. Definition must have been provided at init time. |
| index | [Integer](../reference_2.md#type-integer) | true | — | index to add the facet at. 0 = outermost (default innermost) |

### Groups

- facetLayout

### See Also

- [CubeGrid.removeFacet](#method-cubegridremovefacet)
- [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues)

---
## Method: CubeGrid.facetLabelHoverHTML

### Description
Get the HTML for the facet label hover. Default implementation returns null.  
_methodType_ callback

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID for the facet |

### Groups

- hoverTips

---
## Method: CubeGrid.facetValueSelectionChanged

### Description
Handler/Notification function for facetValue selection change (no default implementation).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValues | [FacetValueMap](#type-facetvaluemap) | false | — | facetValues with new selection state |
| newState | [boolean](../reference.md#type-boolean) | false | — | new selection state |

### Groups

- selection

---
## Method: CubeGrid.getAllEditCells

### Description
Method to determine which records currently have pending (unsubmitted) edits. Returns an array of 2 element arrays indicating the `[rowNum,colNum]` of the cells in question.

### Returns

`[Array](#type-array)` — Array of `[rowNum,colNum]` arrays for cells with edit values pending submission.

### Groups

- editing

---
## Method: CubeGrid.setFixedFacetValue

### Description
Modify fixedFacetValues for this cubeGrid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facetId |
| fixedFacetValueId | [Identifier](../reference.md#type-identifier) | false | — | New fixed value for the facet, to be added to [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues). Default is the rollup value for the facet. |

### Groups

- facetLayout

---
## Method: CubeGrid.getFacetValue

### Description
Get a facet value definition by facetId and facetValueId. Constant time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | the id of the facet to retrieve |
| facetValueId | [String](#type-string) | false | — | the id of the facet value to retrieve |

### Returns

`[FacetValue](#type-facetvalue)` — the FacetValue if found, or null

### See Also

- [FacetValue](../reference.md#object-facetvalue)

---
## Method: CubeGrid.hiliteCell

### Description
Apply a hilite to a specific cell. Note: can be called either as hiliteCell(cellObject, hiliteID) or hiliteCell(row, column, hiliteID)  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellObj | [Cell Object](#type-cell-object)|[Row number](#type-row-number) | false | — | cell to hilite / row of cell to hilite |
| hiliteID | [String](#type-string)|[Column number](#type-column-number) | false | — | hilite ID / column of cell to hilite |
| alternateHiliteID | [String](#type-string) | true | — | optional third parameter - hilite ID. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the cell was successfully hilited.

### Groups

- hiliting

---
## Method: CubeGrid.selectCell

### Description
Select / deselect a single cell - accepts cell ID or [CellRecord](../reference.md#object-cellrecord).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cell | [CellRecord](#type-cellrecord)|[ID](#type-id) | false | — | cell to select / deselect |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |

### Groups

- selection

---
## Method: CubeGrid.addColumnFacet

### Description
Add a column facet to the view at index "index". Handles the facet already being in the view (does a pivot).  
  
The facet being added should currently have a fixed facet value (unless it's already part of the view), which will be removed from cubeGrid.fixedFacetValues.  
_methodType_ action

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [Identifier](../reference.md#type-identifier) | false | — | facetId to add. Definition must have been provided at init time. |
| index | [Integer](../reference_2.md#type-integer) | true | — | index to add the facet at. 0 = outermost (default innermost) |

### Groups

- facetLayout

### See Also

- [CubeGrid.removeFacet](#method-cubegridremovefacet)
- [CubeGrid.fixedFacetValues](#attr-cubegridfixedfacetvalues)

---
## Method: CubeGrid.hideFacetValues

### Description
Hides the specified field if it is currently visible. No-ops if it's already hidden.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetValueMap | [FacetValueMap](#type-facetvaluemap) | false | — | field specified as a facetValueMap |

### Returns

`[boolean](../reference.md#type-boolean)` — whether specified field was actually hidden

---
## Method: CubeGrid.facetAdded

### Description
Notification fired when a new facet is added.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | facetId that was added |

### Groups

- facetLayout

### See Also

- [CubeGrid.facetRemoved](#method-cubegridfacetremoved)

---
## Method: CubeGrid.setEnableCharting

### Description
Setter for the [CubeGrid.enableCharting](#attr-cubegridenablecharting) attribute.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| enableCharting | [boolean](../reference.md#type-boolean) | false | — | — |

---
## Method: CubeGrid.saveAllEdits

### Description
Save a number of outstanding edits for this CubeGrid. If no cells are specified, all outstanding edits will be saved

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cells | [Array of Array of int](#type-array-of-array-of-int) | true | — | optionally specify which cells to save. Each cell should be specified as a 2 element array in the format `[rowNum,colNum]`. |
| saveCallback | [Callback](../reference.md#type-callback) | true | — | If specified this callback will be fired on a successful save of the specified rows. Note that if there are no pending edits to be saved this callback will not fire - you can check for this condition using [CubeGrid.hasChanges](#method-cubegridhaschanges) or [CubeGrid.recordHasChanges](#method-cubegridrecordhaschanges). |

### Returns

`[boolean](../reference.md#type-boolean)` — true if a save has been initiated (at least one row had changes, passed client-side validation, and a save has been attempted). False otherwise

### Groups

- editing

---
## Method: CubeGrid.clearEditValue

### Description
Clear a field value being tracked as an unsaved user edit for some cell.

The saved record value will be displayed in the the appropriate cell instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editValuesID | [number](#type-number)|[Object](../reference.md#type-object) | false | — | Row number, primary keys object for the record, or editValues object |
| colNum | [number](#type-number) | true | — | Column number for the cell in question. Only required if the first parameter is a row number. |

### Groups

- editing

**Flags**: A

---
## Method: CubeGrid.facetContextClick

### Description
StringMethod handler fired when the user right clicks on a facet label.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of facet |

### Groups

- events

---
## Method: CubeGrid.cellSelectionChanged

### Description
Handler/Notification function for cell selection change May update header button styles.  
_methodType_ handler

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cellList | [Array of CellRecord](#type-array-of-cellrecord) | false | — | array of cells with new selection state |

### Returns

`[boolean](../reference.md#type-boolean)` — —

### Groups

- selection

---
## Method: CubeGrid.sortByFacetId

### Description
Called when a sort control is clicked on a FacetHeader. Does nothing by default.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of facet to sort |
| sortDirection | [boolean](../reference.md#type-boolean) | false | — | true for ascending |

### Groups

- columnControls

---
## Method: CubeGrid.loadAllRecords

### Description
This method is not currently supported for this grid-type. See [ListGrid.loadAllRecords](ListGrid_2.md#method-listgridloadallrecords) for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| maxRecords | [Integer](../reference_2.md#type-integer) | true | — | optional maximum record count - if passed, no fetch takes place if maxRecords is below the known length of the data |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to fire if a fetch is issued - if all data was already loaded, the callback is fired with no parameters |

### Returns

`[Boolean](#type-boolean)` — true if a fetch was made or was not needed - false otherwise

---
## Method: CubeGrid.getSelectedCellIds

### Description
Returns an array of the IDs of all selected cell records.  
_methodType_ getter

### Returns

`[Array of String](#type-array-of-string)` — array of the selected cell IDs

### Groups

- selection

---
## Method: CubeGrid.facetLabelOver

### Description
StringMethod handler fired when mouseover occurs over a facet label

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| facetId | [String](#type-string) | false | — | ID of the appropriate facet |

### Groups

- events

---
