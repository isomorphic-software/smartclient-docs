# TreeGrid drag and drop

[← Back to API Index](../reference.md)

---

## KB Topic: TreeGrid drag and drop

### Description
TreeGrids support drag and drop interactions to reorder or reparent nodes within the data tree, or to add new data to the tree.

As with listGrid, drag and drop capabilities may be enabled via properties such as [TreeGrid.canAcceptDroppedRecords](../classes/TreeGrid.md#attr-treegridcanacceptdroppedrecords), [TreeGrid.canReorderRecords](../classes/TreeGrid.md#attr-treegridcanreorderrecords) and [TreeGrid.canDragRecordsOut](../classes/TreeGrid.md#attr-treegridcandragrecordsout). By default, drops are only accepted on folders; set [TreeGrid.canDropOnLeaves](../classes/TreeGrid.md#attr-treegridcandroponleaves) to true to allow dropping on leaf nodes as well.

Note that the behaviors described below are triggered automatically by interactive drag and drop, and can also be triggered programmatically by calling [TreeGrid.transferNodes](../classes/TreeGrid.md#method-treegridtransfernodes).

**Custom drop behavior**: To implement custom drop behavior, developers may override [TreeGrid.folderDrop](../classes/TreeGrid.md#method-treegridfolderdrop). Return false from `folderDrop()` to suppress the built-in persistence behavior, then perform the desired drop action such as calling [updateData()](../classes/DataSource.md#method-datasourceupdatedata) or [addData()](../classes/DataSource.md#method-datasourceadddata).

**Drag within the same tree:** Default behavior when dragging node(s) to a new folder within the same tree is to reparent the dropped node(s) by modifying their [parentId](../classes/Tree.md#attr-treeparentidfield) field value. For [databound treeGrids](../classes/TreeGrid.md#attr-treegriddatasource), an update operation will be issued unless the tree has been configured to [save locally](../classes/ListGrid_1.md#attr-listgridsavelocally).  
Dragging a node to a different position within its current parent reorders it locally.  
See also [TreeGrid.canReparentNodes](../classes/TreeGrid.md#attr-treegridcanreparentnodes).

**Drops from another component:** For drops from another widget default behavior is governed by [dragDataAction](../classes/TreeGrid.md#attr-treegriddragdataaction) on the source widget plus [dragRecategorize](../classes/DataBoundComponent.md#attr-databoundcomponentdragrecategorize) on this treeGrid. `dragDataAction` (set on the source) controls whether dragged records are removed from the source data set on successful drop, or left in place. `dragRecategorize` (set on this treeGrid) controls how the dropped records are persisted.  
Dropped data may either be recategorized or added as a new node.

_Drag-Recategorize_: TreeGrids support recategorizing records on drop when the source component is either bound to the same DataSource, or a DataSource with a [foreignKey](../classes/DataSourceField.md#attr-datasourcefieldforeignkey) relationship with this treeGrid's DataSource.

When both the source and target components are bound to the same DataSource - for example when a ListGrid is used to display a flat list of nodes from the selected folder of a TreeGrid - dropping a record into the TreeGrid will update the [parentIdField](../classes/Tree.md#attr-treeparentidfield) on the dropped records to match the [idField](../classes/Tree.md#attr-treeidfield) of the target folder.

When the source and target components' DataSources are related by foreignKey - for example when a ListGrid displays related records from a master tree of categories - the foreignKey field on the dropped records is updated to point to the target folder.

Whether this automatic behavior is applied depends on [dragRecategorize](../classes/DataBoundComponent.md#attr-databoundcomponentdragrecategorize) (set on the target):

*   `"checked"` (the default): recategorize only if the source widget's [dragDataAction](../classes/TreeGrid.md#attr-treegriddragdataaction) is "move". This is the normal case: the user is moving data to a new location, so updating the foreignKey or parentId is appropriate.
*   `"always"`: recategorize regardless of `dragDataAction`. This allows you to update the foreignKey/parentId even when the source retains a copy of the record due to `dragDataAction:"copy"` (e.g., dragging from a template palette).
*   `"never"`: never recategorize. Drops always go through the generic add path below.

_Add data:_ The default TreeGrid drop behavior when drag-recategorize is not applicable or has been disabled via `dragRecategorize:"never"` is to add dropped records to the tree via [DataSource.addData](../classes/DataSource.md#method-datasourceadddata), with the [parentId](../classes/Tree.md#attr-treeparentidfield) set to the target folder. [addDropValues](../classes/DataBoundComponent.md#attr-databoundcomponentadddropvalues) and [getDropValues](../classes/DataBoundComponent.md#method-databoundcomponentgetdropvalues) are applied. If [DataBoundComponent.preventDuplicates](../classes/DataBoundComponent.md#attr-databoundcomponentpreventduplicates) is set, a duplicate check is performed (which may require a server round-trip if the cache is incomplete).

In all databound cases, [queuing](../classes/RPCManager.md#class-rpcmanager) is used to combine the DSRequests for a multi-record drop into a single HTTP request, allowing the server to persist all changes in a single transaction.

**Visual feedback**

The [TreeGrid.showDropIcons](../classes/TreeGrid.md#attr-treegridshowdropicons) and [ListGrid.showDropLines](../classes/ListGrid_1.md#attr-listgridshowdroplines) properties enable customization of the grid appearance during drag interactions.

By default users may drop data after the last node in the grid. The [TreeGrid.canDropSiblingAfterLastNode](../classes/TreeGrid.md#attr-treegridcandropsiblingafterlastnode) feature allows data to be added as either a sibling of the last node, or to the tree's root node. The [TreeGrid.showDropEndSpace](../classes/TreeGrid.md#attr-treegridshowdropendspace) causes a spacer to be written out after the last node during drag, so there is space available to accept the drop even if the data fills the TreeGrid viewport. To entirely disable this behavior, set [ListGrid.canDropInEmptyArea](../classes/ListGrid_1.md#attr-listgridcandropinemptyarea) to false.

For details of how data transfer _from_ a TreeGrid to another DataBoundComponent is handled, see [TreeGrid.transferDragData](../classes/TreeGrid.md#method-treegridtransferdragdata) and [ListGrid.getDragData](../classes/ListGrid_2.md#method-listgridgetdragdata).

### Related

- [TreeGrid.willAcceptDrop](../classes/TreeGrid.md#method-treegridwillacceptdrop)
- [TreeGrid.folderDrop](../classes/TreeGrid.md#method-treegridfolderdrop)
- [TreeGrid.transferNodes](../classes/TreeGrid.md#method-treegridtransfernodes)
- [TreeGrid.canDragRecordsOut](../classes/TreeGrid.md#attr-treegridcandragrecordsout)
- [TreeGrid.canAcceptDroppedRecords](../classes/TreeGrid.md#attr-treegridcanacceptdroppedrecords)
- [TreeGrid.canReorderRecords](../classes/TreeGrid.md#attr-treegridcanreorderrecords)
- [TreeGrid.canDropOnLeaves](../classes/TreeGrid.md#attr-treegridcandroponleaves)
- [TreeGrid.canReparentNodes](../classes/TreeGrid.md#attr-treegridcanreparentnodes)
- [TreeGrid.dragDataAction](../classes/TreeGrid.md#attr-treegriddragdataaction)
- [TreeGrid.showDropEndSpace](../classes/TreeGrid.md#attr-treegridshowdropendspace)

---
