# ResultTree Documentation

[← Back to API Index](../reference.md)

---

## Class: ResultTree

*Inherits from:* [Tree](Tree.md#class-tree)

### Description
ResultTrees are an implementation of the [Tree](Tree.md#class-tree) API, used to handle hierarchical data, whose nodes are DataSource records which are retrieved from a server.

**Modifying ResultTrees**

`ResultTree` nodes cannot be directly added or removed from a [paged](#attr-resulttreefetchmode) `ResultTree` via [Tree](Tree.md#class-tree) APIs such as [Tree.add](Tree.md#method-treeadd) or [Tree.remove](Tree.md#method-treeremove), since such trees are considered to be read-only by virtue of containing [ResultSet](ResultSet.md#class-resultset)s, which are read-only data structures. Even in other [FetchMode](../reference_2.md#type-fetchmode)s, calling such APIs will only update the local cache of the ResultTree, rather than triggering any server traffict to update the DataSource.

Use [DataSource.addData](DataSource.md#method-datasourceadddata)/[removeData()](DataSource.md#method-datasourceremovedata) to add/remove rows from the [DataSource](DataSource.md#class-datasource), and the `ResultTree` will reflect the changes automatically. Alternatively, the [DataSource.updateCaches](DataSource.md#method-datasourceupdatecaches) method may be called to only update local caches of the DataSource in question, without generating any server traffic.

To create a locally modifiable cache of records from a DataSource, you can use [DataSource.fetchData](DataSource.md#method-datasourcefetchdata) to retrieve a List of records which can be modified directly, or you can create a client-only [DataSource](DataSource.md#class-datasource) from the retrieved data to share a modifiable cache between several DataBoundComponents.

---
## Attr: ResultTree.serverKeepParentsOnFilter

### Description
If true, indicates that your own server code will handle the complexities associated with the combination of [keepParentsOnFilter](#attr-resulttreekeepparentsonfilter) and [loadDataOnDemand](#attr-resulttreeloaddataondemand). If this flag is true and your server code does _not_ handle those complexities, the results are undefined, but most likely you will simply exclude non-matching parents if your tree is load-on-demand, which effectively means that filtering will be broken.

If this flag is not set, SmartClient will use its own automatic client-driven algorithm to ensure that `keepParentsOnFilter` is honored on load-on-demand trees. See the `keepParentsOnFilter` overview for details

**Flags**: IRW

---
## Attr: ResultTree.sendNullParentInLinkDataCriteria

### Description
For [multi-link tree](Tree.md#method-treeismultilinktree)s only, should we send up the [parentId](Tree.md#attr-treeparentidfield) in fetch criteria if the criteria value is null? If false, we remove the `parentId` from the criteria when [fetching link data](#attr-resulttreelinkdatasource), **if** the criteria value is null (as it will be by default when fetching the direct child nodes of the tree's root).

Ignored for non-multiLink trees.

### Groups

- multiLinkTree

**Flags**: IR

---
## Attr: ResultTree.autoOpen

### Description
Which nodes should be opened automatically - applied whenever [setRoot()](Tree.md#method-treesetroot) is called, including during initialization and as part of a re-fetch caused, for example, by [duplicate()](Tree.md#method-treeduplicate) or [invalidateCache()](#method-resulttreeinvalidatecache).

Options are:

*   "none" - no nodes are opened automatically
*   "root" - opens the [top-level node](#attr-resulttreerootnode) - in databound trees, this node is always hidden
*   "all" - when [loading data on demand](#attr-resulttreeloaddataondemand), opens the [top-level node](#attr-resulttreerootnode) and all of it's direct descendants - otherwise, opens all loaded nodes

**Flags**: IRW

---
## Attr: ResultTree.matchingLeafJoinDepth

### Description
This property allows you to specify the number of ancestor levels SmartClient attempts to retrieve with each request, when using the built-in support for [keepParentsOnFilter](#attr-resulttreekeepparentsonfilter) on [loadDataOnDemand](#attr-resulttreeloaddataondemand) trees. See the `keepParentsOnFilter` overview for details.

**Flags**: IRW

---
## Attr: ResultTree.autoPreserveOpenState

### Description
Controls what happens to the ["open state"](#method-resulttreegetopenstate) - the set of nodes opened or closed by the end user after tree data is loaded - when an entirely new tree of nodes is loaded from the server, as a consequence of calling [ResultTree.invalidateCache](#method-resulttreeinvalidatecache) or of changing criteria such that the current cache of nodes is dropped.

**Flags**: IRW

---
## Attr: ResultTree.canReturnOpenFolders

### Description
When using [fetchMode:"paged"](../reference_2.md#type-fetchmode) and providing multiple levels of the tree in one DSResponse, this property specifies the default value assumed for the [ResultTree.canReturnOpenSubfoldersProperty](#attr-resulttreecanreturnopensubfoldersproperty) when no value for that property is provided for a node.

**Flags**: IR

---
## Attr: ResultTree.disableCacheSync

### Description
By default when the data of this ResultTree's dataSource is modified, the ResultTree will be updated to display these changes. Set this flag to true to disable this behavior.

### Groups

- cacheSync

**Flags**: IRA

---
## Attr: ResultTree.linkDataFetchMode

### Description
The fetch mode for this tree's link data; ignored if this is not a [multi-link tree](Tree.md#method-treeismultilinktree)

### Groups

- multiLinkTree

**Flags**: IR

---
## Attr: ResultTree.useSimpleCriteriaLOD

### Description
Whether or not we should skip promotion of a simple criteria to an [AdvancedCriteria](../reference.md#object-advancedcriteria) when sending the [DSRequest](../reference_2.md#object-dsrequest) to load the children of a node in a [ResultTree.loadDataOnDemand](#attr-resulttreeloaddataondemand) or [fetchMode:"paged"](#attr-resulttreefetchmode) `ResultTree`. If the [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) is not "exact", we normally convert the simple criteria to an [AdvancedCriteria](../reference.md#object-advancedcriteria) for correctness in matching the node name, but setting this property to `true` will allow that to be skipped for backcompat with older releases.

### See Also

- [TreeGrid.autoFetchTextMatchStyle](TreeGrid.md#attr-treegridautofetchtextmatchstyle)
- [DataSource.defaultTextMatchStyle](DataSource.md#attr-datasourcedefaulttextmatchstyle)

**Flags**: IRWA

---
## Attr: ResultTree.loadDataOnDemand

### Description
Does this resultTree load data incrementally as folders within the tree are opened, or is it all loaded in a single request? Must be true if [ResultTree.fetchMode](#attr-resulttreefetchmode) is "paged"

See the [keepParentsOnFilter](#attr-resulttreekeepparentsonfilter) overview for special considerations when filtering a load-on-demand tree

### See Also

- [TreeGrid.loadDataOnDemand](TreeGrid.md#attr-treegridloaddataondemand)
- [ResultTree.useSimpleCriteriaLOD](#attr-resulttreeusesimplecriterialod)

**Flags**: IR

---
## Attr: ResultTree.fetchMode

### Description
Mode of fetching records from server.

fetchMode:"local" implies that local filtering will always be performed. See [ResultTree.keepParentsOnFilter](#attr-resulttreekeepparentsonfilter) for additional filtering details.

fetchMode:"basic" or "paged" implies that if search criteria change, the entire tree will be discarded and re-fetched from the server. When retrieving the replacement tree data, the default behavior will be to preserve the [openState](#method-resulttreegetopenstate) for any nodes that the server returns which were previously opened by the user. Note that this implies that if [ResultTree.loadDataOnDemand](#attr-resulttreeloaddataondemand) is enabled and the server returns only root-level nodes, open state will be preserved only for root-level nodes, and children of open root-level nodes will be immediately fetched from the server if they are not included in the server's initial response.

fetchMode:"paged" enables paging for nodes that have very large numbers of children. Whenever the children of a folder are loaded, the `resultTree` will set [DSRequest.startRow](DSRequest.md#attr-dsrequeststartrow) and [endRow](DSRequest.md#attr-dsrequestendrow) when requesting children from the DataSource, and will manage loading of further children on demand, similar to how a [ResultSet](ResultSet.md#class-resultset) manages paging for lists. For a deeper discussion see the **Paging large sets of children** section of the [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) overview.

### Groups

- treeDataBinding

### See Also

- [ResultTree.loadDataOnDemand](#attr-resulttreeloaddataondemand)
- [ResultTree.useSimpleCriteriaLOD](#attr-resulttreeusesimplecriterialod)

**Flags**: IR

---
## Attr: ResultTree.linkDataFetchOperation

### Description
The [operationId](DSRequest.md#attr-dsrequestoperationid) this `ResultTree` should use when performing fetch operations on its [ResultTree.linkDataSource](#attr-resulttreelinkdatasource). Has no effect if this is not a [multi-link tree](Tree.md#method-treeismultilinktree)

Note, this value can be overridden by [DSRequest.linkDataFetchOperation](DSRequest.md#attr-dsrequestlinkdatafetchoperation) when calling `fetchData()` on the component (e.g. [TreeGrid.fetchData](TreeGrid.md#method-treegridfetchdata)) directly from application code.

### Groups

- multiLinkTree

**Flags**: IRW

---
## Attr: ResultTree.linkDataAddOperation

### Description
The [operationId](DSRequest.md#attr-dsrequestoperationid) this `ResultTree` should use when performing add operations on its [ResultTree.linkDataSource](#attr-resulttreelinkdatasource). Has no effect if this is not a [multi-link tree](Tree.md#method-treeismultilinktree).

Note, this property wll be used by internal update operations when you drag-move or drag-reparent nodes in a multi-link tree. Do not use it when adding records from application code by directly calling `addData()` on the [linkDataSource](#attr-resulttreelinkdatasource); instead just use the regular `operationId` property in your add request. Also note, because this property is intended to allow your code to influence the operationId used by internal methods, and those methods never directly update link data (moved and re-parented links are always removed and then re-added), there is no corresponding `linkDataUpdateOperation` property.

### Groups

- multiLinkTree

**Flags**: IRW

---
## Attr: ResultTree.resultSize

### Description
How many tree nodes to retrieve at once from each large set of children in the tree.

Applicable only with `fetchMode: "paged"`. When a paged ResultTree is asked for rows that have not yet been loaded, it will fetch adjacent rows that are likely to be required soon, in batches of this size.

### Groups

- treeDataBinding

**Flags**: IRA

---
## Attr: ResultTree.autoUpdateSiblingNodesOnDrag

### Description
For [multi-link trees](Tree.md#method-treeismultilinktree), indicates that we should automatically update the [position](Tree.md#attr-treelinkpositionfield) values of old and new sibling records after a drag reparent or reposition-within-parent operation. For example, say you have a tree like this (where the number in parentheses indicates the node's [position](Tree.md#attr-treelinkpositionfield) value):
```
      A
        - B (1)
        - C (2)
        - D (3)
      E
        - F (1)
        - G (2)
```
and you drag node C out and drop it between nodes F and G. This drag operation will spawn two update operations to the server: a "remove" to delete node C from parent A, and an "add" to re-add it under parent E. With `autoUpdateSiblingNodesOnDrag` in force, we also automatically issue two "update" operations to the server - one to change the position on node D to 2, and another to change the position on node G to 3. The end result of this is that node position values are kept correct.

Please note the following:

*   As noted above, these automatic updates are persistent - we send a queue of actual update requests to the server. This is convenient, but it may not be terribly efficient, particularly if you have just dropped a node at the head of a list of several hundred siblings. This is why we do not default this setting to true
*   The automatic updates work by applying an integer delta value to the existing position value. So in the above example, we would compute a delta of negative 1 for node D and positive 1 for node G. The upshot of this is that `autoUpdateSiblingNodesOnDrag` only works well if your position values are consecutive integers

### Groups

- multiLinkTree

**Flags**: IR

---
## Attr: ResultTree.childCountProperty

### Description
When using [fetchMode:"paged"](../reference_2.md#type-fetchmode) and providing multiple levels of the tree in one DSResponse, `childCountProperty` must be set for any folders that include only a partial list of children. For a deeper discussion see the **Paging large sets of children** section of the [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding) overview.

**Flags**: IR

---
## Attr: ResultTree.linkDataSource

### Description
This property allows you to specify the dataSource to be used for fetching link information in a databound _multilink_ tree. A multilink tree is one where the same node is allowed to appear in multiple places in the tree, and it is achieved by providing the node data and the link data separately. Nodes are provided via the normal [dataSource](#attr-resulttreedatasource); `linkDataSource` is only used for fetching and updating link information.

The `linkDataSource` is an ordinary [DataSource](DataSource.md#class-datasource) that you implement just like any other. However, for correct operation as a `linkDataSource`, it must have the following:

*   A [primaryKey field](DataSourceField.md#attr-datasourcefieldprimarykey). Like any dataSource, a `linkDataSource` is not fully functional without a `primaryKey` field
*   A field named the same as the [Tree.parentIdField](Tree.md#attr-treeparentidfield)
*   A field named the same as the [Tree.idField](Tree.md#attr-treeidfield)
*   Optionally, a field named the same as the [Tree.linkPositionField](Tree.md#attr-treelinkpositionfield)
*   Fields for other values you may wish to store with the link, if any

#### Providing node data and link data
Consider a structure for the components of a bicycle, greatly simplified:
```
         Frame
        /    \
     Wheel   Wheel
    /  \     /  \
  Hub Tire  Hub Tire
 
```
Here, the two wheels are the same assembly, so really it should look like this:
```
       Frame
        | |               
       Wheel
       /   \     
     Hub  Tire 
 
```
Normal SmartClient trees cannot model this arrangement accurately because this is not really a tree, it is a graph; trees do not contain multiple paths to a given node. The only way to handle this arrangement of nodes in a formal tree would be to make two copies of the "Wheel" node, at which point they are no longer the same thing. Either way, in a [TreeGrid](TreeGrid.md#class-treegrid), we would have to visualise it like this:
```
 
   Frame
      Wheel
         Hub
         Tire
      Wheel
         Hub
         Tire
 
```
But if we use copies so that the the two wheels are no longer the same thing, changing one of them will no longer change the other, which is a fundamental problem because in this scenario, the two wheels really are the same thing. Now, changing the name of the "Hub" in one "Wheel" would not change it in the other; adding a "Spokes" node to the second item would not also add it to the first. Drag-reordering child nodes in one "Wheel" would not re-order them in the other. All of these things are incorrect, because the two wheels are the same thing.

Multilink trees provide a way to handle this arrangement without physical copying of the duplicate nodes, preserving the sameness of them and thus fixing all the problems described above.

The node data for the above tree, simplified, would be a flat list something like this:

```
   [
      { id: 1, description: "Frame" },
      { id: 2, description: "Wheel" },
      { id: 3, description: "Hub" },
      { id: 4, description: "Tire" }
   ]
 
```
The link data would look like this:
```
   [
      { linkId: 1, parentId: 1, id: 2, position: 1 },
      { linkId: 2, parentId: 2, id: 3, position: 1 },
      { linkId: 3, parentId: 2, id: 4, position: 2 },
      { linkId: 4, parentId: 1, id: 2, position: 2 }
   ]
 
```
Or, if you were using [ResultTree.linkDataFetchMode](#attr-resulttreelinkdatafetchmode) "single", you would combine the node and link data into a single dataset like this:
```
   [
      { id: 1, position: 0, description: "Frame" },
      { parentId: 1, id: 2, position: 1, description: "Wheel", linkId: 1 },
      { parentId: 2, id: 3, position: 1, description: "Hub", linkId: 2 },
      { parentId: 2, id: 4, position: 2, description: "Tire", linkId: 3 },
      { parentId: 1, id: 2, position: 2, description: "Wheel", linkId: 4 }
   ]
```

**NOTE:** It is also possible to create an unbound multilink tree - see [Tree.linkData](Tree.md#attr-treelinkdata).

**Flags**: IR

---
## Attr: ResultTree.data

### Description
Optional initial data for the tree. If the [fetchMode](#attr-resulttreefetchmode) is `"basic"` or `"local"` then the format of this data is exactly the same [parentId](Tree.md#attr-treeparentidfield)-linked list of tree nodes as documented on [Tree.data](Tree.md#attr-treedata) (when the `modelType` is set to `"parent"`). If the `fetchMode` is `"paged"` then the format is extended to allow the [childCountProperty](#attr-resulttreechildcountproperty) to be set on folder nodes.

Providing an initial set of nodes in this way does not affect the behavior of the ResultTree in its loading of unloaded folders. An equivalent result is achieved if the first fetch from the server returns this same data.

If `fetchMode` is `"paged"` then you may make folder-by-folder choices as to whether to use paging for the childen of each folder. If you would like to use paging in a folder then you may include a partial list of that folder's children with the data, provided that you set the `childCountProperty` to the total number of children. Otherwise you will need to include either all children of the folder or none of the children. Open folders without any children provided will cause immediate, new fetches for the children, as usual.

Because the initial data is treated exactly as though it were returned from the tree's first server fetch, the order of the initial data must match the initial sort order of the TreeGrid displaying the data or, if no such sort is specified, the native storage order on the server. For example, consider initial data containing `n` records having the `parentId` `"X"`, meaning they are all in the same folder. These `n` records are the records at indices `0` through `(n - 1)` that are stored on the server under the parent node. If the `childCountProperty` set on the parent node indicates that there are `m > n` total rows under the parent node then the records at indices `n` to `(m - 1)` will be fetched from the server as the user scrolls the additional rows into view.

### Groups

- treeDataBinding

### See Also

- [Tree.data](Tree.md#attr-treedata)
- [TreeNode](../reference_2.md#object-treenode)

**Flags**: IRA

---
## Attr: ResultTree.serverFilterFields

### Description
For [fetchMode:"local"](../reference_2.md#type-fetchmode) ResultTrees, this property lists field names that will be sent to the server if they are present in the criteria.

This property may be used to ensure a dataSource receives the necessary criteria to populate a ResultTree's data, and also support [ResultTree.keepParentsOnFilter](#attr-resulttreekeepparentsonfilter).

Note that for some AdvancedCriteria it will not be possible to extract the subcriteria that apply to certain fields. See [DataSource.splitCriteria](DataSource.md#method-datasourcesplitcriteria) for details on how serverFilterFields-applicable subcriteria are extracted from the specified criteria for the tree.

**Flags**: IR

---
## Attr: ResultTree.keepParentsOnFilterMaxNodes

### Description
When a tree specifies the combination of [keepParentsOnFilter](#attr-resulttreekeepparentsonfilter) and [loadDataOnDemand](#attr-resulttreeloaddataondemand), SmartClient by default automatically fetches the "skeleton" of the filtered tree - see the `keepParentsOnFilter` overview for details, including the definition of "skeleton" and other relevant terminology

A problem can arise with this approach if the user enters overly inclusive filter criteria. For example, say you have a 200,000 row dataset and the user chooses to apply a filter of "a". Chances are that is going to include the majority of the nodes in the tree, which would be OK because this is a load-on-demand tree. However, because we will build, cache and then pass around the list of id's of the dangling parents, this may become a performance issue. A lot depends on the nature of your data - this will be much less of an issue for shallow trees with lots of leaf nodes relative to parents, compared to deep trees with a lot of dangling parents to record.

If the user tries to filter the TreeGrid such that there are more matching nodes than is allowed by this setting, the system will truncate the fetch and show the warning message defined in [RPCManager.keepParentsOnFilterMaxNodesExceededMessage](RPCManager.md#classattr-rpcmanagerkeepparentsonfiltermaxnodesexceededmessage). Since the cached node-list is derived from bottom to top, this truncation of the fetch process will usually mean we have not yet derived any top-level nodes. This in turn means that the tree will appear to be empty.

Setting this property to a suitable value for your specific use case is an application tuning exercise, finding the right balance between usability and performance. To remove the node limit altogether, set this property to -1. However, if you have a load-on-demand tree over a large dataset, we do not recommend that you remove the limit completely, as it can lead to serious problems on both the client and server, as the application tries to cope with criteria that contains huge numbers of id's.

**Flags**: IRW

---
## Attr: ResultTree.criteria

### Description
The filter criteria to use when fetching rows. For usage see [ResultTree.setCriteria](#method-resulttreesetcriteria).

**Flags**: IRW

---
## Attr: ResultTree.defaultNewNodesToRoot

### Description
This attribute governs how to handle cache-synch when a new node is added to this dataSource with no explicit parentId.

If set to `true`, when a new node is added to this dataSource via [DataSource.addData](DataSource.md#method-datasourceadddata), with no explicit parentId, the node will be added as a child of the root node of this result tree. Otherwise it will be ignored.

Similar logic applies to [updated nodes](DataSource.md#method-datasourceupdatedata) - if this property is true and the parentId of an updated node is cleared, it will be moved to become a child of root, otherwise it will be dropped from the tree.

**Flags**: IRWA

---
## Attr: ResultTree.updateCacheFromRequest

### Description
When a successful Add, Update or Remove type operation fires on this ResultTree's dataSource, if [DSResponse.data](DSResponse.md#attr-dsresponsedata) is unset, should we integrate the submitted data values (from the request) into our data-set?

### Groups

- cacheSync

**Flags**: IRA

---
## Attr: ResultTree.modelType

### Description
Selects the model used to construct the tree representation. See [TreeModelType](../reference.md#type-treemodeltype) for the available options and their implications.

If the "parent" modelType is used, you can provide the initial parent-linked data set to the tree via the [Tree.data](Tree.md#attr-treedata) attribute. If the "children" modelType is used, you can provide the initial tree structure to the Tree via the [Tree.root](Tree.md#attr-treeroot) attribute.

### See Also

- [Tree.data](Tree.md#attr-treedata)
- [Tree.root](Tree.md#attr-treeroot)

**Flags**: IRWA

---
## Attr: ResultTree.canReturnOpenSubfoldersProperty

### Description
When using [fetchMode:"paged"](../reference_2.md#type-fetchmode) and providing multiple levels of the tree in one DSResponse, `canReturnOpenSubfoldersProperty` may be set on any folder to indicate whether child folders might be returned by the server already open. If the property is set to false on a folder then subfolders of that folder are never allowed to be returned already open. This enables the paging mechanism to be more efficient in the amount of data that it requests from the server.

For example, setting the `canReturnOpenSubfoldersProperty` value to `false` on a node is appropriate if the server-side code determines that the the node's children consist of entirely leaf nodes.

### See Also

- [ResultTree.canReturnOpenFolders](#attr-resulttreecanreturnopenfolders)

**Flags**: IR

---
## Attr: ResultTree.implicitCriteria

### Description
Criteria that are never shown to or edited by the user and are cumulative with any criteria provided via [DataBoundComponent.initialCriteria](DataBoundComponent.md#attr-databoundcomponentinitialcriteria), [ResultTree.setCriteria](#method-resulttreesetcriteria) etc.

**Flags**: IRW

---
## Attr: ResultTree.defaultIsFolder

### Description
Controls whether nodes are assumed to be folders or leaves by default.

Nodes that have children or have the [isFolderProperty](Tree.md#attr-treeisfolderproperty) set to true will always be considered folders. Other nodes will be considered folders or leaves by default according to this setting.

If `defaultIsFolder` is unset, the ResultTree will automatically set it to match the value of [ResultTree.loadDataOnDemand](#attr-resulttreeloaddataondemand). This means that, when using folder-by-folder load on demand (`loadDataOnDemand:true`), by default a newly loaded node will be considered to be a folder that has not loaded its children yet.

When not using folder-by-folder load on demand, by default a newly loaded node is considered a leaf. If you set `defaultIsFolder:true` explicitly, by default a newly loaded node is considered to be a folder with no children.

See [Tree.isFolder](Tree.md#method-treeisfolder) for details on how to explicitly mark nodes as folders or leaves.

### See Also

- [TreeGrid.loadDataOnDemand](TreeGrid.md#attr-treegridloaddataondemand)

**Flags**: IR

---
## Attr: ResultTree.linkDataRemoveOperation

### Description
The [operationId](DSRequest.md#attr-dsrequestoperationid) this `ResultTree` should use when performing remove operations on its [ResultTree.linkDataSource](#attr-resulttreelinkdatasource). Has no effect if this is not a [multi-link tree](Tree.md#method-treeismultilinktree).

See [ResultTree.linkDataAddOperation](#attr-resulttreelinkdataaddoperation) for more information on how this property is intended to be used.

### Groups

- multiLinkTree

**Flags**: IRW

---
## Attr: ResultTree.firstPositionValue

### Description
If [ResultTree.autoUpdateSiblingNodesOnDrag](#attr-resulttreeautoupdatesiblingnodesondrag) is in force, this is the value we will use to auto-update the position of a node when we cannot derive that value from the existing value of a neighbor. This happens when a node is dropped into the very first position below a parent (including the special case of the parent being previously empty)

### Groups

- multiLinkTree

**Flags**: IRW

---
## Attr: ResultTree.rootNode

### Description
This attribute may be used to specify a root value for the parentIdField of this resultTree. This overrides the default [DataSourceField.rootValue](DataSourceField.md#attr-datasourcefieldrootvalue) for this tree, allowing a component to navigate a tree starting at a specific node.

May be overridden via [TreeGrid.treeRootValue](TreeGrid.md#attr-treegridtreerootvalue) for ResultTrees generated by a TreeGrid component.

**Flags**: IR

---
## Attr: ResultTree.keepParentsOnFilter

### Description
If set, tree-based filtering is performed such that parent nodes are kept as long as they have children that match the filter criteria, even if the parents themselves do not match the filter criteria. If not set, filtering will exclude parent nodes not matching the criteria, and all nodes below them in the tree.

If some criteria _must_ be sent to the server in order to produce a valid tree of data, but `keepParentsOnFilter` is also required, the [ResultTree.serverFilterFields](#attr-resulttreeserverfilterfields) attribute may be used to specify a list of field names that will be sent to the server whenever they are present in the criteria. Note that for the subset of criteria applied to these fields, `keepParentsInFilter` behavior will not occur without custom logic in the DataSource fetch operation.

If [FetchMode](../reference_2.md#type-fetchmode) is explicitly set to `"paged"`, it is not possible to implement `keepParentsOnFilter`, either by local filtering or with the automatic client-driven handling mentioned below. Support for `keepParentsOnFilter` for a paged ResultTree therefore also requires custom logic in the DataSource fetch operation. To support this a developer must ensure that their fetch operation returns the appropriate set of nodes - all nodes that match the specified criteria plus their ancestor nodes even if they do not match the specified criteria.

#### keepParentsOnFilter with load-on-demand trees
The combination of `keepParentsOnFilter` and [loadDataOnDemand](#attr-resulttreeloaddataondemand) presents additional difficulties that require special handling. The problem is that in order to determine even the top-level folders, you have to examine every node in the entire tree. For example, say there is one top-level folder that has thousands of folders and nodes underneath it, and there is just one leaf node, 6 levels deep, that matches the filter criteria. You have to find out about that node, because it implies the top-level folder must be retained.

So the server basically has to examine every node in the dataset to determine even what shows up at the top level of the tree. If it does not do this, parent nodes that don't match the filter criteria will be excluded from the tree, with the upshot that the child nodes that _do_ match the criteria will be inaccessible because nodes in load-on-demand trees are only loaded when their parent node is opened

By default, SmartClient solves this with a client-driven implementation of this special handling. This algorithm involves finding the nodes that match the filter criteria - which we term **matching leaves** - and then recursively travelling back up the tree, determining the ancestors of the matching leaves - the so-called **dangling parents**. When we have traversed all the way back to the root node from every matching leaf, we have recorded every dangling parent and have what we term the **skeleton** of the tree. The skeleton is then added to fetch criteria whenever a load-on-demand fetch request is made, ensuring that we fetch both dangling parents and matching leaves.

There are three ways this recursive traversal can be implemented:

*   For dataSources that [support dynamic tree joins](DataSource.md#method-datasourcesupportsdynamictreejoins), we use the [additionalOutputs](DSRequest.md#attr-dsrequestadditionaloutputs) feature to declare self-joins that fetch multiple levels of parent in one query (the number of levels is configurable, see [ResultTree.matchingLeafJoinDepth](#attr-resulttreematchingleafjoindepth)). Of SmartClient's built-in DataSource types, only SQLDataSource is currently capable of this approach
*   For server-side dataSources that do not support self-joins, we combine individual single-level fetches into a [queue](RPCManager.md#classmethod-rpcmanagersendqueue), using [fieldValueExpressions](DSRequest.md#attr-dsrequestfieldvalueexpressions) with [responseData "allRecords"](DSRequestModifier.md#attr-dsrequestmodifiervalue) so that each fetch in the queue uses the output of the previous fetch as its criteria (so the first fetch returns the parents of the matching nodes, the second fetch returns the parents of those nodes, and so on). Again, the number of fetches per queue can be configured with the `matchingLeafJoinDepth` property. This approach works for any server-side DataSource implementation, including your own custom implementations
*   For [client-side](DataSource.md#attr-datasourceclientonly) dataSources, which support neither self-joins not queueing, the algorithm simply makes as many single-level requests as necessary to build the entire skeleton. Note, this is exactly what would happen with previously-mentioned queueing approach, if you set `matchingLeafJoinDepth` to 1

If you want to disable the automatic handling of `keepParentsOnFilter` on load-on-demand trees, see [ResultTree.serverKeepParentsOnFilter](#attr-resulttreeserverkeepparentsonfilter)

### Groups

- treeDataBinding

### See Also

- [ResultTree.keepParentsOnFilterMaxNodes](#attr-resulttreekeepparentsonfiltermaxnodes)

**Flags**: IR

---
## Attr: ResultTree.progressiveLoading

### Description
Sets [progressive loading mode](DataSource.md#attr-datasourceprogressiveloading) for this ResultTree. The ResultTree will copy this setting onto the [DSRequest](../reference_2.md#object-dsrequest)s that it issues, overriding the OperationBinding- and DataSource-level settings, in cases where the use of progressive loading does not affect the correctness of the tree's paging algorithm.

This setting is applied automatically by [DataBoundComponent](../reference.md#interface-databoundcomponent)s that have their own explicit setting for [progressiveLoading](DataBoundComponent.md#attr-databoundcomponentprogressiveloading).

**Note:** This property only has an effect for [fetchMode:"paged"](../reference_2.md#type-fetchmode) ResultTrees.

### Groups

- progressiveLoading

### See Also

- [DataSource.progressiveLoading](DataSource.md#attr-datasourceprogressiveloading)
- [OperationBinding.progressiveLoading](OperationBinding.md#attr-operationbindingprogressiveloading)
- [DSRequest.progressiveLoading](DSRequest.md#attr-dsrequestprogressiveloading)
- [DataBoundComponent.progressiveLoading](DataBoundComponent.md#attr-databoundcomponentprogressiveloading)

**Flags**: IRW

---
## Attr: ResultTree.discardParentlessNodes

### Description
When data is loaded from the server, should nodes with an explicit value for the [Tree.parentIdField](Tree.md#attr-treeparentidfield) which doesn't map to a valid parent node be dropped? If set to false, for [TreeGrid.loadDataOnDemand](TreeGrid.md#attr-treegridloaddataondemand):false trees, parentless nodes will be added as children of the root node - for [TreeGrid.loadDataOnDemand](TreeGrid.md#attr-treegridloaddataondemand):true, they will be added as children of the folder currently requesting children.

This effectively allows nodes to be loaded into the current (or root) folder without needing an explicit [parentIdField value](Tree.md#attr-treeparentidfield) that matches the folder's ID or `rootValue` for the resultTree.

Note: For `loadDataOnDemand:false` trees, if this property is unset at init time, it will default to `true` if an explicit [ResultTree.rootNode](#attr-resulttreerootnode) has been specified. This ensures that if the data tree retrieved from the server includes ancestors of the desired root-node we don't display them. Otherwise this property always defaults to false.

**Flags**: IRA

---
## Attr: ResultTree.dataSource

### Description
What [DataSource](DataSource.md#class-datasource) is this resultTree associated with?

### Groups

- databinding

**Flags**: IR

---
## Method: ResultTree.willFetchData

### Description
Will changing the criteria for this resultTree require fetching new data from the server or can the new criteria be satisfied from data already cached on the client?

This method can be used to determine whether [TreeGrid.fetchData](TreeGrid.md#method-treegridfetchdata) or [TreeGrid.filterData](TreeGrid.md#method-treegridfilterdata) will cause a server side fetch when passed a certain set of criteria.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | new criteria to test. |

### Returns

`[Boolean](#type-boolean)` — true if server fetch would be required to satisfy new criteria.

---
## Method: ResultTree.setCriteria

### Description
Set the filter criteria to use when fetching rows.

Depending on the result of [ResultTree.compareCriteria](#method-resulttreecomparecriteria) and setting for [ResultTree.fetchMode](#attr-resulttreefetchmode), setting criteria may cause a trip to the server to get a new set of nodes, or may simply cause already-fetched nodes to be re-filtered according to the new criteria.

For a basic overview on when server fetches are generally performed, see [ResultTree.fetchMode](#attr-resulttreefetchmode). However, this is not the final determination of when server fetches occur. Criteria can be split into local criteria and server criteria by specifying [ResultTree.serverFilterFields](#attr-resulttreeserverfilterfields). Thus, even when using fetchMode:"local" a new server fetch will occur if the server criteria changes. For details on how the criteria is split, see [DataSource.splitCriteria](DataSource.md#method-datasourcesplitcriteria).

Note: if criteria is being split to retrieve server criteria portion and the criteria is an [AdvancedCriteria](../reference.md#object-advancedcriteria), the criteria must consist of a single "and" operator and one or more simple criteria below it. No other logical operators may be used. In other words, the [AdvancedCriteria](../reference.md#object-advancedcriteria) provided must be exactly representable by a simple criteria.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | the filter criteria |

---
## Method: ResultTree.compareCriteria

### Description
Default behavior is to call [DataSource.compareCriteria](DataSource.md#method-datasourcecomparecriteria) to determine whether new criteria is equivalent to the old criteria (returns 0) or not.

See [DataSource.compareCriteria](DataSource.md#method-datasourcecomparecriteria) for a full explanation of the default behavior. The [CriteriaPolicy](../reference_2.md#type-criteriapolicy) used is "dropOnChange".

Override this method or [DataSource.compareCriteria](DataSource.md#method-datasourcecomparecriteria) to implement your own client-side filtering behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | new filter criteria |
| oldCriteria | [Criteria](../reference_2.md#type-criteria) | false | — | old filter criteria |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | dataSource request properties |

### Returns

`[Number](#type-number)` — 0 if the criteria are equivalent, -1 if the criteria are different

### See Also

- [CriteriaPolicy](../reference_2.md#type-criteriapolicy)

---
## Method: ResultTree.dataArrived

### Description
This callback fires whenever the resultTree receives new nodes from the server, after the new nodes have been integrated into the tree.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| parentNode | [TreeNode](#type-treenode) | false | — | The parentNode for which children were just loaded |

---
## Method: ResultTree.get

### Description
Get the item in the openList at a particular position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pos | [Number](#type-number) | false | — | position of the node to get |

### Returns

`[TreeNode](#type-treenode)` — node at that position

### Groups

- openList
- Items

---
## Method: ResultTree.getOpenState

### Description
Returns a snapshot of the current open state of this tree's data as a [TreeGridOpenState](../reference_2.md#type-treegridopenstate) object.

This object can be passed to [ResultTree.setOpenState](#method-resulttreesetopenstate) or [TreeGrid.setOpenState](TreeGrid.md#method-treegridsetopenstate) to open the same set of folders within the tree's data (assuming the nodes are still present in the data).

### Returns

`[TreeGridOpenState](../reference_2.md#type-treegridopenstate)` — current open state for the grid.

### Groups

- viewState

### See Also

- [ResultTree.setOpenState](#method-resulttreesetopenstate)

---
## Method: ResultTree.invalidateCache

### Description
Manually invalidate this ResultTree's cache.

Generally a ResultTree will observe and incorporate updates to the DataSource that provides its records, but when this is not possible, `invalidateCache()` allows manual cache invalidation.

Components bound to this ResultTree will typically re-request the currently visible portion of the dataset, causing the ResultTree to re-fetch data from the server.

**Flags**: A

---
## Method: ResultTree.unloadChildren

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
## Method: ResultTree.setChildren

### Description
Replaces the existing children of a parent node. This leaves the node in the loaded state (unless a partially loaded set of children is specified using the optional `totalChildren` argument). The supplied array of children may be null or empty to indicate there are none, but if present must be in the standard format as would be sent from the server, as described by [treeDataBinding](../kb_topics/treeDataBinding.md#kb-topic-tree-databinding).

In particular, note that for a [paged](#attr-resulttreefetchmode) `ResultTree`, each child node:

:*   can have nested children spcified under the [Tree.childrenProperty](Tree.md#attr-treechildrenproperty) (but not via [TreeNode.id](TreeNode.md#attr-treenodeid)/[TreeNode.parentId](TreeNode.md#attr-treenodeparentid) linking)
*   cannot be open unless it includes either a complete set of children, or partial set of children and a childCount

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| parent | [TreeNode](#type-treenode) | false | — | parent of children |
| newChildren | [List of TreeNode](#type-list-of-treenode) | false | — | children to be set |
| totalChildren | [Integer](../reference_2.md#type-integer) | true | — | number of total children (if not all have been provided as newChildren); only allowed if paging |

### Groups

- loadState

### See Also

- [Tree.removeChildren](Tree.md#method-treeremovechildren)
- [DataSource.updateCaches](DataSource.md#method-datasourceupdatecaches)

---
## Method: ResultTree.getRange

### Description
Get a range of items from the open list

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [number](#type-number) | false | — | start position |
| end | [number](#type-number) | false | — | end position (NOT inclusive) |

### Returns

`[Array of TreeNode](#type-array-of-treenode)` — list of nodes in the open list

### Groups

- openList
- Items

---
## Method: ResultTree.getCombinedCriteria

### Description
Returns a copy of all [explicit](#attr-resulttreecriteria) and [implicit](#method-resulttreegetimplicitcriteria) criteria currently applied to this `ResultTree`.

### Returns

`[Criteria](../reference_2.md#type-criteria)|[AdvancedCriteria](#type-advancedcriteria)` — combined criteria

---
## Method: ResultTree.loadChildren

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
## Method: ResultTree.applyFilter

### Description
The ResultTree will call applyFilter() when it needs to locally filter the tree using the current filter criteria.

Default behavior is to call [Tree.getFilteredTree](Tree.md#method-treegetfilteredtree) to obtain a new, filtered tree.

Override this method or [Tree.getFilteredTree](Tree.md#method-treegetfilteredtree) to implement your own client-side filtering behavior. Note that the original tree should not be affected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tree | [Tree](#type-tree) | false | — | the source tree to be filtered |
| criteria | [Criteria](../reference_2.md#type-criteria) | false | — | the filter criteria |
| filterMode | [TreeFilterMode](../reference.md#type-treefiltermode) | false | — | mode to use for filtering |
| dataSource | [DataSource](#type-datasource) | false | — | dataSource for filtering if the Tree does not already have one |
| requestProperties | [DSRequest](#type-dsrequest) | true | — | Request properties block. This allows developers to specify properties that would impact the filter such as [DSRequest.textMatchStyle](DSRequest.md#attr-dsrequesttextmatchstyle) |

### Returns

`[Tree](#type-tree)` — the filtered tree (copy)

**Flags**: A

---
## Method: ResultTree.setOpenState

### Description
Reset the set of open folders within this tree's data to match the [TreeGridOpenState](../reference_2.md#type-treegridopenstate) object passed in.

Used to restore previous state retrieved from the tree by a call to [ResultTree.getOpenState](#method-resulttreegetopenstate).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| openState | [TreeGridOpenState](../reference_2.md#type-treegridopenstate) | false | — | Object describing the desired set of open folders. |

### Groups

- viewState

### See Also

- [ResultTree.getOpenState](#method-resulttreegetopenstate)

---
