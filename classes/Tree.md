# Tree Documentation

[← Back to API Index](../reference.md)

---

## Class: Tree

### Description
A Tree is a data model representing a set of objects linked into a hierarchy.

A Tree has no visual presentation, it is displayed by a [TreeGrid](TreeGrid.md#class-treegrid) or [ColumnTree](ColumnTree.md#class-columntree) when supplied as [TreeGrid.data](TreeGrid.md#attr-treegriddata) or [ColumnTree.data](ColumnTree.md#attr-columntreedata).

A Tree can be constructed out of a List of objects interlinked by IDs or via explicitly specified Arrays of child objects. See [Tree.modelType](#attr-treemodeltype) for an explanation of how to pass data to a Tree.

Typical usage is to call [TreeGrid.fetchData](TreeGrid.md#method-treegridfetchdata) to cause automatic creation of a [ResultTree](ResultTree.md#class-resulttree), which is a type of Tree that automatically handles loading data on demand. For information on DataBinding Trees, see [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding).

---
## ClassAttr: Tree.isNodeLocatorProperty

### Description
Name of property that identifies a [NodeLocator](../reference_2.md#object-nodelocator) object for any [multi-link tree](#method-treeismultilinktree)s.

**Flags**: IRW

---
## ClassAttr: Tree.LOADED

### Description
A declared value of the enum type [LoadState](../reference.md#type-loadstate).

**Flags**: R

---
## ClassAttr: Tree.UNLOADED

### Description
A declared value of the enum type [LoadState](../reference.md#type-loadstate).

**Flags**: R

---
## ClassAttr: Tree.LOADING

### Description
A declared value of the enum type [LoadState](../reference.md#type-loadstate).

**Flags**: R

---
## ClassAttr: Tree.FOLDERS_LOADED

### Description
A declared value of the enum type [LoadState](../reference.md#type-loadstate).

**Flags**: R

---
## ClassAttr: Tree.LOADED_PARTIAL_CHILDREN

### Description
A declared value of the enum type [LoadState](../reference.md#type-loadstate).

**Flags**: R

---
## Attr: Tree.titleProperty

### Description
Name of the property on a [TreeNode](../reference_2.md#object-treenode) that holds the title of the node as it should be shown to the user. Default value is "title". See [TreeNode.title](TreeNode.md#attr-treenodetitle) for usage.

**Flags**: IRW

---
## Attr: Tree.linkPositionField

### Description
The name of the "position" field in this [multi-link tree](#attr-treelinkdata)'s link data. Ignored if this tree is not a multi-link tree. Note, these values are only used to order the nodes within a parent - so a node with link position -123 will appear before a node with link position 87, but that is the only significance of the link position values

### Groups

- multiLinkTree

**Flags**: IR

---
## Attr: Tree.rootValue

### Description
If you are using the "parent" modelType and did not specify a root node via [Tree.root](#attr-treeroot) with an id ([Tree.idField](#attr-treeidfield)), then you can provide the root node's id via this property.

This setting is invalid if [TreeGrid.keepParentsOnFilter](TreeGrid.md#attr-treegridkeepparentsonfilter) is set and [fetch-mode](TreeGrid.md#attr-treegriddatafetchmode) is set to anything other than ["paged"](../reference_2.md#type-fetchmode) - a root-value cannot be used in this case because there is no efficient way to load a subtree to include all parents. If `fetchMode` is specifically set to "paged", the rootValue is passed as criteria and the [keepParentsOnFilter](DSRequest.md#attr-dsrequestkeepparentsonfilter) flag is set on the request so the server knows to use special filtering rules, but these rules are not built-in - the developer is responsible for this logic.

See [Tree.data](#attr-treedata) for an example.

### See Also

- [Tree.data](#attr-treedata)

**Flags**: IR

---
## Attr: Tree.defaultIsFolder

### Description
Controls whether nodes are assumed to be folders or leaves by default.

Nodes that have children or have the [Tree.isFolderProperty](#attr-treeisfolderproperty) set to true will be considered folders by default. Other nodes will be considered folders or leaves by default according to this setting.

See also [ResultTree.defaultIsFolder](ResultTree.md#attr-resulttreedefaultisfolder) for more details on how `defaultIsFolder` interacts with [loading data on demand](TreeGrid.md#attr-treegridloaddataondemand).

**Flags**: IR

---
## Attr: Tree.data

### Description
Optional initial data for the tree. How this data is interpreted depends on this tree's [Tree.modelType](#attr-treemodeltype).

If `modelType` is `"parent"`, the list that you provide will be passed to [Tree.linkNodes](#method-treelinknodes), integrating the nodes into the tree.

In this case the root node may be supplied explicitly via [Tree.root](#attr-treeroot), or auto generated, picking up its `id` via [Tree.rootValue](#attr-treerootvalue). Any nodes in the data with no explicitly specified [TreeNode.parentId](TreeNode.md#attr-treenodeparentid) will be added as children to this root element.

To create this tree:

```
 foo
   bar
 zoo
 
```
with modelType:"parent", you can do this:
```
 Tree.create({
   data: [
     {name: "foo", id: "foo"},
     {name: "bar", id: "bar", parentId: "foo"},
     {name: "zoo", id: "zoo"}
 });
 
```
Or this (explicitly specified root):
```
 Tree.create({
   root: {id: "root"},
   data: [
     {name: "foo", id: "foo", parentId: "root"},
     {name: "bar", id: "bar", parentId: "foo"},
     {name: "zoo", id: "zoo", parentId: "root"}
 });
 
```
Or this (explicitly specified rootValue):
```
 Tree.create({
   rootValue: "root",
   data: [
     {name: "foo", id: "foo", parentId: "root"},
     {name: "bar", id: "bar", parentId: "foo"},
     {name: "zoo", id: "zoo", parentId: "root"}
 });
 
```
Specifying the root node explicitly allows you to give it a name, changing the way path derivation works (see [Tree.root](#attr-treeroot) for more on naming the root node).

For `modelType:"children"` trees, the data passed in will be assumed to be an array of children of the tree's root node.

### See Also

- [Tree.modelType](#attr-treemodeltype)
- [TreeNode](../reference_2.md#object-treenode)

**Flags**: IR

---
## Attr: Tree.allowFilterOnLinkFields

### Description
For a [multi-link tree](#method-treeismultilinktree), indicates whether client-side filtering is allowed on the fields of the [linkDataSource](ResultTree.md#attr-resulttreelinkdatasource). When this property is true, filtering operations involving link fields work as expected (ie, as if those fields were present on the main [dataSource](ResultTree.md#attr-resulttreedatasource)); when this value is not true, criterions involving link fields are simply ignored.

Note, setting this property true causes filtering operations to perform an additional record duplication per node in the dataset to be filtered. This adds some overhead, so you should consider likely data volumes before enabling it (though in fact, client-side filtering of trees is relatively expensive anyway, so acceptable use cases probably already involve quite low data volumes)

This property has no effect for regular, non-multiLink trees.

### Groups

- multiLinkTree

**Flags**: IR

---
## Attr: Tree.pathDelim

### Description
Specifies the delimiter between node names. The pathDelim is used to construct a unique path to each node. A path can be obtained for any node by calling [Tree.getPath](#method-treegetpath) and can be used to find any node in the tree by calling [Tree.find](#method-treefind). Note that you can also hand-construct a path - in other words you are not required to call [Tree.getPath](#method-treegetpath) in order to later use [Tree.find](#method-treefind) to retrieve it.  
  
The pathDelim can be any character or sequence of characters, but must be a unique string with respect to the text that can appear in the [Tree.nameProperty](#attr-treenameproperty) that's used for naming the nodes. So for example, if you have the following tree:
```
 one
   two
     three/four
 
```
Then you will be unable to find the `three/four` node using [Tree.find](#method-treefind) if your tree is using the default pathDelim of /. In such a case, you can use a different pathDelim for the tree. For example if you used | for the path delim, then you can find the `three/four` node in the tree above by calling `tree.find("one|two|three/four")`.  
  
The pathDelim is used only by [Tree.getPath](#method-treegetpath) and [Tree.find](#method-treefind) and does not affect any aspect of the tree structure or other forms of tree navigation (such as via [Tree.getChildren](#method-treegetchildren)).

### See Also

- [Tree.nameProperty](#attr-treenameproperty)
- [Tree.find](#method-treefind)

**Flags**: IRWA

---
## Attr: Tree.idField

### Description
Name of the property on a [TreeNode](../reference_2.md#object-treenode) that holds an id for the node which is unique across the entire Tree. Required for all nodes for trees with modelType "parent". Default value is "id". See [TreeNode.id](TreeNode.md#attr-treenodeid) for usage.

### See Also

- [TreeNode.id](TreeNode.md#attr-treenodeid)

**Flags**: IRA

---
## Attr: Tree.defaultNodeTitle

### Description
Title assigned to nodes without a [Tree.titleProperty](#attr-treetitleproperty) value or a [Tree.nameProperty](#attr-treenameproperty) value.

**Flags**: IRW

---
## Attr: Tree.dataSource

### Description
Specifies what [DataSource](DataSource.md#class-datasource) this tree is associated with.

A [DataSource](DataSource.md#class-datasource) is required when filtering a tree, even if it isn't a [ResultTree](ResultTree.md#class-resulttree), though it may be passed to [Tree.getFilteredTree](#method-treegetfilteredtree) rather than set on the tree itself. If a [DataSource](DataSource.md#class-datasource) is specified it will also affect sorting, where relevant, such as if the tree is set as [TreeGrid.data](TreeGrid.md#attr-treegriddata).

### Groups

- treeFilter

### See Also

- [DataBoundComponent.dataSource](DataBoundComponent.md#attr-databoundcomponentdatasource)

**Flags**: IR

---
## Attr: Tree.autoOpenRoot

### Description
If true, the root node is automatically opened when the tree is created or [Tree.setRoot](#method-treesetroot) is called.

**Flags**: IRW

---
## Attr: Tree.openProperty

### Description
The property consulted by the default implementation of [Tree.isOpen](#method-treeisopen) to determine if the node is open or not. By default, this property is auto-generated for you, but you can set it to a custom value if you want to declaratively specify this state, but be careful - if you display this Tree in multiple TreeGrids at the same time, the open state will not be tracked independently - see [sharingNodes](../kb_topics/sharingNodes.md#kb-topic-sharing-nodes) for more info on this.

For [multi-link tree](#method-treeismultilinktree)s, we do not track open state on the nodes themselves, because this would mean that multiple instances of a node in the tree would open and close in lockstep. Instead, open state is tracked in an internal index structure, and the `openProperty` is not used at all.

### Groups

- openList

### See Also

- [sharingNodes](../kb_topics/sharingNodes.md#kb-topic-sharing-nodes)

**Flags**: IRWA

---
## Attr: Tree.sortFoldersBeforeLeaves

### Description
If [Tree.separateFolders](#attr-treeseparatefolders) is true, should folders be displayed above or below leaves? When set to `true` folders will appear above leaves when the `sortDirection` applied to the tree is ["ascending"](../reference_2.md#type-sortdirection)

**Flags**: IRW

---
## Attr: Tree.showRoot

### Description
Controls whether the implicit root node is returned as part of the visible tree, specifically, whether it is returned in [Tree.getOpenList](#method-treegetopenlist), which is the API view components typically use to get the list of visible nodes.

Default is to have the root node be implicit and not included in the open list, which means that the visible tree begins with the children of root. This allows multiple nodes to appear at the top level of the tree.

You can set `showRoot:true` to show the single, logical root node as the only top-level node. This property is only meaningful for Trees where you supplied a value for [Tree.root](#attr-treeroot), otherwise, you will see an automatically generated root node that is meaningless to the user.

**Flags**: IRW

---
## Attr: Tree.nameProperty

### Description
Name of the property on a [TreeNode](../reference_2.md#object-treenode) that holds a name for the node that is unique among its immediate siblings, thus allowing a unique path to be used to identify the node, similar to a file system. Default value is "name". See [TreeNode.name](TreeNode.md#attr-treenodename) for usage.

### See Also

- [TreeNode.name](TreeNode.md#attr-treenodename)

**Flags**: IRW

---
## Attr: Tree.modelType

### Description
Selects the model used to construct the tree representation. See [TreeModelType](../reference.md#type-treemodeltype) for the available options and their implications.

If the "parent" modelType is used, you can provide the initial parent-linked data set to the tree via the [Tree.data](#attr-treedata) attribute. If the "children" modelType is used, you can provide the initial tree structure to the Tree via the [Tree.root](#attr-treeroot) attribute.

### See Also

- [Tree.data](#attr-treedata)
- [Tree.root](#attr-treeroot)

**Flags**: IRWA

---
## Attr: Tree.separateFolders

### Description
Should folders be sorted separately from leaves or should nodes be ordered according to their sort field value regardless of whether the node is a leaf or folder?

### See Also

- [Tree.sortFoldersBeforeLeaves](#attr-treesortfoldersbeforeleaves)

**Flags**: IRW

---
## Attr: Tree.multiLinkTree

### Description
If true, indicates this is a "multiLink" tree - ie, one that can contain the same node in more than one place. Note, multiLink trees **must** use the "parent" [model type](#attr-treemodeltype)

See [Tree.linkData](#attr-treelinkdata) and [ResultTree.linkDataSource](ResultTree.md#attr-resulttreelinkdatasource) for further details of multiLink trees.

### Groups

- multiLinkTree

**Flags**: IR

---
## Attr: Tree.discardParentlessNodes

### Description
If this tree has [modelType:"parent"](#attr-treemodeltype), should nodes in the data array for the tree be dropped if they have an explicitly specified value for the [Tree.parentIdField](#attr-treeparentidfield) which doesn't match any other nodes in the tree. If set to false these nodes will be added as children of the root node.

**Flags**: IRA

---
## Attr: Tree.reportCollisions

### Description
If new nodes are added to a tree with modelType:"parent" which have the same [id field value](#attr-treeidfield) as existing nodes, the existing nodes are removed when the new nodes are added.

If reportCollisions is true, the Tree will log a warning in the developer console about this.

Note that if an id collision occurs between a new node and its ancestor, the ancestor will be removed and the new node will not be added to the tree.

**Flags**: IR

---
## Attr: Tree.root

### Description
If you're using the "parent" modelType, you can provide the root node configuration via this property. If you don't provide it, one will be auto-created for you with an empty name. Read on for a description of what omitting the name property on the root node means for path derivation.

If you're using the "children" modelType, you can provide the initial tree data via this property. So, for example, to construct the following tree:

```
 foo
   bar
 zoo
 
```
You would initialize the tree as follows:
```
 Tree.create({
     root: { name:"root", children: [
         { name:"foo", children: [
             { name: "bar" }
         ]},
         { name: "zoo" }
     ]}
 });
 
```
Note that if you provide a `name` property for the root node, then the path to any node underneath it will start with that name. So in the example above, the path to the `bar` node would be `root/foo/bar` (assuming you're using the default [Tree.pathDelim](#attr-treepathdelim). If you omit the name attribute on the root node, then its name is automatically set to the [Tree.pathDelim](#attr-treepathdelim) value. So in the example above, if you omitted `name:"root"`, then the path to the `bar` node would be `/foo/bar`.  
  
Note: if you initialize a Tree with no `root` value, a root node will be auto-created for you. You can then call [Tree.add](#method-treeadd) to construct the tree.

### See Also

- [Tree.modelType](#attr-treemodeltype)
- [Tree.setRoot](#method-treesetroot)

**Flags**: IRW

---
## Attr: Tree.linkData

### Description
For a [multi-link tree](#attr-treemultilinktree), this property specifies the parent-child relationships between the nodes. The nodes themselves are provided in [Tree.data](#attr-treedata). Note that multi-link trees must specify a [modelType](#attr-treemodeltype) of "parent".

For a regular, non-multiLink tree, the `linkData` property is ignored.

Minimally, the link data should include a node id, parent id and optionally the position of the child within that parent. To describe this multi-link tree:

```
   foo
     bar
       baz
     zoo
       bar
         baz
 
```
you would provide node information in the `data` property like this:
```
   [
     {id: "foo"},
     {id: "bar"},
     {id: "baz"},
     {id: "zoo"}
   ]
 
```
and link information in `linkData` like this:
```
   [
     {id: "bar", parentId: "foo"},
     {id: "baz", parentId: "bar"},
     {id: "zoo", parentId: "foo"},
     {id: "bar", parentId: "zoo"}
   ]
 
```
For information on databinding multi-link trees, and further discussion on multi-link trees generally, see [ResultTree.linkDataSource](ResultTree.md#attr-resulttreelinkdatasource)

### Groups

- multiLinkTree

### See Also

- [ResultTree.linkDataSource](ResultTree.md#attr-resulttreelinkdatasource)

**Flags**: IR

---
## Attr: Tree.parentIdField

### Description
For trees with modelType "parent", this property specifies the name of the property that contains the unique parent ID of a node. Default value is "parentId". See [TreeNode.parentId](TreeNode.md#attr-treenodeparentid) for usage.

### See Also

- [TreeNode.parentId](TreeNode.md#attr-treenodeparentid)

**Flags**: IRA

---
## Attr: Tree.childrenProperty

### Description
For trees with the modelType "children", this property specifies the name of the property that contains the list of children for a node.

### See Also

- [Tree.modelType](#attr-treemodeltype)

**Flags**: IRW

---
## Attr: Tree.isFolderProperty

### Description
Name of property that defines whether a node is a folder. By default this is set to [TreeNode.isFolder](TreeNode.md#attr-treenodeisfolder).

### See Also

- [TreeNode.isFolder](TreeNode.md#attr-treenodeisfolder)

**Flags**: IRW

---
## ClassMethod: Tree.findChildrenProperty

### Description
heuristically find a property that appears to contain child objects. Searches through a node and find a property that is either Array or Object valued.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | the node to check |
| mode | [ChildrenPropertyMode](../reference.md#type-childrenpropertymode) | false | — | determines how to chose the property that appears to contain child objects |

### Returns

`[String](#type-string)` — the name of the property that holds the children

---
## ClassMethod: Tree.discoverTree

### Description
given a hierarchy of objects with children under mixed names, heuristically discover the property that holds children and copy it to a single, uniform childrenProperty. Label each discovered child with a configurable "typeProperty" set to the value of the property that held the children.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of TreeNode](#type-array-of-treenode) | false | — | list of nodes to link into the tree. |
| settings | [DiscoverTreeSettings](#type-discovertreesettings) | false | — | configures how the tree will be explored |
| parentChildrenField | [String](#type-string) | false | — | — |

---
## Method: Tree.remove

### Description
Removes a node, along with all its children. See ["Modifying ResultTrees"](ResultTree.md#class-resulttree) when working with a `ResultTree` for limitations. Note, if this is a [multi-link tree](#method-treeismultilinktree), you must pass in a [NodeLocator](../reference_2.md#object-nodelocator) rather than a node or id.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[String](#type-string)|[Integer](../reference_2.md#type-integer)|[NodeLocator](#type-nodelocator) | false | — | node to remove, or the node's ID, or a NodeLocator |

### Returns

`[Boolean](#type-boolean)` — true if the tree was changed as a result of this call

---
## Method: Tree.getParents

### Description
Given a node, return an array of the node's ancestors, with the immediate parent first, then the grandparent, and so on. The node itself is not included in the result. For example, for the following tree:
```
 root
   foo
     bar
 
```
Calling `tree.getParents(bar)` would return: `[foo, root]`. Note that the returned array will contain references to the nodes, not the names.

Note, for reasons of backwards compatibility, if you pass this method a `TreeNode` instance on a [multi-link tree](#method-treeismultilinktree), it will return an array representing one path through the node's ancestors, which is unlikely to be useful. To get the ancestor chain of a specific node occurence, you must pass a [NodeLocator](../reference_2.md#object-nodelocator) that specifies the full ID-based path to that occurence. If what you actually want is a list of the node's direct parents, see [Tree.getMultiLinkParents](#method-treegetmultilinkparents).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[NodeLocator](#type-nodelocator) | false | — | node in question, or a NodeLocator |

### Returns

`[Array](#type-array)` — array of node's parents

---
## Method: Tree.getFolders

### Description
Returns all the first-level folders of a node.  
  
For load on demand trees (those that only have a partial representation client-side), this method will return only nodes that have already been loaded from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — List of immediate children that are folders

---
## Method: Tree.getLeaves

### Description
Return all the first-level leaves of a node.  
  
For load on demand trees (those that only have a partial representation client-side), this method will return only nodes that have already been loaded from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — List of immediate children that are leaves.

---
## Method: Tree.removeChildren

### Description
Removes all children of the node and sets it to a loaded state. For non-[ResultTree](ResultTree.md#class-resulttree)s, or non-[paged](ResultTree.md#attr-resulttreefetchmode) `ResultTree`s, [Tree.add](#method-treeadd) or [Tree.addList](#method-treeaddlist) can then be used to provide new children. For [paged](ResultTree.md#attr-resulttreefetchmode) `ResultTrees`, [DataSource.updateCaches](DataSource.md#method-datasourceupdatecaches) must be used to insert nodes into the cache as local data, since such `ResultTree`s are considered read-only, and [Tree.add](#method-treeadd) and [Tree.addList](#method-treeaddlist) are not perrmitted.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | folder in question |

### Groups

- loadState

### See Also

- [Tree.getLoadState](#method-treegetloadstate)
- [Tree.reloadChildren](#method-treereloadchildren)

---
## Method: Tree.hasLeaves

### Description
Return whether this node has any children that are leaves.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Boolean](#type-boolean)` — true if the node has children that are leaves

---
## Method: Tree.addList

### Description
Add a list of nodes to some parent. See ["Modifying ResultTrees"](ResultTree.md#class-resulttree) when working with a `ResultTree` for limitations.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodeList | [List of TreeNode](#type-list-of-treenode) | false | — | The list of nodes to add |
| parent | [String](#type-string)|[TreeNode](#type-treenode) | false | — | Parent of the nodes being added. You can pass in either the [TreeNode](../reference_2.md#object-treenode) itself, or a path to the node (as a String), in which case a [Tree.find](#method-treefind) is performed to find the node. |
| position | [number](#type-number) | true | — | Position of the new nodes in the children list. If not specified, the nodes will be added at the end of the list. |

### Returns

`[List](#type-list)` — List of added nodes.

### See Also

- [sharingNodes](../kb_topics/sharingNodes.md#kb-topic-sharing-nodes)

---
## Method: Tree.openAll

### Description
Open all nodes under a particular node.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[String](#type-string)|[Integer](../reference_2.md#type-integer)|[NodeLocator](#type-nodelocator) | true | — | node from which to open folders, or the node's ID, or a NodeLocator object (if not specified, the root node is used) |

---
## Method: Tree.getDescendants

### Description
Returns the list of all descendants of a node. Note: this method can be very slow, especially on large trees because it assembles a list of all descendants recursively. Generally, [Tree.find](#method-treefind) in combination with [Tree.getChildren](#method-treegetchildren) will be much faster.  
  
For load on demand trees (those that only have a partial representation client-side), this method will return only nodes that have already been loaded from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | true | — | node in question (root node is assumed if none is specified) |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — List of descendants of the node.

---
## Method: Tree.setSortFoldersBeforeLeaves

### Description
Setter for [Tree.sortFoldersBeforeLeaves](#attr-treesortfoldersbeforeleaves).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sortFoldersBeforeLeaves | [Boolean](#type-boolean) | false | — | new `sortFoldersBeforeLeaves` value |

---
## Method: Tree.getDescendantNodeLocators

### Description
Returns a list of link{type:NodeLocator)s identifying all descendants of a node (identified by the parameter `NodeLocator`). This method is the equivalent of [getDescendants()](#method-treegetdescendants), but for [multi-link trees](#method-treeismultilinktree). The list of descendant nodes returned from both methods is identical - a node's descendants are the same regardless of where or how many times that node appears in the tree - but the `NodeLocator`s returned by this method provide additional context that allows you to determine particular occurences of descendant nodes. This is necessary for some use cases - for example, when trying to determine if a particular node occurence is open, or selected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | true | — | node in question (root node is assumed if none is specified) |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — List of descendants of the node.

---
## Method: Tree.openFolders

### Description
Open a set of folders, specified by path or as pointers to nodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodeList | [List of TreeNode](#type-list-of-treenode) | false | — | List of nodes or node paths or NodeLocators |

### See Also

- [ResultTree.dataArrived](ResultTree.md#method-resulttreedataarrived)

---
## Method: Tree.getTitle

### Description
Return the title of a node -- the name as it should be presented to the user. This method works as follows:

*   If a [Tree.titleProperty](#attr-treetitleproperty) is set on the node, the value of that property is returned.
*   Otherwise, if the [Tree.nameProperty](#attr-treenameproperty) is set on the node, that value is returned, minus any trailing [Tree.pathDelim](#attr-treepathdelim).
*   Finally, if none of the above yielded a title, the value of [Tree.defaultNodeTitle](#attr-treedefaultnodetitle) is returned.

You can override this method to return the title of your choice for a given node.  
  
To override the title for an auto-constructed tree (for example, in a databound TreeGrid), override [TreeGrid.getNodeTitle](TreeGrid.md#method-treegridgetnodetitle) instead.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node for which the title is being requested |

### Returns

`[String](#type-string)` — title to display

### See Also

- [TreeGrid.getNodeTitle](TreeGrid.md#method-treegridgetnodetitle)

---
## Method: Tree.getMultiLinkParents

### Description
For [multiLink trees](#method-treeismultilinktree), returns the array of this node's direct parents (the actual node objects, not the IDs). For non-multiLink trees, returns an array containing the single parent of this node. See also [Tree.getParentsAndPositions](#method-treegetparentsandpositions).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — the parents of this node

---
## Method: Tree.getFilteredTree

### Description
Filters this tree by the provided criteria, returning a new Tree containing just the nodes that match the criteria.

If `filterMode` is "keepParents", parents are retained if any of their children match the criteria even if those parents do not match the criteria.

Note that the [DataSource](DataSource.md#class-datasource) argument is **required** if one is not [already specified](DataSource.md#class-datasource) on the tree.

If you want a [TreeGrid](TreeGrid.md#class-treegrid) with local tree data that supports filtering, please consider using a [TreeGrid](TreeGrid.md#class-treegrid) bound to a [client-only DataSource](DataSource.md#attr-datasourceclientonly) rather than writing your own code to filter the tree's data with this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| criteria | [Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria) | false | — | criteria to filter by |
| filterMode | [TreeFilterMode](../reference.md#type-treefiltermode) | true | — | mode to use for filtering, defaults to "strict" |
| dataSource | [DataSource](#type-datasource) | true | — | dataSource to use for filtering, if this Tree does not already have one |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | Request properties block. This allows developers to specify properties that would impact the filter such as [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) |

### Returns

`[Tree](#type-tree)` — filtered tree

### Groups

- treeFilter

### See Also

- [ListGrid.setCriteria](ListGrid_2.md#method-listgridsetcriteria)
- [TreeGrid.filterData](TreeGrid.md#method-treegridfilterdata)
- [ResultTree](ResultTree.md#class-resulttree)

---
## Method: Tree.closeFolder

### Description
Closes a folder. Note, for [multi-link tree](#method-treeismultilinktree)s, passing a `NodeLocator` is the only unambiguous way to specify the node.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[String](#type-string)|[Integer](../reference_2.md#type-integer)|[NodeLocator](#type-nodelocator) | false | — | the node to open, or its ID, or a NodeLocator object |

---
## Method: Tree.getChildrenResultSet

### Description
Returns a ResultSet that provides access to any partially-loaded children of a node. If the node is a leaf, this method returns null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | The node whose children you want to fetch. |

### Returns

`[ResultSet](#type-resultset)` — List of children for the node, including an empty ResultSet if the node has no children. For a leaf, returns null.

### See Also

- [Tree.getChildren](#method-treegetchildren)
- [Tree.allChildrenLoaded](#method-treeallchildrenloaded)

---
## Method: Tree.isDescendantOf

### Description
Is one node a descendant of the other?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [TreeNode](#type-treenode) | false | — | child node |
| parent | [TreeNode](#type-treenode) | false | — | parent node |

### Returns

`[Boolean](#type-boolean)` — true == parent is an ancestor of child

---
## Method: Tree.linkNodes

### Description
Adds an array of tree nodes into a Tree of [Tree.modelType](#attr-treemodeltype) "parent".

The provided TreeNodes must contain, at a minimum, a field containing a unique ID for the node (specified by [Tree.idField](#attr-treeidfield)) and a field containing the ID of the node's parent node (specified by [Tree.parentIdField](#attr-treeparentidfield)).

This method handles receiving a mixture of leaf nodes and parent nodes, even out of order and with any tree depth.

Nodes may be passed with the [Tree.childrenProperty](#attr-treechildrenproperty) already populated with an Array of children that should also be added to the Tree, and this is automatically handled.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of TreeNode](#type-array-of-treenode) | false | — | list of nodes to link into the tree. |

### See Also

- [Tree.data](#attr-treedata)
- [Tree.modelType](#attr-treemodeltype)

---
## Method: Tree.getParentPath

### Description
Given a node, return the path to its parent. This works just like [Tree.getPath](#method-treegetpath) except the node itself is not reported as part of the path.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[String](#type-string)` — path to the node's parent

### See Also

- [Tree.getPath](#method-treegetpath)

---
## Method: Tree.getDescendantLeaves

### Description
Returns the list of all descendants of a node that are leaves. This works just like [Tree.getDescendants](#method-treegetdescendants), except folders are not part of the returned list. Folders are still recursed into, just not returned. Like [Tree.getDescendants](#method-treegetdescendants), this method can be very slow for large trees. Generally, [Tree.find](#method-treefind) in combination with [Tree.getLeaves](#method-treegetleaves) will be much faster.  
  
For load on demand trees (those that only have a partial representation client-side), this method will return only nodes that have already been loaded from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | true | — | node in question (root node is assumed if none specified) |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — List of descendants of the node that are leaves.

---
## Method: Tree.unloadChildren

### Description
Unload the children of a folder, returning the folder to the "unloaded" state.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | folder in question |

### Groups

- loadState

**Deprecated**

---
## Method: Tree.isMultiLinkTree

### Description
Returns true if this is a _multi-link_ tree - ie, one that can contain the same node in more than one place. Otherwise, returns false. The default implementation simply returns the value of the `multiLinkTree` flag

See [Tree.linkData](#attr-treelinkdata) and [ResultTree.linkDataSource](ResultTree.md#attr-resulttreelinkdatasource) for further details of multiLink trees.

---
## Method: Tree.hasChildren

### Description
Returns true if this node has any children.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Boolean](#type-boolean)` — true if the node has children

---
## Method: Tree.getNodeLocator

### Description
For a [multi-link tree](#method-treeismultilinktree), this method returns the [nodeLocator](../reference_2.md#object-nodelocator) associated with the particular occurence of the node at the specified index within the current [open list](#method-treegetopenlist) of nodes in the tree. Not applicable to non-multilink trees (always returns null)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recordIndex | [Integer](../reference_2.md#type-integer) | false | — | position of a node occurence within the open list of the tree |

### Returns

`[NodeLocator](#type-nodelocator)` — NodeLocator unambiguously identifying the specific node occurence

---
## Method: Tree.getLength

### Description
Returns the number of items in the current open list.

### Returns

`[number](#type-number)` — number of items in open list

### See Also

- [Tree.getOpenList](#method-treegetopenlist)

---
## Method: Tree.findNodeIndex

### Description
Like [Tree.findIndex](#method-treefindindex), but searches all tree nodes regardless of their open/closed state.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[int](../reference.md#type-int)` — index of the first matching Object or -1 if not found

### Groups

- access
- find

---
## Method: Tree.isInAncestorChain

### Description
Returns true if the passed-in node ID is already present in the parent's ancestor chain. This means that either the parent node itself, or its parent, grandparent, and so on, has the same ID as the one passed in. This method is used when linking new nodes into a tree, to ensure that we don't link in nodes that will lead to circular references by virtue of a node being its own parent (or its own child, depending which way round you prefer to think of it)

Note that [multi-link trees](#method-treeismultilinktree) potentially have more than one ancestor chain for any given node, so this method returns true if the parameter ID is used by any node in any of the parent's ancestor chains.

---
## Method: Tree.dataChanged

### Description
Called when the structure of this tree is changed in any way. Intended to be observed.  
  
Note that on a big change (many items being added or deleted) this may be called multiple times

**Flags**: A

---
## Method: Tree.closeAll

### Description
Close all nodes under a particular node

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[NodeLocator](#type-nodelocator) | true | — | node from which to close folders (if not specified, the root node is used). If this is a [multi-link tree](#method-treeismultilinktree), you must provide a [NodeLocator](../reference_2.md#object-nodelocator) for any node other than the root node |

---
## Method: Tree.getLoadState

### Description
What is the loadState of a given folder?

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | folder in question |

### Returns

`[LoadState](../reference.md#type-loadstate)` — state of the node

### Groups

- loadState

---
## Method: Tree.isOpen

### Description
Whether a particular node is open or closed (works for leaves and folders). Note, for [multi-link tree](#method-treeismultilinktree)s, passing a `NodeLocator` is the only unambiguous way to specify the node.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[String](#type-string)|[Integer](../reference_2.md#type-integer)|[NodeLocator](#type-nodelocator) | false | — | the node in question, or the the node's ID, or a NodeLocator object |

### Returns

`[Boolean](#type-boolean)` — true if the node is open

---
## Method: Tree.reloadChildren

### Description
Reload the children of a folder.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Groups

- loadState

### See Also

- [Tree.removeChildren](#method-treeremovechildren)

---
## Method: Tree.openFolder

### Description
Open a particular node. Note, for [multi-link tree](#method-treeismultilinktree)s, passing a `NodeLocator` is the only unambiguous way to specify the node.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[String](#type-string)|[Integer](../reference_2.md#type-integer)|[NodeLocator](#type-nodelocator) | false | — | the node to open, or its ID, or a NodeLocator object |
| callback | [Callback](../reference.md#type-callback) | true | — | Optional callback (stringMethod) to fire when loading completes. Has a single param `node` - the node whose children have been loaded, and is fired in the scope of the Tree. |

### See Also

- [ResultTree.dataArrived](ResultTree.md#method-resulttreedataarrived)

---
## Method: Tree.getRoot

### Description
Returns the root node of the tree.

### Returns

`[TreeNode](#type-treenode)` — the root node

---
## Method: Tree.getDescendantFolders

### Description
Returns the list of all descendants of a node that are folders. This works just like [Tree.getDescendants](#method-treegetdescendants), except leaf nodes are not part of the returned list. Like [Tree.getDescendants](#method-treegetdescendants), this method can be very slow for large trees. Generally, [Tree.find](#method-treefind) in combination with [Tree.getFolders](#method-treegetfolders) will be much faster.  
  
For load on demand trees (those that only have a partial representation client-side), this method will return only nodes that have already been loaded from the server.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | true | — | node in question (root node is assumed if none is specified) |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — List of descendants of the node that are folders.

---
## Method: Tree.isLoaded

### Description
For a databound tree, has this folder either already loaded its children or is it in the process of loading them.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | folder in question |

### Returns

`[Boolean](#type-boolean)` — folder is loaded or is currently loading

### Groups

- loadState

---
## Method: Tree.findById

### Description
Find the node with the specified ID. Specifically, it returns the node whose idField matches the id passed to this method. If the tree is using the "parent" modelType, this lookup will be constant-time. For all other modelTypes, the tree will be searched recursively.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | ID of the node to return. |

### Returns

`[Object](../reference.md#type-object)` — node with appropriate ID, or null if not found.

### Groups

- location

### See Also

- [Tree.idField](#attr-treeidfield)
- [Tree.find](#method-treefind)

**Flags**: A

---
## Method: Tree.add

### Description
Add a single node under the specified parent. See ["Modifying ResultTrees"](ResultTree.md#class-resulttree) when working with a `ResultTree` for limitations.

#### Adding nodes to Multi-link trees
[Multi-link trees](#attr-treemultilinktree) support ordering of nodes amongst their peers by setting the value of the [linkPositionField](#attr-treelinkpositionfield) in the associated [linkData](#attr-treelinkdata). Nodes can also be added at a specific index position in the child list via this API, but be aware that - like other kinds of [databound tree](ResultTree.md#class-resulttree) - nodes added using this API are not automatically persisted. Because of this, typically you would not use this API for a databound multi-link tree; you would instead [add a record](DataSource.md#method-datasourceadddata) to the tree's [linkDataSource](ResultTree.md#attr-resulttreelinkdatasource), and possibly also to its primary [dataSource](ResultTree.md#attr-resulttreedatasource), if this is an entirely new node that does not already exist elsewhere in the tree. [Cache synchronization](DataSource.md#method-datasourceupdatecaches) will then take care of linking the new node into the tree (or the existing node into a new position in the tree).

That said, if you do choose to use this `add()` API to add a node to a multi-link tree, the following rules are used:

*   If you specify a non-null "position" parameter on the `add()` call, that will be honored. So, for example, passing a position of 0 will always cause the new node to be inserted first in the list of its parent's children
*   If no position parameter is provided, we will attempt to insert the new node at the position implied by the value of the `linkPositionField` in the parameter "linkRecord". So if you provide a value of 5 for that field in the linkRecord, the node will be inserted immediately before the first existing node in the parent's child list that has a position value of 5 or greater
*   If there is no position parameter and no value for the `linkPositionField`, the new node will inserted at the end of the parent node's list of children

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node to add |
| parent | [String](#type-string)|[TreeNode](#type-treenode) | false | — | Parent of the node being added. You can pass in either the [TreeNode](../reference_2.md#object-treenode) itself, or a path to the node (as a String), in which case a [Tree.find](#method-treefind) is performed to find the node. |
| position | [number](#type-number) | true | — | Position of the new node in the children list. If not specified, the node will be added at the end of the list (this is not necessarily true for multi-link trees - see the discussion above) |
| linkRecord | [Record](#type-record) | true | — | Optional record containing attributes associated with the link between the nodes, rather than either of the nodes themselves. Only applicable to [multi-link trees](#attr-treemultilinktree), and only required if you want to provide a [linkPositionField](#attr-treelinkpositionfield) value |

### Returns

`[TreeNode](#type-treenode)` — The added node. Will return null if the node was not added (typically because the specified `parent` could not be found in the tree).

### See Also

- [sharingNodes](../kb_topics/sharingNodes.md#kb-topic-sharing-nodes)
- [Tree.addList](#method-treeaddlist)

---
## Method: Tree.isFolder

### Description
Determines whether a particular node is a folder. The logic works as follows:  
  

*   If the [TreeNode](../reference_2.md#object-treenode) has a value for the [Tree.isFolderProperty](#attr-treeisfolderproperty) ([TreeNode.isFolder](TreeNode.md#attr-treenodeisfolder) by default) that value is returned.
*   Next, the existence of the [Tree.childrenProperty](#attr-treechildrenproperty) (by default [TreeNode.children](TreeNode.md#attr-treenodechildren)) is checked on the [TreeNode](../reference_2.md#object-treenode). If the node has the children property defined (regardless of whether it actually has any children), then isFolder() returns true for that node.

You can override this method to provide your own interpretation of what constitutes a folder. However, you cannot change the return value for a node after the associated folder is loaded.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Boolean](#type-boolean)` — true if the node is a folder

---
## Method: Tree.getOpenList

### Description
Return a flattened list of all nodes that are visible under some parent based on whether the node itself or any folders underneath it are open. Returned list will include the passed node.

If the passed in node is a leaf, this method returns null.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[String](#type-string)|[Integer](../reference_2.md#type-integer)|[NodeLocator](#type-nodelocator) | false | — | the node in question, or the the node's ID, or a NodeLocator object. Defaults to the root node |

### Returns

`[List of TreeNode](#type-list-of-treenode)` — flattened list of open nodes

---
## Method: Tree.getPathForOpenListIndex

### Description
This method returns the path to the node at the specified index within the current open list of nodes in this tree. Note that for a node that appears in more than one place in a [multi-link tree](#method-treeismultilinktree), the returned path will be the visible path to the node in the specified index.

See [Tree.getPath](#method-treegetpath) for more information on paths for TreeNodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| recordIndex | [Integer](../reference_2.md#type-integer) | false | — | position of a node within the open list of the tree |

### Returns

`[String](#type-string)` — path to the node

---
## Method: Tree.createNodeLocator

### Description
Returns a [NodeLocator](../reference_2.md#object-nodelocator) object suitable for passing to methods, such as [Tree.getParent](#method-treegetparent), which require a `NodeLocator` when the tree is [multi-linked](#method-treeismultilinktree). Note, `NodeLocator`s are specific to multiLink trees; they are never required for regular trees.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | the child node |
| parent | [TreeNode](#type-treenode) | false | — | the parent node |
| position | [Integer](../reference_2.md#type-integer) | false | — | the child node's position within the parent |
| path | [String](#type-string) | false | — | the full path to the child node |
| openListIndex | [Integer](../reference_2.md#type-integer) | true | — | the index of the node occurence in the tree's current openList. This is the same as the record index of the node in an associated [TreeGrid](TreeGrid.md#class-treegrid) |

---
## Method: Tree.getParent

### Description
Returns the parent of this node. For [multiLink trees](#method-treeismultilinktree), you must pass in a [NodeLocator](../reference_2.md#object-nodelocator) rather than a node, otherwise it will just return the first parent, which is unlikely to be useful unless you know that this node only has one parent, or you just want to know whether the node has at least one parent. See also [Tree.getMultiLinkParents](#method-treegetmultilinkparents).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[String](#type-string)|[Integer](../reference_2.md#type-integer)|[NodeLocator](#type-nodelocator) | false | — | the node in question, or its ID, or a NodeLocator object |

### Returns

`[TreeNode](#type-treenode)` — parent of this node

---
## Method: Tree.findNextIndex

### Description
Like [Tree.findIndex](#method-treefindindex), but inspects a range from `startIndex` to `endIndex`. Note that as in [Tree.findIndex](#method-treefindindex), only open nodes are included. To include both open and closed nodes, use [Tree.findNextNodeIndex](#method-treefindnextnodeindex).

For convenience, findNextIndex() may also be called with a function (called the predicate function) for the `propertyName` parameter. In this usage pattern, the predicate function is invoked for each value of the list until the predicate returns a true value. The predicate function is passed three parameters: the current value, the current index, and the list. The value of `this` when the predicate function is called is the `value` parameter. For example:

```
var currentUserRecord = recordList.findNextIndex(0, function (record, i, recordList) {
    if (record.username == currentUsername && !record.accountDisabled) {
        return true;
    }
});
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startIndex | [int](../reference.md#type-int) | false | — | first index to consider. |
| propertyName | [String](#type-string)|[Function](#type-function)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match; or, if a function is passed, the predicate function to call; or, if an object is passed, set of properties and values to match. |
| value | [Any](#type-any) | true | — | value to compare against (if `propertyName` is a string) or the value of `this` when the predicate function is invoked (if `propertyName` is a function) |
| endIndex | [int](../reference.md#type-int) | true | — | last index to consider (inclusive). |

### Returns

`[int](../reference.md#type-int)` — index of the first matching value or -1 if not found.

### Groups

- access
- find

---
## Method: Tree.getParentsAndPositions

### Description
For [multiLink trees](#method-treeismultilinktree), returns the array of this node's direct parents and the node's position within each parent. Each entry is a record like this:
```
 [
     {parent: [reference-to-parent-node], position: [this-node's-position-within-the-parent]},
     {parent: [reference-to-parent-node], position: [this-node's-position-within-the-parent]}
 ]
 
```
For non-multiLink trees, returns null (calling this method makes no sense for non-multiLink trees).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Array of Record](#type-array-of-record)` — the parents and positions of this node

---
## Method: Tree.isLeaf

### Description
Returns true if the passed in node is a leaf.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Boolean](#type-boolean)` — true if the node is a leaf

### See Also

- [Tree.isFolder](#method-treeisfolder)

---
## Method: Tree.duplicate

### Description
Create a copy of tree. If includeData is `true`, the tree nodes are copied. Otherwise, just the tree settings and an empty root node are in the new tree.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| includeData | [boolean](../reference.md#type-boolean) | true | — | Should tree nodes be copied? |
| includeLoadState | [boolean](../reference.md#type-boolean) | true | — | Should tree node loadState be retained? |

### Returns

`[Tree](#type-tree)` — copy of tree.

### Groups

- creation

---
## Method: Tree.find

### Description
Find nodes within this tree using a string path or by attribute value(s). This method can be called with 1 or 2 arguments. If a single String argument is supplied, the value of the argument is treated as the path to the node. If a single argument of type Object is provided, it is treated as a set of field name/value pairs to search for (see [List.find](List.md#method-listfind)).  
If 2 arguments are supplied, this method will treat the first argument as a fieldName, and return the first node encountered where `node[fieldName]` matches the second argument. So for example, given this tree:
```
 foo
   zoo
     bar
   moo
     bar
 
```
Assuming your [Tree.pathDelim](#attr-treepathdelim) is the default `/` and `foo` is the name of the root node, then `tree.find("foo/moo/bar")` would return the `bar` node under the `moo` node.  
  
`tree.find("name", "bar")` would return the first `bar` node because it is the first one in the list whose `name` (default value of [Tree.nameProperty](#attr-treenameproperty)) property matches the value `bar`. The two argument usage is generally more interesting when your tree nodes have some custom unique property that you wish to search on. For example if your tree nodes had a unique field called "UID", their serialized form would look something like this:
```
 { name: "foo", children: [...], UID:"someUniqueId"}
 
```
You could then call `tree.find("UID", "someUniqueId")` to find that node. Note that the value doesn't have to be a string - it can be any valid value, but since this data generally comes from the server, the typical types are string, number, and boolean. Also note that a find() on the [Tree.idField](#attr-treeidfield) will be constant time, and that find() will not work on the idField if idField is set to a property that is not unique or not present on all nodes in the Tree.  
  
The usage where you pass a single object is interesting when your tree nodes have a number of custom properties that you want to search for in combination. Say your tree nodes had properties for "color" and "shape"; `tree.find({color: "green", shape: "circle"})` would return the first node in the tree where both properties matched.  
  
When searching by path, trailing path delimiters are ignored. So for example `tree.find("foo/zoo/bar")` is equivalent to `tree.find("foo/zoo/bar/")`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fieldNameOrPath | [String](#type-string) | false | — | Either the path to the node to be found, or the name of a field which should match the value passed as a second parameter |
| value | [Any](#type-any) | true | — | If specified, this is the desired value for the appropriate field |

### Returns

`[Object](../reference.md#type-object)` — the node matching the supplied criteria or null if not found

### Groups

- location

### See Also

- [Tree.root](#attr-treeroot)
- [Tree.pathDelim](#attr-treepathdelim)
- [Tree.nameProperty](#attr-treenameproperty)

---
## Method: Tree.getLevel

### Description
Return the number of levels deep this node is in the tree. For example, for this tree:
```
 root
   foo
     bar
 
```
Calling `tree.getLevel(bar)` will return `2`.

Note [Tree.showRoot](#attr-treeshowroot) defaults to false so that multiple nodes can be shown at top level. In this case, the top-level nodes still have root as a parent, so have level 1, even though they have no visible parents.

For [multi-link trees](#method-treeismultilinktree), passing a `TreeNode` to this method will return the level of one of that node's occurences; it is not predictable which occurence will be used. For multi-link trees, therefore, you should pass a [NodeLocator](../reference_2.md#object-nodelocator) with a path that unambiguously identifies the node occurence you are interested in

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[NodeLocator](#type-nodelocator) | false | — | node in question, or a suitable `NodeLocator` |

### Returns

`[number](#type-number)` — number of parents the node has

**Flags**: A

---
## Method: Tree.findNextNodeIndex

### Description
Like [Tree.findNextIndex](#method-treefindnextindex), but includes both open and closed nodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startIndex | [int](../reference.md#type-int) | false | — | first index to consider. |
| propertyName | [String](#type-string)|[Function](#type-function)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match; or, if a function is passed, the predicate function to call; or, if an object is passed, set of properties and values to match. |
| value | [Any](#type-any) | true | — | value to compare against (if `propertyName` is a string) or the value of `this` when the predicate function is invoked (if `propertyName` is a function) |
| endIndex | [int](../reference.md#type-int) | true | — | last index to consider (inclusive). |

### Returns

`[int](../reference.md#type-int)` — index of the first matching value or -1 if not found.

### Groups

- access
- find

---
## Method: Tree.loadChildren

### Description
Load the children of a given node.

For a databound tree this will trigger a fetch against the Tree's DataSource.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | Optional callback (stringMethod) to fire when loading completes. Has a single param `node` - the node whose children have been loaded, and is fired in the scope of the Tree. |

### Groups

- loadState

---
## Method: Tree.setChildren

### Description
Replaces the existing children of a parent node, leaving the node in the loaded state. Only a flat list of children nodes is supported, as in [Tree.addList](#method-treeaddlist).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| parent | [TreeNode](#type-treenode) | false | — | parent of children |
| newChildren | [List of TreeNode](#type-list-of-treenode) | false | — | children to be set |

### Groups

- loadState

### See Also

- [Tree.removeChildren](#method-treeremovechildren)
- [DataSource.updateCaches](DataSource.md#method-datasourceupdatecaches)

---
## Method: Tree.linkDataChanged

### Description
For [multi-link tree](#method-treeismultilinktree)s only, called when links are added to or removed form the tree. Intended to be observed.  
  
Note that on a big change (many items being added or deleted) this may be called multiple times

**Flags**: A

---
## Method: Tree.setRoot

### Description
Set the root node of the tree. Called automatically on this Tree during initialization and on the Tree returned from a call to [duplicate()](#method-treeduplicate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newRoot | [TreeNode](#type-treenode) | false | — | new root node |
| autoOpen | [boolean](../reference.md#type-boolean) | false | — | set to true to automatically open the new root node. |

---
## Method: Tree.lastIndexOf

### Description
Return the position in the list of the last instance of the specified object.

If pos is specified, starts looking before that position.

Returns -1 if not found.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to look for |
| pos | [number](#type-number) | true | — | last index to consider |
| endPos | [number](#type-number) | true | — | earliest index to consider |

### Returns

`[number](#type-number)` — position of the item, if found, -1 if not found

### Groups

- access

---
## Method: Tree.hasFolders

### Description
Return true if this this node has any children that are folders.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[Boolean](#type-boolean)` — true if the node has children that are folders

---
## Method: Tree.getAllNodes

### Description
Get all the nodes that exist in the tree under a particular node, as a flat list, in depth-first traversal order.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | true | — | optional node to start from. Default is root. |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — all the nodes that exist in the tree

---
## Method: Tree.removeList

### Description
Remove a list of nodes (not necessarily from the same parent), and all children of those nodes. See ["Modifying ResultTrees"](ResultTree.md#class-resulttree) when working with a `ResultTree` for limitations.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodeList | [List of TreeNode](#type-list-of-treenode) | false | — | list of nodes to remove |

### Returns

`[boolean](../reference.md#type-boolean)` — true if the tree was changed as a result of this call

---
## Method: Tree.closeFolders

### Description
Close a set of folders, specified by path or as pointers to nodes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodeList | [List of TreeNode](#type-list-of-treenode) | false | — | List of nodes or node paths or NodeLocators |

---
## Method: Tree.getName

### Description
Get the 'name' of a node. This is node\[[Tree.nameProperty](#attr-treenameproperty)\]. If that value has not been set on the node, the node's 'ID' value will be tried (this is node\[[Tree.idField](#attr-treeidfield)\]). If that value is not present on the node, a unique value (within this parent) will be auto-generated and returned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode)|[NodeLocator](#type-nodelocator) | false | — | node in question, or a suitable [NodeLocator](../reference_2.md#object-nodelocator) |

### Returns

`[String](#type-string)` — name of the node

---
## Method: Tree.findIndex

### Description
Like [List.findIndex](List.md#method-listfindindex), but operates only on the list of currently opened nodes. To search all loaded nodes open or closed, use [Tree.findNodeIndex](#method-treefindnodeindex).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string)|[Object](../reference.md#type-object)|[AdvancedCriteria](#type-advancedcriteria) | false | — | property to match, or if an Object is passed, set of properties and values to match |
| value | [Any](#type-any) | true | — | value to compare against (if propertyName is a string) |

### Returns

`[int](../reference.md#type-int)` — index of the first matching Object or -1 if not found

### Groups

- access
- find

---
## Method: Tree.indexOf

### Description
Return the position in the list of the first instance of the specified object.

If pos is specified, starts looking after that position.

Returns -1 if not found.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| obj | [Any](#type-any) | false | — | object to look for |
| pos | [number](#type-number) | true | — | earliest index to consider |
| endPos | [number](#type-number) | true | — | last index to consider |

### Returns

`[number](#type-number)` — position of the item, if found, -1 if not found

### Groups

- access

---
## Method: Tree.getPath

### Description
Returns the path of a node - a path has the following format: `([name][pathDelim]?)*`  
  
For example, in this tree:
```
 root
   foo
     bar
 
```
Assuming that [Tree.pathDelim](#attr-treepathdelim) is the default `/`, the `bar` node would have the path `root/foo/bar` and the path for the `foo` node would be `root/foo`.  
  
Once you have a path to a node, you can call find(path) to retrieve a reference to the node later.

**Note:** Nodes in [multi-link trees](#method-treeismultilinktree) do not have a single path, because a given node can occur in multiple places in the tree. Therefore, if you pass a `TreeNode` instance to this method, it returns the path to one occurence of the node; which particular occurence it chooses is not predictable, and there may be other paths to other occurences of the same node in the tree. The only way to obtain an unambiguous path for a particular occurence of a node is to call [Tree.getPathForOpenListIndex](#method-treegetpathforopenlistindex), passing in the position of the node occurence in the tree's openList (which will be the same as the record number of the node's visual occurence in a [treeGrid](TreeGrid.md#class-treegrid)); if the node occurence is not yet in the tree's openList - either because its parent has not yet been opened, or because the tree is in the process of being built - the tree is not able to provide a path to the node occurence. In this case, you would have to obtain the path in application code, by reference to the original [Tree.data](#attr-treedata) and [Tree.linkData](#attr-treelinkdata)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node in question |

### Returns

`[String](#type-string)` — path to the node

### See Also

- [Tree.getParentPath](#method-treegetparentpath)

---
## Method: Tree.setSeparateFolders

### Description
Setter for [Tree.separateFolders](#attr-treeseparatefolders).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| separateFolders | [Boolean](#type-boolean) | false | — | new `separateFolders` value |

---
## Method: Tree.setShowRoot

### Description
Setter for [Tree.showRoot](#attr-treeshowroot).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showRoot | [Boolean](#type-boolean) | false | — | new `showRoot` value |

---
## Method: Tree.isRoot

### Description
Return true if the passed node is the root node.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node to test |

### Returns

`[Boolean](#type-boolean)` — true if the node is the root node

---
## Method: Tree.getChildren

### Description
Returns all children of a node. If the node is a leaf, this method returns null.

For databound trees the return value could be a [ResultSet](ResultSet.md#class-resultset) rather than a simple array - so it's important to access the return value using the [List](../reference_2.md#interface-list) interface instead of as a native Javascript Array. The case that a ResultSet may be returned can only happen if the tree is a [ResultTree](ResultTree.md#class-resulttree) and the [ResultTree.fetchMode](ResultTree.md#attr-resulttreefetchmode) is set to "paged".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | The node whose children you want to fetch. |

### Returns

`[List of TreeNode](#type-list-of-treenode)` — List of children for the node, including an empty List if the node has no children. For a leaf, returns null.

### See Also

- [Tree.getChildrenResultSet](#method-treegetchildrenresultset)

---
## Method: Tree.isParent

### Description
Returns true if "parent" is the parent of "node". This is straightforward and definitive for ordinary trees, because nodes can only have one parent. In [multiLink trees](#method-treeismultilinktree), however, nodes can have multiple parents, so this method returning true only means that "parent" is _a_ parent of "node" - there may or may not be others.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | the node in question |
| parent | [TreeNode](#type-treenode) | false | — | the node to query to see if is a parent of the other node |

### Returns

`[Boolean](#type-boolean)` — true if "parent" is a parent of "node"; otherwise false

---
## Method: Tree.move

### Description
Moves the specified node to a new parent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | node to move |
| newParent | [TreeNode](#type-treenode) | false | — | new parent to move the node to |
| position | [Integer](../reference_2.md#type-integer) | true | — | Position of the new node in the children list. If not specified, the node will be added at the end of the list. |

---
## Method: Tree.allChildrenLoaded

### Description
For a databound tree, do the children of this folder form a ResultSet with a full cache.

Note that this method only applies to [ResultTree.fetchMode](ResultTree.md#attr-resulttreefetchmode) "paged".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | folder in question |

### Returns

`[Boolean](#type-boolean)` — folder's children are a ResultSet with a full cache

### Groups

- loadState

### See Also

- [Tree.getChildrenResultSet](#method-treegetchildrenresultset)

---
