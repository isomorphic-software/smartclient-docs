# TreeNode Documentation

[← Back to API Index](../main.md)

---

## Attr: TreeNode.iconPadding

### Description
Developers may customize the padding between the folder or leaf node icon and the text content of the tree cell for individual nodes.

You can change the name of this property by setting [TreeGrid.iconPaddingProperty](TreeGrid.md#attr-treegridiconpaddingproperty)

### Groups

- treeIcons

**Flags**: IRA

---
## Attr: TreeNode.isFolder

### Description
Set to `true` or a string that is not equal to (ignoring case) `"false"` to explicitly mark this node as a folder. See [Tree.isFolder](Tree.md#method-treeisfolder) for a full description of how the [Tree](Tree.md#class-tree) determines whether a node is a folder or not.

Note: the name of this property can be changed by setting [Tree.isFolderProperty](Tree.md#attr-treeisfolderproperty).

### See Also

- [Tree.isFolderProperty](Tree.md#attr-treeisfolderproperty)

**Flags**: IR

---
## Attr: TreeNode.name

### Description
Provides a name for the node that is unique among its immediate siblings, thus allowing a unique path to be used to identify the node, similar to a file system. See [Tree.getPath](Tree.md#method-treegetpath).

If the nameProperty is not set on a given node, the [TreeNode.id](#attr-treenodeid) will be used instead. If this is also missing, [Tree.getName](Tree.md#method-treegetname) and [Tree.getPath](Tree.md#method-treegetpath) will auto-generate a unique name for you. Thus names are not required, but if the dataset you are using already has usable names for each node, using them can make APIs such as [Tree.find](Tree.md#method-treefind) more useful. Alternatively, if your dataset has unique ids consider providing those as [TreeNode.id](#attr-treenodeid).

If a value provided for the nameProperty of a node (e.g. node.name) is not a string, it will be converted to a string by the Tree via ""+value.

This property is also used as the default title for the node (see [Tree.getTitle](Tree.md#method-treegettitle)) if [TreeNode.title](#attr-treenodetitle) is not specified.

Note: the name of this property can be changed by setting [Tree.nameProperty](Tree.md#attr-treenameproperty).

### See Also

- [Tree.nameProperty](Tree.md#attr-treenameproperty)
- [Tree.pathDelim](Tree.md#attr-treepathdelim)
- [Tree.getPath](Tree.md#method-treegetpath)
- [Tree.getTitle](Tree.md#method-treegettitle)

**Flags**: IR

---
## Attr: TreeNode.icon

### Description
This Property allows the developer to customize the icon displayed next to a node. Set `node.icon` to the URL of the desired icon to display and it will be shown instead of the standard [TreeGrid.nodeIcon](TreeGrid.md#attr-treegridnodeicon) for this node.  
Note that if [TreeNode.showOpenIcon](#attr-treenodeshowopenicon) and/or [TreeNode.showDropIcon](#attr-treenodeshowdropicon) is true for this node, customized icons for folder nodes will be appended with the [TreeGrid.openIconSuffix](TreeGrid.md#attr-treegridopeniconsuffix) or [TreeGrid.dropIconSuffix](TreeGrid.md#attr-treegriddropiconsuffix) suffixes on state change as with the standard [TreeGrid.folderIcon](TreeGrid.md#attr-treegridfoldericon) for this treeGrid. Also note that for custom folder icons, the [TreeGrid.closedIconSuffix](TreeGrid.md#attr-treegridclosediconsuffix) will never be appended.

You can change the name of this property by setting [TreeGrid.customIconProperty](TreeGrid.md#attr-treegridcustomiconproperty).

### Groups

- treeIcons

**Flags**: IRW

---
## Attr: TreeNode.enabled

### Description
Default property name denoting whether this record is enabled. Property name may be modified for some grid via [ListGrid.recordEnabledProperty](ListGrid_1.md#attr-listgridrecordenabledproperty).

**Flags**: IR

---
## Attr: TreeNode.canDrag

### Description
Governs whether this node can be dragged. Only has an effect if this node is displayed in a [TreeGrid](TreeGrid.md#class-treegrid) where [TreeGrid.canDragRecordsOut](TreeGrid.md#attr-treegridcandragrecordsout), [TreeGrid.canReorderRecords](TreeGrid.md#attr-treegridcanreorderrecords) or [TreeGrid.canReparentNodes](TreeGrid.md#attr-treegridcanreparentnodes) is `true`.

**Flags**: IRA

---
## Attr: TreeNode.parentId

### Description
For trees with modelType:"parent", this property specifies the unique ID of this node's parent node. The unique ID of a node, together with the unique ID of its parent is used by [Tree.linkNodes](Tree.md#method-treelinknodes) to link a list of nodes into a tree.

Note: the name of this property can be changed by setting [Tree.parentIdField](Tree.md#attr-treeparentidfield).

### See Also

- [TreeNode.id](#attr-treenodeid)
- [Tree.linkNodes](Tree.md#method-treelinknodes)
- [Tree.modelType](Tree.md#attr-treemodeltype)
- [Tree.parentIdField](Tree.md#attr-treeparentidfield)

**Flags**: IR

---
## Attr: TreeNode.id

### Description
Specifies the unique ID of this node.

Required for trees with [Tree.modelType](Tree.md#attr-treemodeltype) "parent". With modelType:"parent", the unique ID of a node, together with the unique ID of its parent (see [TreeNode.parentId](#attr-treenodeparentid)) is used by [Tree.linkNodes](Tree.md#method-treelinknodes) to link a list of nodes into a tree.

Note: the name of this property can be changed by setting [Tree.idField](Tree.md#attr-treeidfield).

### See Also

- [TreeNode.parentId](#attr-treenodeparentid)
- [Tree.linkNodes](Tree.md#method-treelinknodes)
- [Tree.modelType](Tree.md#attr-treemodeltype)
- [Tree.idField](Tree.md#attr-treeidfield)

**Flags**: IR

---
## Attr: TreeNode.children

### Description
For trees with the modelType "children", this property specifies the children of this TreeNode.

Note: the name of this property can be changed by setting [Tree.childrenProperty](Tree.md#attr-treechildrenproperty)

### See Also

- [Tree.modelType](Tree.md#attr-treemodeltype)
- [Tree.childrenProperty](Tree.md#attr-treechildrenproperty)

**Flags**: IRW

---
## Attr: TreeNode.showOpenIcon

### Description
For folder nodes showing custom icons (set via [TreeNode.icon](#attr-treenodeicon)), this property allows the developer to specify on a per-node basis whether an open state icon should be displayed when the folder is open. Set `node.showOpenIcon` to true to show the open state icons, or false to suppress this.  
If not specified, this behavior is determined by [TreeGrid.showCustomIconOpen](TreeGrid.md#attr-treegridshowcustomiconopen) for this node.

You can change the name of this property by setting [TreeGrid.customIconOpenProperty](TreeGrid.md#attr-treegridcustomiconopenproperty).

### Groups

- treeIcons

### See Also

- [TreeGrid.customIconProperty](TreeGrid.md#attr-treegridcustomiconproperty)
- [TreeGrid.showCustomIconOpen](TreeGrid.md#attr-treegridshowcustomiconopen)

**Flags**: IRWA

---
## Attr: TreeNode.showSelectedIcon

### Description
For folder nodes showing custom icons (set via [TreeNode.icon](#attr-treenodeicon)), this property allows the developer to specify on a per-node basis whether a selected state icon should be displayed when the folder is open. Set `node.showSelectedIcon` to true to show the selected state icons, or false to suppress this.  
If not specified, this behavior is determined by [TreeGrid.showCustomIconSelected](TreeGrid.md#attr-treegridshowcustomiconselected) for this node.

You can change the name of this property by setting [TreeGrid.customIconSelectedProperty](TreeGrid.md#attr-treegridcustomiconselectedproperty).

### Groups

- treeIcons

### See Also

- [TreeGrid.customIconProperty](TreeGrid.md#attr-treegridcustomiconproperty)
- [TreeGrid.showCustomIconSelected](TreeGrid.md#attr-treegridshowcustomiconselected)

**Flags**: IRWA

---
## Attr: TreeNode.showDropIcon

### Description
For folder nodes showing custom icons (set via [TreeNode.icon](#attr-treenodeicon)), this property allows the developer to specify on a per-node basis whether a drop state icon should be displayed when the user drop-hovers over this folder.  
Set `node.showDropIcon` to true to show the drop state icon, or false to suppress this.  
If not specified, this behavior is determined by [TreeGrid.showCustomIconDrop](TreeGrid.md#attr-treegridshowcustomicondrop) for this node.

You can change the name of this property by setting [TreeGrid.customIconDropProperty](TreeGrid.md#attr-treegridcustomicondropproperty).

### Groups

- treeIcons

### See Also

- [TreeGrid.customIconProperty](TreeGrid.md#attr-treegridcustomiconproperty)
- [TreeGrid.showCustomIconDrop](TreeGrid.md#attr-treegridshowcustomicondrop)

**Flags**: IRWA

---
## Attr: TreeNode.title

### Description
The title of the node as it should appear next to the node icon in the [Tree](Tree.md#class-tree). If left unset, the value of [TreeNode.name](#attr-treenodename) is used by default. See the description in [Tree.getTitle](Tree.md#method-treegettitle) for full details.

Note: the name of this property can be changed by setting [Tree.titleProperty](Tree.md#attr-treetitleproperty).

### See Also

- [Tree.titleProperty](Tree.md#attr-treetitleproperty)
- [Tree.getTitle](Tree.md#method-treegettitle)

**Flags**: IR

---
## Attr: TreeNode.canAcceptDrop

### Description
Governs whether dragged data (typically other `treeNode`s) may be dropped over this node. Only has an effect if this node is displayed in a [TreeGrid](TreeGrid.md#class-treegrid) where [TreeGrid.canAcceptDroppedRecords](TreeGrid.md#attr-treegridcanacceptdroppedrecords), [TreeGrid.canReorderRecords](TreeGrid.md#attr-treegridcanreorderrecords) or [TreeGrid.canReparentNodes](TreeGrid.md#attr-treegridcanreparentnodes) is true.

**Flags**: IRA

---
