# NodeGraphTree Documentation

[← Back to API Index](../reference.md)

---

## Class: NodeGraphTree

### Description
A live view of a [NodeGraph](NodeGraph.md#class-nodegraph): a multi-link [Tree](Tree.md#class-tree) whose structure is a traversal of the graph from [focusedNode](#attr-nodegraphtreefocusednode). Change the focus or the traversal settings, or change the graph, and the Tree re-derives, firing dataChanged() as any Tree does, so a TreeGrid or ColumnTree showing it follows; open folders and grid selections are kept. See [nodeGraph](../kb_topics/nodeGraph.md#kb-topic-node-graphs) for an overview.

Created only by [NodeGraph.getTree](NodeGraph.md#method-nodegraphgettree). The Tree's nodes are the graph's own node records, shared by every view of the graph, so a value changed on a node is the same in every view. As in a [ResultTree](ResultTree.md#class-resulttree), nodes are named by a generated property rather than `name`, so a node's title comes from [titleProperty](Tree.md#attr-treetitleproperty) and otherwise its ID. titleProperty defaults to the [titleField](DataSource_1.md#attr-datasourcetitlefield) of the graph's [nodeDataSource](NodeGraph.md#attr-nodegraphnodedatasource), or `title` for an unbound graph; set it to show another field.

### Groups

- nodeGraph

---
## Attr: NodeGraphTree.showParallelEdges

### Description
In a "dag" or "shortestPaths" [NodeGraphTree.traversalMode](#attr-nodegraphtreetraversalmode), whether a node with several edges from the same parent (two relations between the same pair of tables, say) appears under that parent once per edge, rather than once. Each occurrence then stands for its own edge - see [NodeGraphTree.getLinkEdge](#method-nodegraphtreegetlinkedge) - and keeps its own open and selected state. A "spanning" view places each node once, so shows one row whatever this setting.

**Flags**: IR

---
## Attr: NodeGraphTree.graph

### Description
The graph this Tree is a view of. Set by [NodeGraph.getTree](NodeGraph.md#method-nodegraphgettree).

**Flags**: IR

---
## Attr: NodeGraphTree.nodeFilter

### Description
Nodes the view may show - see [NodeGraphQuerySettings.nodeFilter](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsnodefilter).

**Flags**: IR

---
## Attr: NodeGraphTree.showBackReferences

### Description
Whether an edge that closes a loop - a self-edge; in an "out" or "in" traversal an edge back to a node above it; in a "both" traversal ("spanning" or "shortestPaths") an edge between two nodes the tree places apart (see `backReferences` in [NodeGraph.getTraversal](NodeGraph.md#method-nodegraphgettraversal)) - is shown, as a leaf under the node it leaves, or for a "both" traversal under the end reached first. A tree cannot hold a loop itself, so without these a cycle in the data (a workflow step leading back to an earlier one, a manager chain that loops through bad data, or a flight route between two cities the view reaches by other routes) is silently left out.

The leaf is a record of this view's own, not a graph node: it has an ID of its own, carries the ID of the node the edge leads to in `backReference`, is never a folder, and is titled with that node's title plus [NodeGraphTree.backReferenceTitleSuffix](#attr-nodegraphtreebackreferencetitlesuffix). Use [NodeGraphTree.isBackReference](#method-nodegraphtreeisbackreference) and [NodeGraphTree.getBackReferenceTarget](#method-nodegraphtreegetbackreferencetarget) to tell it apart.

**Flags**: IR

---
## Attr: NodeGraphTree.traversalMode

### Description
Whether each node appears once ("spanning"), under every node one step nearer the focus ("shortestPaths"), or under every parent it has ("dag").

**Flags**: IR

---
## Attr: NodeGraphTree.canEditStructure

### Description
Whether changes to this view's structure - a TreeGrid drag-move within it, a drop from another component, a delete, or the Tree's own [add()](Tree.md#method-treeadd), `moveList()` and [remove()](Tree.md#method-treeremove) - become changes to the graph's edges. When false the view is read-only: those calls change nothing and log a warning. (Whether a TreeGrid offers drags and drops at all is its own setting, such as [ListGrid.canReorderRecords](ListGrid_2.md#attr-listgridcanreorderrecords).)

When true, in a "dag" [NodeGraphTree.traversalMode](#attr-nodegraphtreetraversalmode) (any other view is read-only whatever this setting, since a row there need not show every edge between the two nodes):

*   removing an occurrence removes the edge it stands for (see [NodeGraphTree.getLinkEdge](#method-nodegraphtreegetlinkedge)) - every edge placing a node, for a node rather than an occurrence;
*   moving an occurrence under another parent updates its edge's ends, by [NodeGraph.updateEdge](NodeGraph.md#method-nodegraphupdateedge); a back reference moves its loop edge;
*   adding or dropping a node under a parent adds an edge (a drop from another view of the graph copies the dragged edge's other values), adding the node too when an unbound graph does not have it.

The edge runs the way the view reads: in an "out" view, putting X under Y makes the edge Y to X; in an "in" view, X to Y; in a "both" view a moved edge keeps its direction and a new one runs from parent to child. Unbound, a parent's children follow its edges' order, so a drop also places the edge where it was dropped; bound, the edge DataSource's order holds. Every view of the graph then re-derives, this one included, once per edit; bound, the edit is one queue of edge operations and the views follow when cache sync delivers it.

**Flags**: IR

---
## Attr: NodeGraphTree.edgeFilter

### Description
Edges the view may follow - see [NodeGraphQuerySettings.edgeFilter](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsedgefilter).

**Flags**: IR

---
## Attr: NodeGraphTree.nodeCriteria

### Description
Criteria nodes must match for the view to show them - see [NodeGraphQuerySettings.nodeCriteria](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsnodecriteria).

**Flags**: IR

---
## Attr: NodeGraphTree.traversalDepth

### Description
Levels below the focus; null for no limit.

**Flags**: IR

---
## Attr: NodeGraphTree.focusedNode

### Description
ID of the node the traversal starts from, shown as the only top-level node.

**Flags**: IR

---
## Attr: NodeGraphTree.chooseParent

### Description
In a "spanning" view, which parent each node goes under - see [NodeGraphQuerySettings.chooseParent](NodeGraphQuerySettings.md#attr-nodegraphquerysettingschooseparent).

**Flags**: IR

---
## Attr: NodeGraphTree.backReferenceTitleSuffix

### Description
Appended to the title of the node a back reference leads to, to title the back reference (see [NodeGraphTree.showBackReferences](#attr-nodegraphtreeshowbackreferences)).

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: NodeGraphTree.sortChildren

### Description
The order of each node's children - see [NodeGraphQuerySettings.sortChildren](NodeGraphQuerySettings.md#attr-nodegraphquerysettingssortchildren).

**Flags**: IR

---
## Attr: NodeGraphTree.edgeCriteria

### Description
Criteria edges must match for the view to follow them - see [NodeGraphQuerySettings.edgeCriteria](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsedgecriteria).

**Flags**: IR

---
## Attr: NodeGraphTree.traversalDirection

### Description
Which way the view follows edges from its focus: "out" shows what the focus refers to, "in" what refers to it.

**Flags**: IR

---
## Method: NodeGraphTree.isBackReference

### Description
Whether a record of this Tree is a back reference (see [NodeGraphTree.showBackReferences](#attr-nodegraphtreeshowbackreferences)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | — |

### Returns

`[Boolean](#type-boolean)` — —

---
## Method: NodeGraphTree.setTraversal

### Description
Changes any of [NodeGraphTree.traversalDirection](#attr-nodegraphtreetraversaldirection), [NodeGraphTree.traversalDepth](#attr-nodegraphtreetraversaldepth), [NodeGraphTree.traversalMode](#attr-nodegraphtreetraversalmode), the filters ([NodeGraphTree.edgeFilter](#attr-nodegraphtreeedgefilter), [NodeGraphTree.edgeCriteria](#attr-nodegraphtreeedgecriteria), [NodeGraphTree.nodeFilter](#attr-nodegraphtreenodefilter), [NodeGraphTree.nodeCriteria](#attr-nodegraphtreenodecriteria)), [NodeGraphTree.chooseParent](#attr-nodegraphtreechooseparent) and [NodeGraphTree.sortChildren](#attr-nodegraphtreesortchildren), then re-derives the Tree.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [NodeGraphTree Properties](#type-nodegraphtree-properties) | false | — | — |

---
## Method: NodeGraphTree.refreshGraph

### Description
Re-derives the structure from the graph and the traversal settings. Called by the graph whenever it changes.

---
## Method: NodeGraphTree.setFocusedNode

### Description
Re-derives the Tree from another node.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | — |

---
## Method: NodeGraphTree.getLinkEdge

### Description
The graph edge an occurrence of a node stands for: the edge linking it under its parent in this view, or for a back reference (see [NodeGraphTree.showBackReferences](#attr-nodegraphtreeshowbackreferences)) the edge that closes the loop. With [NodeGraphTree.showParallelEdges](#attr-nodegraphtreeshowparalleledges), each occurrence of a node repeated under one parent has its own edge. Use [Tree.getNodeLocator](Tree.md#method-treegetnodelocator) to get an occurrence from a row number.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodeLocator | [NodeLocator](#type-nodelocator) | false | — | — |

### Returns

`[Record](#type-record)` — the edge record, or null for the focused node, which has no parent

---
## Method: NodeGraphTree.getBackReferenceTarget

### Description
The graph node a back reference leads to (see [NodeGraphTree.showBackReferences](#attr-nodegraphtreeshowbackreferences)).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [TreeNode](#type-treenode) | false | — | — |

### Returns

`[Record](#type-record)` — the graph's node, or null if node is not a back reference

---
## Method: NodeGraphTree.getTraversalInfo

### Description
The traversal the current structure was derived from (see [NodeGraph.getTraversal](NodeGraph.md#method-nodegraphgettraversal)), or null if the view has no focus.

### Returns

`[NodeGraphTraversal](#type-nodegraphtraversal)` — —

---
## Method: NodeGraphTree.getGraphNode

### Description
The graph's record for a node - the same object this Tree shows for it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | node ID |

### Returns

`[Record](#type-record)` — —

---
