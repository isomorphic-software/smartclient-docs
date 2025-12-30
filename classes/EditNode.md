# EditNode Documentation

[← Back to API Index](../reference.md)

---

## Attr: EditNode.liveObject

### Description
Live version of the object created from the [EditNode.defaults](#attr-editnodedefaults). For example, if [EditNode.type](#attr-editnodetype) is "ListGrid", `liveObject` would be a ListGrid.

**Flags**: IR

---
## Attr: EditNode.canDuplicate

### Description
See [PaletteNode.canDuplicate](PaletteNode.md#attr-palettenodecanduplicate).

**Flags**: IRW

---
## Attr: EditNode.editProxyProperties

### Description
Properties to be applied to the [liveObject](#attr-editnodeliveobject).[editProxy](Canvas.md#attr-canvaseditproxy) when created.

Note that the `editProxy` is created the first time a component is placed into editMode, so any `editProxyProperties` must be set before then.

**Flags**: IR

---
## Attr: EditNode.type

### Description
[SCClassName](../reference.md#type-scclassname) of the [EditNode.liveObject](#attr-editnodeliveobject) , for example, "ListGrid".

**Flags**: IR

---
## Attr: EditNode.useEditMask

### Description
Shortcut property to be applied to the [liveObject](#attr-editnodeliveobject).[editProxy](Canvas.md#attr-canvaseditproxy) when created.

**Flags**: IR

---
## Attr: EditNode.defaults

### Description
Properties required to recreate the current [EditNode.liveObject](#attr-editnodeliveobject).

**Flags**: IR

---
