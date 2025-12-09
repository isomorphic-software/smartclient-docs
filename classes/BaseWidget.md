# BaseWidget Documentation

[← Back to API Index](../reference.md)

---

## Class: BaseWidget

### Description
Base class for [Canvas](Canvas.md#class-canvas) and [DrawItem](DrawItem.md#class-drawitem).

---
## Attr: BaseWidget.autoDraw

### Description
If true, this widget will draw itself immediately after it is created.

For [Canvas](Canvas.md#class-canvas), note that you should turn this OFF for any canvases that are provided as children of other canvases, or they will draw initially, then be clear()ed and drawn again when added as children, causing a large performance penalty.

For [DrawItem](DrawItem.md#class-drawitem), the item will be drawn to its [drawPane](DrawItem.md#attr-drawitemdrawpane) immediately, if one is specified.

### Groups

- drawing

**Flags**: IR

---
## Attr: BaseWidget.ID

### Description
Global identifier for referring to the widget in JavaScript. The ID property is optional if you do not need to refer to the widget from JavaScript, or can refer to it indirectly (for example, by storing the reference returned by [create()](Class.md#classmethod-classcreate)).

An internal, unique ID will automatically be created upon instantiation for any widget where one is not provided.

### Groups

- basics

**Flags**: IR

---
