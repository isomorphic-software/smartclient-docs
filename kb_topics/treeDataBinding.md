# Tree DataBinding

[← Back to API Index](../reference.md)

---

## KB Topic: Tree DataBinding

### Description
The SmartClient [TreeGrid](../classes/TreeGrid.md#class-treegrid) component is a visual representation of a tree and requires a [Tree](../classes/Tree.md#class-tree) or [ResultTree](../classes/ResultTree.md#class-resulttree) datatype passed via the [TreeGrid.data](../classes/TreeGrid.md#attr-treegriddata) attribute to initialize the tree view. The [Tree](../classes/Tree.md#class-tree) datatype is used when you want to provide all of the tree nodes in one shot at initialization time. The [ResultTree](../classes/ResultTree.md#class-resulttree) datatype is used when you want portions of the tree to be loaded on demand from the server.

#### Providing all data to the Tree at creation

The simplest mechanism by which to initialize a Tree is to simply provide all the data up-front when the Tree itself is created. Depending on the format of your tree data, this can be done by setting [Tree.root](../classes/Tree.md#attr-treeroot) or [Tree.data](../classes/Tree.md#attr-treedata). This functionality is provided by the [Tree](../classes/Tree.md#class-tree) class.

For examples of this type of databinding, see the following SDK examples:

*   *TreeGrid Initialization Example*
*   [TreeGrid Initialization with JSTL](/examples/server_integration/#jstlTree)

#### Loading Tree nodes on demand

In this mode, tree nodes are loaded on-demand the first time a user expands a folder. This approach is necessary for large trees. This functionality is provided by the [ResultTree](../classes/ResultTree.md#class-resulttree) class, which uses a [DataSource](../classes/DataSource.md#class-datasource) to load data from the server. Each DataSource Record becomes a [TreeNode](../reference.md#object-treenode).

When the user expands a folder whose children have not yet been loaded from the server (or you programmatically call openFolder() on such a node), the client automatically sends a [DSRequest](../reference.md#object-dsrequest) to the server to ask for all immediate children of that node.

If you have a dataset that is ["parent-linked"](../reference.md#type-treemodeltype), that is, every node has a unique ID (the [Tree.idField](../classes/Tree.md#attr-treeidfield)) and also has a property with the unique ID of it's parent node (the [Tree.parentIdField](../classes/Tree.md#attr-treeparentidfield)) the tree can load child nodes by simply sending a DSRequest with appropriate [Criteria](../reference.md#type-criteria). Given a parent node with ID "225" in a tree where the [Tree.parentIdField](../classes/Tree.md#attr-treeparentidfield) is called "parentId", the criteria would be:

```
    { parentId : 225 }
 
```
The client is asking the server: "give me all nodes whose parentId is 225", which are the children of node 225.

If you have a DataSource that supports simple [Criteria](../reference.md#type-criteria) like the above, and your records have nodes with ids and parentIds, this strategy can be used by just declaring the tree relationship in your DataSource: the first [DataSourceField.foreignKey](../classes/DataSourceField.md#attr-datasourcefieldforeignkey) field referring to another field in that same DataSource will be taken as the [Tree.parentIdField](../classes/Tree.md#attr-treeparentidfield), and the field to which it refers, the [Tree.idField](../classes/Tree.md#attr-treeidfield). You can use the [DataSourceField.primaryKey](../classes/DataSourceField.md#attr-datasourcefieldprimarykey) field as your [Tree.idField](../classes/Tree.md#attr-treeidfield), but it's only required that it hold unique values. Note, this only works for DataSources with a single primaryKey field; composite keys are not supported for this kind of tree databinding. See [DataSourceField.primaryKey](../classes/DataSourceField.md#attr-datasourcefieldprimarykey) for more details.

If you have a tree where there is no convenient unique ID, for example, you have mixed types of nodes (for example, departments and employees), use one of the following approaches:

1.  generate a synthetic node ID and return it with every tree node.
    
    Typically two or more properties can be combined into a String that serves as a unique ID. For example, if you are loading a mixed tree of "Departments" and "Users", each of which have unique numeric IDs, you could generate synthetic node IDs like "department:353" and "user:311". Your server-side code will then receive these synthetic node IDs when the tree loads children, and you can parse the IDs, look up the appropriate object and return its child nodes.
    
    In the case of filesystems or XML documents, you can use the full path to the file or XML element as the unique ID.
    
2.  have all properties of the parentNode [sent to the server](../classes/DataSource.md#attr-datasourcesendparentnode)
    
    If having all the properties of the parentNode would allow you to look up children, this approach may be more convenient than having to generate synthetic node IDs and parse them when looking up children.
    
    For example, with a mixed-type tree, your server-side code may be able to quickly identify the type of the parent node be looking for specific properties, and then call methods to look up children for that type of node.
    
    In this case there is no need to declare an idField or parentIdField.
    

[ResultTree](../classes/ResultTree.md#class-resulttree)s are created for you by the [TreeGrid](../classes/TreeGrid.md#class-treegrid) when you set [TreeGrid.dataSource](../classes/TreeGrid.md#attr-treegriddatasource), but you can pass an initial dataset to a databound TreeGrid by setting [TreeGrid.initialData](../classes/TreeGrid.md#attr-treegridinitialdata).

If you do not provide [TreeGrid.initialData](../classes/TreeGrid.md#attr-treegridinitialdata), the first DSRequest you receive will be a request for the nodes under root. The id of the root node of the tree is the value of the `rootValue` attribute on the [Tree.parentIdField](../classes/Tree.md#attr-treeparentidfield) of the Tree DataSource.

For examples of this type of databinding, see the following SDK examples:

*   *TreeGrid DataBinding Example*
*   [TreeGrid XML DataBinding](/examples/server_integration/#xml2JSLOD)

#### Folders and load on demand

When using load on demand, the Tree cannot simply check whether a node has children to determine whether it's a folder, and will assume all loaded nodes are folders. To avoid this, you can add a boolean field to your DataSource called "isFolder" that indicates whether a node is a folder or not. If you already have a boolean field that indicates whether a node is a folder, you can instead set [Tree.isFolderProperty](../classes/Tree.md#attr-treeisfolderproperty) to the name of that field via [TreeGrid.dataProperties](../classes/TreeGrid.md#attr-treegriddataproperties).

#### Multi-Level load on demand

The ResultTree's DSRequests ask for the immediate children of a node only (by specifying `parentId` in the criteria). Any nodes returned whose `parentId` field value is unset or matches this criterion will be added to the tree as immediate children of the node. However you are also free to return multiple levels of children. This can be done by simply returning a flat list of descendents with valid id's and parentId's, exactly as though you were initializing a multi-level tree via [Tree.data](../classes/Tree.md#attr-treedata).

Note that when receiving multiple levels of children, the ResultTree's assumption is that if any children are loaded for a parent, then that parent is considered fully loaded.

When loading children for a given parent node, the ResultTree calls [DataSource.fetchData](../classes/DataSource.md#method-datasourcefetchdata) on its DataSource. For custom code that may need to reference the parentNode or tree in some way, the parent node whose children are being loaded is available on the dsRequest instance in the DataSource flow as dsRequest.parentNode, where it can be inspected during [DataSource.transformRequest](../classes/DataSource.md#method-datasourcetransformrequest).

For an example of this feature, see the following SDK example:

*   *Multi-Level Load on Demand Example*

#### Paging large sets of children

If some nodes in your tree have a very large number of immediate children, you can enable [fetchMode:"paged"](../classes/ResultTree.md#attr-resulttreefetchmode) to load children in batches. This means that whenever the children of a folder are loaded, the `ResultTree` will set [DSRequest.startRow](../classes/DSRequest.md#attr-dsrequeststartrow) and [endRow](../classes/DSRequest.md#attr-dsrequestendrow) when requesting children from the DataSource. This includes the initial fetch of top-level nodes, which are children of the [implicit root node](../classes/Tree.md#attr-treeshowroot).

As with all paged DSRequests, the server is free to ignore startRow/endRow and simply return all children of the node. This allows the server to make on-the-fly folder-by-folder choices as to whether to use paging or just return all children. However, whenever the server returns only some children, the server must provide an accurate value for [DSResponse.totalRows](../classes/DSResponse.md#attr-dsresponsetotalrows). Note that `startRow`, `endRow`, and `totalRows` all refer to the array of siblings that are the direct children of a particular parent node (specified by the criteria or, implicitly, the root node). In particular, `totalRows` is a count of exactly how many nodes match the criteria; this is the same as how many total sibling children are available at that level.

If the server does return a partial list of children, the `ResultTree`. will create a [ResultSet](../classes/ResultSet.md#class-resultset) to represent it rather than an array, and automatically request further children as they are accessed; typically this happens because the user is scrolling around in a [TreeGrid](../classes/TreeGrid.md#class-treegrid) which is viewing the `ResultTree`. The value of [ResultTree.resultSize](../classes/ResultTree.md#attr-resulttreeresultsize) (which may be overridden via [dataPageSize](../classes/ListGrid_1.md#attr-listgriddatapagesize)) will be passed along to any created `ResultSet` as well as used directly for the initial server request for a node's children.

In this mode, the server may return multiple levels of the tree as described above ("Multi-Level load on demand"), however, by default the server is not allowed to return folders that are open, as this creates a potential performance issue: consider the case of a user scrolling rapidly into an unloaded area of the tree, skipping past many nodes that have not been loaded. If the skipped nodes might have been open parents, then the only way to know what nodes should be visible at the new scroll position is to load all skipped nodes and discover how many visible children they had.

If this performance consequence is acceptable, the restriction against returning open folders from the server may be lifted on a tree-wide basis by setting the [canReturnOpenFolders](../classes/ResultTree.md#attr-resulttreecanreturnopenfolders) property to `true` and/or on a folder-by-folder basis by setting the property named by the [canReturnOpenSubfoldersProperty](../classes/ResultTree.md#attr-resulttreecanreturnopensubfoldersproperty) to `true`. In this case, it is recommended to also set [progressiveLoading](../classes/ResultTree.md#attr-resulttreeprogressiveloading) to `true` to prevent users from causing a large number of nodes to be loaded by scrolling too far ahead in the tree.

#### Required Format for Paging

`DsResponse`s from the server for a paging ResultTree should have the format:

```
{startRow:  <n> // requested start row (index within direct siblings)
 endRow:    <m> // requested end row (index within direct siblings)
 totalRows: <p> // total rows that match the criteria (all direct siblings)
 data: [
     // would have m - n entries
     // if for any folder, "isOpen" property is true, node must have the format:
     {isOpen: true,
      children: [
          // child nodes - the server decides how many to send based on paging logic
      ],
      childCount: <q> // for paging; required if more children present than returned
     }
 ]}
 
```
Both `startRow` and `endRow` may differ from the values passed to [ResultTree.getRange](../classes/ResultTree.md#method-resulttreegetrange) (being farther apart) due to paging, and the value of `endRow` returned by the server may be less than that requested due to `totalRows` not allowing enough requested rows. **However, you must provide all requested rows if they're available - you can't return less than the full range requested just because you feel it might improve performance (or other reasons).**

If any child node is open, the rules are:

*   if a node has children, at least one must be included (we recommend at least a page) via the [childrenProperty](../classes/Tree.md#attr-treechildrenproperty), and unless they're all included, the [childCountProperty](../classes/ResultTree.md#attr-resulttreechildcountproperty) must be specified
*   if a node has no children, then either [childrenProperty](../classes/Tree.md#attr-treechildrenproperty) must be specified as the empty array, or [childCountProperty](../classes/ResultTree.md#attr-resulttreechildcountproperty) provided as 0

The [childCountProperty](../classes/ResultTree.md#attr-resulttreechildcountproperty) may be provided even if not required as long as it's consistent with the [childrenProperty](../classes/Tree.md#attr-treechildrenproperty), and both may also be optionally specified for closed nodes. **If the rule about providing children for each open node is violated, a warning will be logged and an immediate fetch issued for the missing children.** Note that in the above `DSResponse`, or in general when paging is active, you can't supply mixed levels of nodes in the data as is described in the section "Multi-Level Load on Demand" above for simpler modes of `ResultTree/Tree`.

Your server logic must choose which nodes to return as open or closed, and intelligently decide how many children to provide for open nodes, but the server should try to satisfy the requested `startRow` and `endRow` at the top level, and the architecture should ensure that the chosen page size is large enough to at least cover the maximum number of visible rows for the `TreeGrid`. One reasonable approach might be to satisfy the top level node count, but also provide the children for all nested, open nodes, counting down, until the requested node count is also met through nested children. (Under such an approach, restrictions on the number of open nodes might be needed to avoid breaking the format rules we mentioned above when the included node count gets high.)

#### Filtering
Paged ResultTrees may also be filtered like other trees (see [ResultTree.setCriteria](../classes/ResultTree.md#method-resulttreesetcriteria)). However, if [ResultTree.keepParentsOnFilter](../classes/ResultTree.md#attr-resulttreekeepparentsonfilter) is enabled then server filtering is required. To illustrate with an example, consider a case where the ResultTree has 10,000 folders at root level and where criteria applied to their children would eliminate all but 20, which happen to be at the end of the 10,000. Purely client-side logic would have to perform 10,000 fetch operations to check whether each root-level node had children before arriving at the final set of 20.

For examples of this feature, see the following SDK example:

*   *Paging for Children Example*

**NOTE:** trees with thousands of visible nodes are very difficult for end users to navigate. A **majority of the time** the best interface for showing a very large tree is to show a TreeGrid that displays just folders, adjacent to a ListGrid that shows items within those folders.

For example, the data in your email account can be thought of as an enormous tree of folders (Inbox, Sent, Drafts, Trash etc) with thousands of messages in each folder. However, none of the common email clients display email this way; all of them choose to show folders and messages separately, as this is clearly more usable.

Before starting on implementing paging within sets of children, carefully consider whether an interface like the above, or some entirely different interface, is actually a superior option. It is exceedingly rare that paging within sets of children is the best choice.

### Related

- [DSRequest.keepParentsOnFilter](../classes/DSRequest.md#attr-dsrequestkeepparentsonfilter)
- [ResultTree.data](../classes/ResultTree.md#attr-resulttreedata)
- [ResultTree.fetchMode](../classes/ResultTree.md#attr-resulttreefetchmode)
- [ResultTree.resultSize](../classes/ResultTree.md#attr-resulttreeresultsize)
- [ResultTree.keepParentsOnFilter](../classes/ResultTree.md#attr-resulttreekeepparentsonfilter)
- [TreeGrid.keepParentsOnFilter](../classes/TreeGrid.md#attr-treegridkeepparentsonfilter)
- [TreeGrid.dataFetchMode](../classes/TreeGrid.md#attr-treegriddatafetchmode)

---
