# ColumnTree Documentation

[← Back to API Index](../reference.md)

---

## Class: ColumnTree

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
The SmartClient system supports hierarchical data (also referred to as tree data due to its "branching" organization) with:

*   the [Tree](Tree.md#class-tree) class, which manipulates hierarchical data sets
*   the TreeGrid widget class, which extends the ListGrid class to visually present tree data in an expandable/collapsible format.
*   the ColumnTree widget class, which visually presents tree data in a so-called "[Miller Column](http://en.wikipedia.org/wiki/Miller_Columns)" format.

For information on DataBinding Trees, see [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding).

A ColumnTree shows a single branch of the underlying [Tree](Tree.md#class-tree) horizontally, from left to right. Thus, the leftmost column shows all the top-level nodes. When the user clicks one of those nodes, a new column is shown immediately to the right of the top-level column, showing the selected node's children. Additional columns are shown as required to present lower-level children. The behavior of ColumnTree is similar to that of the Browser interface in the Apple™ iTunes™ application.

---
## Attr: ColumnTree.fields

### Description
An array of field objects, specifying the order, layout, dynamic calculation, and sorting behavior of each field in each column in the columnTree object. In ColumnTrees, the fields array specifies sub-columns within each main column. Each field in the fields array is a ListGridField object.

If [ColumnTree.dataSource](#attr-columntreedatasource) is also set, this value acts as a set of overrides as explained in [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields).

### Groups

- databinding

### See Also

- [ListGridField](../reference_2.md#object-listgridfield)

**Flags**: IRW

---
## Attr: ColumnTree.showOpenIcons

### Description
If true, show a different icon for `open` folders than closed folders. This is achieved by appending the [ColumnTree.openIconSuffix](#attr-columntreeopeniconsuffix) onto the [ColumnTree.folderIcon](#attr-columntreefoldericon) URL \[for example `"[SKIN]/folder.gif"` might be replaced by `"[SKIN]/folder_open.gif"`.  
**Note** If this property is set to `false` the same icon is shown for open folders as for closed folders, unless a custom folder icon was specified. This will be determined by [ColumnTree.folderIcon](#attr-columntreefoldericon) plus the [ColumnTree.closedIconSuffix](#attr-columntreeclosediconsuffix).

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: ColumnTree.openIconSuffix

### Description
If [ColumnTree.showOpenIcons](#attr-columntreeshowopenicons) is true, this suffix will be appended to the [ColumnTree.folderIcon](#attr-columntreefoldericon) for open folders in this grid.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: ColumnTree.showDetailFields

### Description
Whether to show fields marked `detail:true` when a DataBoundComponent is given a DataSource but no `component.fields`.

The `detail` property is used on DataSource fields to mark fields that shouldn't appear by default in a view that tries to show many records in a small space.

### Groups

- databinding

**Flags**: IR

---
## Attr: ColumnTree.autoFetchTextMatchStyle

### Description
If [ColumnTree.autoFetchData](#attr-columntreeautofetchdata) is `true`, this attribute allows the developer to specify a textMatchStyle for the initial [fetchData()](ListGrid_2.md#method-listgridfetchdata) call.

### Groups

- databinding

**Flags**: IR

---
## Attr: ColumnTree.autoFetchData

### Description
If true, when this component is first drawn, automatically call `this.fetchData()`. Criteria for this fetch may be picked up from [ColumnTree.initialCriteria](#attr-columntreeinitialcriteria), and textMatchStyle may be specified via [autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle). Additional request properties may be specified using [fetchRequestProperties](#attr-databoundcomponentfetchrequestproperties).

NOTE: if `autoFetchData` is set, calling [fetchData()](ListGrid_2.md#method-listgridfetchdata) before draw will cause two requests to be issued, one from the manual call to fetchData() and one from the autoFetchData setting. The second request will use only [ColumnTree.initialCriteria](#attr-columntreeinitialcriteria) and not any other criteria or settings from the first request. Generally, turn off autoFetchData if you are going to manually call [fetchData()](ListGrid_2.md#method-listgridfetchdata) at any time. Note: If you are using saved searches - either via [SavedSearchItem](SavedSearchItem.md#class-savedsearchitem) or [ListGrid.saveDefaultSearch](ListGrid_1.md#attr-listgridsavedefaultsearch), autoFetchData will be automatically suspended and replaced with the saved criteria/view state, if applicable.

### Groups

- databinding

### See Also

- [ListGrid.fetchData](ListGrid_2.md#method-listgridfetchdata)

**Flags**: IR

---
## Attr: ColumnTree.closedIconSuffix

### Description
This suffix will be appended to the [ColumnTree.folderIcon](#attr-columntreefoldericon) for closed folders. If [ColumnTree.showOpenIcons](#attr-columntreeshowopenicons) is set to `false` this suffix will also be appended to open folders' icons.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: ColumnTree.loadDataOnDemand

### Description
For databound columnTree instances, should the entire tree of data be loaded on initial fetch, or should each column be loaded as needed. If unset the default ResultTree.loadDataOnDemand setting will be used.

### Groups

- databinding

**Flags**: IR

---
## Attr: ColumnTree.nodeIcon

### Description
The filename of the default icon for all leaf nodes in this grid. To specify a custom image for an individual node, set the [ColumnTree.customIconProperty](#attr-columntreecustomiconproperty) directly on the node.

See [TreeGrid.showNodeIcons](TreeGrid.md#attr-treegridshownodeicons) and [TreeGrid.showFolderIcons](TreeGrid.md#attr-treegridshowfoldericons) for details on suppressing display of icons

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: ColumnTree.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria) and related methods.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

**Flags**: IRW

---
## Attr: ColumnTree.columnWidths

### Description
With [ColumnTree.fixedColumns](#attr-columntreefixedcolumns) enabled, defines the pixel or % width per column.

**Flags**: IR

---
## Attr: ColumnTree.backButton

### Description
When using [single-column mode](#attr-columntreeshowmultiplecolumns), this is the "Back" button that you see hovering above the column UI and that allows backward navigation.

**Flags**: IRW

---
## Attr: ColumnTree.showMultipleColumns

### Description
When set to false, only displays a single column at a time, showing a slide animation when moving between columns.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: ColumnTree.column

### Description
Instance of ListGrid used to display each column of the tree.

**Flags**: IR

---
## Attr: ColumnTree.customIconProperty

### Description
This property allows the developer to customize the icon displayed next to a node. Set `node[grid.customIconProperty]` to the URL of the desired icon to display and it will be shown instead of the standard [ColumnTree.nodeIcon](#attr-columntreenodeicon) for this node.  
Note that if [ColumnTree.showCustomIconOpen](#attr-columntreeshowcustomiconopen) is true for this grid, customized icons for folder nodes will be appended with the [ColumnTree.openIconSuffix](#attr-columntreeopeniconsuffix) suffix on state change, as with the standard [ColumnTree.folderIcon](#attr-columntreefoldericon). Also note that for custom folder icons, the [ColumnTree.closedIconSuffix](#attr-columntreeclosediconsuffix) will never be appended.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: ColumnTree.columnTitles

### Description
With [ColumnTree.fixedColumns](#attr-columntreefixedcolumns) enabled, defines the header title for each column.

**Flags**: IR

---
## Attr: ColumnTree.columnProperties

### Description
Standard set of properties to apply to each generated [column](#attr-columntreecolumn) in this columnTree. Developers may also override [ColumnTree.getColumnProperties](#method-columntreegetcolumnproperties) to return dynamic properties based on the node being displayed.

**Flags**: IRA

---
## Attr: ColumnTree.folderIcon

### Description
The URL of the base icon for all folder nodes in this columnTree. Note that this URL will have [ColumnTree.openIconSuffix](#attr-columntreeopeniconsuffix) or [ColumnTree.closedIconSuffix](#attr-columntreeclosediconsuffix) appended to indicate state changes if appropriate - see documentation on [ColumnTree.showOpenIcons](#attr-columntreeshowopenicons)

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: ColumnTree.data

### Description
A [Tree](Tree.md#class-tree) object consisting of nested [TreeNode](../reference_2.md#object-treenode)s to display in this ColumnTree. The `data` property will typically not be explicitly specified for databound ColumnTrees, where the data is returned from the server via databound component methods such as `fetchData()`

### Groups

- data

**Flags**: IRW

---
## Attr: ColumnTree.dataProperties

### Description
For a `ColumnTree` that uses a DataSource, these properties will be passed to the automatically-created ResultTree. This can be used for various customizations such as modifying the automatically-chosen [Tree.parentIdField](Tree.md#attr-treeparentidfield).

### Groups

- databinding

**Flags**: IR

---
## Attr: ColumnTree.dataFetchMode

### Description
How to fetch and manage records retrieve from the server. See [FetchMode](../reference_2.md#type-fetchmode).

This setting only applies to the [ResultSet](ResultSet.md#class-resultset) automatically created by calling [fetchData()](ListGrid_2.md#method-listgridfetchdata). If a pre-existing ResultSet is passed to setData() instead, it's existing setting for [ResultSet.fetchMode](ResultSet.md#attr-resultsetfetchmode) applies.

### Groups

- databinding

**Flags**: IRW

---
## Attr: ColumnTree.firstColumnTitle

### Description
A title for the leftmost column if [ColumnTree.showHeaders](#attr-columntreeshowheaders) is set (the remaining columns have their titles derived from the item selected in the column to the left). Ignored if [ColumnTree.showHeaders](#attr-columntreeshowheaders) is not set.  
  
Note: if you do not want a heading for the first column leave this attribute at its default value of " ". If you set it to null or the empty string, SmartClient will fall back to displaying the field's name in the heading.

**Flags**: IR

---
## Attr: ColumnTree.emptyColumnMessages

### Description
With [ColumnTree.fixedColumns](#attr-columntreefixedcolumns) enabled, defines each column's [ListGrid.emptyMessage](ListGrid_1.md#attr-listgridemptymessage).

**Flags**: IR

---
## Attr: ColumnTree.showHeaders

### Description
If set, each column in the ColumnTree will show a header with the title of the selected node from the column to the left.

**Flags**: IR

---
## Attr: ColumnTree.canDragRecordsOut

### Description
Indicates whether records can be dragged from this listGrid and dropped elsewhere.

**NOTE:** If `canDragRecordsOut` is initially enabled or might be dynamically enabled after the grid is created, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging a record starts a drag operation rather than a scroll, but see the discussion of [drag handles](ListGrid_2.md#method-listgridshowdraghandles). If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag and drop of records out of the grid.

### Groups

- dragdrop

### See Also

- [TreeNode.canDrag](TreeNode.md#attr-treenodecandrag)
- [TreeNode.canAcceptDrop](TreeNode.md#attr-treenodecanacceptdrop)
- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)

**Flags**: IRW

---
## Attr: ColumnTree.showCustomIconOpen

### Description
Should folder nodes showing custom icons (set via the [ColumnTree.customIconProperty](#attr-columntreecustomiconproperty)), show open state images when the folder is opened. If true, the [ColumnTree.openIconSuffix](#attr-columntreeopeniconsuffix) will be appended to the image URL (so `"customFolder.gif"` might be replaced with `"customFolder_open.gif"`).  
**Note** that the [ColumnTree.closedIconSuffix](#attr-columntreeclosediconsuffix) is never appended to custom folder icons.  
Can be overridden at the node level via the default property [TreeNode.showOpenIcon](TreeNode.md#attr-treenodeshowopenicon) and that property can be renamed via [TreeGrid.customIconOpenProperty](TreeGrid.md#attr-treegridcustomiconopenproperty).

### Groups

- treeIcons

**Flags**: IRWA

---
## Attr: ColumnTree.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference_2.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: ColumnTree.backButtonTitle

### Description
When using [single-column mode](#attr-columntreeshowmultiplecolumns), this i18n property dictates the title for the [button](#attr-columntreebackbutton) docked to the top left which allows navigation back through the column tree.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: ColumnTree.initialCriteria

### Description
Criteria to be used when [ColumnTree.autoFetchData](#attr-columntreeautofetchdata) is set.

This property supports [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) - use [Criterion.valuePath](Criterion.md#attr-criterionvaluepath) to refer to values in the [Canvas.ruleScope](Canvas.md#attr-canvasrulescope).

### Groups

- searchCriteria

**Flags**: IR

---
## Attr: ColumnTree.fixedColumns

### Description
Enables fixed columns mode. All columns are created in advance instead of as navigation occurs.

**Flags**: IR

---
## Attr: ColumnTree.showNodeCount

### Description
If set, and [ColumnTree.showHeaders](#attr-columntreeshowheaders) is also set, each column's header will show a count of the number of nodes in that column

**Flags**: IR

---
## Attr: ColumnTree.customIconOpenProperty

### Description
This property allows the developer to rename the [default node.showOpenIcon](TreeNode.md#attr-treenodeshowopenicon) property.

### Groups

- treeIcons

### See Also

- [TreeGrid.customIconProperty](TreeGrid.md#attr-treegridcustomiconproperty)
- [TreeGrid.showCustomIconOpen](TreeGrid.md#attr-treegridshowcustomiconopen)

**Flags**: IRWA

---
## Method: ColumnTree.selectRecords

### Description
Select/deselect a list of [Record](../reference.md#object-record)s passed in explicitly, or by index.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record)|[number](#type-number) | false | — | records (or row numbers) to select |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |
| rowNums | [Array of Integer](#type-array-of-integer)|[Integer](../reference_2.md#type-integer) | true | — | row numbers to select. Required for [multi-link trees](Tree.md#attr-treemultilinktree) unless row numbers are passed in the "records" param. If passed, the rowNums array should correspond to the records array (ie, rowNums\[0\] refers to the same object as records\[0\]) |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column number |

### Groups

- selection

---
## Method: ColumnTree.getRecord

### Description
Retrieve a record by index.

If `colNum` is passed, returns the record found in that column at that index, or null if the column doesn't exist or the index is too high.

With no `colNum` parameter, a record's index is it's position counting from the first record of the first column and including all records in each column. Note that both index and colNum are zero-based - so the first column is column 0, not column 1.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| index | [int](../reference.md#type-int) | false | — | index of record to return. |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | optional index of the column |

### Returns

`[TreeNode](#type-treenode)` — node at the specified index

---
## Method: ColumnTree.nodeSelected

### Description
Called when a node is selected in any column. Default behavior is to show the next level of the tree in a column to the right of the current column.

The new column will be created if it is not already showing. Any columns further to the right, showing deeper levels of the tree, will be removed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| column | [ListGrid](#type-listgrid) | false | — | the column where a node was selected |
| node | [TreeNode](#type-treenode) | false | — | the node that was selected |

### Returns

`[boolean](../reference.md#type-boolean)` — override and return false to cancel the default action

---
## Method: ColumnTree.getColumnTitle

### Description
Returns the title to show for the header of indicated column. Only called if [ColumnTree.shouldShowHeader](#method-columntreeshouldshowheader) returns true for this column.

By default, returns [ColumnTree.firstColumnTitle](#attr-columntreefirstcolumntitle) for the first column, and for subsequent columns, the result of [this.data.getTitle()](Tree.md#method-treegettitle) called on the `node` passed to this function.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | parent node for the nodes to be shown in the column |
| colNum | [int](../reference.md#type-int) | false | — | index of the column |

---
## Method: ColumnTree.setData

### Description
Set the [Tree](Tree.md#class-tree) object this ColumnTree will view

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [Tree](#type-tree) | false | — | Tree to show |

---
## Method: ColumnTree.transferNodes

### Description
Transfer a list of [TreeNode](../reference_2.md#object-treenode)s within this treeGrid or from from some other component (does not have to be a databound component) into this component. This method is only applicable to list-type components, such as [listGrid](ListGrid_1.md#class-listgrid), [treeGrid](TreeGrid.md#class-treegrid) or [tileGrid](TileGrid.md#class-tilegrid). Please see the paragraph below for special rules concerning [multi-link trees](Tree.md#method-treeismultilinktree).

This method implements the automatic drag-copy and drag-move behavior and calling it is equivalent to completing a drag and drop of the `nodes` (the default [ColumnTree.folderDrop](#method-columntreefolderdrop) implementation simply calls `transferNodes()`)

Note that this method is asynchronous - it may need to perform server turnarounds to prevent duplicates in the target component's data. If you wish to be notified when the transfer process has completed, you can either pass the optional callback to this method or implement the [DataBoundComponent.dropComplete](DataBoundComponent.md#method-databoundcomponentdropcomplete) method on this component.

For a TreeGrid, see also [transferSelectedData()](TreeGrid.md#method-treegridtransferselecteddata).

**Multi-link trees**  
If both the target treeGrid and the `sourceWidget` for this transfer are multi-link treeGrids, the `nodes` parameter must be an array of [NodeLocator](../reference_2.md#object-nodelocator)s rather than TreeNodes. Likewise, if the target (this) component is a multi-link treeGrid, the `folder` parameter must be a NodeLocator.

You can obtain a NodeLocator for a visible node occurence in a multi-link TreeGrid by calling its data model's [getNodeLocator()](Tree.md#method-treegetnodelocator) method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of TreeNode](#type-array-of-treenode)|[Array of NodeLocator](#type-array-of-nodelocator) | false | — | Nodes to transfer to this component |
| folder | [TreeNode](#type-treenode) | false | — | The target folder (eg, of a drop interaction), for context |
| index | [Integer](../reference_2.md#type-integer) | false | — | Insert point within the target folder data for the transferred nodes |
| sourceWidget | [Canvas](#type-canvas) | false | — | The databound or non-databound component from which the nodes are to be transferred. |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback to be fired when the transfer process has completed. The callback will be passed a single parameter "records", the list of nodes actually transferred to this component (it is called "records" because this is logic shared with [ListGrid](ListGrid_1.md#class-listgrid)) |

### Groups

- dragdrop

---
## Method: ColumnTree.setHilites

### Description
Only supported on ListGrid for now.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hilites | [Array of Hilite](#type-array-of-hilite) | false | — | Array of hilite objects |

### Groups

- hiliting

---
## Method: ColumnTree.anySelected

### Description
Whether at least one item is selected in the supplied column (the first column if none is passed)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column number |

### Returns

`[Boolean](#type-boolean)` — true == at least one item is selected in the supplied column, false == nothing at all is selected in the supplied column (note that there may be selections in other columns in this columnTree)

### Groups

- selection

---
## Method: ColumnTree.fetchData

### Description
Uses a "fetch" operation on the current [grid.dataSource](DataSource.md#class-datasource) to retrieve data that matches the provided criteria, and displays the matching data in this component as a tree.

This method will create a [ResultTree](ResultTree.md#class-resulttree) to manage tree data, which will subsequently be available as `columnTree.data`. DataSource records returned by the "fetch" operation are linked into a tree structure according to [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) and [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) declarations on DataSource fields. See the [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) topic for complete details.

By default, the created ResultTree will use folder-by-folder load on demand, asking the server for the children of each folder as the user opens it.

The [ResultTree](ResultTree.md#class-resulttree) created by `fetchData()` can be customized by setting [ColumnTree.dataProperties](#attr-columntreedataproperties) to an Object containing properties and methods to apply to the created ResultTree. For example, the property that determines whether a node is a folder ([isFolderProperty](Tree.md#attr-treeisfolderproperty)) can be customized, or level-by-level loading can be disabled via [loadDataOnDemand:false](ResultTree.md#attr-resulttreeloaddataondemand).

The callback passed to `fetchData` will fire once, the first time that data is loaded from the server. If using folder-by-folder load on demand, use the [ResultTree.dataArrived](ResultTree.md#method-resulttreedataarrived) notification to be notified each time new nodes are loaded.

Note that, if criteria are passed to `fetchData()`, they will be passed every time a new "fetch" operation is sent to the server. This allows you to retrieve multiple different tree structures from the same DataSource. However note that the server is expected to always respond with an intact tree - returned nodes which do not have parents are dropped from the dataset and not displayed.

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
## Method: ColumnTree.getNodeTitle

### Description
Returns the title to show for a node in the ColumnTree. The default implementation returns the result of calling [Tree.getTitle](Tree.md#method-treegettitle) on the node.  
  
You can override this method to return a custom title for nodes in the tree.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | The node for which the title is being requested. |
| recordNum | [Number](#type-number) | false | — | The index of the node. |
| field | [DSField](#type-dsfield) | false | — | The field for which the title is being requested. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the title to display.

### See Also

- [Tree.getTitle](Tree.md#method-treegettitle)

---
## Method: ColumnTree.selectAllRecords

### Description
Select all records in the supplied column (the first column if none is passed)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column number |

### Groups

- selection

---
## Method: ColumnTree.getData

### Description
Returns the [Tree](Tree.md#class-tree) object this ColumnTree is viewing

---
## Method: ColumnTree.getSelectedRecord

### Description
Get the selected record, that is, the parent of the nodes in the rightmost visible column.

This is generally the most recently clicked node unless programmatic navigation has taken place.

If only the first column is showing, the root node is returned (which can be detected via [Tree.isRoot](Tree.md#method-treeisroot)).

### Returns

`[Record](#type-record)` — the selected record

---
## Method: ColumnTree.getColumn

### Description
Advanced API - get the ListGrid representing the indicated column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| column | [int](../reference.md#type-int)|[TreeNode](#type-treenode) | false | — | column number, or parent node of the nodes shown in the column |

### Returns

`[ListGrid](#type-listgrid)` — ListGrid that renders the indicated column, or null if column is not shown

**Flags**: A

---
## Method: ColumnTree.deselectRecords

### Description
Deselect a list of [Record](../reference.md#object-record)s passed in explicitly, or by index.

Synonym for `selectRecords(records, false)`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of Record](#type-array-of-record)|[number](#type-number) | false | — | records (or row numbers) to deselect |
| rowNums | [Array of Integer](#type-array-of-integer)|[Integer](../reference_2.md#type-integer) | true | — | row numbers to select. Required for [multi-link trees](Tree.md#attr-treemultilinktree) unless row numbers are passed in the "records" param. If passed, the rowNums array should correspond to the records array (ie, rowNums\[0\] refers to the same object as records\[0\]) |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column number |

### Groups

- selection

---
## Method: ColumnTree.getColumnProperties

### Description
Additional properties to apply to the ListGrid that will show the indicated column. Returns nothing by default. This method can be overridden to allow, for example, different styling, icons, or row heights per column.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | parent node for the nodes to be shown in the column |
| colNum | [int](../reference.md#type-int) | false | — | index of the column |

### Returns

`[ListGrid Properties](#type-listgrid-properties)` — properties to be applied to the column

**Flags**: A

---
## Method: ColumnTree.folderDrop

### Description
Process a drop of one or more nodes on a TreeGrid folder.  
Note: See [treeGridDrop](../kb_topics/treeGridDrop.md#kb-topic-treegrid-drag-and-drop) for an overview of TreeGrid drag and drop behavior.

This method can be overridden to provide custom drop behaviors and is a more appropriate override point than the lower level [Canvas.drop](Canvas.md#method-canvasdrop) handler.

The default behavior is to simply delegate to the [ColumnTree.transferNodes](#method-columntreetransfernodes) method; thus, the correct way to perform a programmatic folder drop, with all the built-in behaviors described below, is to call `transferNodes()`

If this is a self-drop, nodes are simply reordered. An "update" operation will be submitted to update the [parentId](Tree.md#attr-treeparentidfield) field of the moved node(s).

For a drop from another widget, [TreeGrid.transferDragData](TreeGrid.md#method-treegridtransferdragdata) is called which, depending on the [dragDataAction](TreeGrid.md#attr-treegriddragdataaction) specified on the source widget, may either remove the source nodes from the original list (`dragDataAction:"move"`) or just provide a copy to this tree (`dragDataAction:"copy"`).

In either case the new row(s) appear in the `folder` at the `index` specified by the arguments of the same name.

If this grid is databound, the new nodes will be added to the dataset by calling [DataSource.addData](DataSource.md#method-datasourceadddata). Further, if the new nodes were dragged from another databound component, and [addDropValues](DataBoundComponent.md#attr-databoundcomponentadddropvalues) is true, [getDropValues](DataBoundComponent.md#method-databoundcomponentgetdropvalues) will be called for every item being dropped.

As a special case, if the `sourceWidget` is also databound and a [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) relationship is declared from the `sourceWidget`'s DataSource to this TreeGrid's DataSource, the interaction will be treated as a "drag recategorization" use case such as files being placed in folders, employees being assigned to teams, etc. "update" DSRequests will be submitted that change the foreignKey field in the dropped records to point to the tree folder that was the target of the drop. In this case no change will be made to the Tree data as such, only to the dropped records.

For multi-record drops, Queuing is automatically used to combine all DSRequests into a single HTTP Request (see QuickStart Guide, Server Framework chapter). This allows the server to persist all changes caused by the drop in a single transaction (and this is automatically done when using the built-in server DataSources with Power Edition and above).

If these default persistence behaviors are undesirable, return false to cancel them , then implement your own behavior, typically by using grid.updateData() or addData() to add new records.

**NOTE:** the records you receive in this event are the actual Records from the source component. Use [DataSource.copyRecords](DataSource.md#method-datasourcecopyrecords) to create a copy before modifying the records or using them with updateData() or addData().

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of TreeNode](#type-array-of-treenode) | false | — | List of nodes being dropped |
| folder | [TreeNode](#type-treenode) | false | — | The folder being dropped on |
| index | [int](../reference.md#type-int) | false | — | Within the folder being dropped on, the index at which the drop is occurring. Only passed if [canReorderRecords](TreeGrid.md#attr-treegridcanreorderrecords) is true. |
| sourceWidget | [Canvas](#type-canvas) | false | — | The component that is the source of the nodes (where the nodes were dragged from) |

### Groups

- dragdrop

### See Also

- [ColumnTree.transferNodes](#method-columntreetransfernodes)

---
## Method: ColumnTree.filterData

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
## Method: ColumnTree.navigateBack

### Description
Navigate to the previous column.

---
## Method: ColumnTree.selectRecord

### Description
Select/deselect a [Record](../reference.md#object-record) passed in explicitly, or by index.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record)|[number](#type-number) | false | — | record (or row number) to select |
| newState | [boolean](../reference.md#type-boolean) | true | — | new selection state (if null, defaults to true) |
| rowNum | [Integer](../reference_2.md#type-integer) | true | — | row number to select. Required for [multi-link trees](Tree.md#attr-treemultilinktree) unless row number is passed in the "record" param |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column number |

### Groups

- selection

---
## Method: ColumnTree.deselectRecord

### Description
Deselect a [Record](../reference.md#object-record) passed in explicitly, or by index.

Synonym for `selectRecord(record, false)`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [Record](#type-record)|[number](#type-number) | false | — | record (or row number) to deselect |
| rowNum | [Integer](../reference_2.md#type-integer) | true | — | row number to select. Required for [multi-link trees](Tree.md#attr-treemultilinktree) unless row number is passed in the "record" param |
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column number |

### Groups

- selection

---
## Method: ColumnTree.deselectAllRecords

### Description
Deselect all records in the supplied column (the first column if none is passed)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| colNum | [Integer](../reference_2.md#type-integer) | true | — | Column number |

### Groups

- selection

---
## Method: ColumnTree.shouldShowHeader

### Description
Whether the indicated column should show a header. Returns this.showHeaders by default, override for different behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | parent node for the nodes to be shown in the column |
| colNum | [int](../reference.md#type-int) | false | — | index of the column |

---
