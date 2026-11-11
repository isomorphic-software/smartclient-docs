# Node Graphs

[← Back to API Index](../reference.md)

---

## KB Topic: Node Graphs

### Description
A [NodeGraph](../classes/NodeGraph.md#class-nodegraph) holds data whose records are related as a graph rather than a tree: each node may have any number of parents and children, two nodes may be related by several edges, a node may be related to itself, and relations may run in a circle. Organization charts with dotted-line managers, workflows whose steps loop back, data models whose tables reference each other, and dependency networks are all graphs of this kind.

**The model and its views.** The graph itself holds the nodes and the edges, and answers questions about them: which nodes are within some number of steps of a node ([getReach()](../classes/NodeGraph.md#method-nodegraphgetreach)), the shortest route between two ([findPath()](../classes/NodeGraph.md#method-nodegraphfindpath)), the most referenced node ([getMostReferenced()](../classes/NodeGraph.md#method-nodegraphgetmostreferenced)), a layering for drawing ([getRanks()](../classes/NodeGraph.md#method-nodegraphgetranks)) and others. To show the graph, ask it for a [NodeGraphTree](../classes/NodeGraphTree.md#class-nodegraphtree) - a live [Tree](../classes/Tree.md#class-tree) view of it from one node, the [focused node](../classes/NodeGraphTree.md#attr-nodegraphtreefocusednode) - with [getTree()](../classes/NodeGraph.md#method-nodegraphgettree), and give that view to a [TreeGrid](../classes/TreeGrid.md#class-treegrid) or any other component that shows a Tree. A graph can have any number of views, each with its own focus, direction and filters, so one panel can show who reports to a manager while another shows the chain of command above an employee. Every view follows changes to the graph.

**Edges and direction.** An edge is a record naming the node it leaves in [edgeSourceField](../classes/NodeGraph.md#attr-nodegraphedgesourcefield) and the node it leads to in [edgeTargetField](../classes/NodeGraph.md#attr-nodegraphedgetargetfield); nothing else about it is assumed. Queries and views follow edges in a [direction](../reference_2.md#type-nodegraphdirection): "out" from source to target, "in" from target to source, or "both".

**Views of a graph.** A view lists the nodes it reaches from its focus in one of three [modes](../reference_2.md#type-nodegraphtraversalmode): each node once ("spanning"), each node under every node one step nearer the focus ("shortestPaths"), or every node under every parent it has ("dag"). The last two are shown as a [multi-link tree](../classes/Tree.md#method-treeismultilinktree). A view shows the graph's own node records, so a value changed on a node is the same in every view. Because no tree can hold a loop, an edge that closes one - leading back to a node above, or, in a view following edges both ways, joining two nodes the tree places apart - is shown as a marked leaf, a [back reference](../classes/NodeGraphTree.md#attr-nodegraphtreeshowbackreferences); two edges between the same pair of nodes are two rows ([NodeGraphTree.showParallelEdges](../classes/NodeGraphTree.md#attr-nodegraphtreeshowparalleledges)), and [getLinkEdge()](../classes/NodeGraphTree.md#method-nodegraphtreegetlinkedge) tells which edge a row stands for. Open folders and grid selections are kept when the graph changes.

**Filters.** Queries and views can be limited to some edges and nodes, by a function ([edgeFilter](../classes/NodeGraphQuerySettings.md#attr-nodegraphquerysettingsedgefilter), [nodeFilter](../classes/NodeGraphQuerySettings.md#attr-nodegraphquerysettingsnodefilter)) or by [AdvancedCriteria](../reference.md#object-advancedcriteria) ([edgeCriteria](../classes/NodeGraphQuerySettings.md#attr-nodegraphquerysettingsedgecriteria), [nodeCriteria](../classes/NodeGraphQuerySettings.md#attr-nodegraphquerysettingsnodecriteria)), or both, in which case both must pass. Criteria are evaluated by the framework's client-side filtering, so a view described by criteria can be saved and restored as data.

**Data from DataSources.** Given a [nodeDataSource](../classes/NodeGraph.md#attr-nodegraphnodedatasource) and an [edgeDataSource](../classes/NodeGraph.md#attr-nodegraphedgedatasource), a graph loads every node and edge, follows every change made to either DataSource anywhere in the application through standard cache sync, and sends its own changes ([addEdge()](../classes/NodeGraph.md#method-nodegraphaddedge) and the like) to the DataSources.

**Editing through a view.** With [NodeGraphTree.canEditStructure](../classes/NodeGraphTree.md#attr-nodegraphtreecaneditstructure), dragging a row to another parent, dropping a node in from another component, or deleting a row in a TreeGrid changes the graph's edges, and every view follows.

**Samples.** Each shows a different side of the feature:

*   *Multi-Link Tree (Org Chart)*: an employee with a dotted-line manager appears under both managers. Two "dag" views of one DataSource-backed graph show the organization from the top down and, re-rooted on the selected employee with [setFocusedNode()](../classes/NodeGraphTree.md#method-nodegraphtreesetfocusednode), that employee's chain of command upward. [getLinkEdge()](../classes/NodeGraphTree.md#method-nodegraphtreegetlinkedge) labels the reporting line each row stands for, edge criteria hide dotted lines, and dragging an employee onto a new manager updates the reporting line's record ([canEditStructure](../classes/NodeGraphTree.md#attr-nodegraphtreecaneditstructure)).
*   *Graph with Loops (Order Lifecycle)*: a workflow whose transitions lead back to earlier statuses. Views forward from the first status and backward to the selected one show each loop as a [back reference](../classes/NodeGraphTree.md#attr-nodegraphtreeshowbackreferences) and two transitions between the same statuses as two rows; [findPath()](../classes/NodeGraph.md#method-nodegraphfindpath) gives the quickest way through, and edge criteria limit the transitions to those a role may take.
*   *NodeGraph Pathfinding (Flight Routes)*: a route network flown both ways. A "shortestPaths" view places every city under each city it can be reached through with the fewest connections and marks the routes it does not use as back references; [findPaths()](../classes/NodeGraph.md#method-nodegraphfindpaths) lists every equally short route and [getReach()](../classes/NodeGraph.md#method-nodegraphgetreach) counts the cities within each number of connections, with an airline filter (edge criteria) and a connection limit ([traversalDepth](../classes/NodeGraphTree.md#attr-nodegraphtreetraversaldepth)).

### Related

- [NodeGraphDirection](../reference_2.md#type-nodegraphdirection)
- [NodeGraphTraversalMode](../reference_2.md#type-nodegraphtraversalmode)
- [Callbacks.NodeGraphEdgeFilter](../classes/Callbacks.md#method-callbacksnodegraphedgefilter)
- [Callbacks.NodeGraphNodeFilter](../classes/Callbacks.md#method-callbacksnodegraphnodefilter)
- [Callbacks.NodeGraphChooseParent](../classes/Callbacks.md#method-callbacksnodegraphchooseparent)
- [Callbacks.NodeGraphSortChildren](../classes/Callbacks.md#method-callbacksnodegraphsortchildren)
- [NodeGraph.getTree](../classes/NodeGraph.md#method-nodegraphgettree)
- [NodeGraph.getEdges](../classes/NodeGraph.md#method-nodegraphgetedges)
- [NodeGraph.getNeighbors](../classes/NodeGraph.md#method-nodegraphgetneighbors)
- [NodeGraph.getDegree](../classes/NodeGraph.md#method-nodegraphgetdegree)
- [NodeGraph.getReach](../classes/NodeGraph.md#method-nodegraphgetreach)
- [NodeGraph.findPath](../classes/NodeGraph.md#method-nodegraphfindpath)
- [NodeGraph.findPaths](../classes/NodeGraph.md#method-nodegraphfindpaths)
- [NodeGraph.getConnectingSet](../classes/NodeGraph.md#method-nodegraphgetconnectingset)
- [NodeGraph.getMostReferenced](../classes/NodeGraph.md#method-nodegraphgetmostreferenced)
- [NodeGraph.getBestConnected](../classes/NodeGraph.md#method-nodegraphgetbestconnected)
- [NodeGraph.classifyNodes](../classes/NodeGraph.md#method-nodegraphclassifynodes)
- [NodeGraph.getRanks](../classes/NodeGraph.md#method-nodegraphgetranks)
- [NodeGraph.getTraversal](../classes/NodeGraph.md#method-nodegraphgettraversal)
- [NodeGraphQuerySettings](../reference_2.md#object-nodegraphquerysettings)
- [NodeGraphReach](../reference_2.md#object-nodegraphreach)
- [NodeGraphReachStep](../reference.md#object-nodegraphreachstep)
- [NodeGraphPath](../reference.md#object-nodegraphpath)
- [NodeGraphTraversal](../reference_2.md#object-nodegraphtraversal)
- [NodeGraphLink](../reference_2.md#object-nodegraphlink)
- [NodeGraphBackReference](../reference.md#object-nodegraphbackreference)
- [NodeGraphNodeRoles](../reference.md#object-nodegraphnoderoles)
- [NodeGraph](../classes/NodeGraph.md#class-nodegraph)
- [NodeGraphTree](../classes/NodeGraphTree.md#class-nodegraphtree)

---
