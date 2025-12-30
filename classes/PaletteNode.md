# PaletteNode Documentation

[← Back to API Index](../reference.md)

---

## Attr: PaletteNode.editNodeProperties

### Description
Properties to be applied to the [editNode](../reference.md#object-editnode) when created.

**Flags**: IR

---
## Attr: PaletteNode.icon

### Description
Icon for this paletteNode.

**Flags**: IR

---
## Attr: PaletteNode.idPrefix

### Description
Prefix used to create unique component ID. If not specified, [PaletteNode.type](#attr-palettenodetype) is used.

**Deprecated**

**Flags**: IR

---
## Attr: PaletteNode.idName

### Description
Name used to create unique component ID. If not specified, [PaletteNode.type](#attr-palettenodetype) is used.

Note: idName must follow all rules for a [Identifier](../reference.md#type-identifier).

**Flags**: IR

---
## Attr: PaletteNode.defaults

### Description
Defaults for the component to be created from this palette.

For example, if [PaletteNode.type](#attr-palettenodetype) is "ListGrid", properties valid to pass to [ListGrid.create()](Class.md#classmethod-classcreate).

Note that event handlers or method overrides cannot be configured as `defaults`, as they cannot be serialized or restored. Instead, create a subclass that implements the desired behaviors, and use that subclass as [PaletteNode.type](#attr-palettenodetype).

**Flags**: IR

---
## Attr: PaletteNode.editProxyProperties

### Description
Properties to be applied to the [liveObject](#attr-palettenodeliveobject).[editProxy](Canvas.md#attr-canvaseditproxy) when created.

**Flags**: IR

---
## Attr: PaletteNode.liveObject

### Description
For a paletteNode which should be a "singleton", that is, always provides the exact same object (==) rather than a dynamically created copy, provide the singleton object as `liveObject`.

Instead of dynamically creating an object from defaults, the `liveObject` will simply be assigned to [EditNode.liveObject](EditNode.md#attr-editnodeliveobject) for the created editNode.

**Flags**: IR

---
## Attr: PaletteNode.type

### Description
[SCClassName](../reference.md#type-scclassname) this paletteNode creates, for example, "ListGrid".

**Flags**: IR

---
## Attr: PaletteNode.title

### Description
Textual title for this paletteNode.

**Flags**: IR

---
## Attr: PaletteNode.canDuplicate

### Description
If set to false, indicates that this node cannot be [copy & pasted](EditProxy.md#attr-editproxyusecopypasteshortcuts), including disallowing calls to [EditContext.makePaletteNode](EditContext.md#method-editcontextmakepalettenode) for [EditNodes](../reference.md#object-editnode) created from this [PaletteNode](../reference_2.md#object-palettenode).

**Flags**: IR

---
