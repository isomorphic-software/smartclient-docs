# DrawLinePath Documentation

[← Back to API Index](../main.md)

---

## Class: DrawLinePath

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to render a connector between two points. If the points are aligned on one axis, this connector will draw as a straight line. If the points are offset on both axes and there is enough space, the connector will by default draw short horizontal segments from the start and end points, and a diagonal segment connecting the ends of these 'tail' segments. Connector style and orientation defaults may be changed through configuration.

---
## Attr: DrawLinePath.connectorOrientation

### Description
The ConnectorOrientation controlling the orientation and behavior of this line's tail segments.

### Groups

- line

**Flags**: IR

---
## Attr: DrawLinePath.startTop

### Description
Starting top coordinate of the line. Overrides top coordinate of [DrawLinePath.startPoint](#attr-drawlinepathstartpoint) if both are set.

**Flags**: IR

---
## Attr: DrawLinePath.endArrow

### Description
Style of arrow head to draw at the end of the line or path.

**Flags**: IRW

---
## Attr: DrawLinePath.endTop

### Description
Ending top coordinate of the line. Overrides top coordinate of [DrawLinePath.endPoint](#attr-drawlinepathendpoint) if both are set.

**Flags**: IR

---
## Attr: DrawLinePath.controlPoint1

### Description
The point at which the leading tail segment joins the connecting center segment.

**Flags**: IRW

---
## Attr: DrawLinePath.startLeft

### Description
Starting left coordinate of the line. Overrides left coordinate of [DrawLinePath.startPoint](#attr-drawlinepathstartpoint) if both are set.

**Flags**: IR

---
## Attr: DrawLinePath.showTitleLabelBackground

### Description
If the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) is showing, should the [titleLabelBackground](DrawItem.md#attr-drawitemtitlelabelbackground) be created and placed behind the `titleLabel`?

This defaults to true for [DrawSector](DrawSector.md#class-drawsector)s and shapes that are not commonly filled (e.g. [DrawLine](DrawLine.md#class-drawline)s).

**Flags**: IRA

---
## Attr: DrawLinePath.endPoint

### Description
End point of the line

**Flags**: IRW

---
## Attr: DrawLinePath.titleRotationMode

### Description
The mode in which the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) (if shown) is rotated with this draw item.

### See Also

- [DrawItem.title](DrawItem.md#attr-drawitemtitle)

**Flags**: IRA

---
## Attr: DrawLinePath.knobs

### Description
Array of control knobs to display for this item. Each [KnobType](../main.md#type-knobtype) specified in this will turn on UI element(s) allowing the user to manipulate this DrawLinePath. To update the set of knobs at runtime use [DrawItem.showKnobs](DrawItem.md#method-drawitemshowknobs) and [DrawItem.hideKnobs](DrawItem.md#method-drawitemhideknobs).

DrawLinePath supports the "startPoint", "endPoint", "controlPoint1", and "controlPoint2" knob types.

### See Also

- [DrawItem.knobs](DrawItem.md#attr-drawitemknobs)

**Flags**: IR

---
## Attr: DrawLinePath.connectorStyle

### Description
The ConnectorStyle controlling the presentation and behavior of this line's tail segments.

### Groups

- line

**Flags**: IR

---
## Attr: DrawLinePath.endLeft

### Description
Ending left coordinate of the line. Overrides left coordinate of [DrawLinePath.endPoint](#attr-drawlinepathendpoint) if both are set.

**Flags**: IR

---
## Attr: DrawLinePath.tailSize

### Description
Length of the horizontal/vertical "tail segments" between the start and end points of this DrawLinePath and the connecting center segment.

**Flags**: IR

---
## Attr: DrawLinePath.startPoint

### Description
Start point of the line

**Flags**: IRW

---
## Attr: DrawLinePath.controlPoint2

### Description
The point at which the trailing tail segment joins the connecting center segment. Has no effect on lines with right angle ConnectorStyles.

**Flags**: IRW

---
## Method: DrawLinePath.getCenter

### Description
Get the center point of the line path.

### Returns

`[Point](#type-point)` — the center point

---
## Method: DrawLinePath.moveStartPointTo

### Description
Moves the line path such that the [DrawLinePath.startPoint](#attr-drawlinepathstartpoint) ends up at the specified point.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../main_2.md#type-integer) | false | — | new left coordinate in pixels |
| top | [Integer](../main_2.md#type-integer) | false | — | new top coordinate in pixels |

---
## Method: DrawLinePath.setStartPoint

### Description
Update the startPoint

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for start point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for start point, in pixels |

---
## Method: DrawLinePath.moveBy

### Description
Move both the start and end points of the line by a relative amount.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Distance](../main.md#type-distance) | false | — | change to left coordinate in pixels |
| top | [Distance](../main.md#type-distance) | false | — | change to top coordinate in pixels |

---
## Method: DrawLinePath.setControlPoint2

### Description
Sets the coordinates of the controlPoint2 knob and by extension the coordinates of this DrawLinePath's trailing tail segment.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for start point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for start point, in pixels |

---
## Method: DrawLinePath.getBoundingBox

### Description
Returns the startPoint, endPoint

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
## Method: DrawLinePath.setEndPoint

### Description
Update the endPoint

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for end point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for end point, in pixels |

---
## Method: DrawLinePath.setControlPoint1

### Description
Sets the coordinates of the controlPoint1 knob and by extension the coordinates of this DrawLinePath's leading tail segment.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | left coordinate for start point, in pixels |
| top | [Coordinate](../main.md#type-coordinate) | false | — | top coordinate for start point, in pixels |

---
