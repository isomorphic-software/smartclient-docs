# Palette Documentation

[← Back to API Index](../reference.md)

---

## Attr: Palette.defaultEditContext

### Description
Default EditContext that this palette should use. Palettes generally create components via drag and drop, but may also support creation via double-click or other UI idioms when a defaultEditContext is set.

**Flags**: IRW

---
## Attr: Palette.generateNames

### Description
Whether created components should have their "ID" or "name" property automatically set to a unique value based on the component's type, eg, "ListGrid0".

### Groups

- devTools

**Flags**: IR

---
## Method: Palette.makeEditNode

### Description
Given a [PaletteNode](../reference.md#object-palettenode), make an [EditNode](../reference.md#object-editnode) from it by creating a [liveObject](EditNode.md#attr-editnodeliveobject) from the [PaletteNode.defaults](PaletteNode.md#attr-palettenodedefaults) and copying presentation properties (eg [title](PaletteNode.md#attr-palettenodetitle) to the editNode.

If `editNodeProperties` is specified as an object on on the paletteNode, each property in this object will also be copied across to the editNode.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| paletteNode | [PaletteNode](#type-palettenode) | false | — | paletteNode to create from |
| editContext | [EditContext](#type-editcontext) | true | — | the [EditContext](EditContext.md#class-editcontext) where the node will be added. Only required in +{EditContext.screenMode,screenMode}. |

### Returns

`[EditNode](#type-editnode)` — created EditNode

---
## Method: Palette.setDefaultEditContext

### Description
Sets the default EditContext that this palette should use. Palettes generally create components via drag and drop, but may also support creation via double-click or other UI idioms when a defaultEditContext is set.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| defaultEditContext | [EditContext](#type-editcontext)|[EditTree](#type-edittree)|[EditPane](#type-editpane) | false | — | the default EditContext used by this Palette |

---
