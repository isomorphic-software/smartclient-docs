# DrawPolygon Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawPolygon

*Inherits from:* [DrawPath](DrawPath.md#class-drawpath)

### Description
DrawItem subclass to render polygons

---
## Attr: DrawPolygon.knobs

### Description
DrawPolygon only supports the "move" knob type.

### See Also

- [DrawItem.knobs](DrawItem.md#attr-drawitemknobs)

**Flags**: IR

---
## Attr: DrawPolygon.lineCap

### Description
Style of drawing the corners of the polygon.

### Groups

- line

**Flags**: IRW

---
## Attr: DrawPolygon.points

### Description
Array of points of the polygon, specified in the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawPolygon.titleRotationMode

### Description
The mode in which the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) (if shown) is rotated with this draw item.

### See Also

- [DrawItem.title](DrawItem.md#attr-drawitemtitle)

**Flags**: IRA

---
## Attr: DrawPolygon.showTitleLabelBackground

### Description
If the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) is showing, should the [titleLabelBackground](DrawItem.md#attr-drawitemtitlelabelbackground) be created and placed behind the `titleLabel`?

This defaults to true for [DrawSector](DrawSector.md#class-drawsector)s and shapes that are not commonly filled (e.g. [DrawLine](DrawLine.md#class-drawline)s).

**Flags**: IRA

---
