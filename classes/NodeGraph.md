# NodeGraph Documentation

[← Back to API Index](../reference.md)

---

## Class: NodeGraph

### Description
A graph of nodes and edges: the model behind any number of live [NodeGraphTree](NodeGraphTree.md#class-nodegraphtree) views ([getTree()](#method-nodegraphgettree)), with queries over it such as [getReach()](#method-nodegraphgetreach), [findPath()](#method-nodegraphfindpath) and [getTraversal()](#method-nodegraphgettraversal). See [nodeGraph](../kb_topics/nodeGraph.md#kb-topic-node-graphs) for an overview.

Change the graph through [addNode()](#method-nodegraphaddnode), [addEdge()](#method-nodegraphaddedge) and the other mutation methods, or change [nodes](#attr-nodegraphnodes) and [edges](#attr-nodegraphedges) in place and call [graphChanged()](#method-nodegraphgraphchanged); with DataSources ([nodeDataSource](#attr-nodegraphnodedatasource)), change it through the DataSources from anywhere. Every view follows. Results list nodes and edges in a stable order: the order of [edges](#attr-nodegraphedges) for edges, and the order in which a search reaches nodes.

### Groups

- nodeGraph

---
## Attr: NodeGraph.nodes

### Description
Node records, each with a unique ID in [NodeGraph.nodeIdField](#attr-nodegraphnodeidfield). Change through [NodeGraph.addNode](#method-nodegraphaddnode) / [NodeGraph.updateNode](#method-nodegraphupdatenode) / [NodeGraph.removeNode](#method-nodegraphremovenode) or [NodeGraph.setData](#method-nodegraphsetdata); after changing it in place, call [NodeGraph.graphChanged](#method-nodegraphgraphchanged).

**Flags**: IR

---
## Attr: NodeGraph.nodeIdField

### Description
Node property holding the node's ID.

**Flags**: IR

---
## Attr: NodeGraph.edgeDataSource

### Description
A DataSource the graph's edges are loaded from - see [NodeGraph.nodeDataSource](#attr-nodegraphnodedatasource).

**Flags**: IR

---
## Attr: NodeGraph.edgeIdField

### Description
Edge property holding a unique ID for each edge, if edges have one. When set, [NodeGraph.removeEdge](#method-nodegraphremoveedge) and [NodeGraph.getEdge](#method-nodegraphgetedge) accept the ID; edges are otherwise identified by the record itself. With an [NodeGraph.edgeDataSource](#attr-nodegraphedgedatasource), defaults to its primary key.

**Flags**: IR

---
## Attr: NodeGraph.nodeDataSource

### Description
A DataSource the graph's nodes are loaded from, as a [ResultTree](ResultTree.md#class-resulttree) loads its nodes from its dataSource. Used with [NodeGraph.edgeDataSource](#attr-nodegraphedgedatasource): the graph holds every node and edge (see [NodeGraph.loadGraph](#method-nodegraphloadgraph)), keeps them in sync with each DataSource through the standard cache sync of a [ResultSet](ResultSet.md#class-resultset), so an add, update or remove made anywhere reaches every view of the graph, and sends its own changes ([NodeGraph.addNode](#method-nodegraphaddnode), [NodeGraph.addEdge](#method-nodegraphaddedge) and the others) to the DataSources as the matching operation.

Field names default from the DataSources: [NodeGraph.nodeIdField](#attr-nodegraphnodeidfield) to this DataSource's primary key, [NodeGraph.edgeIdField](#attr-nodegraphedgeidfield) to the edge DataSource's, and [NodeGraph.edgeSourceField](#attr-nodegraphedgesourcefield) / [NodeGraph.edgeTargetField](#attr-nodegraphedgetargetfield) to the edge DataSource's two foreign keys to this one, in field order.

**Flags**: IR

---
## Attr: NodeGraph.autoFetchData

### Description
With [NodeGraph.nodeDataSource](#attr-nodegraphnodedatasource) and [NodeGraph.edgeDataSource](#attr-nodegraphedgedatasource) set, whether the graph loads them as soon as it is created; otherwise call [NodeGraph.loadGraph](#method-nodegraphloadgraph).

**Flags**: IR

---
## Attr: NodeGraph.edges

### Description
Edge records, each naming its two ends in [NodeGraph.edgeSourceField](#attr-nodegraphedgesourcefield) and [NodeGraph.edgeTargetField](#attr-nodegraphedgetargetfield). Change through [NodeGraph.addEdge](#method-nodegraphaddedge) / [NodeGraph.removeEdge](#method-nodegraphremoveedge) or [NodeGraph.setData](#method-nodegraphsetdata); after changing it in place, call [NodeGraph.graphChanged](#method-nodegraphgraphchanged).

**Flags**: IR

---
## Attr: NodeGraph.edgeSourceField

### Description
Edge property holding the ID of the edge's source node.

**Flags**: IR

---
## Attr: NodeGraph.edgeTargetField

### Description
Edge property holding the ID of the edge's target node.

**Flags**: IR

---
## Method: NodeGraph.classifyNodes

### Description
Structural roles of the nodes, from the edges passing the edge filters, self-edges ignored. A node may have neither role.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[NodeGraphNodeRoles](#type-nodegraphnoderoles)` — each list in [NodeGraph.nodes](#attr-nodegraphnodes) order

### Groups

- nodeGraph

---
## Method: NodeGraph.getSubgraph

### Description
The induced subgraph on some nodes: a new NodeGraph holding those nodes and every edge between two of them (the same records, not copies).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ids | [Array of String](#type-array-of-string) | false | — | — |

### Returns

`[NodeGraph](#type-nodegraph)` — —

---
## Method: NodeGraph.getTree

### Description
A live Tree view of this graph: a [NodeGraphTree](NodeGraphTree.md#class-nodegraphtree) whose structure is the traversal from rootId that `settings` describes - any NodeGraphTree property, such as [traversalDirection](NodeGraphTree.md#attr-nodegraphtreetraversaldirection), [traversalDepth](NodeGraphTree.md#attr-nodegraphtreetraversaldepth) or [traversalMode](NodeGraphTree.md#attr-nodegraphtreetraversalmode). Destroy it when done with it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rootId | [String](#type-string) | false | — | node ID of the view's [focus](NodeGraphTree.md#attr-nodegraphtreefocusednode) |
| settings | [NodeGraphTree Properties](#type-nodegraphtree-properties) | true | — | — |

### Returns

`[NodeGraphTree](#type-nodegraphtree)` — —

### Groups

- nodeGraph

---
## Method: NodeGraph.getEdge

### Description
The edge record with an ID in [NodeGraph.edgeIdField](#attr-nodegraphedgeidfield).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | — |

### Returns

`[Record](#type-record)` — the edge, or null if there is none or no edgeIdField is set

---
## Method: NodeGraph.removeNode

### Description
Removes a node and every edge touching it. Bound, the edges' removes and then the node's are sent in one queue.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | — |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | bound only: fired when the node's remove completes |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | bound only |

### Returns

`[Boolean](#type-boolean)` — whether there was such a node

---
## Method: NodeGraph.getBestConnected

### Description
The node with the most distinct neighbors in either direction, ignoring self-edges; null if no edge passes the edge filters. Ties go to the node first listed as an edge end.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[String](#type-string)` — node ID, or null

### Groups

- nodeGraph

---
## Method: NodeGraph.graphChanged

### Description
Call after changing [NodeGraph.nodes](#attr-nodegraphnodes) or [NodeGraph.edges](#attr-nodegraphedges) in place: indexes and cached criteria results are rebuilt on next use, and every view from [NodeGraph.getTree](#method-nodegraphgettree) re-derives its structure. The mutation methods call this themselves.

---
## Method: NodeGraph.getDegree

### Description
The number of edges leaving a node in a direction; parallel edges each count.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | node ID |
| direction | [NodeGraphDirection](../reference_2.md#type-nodegraphdirection) | true | — | default "both" |
| edgeFilter | [NodeGraphEdgeFilter](#type-nodegraphedgefilter)|[AdvancedCriteria](#type-advancedcriteria) | true | — | as for [NodeGraph.getEdges](#method-nodegraphgetedges) |

### Returns

`[Integer](../reference_2.md#type-integer)` — —

### Groups

- nodeGraph

---
## Method: NodeGraph.findPath

### Description
A shortest path between two nodes, chosen among equally short ones as [NodeGraph.getReach](#method-nodegraphgetreach) chooses; uses the same settings. [NodeGraph.findPaths](#method-nodegraphfindpaths) returns every shortest path.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fromId | [String](#type-string) | false | — | node ID |
| toId | [String](#type-string) | false | — | node ID |
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[NodeGraphPath](#type-nodegraphpath)` — the path from fromId to toId, or null if there is none

### Groups

- nodeGraph

---
## Method: NodeGraph.getEdges

### Description
The edges that leave a node in a direction (for "both", every edge touching it).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | node ID |
| direction | [NodeGraphDirection](../reference_2.md#type-nodegraphdirection) | true | — | default "both" |
| edgeFilter | [NodeGraphEdgeFilter](#type-nodegraphedgefilter)|[AdvancedCriteria](#type-advancedcriteria) | true | — | edges it does not pass are left out (see [NodeGraphQuerySettings.edgeFilter](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsedgefilter)) |

### Returns

`[Array of Record](#type-array-of-record)` — edges, in [NodeGraph.edges](#attr-nodegraphedges) order

### Groups

- nodeGraph

---
## Method: NodeGraph.updateNode

### Description
Applies new values to a node's record in place, then [NodeGraph.graphChanged](#method-nodegraphgraphchanged) (a node filter or criteria may depend on them). A node's ID cannot be changed this way: a value for [NodeGraph.nodeIdField](#attr-nodegraphnodeidfield) is ignored, with a warning. Bound, the values are sent as an update and the node changes when it completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | — |
| values | [Object](../reference_2.md#type-object) | false | — | properties to set on the node |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | bound only: fired when the update completes |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | bound only |

### Returns

`[Record](#type-record)` — the node, or null if there is no node with that ID

---
## Method: NodeGraph.getReach

### Description
Breadth-first search from a node: the nodes reached, how far away each is, and the step each was first reached by. Of two equally short routes, the one whose edge is listed first in [NodeGraph.edges](#attr-nodegraphedges) wins. Uses the settings [direction](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsdirection), [maxHops](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsmaxhops), [stopAt](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsstopat) and the filters; the start node is never filtered.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fromId | [String](#type-string) | false | — | node ID |
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[NodeGraphReach](#type-nodegraphreach)` — —

### Groups

- nodeGraph

---
## Method: NodeGraph.loadGraph

### Description
Fetches every node from [NodeGraph.nodeDataSource](#attr-nodegraphnodedatasource) and every edge from [NodeGraph.edgeDataSource](#attr-nodegraphedgedatasource), in one queue, replacing what the graph holds; every view then re-derives. Called on creation unless [NodeGraph.autoFetchData](#attr-nodegraphautofetchdata) is false.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [Callback](../reference.md#type-callback) | true | — | fired once both have arrived |

---
## Method: NodeGraph.getNeighbors

### Description
The distinct nodes one edge away from a node in a direction, not counting the node itself (a self-edge leads nowhere new).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | node ID |
| direction | [NodeGraphDirection](../reference_2.md#type-nodegraphdirection) | true | — | default "both" |
| edgeFilter | [NodeGraphEdgeFilter](#type-nodegraphedgefilter)|[AdvancedCriteria](#type-advancedcriteria) | true | — | as for [NodeGraph.getEdges](#method-nodegraphgetedges) |

### Returns

`[Array of String](#type-array-of-string)` — node IDs, in the order their first edge is listed

### Groups

- nodeGraph

---
## Method: NodeGraph.getConnectingSet

### Description
The given nodes plus the nodes needed to connect them: the union of the shortest paths from the first node to each other one (searched as by [NodeGraph.getReach](#method-nodegraphgetreach), with the same settings). Nodes the first cannot reach are included on their own. Not the smallest possible connecting set (a Steiner tree, which is NP-hard), but stable and never larger than the sum of the paths.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ids | [Array of String](#type-array-of-string) | false | — | node IDs |
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[Object](../reference_2.md#type-object)` — an object with a `true` property for the ID of every node kept

### Groups

- nodeGraph

---
## Method: NodeGraph.updateEdge

### Description
Changes an edge's values - typically its [source](#attr-nodegraphedgesourcefield) or [target](#attr-nodegraphedgetargetfield), which moves it. Both ends after the change must be nodes of this graph; otherwise nothing changes, with a warning. Bound, the values are sent as an update and the edge changes when it completes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| edge | [Record](#type-record)|[String](#type-string) | false | — | the edge record, or its ID |
| values | [Object](../reference_2.md#type-object) | false | — | properties to set on the edge |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | bound only: fired when the update completes |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | bound only |

### Returns

`[Boolean](#type-boolean)` — whether the edge was changed (bound: whether the update was sent)

---
## Method: NodeGraph.findPaths

### Description
Every shortest path between two nodes - all the paths with the fewest edges, where [NodeGraph.findPath](#method-nodegraphfindpath) returns one of them. The first is the path findPath() returns; the rest follow in the order the search reached their steps, so paths sharing a start stay together. Uses the settings of [NodeGraph.getReach](#method-nodegraphgetreach), plus [parallelEdges](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsparalleledges) (whether paths differing only in which of two parallel edges they take are listed separately) and [maxPaths](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsmaxpaths).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fromId | [String](#type-string) | false | — | node ID |
| toId | [String](#type-string) | false | — | node ID |
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[Array of NodeGraphPath](#type-array-of-nodegraphpath)` — the paths from fromId to toId; empty if there is none

### Groups

- nodeGraph

---
## Method: NodeGraph.getNodeIds

### Description
The ID of every node, in [NodeGraph.nodes](#attr-nodegraphnodes) order.

### Returns

`[Array of String](#type-array-of-string)` — —

---
## Method: NodeGraph.isLoaded

### Description
For a DataSource-backed graph, whether [NodeGraph.loadGraph](#method-nodegraphloadgraph) has completed; always true for a graph given its nodes and edges directly.

### Returns

`[Boolean](#type-boolean)` — —

---
## Method: NodeGraph.removeEdge

### Description
Removes an edge, given its record or, with [NodeGraph.edgeIdField](#attr-nodegraphedgeidfield) set, its ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| edge | [Record](#type-record)|[String](#type-string) | false | — | the edge record, or its ID |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | bound only: fired when the remove completes |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | bound only |

### Returns

`[Boolean](#type-boolean)` — whether the edge was in the graph

---
## Method: NodeGraph.addNode

### Description
Adds a node. A node whose ID is already in the graph is not added, with a warning; unbound, a node must have an ID, while bound the DataSource may assign one.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| node | [Record](#type-record) | false | — | — |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | bound only: fired when the add completes |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | bound only |

### Returns

`[Boolean](#type-boolean)` — whether the node was added (bound: whether the add was sent)

---
## Method: NodeGraph.getRanks

### Description
A layering for a left-to-right or top-to-bottom drawing: each node's rank is the length of the longest chain of edges (followed source to target) below it, after a depth-first search drops the edges that close cycles. Self-edges and parallel edges are ignored. Uses the edge filters and [nodeIds](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsnodeids), whose order decides which edge of a cycle is dropped.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[Object](../reference_2.md#type-object)` — each node's rank, by ID

### Groups

- nodeGraph

---
## Method: NodeGraph.getNode

### Description
The node record with an ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [String](#type-string) | false | — | — |

### Returns

`[Record](#type-record)` — the node, or null if there is none

---
## Method: NodeGraph.getMostReferenced

### Description
The node that edges come in to from the most distinct other nodes, ignoring self-edges; null unless some node has at least [minimum](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsminimum). Ties go to the node first listed as a target. Uses the edge filters.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[String](#type-string)` — node ID, or null

### Groups

- nodeGraph

---
## Method: NodeGraph.getTraversal

### Description
The tree a traversal from a root node finds: the structure a [NodeGraphTree](NodeGraphTree.md#class-nodegraphtree) shows, as data. Uses [direction](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsdirection), [maxDepth](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsmaxdepth), [mode](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsmode), [parallelEdges](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsparalleledges), [chooseParent](NodeGraphQuerySettings.md#attr-nodegraphquerysettingschooseparent), [sortChildren](NodeGraphQuerySettings.md#attr-nodegraphquerysettingssortchildren) and the filters.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rootId | [String](#type-string) | false | — | node ID |
| settings | [NodeGraphQuerySettings](#type-nodegraphquerysettings) | true | — | — |

### Returns

`[NodeGraphTraversal](#type-nodegraphtraversal)` — —

### Groups

- nodeGraph

---
## Method: NodeGraph.setData

### Description
Replaces the nodes and edges, then [NodeGraph.graphChanged](#method-nodegraphgraphchanged).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| nodes | [Array of Record](#type-array-of-record) | false | — | — |
| edges | [Array of Record](#type-array-of-record) | false | — | — |

---
## Method: NodeGraph.addEdge

### Description
Adds an edge. Both ends must be nodes of this graph; otherwise the edge is not added, with a warning. Parallel edges and self-edges are allowed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| edge | [Record](#type-record) | false | — | — |
| callback | [DSCallback](../reference_2.md#type-dscallback) | true | — | bound only: fired when the add completes |
| requestProperties | [DSRequest Properties](#type-dsrequest-properties) | true | — | bound only |

### Returns

`[Boolean](#type-boolean)` — whether the edge was added (bound: whether the add was sent)

---
