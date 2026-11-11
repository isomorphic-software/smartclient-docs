# NodeGraphQuerySettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: NodeGraphQuerySettings.maxHops

### Description
[NodeGraph.getReach](NodeGraph.md#method-nodegraphgetreach) and the queries built on it: nodes this many edges away are reached but not searched beyond. No limit by default.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.direction

### Description
Which way edges are followed.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.parallelEdges

### Description
[NodeGraph.getTraversal](NodeGraph.md#method-nodegraphgettraversal) in "dag" or "shortestPaths" [NodeGraphQuerySettings.mode](#attr-nodegraphquerysettingsmode): true for one link per edge, so a child with two edges from the same parent is linked under it twice; otherwise a parent-child pair is linked once, by the first of its edges. Likewise for [NodeGraph.findPaths](NodeGraph.md#method-nodegraphfindpaths): true for one path per parallel edge taken.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.minimum

### Description
[NodeGraph.getMostReferenced](NodeGraph.md#method-nodegraphgetmostreferenced): the fewest distinct referring nodes a node needs.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.edgeFilter

### Description
A function deciding which edges may be followed. With [NodeGraphQuerySettings.edgeCriteria](#attr-nodegraphquerysettingsedgecriteria) also set, an edge must pass both.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.maxPaths

### Description
[NodeGraph.findPaths](NodeGraph.md#method-nodegraphfindpaths): the most paths returned. The number of shortest paths can grow exponentially with the size of a graph (a grid of streets, say), so it is capped.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.mode

### Description
[NodeGraph.getTraversal](NodeGraph.md#method-nodegraphgettraversal): how reached nodes are placed.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.nodeIds

### Description
[NodeGraph.getRanks](NodeGraph.md#method-nodegraphgetranks): the nodes to rank, and the order the search starts from. By default every node.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.nodeCriteria

### Description
Criteria a node record must match to be entered. With [NodeGraphQuerySettings.nodeFilter](#attr-nodegraphquerysettingsnodefilter) also set, a node must pass both.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.maxDepth

### Description
[NodeGraph.getTraversal](NodeGraph.md#method-nodegraphgettraversal): levels below the root. No limit by default.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.chooseParent

### Description
[NodeGraph.getTraversal](NodeGraph.md#method-nodegraphgettraversal) in "spanning" [NodeGraphQuerySettings.mode](#attr-nodegraphquerysettingsmode): which of its candidate parents a node goes under. By default the first candidate.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.sortChildren

### Description
[NodeGraph.getTraversal](NodeGraph.md#method-nodegraphgettraversal): the order of each node's children. By default the order they were reached.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.edgeCriteria

### Description
Criteria an edge record must match to be followed, evaluated as client-side filtering evaluates them. With [NodeGraphQuerySettings.edgeFilter](#attr-nodegraphquerysettingsedgefilter) also set, an edge must pass both.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.nodeFilter

### Description
A function deciding which nodes may be entered; the node a search or traversal starts from is never filtered. With [NodeGraphQuerySettings.nodeCriteria](#attr-nodegraphquerysettingsnodecriteria) also set, a node must pass both.

**Flags**: IR

---
## Attr: NodeGraphQuerySettings.stopAt

### Description
[NodeGraph.getReach](NodeGraph.md#method-nodegraphgetreach): a node ID at which the search ends once reached.

**Flags**: IR

---
