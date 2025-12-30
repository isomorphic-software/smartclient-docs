# DiscoverTreeSettings Documentation

[← Back to API Index](../reference.md)

---

## Attr: DiscoverTreeSettings.scanMode

### Description
Determines how to scan for the [Tree.childrenProperty](Tree.md#attr-treechildrenproperty)

**Flags**: IRW

---
## Attr: DiscoverTreeSettings.typeProperty

### Description
Each discovered child is labeled with a configurable "typeProperty" set to the value of the property that held the children

**Flags**: IRW

---
## Attr: DiscoverTreeSettings.childrenMode

### Description
When heuristically finding a property that appears to contain child objects, the childrenMode determines how to chose the property that appears to contain child objects

**Flags**: IR

---
## Attr: DiscoverTreeSettings.tieMode

### Description
What to do if there is more than one possible [Tree.childrenProperty](Tree.md#attr-treechildrenproperty) when using scanMode "branch" or "level"

**Flags**: IRW

---
## Attr: DiscoverTreeSettings.nameProperty

### Description
For string leaf nodes (if allowed), the name of the property to store the string under in the auto-created object

**Flags**: IRW

---
## Attr: DiscoverTreeSettings.newChildrenProperty

### Description
What to rename the array of children once discovered. If not set, it will default to the value of [Tree.childrenProperty](Tree.md#attr-treechildrenproperty) inside discoverTree()

**Flags**: IRW

---
