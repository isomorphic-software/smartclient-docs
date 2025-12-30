# DrawOval Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawOval

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to render oval shapes, including circles.

---
## Attr: DrawOval.left

### Description
Left coordinate in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawOval.titleRotationMode

### Description
The mode in which the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) (if shown) is rotated with this draw item.

### See Also

- [DrawItem.title](DrawItem.md#attr-drawitemtitle)

**Flags**: IRA

---
## Attr: DrawOval.height

### Description
Height in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawOval.centerPoint

### Description
Center point of the oval. If unset, derived from left/top/width/height.

**Flags**: IRW

---
## Attr: DrawOval.width

### Description
Width in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawOval.top

### Description
Top coordinate in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawOval.radius

### Description
Radius of the oval. Since this is used to initialize the [horizontal](#method-drawovalgetradiusx) and [vertical](#method-drawovalgetradiusy) radii, then the oval is a circle.

If unset, the horizontal and vertical radii are set to half the [width](#attr-drawovalwidth) and [height](#attr-drawovalheight).

### See Also

- [DrawOval.getRadiusX](#method-drawovalgetradiusx)
- [DrawOval.getRadiusY](#method-drawovalgetradiusy)

**Flags**: IW

---
## Method: DrawOval.setHeight

### Description
Set the height of the drawOval

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Distance](../reference.md#type-distance) | false | — | new height |

---
## Method: DrawOval.resizeBy

### Description
Resize by the specified delta. Note that the resize will occur from the current top/left coordinates, meaning the center positon of the oval may change. You may also use [DrawOval.setRadii](#method-drawovalsetradii) to change the radius in either direction without modifying the centerpoint.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../reference.md#type-distance) | false | — | number of pixels to resize by horizontally |
| dY | [Distance](../reference.md#type-distance) | false | — | number of pixels to resize by vertically |

---
## Method: DrawOval.setOval

### Description
Resize and reposition the drawOval by setting its radius, and centerPoint.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cx | [Coordinate](../reference.md#type-coordinate) | false | — | new horizontal center point coordinate |
| cy | [Coordinate](../reference.md#type-coordinate) | false | — | new vertical center point coordinate |
| rx | [Distance](../reference.md#type-distance) | false | — | new horizontal radius |
| ry | [Distance](../reference.md#type-distance) | false | — | new vertical radius |

---
## Method: DrawOval.getRadiusX

### Description
Returns the horizontal radius of the DrawOval.

### Returns

`[Distance](../reference.md#type-distance)` — the horizontal radius.

### See Also

- [DrawOval.setRadii](#method-drawovalsetradii)

---
## Method: DrawOval.setRadii

### Description
Resize the drawOval by setting its horizontal and vertical radius, and retaining its current center point.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| rx | [Distance](../reference.md#type-distance) | false | — | new horizontal radius |
| ry | [Distance](../reference.md#type-distance) | false | — | new vertical radius |

### See Also

- [DrawOval.getRadiusX](#method-drawovalgetradiusx)
- [DrawOval.getRadiusY](#method-drawovalgetradiusy)

---
## Method: DrawOval.setCenterPoint

### Description
Change the center point for this oval.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../reference.md#type-coordinate) | false | — | left coordinate (in the global coordinate system) |
| top | [Coordinate](../reference.md#type-coordinate) | false | — | top coordinate (in the global coordinate system) |

---
## Method: DrawOval.moveTo

### Description
Move the drawOval to the specified left/top position. You may also call [DrawOval.setCenterPoint](#method-drawovalsetcenterpoint) to reposition the oval around a new center position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left coordinate |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top coordinate |

---
## Method: DrawOval.getRadiusY

### Description
Returns the vertical radius of the DrawOval.

### Returns

`[Distance](../reference.md#type-distance)` — the vertical radius.

### See Also

- [DrawOval.setRadii](#method-drawovalsetradii)

---
## Method: DrawOval.getCenter

### Description
Get the center of the oval.

### Returns

`[Point](#type-point)` — the center point

---
## Method: DrawOval.setLeft

### Description
Set the left coordinate of the drawOval

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../reference.md#type-coordinate) | false | — | new left coordinate |

---
## Method: DrawOval.setWidth

### Description
Set the width of the drawOval

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Distance](../reference.md#type-distance) | false | — | new width |

---
## Method: DrawOval.setRadius

### Description
Resize the drawOval by setting its radius, and retaining its current center point. Equivalent to `setRadii(radius, radius)`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| radius | [Distance](../reference.md#type-distance) | false | — | new radius. This will be applied on both axes, meaning calling this method will always result in the DrawOval being a circle. |

### See Also

- [DrawOval.setRadii](#method-drawovalsetradii)

---
## Method: DrawOval.moveBy

### Description
Move the drawOval by the specified delta

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../reference.md#type-distance) | false | — | number of pixels to move horizontally |
| dY | [Distance](../reference.md#type-distance) | false | — | number of pixels to move vertically |

---
## Method: DrawOval.setTop

### Description
Set the top coordinate of the drawOval

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| top | [Coordinate](../reference.md#type-coordinate) | false | — | new top coordinate |

---
## Method: DrawOval.getBoundingBox

### Description
Returns the top, left, top+height, left+width

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
## Method: DrawOval.setRect

### Description
Move and resize the drawOval to match the specified coordinates and size.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left coordinate |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top coordinate |
| width | [Integer](../reference_2.md#type-integer) | false | — | new width |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height |

---
## Method: DrawOval.resizeTo

### Description
Resize to the specified size. Note that the resize will occur from the current top/left coordinates, meaning the center positon of the oval may change. You may also use [DrawOval.setRadii](#method-drawovalsetradii) to change the radius in either direction without modifying the centerpoint.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Integer](../reference_2.md#type-integer) | false | — | new width |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height |

---
