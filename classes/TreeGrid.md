# TreeGrid Documentation

[← Back to API Index](../reference.md)

---

## Class: TreeGrid

*Inherits from:* [ListGrid](ListGrid_1.md#class-listgrid)

### Description
The SmartClient system supports hierarchical data (also referred to as tree data due to its "branching" organization) with:

*   the [Tree](Tree.md#class-tree) class, which manipulates hierarchical data sets
*   the TreeGrid widget class, which extends the ListGrid class to visually present tree data in an expandable/collapsible format.

For information on DataBinding Trees, see [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding).

A TreeGrid works just like a [ListGrid](ListGrid_1.md#class-listgrid), except one column (specified by [TreeGridField.treeField](TreeGridField.md#attr-treegridfieldtreefield)) shows a hierarchical [Tree](Tree.md#class-tree). A TreeGrid is not limited to displaying just the [Tree](Tree.md#class-tree) column - you can define additional columns (via [TreeGrid.fields](#attr-treegridfields)) which will render just like the columns of a [ListGrid](ListGrid_1.md#class-listgrid), and support all of the functionality of ListGrid columns, such as [formatters](ListGridField.md#method-listgridfieldformatcellvalue).

Except where explicitly overridden, [ListGrid](ListGrid_1.md#class-listgrid) methods, callbacks, and properties apply to TreeGrids as well. The [ListGrid](ListGrid_1.md#class-listgrid) defines some methods as taking/returning [ListGridField](../reference_2.md#object-listgridfield) and [ListGridRecord](../reference_2.md#object-listgridrecord). When using those methods in a TreeGrid, those types will be [TreeGridField](../reference.md#object-treegridfield) and [TreeNode](../reference_2.md#object-treenode), respectively.

---
## Attr: TreeGrid.customIconDropProperty

### Description
This property allows the developer to rename the [default node.showDropIcon](TreeNode.md#attr-treenodeshowdropicon) property.

### Groups

- treeIcons

### See Also

- [TreeGrid.customIconProperty](#attr-treegridcustomiconproperty)
- [TreeGrid.showCustomIconDrop](#attr-treegridshowcustomicondrop)

**Flags**: IRWA

---
## Attr: TreeGrid.useAllDataSourceFields

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
## Attr: TreeGrid.customIconOpenProperty

### Description
This property allows the developer to rename the [default node.showOpenIcon](TreeNode.md#attr-treenodeshowopenicon) property.

### Groups

- treeIcons

### See Also

- [TreeGrid.customIconProperty](#attr-treegridcustomiconproperty)
- [TreeGrid.showCustomIconOpen](#attr-treegridshowcustomiconopen)

**Flags**: IRWA

---
## Attr: TreeGrid.selectedIconSuffix

### Description
If [TreeGrid.showSelectedIcons](#attr-treegridshowselectedicons) is true, this suffix will be appended to the [TreeGrid.folderIcon](#attr-treegridfoldericon) for selected nodes in this grid.

### Groups

- treeIcons

**Flags**: IR

---
## Attr: TreeGrid.openerIconSize

### Description
Default width and height in pixels of the opener icons, that is, the icons which show the open or closed state of the node, typically a \[+\] or \[-\] symbol, if not overridden by [TreeGrid.openerIconWidth](#attr-treegridopenericonwidth)/[TreeGrid.openerIconHeight](#attr-treegridopenericonheight).

If [TreeGrid.showConnectors](#attr-treegridshowconnectors) is true, the opener icon includes the connector line, and defaults to [cellHeight](ListGrid_1.md#attr-listgridcellheight).

Otherwise, `openerIconSize` defaults to [TreeGrid.iconSize](#attr-treegridiconsize).

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.canReorderRecords

### Description
Indicates whether records can be reordered by dragging within this `ListGrid`.

**NOTE:** If `canReorderRecords` is initially enabled or might be [dynamically enabled](ListGrid_2.md#method-listgridsetcanreorderrecords) after the grid is created, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging a record starts a reorder operation rather than a scroll, but see the discussion of [drag handles](ListGrid_2.md#method-listgridshowdraghandles). If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag-reordering of records.

### Groups

- treeGridDrop

### See Also

- [TreeNode.canDrag](TreeNode.md#attr-treenodecandrag)
- [TreeNode.canAcceptDrop](TreeNode.md#attr-treenodecanacceptdrop)
- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)

**Flags**: IRWA

---
## Attr: TreeGrid.showSelectedIcons

### Description
If true, show a different icon for selected nodes than unselected nodes. This is achieved by appending the [TreeGrid.selectedIconSuffix](#attr-treegridselectediconsuffix) onto the [TreeGrid.folderIcon](#attr-treegridfoldericon) URL or [TreeGrid.nodeIcon](#attr-treegridnodeicon) for selected records.

If appropriate, this suffix will be combined with the [TreeGrid.openIconSuffix](#attr-treegridopeniconsuffix) or [TreeGrid.closedIconSuffix](#attr-treegridclosediconsuffix) (see [TreeGrid.showOpenIcons](#attr-treegridshowopenicons). So a treeGrid with its `folderIcon` property set to `"[SKIN]/folder.gif"`, with both `showSelectedIcons` and `showOpenIcons` set to true would show an icon with the URL `"[SKIN]/folder_open_selected.gif"` for a folder that was both selected and opened.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.cantDragMultipleNodeOccurencesMessage

### Description
For [Multi-link trees](Tree.md#method-treeismultilinktree) only, the message displayed when the user attempts to drag two or more occurrences of the same node into a parent.

### Groups

- i18nMessages

### See Also

- [TreeGrid.canDragRecordsOut](#attr-treegridcandragrecordsout)
- [TreeGrid.canAcceptDroppedRecords](#attr-treegridcanacceptdroppedrecords)
- [TreeGrid.canReorderRecords](#attr-treegridcanreorderrecords)
- [TreeGrid.parentAlreadyContainsChildMessage](#attr-treegridparentalreadycontainschildmessage)

**Flags**: IR

---
## Attr: TreeGrid.connectorIconWidth

### Description
Width in pixels of the connector-icons, that is, the icons which show the open or closed state of the node when using [connectors](#attr-treegridshowconnectors), typically a \[+\] or \[-\] symbol with connecting lines.

If not specified, [TreeGrid.openerIconWidth](#attr-treegridopenericonwidth) is used instead.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.groupByField

### Description
Not applicable to TreeGrids, as the [TreeGrid.data](#attr-treegriddata) already represents a tree.

### Groups

- grouping

### See Also

- [TreeGrid.groupBy](#method-treegridgroupby)

**Flags**: IR

---
## Attr: TreeGrid.manyItemsImage

### Description
The filename of the icon displayed use as the default drag tracker when for multiple files and/or folders are being dragged.

### Groups

- dragdrop

**Flags**: IRW

---
## Attr: TreeGrid.showFullConnectors

### Description
If [TreeGrid.showConnectors](#attr-treegridshowconnectors) is true, this property determines whether we should show vertical continuation lines for each level of indenting within the tree. Setting to false will show only the hierarchy lines for the most indented path ("sparse" connectors).

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.iconSize

### Description
The standard size (same height and width, in pixels) of node icons in this treeGrid.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.createDefaultTreeField

### Description
If no fields are specified, create a single field with [TreeGridField.treeField](TreeGridField.md#attr-treegridfieldtreefield) set to `true` to show the tree.

This automatically generated field will display values derived by calling [TreeGrid.getNodeTitle](#method-treegridgetnodetitle), and have the column title set to the specified [TreeGrid.treeFieldTitle](#attr-treegridtreefieldtitle).

Has no effect if fields are explicitly specified.

This is a convenience setting to allow a TreeGrid to be created without specifying a field list. If fields are specified, refer to the documentation on property [TreeGrid.autoAssignTreeField](#attr-treegridautoassigntreefield) for a way to automatically have one of the fields be use as the tree field if no fields have [TreeGridField.treeField](TreeGridField.md#attr-treegridfieldtreefield) set.

For databound treeGrids, if there is no explicit fields array specified, developers who wish to pick up all fields from the DataSource definition rather than displaying this single automatically generated tree field may either set this property to false, or set [TreeGrid.useAllDataSourceFields](#attr-treegridusealldatasourcefields) to `true`.

**Flags**: IR

---
## Attr: TreeGrid.childCannotBeItsOwnAncestorMessage

### Description
Message displayed when user attempts to drop a node into a parent that has the same ID as the dropped node somewhere in its ancestor chain (ie, the same node as the parent, or grandparent, and so on)

### Groups

- i18nMessages

### See Also

- [TreeGrid.canDragRecordsOut](#attr-treegridcandragrecordsout)
- [TreeGrid.canAcceptDroppedRecords](#attr-treegridcanacceptdroppedrecords)
- [TreeGrid.canReorderRecords](#attr-treegridcanreorderrecords)

**Flags**: IR

---
## Attr: TreeGrid.parentAlreadyContainsChildMessage

### Description
Message displayed when user attempts to drag a node into a parent that already contains a child of the same name/ID.

### Groups

- i18nMessages

### See Also

- [TreeGrid.canDragRecordsOut](#attr-treegridcandragrecordsout)
- [TreeGrid.canAcceptDroppedRecords](#attr-treegridcanacceptdroppedrecords)
- [TreeGrid.canReorderRecords](#attr-treegridcanreorderrecords)
- [TreeGrid.cantDragMultipleNodeOccurencesMessage](#attr-treegridcantdragmultiplenodeoccurencesmessage)

**Flags**: IR

---
## Attr: TreeGrid.animateFolderEffect

### Description
When animating folder opening / closing, this property can be set to apply an animated acceleration effect. This allows the animation speed to be "weighted", for example expanding or collapsing at a faster rate toward the beginning of the animation than at the end.

### Groups

- animation

**Flags**: IRW

---
## Attr: TreeGrid.extraIconGap

### Description
The amount of gap (in pixels) between the extraIcon (see [TreeGrid.getExtraIcon](#method-treegridgetextraicon)) or checkbox icon and the [nodeIcon](#attr-treegridnodeicon)/ [folderIcon](#attr-treegridfoldericon) or node text.

### Groups

- appearance

**Flags**: IR

---
## Attr: TreeGrid.iconPadding

### Description
Default padding to show between the folder or leaf node icon and cell value in the tree cell.

May be overridden for [folderIcons](#attr-treegridfoldericon) via [TreeGrid.folderIconPadding](#attr-treegridfoldericonpadding). May also be overridden for individual nodes by setting the [TreeGrid.iconPaddingProperty](#attr-treegridiconpaddingproperty) value on individual nodes

**Flags**: IR

---
## Attr: TreeGrid.canAcceptDroppedRecords

### Description
Indicates whether records can be dropped into this listGrid.

### Groups

- treeGridDrop

### See Also

- [treeGridDrop](../kb_topics/treeGridDrop.md#kb-topic-treegrid-drag-and-drop)
- [TreeNode.canDrag](TreeNode.md#attr-treenodecandrag)
- [TreeNode.canAcceptDrop](TreeNode.md#attr-treenodecanacceptdrop)

**Flags**: IRW

---
## Attr: TreeGrid.offlineNodeMessage

### Description
For TreeGrids with loadDataOnDemand: true, a message to show the user if an attempt is made to open a folder, and thus load that node's children, while we are offline and there is no offline cache of that data. The message will be presented to the user in in a pop-up dialog box.

### Groups

- offlineGroup
- i18nMessages

### See Also

- [DataBoundComponent.offlineMessage](DataBoundComponent.md#attr-databoundcomponentofflinemessage)

**Flags**: IRW

---
## Attr: TreeGrid.showFolderIcons

### Description
Should folder nodes in this TreeGrid show icons by default?

If unset, folder node icons will be shown if [TreeGrid.showNodeIcons](#attr-treegridshownodeicons) is true

See [TreeGrid.getIcon](#method-treegridgeticon) for more details on treeGrid icons

**Flags**: IRW

---
## Attr: TreeGrid.displayNodeType

### Description
Specifies the type of nodes displayed in the treeGrid.

### Groups

- treeField

### See Also

- [DisplayNodeType](../reference.md#type-displaynodetype)

**Flags**: IRW

---
## Attr: TreeGrid.openerImage

### Description
The base filename or [stateful image block](../reference.md#object-scstatefulimgconfig) for the opener icon for folder nodes when "showConnectors" is false for this TreeGrid. The opener icon is displayed beside the folder icon in the Tree column for folder nodes. Clicking on this icon will toggle the open state of the folder.

**When set to an [SCImgURL](../reference.md#type-scimgurl):** the stateful filenames for these icons are assembled from this base filename and the state of the node, as follows: If the openerImage is set to `{baseName}.{extension}`, `{baseName}_opened.{extension}` will be displayed next to opened folders, and `{baseName}_closed.{extension}` will be displayed next to closed folders, or if this page is in RTL mode, `{baseName}_opened_rtl.{extension}` and `{baseName}_closed_rtl.{extension}` will be used.

If [TreeGrid.showSelectedOpener](#attr-treegridshowselectedopener) is true the URL for selected nodes will append the string `"_selected"` to the image URLs described above. So for an openerImage set to `{baseName}.{extension}`, the URLs for selected records would be `{baseName}_opened_selected.{extension}`, `{baseName}_closed_selected.{extension}`, etc.

**When set to an _SCStatefulImgConfig:_** _it should contain entries for the default _\_base_ state, as well as the custom states: _opened, closed, opened\_selected and closed\_selected_ (RTL styles are also available, see above). These entries may be set to any combination of supported src strings, including file-paths and sprite-strings._

_The following code shows using [SVG Symbols](../kb_topics/svgSymbols.md#kb-topic-svg-symbols-overview) from a sprite-file:_

```
  openerImage: {
      // _base state is required, although will not be displayed in this case 
      _base: "sprite:svg:fileName.svg#arrowRight;size:12,12;",
      // closed and closed_selected states - make the selected icon blue 
      closed: "sprite:svg:fileName.svg#arrowRight;size:12,12;",
      closed_selected: "sprite:svg:fileName.svg#arrowRight;size:12,12;color:blue;",
      // opened and opened_selected states - make the selected icon blue
      opened: "sprite:svg:fileName.svg#arrowDown;size:12,12;",
      opened_selected: "sprite:svg:fileName.svg#arrowDown;size:12,12;color:blue;"
  }
 
```

### Groups

- treeIcons

**Flags**: IR

---
## Attr: TreeGrid.dataArity

### Description
A TreeGrid is a [dataArity](DataBoundComponent.md#attr-databoundcomponentdataarity):multiple component.

### Groups

- databinding

**Flags**: IRWA

---
## Attr: TreeGrid.closedIconSuffix

### Description
This suffix will be appended to the [TreeGrid.folderIcon](#attr-treegridfoldericon) for closed folders. If [TreeGrid.showOpenIcons](#attr-treegridshowopenicons) is set to `false` this suffix will also be appended to open folders' icons.

### Groups

- treeIcons

**Flags**: IR

---
## Attr: TreeGrid.initialData

### Description
You can specify the initial set of data for a databound TreeGrid using this property. The value of this attribute should be a list of `parentId`\-linked [TreeNode](../reference_2.md#object-treenode)s in a format equivalent to that documented on [Tree.data](Tree.md#attr-treedata) or, for TreeGrids with [dataFetchMode](#attr-treegriddatafetchmode) set to ["paged"](../reference_2.md#type-fetchmode), on [ResultTree.data](ResultTree.md#attr-resulttreedata).

If you create a standalone [Tree](Tree.md#class-tree) or [ResultTree](ResultTree.md#class-resulttree) as the TreeGrid's [data](#attr-treegriddata) then you may equivalently specify this initial set of tree nodes in that tree's [data](Tree.md#attr-treedata) property.

### See Also

- [TreeNode](../reference_2.md#object-treenode)
- [Tree.data](Tree.md#attr-treedata)
- [ResultTree.data](ResultTree.md#attr-resulttreedata)

**Flags**: IRA

---
## Attr: TreeGrid.showRoot

### Description
Specifies whether the root node should be displayed in the treeGrid.

This property is only available for "children" modelType trees, hence is not allowed for trees that load data from the server dynamically via [TreeGrid.fetchData](#method-treegridfetchdata).

To get the equivalent of a visible "root" node in a tree that loads data dynamically, add a singular, top-level parent to the data. However, note that this top-level parent will technically be the only child of root, and the implicit root object will be returned by [this.data.getRoot()](Tree.md#method-treegetroot).

### Groups

- treeField

**Flags**: IR

---
## Attr: TreeGrid.showDisabledSelectionCheckbox

### Description
Should tree nodes show a disabled checkbox [selectionAppearance](ListGrid_1.md#attr-listgridselectionappearance):"checkbox" is set on the treegrid, and a node can't be selected?

If set to `false` the treeGrid will use [TreeGrid.leaveSelectionCheckboxGap](#attr-treegridleaveselectioncheckboxgap) to determine whether to leave a blank space where the checkbox would normally appear.

### Groups

- treeIcons

### See Also

- [ListGrid.recordCanSelectProperty](ListGrid_1.md#attr-listgridrecordcanselectproperty)

**Flags**: IR

---
## Attr: TreeGrid.selectionProperty

### Description
If specified, the selection object for this list will use this property to mark records as selected. In other words, if this attribute were set to `"isSelected"` any records in the listGrid data where `"isSelected"` is `true` will show up as selected in the grid. Similarly if records are selected within the grid after the grid has been created, this property will be set to true on the selected records.

### Groups

- selection
- appearance

**Flags**: IRA

---
## Attr: TreeGrid.keepParentsOnFilter

### Description
If set, tree-based filtering is performed such that parent nodes are kept as long as they have children that match the filter criteria, even if the parents themselves do not match the filter criteria. If not set, filtering will exclude parent nodes not matching the criteria, and all nodes below them in the tree.

ResultTrees will default to [fetchMode:"local"](../reference_2.md#type-fetchmode) whenever `keepParentsOnFilter` is true, unless fetchMode was explicitly set to "paged" (see below). This allows the filtering logic to fetch a complete tree of nodes from the DataSource (or if loadDataOnDemand:true, a complete set of nodes under a given parent) and then filter the resulting data locally on the client.

This means that the server does not need to implement special tree filtering logic to support looking up nodes that match the specified criteria as well as ancestor nodes that may not.

If some criteria _must_ be sent to the server in order to produce a valid tree of data, but `keepParentsOnFilter` is also required, the [ResultTree.serverFilterFields](ResultTree.md#attr-resulttreeserverfilterfields) attribute may be used to specify a list of field names that will be sent to the server whenever they are present in the criteria. Note that for the subset of criteria applied to these fields, `keepParentsInFilter` behavior will not occur without custom logic in the DataSource fetch operation.

If [FetchMode](../reference_2.md#type-fetchmode) is explicitly set to `"paged"`, it is not possible to implement `keepParentsOnFilter` by local filtering. Support for `keepParentsOnFilter` for a paged ResultTree therefore also requires custom logic in the DataSource fetch operation. To support this a developer must ensure that their fetch operation returns the appropriate set of nodes - all nodes that match the specified criteria plus their ancestor nodes even if they do not match the specified criteria.

### Groups

- treeDataBinding

**Flags**: IR

---
## Attr: TreeGrid.canSelectAll

### Description
This property is not supported on TreeGrid, and only applies to the [ListGrid](ListGrid_1.md#class-listgrid) superclass.

### Groups

- selection

**Flags**: IRW

---
## Attr: TreeGrid.openerIconHeight

### Description
Height in pixels of the opener icons, that is, the icons which show the open or closed state of the node, typically a \[+\] or \[-\] symbol.

If not specified, [TreeGrid.openerIconSize](#attr-treegridopenericonsize) is used instead.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.customIconSelectedProperty

### Description
This property allows the developer to rename the [default node.showSelectedIcon](TreeNode.md#attr-treenodeshowselectedicon) property.

### Groups

- treeIcons

### See Also

- [TreeGrid.customIconProperty](#attr-treegridcustomiconproperty)
- [TreeGrid.showCustomIconSelected](#attr-treegridshowcustomiconselected)

**Flags**: IRWA

---
## Attr: TreeGrid.treeFieldTitle

### Description
Visible title for the tree column (field).

### Groups

- treeField

**Flags**: IR

---
## Attr: TreeGrid.iconBaseStyle

### Description
The base CSS class to apply to icons used in this grid. Used to affect the colors of SVG graphics.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.treeRootValue

### Description
For databound trees, use this attribute to supply a [DataSourceField.rootValue](DataSourceField.md#attr-datasourcefieldrootvalue) for this component's generated data object.

This property allows you to have a particular component navigate a tree starting from any given node as the root.

This setting is invalid if [TreeGrid.keepParentsOnFilter](#attr-treegridkeepparentsonfilter) is set and [fetch-mode](#attr-treegriddatafetchmode) is set to anything other than ["paged"](../reference_2.md#type-fetchmode) - a root-value cannot be used in this case because there is no efficient way to load a subtree to include all parents. If `fetchMode` is specifically set to "paged", the [keepParentsOnFilter](DSRequest.md#attr-dsrequestkeepparentsonfilter) flag is set on the request so the server knows to use special filtering rules, but these rules are not built-in - the developer is responsible for this logic.

### Groups

- databinding

**Flags**: IRA

---
## Attr: TreeGrid.autoAssignTreeField

### Description
If this grid was passed an explicit set of fields, but no field was specified as the "tree-field" (showing indentations for tree hierarchy and tree icons), should we assign one of the other fields to be the tree-field?

When true, if we're showing a field for the [Tree.titleProperty](Tree.md#attr-treetitleproperty) of the tree, this will be displayed as a Tree Field by default. If not, the first entry in the specified fields array will be used.

This may be set to false to display a tree or partial tree as a flattened list within a TreeGrid.

### Groups

- treeField

**Flags**: IR

---
## Attr: TreeGrid.dataFetchMode

### Description
Mode of fetching records from server.

fetchMode:"local" implies that local filtering will always be performed. See [TreeGrid.keepParentsOnFilter](#attr-treegridkeepparentsonfilter) for additional filtering details.

fetchMode:"basic" or "paged" implies that if search criteria change, the entire tree will be discarded and re-fetched from the server. When retrieving the replacement tree data, the default behavior will be to preserve the [openState](#method-treegridgetopenstate) for any nodes that the server returns which were previously opened by the user. Note that this implies that if [TreeGrid.loadDataOnDemand](#attr-treegridloaddataondemand) is enabled and the server returns only root-level nodes, open state will be preserved only for root-level nodes, and children of open root-level nodes will be immediately fetched from the server if they are not included in the server's initial response.

fetchMode:"paged" enables paging for nodes that have very large numbers of children. Whenever the children of a folder are loaded, the `resultTree` will set [DSRequest.startRow](DSRequest.md#attr-dsrequeststartrow) and [endRow](DSRequest.md#attr-dsrequestendrow) when requesting children from the DataSource, and will manage loading of further children on demand, similar to how a [ResultSet](ResultSet.md#class-resultset) manages paging for lists. For a deeper discussion see the **Paging large sets of children** section of the [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) overview.

### Groups

- treeDataBinding

### See Also

- [ResultTree.loadDataOnDemand](ResultTree.md#attr-resulttreeloaddataondemand)
- [ResultTree.useSimpleCriteriaLOD](ResultTree.md#attr-resulttreeusesimplecriterialod)

**Flags**: IR

---
## Attr: TreeGrid.connectorImage

### Description
The base filename or [stateful image block](../reference.md#object-scstatefulimgconfig) for the connector icons shown when [TreeGrid.showConnectors](#attr-treegridshowconnectors) is true. Connector icons are rendered into the title field of each row and show the dotted hierarchy lines between siblings of the same parent node. For each node, a connector icon may be shown:

*   As an opener icon for folder nodes, next to the folder icon
*   In place of an opener icon for leaf nodes, next to the leaf icon
*   As a standalone vertical continuation line in the indent to the left of the node, to show a connection between some ancestor node's siblings (only relevant if [TreeGrid.showFullConnectors](#attr-treegridshowfullconnectors) is true).

Note that [TreeGrid.showFullConnectors](#attr-treegridshowfullconnectors) governs whether connector lines will be displayed for all indent levels, or just for the innermost level of the tree.

**When set to an [SCImgURL](../reference.md#type-scimgurl):** the stateful filenames for these icons are assembled from this base filename and the state of the node. Assuming the connectorImage is set to `{baseName}.{extension}`, the full set of images to be displayed will be:

`{baseName}_ancestor[_rtl].{extension}` if [TreeGrid.showFullConnectors](#attr-treegridshowfullconnectors) is true, this is the URL for the vertical continuation image to be displayed at the appropriate indent levels for ancestor nodes with subsequent children.

For nodes with no children:

*   `{baseName}_single[_rtl].{extension}`: Shown when there is no connector line attached to the parent or previous sibling, and no connector line to the next sibling. For [showFullConnectors:true](#attr-treegridshowfullconnectors) trees, there will always be a connector leading to the parent or previous sibling if its present in the tree so this icon can only be displayed for the first row.
*   `{baseName}_start[_rtl].{extension}`: Shown when the there is no connector line attached to the parent or previous sibling, but there is a connector to the next sibling. As with `_single` this will only ever be used for the first row if [TreeGrid.showFullConnectors](#attr-treegridshowfullconnectors) is true
*   `{baseName}_end[_rtl].{extension}`: Shown if we are not showing a connector line attached to the next sibling of this node (but are showing a connection to the previous sibling or parent).
*   `{baseName}_middle[_rtl].{extension}`: Shown where the we have a connector line leading to both the previous sibling (or parent) and the next sibling.

For folders with children. Note that if [TreeGrid.showFullConnectors](#attr-treegridshowfullconnectors) is false, open folders will never show a connector to subsequent siblings:

*   `{baseName}_opened_single[_rtl].{extension}` opened folder node with children when no connector line is shown attaching to either the folder's previous sibling or parent, or to any subsequent siblings.
*   `{baseName}_opened_start[_rtl].{extension}`: opened folder with children when the there is no connector line attached to the parent or previous sibling, but there is a connector to the next sibling.
*   `{baseName}_opened_end[_rtl].{extension}`: opened folder with children if we are not showing a connector line attached to the next sibling of this node (but are showing a connection to the previous sibling or parent).
*   `{baseName}_opened_middle[_rtl].{extension}`: opened folder with children where the we have a connector line leading to both the previous sibling (or parent) and the next sibling.

*   `{baseName}_closed_single[_rtl].{extension}` closed folder node with children when no connector line is shown attaching to either the folder's previous sibling or parent, or to any subsequent siblings.
*   `{baseName}_closed_start[_rtl].{extension}`: closed folder with children when the there is no connector line attached to the parent or previous sibling, but there is a connector to the next sibling.
*   `{baseName}_closed_end[_rtl].{extension}`: closed folder with children if we are not showing a connector line attached to the next sibling of this node (but are showing a connection to the previous sibling or parent).
*   `{baseName}_closed_middle[_rtl].{extension}`: closed folder with children where the we have a connector line leading to both the previous sibling (or parent) and the next sibling.

(Note '\[\_rtl\]' means that "\_rtl" will be attached if isRTL() is true for this widget).

If [TreeGrid.showSelectedOpener](#attr-treegridshowselectedopener) is true the URL for selected nodes will append the string `"_selected"` to the image URLs described above. So for a connectorImage set to `{baseName}.{extension}`, the URLs for selected records would be `{baseName}_ancestor[_rtl]_selected.{extension}`, `{baseName}_single[_rtl]_selected.{extension}`, etc.

**When set to an _SCStatefulImgConfig:_** _it should contain entries for the default _\_base_ state, as well as the custom states listed above. These entries may be set to any combination of supported src strings, including file-paths and sprite-strings._

### Groups

- treeIcons

**Flags**: IR

---
## Attr: TreeGrid.showCustomIconDrop

### Description
Should folder nodes showing custom icons (set via the [TreeGrid.customIconProperty](#attr-treegridcustomiconproperty), default [TreeNode.icon](TreeNode.md#attr-treenodeicon)), show drop state images when the user is drop-hovering over the folder. If true, the [TreeGrid.dropIconSuffix](#attr-treegriddropiconsuffix) will be appended to the image URL (so `"customFolder.gif"` might be replaced with `"customFolder_drop.gif"`).  
Can be overridden at the node level via the default property [TreeNode.showDropIcon](TreeNode.md#attr-treenodeshowdropicon) and that property can be renamed via [TreeGrid.customIconDropProperty](#attr-treegridcustomicondropproperty).

### Groups

- treeIcons

**Flags**: IRWA

---
## Attr: TreeGrid.showNodeIcons

### Description
Should nodes in this TreeGrid show folder / leaf node icons by default?

May be overridden for folder nodes via [TreeGrid.showFolderIcons](#attr-treegridshowfoldericons)

See [TreeGrid.getIcon](#method-treegridgeticon) for more details on treeGrid icons

**Flags**: IRW

---
## Attr: TreeGrid.recordDropAppearance

### Description
If [TreeGrid.canAcceptDroppedRecords](#attr-treegridcanacceptdroppedrecords) is true for this treeGrid, this property governs whether the user can drop between, or over records within the grid. This controls what [RecordDropPosition](../reference.md#type-recorddropposition) is passed to the [TreeGrid.recordDrop](#method-treegridrecorddrop) event handler.

**Flags**: IRW

---
## Attr: TreeGrid.canReparentNodes

### Description
If set this property allows the user to reparent nodes by dragging them from their current folder to a new folder.  
**Backcompat:** For backwards compatibility with versions prior to SmartClient 1.5, if this property is unset, but `this.canAcceptDroppedRecords` is true, we allow nodes to be dragged to different folders.

### Groups

- treeGridDrop

### See Also

- [TreeNode.canDrag](TreeNode.md#attr-treenodecandrag)
- [TreeNode.canAcceptDrop](TreeNode.md#attr-treenodecanacceptdrop)

**Flags**: IRW

---
## Attr: TreeGrid.customIconProperty

### Description
This property allows the developer to rename the [default node.icon](TreeNode.md#attr-treenodeicon) property.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.cascadeSelection

### Description
Should children be selected when parent is selected? And should parent be selected when any child is selected?

**Flags**: IR

---
## Attr: TreeGrid.animateFolderSpeed

### Description
When animating folder opening / closing, this property designates the speed of the animation in pixels shown (or hidden) per second. Takes precedence over the [TreeGrid.animateFolderTime](#attr-treegridanimatefoldertime) property, which allows the developer to specify a duration for the animation rather than a speed.

### Groups

- animation

### See Also

- [TreeGrid.animateFolderTime](#attr-treegridanimatefoldertime)

**Flags**: IRW

---
## Attr: TreeGrid.showCustomIconSelected

### Description
Should folder nodes showing custom icons (set via the [TreeGrid.customIconProperty](#attr-treegridcustomiconproperty)), show selected state images when the folder is selected, if [TreeGrid.showSelectedIcons](#attr-treegridshowselectedicons) is true?

If true, the [TreeGrid.selectedIconSuffix](#attr-treegridselectediconsuffix) will be appended to the image URL (so `"customFolder.gif"` might be replaced with `"customFolder_selected.gif"`).  
Can be overridden at the node level via the default property [TreeNode.showSelectedIcon](TreeNode.md#attr-treenodeshowselectedicon) and that property can be renamed via [TreeGrid.customIconSelectedProperty](#attr-treegridcustomiconselectedproperty).

### Groups

- treeIcons

**Flags**: IRWA

---
## Attr: TreeGrid.leaveSelectionCheckboxGap

### Description
If [selectionAppearance](ListGrid_1.md#attr-listgridselectionappearance):"checkbox" is set on the treegrid, and a node can't be selected, should a gap be left where the checkbox icon would normally appear, in order to make the node's icon and title line up with the content for other nodes in the same parent?

Has no effect if [TreeGrid.showDisabledSelectionCheckbox](#attr-treegridshowdisabledselectioncheckbox) is `true`

### Groups

- treeIcons

### See Also

- [ListGrid.recordCanSelectProperty](ListGrid_1.md#attr-listgridrecordcanselectproperty)

**Flags**: IR

---
## Attr: TreeGrid.animateFolderMaxRows

### Description
If [TreeGrid.animateFolders](#attr-treegridanimatefolders) is true for this grid, this number can be set to designate the maximum number of rows to animate at a time when opening / closing a folder.

### Groups

- animation

### See Also

- [TreeGrid.getAnimateFolderMaxRows](#method-treegridgetanimatefoldermaxrows)

**Flags**: IRW

---
## Attr: TreeGrid.canDragRecordsOut

### Description
Indicates whether records can be dragged from this listGrid and dropped elsewhere.

**NOTE:** If `canDragRecordsOut` is initially enabled or might be dynamically enabled after the grid is created, it may be desirable to disable [touch scrolling](Canvas.md#attr-canvasusetouchscrolling) so that touch-dragging a record starts a drag operation rather than a scroll, but see the discussion of [drag handles](ListGrid_2.md#method-listgridshowdraghandles). If [Canvas.disableTouchScrollingForDrag](Canvas.md#attr-canvasdisabletouchscrollingfordrag) is set to `true`, then touch scrolling will be disabled automatically. However, for [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) reasons, it is recommended to leave touch scrolling enabled and provide an alternative set of controls that can be used to perform drag and drop of records out of the grid.

### Groups

- treeGridDrop

### See Also

- [TreeNode.canDrag](TreeNode.md#attr-treenodecandrag)
- [TreeNode.canAcceptDrop](TreeNode.md#attr-treenodecanacceptdrop)
- [ListGrid.showDragHandles](ListGrid_2.md#method-listgridshowdraghandles)

**Flags**: IRW

---
## Attr: TreeGrid.autoPreserveOpenState

### Description
For dataBound treeGrids this specifies the [ResultTree.autoPreserveOpenState](ResultTree.md#attr-resulttreeautopreserveopenstate), governing whether the open state of the tree should be preserved when new data arrives due to cache invalidation.

**Flags**: IR

---
## Attr: TreeGrid.cantDragIntoSelfMessage

### Description
Message displayed when user attempts to drop a dragged node onto itself.

### Groups

- i18nMessages

### See Also

- [TreeGrid.canDragRecordsOut](#attr-treegridcandragrecordsout)
- [TreeGrid.canAcceptDroppedRecords](#attr-treegridcanacceptdroppedrecords)
- [TreeGrid.canReorderRecords](#attr-treegridcanreorderrecords)

**Flags**: IR

---
## Attr: TreeGrid.loadingIcon

### Description
If [TreeGrid.showLoadingIcons](#attr-treegridshowloadingicons) is set, this icon will be used when the folder is [loading children from the server](Tree.md#method-treegetloadstate).

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.separateFolders

### Description
If specified, this attribute will override [Tree.separateFolders](Tree.md#attr-treeseparatefolders) on the data for this treeGrid.

Specifies whether folders and leaves should be segregated in the treeGrid display. Use [Tree.sortFoldersBeforeLeaves](Tree.md#attr-treesortfoldersbeforeleaves) to customize whether folders appear before or after their sibling leaves.

If unset, at the treeGrid level, the property can be set directly on [the tree data object](#attr-treegriddata) or for dataBound TreeGrids on the [TreeGrid.dataProperties](#attr-treegriddataproperties).

### Groups

- treeField

**Flags**: IR

---
## Attr: TreeGrid.nodeIcon

### Description
The filename of the default icon for all leaf nodes in this grid. To specify a custom image for an individual node, set the [TreeGrid.customIconProperty](#attr-treegridcustomiconproperty) directly on the node.

See [TreeGrid.showNodeIcons](#attr-treegridshownodeicons) and [TreeGrid.showFolderIcons](#attr-treegridshowfoldericons) for details on suppressing display of icons

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.canDropOnLeaves

### Description
Whether drops are allowed on leaf nodes.

Dropping is ordinarily not allowed on leaf nodes unless [TreeGrid.canReorderRecords](#attr-treegridcanreorderrecords) is set.

The default action for a drop on a leaf node is to place the node in that leaf's parent folder. This can be customized by overriding [TreeGrid.folderDrop](#method-treegridfolderdrop).

Note that enabling `canDropOnLeaves` is usually only appropriate where you intend to add a custom [TreeGrid.folderDrop](#method-treegridfolderdrop) implementation that **does not** add a child node under the leaf. If you want to add a child nodes to a leaf, instead of enabling canDropOnLeaves, use empty folders instead - see [Tree.isFolder](Tree.md#method-treeisfolder) for how to control whether a node is considered a folder.

### Groups

- treeGridDrop

**Flags**: IRWA

---
## Attr: TreeGrid.indentRecordComponents

### Description
For record components placed "within" the [treeField](TreeGridField.md#attr-treegridfieldtreefield) column, should the component be indented to the position where a title would normally show?

For more general placement of embedded components, see [addEmbeddedComponent](ListGrid_2.md#method-listgridaddembeddedcomponent).

**Flags**: IRW

---
## Attr: TreeGrid.autoFetchTextMatchStyle

### Description
With [TreeGrid.loadDataOnDemand](#attr-treegridloaddataondemand):true, TreeGrids fetch data by selecting the child nodes of each parent, which should be exact match, so we default to `autoFetchTextMatchStyle:"exact"` when autoFetchData is true.

See [ListGrid.autoFetchTextMatchStyle](ListGrid_1.md#attr-listgridautofetchtextmatchstyle) for details.

### Groups

- databinding

### See Also

- [ResultTree.useSimpleCriteriaLOD](ResultTree.md#attr-resulttreeusesimplecriterialod)

**Flags**: IR

---
## Attr: TreeGrid.iconPaddingProperty

### Description
This property allows the developer to specify custom [TreeGrid.iconPadding](#attr-treegridiconpadding) for specific nodes

### Groups

- treeIcons

**Flags**: IR

---
## Attr: TreeGrid.animateFolderTime

### Description
When animating folder opening / closing, if [TreeGrid.animateFolderSpeed](#attr-treegridanimatefolderspeed) is not set, this property designates the duration of the animation in ms.

### Groups

- animation

### See Also

- [TreeGrid.animateFolderSpeed](#attr-treegridanimatefolderspeed)

**Flags**: IRW

---
## Attr: TreeGrid.serverFilterFields

### Description
For [fetchMode:"local"](../reference_2.md#type-fetchmode) ResultTrees, this property lists field names that will be sent to the server if they are present in the criteria.

This property may be used to ensure a dataSource receives the necessary criteria to populate a ResultTree's data, and also support [TreeGrid.keepParentsOnFilter](#attr-treegridkeepparentsonfilter).

Note that for some AdvancedCriteria it will not be possible to extract the subcriteria that apply to certain fields. See [DataSource.splitCriteria](DataSource.md#method-datasourcesplitcriteria) for details on how serverFilterFields-applicable subcriteria are extracted from the specified criteria for the tree.

**Flags**: IR

---
## Attr: TreeGrid.showDropEndSpace

### Description
When the user drags over the treeGrid body, should the grid show some space under the last node in the grid allowing the user to drop after the last node? The height of this space can be customized via [TreeGrid.dropEndSpace](#attr-treegriddropendspace)

See also [canDropInEmptyArea](ListGrid_1.md#attr-listgridcandropinemptyarea) and [TreeGrid.canDropSiblingAfterLastNode](#attr-treegridcandropsiblingafterlastnode)

### Groups

- treeGridDrop

**Flags**: IRWA

---
## Attr: TreeGrid.data

### Description
A [Tree](Tree.md#class-tree) object containing of nested [TreeNode](../reference_2.md#object-treenode)s to display as rows in this TreeGrid. The `data` property will typically not be explicitly specified for databound TreeGrids, where the data is returned from the server via databound component methods such as `fetchData()`

### Groups

- data

**Flags**: IRW

---
## Attr: TreeGrid.showConnectors

### Description
Should this treeGrid show connector lines illustrating the tree's hierarchy?

For the set of images used to show connectors, see [TreeGrid.connectorImage](#attr-treegridconnectorimage).

**Note**: in order for connector images to be perfectly connected, all styles for cells must have no top or bottom border or padding. If you see small gaps in connector lines, check your CSS files. See the example below for an example of correct configuration, including example CSS.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.sortFoldersBeforeLeaves

### Description
If specified, this attribute will override [Tree.sortFoldersBeforeLeaves](Tree.md#attr-treesortfoldersbeforeleaves) on the data for this treeGrid.

Specifies whether when [Tree.separateFolders](Tree.md#attr-treeseparatefolders) is true, folders should be displayed before or after their sibling leaves in a sorted tree. If set to true, with sortDirection set to Array.ASCENDING, folders are displayed before their sibling leaves and with sort direction set to Array.DESCENDING they are displayed after. To invert this behavior, set this property to false.

### Groups

- treeField

### See Also

- [TreeGrid.separateFolders](#attr-treegridseparatefolders)

**Flags**: IR

---
## Attr: TreeGrid.showLoadingIcons

### Description
If set, when a folder is loading its children from the server ([Tree.getLoadState](Tree.md#method-treegetloadstate) returns "loading"), it uses a distinct icon image given by [TreeGrid.loadingIcon](#attr-treegridloadingicon). This is typically used to show a small animating "spinner" icon to let the user know data is being fetched.

### Groups

- treeIcons

**Flags**: IR

---
## Attr: TreeGrid.autoOpenTree

### Description
Which nodes should be opened automatically. This applies directly to [ResultTree.autoOpen](ResultTree.md#attr-resulttreeautoopen).

**Flags**: IR

---
## Attr: TreeGrid.openIconPadding

### Description
Default padding to show between the [openIcon](#attr-treegridshowopenicons) and the extra or folder icon in the tree cell.

**Flags**: IR

---
## Attr: TreeGrid.showOpener

### Description
Should the opener icon be displayed next to folder nodes? This is an icon which visually indicates whether the folder is opened or closed (typically via a \[+\] or \[-\] image, or a turn-down arrow) and may be clicked to expand or collapse the folder.

For folders with no children, this icon is not shown unless [TreeGrid.alwaysShowOpener](#attr-treegridalwaysshowopener) is `true`. Note that for trees which [load data on demand](#attr-treegridloaddataondemand), we may not know if a folder has any descendants if it has never been opened. As such we will show the opener icon next to the folder. Once the user opens the icon and a fetch occurs, if the folder is empty, and [TreeGrid.alwaysShowOpener](#attr-treegridalwaysshowopener) is false, the opener icon will be hidden.

For more information on load on demand trees, and how we determine whether a node is a a folder or a leaf, please refer to the [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) documentation.

The opener icon URL is derived from the specified [TreeGrid.openerImage](#attr-treegridopenerimage) or [TreeGrid.connectorImage](#attr-treegridconnectorimage) depending on [TreeGrid.showConnectors](#attr-treegridshowconnectors). If [TreeGrid.showSelectedOpener](#attr-treegridshowselectedopener) is specified a separate opener icon will be displayed for selected nodes.

**Flags**: IRW

---
## Attr: TreeGrid.dragDataAction

### Description
Specifies what to do with data dragged from this TreeGrid (into another component, or another node in this TreeGrid. The default action is to move the data. A setting of "none" is not recommended for trees because Trees maintain the node open state on the nodes themselves, and hence having multiple Tree objects share a reference to a node can have unintended consequences (such as opening a folder in one tree also triggering an open in another tree that shares the same node).

See [TreeGrid.folderDrop](#method-treegridfolderdrop) for a full explanation of default behaviors on drop, and how to customize them.

### Groups

- treeGridDrop

### See Also

- [sharingNodes](../kb_topics/sharingNodes.md#kb-topic-sharing-nodes)

**Flags**: IRWA

---
## Attr: TreeGrid.openerIconWidth

### Description
Width in pixels of the opener icons, that is, the icons which show the open or closed state of the node, typically a \[+\] or \[-\] symbol.

If not specified, [TreeGrid.openerIconSize](#attr-treegridopenericonsize) is used instead.

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.canDropSiblingAfterLastNode

### Description
When performing a drag and drop to add or move data within the tree, should users be able to make the dropped node a sibling of the last node in the tree by dropping just below it?

When set to true, if a user performs a drop action in the space immediately below the last node, (less than half the grid's specified cellHeight away), the dropped data will be added to the parent of that last node, making them siblings. If the parent [will not accept drops](TreeNode.md#attr-treenodecanacceptdrop), the dropped data will be added to the first ancestor that will accept a drop.

If the user performs the drop lower down in the empty area below the last row, of if this property is set to `false`, the dropped data will be added as a last child to the root node instead.

**Flags**: IRWA

---
## Attr: TreeGrid.dropIconSuffix

### Description
If [TreeGrid.showDropIcons](#attr-treegridshowdropicons) is true, this suffix will be appended to the [TreeGrid.folderIcon](#attr-treegridfoldericon) when the user drop-hovers over some folder.

### Groups

- treeIcons

**Flags**: IR

---
## Attr: TreeGrid.showSelectedOpener

### Description
If [TreeGrid.showOpener](#attr-treegridshowopener) is true, should a different opener icon be displayed for selected nodes? This provides a way for developers to show a "selected" version of the opener icon set which looks optimal with the [selected appearance](../kb_topics/cellStyleSuffixes.md#kb-topic-cellstylesuffixes) applied the selected record.

The selected icon URL is created by appending the suffix `"_selected"` to the [TreeGrid.openerImage](#attr-treegridopenerimage) or [TreeGrid.connectorImage](#attr-treegridconnectorimage).

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.showDropIcons

### Description
If true, when the user drags a droppable target over a folder in this TreeGrid, show a different folder icon. This is achieved by appending the [TreeGrid.dropIconSuffix](#attr-treegriddropiconsuffix) onto the [TreeGrid.folderIcon](#attr-treegridfoldericon) URL (for example `"[SKIN]/folder.gif"` may be replaced by `"[SKIN]/folder_drop.gif"`).

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.alwaysShowOpener

### Description
If [TreeGrid.showOpener](#attr-treegridshowopener) is true, should we display the opener icon for folders even if they have no children?

Note that for trees which [load data on demand](#attr-treegridloaddataondemand), we may not know if a folder has any descendants if it has never been opened. As such we will show the opener icon next to the folder. Once the user opens the icon and a fetch occurs, if the folder is empty, and this property is false, the opener icon will be hidden.

For more information on load on demand trees, and how we determine whether a node is a a folder or a leaf, please refer to the [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) documentation.

**Flags**: IRW

---
## Attr: TreeGrid.dropEndSpace

### Description
If [TreeGrid.showDropEndSpace](#attr-treegridshowdropendspace) is set to true, this property governs how large the space under the last node during drop should be. If unset, the spacer will be sized to be half the specified [cellHeight](ListGrid_1.md#attr-listgridcellheight) for the grid.

**Flags**: IRWA

---
## Attr: TreeGrid.loadDataOnDemand

### Description
For databound treeGrid instances, should the entire tree of data be loaded on initial fetch, or should folders load their children as they are opened.

If unset, calling [TreeGrid.fetchData](#method-treegridfetchdata) will default it to true, otherwise, if a ResultTree is passed to [TreeGrid.setData](#method-treegridsetdata), the [ResultTree.loadDataOnDemand](ResultTree.md#attr-resulttreeloaddataondemand) setting is respected. Must be enabled on the underlying [ResultTree](ResultTree.md#class-resulttree) when using [TreeGrid.dataFetchMode](#attr-treegriddatafetchmode): "paged".

Note that when using `loadDataOnDemand`, every node returned by the server is assumed be a folder which may load further children. See [ResultTree.defaultIsFolder](ResultTree.md#attr-resulttreedefaultisfolder) for how to control this behavior.

### Groups

- databinding

### See Also

- [TreeGrid.dataFetchMode](#attr-treegriddatafetchmode)

**Flags**: IRW

---
## Attr: TreeGrid.showCustomIconOpen

### Description
Should folder nodes showing custom icons (set via the [TreeGrid.customIconProperty](#attr-treegridcustomiconproperty)), show open state images when the folder is opened. If true, the [TreeGrid.openIconSuffix](#attr-treegridopeniconsuffix) will be appended to the image URL (so `"customFolder.gif"` might be replaced with `"customFolder_open.gif"`).  
**Note** that the [TreeGrid.closedIconSuffix](#attr-treegridclosediconsuffix) is never appended to custom folder icons.  
Can be overridden at the node level via the default property [TreeNode.showOpenIcon](TreeNode.md#attr-treenodeshowopenicon) and that property can be renamed via [TreeGrid.customIconOpenProperty](#attr-treegridcustomiconopenproperty).

### Groups

- treeIcons

**Flags**: IRWA

---
## Attr: TreeGrid.openIconSuffix

### Description
If [TreeGrid.showOpenIcons](#attr-treegridshowopenicons) is true, this suffix will be appended to the [TreeGrid.folderIcon](#attr-treegridfoldericon) for open folders in this grid.

### Groups

- treeIcons

**Flags**: IR

---
## Attr: TreeGrid.treeFieldMinWidth

### Description
Default [minimum width](ListGridField.md#attr-listgridfieldminwidth) for the [treeField](TreeGridField.md#attr-treegridfieldtreefield). If unset, the default minimum width will be derived from [minFieldWidth](ListGrid_1.md#attr-listgridminfieldwidth), like any every other field.

**Flags**: IR

---
## Attr: TreeGrid.folderIcon

### Description
The URL of the base icon for all folder nodes in this treeGrid. Note that this URL will have [TreeGrid.openIconSuffix](#attr-treegridopeniconsuffix), [TreeGrid.closedIconSuffix](#attr-treegridclosediconsuffix) or [TreeGrid.dropIconSuffix](#attr-treegriddropiconsuffix) appended to indicate state changes if appropriate - see documentation on [TreeGrid.showOpenIcons](#attr-treegridshowopenicons), [TreeGrid.showSelectedIcons](#attr-treegridshowselectedicons) and [TreeGrid.showDropIcons](#attr-treegridshowdropicons).

See [TreeGrid.showNodeIcons](#attr-treegridshownodeicons) and [TreeGrid.showFolderIcons](#attr-treegridshowfoldericons) for details on suppressing display of icons

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeGrid.animateFolders

### Description
If true, when folders are opened / closed children will be animated into view.

Folder animations are automatically disabled if [ListGrid.autoFitData](ListGrid_1.md#attr-listgridautofitdata) is set to "vertical" or "both", or if [records components](ListGrid_1.md#attr-listgridshowrecordcomponents) are used.

### Groups

- animation

**Flags**: IRW

---
## Attr: TreeGrid.showPartialSelection

### Description
Should partially selected parents be shown with special icon?

**Flags**: IRW

---
## Attr: TreeGrid.fields

### Description
An array of field objects, specifying the order, layout, dynamic calculation, and sorting behavior of each field in the treeGrid object. In TreeGrids, the fields array specifies columns. Each field in the fields array is TreeGridField object.

If [TreeGrid.dataSource](#attr-treegriddatasource) is also set, this value acts as a set of overrides as explained in [DataBoundComponent.fields](DataBoundComponent.md#attr-databoundcomponentfields).

### Groups

- databinding

### See Also

- [TreeGridField](../reference.md#object-treegridfield)

**Flags**: IRW

---
## Attr: TreeGrid.folderIconPadding

### Description
Default padding to show between folder icon and cell value in the tree cell. This property is only consulted for folder nodes. If unset, [TreeGrid.iconPadding](#attr-treegridiconpadding) will be applied to both folder and leaf nodes.

To set the icon padding for individual nodes, use [TreeGrid.iconPaddingProperty](#attr-treegridiconpaddingproperty)

**Flags**: IR

---
## Attr: TreeGrid.dataProperties

### Description
For a `TreeGrid` that uses a DataSource, these properties will be passed to the automatically-created ResultTree. This can be used for various customizations such as modifying the automatically-chosen [Tree.parentIdField](Tree.md#attr-treeparentidfield).

### Groups

- databinding

**Flags**: IR

---
## Attr: TreeGrid.dataSource

### Description
The DataSource that this component should bind to for default fields and for performing [DataSource requests](../reference.md#object-dsrequest).

Can be specified as either a DataSource instance or the String ID of a DataSource.

### Groups

- databinding

**Flags**: IRW

---
## Attr: TreeGrid.saveOpenStateInViewState

### Description
Should the current [open state](#method-treegridgetopenstate) of the tree be included along with other details when saving this grid's [view-state](#method-treegridgetviewstate)?

### Groups

- viewState

**Flags**: IRW

---
## Attr: TreeGrid.indentSize

### Description
The amount of indentation (in pixels) to add to a node's icon/title for each level down in this tree's hierarchy.

This value is ignored when [showConnectors](#attr-treegridshowconnectors) is `true` because fixed-size images are used to render the connectors.

### Groups

- appearance

**Flags**: IRW

---
## Attr: TreeGrid.cantDragIntoChildMessage

### Description
Message displayed when user attempts to drop a node into a child of itself.

### Groups

- i18nMessages

### See Also

- [TreeGrid.canDragRecordsOut](#attr-treegridcandragrecordsout)
- [TreeGrid.canAcceptDroppedRecords](#attr-treegridcanacceptdroppedrecords)
- [TreeGrid.canReorderRecords](#attr-treegridcanreorderrecords)

**Flags**: IR

---
## Attr: TreeGrid.showOpenIcons

### Description
If true, show a different icon for `open` folders than closed folders. This is achieved by appending the [TreeGrid.openIconSuffix](#attr-treegridopeniconsuffix) onto the [TreeGrid.folderIcon](#attr-treegridfoldericon) URL \[for example `"[SKIN]/folder.gif"` might be replaced by `"[SKIN]/folder_open.gif"`.  
**Note** If this property is set to `false` the same icon is shown for open folders as for closed folders, unless a custom folder icon was specified. This will be determined by [TreeGrid.folderIcon](#attr-treegridfoldericon) plus the [TreeGrid.closedIconSuffix](#attr-treegridclosediconsuffix).

### Groups

- treeIcons

**Flags**: IRW

---
## Method: TreeGrid.getDropFolder

### Description
When the user is dragging a droppable element over this grid, this method returns the folder which would contain the item if dropped. This is the current drop node if the user is hovering over a folder, or the node's parent if the user is hovering over a leaf.

### Returns

`[TreeNode](#type-treenode)|[NodeLocator](#type-nodelocator)` — If this is a regular treeGrid, the target drop folder; if this is a treeGrid based on a [multiLink tree](Tree.md#attr-treemultilinktree), a NodeLocator unambiguously identifying the specific occurence of the drop folder in the tree

### Groups

- events

---
## Method: TreeGrid.openFolder

### Description
Opens a folder.

Executed when a folder node receives a 'doubleClick' event. If you override this method, the single parameter passed will be a reference to the relevant folder node in the tree's data.

See the ListGrid Widget Class for inherited recordClick and recordDoubleClick events.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node to open |
| path | [String](#type-string) | true | — | optional parameter containing the full path to the node. This is essential context for a [multi-link tree](Tree.md#attr-treemultilinktree), but is not required in ordinary trees |

### See Also

- [TreeGrid.closeFolder](#method-treegridclosefolder)
- [TreeGrid.folderOpened](#method-treegridfolderopened)
- [ListGrid](ListGrid_1.md#class-listgrid)

**Flags**: A

---
## Method: TreeGrid.getOpenIcon

### Description
Get the appropriate open/close opener icon for a node. Returns null if [TreeGrid.showOpener](#attr-treegridshowopener) is set to false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | tree node in question |

### Returns

`[URL](../reference_2.md#type-url)` — URL for the icon to show the node's open state

**Flags**: A

---
## Method: TreeGrid.isExportingClientData

### Description
Returns true if this component is currently [exporting client data](#method-treegridexportclientdata). This method can be called from custom cell formatters if you need to return a different formatted value for an export than for a live TreeGrid

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if this component is currently exporting client data

### See Also

- [TreeGrid.exportClientData](#method-treegridexportclientdata)

---
## Method: TreeGrid.getViewState

### Description
Overridden to return a [TreeGridViewState](../reference.md#type-treegridviewstate) object for the grid including open state if [TreeGrid.saveOpenStateInViewState](#attr-treegridsaveopenstateinviewstate) is true.

### Returns

`[TreeGridViewState](../reference.md#type-treegridviewstate)` — current view state for the grid.

### Groups

- viewState

### See Also

- [TreeGridViewState](../reference.md#type-treegridviewstate)
- [TreeGrid.setViewState](#method-treegridsetviewstate)

---
## Method: TreeGrid.getCellAlign

### Description
Return the horizontal alignment for cell contents. Default implementation will always left-align the special [TreeGridField.treeField](TreeGridField.md#attr-treegridfieldtreefield) \[or right-align if the page is in RTL mode\] - otherwise will return [ListGridField.cellAlign](ListGridField.md#attr-listgridfieldcellalign) if specified, otherwise [ListGridField.align](ListGridField.md#attr-listgridfieldalign).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [ListGridRecord](#type-listgridrecord) | false | — | this cell's record |
| rowNum | [number](#type-number) | false | — | row number for the cell |
| colNum | [number](#type-number) | false | — | column number of the cell |

### Returns

`[Alignment](../reference_2.md#type-alignment)` — Horizontal alignment of cell contents: 'right', 'center', or 'left'

---
## Method: TreeGrid.recordDoubleClick

### Description
Handle a doubleClick on a tree node - override of ListGrid stringMethod of same name. If the node is a folder, this implementation calls [TreeGrid.toggleFolder](#method-treegridtogglefolder) on it. If the node is a leaf, calls [TreeGrid.openLeaf](#method-treegridopenleaf) on it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TreeGrid](#type-treegrid) | false | — | the treeGrid that contains doubleclick event |
| record | [TreeNode](#type-treenode) | false | — | the record that was double-clicked |
| recordNum | [number](#type-number) | false | — | number of the record clicked on in the current set of displayed records (starts with 0) |
| field | [TreeGridField](#type-treegridfield) | false | — | the field that was clicked on (field definition) |
| fieldNum | [number](#type-number) | false | — | number of the field clicked on in the treeGrid.fields array |
| value | [Object](../reference.md#type-object) | false | — | value of the cell (after valueMap, etc. applied) |
| rawValue | [Object](../reference.md#type-object) | false | — | raw value of the cell (before valueMap, etc applied) |

### Returns

`[boolean](../reference.md#type-boolean)` — false to stop event bubbling

### Groups

- events

### See Also

- [ListGrid.recordDoubleClick](ListGrid_2.md#method-listgridrecorddoubleclick)

---
## Method: TreeGrid.folderContextClick

### Description
This method is called when a context click occurs on a folder record.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TreeGrid](#type-treegrid) | false | — | The TreeGrid on which the contextclick occurred. |
| folder | [TreeNode](#type-treenode) | false | — | The folder (record) on which the contextclick occurred. |
| recordNum | [number](#type-number) | false | — | Index of the row where the contextclick occurred. |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### See Also

- [TreeGrid.nodeContextClick](#method-treegridnodecontextclick)

---
## Method: TreeGrid.transferNodes

### Description
Transfer a list of [TreeNode](../reference_2.md#object-treenode)s within this treeGrid or from from some other component (does not have to be a databound component) into this component. This method is only applicable to list-type components, such as [listGrid](ListGrid_1.md#class-listgrid), [treeGrid](#class-treegrid) or [tileGrid](TileGrid.md#class-tilegrid). Please see the paragraph below for special rules concerning [multi-link trees](Tree.md#method-treeismultilinktree).

This method implements the automatic drag-copy and drag-move behavior and calling it is equivalent to completing a drag and drop of the `nodes` (the default [TreeGrid.folderDrop](#method-treegridfolderdrop) implementation simply calls `transferNodes()`)

Note that this method is asynchronous - it may need to perform server turnarounds to prevent duplicates in the target component's data. If you wish to be notified when the transfer process has completed, you can either pass the optional callback to this method or implement the [DataBoundComponent.dropComplete](DataBoundComponent.md#method-databoundcomponentdropcomplete) method on this component.

For a TreeGrid, see also [transferSelectedData()](#method-treegridtransferselecteddata).

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

- treeGridDrop

**Flags**: A

---
## Method: TreeGrid.toggleFolder

### Description
Opens the folder specified by node if it's closed, and closes it if it's open. TreeGrid will redraw if there's a change in the folder's open/closed state.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[String](#type-string)|[Integer](../reference_2.md#type-integer)|[NodeLocator](#type-nodelocator) | false | — | the node in question, or the the node's ID, or a NodeLocator object |

---
## Method: TreeGrid.leafContextClick

### Description
This method is called when a context click occurs on a leaf record.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TreeGrid](#type-treegrid) | false | — | The TreeGrid on which the contextclick occurred. |
| leaf | [TreeNode](#type-treenode) | false | — | The leaf (record) on which the contextclick occurred. |
| recordNum | [number](#type-number) | false | — | Index of the row where the contextclick occurred. |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### See Also

- [TreeGrid.nodeContextClick](#method-treegridnodecontextclick)

---
## Method: TreeGrid.setSelectedPaths

### Description
Reset this grid's selection to match the [ListGridSelectedState](../reference_2.md#type-listgridselectedstate) object passed in.  
Used to restore previous state retrieved from the grid by a call to [TreeGrid.getSelectedPaths](#method-treegridgetselectedpaths).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| selectedPaths | [ListGridSelectedState](../reference_2.md#type-listgridselectedstate) | false | — | Object describing the desired selection state of the grid |

### Groups

- viewState

### See Also

- [TreeGrid.getSelectedPaths](#method-treegridgetselectedpaths)

---
## Method: TreeGrid.nodeContextClick

### Description
This method is called when a context click occurs on a leaf or folder record. Note that if you set up a callback for `nodeContextClick()` and e.g. [TreeGrid.leafContextClick](#method-treegridleafcontextclick), then both will fire (in that order) if a leaf is contextclicked - unless `nodeContextClick()` returns false, in which case no further contextClick callbacks will be called.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TreeGrid](#type-treegrid) | false | — | The TreeGrid on which the contextclick occurred. |
| node | [TreeNode](#type-treenode) | false | — | The node (record) on which the contextclick occurred. |
| recordNum | [number](#type-number) | false | — | Index of the row where the contextclick occurred. |

### Returns

`[boolean](../reference.md#type-boolean)` — whether to cancel the event

### See Also

- [TreeGrid.folderContextClick](#method-treegridfoldercontextclick)
- [TreeGrid.leafContextClick](#method-treegridleafcontextclick)

---
## Method: TreeGrid.isOverOpenArea

### Description
Returns true if the last event occurred over the indented area or over the open / close icon of a folder node in this TreeGrid. Returns false if the event did not occur over a folder node.

### Returns

`[Boolean](#type-boolean)` — true if the user clicked the open icon

---
## Method: TreeGrid.setViewState

### Description
Overridden to take a [TreeGridViewState](../reference.md#type-treegridviewstate) object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewState | [TreeGridViewState](../reference.md#type-treegridviewstate) | false | — | Object describing the desired view state for the grid |

### Groups

- viewState

### See Also

- [TreeGrid.getViewState](#method-treegridgetviewstate)

---
## Method: TreeGrid.shouldAnimateFolder

### Description
Should this folder be animated when opened / closed? Default implementation will return true if [TreeGrid.animateFolders](#attr-treegridanimatefolders) is true, the folder being actioned has children and the child-count is less than the result of [TreeGrid.getAnimateFolderMaxRows](#method-treegridgetanimatefoldermaxrows).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| folder | [TreeNode](#type-treenode) | false | — | folder being opened or closed. |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if folders should be animated when opened / closed.

### Groups

- animation

---
## Method: TreeGrid.filterData

### Description
Retrieves data that matches the provided criteria and displays the matching data in this component.

This method behaves exactly like [TreeGrid.fetchData](#method-treegridfetchdata) except that [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) is automatically set to "substring" so that String-valued fields are matched by case-insensitive substring comparison.

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
## Method: TreeGrid.leafClick

### Description
This method is called when a leaf record is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TreeGrid](#type-treegrid) | false | — | The TreeGrid on which leafClick() occurred. |
| leaf | [TreeNode](#type-treenode) | false | — | The leaf (record) that was clicked |
| recordNum | [number](#type-number) | false | — | Index of the row where the click occurred. |

### See Also

- [TreeGrid.nodeClick](#method-treegridnodeclick)

---
## Method: TreeGrid.folderClosed

### Description
This method is called when a folder is closed either via the user manipulating the expand/collapse control in the UI or via [TreeGrid.closeFolder](#method-treegridclosefolder). You can return `false` to cancel the close.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | the folder (record) that is being closed |

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel the close, true to all it to proceed

---
## Method: TreeGrid.getDragTrackerIcon

### Description
Return an icon to display as a drag tracker when the user drags some node(s).  
Default implementation:  
If multiple nodes are selected and [TreeGrid.manyItemsImage](#attr-treegridmanyitemsimage) is defined, this image will be returned.  
Otherwise returns the result of [TreeGrid.getIcon](#method-treegridgeticon) for the first node being dragged.

Note: Only called if [ListGrid.dragTrackerMode](ListGrid_1.md#attr-listgriddragtrackermode) is set to `"icon"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| records | [Array of ListGridRecord](#type-array-of-listgridrecord) | false | — | Records being dragged |

### Returns

`[String](#type-string)` — Image URL of icon to display

### Groups

- dragTracker

---
## Method: TreeGrid.recordDrop

### Description
The superclass event [ListGrid.recordDrop](ListGrid_2.md#method-listgridrecorddrop) does not fire on a TreeGrid, use [TreeGrid.folderDrop](#method-treegridfolderdrop) instead.

---
## Method: TreeGrid.getDraggedNodeLocators

### Description
**NOTE:** Applicable only to [multi-link trees](Tree.md#attr-treemultilinktree); if called on a regular `TreeGrid`, returns an empty array.

During a drag-and-drop interaction, this method returns the set of node occurrences being dragged out of the component, wrapped inside [NodeLocator](../reference_2.md#object-nodelocator)s. In the default implementation, this is the list of currently selected node occurrences

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| source | [TreeGrid](#type-treegrid) | false | — | source grid from which the records will be transferred |

### Returns

`[Array of NodeLocator](#type-array-of-nodelocator)` — Array of [NodeLocator](../reference_2.md#object-nodelocator)s unambiguously identifying the node occurrences that are currently selected

### Groups

- dragging
- data

**Flags**: A

---
## Method: TreeGrid.transferDragData

### Description
During a drag-and-drop interaction, this method is called to transfer a set of records that were dropped onto some other component. This method is called after the set of records has been copied to the other component. Whether or not this component's data is modified is determined by the value of [DataBoundComponent.dragDataAction](DataBoundComponent.md#attr-databoundcomponentdragdataaction).

With a `dragDataAction` of "move", a databound component will issue "remove" dsRequests against its DataSource to actually remove the data, via [DataSource.removeData](DataSource.md#method-datasourceremovedata).

### Returns

`[Array](#type-array)` — Array of objects that were dragged out of this ListGrid.

### See Also

- [DataBoundComponent.getDragData](DataBoundComponent.md#method-databoundcomponentgetdragdata)
- [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop)

---
## Method: TreeGrid.getNodeTitle

### Description
Returns the title to show for a node in the tree column. If the field specifies the `name` attribute, then the current `node[field.name]` is returned. Otherwise, the result of calling [Tree.getTitle](Tree.md#method-treegettitle) on the node is called.

You can override this method to return a custom title for node titles in the tree column.

**Note:** if a default tree field is generated for you by [TreeGrid.createDefaultTreeField](#attr-treegridcreatedefaulttreefield) being true, and you've overridden this method, it will be called with `recordNum: -1` during sorting of the tree field, if the tree is [paged](ResultTree.md#attr-resulttreefetchmode).

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
## Method: TreeGrid.willAcceptDrop

### Description
Should this treeGrid process a specific drop event?  
Note: See [treeGridDrop](../kb_topics/treeGridDrop.md#kb-topic-treegrid-drag-and-drop) for an overview of TreeGrid drag and drop behavior.

This method overrides [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop) and works as follows:  
  
First, [ListGrid.willAcceptDrop](ListGrid_2.md#method-listgridwillacceptdrop) (the superclass definition) is consulted. If it returns false, then this method returns false immediately.  
This handles the following cases:  
\- reordering of records withing this TreeGrid when [ListGrid.canReorderRecords](ListGrid_1.md#attr-listgridcanreorderrecords) is true  
\- accepting dropped records from another dragTarget when [ListGrid.canAcceptDroppedRecords](ListGrid_1.md#attr-listgridcanacceptdroppedrecords) is true and the dragTarget gives us a valid set of records to drop into place.  
\- disallowing drop over disabled nodes, or nodes with `canAcceptDrop:false`  
This method will also return false if the drop occurred over a leaf node whos immediate parent has `canAcceptDrop` set to `false`  
If [TreeGrid.canReparentNodes](#attr-treegridcanreparentnodes) is true, and the user is dragging a node from one folder to another, this method will return true to allow the change of parent folder.  
  
  
Otherwise this method returns true.

### Returns

`[boolean](../reference.md#type-boolean)` — true if this component will accept a drop of the dragData

### Groups

- treeGridDrop

**Flags**: A

---
## Method: TreeGrid.rowClick

### Description
This override to [ListGrid.rowClick](ListGrid_2.md#method-listgridrowclick). This implementation calls through to the [TreeGrid.nodeClick](#method-treegridnodeclick), [TreeGrid.folderClick](#method-treegridfolderclick), [TreeGrid.leafClick](#method-treegridleafclick) methods, as appropriate unless the click was on the expand/collapse control of a folder - in which case those callbacks are not fired.

Do not override this method unless you need a rowClick callback that fires even when the user clicks on the expand/collapse control. If you do override this method, be sure to call `return this.Super("rowClick", arguments);` at the end of your override to preserve other handlers that are called from the superclass (for example, [ListGrid.recordClick](ListGrid_2.md#method-listgridrecordclick).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| record | [TreeNode](#type-treenode) | false | — | record that was clicked on |
| recordNum | [number](#type-number) | false | — | index of the row where the click occurred |
| fieldNum | [number](#type-number) | false | — | index of the col where the click occurred |

### Returns

`[boolean](../reference.md#type-boolean)` — false == cancel further event processing

### Groups

- event handling

### See Also

- [TreeGrid.nodeClick](#method-treegridnodeclick)
- [TreeGrid.folderClick](#method-treegridfolderclick)
- [TreeGrid.leafClick](#method-treegridleafclick)
- [ListGrid.recordClick](ListGrid_2.md#method-listgridrecordclick)

---
## Method: TreeGrid.getEventRow

### Description
Returns the row number of the provided Y-coordinate, or the most recent mouse event if a Y-coordinate is not provided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| y | [Integer](../reference_2.md#type-integer) | true | — | Y-coordinate relative to the top edge of the content to obtain the row number for. If not provided, then [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety) will be used. |

### Returns

`[int](../reference.md#type-int)` — row number, or -2 if beyond last drawn row

### Groups

- events

---
## Method: TreeGrid.getAnimateFolderMaxRows

### Description
If [TreeGrid.animateFolders](#attr-treegridanimatefolders) is true for this treeGrid, this method returns the the maximum number of rows to animate at a time when opening / closing a folder. This method will return [TreeGrid.animateFolderMaxRows](#attr-treegridanimatefoldermaxrows) if set. Otherwise the value will be calculated as 3x the number of rows required to fill a viewport, capped at a maximum value of 75.

### Returns

`[Integer](../reference_2.md#type-integer)` — maximum number of rows to be animated when opening or closing folders.

### Groups

- animation

**Flags**: A

---
## Method: TreeGrid.fetchData

### Description
Uses a "fetch" operation on the current [grid.dataSource](DataSource.md#class-datasource) to retrieve data that matches the provided criteria, and displays the matching data in this component as a tree.

This method will create a [ResultTree](ResultTree.md#class-resulttree) to manage tree data, which will subsequently be available as `treeGrid.data`. DataSource records returned by the "fetch" operation are linked into a tree structure according to [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) and [foreignKey](DataSourceField.md#attr-datasourcefieldforeignkey) declarations on DataSource fields. See the [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) topic for complete details.

By default, the created ResultTree will use folder-by-folder load on demand, asking the server for the children of each folder as the user opens it.

The [ResultTree](ResultTree.md#class-resulttree) created by `fetchData()` can be customized by setting [ListGrid.dataProperties](ListGrid_1.md#attr-listgriddataproperties) to an Object containing properties and methods to apply to the created ResultTree. For example, the property that determines whether a node is a folder ([isFolderProperty](Tree.md#attr-treeisfolderproperty)) can be customized, or level-by-level loading can be disabled via [loadDataOnDemand:false](ResultTree.md#attr-resulttreeloaddataondemand).

If [TreeGrid.loadDataOnDemand](#attr-treegridloaddataondemand) is true, this grid will issue fetch requests each time the user opens a folder to load its child data.  
The criteria on this fetch request will consist of the appropriate value for the foreignKey field, combined with the criteria passed to `fetchData()` when the data was first loaded. This allows you to retrieve multiple different tree structures from the same DataSource. However note that the server is expected to always respond with an intact tree - returned nodes which do not have parents are dropped from the dataset and not displayed.

The callback passed to `fetchData` will fire once, the first time that data is loaded from the server. If using folder-by-folder load on demand, use the [ResultTree.dataArrived](ResultTree.md#method-resulttreedataarrived) notification to be notified each time new nodes are loaded.

Note that when calling 'fetchData()', changes to criteria may or may not result in a DSRequest to the server due to client-side filtering (see [ResultTree.fetchMode](ResultTree.md#attr-resulttreefetchmode). You can call willFetchData(criteria) to determine if new criteria will result in a server fetch.

If you need to force data to be re-fetched, you can call invalidateCache() and new data will automatically be fetched from the server using the current criteria and sort direction.  
When using invalidateCache() there is no need to also call fetchData() and in fact this could produce unexpected results.

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
## Method: TreeGrid.exportClientData

### Description
Exports this component's data with client-side formatters applied, so is suitable for direct display to users. See [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata) for details of the general requirements and restrictions when exporting client data.

The following notes apply when exporting client data from TreeGrids:

*   Export only works correctly if you specify [fields](#attr-treegridfields); if you allow it to generate a [default field](#attr-treegridcreatedefaulttreefield), nothing will be exported
*   Only visible nodes are exported; if you close a node, its children are not exported even if they are loaded and known to the client
*   Tree nodes are exported as a flat list, in the same order they are displayed in the TreeGrid

If your TreeGrid has custom formatters, formatted values will be exported by default, with HTML normalized to text where possible. Since some levels of HTML normalizing aren't possible, this may result in missing or incorrect export values. In this case, you have two possible approaches:

*   Set [exportRawValues](ListGridField.md#attr-listgridfieldexportrawvalues) on the field. This will export the raw underlying value of the field; your formatter will not be called
*   Have your formatter call [isExportingClientData()](#method-treegridisexportingclientdata) and perform whatever alternative formatting you require if that method returns true

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | Request properties for the export. Note that specifying [exportData](DSRequest.md#attr-dsrequestexportdata) on the request properties allows the developer to pass in an explicit data set to export. |
| callback | [RPCCallback](#type-rpccallback) | true | — | Optional callback. If you specify [exportToClient](DSRequest.md#attr-dsrequestexporttoclient): false in the request properties, this callback will fire after export completes. Otherwise the callback will fire right before the download request is made to the server. |

### See Also

- [ListGrid.exportClientData](ListGrid_2.md#method-listgridexportclientdata)

---
## Method: TreeGrid.folderOpened

### Description
This method is called when a folder is opened either via the user manipulating the expand/collapse control in the UI or via [TreeGrid.openFolder](#method-treegridopenfolder). You can return `false` to cancel the open.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | the folder (record) that is being opened |
| path | [String](#type-string) | true | — | optional parameter containing the full path to the node. This is essential context for a [multi-link tree](Tree.md#attr-treemultilinktree), but is not required in ordinary trees |

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel the open, true to all it to proceed

---
## Method: TreeGrid.isOverExtraIcon

### Description
Returns true if the last event occurred over [extra icon](#method-treegridgetextraicon) for the current node.

Returns false if the event did not occur over an extraIcon, or if no extraIcon is showing for the node in question.

### Returns

`[Boolean](#type-boolean)` — true if the user clicked the extra icon

---
## Method: TreeGrid.nodeClick

### Description
This method is called when a leaf or folder record is clicked on. Note that if you set up a callback for `nodeClick()` and e.g. [TreeGrid.leafClick](#method-treegridleafclick), then both will fire (in that order) if a leaf is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TreeGrid](#type-treegrid) | false | — | The TreeGrid on which leafClick() occurred. |
| node | [TreeNode](#type-treenode) | false | — | The node (record) that was clicked |
| recordNum | [number](#type-number) | false | — | Index of the row where the click occurred. |

### See Also

- [TreeGrid.folderClick](#method-treegridfolderclick)
- [TreeGrid.leafClick](#method-treegridleafclick)

---
## Method: TreeGrid.getSelectedPaths

### Description
Returns a snapshot of the current selection within this treeGrid as a [ListGridSelectedState](../reference_2.md#type-listgridselectedstate) object.  
This object can be passed to [TreeGrid.setSelectedPaths](#method-treegridsetselectedpaths) to reset this grid's selection the current state (assuming the same data is present in the grid).

### Returns

`[ListGridSelectedState](../reference_2.md#type-listgridselectedstate)` — current state of this grid's selection

### Groups

- viewState

### See Also

- [TreeGrid.setSelectedPaths](#method-treegridsetselectedpaths)

---
## Method: TreeGrid.folderDrop

### Description
Process a drop of one or more nodes on a TreeGrid folder.  
Note: See [treeGridDrop](../kb_topics/treeGridDrop.md#kb-topic-treegrid-drag-and-drop) for an overview of TreeGrid drag and drop behavior.

This method can be overridden to provide custom drop behaviors and is a more appropriate override point than the lower level [Canvas.drop](Canvas.md#method-canvasdrop) handler.

The default behavior is to simply delegate to the [TreeGrid.transferNodes](#method-treegridtransfernodes) method; thus, the correct way to perform a programmatic folder drop, with all the built-in behaviors described below, is to call `transferNodes()`

If this is a self-drop, nodes are simply reordered. An "update" operation will be submitted to update the [parentId](Tree.md#attr-treeparentidfield) field of the moved node(s).

For a drop from another widget, [TreeGrid.transferDragData](#method-treegridtransferdragdata) is called which, depending on the [dragDataAction](#attr-treegriddragdataaction) specified on the source widget, may either remove the source nodes from the original list (`dragDataAction:"move"`) or just provide a copy to this tree (`dragDataAction:"copy"`).

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
| index | [int](../reference.md#type-int) | false | — | Within the folder being dropped on, the index at which the drop is occurring. Only passed if [canReorderRecords](#attr-treegridcanreorderrecords) is true. |
| sourceWidget | [Canvas](#type-canvas) | false | — | The component that is the source of the nodes (where the nodes were dragged from) |

### Groups

- treeGridDrop

### See Also

- [TreeGrid.transferNodes](#method-treegridtransfernodes)

**Flags**: A

---
## Method: TreeGrid.getIcon

### Description
Get the appropriate icon for a node.

By default icons are derived from [TreeGrid.folderIcon](#attr-treegridfoldericon) and [TreeGrid.nodeIcon](#attr-treegridnodeicon). Custom icons for individual nodes can be overridden by setting the [TreeGrid.customIconProperty](#attr-treegridcustomiconproperty) on a node.

To suppress icons altogether, set [showNodeIcons:false](#attr-treegridshownodeicons), or, for folder icons only [showFolderIcons:false](#attr-treegridshowfoldericons).  
You can also provide an override of this method that returns null to suppress icons for specific nodes.

Note that the full icon URL will be derived by applying [Canvas.getImgURL](Canvas.md#method-canvasgetimgurl) to the value returned from this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | tree node in question |
| rowNum | [Integer](../reference_2.md#type-integer) | true | — | the row number of the node in the TreeGrid. This additional context is required for [multi-link trees](Tree.md#attr-treemultilinktree) because the same node can appear in multiple places |

### Returns

`[URL](../reference_2.md#type-url)` — URL for the icon to show for this node

---
## Method: TreeGrid.closeFolder

### Description
Closes a folder.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node to close |

### See Also

- [TreeGrid.openFolder](#method-treegridopenfolder)
- [TreeGrid.folderClosed](#method-treegridfolderclosed)

---
## Method: TreeGrid.dataArrived

### Description
Notification method fired whenever this TreeGrid receives new data nodes from the dataSource. Only applies to databound TreeGrids where [TreeGrid.data](#attr-treegriddata) is a [ResultTree](ResultTree.md#class-resulttree) - either explicitly created and applied via [TreeGrid.setData](#method-treegridsetdata) or automatically generated via a [fetchData()](#method-treegridfetchdata) call.

Note that `dataArrived()`, unlike [TreeGrid.dataChanged](#method-treegriddatachanged), only fires in limited circumstances - when data for a [ResultTree](ResultTree.md#class-resulttree) arrives from the server due to a fetch or cache invalidation, or as a result of filtering. If you want to catch all data changes, you should instead react to [TreeGrid.dataChanged](#method-treegriddatachanged).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| parentNode | [TreeNode](#type-treenode) | false | — | The parentNode for which children were just loaded |

### See Also

- [TreeGrid.dataChanged](#method-treegriddatachanged)

---
## Method: TreeGrid.dataChanged

### Description
Notification method fired when the TreeGrid's data changes, for any reason. If overridden (rather than [observed](Class.md#method-classobserve)), you must [call the\\n superclass implementation](Class.md#method-classsuper) to ensure proper Framework behavior.

Examples of why data changed might be:

*   a call to [addData()](ListGrid_2.md#method-listgridadddata), [updateData()](ListGrid_2.md#method-listgridupdatedata), or [removeData()](ListGrid_2.md#method-listgridremovedata)
*   [DataSource](DataSource.md#class-datasource) updates from the server for [ResultTree](ResultTree.md#class-resulttree) data (triggered by record editing, etc.)
*   fetches arriving back from the server for [ResultTree](ResultTree.md#class-resulttree) data
*   programmatic changes to [Tree](Tree.md#class-tree) data if made through APIs such as [Tree.add](Tree.md#method-treeadd), [Tree.remove](Tree.md#method-treeremove), etc.
*   cache invalidation
*   filtering

Calling [TreeGrid.setData](#method-treegridsetdata) doesn't call this notification directly, but it may fire if one of the above listed events is triggered (e.g. a server fetch for [ResultTree](ResultTree.md#class-resulttree) data).

Note that the `operationType` parameter is optional and will be passed and contain the operation (e.g. "update") if this notification was triggered by a fetch, an [addData()](ListGrid_2.md#method-listgridadddata), [updateData()](ListGrid_2.md#method-listgridupdatedata), or [removeData()](ListGrid_2.md#method-listgridremovedata), or a [DataSource](DataSource.md#class-datasource) update for [ResultTree](ResultTree.md#class-resulttree) data (the first three reasons listed above) but otherwise will be undefined.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| operationType | [String](#type-string) | true | — | optionally passed operation causing the change |

### See Also

- [TreeGrid.dataArrived](#method-treegriddataarrived)

**Flags**: A

---
## Method: TreeGrid.loadAllRecords

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
## Method: TreeGrid.getExtraIcon

### Description
Get an additional icon to show between the open icon and folder/node icon for a particular node.

NOTE: If [ListGrid.selectionAppearance](ListGrid_1.md#attr-listgridselectionappearance) is `"checkbox"`, this method will NOT be called. Extra icons cannot be shown for that appearance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | tree node in question |

### Returns

`[URL](../reference_2.md#type-url)` — URL for the extra icon (null if none required)

**Flags**: A

---
## Method: TreeGrid.setData

### Description
Set the [Tree](Tree.md#class-tree) object this TreeGrid will view and manipulate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newData | [Tree](#type-tree) | false | — | Tree to show |

---
## Method: TreeGrid.groupBy

### Description
Not applicable to TreeGrids, as the [TreeGrid.data](#attr-treegriddata) already represents a tree.

### Groups

- grouping

### See Also

- [TreeGrid.groupByField](#attr-treegridgroupbyfield)

---
## Method: TreeGrid.setOpenState

### Description
Reset this set of open folders within this grid's data to match the [TreeGridOpenState](../reference_2.md#type-treegridopenstate) object passed in.  
Used to restore previous state retrieved from the grid by a call to [TreeGrid.getOpenState](#method-treegridgetopenstate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| openState | [TreeGridOpenState](../reference_2.md#type-treegridopenstate) | false | — | Object describing the desired set of open folders. |

### Groups

- viewState

### See Also

- [TreeGrid.getOpenState](#method-treegridgetopenstate)

---
## Method: TreeGrid.setNodeIcon

### Description
Set the icon for a particular treenode to a specified URL

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | tree node |
| icon | [SCImgURL](../reference.md#type-scimgurl) | false | — | path to the resource |

### Groups

- treeIcons

---
## Method: TreeGrid.startEditingNew

### Description
This inherited [ListGrid API](ListGrid_2.md#method-listgridstarteditingnew) is not supported by the TreeGrid since adding a new tree node arbitrarily at the end of the tree is usually not useful. Instead, to add a new tree node and begin editing it, use either of these two strategies:

1.  add a new node to the client-side Tree model via [Tree.add](Tree.md#method-treeadd), then use [TreeGrid.startEditing()](ListGrid_2.md#method-listgridstartediting) to begin editing this node. Note that if using a DataSource, when the node is saved, an "update" operation will be used since adding a node directly to the client-side [ResultTree](ResultTree.md#class-resulttree) effectively means a new node has been added server side.
2.  use [DataSource.addData](DataSource.md#method-datasourceadddata) to immediately save a new node. Automatic cache sync by the [ResultTree](ResultTree.md#class-resulttree) will cause the node to be integrated into the tree. When the callback to addData() fires, locate the new node by matching primary key and call [TreeGrid.startEditing()](ListGrid_2.md#method-listgridstartediting) to begin editing it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValues | [Object](../reference.md#type-object) | true | — | Optional initial set of properties for the new record |
| suppressFocus | [boolean](../reference.md#type-boolean) | true | — | Whether to suppress the default behavior of moving focus to the newly shown editor. |

### Groups

- editing

---
## Method: TreeGrid.transferSelectedData

### Description
Simulates a drag / drop type transfer of the selected records in some other grid to this treeGrid, without requiring any user interaction.  
See the [dragging](../reference.md#kb-topic-dragging) documentation for an overview of grid drag/drop data transfer.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sourceGrid | [ListGrid](#type-listgrid) | false | — | source grid from which the records will be transferred |
| folder | [TreeNode](#type-treenode) | true | — | parent node into which records should be dropped - if null records will be transferred as children of the root node. |
| index | [Integer](../reference_2.md#type-integer) | true | — | target index (drop position) within the parent folder |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback to be fired when the transfer process has completed. The callback will be passed a single parameter "records", the list of nodes actually transferred to this component (it is called "records" because this logic is shared with [ListGrid](ListGrid_1.md#class-listgrid)). |

### Groups

- dragging

---
## Method: TreeGrid.canEditCell

### Description
Overridden to disallow editing of the [name](TreeNode.md#attr-treenodename) field of this grid's data tree. Also disallows editing of the auto-generated tree field, which displays the result of [Tree.getTitle](Tree.md#method-treegettitle) on the node.

### Returns

`[Boolean](#type-boolean)` — Whether to allow editing this cell

---
## Method: TreeGrid.folderClick

### Description
This method is called when a folder record is clicked on.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| viewer | [TreeGrid](#type-treegrid) | false | — | The TreeGrid on which folderClick() occurred. |
| folder | [TreeNode](#type-treenode) | false | — | The folder (record) that was clicked |
| recordNum | [number](#type-number) | false | — | Index of the row where the click occurred. |

### See Also

- [TreeGrid.nodeClick](#method-treegridnodeclick)

---
## Method: TreeGrid.getOpenState

### Description
Returns a snapshot of the current open state of this grid's data as a [TreeGridOpenState](../reference_2.md#type-treegridopenstate) object.  
This object can be passed to [TreeGrid.setOpenState](#method-treegridsetopenstate) to open the same set of folders within the treeGrid's data (assuming the nodes are still present in the data).

### Returns

`[TreeGridOpenState](../reference_2.md#type-treegridopenstate)` — current open state for the grid.

### Groups

- viewState

### See Also

- [TreeGrid.setOpenState](#method-treegridsetopenstate)

---
## Method: TreeGrid.openLeaf

### Description
Executed when a leaf node receives a 'doubleClick' event. This handler must be specified as a function, whose single parameter is a reference to the relevant leaf node in the tree's data.  
See the ListGrid Widget Class for inherited recordClick and recordDoubleClick events.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node to open |

### See Also

- [ListGrid](ListGrid_1.md#class-listgrid)

**Flags**: A

---
