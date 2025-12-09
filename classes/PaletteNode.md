# PaletteNode Documentation

[← Back to API Index](../reference.md)

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
## Attr: PaletteNode.recreateOnChange

### Description
If set to true, indicates instead of updating the changed property on the target live component a new live component is created with the current configured properties.

This property is typically set when a custom component is being used that doesn't support setters for any or most of its properties and a change can be reflected by recreating the component.

Individual properties of the target component can be marked similarly on the component's schema for more fine-grained control. See [DataSourceField.recreateOnChange](DataSourceField.md#attr-datasourcefieldrecreateonchange).

**Flags**: IR

---
## Attr: PaletteNode.placeholderImage

### Description
Image to display in lieu of the usual placeholder text.

**Flags**: IR

---
## Attr: PaletteNode.canDuplicate

### Description
If set to false, indicates that this node cannot be [copy & pasted](EditProxy.md#attr-editproxyusecopypasteshortcuts), including disallowing calls to [EditContext.makePaletteNode](EditContext.md#method-editcontextmakepalettenode) for [EditNodes](../reference.md#object-editnode) created from this [PaletteNode](../reference.md#object-palettenode).

**Flags**: IR

---
## Attr: PaletteNode.editNodeProperties

### Description
Properties to be applied to the [editNode](../reference.md#object-editnode) when created.

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
## Attr: PaletteNode.alwaysUsePlaceholder

### Description
If set to true, indicates that a [Placeholder](Placeholder.md#class-placeholder) should always be shown in place of the actual component.

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
## Attr: PaletteNode.requiredProperties

### Description
Comma separated list of properties for this component that must be provided in [EditNode.defaults](EditNode.md#attr-editnodedefaults) before the component will be created. Otherwise a [Placeholder](Placeholder.md#class-placeholder) will be used until the required properties are satisfied.

**Flags**: IR

---
## Attr: PaletteNode.placeholderProperties

### Description
Properties to be applied to the [liveObject](#attr-palettenodeliveobject) when created as a [Placeholder](Placeholder.md#class-placeholder).

**Flags**: IR

---
