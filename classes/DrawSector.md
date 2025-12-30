# DrawSector Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawSector

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to render Pie Slices.

---
## Attr: DrawSector.radius

### Description
Radius of the sector.

**Flags**: IR

---
## Attr: DrawSector.startAngle

### Description
Start angle of the sector in degrees. Default of 0.0 will create a sector that starts with a line from the [DrawSector.centerPoint](#attr-drawsectorcenterpoint) and extends horizontally to the right for the indicated [DrawSector.radius](#attr-drawsectorradius), then sweeps clockwise toward the [DrawSector.endAngle](#attr-drawsectorendangle).

Note that the startAngle may validly be a greater numeric value than the endAngle. The sector will always be drawn clockwise from startAngle to endAngle, so a sector with startAngle of 350 and endAngle of 10 would draw a 20-degree segment sticking out to the right of the centerPoint.

Drawing a full circle: A developer may have a drawSector transcribe a full circle by using values of 360 or greater as the end point. For example a drawSector with startAngle set to 350 and endAngle set to 710 would transcribe a full circle which starts and ends on the same line (10 degrees above the horizontal, to the right of the centerPoint).

**Flags**: IR

---
## Attr: DrawSector.showTitleLabelBackground

### Description
If the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) is showing, should the [titleLabelBackground](DrawItem.md#attr-drawitemtitlelabelbackground) be created and placed behind the `titleLabel`?

This defaults to true for [DrawSector](#class-drawsector)s and shapes that are not commonly filled (e.g. [DrawLine](DrawLine.md#class-drawline)s).

**Flags**: IRA

---
## Attr: DrawSector.centerPoint

### Description
Center point of the sector

**Flags**: IRW

---
## Attr: DrawSector.endAngle

### Description
End angle of the sector in degrees. See [DrawSector.startAngle](#attr-drawsectorstartangle) for further details.

**Flags**: IR

---
## Attr: DrawSector.rotation

### Description
Rotation in degrees about the [centerPoint](#attr-drawsectorcenterpoint) of the DrawSector. The positive direction is clockwise.

**Flags**: IR

---
## Attr: DrawSector.knobs

### Description
DrawSector only supports the "move" knob type.

### See Also

- [DrawItem.knobs](DrawItem.md#attr-drawitemknobs)

**Flags**: IR

---
## ClassMethod: DrawSector.getArcMidpoint

### Description
Calculates the midpoint coordinates of the circular arc of the sector defined by the given centerPoint, startAngle, endAngle, and radius. The formula for this point is:

> ```
> var averageAngle = (startAngle + endAngle) / 2; // in degrees
> [centerX + radius * cosdeg(averageAngle), centerY + radius * sindeg(averageAngle)]
> ```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| centerX | [double](../reference.md#type-double) | false | — | X coordinate of the center point of the sector. |
| centerY | [double](../reference.md#type-double) | false | — | Y coordinate of the center point of the sector. |
| startAngle | [double](../reference.md#type-double) | false | — | start angle of the sector in degrees. |
| endAngle | [double](../reference.md#type-double) | false | — | end angle of the sector in degrees. |
| radius | [double](../reference.md#type-double) | false | — | radius of the sector. |

### Returns

`[Point](#type-point)` — the coordinates of the midpoint of the arc.

---
## Method: DrawSector.getCenter

### Description
Returns the sector's [centerPoint](#attr-drawsectorcenterpoint).

### Returns

`[Point](#type-point)` — the current centerPoint

---
## Method: DrawSector.setCenterPoint

### Description
Change the center point for this sector.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../reference.md#type-coordinate) | false | — | X coordinate of the center point (in the global coordinate system). |
| top | [Coordinate](../reference.md#type-coordinate) | false | — | Y coordinate of the center point (in the global coordinate system. |

---
## Method: DrawSector.moveBy

### Description
Move the DrawSector by the specified amounts.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [Distance](../reference.md#type-distance) | false | — | number of pixels to move by horizontally |
| y | [Distance](../reference.md#type-distance) | false | — | number of pixels to move by vertically |

---
## Method: DrawSector.getArcMidpoint

### Description
Calculates the coordinates of the midpoint of this DrawSector's circular arc. The formula for this point is:

> ```
> var averageAngle = (startAngle + endAngle) / 2; // in degrees
> [centerX + radius * cosdeg(averageAngle), centerY + radius * sindeg(averageAngle)]
> ```

### Returns

`[Point](#type-point)` — the coordinates of the midpoint of the arc.

---
## Method: DrawSector.getBoundingBox

### Description
Returns the centerPoint endPoint

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
