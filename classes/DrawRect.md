# DrawRect Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawRect

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to render rectangle shapes, optionally with rounded corners.

---
## Attr: DrawRect.top

### Description
Top coordinate in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawRect.height

### Description
Height in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawRect.titleRotationMode

### Description
The mode in which the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) (if shown) is rotated with this draw item.

### See Also

- [DrawItem.title](DrawItem.md#attr-drawitemtitle)

**Flags**: IRA

---
## Attr: DrawRect.lineCap

### Description
Style of drawing the endpoints of a line.

Note that for dashed and dotted lines, the lineCap style affects each dash or dot.

### Groups

- line

**Flags**: IRW

---
## Attr: DrawRect.left

### Description
Left coordinate in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawRect.rounding

### Description
Rounding of corners, from 0 (square corners) to 1.0 (shorter edge is a semicircle).

**Flags**: IR

---
## Attr: DrawRect.width

### Description
Width in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Method: DrawRect.isPointInPath

### Description
Returns true if the given point in the drawing coordinate system is within this DrawItem's shape, taking into account local transforms.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [int](../reference.md#type-int) | false | — | X coordinate of the test point. |
| y | [int](../reference.md#type-int) | false | — | Y coordinate of the test point. |

### Returns

`[boolean](../reference.md#type-boolean)` — —

---
## Method: DrawRect.moveTo

### Description
Move the drawRect to the specified position

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left coordinate |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top coordinate |

---
## Method: DrawRect.getBoundingBox

### Description
Returns the top, left, top+height, left+width

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
## Method: DrawRect.setRect

### Description
Move and resize the drawRect to match the specified coordinates and size.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left coordinate |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top coordinate |
| width | [Integer](../reference_2.md#type-integer) | false | — | new width |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height |

---
## Method: DrawRect.getCenter

### Description
Get the center point of the rectangle.

### Returns

`[Point](#type-point)` — the center point

---
## Method: DrawRect.setHeight

### Description
Set the height of the drawRect

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Distance](../reference.md#type-distance) | false | — | new height |

---
## Method: DrawRect.resizeTo

### Description
Resize to the specified size

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Integer](../reference_2.md#type-integer) | false | — | new width |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height |

---
## Method: DrawRect.setCenter

### Description
Move the drawRect such that it is centered over the specified coordinates.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../reference.md#type-coordinate) | false | — | left coordinate for new center position |
| top | [Coordinate](../reference.md#type-coordinate) | false | — | top coordinate for new center postiion |

---
## Method: DrawRect.setTop

### Description
Set the top coordinate of the drawRect

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| top | [Coordinate](../reference.md#type-coordinate) | false | — | new top coordinate |

---
## Method: DrawRect.moveBy

### Description
Move the drawRect by the specified delta

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../reference.md#type-distance) | false | — | number of pixels to move horizontally |
| dY | [Distance](../reference.md#type-distance) | false | — | number of pixels to move vertically |

---
## Method: DrawRect.setLeft

### Description
Set the left coordinate of the drawRect

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../reference.md#type-coordinate) | false | — | new left coordinate |

---
## Method: DrawRect.resizeBy

### Description
Resize by the specified delta

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../reference.md#type-distance) | false | — | number of pixels to resize by horizontally |
| dY | [Distance](../reference.md#type-distance) | false | — | number of pixels to resize by vertically |

---
## Method: DrawRect.setWidth

### Description
Set the width of the drawRect

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Distance](../reference.md#type-distance) | false | — | new width |

---
## Method: DrawRect.setRounding

### Description
Setter method for [DrawRect.rounding](#attr-drawrectrounding)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rounding | [float](../reference.md#type-float) | false | — | new rounding value. Should be between zero (a rectangle) and 1 (shorter edge is a semicircle) |

---
