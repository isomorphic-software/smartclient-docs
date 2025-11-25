# DrawCurve Documentation

[← Back to API Index](../main.md)

---

## Class: DrawCurve

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem that renders cubic bezier curves.

---
## Attr: DrawCurve.controlPoint1

### Description
First cubic bezier control point.

**Flags**: IRW

---
## Attr: DrawCurve.lineCap

### Description
Style of drawing the endpoints of a line.

Note that for dashed and dotted lines, the lineCap style affects each dash or dot.

### Groups

- line

**Flags**: IRW

---
## Attr: DrawCurve.endPoint

### Description
End point of the curve

**Flags**: IRW

---
## Attr: DrawCurve.showTitleLabelBackground

### Description
If the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) is showing, should the [titleLabelBackground](DrawItem.md#attr-drawitemtitlelabelbackground) be created and placed behind the `titleLabel`?

This defaults to true for [DrawSector](DrawSector.md#class-drawsector)s and shapes that are not commonly filled (e.g. [DrawLine](DrawLine.md#class-drawline)s).

**Flags**: IRA

---
## Attr: DrawCurve.knobs

### Description
Array of control knobs to display for this item. Each [KnobType](../main.md#type-knobtype) specified in this will turn on UI element(s) allowing the user to manipulate this DrawCurve. To update the set of knobs at runtime use [DrawItem.showKnobs](DrawItem.md#method-drawitemshowknobs) and [DrawItem.hideKnobs](DrawItem.md#method-drawitemhideknobs).

DrawCurve supports the "startPoint", "endPoint", "controlPoint1", and "controlPoint2" knob types.

### See Also

- [DrawItem.knobs](DrawItem.md#attr-drawitemknobs)

**Flags**: IR

---
## Attr: DrawCurve.startPoint

### Description
Start point of the curve

**Flags**: IRW

---
## Attr: DrawCurve.c2Knob

### Description
If this item is showing "controlPoint2" [control knobs](DrawItem.md#attr-drawitemknobs), this attribute specifies the AutoChild for the [DrawKnob](DrawKnob.md#class-drawknob) for control point 2 of current drawCurve.

**Flags**: IR

---
## Attr: DrawCurve.controlPoint2

### Description
Second cubic bezier control point.

**Flags**: IRW

---
## Attr: DrawCurve.c1Knob

### Description
If this item is showing "controlPoint1" [control knobs](DrawItem.md#attr-drawitemknobs), this attribute specifies the AutoChild for the [DrawKnob](DrawKnob.md#class-drawknob) for control point 1 of current drawCurve.

**Flags**: IR

---
## Method: DrawCurve.setStartPoint

### Description
Update the startPoint

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for start point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for start point, in pixels |

---
## Method: DrawCurve.getBoundingBox

### Description
Returns the smallest box containing the entire curve.

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
## Method: DrawCurve.setEndPoint

### Description
Update the endPoint

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for end point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for end point, in pixels |

---
## Method: DrawCurve.moveStartPointTo

### Description
Move the start point, end point, and control points of the curve such that the [DrawCurve.startPoint](#attr-drawcurvestartpoint) ends up at the specified coordinates and the shape of the curve is unchanged.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Integer](../main_2.md#type-integer) | false | — | new x coordinate in pixels |
| y | [Integer](../main_2.md#type-integer) | false | — | new y coordinate in pixels |

---
## Method: DrawCurve.moveBy

### Description
Increment start, end and control points of this curve

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Distance](../main.md#type-distance) | false | — | new x coordinate in pixels |
| y | [Distance](../main.md#type-distance) | false | — | new y coordinate in pixels |

---
## Method: DrawCurve.setControlPoint2

### Description
Updates the second cubic Bézier control point.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for control point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for control point, in pixels |

---
## Method: DrawCurve.setControlPoint1

### Description
Updates the first cubic Bézier control point.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for control point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for control point, in pixels |

---
## Method: DrawCurve.getCenter

### Description
Get the center point of the rectangle from the curve's [startPoint](#attr-drawcurvestartpoint) to the [endPoint](#attr-drawcurveendpoint).

### Returns

`[Point](#type-point)` — the center point

---
