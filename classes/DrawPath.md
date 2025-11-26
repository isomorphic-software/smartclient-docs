# DrawPath Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawPath

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
Draws a multi-segment line.

---
## Attr: DrawPath.showTitleLabelBackground

### Description
If the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) is showing, should the [titleLabelBackground](DrawItem.md#attr-drawitemtitlelabelbackground) be created and placed behind the `titleLabel`?

This defaults to true for [DrawSector](DrawSector.md#class-drawsector)s and shapes that are not commonly filled (e.g. [DrawLine](DrawLine.md#class-drawline)s).

**Flags**: IRA

---
## Attr: DrawPath.points

### Description
Array of Points for the line, specified in the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawPath.knobs

### Description
DrawPath only supports the "move" knob type.

### See Also

- [DrawItem.knobs](DrawItem.md#attr-drawitemknobs)

**Flags**: IR

---
## Method: DrawPath.getBoundingBox

### Description
Returns the min, max points

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
## Method: DrawPath.resizeBy

### Description
Resize by the specified delta

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../reference.md#type-distance) | false | — | number of pixels to resize by horizontally |
| dY | [Distance](../reference.md#type-distance) | false | — | number of pixels to resize by vertically |

---
## Method: DrawPath.moveBy

### Description
Move the points by dX,dY

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../reference.md#type-distance) | false | — | delta x coordinate in pixels |
| dY | [Distance](../reference.md#type-distance) | false | — | delta y coordinate in pixels |

---
## Method: DrawPath.resizeTo

### Description
Resize to the specified size

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Integer](../reference_2.md#type-integer) | false | — | new width |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height |

---
## Method: DrawPath.moveFirstPointTo

### Description
Move all points in the path such that the first point ends up at the specified coordinates and the line lengths and angles are unchanged.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left coordinate in pixels |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top coordinate in pixels |

---
## Method: DrawPath.getCenter

### Description
Get the mean center of the path.

### Returns

`[Point](#type-point)` — the mean center

---
