# EdgedCanvas Documentation

[← Back to API Index](../main.md)

---

## Class: EdgedCanvas

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
EdgedCanvas acts as a decorative, image-based frame around another single Canvas.

### Groups

- imageEdges

---
## Attr: EdgedCanvas.edgeRight

### Description
Height in pixels for right corners and edges. Defaults to edgeSize when unset.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.edgeOffsetBottom

### Description
Amount the contained Canvas should be offset from the bottom. Defaults to the size for the bottom edge. Set smaller to allow the contained Canvas to overlap the edge and corner media.

### Groups

- imageEdges

**Flags**: IRA

---
## Attr: EdgedCanvas.edgeOffsetRight

### Description
Amount the contained Canvas should be offset from the right. Defaults to the size for the right edge. Set smaller to allow the contained Canvas to overlap the edge and corner media.

### Groups

- imageEdges

**Flags**: IRA

---
## Attr: EdgedCanvas.edgeOffset

### Description
Amount the contained Canvas should be offset. Defaults to edgeSize; set to less than edgeSize to allow the contained Canvas to overlap the edge and corner media.

### Groups

- imageEdges

**Flags**: IRA

---
## Attr: EdgedCanvas.showCenter

### Description
Whether to show media in the center section, that is, behind the decorated Canvas.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.edgeLeft

### Description
Height in pixels for left corners and edges. Defaults to edgeSize when unset.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.edgeBottom

### Description
Height in pixels for bottom corners and edges. Defaults to edgeSize when unset.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.centerBackgroundColor

### Description
Background color for the center section only. Can be used as a surrogate background color for the decorated Canvas, if the Canvas is set to partially overlap the edges and hence can't show a background color itself without occluding media.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.edgeOffsetTop

### Description
Amount the contained Canvas should be offset from the top. Defaults to the size for the top edge. Set smaller to allow the contained Canvas to overlap the edge and corner media.

### Groups

- imageEdges

**Flags**: IRA

---
## Attr: EdgedCanvas.customEdges

### Description
Array of side names ("T", "B", "L", "R") specifying which sides of the decorated component should show edges. For example:
```
      customEdges : ["T", "B"]
 
```
.. would show edges only on the top and bottom of a component.

The default of `null` means edges will be shown on all sides.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.edgeStyleName

### Description
Optional property specifying the CSS ClassName to apply to the various parts of this edged canvas (top, bottom, corners, sides and center). To apply separate styles for each part, use [EdgedCanvas.addEdgeStyleSuffix](#attr-edgedcanvasaddedgestylesuffix).

### Groups

- imageEdgeStyles
- imageEdges

**Flags**: IRW

---
## Attr: EdgedCanvas.edgeColor

### Description
CSS color (WITHOUT "#") for the edges. If specified, will be used as part of image names. Example: "edge\_88FF88\_TL.gif".

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.edgeImage

### Description
Base name of images for edges. Extensions for each corner or edge piece will be added to this image URL, before the extension. For example, with the default base name of "edge.gif", the top-left corner image will be "edge\_TL.gif".

The full list of extensions is: "\_TL", "\_TR", "\_BL", "\_BR", "\_T", "\_L", "\_B", "\_R", "\_center".

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.addEdgeStyleSuffix

### Description
If specified, the [EdgedCanvas.edgeStyleName](#attr-edgedcanvasedgestylename) will be treated as a base style name and appended with following suffixes to support separate styling per cell:

`_TL` (top left cell)  
`_T` (top center cell)  
`_TR` (top right cell)  
`_L` (middle left cell)  
`_C` (center cell)  
`_R` (middle right cell)  
`_BL` (bottom left cell)  
`_B` (bottom center cell)  
`_BR` (bottom right cell)

### Groups

- imageEdgeStyles
- imageEdges

**Flags**: IRW

---
## Attr: EdgedCanvas.edgeSize

### Description
Size in pixels for corners and edges

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.edgeTop

### Description
Height in pixels for top corners and edges. Defaults to edgeSize when unset.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: EdgedCanvas.edgeOffsetLeft

### Description
Amount the contained Canvas should be offset from the left. Defaults to the size for the left edge. Set smaller to allow the contained Canvas to overlap the edge and corner media.

### Groups

- imageEdges

**Flags**: IRA

---
## Attr: EdgedCanvas.skinImgDir

### Description
Standard skin directory for edge images (sides and corners).

### Groups

- imageEdges

**Flags**: IR

---
