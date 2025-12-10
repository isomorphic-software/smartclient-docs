# TileGrid Documentation

[← Back to API Index](../reference.md)

---

## Class: TileGrid

*Inherits from:* [TileLayout](TileLayout.md#class-tilelayout)

### Description
A TileGrid is a [DataBoundComponent](../reference.md#interface-databoundcomponent) that displays a list of objects as a set of "tiles", where each tile represents one object, and the tiles are laid out in a grid with multiple tiles per row. Each tile displays one or more properties of the object it represents.

---
## Attr: TileGrid.wrapValues

### Description
Whether values should be allowed to wrap by default, or should be shown on one line regardless of length.

**Flags**: IR

---
## Attr: TileGrid.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria) and related methods.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

**Flags**: IRW

---
## Attr: TileGrid.fields

### Description
Array of field definitions to control the default rendering of tiles.

If not specified, if the DataSource has an [iconField](DataSource.md#attr-datasourceiconfield), only the `iconField` and [titleField](DataSource.md#attr-datasourcetitlefield) will be shown. Otherwise, all non-[hidden](DataSourceField.md#attr-datasourcefieldhidden) non-[detail](DataSourceField.md#attr-datasourcefielddetail) fields will be shown, similar to the default set of fields shown by a [ListGrid](ListGrid_1.md#class-listgrid).

Only applicable if using the default [SimpleTile](SimpleTile.md#class-simpletile) class for tiles. (See [TileGrid.tile](#attr-tilegridtile) for more information).

For SimpleTiles, it is possible to use [DetailViewerField.getCellStyle](DetailViewerField.md#method-detailviewerfieldgetcellstyle) and [StatefulCanvas.getStateSuffix](StatefulCanvas.md#method-statefulcanvasgetstatesuffix) to make a single field statefully styled:

```
 
 isc.TileGrid.create({
      fields:[
          {name:'animalName',
           getCellStyle : function (value, field, record, viewer) {
               if (value == "Tiger") return "tigerStyle" + viewer.currentTile.getStateSuffix();
               else return viewer.tileGrid.tileValueStyle + viewer.currentTile.getStateSuffix();
           }
          }
      ]
 });
 
 
 
```

**Flags**: IR

---
## Attr: TileGrid.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: TileGrid.valuesShowRollOver

### Description
Should tile values change state when the mouse goes over them?

**Flags**: IR

---
## Attr: TileGrid.reselectOnUpdate

### Description
If true, when an update operation occurs on a selected tile's record in a [databound](#attr-tilegriddatasource) tileGrid, ensure the updated tile is re-selected when the operation completes. The [TileGrid.reselectOnUpdateNotifications](#attr-tilegridreselectonupdatenotifications) attributes governs whether [selectionUpdated()](DataBoundComponent.md#method-databoundcomponentselectionupdated) and [CubeGrid.selectionChanged()](ListGrid_2.md#method-listgridselectionchanged) will fire when this occurs.

**Flags**: IRA

---
## Attr: TileGrid.detailViewer

### Description
Automatically genereated DetailViewer instance used to render the content shown in Tiles by default.

This detailViewer is never actually drawn or displayed to the user - it is simply used to generate the contents of SimpleTiles as described in [TileGrid.getTileHTML](#method-tilegridgettilehtml).

**Flags**: IR

---
## Attr: TileGrid.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference_2.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: TileGrid.dragDataAction

### Description
Indicates what to do with data dragged into another DataBoundComponent. See DragDataAction type for details.

### Groups

- dragging

**Flags**: IRW

---
## Attr: TileGrid.animateTileChange

### Description
If set, when the dataset changes due to filtering, sorting or other actions, any tiles that were showing before and after the change will animate from their old positions to their new positions.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: TileGrid.tiles

### Description
List of tiles that may be used by the TileGrid to show its current data set. Note that the SmartClient framework manages this array for optimal performance, and not all tiles in the array are necessarily visible or assigned a record. This is true regardless of whether [TileGrid.recycleTiles](#attr-tilegridrecycletiles) is set or not.

The number of records in the `TileGrid`'s current [data set](#attr-tilegriddata) may be determined by calling [getLength()](List.md#method-listgetlength) on it.

### See Also

- [TileGrid.recycleTiles](#attr-tilegridrecycletiles)
- [TileGrid.tileConstructor](#attr-tilegridtileconstructor)

**Flags**: IR

---
## Attr: TileGrid.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [TileGrid.initialCriteria](#attr-tilegridinitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle). Additional request properties may be specified using [TileGrid.fetchRequestProperties](#attr-tilegridfetchrequestproperties).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_2.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [TileGrid.initialCriteria](#attr-tilegridinitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_2.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- databinding

### See Also

- [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata)

**Flags**: IR

---
## Attr: TileGrid.tile

### Description
A TileGrid automatically creates one tile per record in the dataset, via the [AutoChild](../reference.md#type-autochild) pattern.

By default, the [SimpleTile](SimpleTile.md#class-simpletile) class will be used. This class automatically invokes [TileGrid.getTileHTML](#method-tilegridgettilehtml) on the tileGrid to generate its content. The standard [TileGrid.getTileHTML](#method-tilegridgettilehtml) method uses a [detailViewer](#attr-tilegriddetailviewer) to render html for the tile's record, based on the provided [TileGrid.fields](#attr-tilegridfields) (or on the default set of fields).

To create a completely different appearance, override [TileGrid.tileConstructor](#attr-tilegridtileconstructor) with the name of the custom SmartClient class to use for each tile. For example, subclass [SimpleTile](SimpleTile.md#class-simpletile) and override [getInnerHTML()](Canvas.md#method-canvasgetinnerhtml), returning custom HTML for each tile.

```
     isc.defineClass("MyCustomTile", "SimpleTile").addProperties({
        getInnerHTML : function () {
           return this.Super("getInnerHTML", arguments) +
                this.getRecord().width + " x " + this.getRecord().height;
        }
     });

     isc.TileGrid.create({
        tileConstructor:"MyCustomTile"
     });
 
```

Note that you can also override tile behaviors on a per-record basis, via [TileRecord.tileConstructor](../reference.md#attr-tilerecordtileconstructor) and [TileRecord.tileProperties](../reference.md#attr-tilerecordtileproperties).

**Flags**: IR

---
## Attr: TileGrid.dragTrackerStyle

### Description
CSS Style to apply to the drag tracker when dragging occurs on this component.

**Flags**: IRW

---
## Attr: TileGrid.styleName

### Description
Style for the overall TileGrid component.

### Groups

- appearance

**Flags**: IR

---
## Attr: TileGrid.drawAllMaxTiles

### Description
If drawing all tiles would cause no more than `drawAllMaxTiles` tiles to be rendered, the full dataset will instead be drawn even if [TileGrid.showAllRecords](#attr-tilegridshowallrecords) is false and incremental rendering would have otherwise been used.

The `drawAllMaxTiles` setting prevents incremental rendering from being used in situations where it's really unnecessary, such as a 25 record dataset which happens to be in a grid with a viewport showing only 15 or so tiles. Incremental rendering causes a brief "flash" during scrolling as the visible portion of the dataset is redrawn, and a better scrolling experience can be obtained in this situation by drawing the entire dataset up front, which in this example would have negligible effect on initial draw time.

`drawAllMaxTiles:0` disables this features. You may want to disable this feature if performance is an issue and:

*   you very frequently redraw a grid
*   you do a lot of computation when rendering each tile
*   you are showing many grids on one screen and the user won't scroll most of them

### Groups

- performance

### See Also

- [TileGrid.tileConstructor](#attr-tilegridtileconstructor)

**Flags**: IRWA

---
## Attr: TileGrid.tileDragAppearance

### Description
Visual appearance to show when the tile is being dragged.

### Groups

- dragdrop

### See Also

- [Canvas.dragAppearance](Canvas.md#attr-canvasdragappearance)

**Flags**: IRWA

---
## Attr: TileGrid.detailViewerProperties

### Description
Properties for the [DetailViewer](DetailViewer.md#class-detailviewer) that is automatically created to render the contents of tiles by default.

**Flags**: IR

---
## Attr: TileGrid.canAcceptDroppedRecords

### Description
Indicates whether records can be dropped into this TileGrid.

### Groups

- dragging

**Flags**: IRW

---
## Attr: TileGrid.tileValueStyle

### Description
When using the default [SimpleTile](SimpleTile.md#class-simpletile), CSS style for each value shown within a tile.

**Flags**: IR

---
## Attr: TileGrid.fetchRequestProperties

### Description
If [TileGrid.autoFetchData](#attr-tilegridautofetchdata) is `true`, this attribute allows the developer to declaratively specify [DSRequest](../reference_2.md#object-dsrequest) properties for the initial [fetchData()](ListGrid_2.md#method-listgridfetchdata) call.

Note that any properties governing more specific request attributes for the initial fetch (such as [TileGrid.autoFetchTextMatchStyle](#attr-tilegridautofetchtextmatchstyle) and initial sort specifiers) will be applied on top of this properties block.

### Groups

- databinding

**Flags**: IR

---
## Attr: TileGrid.loadingDataMessageStyle

### Description
The CSS style name applied to the loadingDataMessage string if displayed.

### Groups

- emptyMessage

**Flags**: IRW

---
## Attr: TileGrid.data

### Description
A List of TileRecord objects, specifying the data to be used to create the tiles.

This property will typically not be explicitly specified for databound TileGrids, where the data is returned from the server via databound component methods such as [TileGrid.fetchData](#method-tilegridfetchdata). In this case the data objects will be set to a [resultSet](ResultSet.md#class-resultset) rather than a simple array.

### Groups

- data

### See Also

- [TileRecord](../reference.md#object-tilerecord)

**Flags**: IRW

---
## Attr: TileGrid.reselectOnUpdateNotifications

### Description
if [TileGrid.reselectOnUpdate](#attr-tilegridreselectonupdate) is true, this property governs what selection changed notifications should be triggered when a selected tile's record is edited then automatically reselected when the edited data is merged into the data set.

**Flags**: IRWA

---
## Attr: TileGrid.emptyMessageStyle

### Description
The CSS style name applied to the [TileGrid.emptyMessage](#attr-tilegridemptymessage) if displayed.

### Groups

- emptyMessage

**Flags**: IRW

---
## Attr: TileGrid.dataFetchMode

### Description
How to fetch and manage records retrieve from the server. See [FetchMode](../reference_2.md#type-fetchmode).

This setting only applies to the [ResultSet](ResultSet.md#class-resultset) automatically created by calling [fetchData()](ListGrid_2.md#method-listgridfetchdata). If a pre-existing ResultSet is passed to setData() instead, it's existing setting for [ResultSet.fetchMode](ResultSet.md#attr-resultsetfetchmode) applies.

### Groups

- databinding

### See Also

- [TileGrid.showAllRecords](#attr-tilegridshowallrecords)

**Flags**: IRW

---
## Attr: TileGrid.tileValueAlign

### Description
Horizontal alignment for tile values: "left", "right" or "center".

**Flags**: IR

---
## Attr: TileGrid.tileProperties

### Description
Common properties to use when creating every tile.

**Flags**: IRW

---
## Attr: TileGrid.printTilesPerLine

### Description
How many tiles should be present in a line when printing?

**Flags**: IR

---
## Attr: TileGrid.tileConstructor

### Description
Class-name of a SmartClient component to use for each tile rendered by this TileGrid. Tiles are created by the [AutoChild](../reference.md#type-autochild) pattern; see [TileGrid.tile](#attr-tilegridtile).

Any subclass of Canvas is allowed, but typically any custom class will derive from [SimpleTile](SimpleTile.md#class-simpletile).

When using a custom component for tileConstructor, DataBoundComponents that display multiple Records (ListGrid, DetailViewer) will have data provided via [ListGrid.setData](ListGrid_2.md#method-listgridsetdata), and components that display a single Record (DynamicForm) will have [DynamicForm.setValues](DynamicForm.md#method-dynamicformsetvalues) called on them.

If the component is not a recognized DataBoundComponent subclass, the Record can be accessed via `this.record`.

If you implement particularly simple or particularly complex tile interfaces, you may wish to adjust the property [TileGrid.drawAllMaxTiles](#attr-tilegriddrawallmaxtiles).

**Flags**: IRW

---
## Attr: TileGrid.valuesShowDown

### Description
Should tile values change state when the mouse goes down on them?

**Flags**: IR

---
## Attr: TileGrid.selectionType

### Description
Defines a tileGrid's clickable-selection behavior.

### Groups

- selection
- appearance

### See Also

- [SelectionStyle](../reference.md#type-selectionstyle)

**Flags**: IRW

---
## Attr: TileGrid.showEmptyMessage

### Description
Indicates whether the text of the emptyMessage property should be displayed if no data is available.

### Groups

- emptyMessage

### See Also

- [TileGrid.emptyMessage](#attr-tilegridemptymessage)

**Flags**: IRW

---
## Attr: TileGrid.canReorderTiles

### Description
Indicates whether tiles can be reordered by dragging within this `TileGrid`.

**NOTE:** If `canReorderTiles` is initially enabled or might be [dynamically enabled](#method-tilegridsetcanreordertiles) after the grid is created, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging a tile starts a reorder operation rather than a scroll. If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag-reordering of tiles.

### Groups

- dragging

**Flags**: IRW

---
## Attr: TileGrid.showAllRecords

### Description
Whether tiles are created and drawn for all records, or only for those currently visible.

This setting is incompatible with [TileGrid.dataFetchMode](#attr-tilegriddatafetchmode): "paged" as it requires all records matching the criteria to be fetched from the server at once.

### Groups

- basics

**Flags**: IR

---
## Attr: TileGrid.tileScreen

### Description
Screen to create (via [createScreen()](RPCManager.md#classmethod-rpcmanagercreatescreen)) for the tile in lieu of calling [TileGrid.getTile](#method-tilegridgettile).

If this grid has a [dataSource](DataBoundComponent.md#attr-databoundcomponentdatasource), the created screen is provided with a [Canvas.dataContext](Canvas.md#attr-canvasdatacontext) that includes the record being expanded. Be sure the tile screen meets these [requirements](Canvas.md#attr-canvasautopopulatedata) to utilize the `dataContext`.

**Flags**: IR

---
## Attr: TileGrid.initialCriteria

### Description
Criteria to be used when [TileGrid.autoFetchData](#attr-tilegridautofetchdata) is set.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

### Groups

- searchCriteria

**Flags**: IR

---
## Attr: TileGrid.showDetailFields

### Description
By default, TileGrids will not show fields marked [detail:true](DataSourceField.md#attr-datasourcefielddetail) in the DataSource. See also [TileGrid.fields](#attr-tilegridfields).

**Flags**: IR

---
## Attr: TileGrid.recycleTiles

### Description
This property determines whether tiles that are no longer visible (due to scrolling) are recycled, allowing a large number of records to be displayed using a (potentially) much smaller set of tiles.

Recycling tiles may significantly reduce the number of live tile widgets needed to support a particular TileGrid, but may also result in extra work when the TileGrid is scrolled, as a scroll that brings off-screen tiles into view will require recycling tiles that have left the view, even if the new tiles have been visited before (in previous scrolling).

Recycling will occur when [TileGrid.getTile](#method-tilegridgettile) is called, unless the supplied record (or record specified by index) is currently bound to an existing tile. Even if recycling is not enabled, the record associated with a given tile may change if the TileGrid data changes.

For more control over the tile creation and recycling process, see [TileGrid.createTile](#method-tilegridcreatetile) and [TileGrid.updateTile](#method-tilegridupdatetile).

**Flags**: IR

---
## Attr: TileGrid.dataArity

### Description
A TileGrid is a [dataArity](DataBoundComponent.md#attr-databoundcomponentdataarity):multiple component.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: TileGrid.autoFetchTextMatchStyle

### Description
If [TileGrid.autoFetchData](#attr-tilegridautofetchdata) is `true`, this attribute allows the developer to specify a textMatchStyle for the initial [fetchData()](ListGrid_2.md#method-listgridfetchdata) call.

### Groups

- databinding

**Flags**: IR

---
## Attr: TileGrid.emptyMessage

### Description
The string to display in the body of a tileGrid with an empty data array, if [TileGrid.showEmptyMessage](#attr-tilegridshowemptymessage) is true.

### Groups

- emptyMessage
- i18nMessages

### See Also

- [TileGrid.showEmptyMessage](#attr-tilegridshowemptymessage)
- [TileGrid.emptyMessageStyle](#attr-tilegridemptymessagestyle)

**Flags**: IRW

---
## Attr: TileGrid.canDragTilesOut

### Description
Indicates whether tiles can be dragged from this `TileGrid` and dropped elsewhere.

**NOTE:** If `canDragTilesOut` is initially enabled or might be [dynamically enabled](#method-tilegridsetcandragtilesout) after the grid is created, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging a tile starts a drag operation rather than a scroll. If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag and drop of tiles out of the grid.

### Groups

- dragging

**Flags**: IRW

---
## Attr: TileGrid.valuesShowSelected

### Description
Should tile values change state when they are selected?

**Flags**: IR

---
## Attr: TileGrid.loadingMessage

### Description
If you have a databound tileGrid and you scroll out of the currently loaded dataset, by default you will see blank tiles until the server returns the data for those rows. The loadingMessage attribute allows you to specify arbitrary html that will be shown in each such "blank" tile while the data for that tile is loading. (e.g. "`<DIV ALIGN='CENTER'>`LOADING`</DIV>`")

### Groups

- emptyMessage
- i18nMessages

**Flags**: IR

---
## Attr: TileGrid.loadingDataMessage

### Description
The string to display in the body of a tileGrid while data is being loaded. Use `"${loadingImage}"` to include [a loading image](Canvas.md#classattr-canvasloadingimagesrc).

### Groups

- emptyMessage
- i18nMessages

### See Also

- [TileGrid.loadingDataMessageStyle](#attr-tilegridloadingdatamessagestyle)

**Flags**: IRW

---
## Method: TileGrid.setHilites

### Description
Only supported on ListGrid for now.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hilites | [Array of Hilite](#type-array-of-hilite) | false | — | Array of hilite objects |

### Groups

- hiliting

---
## Method: TileGrid.filterData

### Description
Retrieves data that matches the provided criteria and displays the matching data in this component.

This method behaves exactly like [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata) except that [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) is automatically set to "substring" so that String-valued fields are matched by case-insensitive substring comparison.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | Search criteria. If a [DynamicForm](DynamicForm.md#class-dynamicform) is passed in as this argument instead of a raw criteria object, will be derived by calling [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke when a fetch is complete. Fires only if server contact was required; see [fetchData()](ListGrid_2.md#method-listgridfetchdata) for details |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | for databound components only - optional additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [DataBoundComponent.willFetchData](DataBoundComponent.md#method-databoundcomponentwillfetchdata)

---
## Method: TileGrid.loadAllRecords

### Description
Loads all records that match this grid's current filter-criteria, optionally firing a callback when the data arrives.

If the length of the data is [not known](ResultSet.md#method-resultsetlengthisknown), or is greater than the passed _maxRecords_, this call returns false. No fetch is issued and the _callback_, if passed, is not fired.

If all data is [already loaded](ResultSet.md#method-resultsetallmatchingrowscached), no fetch is issued and this call returns true. The _callback_, if passed, will be fired, but its parameters will be null, since there was no fetch to provide the values from.

In all other cases, this call returns true and a fetch is issued for all necessary records. When the data arrives, the _callback_ is fired.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| maxRecords | [Integer](../reference_2.md#type-integer) | true | — | optional maximum record count - if passed, no fetch takes place if maxRecords is below the known length of the data |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to fire if a fetch is issued - if all data was already loaded, the callback is fired with no parameters |

### Returns

`[Boolean](#type-boolean)` — true if a fetch was made or was not needed - false otherwise

### Groups

- dataBoundComponentMethods

---
## Method: TileGrid.recordClick

### Description
Executed when the tileGrid receives a 'click' event on a tile. The default implementation does nothing -- override to perform some action when any record is clicked.  
A record event handler can be specified either as a function to execute, or as a string of script to evaluate. If the handler is defined as a string of script, all the parameters below will be available as variables for use in the script.  
If you want to cancel the click based on the parameters, return false. Otherwise, return true so that the click event be registered with the tile.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TileGrid](#type-tilegrid) | false | — | the TileGrid itself |
| tile | [Canvas](#type-canvas) | false | — | the tile that was clicked on |
| record | [TileRecord](#type-tilerecord) | false | — | the record that was clicked on |

### Groups

- events

---
## Method: TileGrid.getTitleField

### Description
Method to return the fieldName which represents the "title" for records in this Component.  
If this.titleField is explicitly specified it will always be used. Otherwise, default implementation will check [DataSource.titleField](DataSource.md#attr-datasourcetitlefield) for databound compounds.  
For non databound components returns the first defined field name of `"title"`, `"name"`, or `"id"` where the field is visible. If we don't find any field-names that match these titles, the first field in the component will be used instead.

### Returns

`[String](#type-string)` — fieldName for title field for this component.

---
## Method: TileGrid.deselectRange

### Description
Deselect a contiguous range of records by index.

This is a synonym for `selectRange(startRow, endRow, false);`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../reference.md#type-int) | false | — | start of selection range |
| endRow | [int](../reference.md#type-int) | false | — | end of selection range (non-inclusive) |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: TileGrid.exportData

### Description
Sends the current filter criteria and sort direction to the server, then exports data in the requested [exportFormat](DSRequest.md#attr-dsrequestexportas).

A variety of DSRequest settings, such as [exportAs](DSRequest.md#attr-dsrequestexportas) and [DSRequest.exportFilename](DSRequest.md#attr-dsrequestexportfilename), affect the exporting process: see [exportResults](DSRequest.md#attr-dsrequestexportresults) for further detail.

Note that data exported via this method skips client-side fields defined only in the component, excludes any client-side formatting and relies on both the SmartClient server and server-side DataSources. To export client-data including client-only fields and with client-side formatting applied, see [exportClientData](ListGrid_2.md#method-listgridexportclientdata), which still requires the SmartClient server but does not rely on server-side DataSource definitions (.ds.xml files).

For more information on exporting data, see [DataSource.exportData](DataSource.md#method-datasourceexportdata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke on completion. Note that this parameter only applies where [DSRequest.exportToClient](DSRequest.md#attr-dsrequestexporttoclient) is explicitly set to false, because file downloads do not provide ordinary SmartClient callbacks |

### Groups

- dataBoundComponentMethods

### See Also

- [exportFormatting](../kb_topics/exportFormatting.md#kb-topic-exports--formatting)

---
## Method: TileGrid.dataArrived

### Description
Notification method fired when new data arrives from the server to be displayed in this tileGrid, (for example in response to the user scrolling a new set of tiles into view). Only applies to databound tileGrid where the [data](#attr-tilegriddata) attribute is a [ResultSet](ResultSet.md#class-resultset). This method is fired directly in response to [dataArrived()](ResultSet.md#method-resultsetdataarrived) firing on the data object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRecord | [int](../reference.md#type-int) | false | — | starting index of the newly loaded set of records |
| endRecord | [int](../reference.md#type-int) | false | — | ending index of the newly loaded set of records (non inclusive). |

**Flags**: A

---
## Method: TileGrid.addData

### Description
Perform a DataSource "add" operation to add new records to this component's DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newRecord | [Record](#type-record) | false | — | new record |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | method to call on operation completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: TileGrid.selectAllRecords

### Description
Select all records

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: TileGrid.selectRange

### Description
Select a contiguous range of records by index

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startRow | [int](../reference.md#type-int) | false | — | start of selection range |
| endRow | [int](../reference.md#type-int) | false | — | end of selection range (non-inclusive) |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: TileGrid.removeSelectedData

### Description
Remove the currently selected records from this component. If this is a databound grid, the records will be removed directly from the DataSource. The grid will automatically be updated if the record deletion succeeds.

If no records are selected, no action is taken and neither callback will be called.

For a grid with no DataSource or where `saveLocally` is true, the data removal is performed on the client and both callbacks will fire with no arguments.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to fire when each record has been removed |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |
| queueCallback | [RPCQueueCallback](#type-rpcqueuecallback) | true | — | callback to fire after all selected data has been removed |

### Groups

- dataBoundComponentMethods

---
## Method: TileGrid.viewSelectedData

### Description
Displays the currently selected record(s) of the selectionComponent widget (typically a listGrid) in this component.

For a DynamicForm the first record of the selection is shown after the form is placed into [read-only mode](DynamicForm.md#attr-dynamicformcanedit). A subsequent call to [DynamicForm.editRecord](DynamicForm.md#method-dynamicformeditrecord) or similar will return the form to editability.

Note that since field-level `canEdit:true` settings override the form-level canEdit setting the automatic change to read-only may not change every field.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectionComponent | [ListGrid](#type-listgrid)|[TileGrid](#type-tilegrid)|[ID](#type-id) | false | — | the ListGrid or TileGrid or ID of a [ListGrid](ListGrid_1.md#class-listgrid)/[TileGrid](#class-tilegrid) whose currently selected record(s) is/are to be viewed |

### Groups

- dataBoundComponentMethods

---
## Method: TileGrid.deselectRecord

### Description
Deselect a [Record](../reference.md#object-record) passed in explicitly, or by index.

Synonym for `selectRecord(record, false)`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record)|[number](#type-number) | false | — | record (or row number) to deselect |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | row number to select. Required for [multi-link trees](Tree.md#attr-treemultilinktree) unless row number is passed in the "record" param |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: TileGrid.transferDragData

### Description
During a drag-and-drop interaction, this method is called to transfer a set of records that were dropped onto some other component. This method is called after the set of records has been copied to the other component. Whether or not this component's data is modified is determined by the value of [DataBoundComponent.dragDataAction](DataBoundComponent.md#attr-databoundcomponentdragdataaction).

With a `dragDataAction` of "move", a databound component will issue "remove" dsRequests against its DataSource to actually remove the data, via [DataSource.removeData](DataSource.md#method-datasourceremovedata).

### Returns

`[Array](#type-array)` — Array of objects that were dragged out of this ListGrid.

### See Also

- [DataBoundComponent.getDragData](DataBoundComponent.md#method-databoundcomponentgetdragdata)
- [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop)

---
## Method: TileGrid.updateTile

### Description
If both this method and [TileGrid.createTile](#method-tilegridcreatetile) are defined and [TileGrid.recycleTiles](#attr-tilegridrecycletiles) is true, this method will be called when the framework needs to recycle a tile to be used with a new record. This notification provides an opportunity to update any widget properties that depend on the specifics of the record.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | record that will be associated with the recycled tile |
| tileIndex | [Integer](../reference_2.md#type-integer) | false | — | index of the record in the tileGrid |
| reclaimedTile | [Canvas](#type-canvas) | false | — | the tile to be recycled |

### See Also

- [TileGrid.recycleTiles](#attr-tilegridrecycletiles)

---
## Method: TileGrid.getTile

### Description
Returns the tile for the passed record or record index.

Note that this method may be overridden but developers should be aware that this method may be called repeatedly for the same record each time the TileGrid refreshes that row. If you override this API, you will need to cache and re-use the same tile objects per record. Typically this would be achieved by storing a pool of Tile objects that are re-used if a Record with the same primaryKey is passed to getTile().

When calling this method directly, if [TileGrid.showAllRecords](#attr-tilegridshowallrecords) is false, this may return null for records that are not currently visible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tile | [TileRecord](#type-tilerecord)|[int](../reference.md#type-int) | false | — | record or index of record in this.data |

### Returns

`[Canvas](#type-canvas)` — tile for this record

### See Also

- [TileGrid.tileScreen](#attr-tilegridtilescreen)

---
## Method: TileGrid.addTile

### Description
This is not allowed for tileGrid. Instead, use [TileGrid.addData](#method-tilegridadddata).

---
## Method: TileGrid.removeData

### Description
Perform a DataSource "remove" operation to remove records from this component's DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Record](#type-record) | false | — | primary key values of record to delete, (or complete record) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | method to call on operation completion |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

---
## Method: TileGrid.transferSelectedData

### Description
Simulates a drag / drop type transfer of the selected records in some other component to this component, without requiring any user interaction. This method acts on the dropped records exactly as if they had been dropped in an actual drag / drop interaction, including any special databound behavior invoked by calling [getDropValues](DataBoundComponent.md#method-databoundcomponentgetdropvalues) for each dropped record.

To transfer **all** data in, for example, a [ListGrid](ListGrid_1.md#class-listgrid), call [ListGrid.selectAllRecords](ListGrid_2.md#method-listgridselectallrecords) first.

Note that drag/drop type transfers of records between components are asynchronous operations: SmartClient may need to perform server turnarounds to establish whether dropped records already exist in the target component. Therefore, it is possible to issue a call to transferSelectedData() and/or the [drop()](ListGrid_2.md#method-listgriddrop) method of a databound component whilst a transfer is still active. When this happens, SmartClient adds the second and subsequent transfer requests to a queue and runs them one after the other. If you want to be notified when a transfer process has actually completed, either provide a callback to this method or implement [DataBoundComponent.dropComplete](DataBoundComponent.md#method-databoundcomponentdropcomplete).

See the [dragging](../reference.md#kb-topic-dragging) documentation for an overview of list grid drag/drop data transfer.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| source | [DataBoundComponent](#type-databoundcomponent) | false | — | source component from which the records will be transferred |
| index | [Integer](../reference_2.md#type-integer) | true | — | target index (drop position) of the rows within this grid. |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback to be fired when the transfer process has completed. The callback will be passed a single parameter "records", the list of records actually transferred to this component. |

### Groups

- dragdrop

---
## Method: TileGrid.deselectRecords

### Description
Deselect a list of [Record](../reference.md#object-record)s passed in explicitly, or by index.

Synonym for `selectRecords(records, false)`

Note that developers may wish to use [TileGrid.deselectRange](#method-tilegriddeselectrange) to select a single contiguous range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record)|[number](#type-number) | false | — | records (or row numbers) to deselect |
| rowNums | [Array of Integer](#type-array-of-integer) | false | — | row numbers to select. Required for [multi-link trees](Tree.md#attr-treemultilinktree) unless row numbers are passed in the "records" param. If passed, the rowNums array should correspond to the records array (ie, rowNums\[0\] refers to the same object as records\[0\]) |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: TileGrid.invalidateCache

### Description
Invalidate the current data cache for this databound component via a call to the dataset's `invalidateCache()` method, for example, [ResultSet.invalidateCache](ResultSet.md#method-resultsetinvalidatecache).

**NOTE:** there is no need to call `invalidateCache()` when a save operation is performed on a DataSource. Automatic cache synchronization features will automatically update caches - see [ResultSet](ResultSet.md#class-resultset) for details. If automatic cache synchronization isn't working, troubleshoot the problem using the steps suggested [in the FAQ](http://forums.smartclient.com/showthread.php?t=8159#aGrid) rather than just calling invalidateCache(). Calling `invalidateCache()` unnecessarily causes extra server load and added code complexity.

Calling `invalidateCache()` will automatically cause a new fetch to be performed with the current set of criteria if data had been previously fetched and the component is currently drawn with data visible - there is no need to manually call fetchData() after invalidateCache() and this could result in duplicate fetches.

While data is being re-loaded after a call to `invalidateCache()`, the widget is in a state similar to initial data load - it doesn't know the total length of the dataset and any APIs that act on records or row indices will necessarily fail and should not be called. To detect that the widget is in this state, call [ResultSet.lengthIsKnown](ResultSet.md#method-resultsetlengthisknown).

`invalidateCache()` only has an effect if this components dataset is a data manager class that manages a cache (eg ResultSet or ResultTree). If data was provided as a simple Array or List, invalidateCache() does nothing.

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.refreshData](ListGrid_2.md#method-listgridrefreshdata)

---
## Method: TileGrid.getDropIndex

### Description
Returns the record index of the tile that would currently be dropped on by the drag in process. Returns one beyond the last valid index to indicate a drop after all records. Except for that special case, a non-null index returned by this method may be passed to [TileGrid.getTile](#method-tilegridgettile) to get the corresponding visible tile.

### Returns

`[int](../reference.md#type-int)` — record index of tile that would currently be dropped on, or the record count for a drop after all records

### See Also

- [TileLayout.transformTileRect](TileLayout.md#method-tilelayouttransformtilerect)

---
## Method: TileGrid.removeTile

### Description
This is not allowed for tileGrid. Instead, use [TileGrid.removeData](#method-tilegridremovedata).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tileID | [Canvas](#type-canvas)|[int](../reference.md#type-int)|[ID](#type-id) | false | — | index or String ID of the tile |

### Returns

`[boolean](../reference.md#type-boolean)` — whether a tile was found and removed

---
## Method: TileGrid.recordContextClick

### Description
Executed when the tileGrid receives a context-click (right mouse button) event on a tile. The default implementation does nothing -- override to perform some action when any record is right-clicked.  
Return `false` to cancel the native behavior (suppressing the browser context menu).

A record event handler can be specified either as a function to execute, or as a string of script to evaluate. If the handler is defined as a string of script, all the parameters below will be available as variables for use in the script.  
If you want to cancel the click based on the parameters, return false. Otherwise, return true so that the click event be registered with the tile.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TileGrid](#type-tilegrid) | false | — | the TileGrid itself |
| tile | [Canvas](#type-canvas) | false | — | the tile that was clicked on |
| record | [TileRecord](#type-tilerecord) | false | — | the record that was clicked on |

### Returns

`[boolean](../reference.md#type-boolean)` — return false to suppress the native browser context menu.

### Groups

- events

---
## Method: TileGrid.createTile

### Description
If defined, this method will be called when a new tile is required. Note that this method is in complete control of how the tile is constructed, so that properties such as [TileGrid.tileProperties](#attr-tilegridtileproperties) and others needed by TileGrid will be applied only after this method returns.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | record that will be associated with new tile |
| tileIndex | [Integer](../reference_2.md#type-integer) | false | — | index of the record in the tileGrid |

### Returns

`[Canvas](#type-canvas)` — return the new tile that will hold the record (cannot be null)

### See Also

- [TileGrid.recycleTiles](#attr-tilegridrecycletiles)
- [TileGrid.tileProperties](#attr-tilegridtileproperties)

---
## Method: TileGrid.getFieldState

### Description
Returns a snapshot of the current presentation of this grid's fields as a [ListGridFieldState](../reference_2.md#type-listgridfieldstate) object.

This object can be passed to [TileGrid.setFieldState](#method-tilegridsetfieldstate) to reset this grid's fields to the current state.

Note that the information stored includes the current width and visibility of each of this grid's fields.

The optional `sparse` parameter governs whether the returned field state should omit state information for hidden fields. If this parameter is not passed explicitly, field state will be sparse if [DataBoundComponent.sparseFieldState](DataBoundComponent.md#attr-databoundcomponentsparsefieldstate) is true.  
When applying sparse field state to a component via [TileGrid.setFieldState](#method-tilegridsetfieldstate), any explicitly defined fields on the component that were not captured in the stored state object will be hidden.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sparse | [Boolean](#type-boolean) | true | — | If true, field state will be ommitted for hidden fields. |

### Returns

`[ListGridFieldState](../reference_2.md#type-listgridfieldstate)` — current state of this grid's fields.

### Groups

- viewState

### See Also

- [TileGrid.setFieldState](#method-tilegridsetfieldstate)

---
## Method: TileGrid.getDragTrackerTitle

### Description
Return "title" HTML to display as a drag tracker when the user drags some record.  
Default implementation will display the cell value for the title field (see [ListGrid.getTitleField](ListGrid_2.md#method-listgridgettitlefield)) for the record(s) being dragged (including any icons / custom formatting / styling, etc).

Note: Only called if [ListGrid.dragTrackerMode](ListGrid_1.md#attr-listgriddragtrackermode) is set to `"title"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | First selected record being dragged |
| rowNum | [number](#type-number) | false | — | row index of first record being dragged |

### Returns

`[String](#type-string)` — Title for the row. Default implementation looks at the value of the title-field cell for the row.

### Groups

- dragTracker

---
## Method: TileGrid.getTileIndex

### Description
Returns the index of the specified tile.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tile | [Canvas](#type-canvas) | false | — | Tile you want to get the index for |

### Returns

`[int](../reference.md#type-int)` — index of the tile in this tileGrid. Will return -1 if the specified tile is not displayed within this grid.

---
## Method: TileGrid.setData

### Description
Provides a new data set to the TileGrid after the grid has been created or drawn. The TileGrid will redraw to show the new data automatically.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [Array of Record](#type-array-of-record)|[Array of TileRecord](#type-array-of-tilerecord)|[ResultSet](#type-resultset) | false | — | data to show in the list |

### Groups

- data

---
## Method: TileGrid.recordDoubleClick

### Description
Executed when the tileGrid receives a 'doubleclick' event on a tile. The default implementation does nothing -- override to perform some action when any record is doubleclicked.  
A record event handler can be specified either as a function to execute, or as a string of script to evaluate. If the handler is defined as a string of script, all the parameters below will be available as variables for use in the script.  
If you want to cancel the doubleclick based on the parameters, return false. Otherwise, return true so that the doubleclick event be registered with the tile.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TileGrid](#type-tilegrid) | false | — | the TileGrid itself |
| tile | [Canvas](#type-canvas) | false | — | the tile that was doubleclicked on |
| record | [TileRecord](#type-tilerecord) | false | — | the record that was doubleclicked on |

### Groups

- events

---
## Method: TileGrid.getCurrentTile

### Description
Returns the tile currently under the mouse.

### Returns

`[SimpleTile](#type-simpletile)` — the tile currently under the mouse

---
## Method: TileGrid.setDragTracker

### Description
Sets the custom tracker HTML to display next to the mouse when the user initiates a drag operation on this component. Default implementation will examine [ListGrid.dragTrackerMode](ListGrid_1.md#attr-listgriddragtrackermode) and set the custom drag tracker to display the appropriate HTML based on the selected record.  
To display custom drag tracker HTML, this method may be overridden - call [EventHandler.setDragTracker](EventHandler.md#classmethod-eventhandlersetdragtracker) to actually update the drag tracker HTML.

### Returns

`[boolean](../reference.md#type-boolean)` — returns false by default to suppress 'setDragTracker' on any ancestors of this component.

### Groups

- dragTracker

---
## Method: TileGrid.getDragData

### Description
During a drag-and-drop interaction, this method returns the set of records being dragged out of the component. In the default implementation, this is the list of currently selected records.

This method is consulted by [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop).

NOTE: If this component is a [multi-linked](Tree.md#method-treeismultilinktree) `TreeGrid`, this method returns a list of [NodeLocator](../reference_2.md#object-nodelocator)s rather than a list of records. Each `nodeLocator` contains a pointer to the associated record in its `node` property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| source | [DataBoundComponent](#type-databoundcomponent) | false | — | source component from which the records will be transferred |

### Returns

`[Array of Record](#type-array-of-record)` — Array of [Record](../reference.md#object-record)s that are currently selected.

### Groups

- dragging
- data

---
## Method: TileGrid.setFieldState

### Description
Sets some presentation properties (visibility, width, userFormula and userSummary) of the grid fields based on the [ListGridFieldState](../reference_2.md#type-listgridfieldstate) object passed in.  
Used to restore previous state retrieved from the grid by a call to [TileGrid.getFieldState](#method-tilegridgetfieldstate).

The optional `isSparse` parameter may be passed to indicate whether the fieldState object is "sparse" - whether it includes explicit state information for hidden fields. In this case any fields defined on the component not explicitly included in the fieldState object will be hidden.  
If `isSparse` is not explicitly passed as a parameter, sparseness will be assumed if [DataBoundComponent.sparseFieldState](DataBoundComponent.md#attr-databoundcomponentsparsefieldstate) is true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldState | [ListGridFieldState](../reference_2.md#type-listgridfieldstate) | false | — | state to apply to the grid's fields. |
| isSparse | [Boolean](#type-boolean) | true | — | If true, the fieldState passed in is assumed to be "sparse". Any fields defined on this component without explicit field state values will be hidden. |

### Groups

- viewState

### See Also

- [TileGrid.getFieldState](#method-tilegridgetfieldstate)

---
## Method: TileGrid.getTileHTML

### Description
Generate the tile HTML for a record in the data set.

This method is invoked automatically by each tile created as an instance of the [SimpleTile](SimpleTile.md#class-simpletile) class to get its content. If [TileGrid.tileConstructor](#attr-tilegridtileconstructor) has been modified this method therefore may not be called. (See also [TileGrid.tile](#attr-tilegridtile)).

The default implementation of this method uses an automatically generated [detailViewer autoChild](DetailViewer.md#class-detailviewer) to generate HTML for the specified `tileRecord` based on the specified [TileGrid.fields](#attr-tilegridfields) for this tileGrid.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tileRecord | [TileRecord](#type-tilerecord) | false | — | the tile for which HTML should be retrieved |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML contents for the tile, as a String

---
## Method: TileGrid.deselectAllRecords

### Description
Deselect all records

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: TileGrid.getSelectedRecord

### Description
Returns the first selected record in this component.

**NOTE:** If a record is returned, it should be treated as read-only and not modified.

### Returns

`[TileRecord](#type-tilerecord)` — first selected record, or null if nothing selected

### Groups

- selection

---
## Method: TileGrid.fetchData

### Description
Retrieves data from the DataSource that matches the specified criteria.

For a discussion of the various filtering and criteria-management APIs and when to use them, see the [Grid Filtering overview](../kb_topics/gridFiltering.md#kb-topic-grid-filtering-overview).

When `fetchData()` is first called, if data has not already been provided via [setData()](ListGrid_2.md#method-listgridsetdata), this method will create a [ResultSet](ResultSet.md#class-resultset), which will be configured based on component settings such as [DataBoundComponent.fetchOperation](DataBoundComponent.md#attr-databoundcomponentfetchoperation) and [DataBoundComponent.dataPageSize](DataBoundComponent.md#attr-databoundcomponentdatapagesize), as well as the general purpose [ListGrid.dataProperties](ListGrid_1.md#attr-listgriddataproperties). The created ResultSet will automatically send a DSRequest to retrieve data from [listGrid.dataSource](ListGrid_1.md#attr-listgriddatasource), and from then on will automatically manage paging through large datasets, as well as performing filtering and sorting operations inside the browser when possible - see the [ResultSet](ResultSet.md#class-resultset) docs for details.

**NOTE:** do not use **both** [autoFetchData:true](DataBoundComponent.md#attr-databoundcomponentautofetchdata) **and** a call to `fetchData()` - this may result in two DSRequests to fetch data. Use either [autoFetchData](DataBoundComponent.md#attr-databoundcomponentautofetchdata) and [Criteria](../reference_2.md#type-criteria) **or** a manual call to fetchData() passing criteria.

Whether a ResultSet was automatically created or provided via [setData()](ListGrid_2.md#method-listgridsetdata), subsequent calls to fetchData() will simply call [ResultSet.setCriteria](ResultSet.md#method-resultsetsetcriteria).

Changes to criteria may or may not result in a DSRequest to the server due to [client-side filtering](ResultSet.md#attr-resultsetuseclientfiltering). You can call [willFetchData(criteria)](DataBoundComponent.md#method-databoundcomponentwillfetchdata) to determine if new criteria will result in a server fetch.

If you need to force data to be re-fetched, you can call [invalidateCache()](ListGrid_2.md#method-listgridinvalidatecache) and new data will automatically be fetched from the server using the current criteria and sort direction. **NOTE:** when using `invalidateCache()` there is no need to **also** call `fetchData()` and in fact this could produce unexpected results.

This method takes an optional callback parameter (set to a [DSCallback](../reference_2.md#type-dscallback)) to fire when the fetch completes. Note that this callback will not fire if no server fetch is performed. In this case the data is updated synchronously, so as soon as this method completes you can interact with the new data. If necessary, you can use [willFetchData()](DataBoundComponent.md#method-databoundcomponentwillfetchdata) to determine whether or not a server fetch will occur when `fetchData()` is called with new criteria.

In addition to the callback parameter for this method, developers can use [dataArrived()](ListGrid_2.md#method-listgriddataarrived) to be notified every time data is loaded.

By default, this method assumes a [TextMatchStyle](../reference_2.md#type-textmatchstyle) of "exact"; that can be overridden by supplying a different value in the requestProperties parameter. See [DataBoundComponent.willFetchData](DataBoundComponent.md#method-databoundcomponentwillfetchdata);

**Changing the request properties**

Changes to [TextMatchStyle](../reference_2.md#type-textmatchstyle) made via `requestProperties` will be honored in combination with the fetch criteria, possibly invalidating cache and triggering a server request if needed, as documented for [willFetchData()](DataBoundComponent.md#method-databoundcomponentwillfetchdata). In contrast, changes to [operationId](DSRequest.md#attr-dsrequestoperationid) in the request properties will cause the [ResultSet](ResultSet.md#class-resultset) or [ResultTree](ResultTree.md#class-resulttree) to be rebuilt, always refetching from the server. However, changes to other request properties after the initial fetch won't be detected, and no fetch will get triggered based on that new request context.

To pick up such changes, we recommend that you call [setData(\[\])](#method-tilegridsetdata) (passing an empty array to ensure the data model is cleared), and then call this method to fetch again. If you try to do it by calling [invalidateCache()](ListGrid_2.md#method-listgridinvalidatecache), you may see duplicate fetches if you haven't already updated the data context by calling this method with the new request properties, and fail to do so before the component is [redrawn](Canvas.md#method-canvasredraw).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria) | true | — | Search criteria. If a [DynamicForm](DynamicForm.md#class-dynamicform) is passed in as this argument instead of a raw criteria object, will be derived by calling [DynamicForm.getValuesAsCriteria](DynamicForm.md#method-dynamicformgetvaluesascriteria) |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | callback to invoke when a fetch is complete. Fires only if server contact was required |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | additional properties to set on the DSRequest that will be issued |

### Groups

- dataBoundComponentMethods

### See Also

- [ListGrid.refreshData](ListGrid_2.md#method-listgridrefreshdata)

---
## Method: TileGrid.getTileRecord

### Description
Given a tile within this this tile-grid, this method will return the associated record.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tile | [Canvas](#type-canvas) | false | — | Tile you want to get the record for |

### Returns

`[TileRecord](#type-tilerecord)` — Record associated with the specified tile

---
## Method: TileGrid.selectRecords

### Description
Select/deselect a list of [Record](../reference.md#object-record)s passed in explicitly, or by index.

Note that developers may wish to use [TileGrid.selectRange](#method-tilegridselectrange) to select a single contiguous range.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record)|[number](#type-number) | false | — | records (or row numbers) to select |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |
| rowNums | [Array of Integer](#type-array-of-integer) | false | — | row numbers to select. Required for [multi-link trees](Tree.md#attr-treemultilinktree) unless row numbers are passed in the "records" param. If passed, the rowNums array should correspond to the records array (ie, rowNums\[0\] refers to the same object as records\[0\]) |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: TileGrid.selectRecord

### Description
Select/deselect a [Record](../reference.md#object-record) passed in explicitly, or by index.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record)|[number](#type-number) | false | — | record (or row number) to select |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |
| rowNum | [Integer](../reference_2.md#type-integer) | false | — | row number to select. Required for [multi-link trees](Tree.md#attr-treemultilinktree) unless row number is passed in the "record" param |

### Groups

- selection

### See Also

- [Selection](Selection.md#class-selection)

---
## Method: TileGrid.setCanReorderTiles

### Description
Setter for [TileGrid.canReorderTiles](#attr-tilegridcanreordertiles).

### Groups

- dragging

---
## Method: TileGrid.anySelected

### Description
Whether at least one item is selected

### Returns

`[boolean](../reference.md#type-boolean)` — true == at least one item is selected false == nothing at all is selected

### Groups

- selection

---
## Method: TileGrid.getSelection

### Description
Returns all selected records, as an Array.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| excludePartialSelections | [Boolean](#type-boolean) | true | — | When true, partially selected records will not be returned. Otherwise, both fully and partially selected records are returned. |

### Returns

`[Array of ListGridRecord](#type-array-of-listgridrecord)` — list of records, empty list if nothing selected

### Groups

- selection

---
## Method: TileGrid.setCanAcceptDroppedRecords

### Description
Setter for [TileGrid.canAcceptDroppedRecords](#attr-tilegridcanacceptdroppedrecords).

### Groups

- dragging

---
## Method: TileGrid.setCanDragTilesOut

### Description
Setter for [TileGrid.canDragTilesOut](#attr-tilegridcandragtilesout).

### Groups

- dragging

---
## Method: TileGrid.selectionChanged

### Description
Called when selection changes within this tileGrid. Note this method fires for each record for which selection is modified - so when a user clicks inside a tileGrid this method will typically fire twice (once for the old record being deselected, and once for the new record being selected).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record) | false | — | record for which selection changed |
| state | [boolean](../reference.md#type-boolean) | false | — | New selection state (true for selected, false for unselected) |

### Groups

- selection

**Flags**: A

---
