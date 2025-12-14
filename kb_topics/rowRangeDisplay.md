# Grid row-range and row-count display

[← Back to API Index](../reference.md)

---

## KB Topic: Grid row-range and row-count display

### Description
ListGrids are able to create a [specialized label](../classes/ListGrid_2.md#method-listgridgetrowrangedisplay) that will display the currently visible range of rows in the viewport along with a total row count for the current data set.

When [progressive loading is active](../classes/DataSource.md#attr-datasourceprogressiveloading), the [reported row count](../classes/ResultSet.md#method-resultsetgetrowcount) for list grid's data may not accurately reflect the true number of rows in the data set.

See [RowCountStatus](../reference.md#type-rowcountstatus) for more details. Note that for custom dataSources where progressive loading is active, the [DSResponse.estimatedTotalRows](../classes/DSResponse.md#attr-dsresponseestimatedtotalrows) may be used to explictly provide either an estimated or exact row count for the data set (distinct from the reported [DSResponse.totalRows](../classes/DSResponse.md#attr-dsresponsetotalrows).

When the true size of the data set is not known, the `rowRangeDisplay` will format the reported length in a way that indicates it is not an exact count (see [ListGrid.getFormattedRowCount](../classes/ListGrid_2.md#method-listgridgetformattedrowcount)). If [ListGrid.autoFetchRowCount](../classes/ListGrid_1.md#attr-listgridautofetchrowcount) is set to `true`, a separate row count fetch will be intiated as soon as data arrives, so an accurate row count will be displayed as soon as that fetch completes. Alternatively, if [ListGrid.canRequestRowCount](../classes/ListGrid_1.md#attr-listgridcanrequestrowcount) is set to `true`, the user may click the label to issue a row count fetch request and get back an accurate row count to display to the user.

As an alternative to using the `rowRangeDisplay` autoChild, developers may also make use of various list grid APIs such as [ListGrid.getRowCountStatus](../classes/ListGrid_1.md#method-listgridgetrowcountstatus), [ListGrid.getRowCount](../classes/ListGrid_2.md#method-listgridgetrowcount), [ListGrid.getRowRangeDisplayValue](../classes/ListGrid_2.md#method-listgridgetrowrangedisplayvalue) and [ListGrid.fetchRowCount](../classes/ListGrid_2.md#method-listgridfetchrowcount) to directly display or retrieve row counts.

### Related

- [RowCountStatus](../reference.md#type-rowcountstatus)
- [RowRangeDisplayStyle](../reference_2.md#type-rowrangedisplaystyle)
- [ResultSet.getRowCountStatus](../classes/ResultSet.md#method-resultsetgetrowcountstatus)
- [ResultSet.getRowCount](../classes/ResultSet.md#method-resultsetgetrowcount)
- [ResultSet.getRowCountRange](../classes/ResultSet.md#method-resultsetgetrowcountrange)
- [Callbacks.RowCountCallback](../classes/Callbacks.md#method-callbacksrowcountcallback)
- [ResultSet.fetchRowCount](../classes/ResultSet.md#method-resultsetfetchrowcount)
- [ListGrid.getRowRangeDisplay](../classes/ListGrid_2.md#method-listgridgetrowrangedisplay)
- [ListGrid.getRowRangeDisplayValue](../classes/ListGrid_2.md#method-listgridgetrowrangedisplayvalue)
- [ListGrid.getFormattedRowCount](../classes/ListGrid_2.md#method-listgridgetformattedrowcount)
- [ListGrid.getRowCount](../classes/ListGrid_2.md#method-listgridgetrowcount)
- [ListGrid.getRowCountRange](../classes/ListGrid_2.md#method-listgridgetrowcountrange)
- [ListGrid.getRowCountStatus](../classes/ListGrid_1.md#method-listgridgetrowcountstatus)
- [ListGrid.fetchRowCount](../classes/ListGrid_2.md#method-listgridfetchrowcount)
- [RowRangeDisplay.setSourceGrid](../classes/RowRangeDisplay.md#method-rowrangedisplaysetsourcegrid)
- [RowRangeDisplay](../classes/RowRangeDisplay.md#class-rowrangedisplay)
- [ResultSet.applyRowCountToLength](../classes/ResultSet.md#attr-resultsetapplyrowcounttolength)
- [ResultSet.rowCountOperation](../classes/ResultSet.md#attr-resultsetrowcountoperation)
- [ResultSet.rowCountContext](../classes/ResultSet.md#attr-resultsetrowcountcontext)
- [ResultSet.blockingRowCountFetch](../classes/ResultSet.md#attr-resultsetblockingrowcountfetch)
- [ListGrid.rowRangeDisplay](../classes/ListGrid_1.md#attr-listgridrowrangedisplay)
- [ListGrid.canRequestRowCount](../classes/ListGrid_1.md#attr-listgridcanrequestrowcount)
- [ListGrid.applyRowCountToLength](../classes/ListGrid_1.md#attr-listgridapplyrowcounttolength)
- [ListGrid.blockingRowCountFetch](../classes/ListGrid_1.md#attr-listgridblockingrowcountfetch)
- [ListGrid.rowRangeDisplayStyle](../classes/ListGrid_1.md#attr-listgridrowrangedisplaystyle)
- [ListGrid.loadingRowCountDisplayIcon](../classes/ListGrid_1.md#attr-listgridloadingrowcountdisplayicon)
- [ListGrid.loadingRowCountDisplayIconWidth](../classes/ListGrid_1.md#attr-listgridloadingrowcountdisplayiconwidth)
- [ListGrid.loadingRowCountDisplayIcoHeight](../classes/ListGrid_1.md#attr-listgridloadingrowcountdisplayicoheight)
- [ListGrid.exactRowCountFormat](../classes/ListGrid_1.md#attr-listgridexactrowcountformat)
- [ListGrid.minimumRowCountFormat](../classes/ListGrid_1.md#attr-listgridminimumrowcountformat)
- [ListGrid.approximateRowCountFormat](../classes/ListGrid_1.md#attr-listgridapproximaterowcountformat)
- [ListGrid.maximumRowCountFormat](../classes/ListGrid_1.md#attr-listgridmaximumrowcountformat)
- [ListGrid.rangeRowCountFormat](../classes/ListGrid_1.md#attr-listgridrangerowcountformat)
- [ListGrid.rowCountDisplayPrecision](../classes/ListGrid_1.md#attr-listgridrowcountdisplayprecision)
- [RowRangeDisplay.wrap](../classes/RowRangeDisplay.md#attr-rowrangedisplaywrap)
- [RowRangeDisplay.align](../classes/RowRangeDisplay.md#attr-rowrangedisplayalign)
- [RowRangeDisplay.vlign](../classes/RowRangeDisplay.md#attr-rowrangedisplayvlign)
- [RowRangeDisplay.sourceGrid](../classes/RowRangeDisplay.md#attr-rowrangedisplaysourcegrid)
- [RowRangeDisplay.canRequestRowCount](../classes/RowRangeDisplay.md#attr-rowrangedisplaycanrequestrowcount)
- [RowRangeDisplay.interactiveStyleName](../classes/RowRangeDisplay.md#attr-rowrangedisplayinteractivestylename)

---
