# DrawShape Documentation

[← Back to API Index](../main.md)

---

## Class: DrawShape

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem to render a shape defined by executing the series of drawing commands in the [commands](#attr-drawshapecommands) array.

---
## Attr: DrawShape.titleRotationMode

### Description
The mode in which the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) (if shown) is rotated with this draw item.

### See Also

- [DrawItem.title](DrawItem.md#attr-drawitemtitle)

**Flags**: IRA

---
## Attr: DrawShape.commands

### Description
The drawing commands that will be executed to render the shape.

**Flags**: IRW

---
## Method: DrawShape.moveBy

### Description
Move the drawShape by the specified delta

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../main.md#type-distance) | false | — | number of pixels to move horizontally |
| dY | [Distance](../main.md#type-distance) | false | — | number of pixels to move vertically |

---
## Method: DrawShape.setCommands

### Description
Sets the [commands](#attr-drawshapecommands) that define this shape.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| commands | [Array of DrawShapeCommand](#type-array-of-drawshapecommand) | false | — | the new commands. |

---
## Method: DrawShape.resizeBy

### Description
Resize by the specified delta

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../main.md#type-distance) | false | — | number of pixels to resize by horizontally |
| dY | [Distance](../main.md#type-distance) | false | — | number of pixels to resize by vertically |

---
