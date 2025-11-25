# Sharing Nodes

[← Back to API Index](../main.md)

---

## KB Topic: Sharing Nodes

### Description
For local Trees, that is, Trees that don't use load on demand, SmartClient supports setting up the Tree structure by setting properties such as "childrenProperty", directly on data nodes. This allows for simpler, faster structures for many common tree uses, but can create confusion if nodes need to be shared across Trees.

**using one node in two places in one Tree**

To do this, either clone the shared node like so:

```
     tree.add(isc.addProperties({}, sharedNode));
 
```
or place the shared data in a shared subobject instead.

**sharing nodes or subtrees across Trees**

Individual nodes within differing tree structures can be shared by two Trees only if [Tree.nameProperty](../classes/Tree.md#attr-treenameproperty), [Tree.childrenProperty](../classes/Tree.md#attr-treechildrenproperty), and [Tree.openProperty](../classes/Tree.md#attr-treeopenproperty) have different values in each Tree.

As a special case of this, two Trees can maintain different open state across a single read-only structure as long as just "openProperty" has a different value in each Tree.

---
