# RibbonGroup Documentation

[← Back to API Index](../reference.md)

---

## Class: RibbonGroup

*Inherits from:* [ToolStripGroup](ToolStripGroup.md#class-toolstripgroup)

### Description
A widget that groups other controls for use in [RibbonBars](../reference.md#class-ribbonbar).

---
## Attr: RibbonGroup.newControlConstructor

### Description
Widget class for controls [created automatically](#method-ribbongroupcreatecontrol) by this RibbonGroup. Since [such controls](#attr-ribbongroupnewcontrolconstructor) are created via the autoChild system, they can be further customized via the newControlProperties property.

**Flags**: IR

---
## Attr: RibbonGroup.newControlDefaults

### Description
Properties used by [createControl](#method-ribbongroupcreatecontrol) when creating new controls.

**Flags**: IR

---
## Method: RibbonGroup.createControl

### Description
Creates a new control and adds it to this RibbonGroup. The control is created using the autoChild system, according to the specified [constructor](#attr-ribbongroupnewcontrolconstructor) and the passed properties are applied to it.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| properties | [Canvas Properties](#type-canvas-properties) | false | — | properties to apply to the new control |
| position | [Integer](../reference_2.md#type-integer) | true | — | the index at which to insert the new control |

---
