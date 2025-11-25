# DrawLine Documentation

[← Back to API Index](../main.md)

---

## Class: DrawLine

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to render line segments.

---
## Attr: DrawLine.startPoint

### Description
Start point of the line

**Flags**: IRW

---
## Attr: DrawLine.endLeft

### Description
Ending left coordinate of the line. Overrides left coordinate of [DrawLine.endPoint](#attr-drawlineendpoint) if both are set.

**Flags**: IR

---
## Attr: DrawLine.knobs

### Description
Array of control knobs to display for this item. Each [KnobType](../main.md#type-knobtype) specified in this will turn on UI element(s) allowing the user to manipulate this DrawLine. To update the set of knobs at runtime use [DrawItem.showKnobs](DrawItem.md#method-drawitemshowknobs) and [DrawItem.hideKnobs](DrawItem.md#method-drawitemhideknobs).

DrawLine supports the "startPoint", "endPoint", and "move" knob types.

**Flags**: IR

---
## Attr: DrawLine.titleRotationMode

### Description
The mode in which the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) (if shown) is rotated with this draw item.

### See Also

- [DrawItem.title](DrawItem.md#attr-drawitemtitle)

**Flags**: IRA

---
## Attr: DrawLine.endPoint

### Description
End point of the line

**Flags**: IRW

---
## Attr: DrawLine.startLeft

### Description
Starting left coordinate of the line. Overrides left coordinate of [DrawLine.startPoint](#attr-drawlinestartpoint) if both are set.

**Flags**: IR

---
## Attr: DrawLine.endTop

### Description
Ending top coordinate of the line. Overrides top coordinate of [DrawLine.endPoint](#attr-drawlineendpoint) if both are set.

**Flags**: IR

---
## Attr: DrawLine.startTop

### Description
Starting top coordinate of the line. Overrides top coordinate of [DrawLine.startPoint](#attr-drawlinestartpoint) if both are set.

**Flags**: IR

---
## Attr: DrawLine.showTitleLabelBackground

### Description
If the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) is showing, should the [titleLabelBackground](DrawItem.md#attr-drawitemtitlelabelbackground) be created and placed behind the `titleLabel`?

This defaults to true for [DrawSector](DrawSector.md#class-drawsector)s and shapes that are not commonly filled (e.g. [DrawLine](#class-drawline)s).

**Flags**: IRA

---
## Method: DrawLine.moveBy

### Description
Move both the start and end points of the line by a relative amount.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Distance](../main.md#type-distance) | false | — | change to left coordinate in pixels |
| top | [Distance](../main.md#type-distance) | false | — | change to top coordinate in pixels |

---
## Method: DrawLine.setStartPoint

### Description
Update the startPoint

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for start point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for start point, in pixels |

---
## Method: DrawLine.getBoundingBox

### Description
Returns a bounding box for the `DrawLine`, taking into account the [lineWidth](DrawItem.md#attr-drawitemlinewidth).

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
## Method: DrawLine.getCenter

### Description
Get the midpoint of the line.

### Returns

`[Point](#type-point)` — the midpoint

---
## Method: DrawLine.setEndPoint

### Description
Update the endPoint

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for end point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for end point, in pixels |

---
## Method: DrawLine.moveStartPointTo

### Description
Move both the start and end points of the line such that the [DrawLine.startPoint](#attr-drawlinestartpoint) ends up at the specified coordinate and the line length and angle are unchanged.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../main_2.md#type-integer) | false | — | new left coordinate in pixels |
| top | [Integer](../main_2.md#type-integer) | false | — | new top coordinate in pixels |

---
## Method: DrawLine.isPointInPath

### Description
Returns true if the given point in the drawing coordinate system is within this DrawItem's shape, taking into account local transforms.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [int](../main.md#type-int) | false | — | X coordinate of the test point. |
| y | [int](../main.md#type-int) | false | — | Y coordinate of the test point. |

### Returns

`[boolean](../main.md#type-boolean)` — —

---
