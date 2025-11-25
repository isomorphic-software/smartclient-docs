# DrawImage Documentation

[← Back to API Index](../main.md)

---

## Class: DrawImage

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to render embedded images.

---
## Attr: DrawImage.top

### Description
Top coordinate in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawImage.src

### Description
URL to the image file.

**Flags**: IRW

---
## Attr: DrawImage.title

### Description
Title (tooltip hover text) for this image.

**Flags**: IR

---
## Attr: DrawImage.height

### Description
Height in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawImage.width

### Description
Width in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Attr: DrawImage.useMatrixFilter

### Description
Configures whether a Matrix filter is used to render this DrawImage in Internet Explorer 6-8.

With the default of `null`, matrix filters may be used unless [Canvas.neverUseFilters](Canvas.md#classattr-canvasneverusefilters) has been set. When set explicitly to `true`, matrix filters may be used even if `neverUseFilters` is `true`.

This setting exists due to platform limitations in Internet Explorer where it is impossible to implement shearing transforms on an image without a matrix filter. Shear can arise by:

*   specifying a nonzero [xShearFactor](DrawItem.md#attr-drawitemxshearfactor) or [yShearFactor](DrawItem.md#attr-drawitemyshearfactor),
*   specifying a nonuniform [scale](DrawItem.md#attr-drawitemscale) (where the scale values along the x- and y-dimensions are not equal) and a nonzero [rotation](DrawItem.md#attr-drawitemrotation), or
*   using "resize" [control knobs](DrawItem.md#attr-drawitemknobs) on a rotated DrawImage.

When prohibited from using a matrix filter, DrawImage will ignore the shearing components of its local transform. If any of the above conditions are met then the DrawImage might not be drawn correctly. Setting `useMatrixFilter` to `true` avoids this possibility but it also suffers from a range of side-effects mentioned [here](../kb_topics/IEFilters.md#kb-topic-internet-explorer-filter-effects).

### Groups

- IEFilters

**Flags**: IR

---
## Attr: DrawImage.left

### Description
Left coordinate in pixels relative to the [local coordinate system](DrawPane.md#class-drawpane).

**Flags**: IRW

---
## Method: DrawImage.setSrc

### Description
Change the URL of the image displayed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| src | [URL](../main_2.md#type-url) | false | — | new URL |

---
## Method: DrawImage.setRect

### Description
Updates the drawImage to match the specified coordinates and size in [local coordinates](DrawPane.md#class-drawpane).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../main_2.md#type-integer) | false | — | new left coordinate |
| top | [Integer](../main_2.md#type-integer) | false | — | new top coordinate |
| width | [Integer](../main_2.md#type-integer) | false | — | new width |
| height | [Integer](../main_2.md#type-integer) | false | — | new height |

---
## Method: DrawImage.setTop

### Description
Set the top coordinate of the drawImage.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| top | [Coordinate](../main.md#type-coordinate) | false | — | new top coordinate |

---
## Method: DrawImage.setHeight

### Description
Set the height of the drawImage.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Distance](../main.md#type-distance) | false | — | new height |

---
## Method: DrawImage.moveBy

### Description
Move the drawImage by the specified delta

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [Distance](../main.md#type-distance) | false | — | number of pixels to move horizontally |
| dY | [Distance](../main.md#type-distance) | false | — | number of pixels to move vertically |

---
## Method: DrawImage.getBoundingBox

### Description
Returns the top, left, top+width, left+height

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
## Method: DrawImage.moveTo

### Description
Move the drawImage to the specified position

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../main_2.md#type-integer) | false | — | new left coordinate |
| top | [Integer](../main_2.md#type-integer) | false | — | new top coordinate |

---
## Method: DrawImage.setLeft

### Description
Set the left coordinate of the drawImage.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Coordinate](../main.md#type-coordinate) | false | — | new left coordinate |

---
## Method: DrawImage.setWidth

### Description
Set the width of the drawImage.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Distance](../main.md#type-distance) | false | — | new width |

---
## Method: DrawImage.getCenter

### Description
Get the center point of the image.

### Returns

`[Point](#type-point)` — the center point

---
