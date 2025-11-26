# DrawDiamond Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawDiamond

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to render diamond shapes

---
## Attr: DrawDiamond.titleRotationMode

### Description
The mode in which the [titleLabel](DrawItem.md#attr-drawitemtitlelabel) (if shown) is rotated with this draw item.

### See Also

- [DrawItem.title](DrawItem.md#attr-drawitemtitle)

**Flags**: IRA

---
## Attr: DrawDiamond.top

### Description
Top coordinate of the diamond. This is the Y coordinate of the northern point of the diamond.

**Flags**: IRW

---
## Attr: DrawDiamond.width

### Description
Width of the diamond. Must be non-negative.

**Flags**: IRW

---
## Attr: DrawDiamond.left

### Description
Left coordinate of the diamond. This is the X coordinate of the western point of the diamond.

**Flags**: IRW

---
## Attr: DrawDiamond.height

### Description
Height of the diamond. Must be non-negative.

**Flags**: IRW

---
## Method: DrawDiamond.setRect

### Description
Move and resize the drawDiamond to match the specified coordinates and size.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left coordinate |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top coordinate |
| width | [Integer](../reference_2.md#type-integer) | false | — | new width |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height |

---
