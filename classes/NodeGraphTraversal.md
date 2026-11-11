# NodeGraphTraversal Documentation

[← Back to API Index](../reference.md)

---

## Attr: NodeGraphTraversal.root

### Description
The node the traversal started from.

**Flags**: R

---
## Attr: NodeGraphTraversal.children

### Description
For each node, by ID, the IDs of its children in display order (a child repeats once per edge with [NodeGraphQuerySettings.parallelEdges](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsparalleledges)).

**Flags**: R

---
## Attr: NodeGraphTraversal.parent

### Description
"spanning" traversals only: for each node, by ID, its parent's ID.

**Flags**: R

---
## Attr: NodeGraphTraversal.parents

### Description
For each node, by ID, the distinct IDs of its parents.

**Flags**: R

---
## Attr: NodeGraphTraversal.backReferences

### Description
The edges that close a loop, which no tree can hold. A self-edge always counts; in an "out" or "in" traversal so does an edge back to an ancestor - in "spanning" and "shortestPaths" mode a node with a chain of links down to it, in "dag" mode a node the depth-first walk had not finished, so the edge would close a cycle. In a "both" traversal in "spanning" or "shortestPaths" mode, every edge between two reached nodes that no link stands for is listed (other than a further edge between a linked pair - see [parallelEdges](NodeGraphQuerySettings.md#attr-nodegraphquerysettingsparalleledges)), once, under whichever end was reached first; in "dag" mode only self-edges are. Each expanded node's back references are listed in [NodeGraph.edges](NodeGraph.md#attr-nodegraphedges) order, once however many places the node appears.

**Flags**: R

---
## Attr: NodeGraphTraversal.links

### Description
Every parent-child link, parents before their children.

**Flags**: R

---
## Attr: NodeGraphTraversal.level

### Description
For each node reached, by ID, its breadth-first depth below the root.

**Flags**: R

---
## Attr: NodeGraphTraversal.weight

### Description
"spanning" traversals only: for each node, by ID, the number of nodes in its subtree, itself included.

**Flags**: R

---
