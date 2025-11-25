# TreeGrid drag and drop

[← Back to API Index](../main.md)

---

## KB Topic: TreeGrid drag and drop

### Description
TreeGrids support drag and drop interactions to reorder or reparent nodes within the data tree, or to add new data to the tree.

As with listGrid, drag and drop capabilities may be enabled via properties such as [TreeGrid.canAcceptDroppedRecords](../classes/TreeGrid.md#attr-treegridcanacceptdroppedrecords), [TreeGrid.canReorderRecords](../classes/TreeGrid.md#attr-treegridcanreorderrecords) and [TreeGrid.canDragRecordsOut](../classes/TreeGrid.md#attr-treegridcandragrecordsout).

For an overview of how the data is added or moved when a drop event occurs see [TreeGrid.folderDrop](../classes/TreeGrid.md#method-treegridfolderdrop).  
For details of how data transfer to another DataBoundComponent is handled, see [TreeGrid.transferDragData](../classes/TreeGrid.md#method-treegridtransferdragdata) and [ListGrid.getDragData](../classes/ListGrid_2.md#method-listgridgetdragdata).

The [TreeGrid.showDropIcons](../classes/TreeGrid.md#attr-treegridshowdropicons) and [ListGrid.showDropLines](../classes/ListGrid_1.md#attr-listgridshowdroplines) enable customization of the grid appearance during drag interactions.

By default users may drop data after the last node in the grid. The [TreeGrid.canDropSiblingAfterLastNode](../classes/TreeGrid.md#attr-treegridcandropsiblingafterlastnode) feature allows data to be added as either a sibling of the last node, or to the tree's root node. The [TreeGrid.showDropEndSpace](../classes/TreeGrid.md#attr-treegridshowdropendspace) causes a spacer to be written out after the last node during drag, so there is space available to accept the drop even if the data fills the TreeGrid viewport. To entirely disable this behavior, set [ListGrid.canDropInEmptyArea](../classes/ListGrid_1.md#attr-listgridcandropinemptyarea) to false

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
