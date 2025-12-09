# Splitbar Documentation

[← Back to API Index](../reference.md)

---

## Class: Splitbar

*Inherits from:* [StretchImg](StretchImg.md#class-stretchimg)

### Description
Resize bar for use in [Layouts](Layout.md#attr-layoutresizebarclass), based on the [StretchImg](StretchImg.md#class-stretchimg) class. As with the [ImgSplitbar](ImgSplitbar.md#class-imgsplitbar) class, widgets of this class can be displayed as a resize-bar for widgets in Layouts where showResizeBar is set to true. Provides a different appearance from the `ImgSplitbar` class.

To specify the resizeBar class for some layout, use the [Layout.resizeBarClass](Layout.md#attr-layoutresizebarclass) property.

On mobile devices, you may find that you need to increase the breadth of the bar to make interacting with it easier (e.g. dragging or tapping). For [Layout](Layout.md#class-layout) resize bars, this can be done by setting [Layout.resizeBarSize](Layout.md#attr-layoutresizebarsize).

### See Also

- [Layout](Layout.md#class-layout)
- [ImgSplitbar](ImgSplitbar.md#class-imgsplitbar)

---
## Attr: Splitbar.showClosedGrip

### Description
If [Splitbar.showGrip](#attr-splitbarshowgrip) is true, this property determines whether the grip image displayed should show the `"Closed"` state when the [Splitbar.target](#attr-splitbartarget) is hidden. Note that if [Splitbar.invertClosedGripIfTargetAfter](#attr-splitbarinvertclosedgripiftargetafter) is true, we may show the "closed" state when the target is visible, rather than when it is hidden.

### Groups

- grip

**Flags**: IRA

---
## Attr: Splitbar.canCollapse

### Description
If this property is true, a click on the Splitbar will collapse its [target](#attr-splitbartarget), hiding it and shifting the Splitbar and other members of the layout across to fill the newly available space. If the target is already hidden a click will expand it again (showing it at its normal size).

Note that on touch devices, to enable collapsing/uncollapsing the `target` in response to a tap, [canCollapseOnTap](#attr-splitbarcancollapseontap) must be set to `true`.

**Flags**: IRW

---
## Attr: Splitbar.vSrc

### Description
Base URL for the image if [StretchImg.vertical](StretchImg.md#attr-stretchimgvertical) is true and [StretchImg.src](StretchImg.md#attr-stretchimgsrc) is unset.

### Groups

- appearance

### See Also

- [StretchImg.src](StretchImg.md#attr-stretchimgsrc)
- [StretchImg.vSrc](StretchImg.md#attr-stretchimgvsrc)

**Flags**: IR

---
## Attr: Splitbar.showDownGrip

### Description
If [StretchImg.showGrip](StretchImg.md#attr-stretchimgshowgrip) is true, this property determines whether to show the 'Down' state on the grip image when the user mousedown's on this widget. Has no effect if [StatefulCanvas.showDown](StatefulCanvas.md#attr-statefulcanvasshowdown) is false.

### Groups

- grip

**Flags**: IRA

---
## Attr: Splitbar.vResizeCursor

### Description
Cursor to display if this Splitbar is to be used for vertical resize of widgets.

### Groups

- cursor

**Flags**: IR

---
## Attr: Splitbar.targetAfter

### Description
Is the [Splitbar.target](#attr-splitbartarget) being shown before or after the bar? This property is automatically populated for `splitbar`s created by a layout.

### See Also

- [Splitbar.invertClosedGripIfTargetAfter](#attr-splitbarinvertclosedgripiftargetafter)

**Flags**: IRWA

---
## Attr: Splitbar.canCollapseOnTap

### Description
If [canCollapse](#attr-splitbarcancollapse) is `true`, should a tap result in collapsing/uncollapsing the [target](#attr-splitbartarget)?

**Flags**: IRW

---
## Attr: Splitbar.capSize

### Description
If the default items are used, capSize is the size in pixels of the first and last images in this stretchImg.

### Groups

- appearance

**Flags**: IR

---
## Attr: Splitbar.src

### Description
The base URL for the image.

The [State](../reference.md#type-state) for the component will be combined with this URL using the same approach as described in [Img.src](Img.md#attr-imgsrc). Then the image segment [name](StretchItem.md#attr-stretchitemname) as specified by each [StretchItem](../reference_2.md#object-stretchitem) is added.

For example, for a stretchImg in "Over" state with a `src` of "button.png" and a segment name of "stretch", the resulting URL would be "button\_Over\_stretch.png".

### Groups

- appearance

### See Also

- [StretchImg.hSrc](StretchImg.md#attr-stretchimghsrc)
- [StretchImg.vSrc](StretchImg.md#attr-stretchimgvsrc)

**Flags**: IR

---
## Attr: Splitbar.skinImgDir

### Description
Default directory for skin images (those defined by the class), relative to the Page-wide [skinDir](Page.md#classmethod-pagegetskindir).

### Groups

- images

**Flags**: IR

---
## Attr: Splitbar.vertical

### Description
Is this split bar vertically orientated?  
When a `Splitbar` is created by a layout to be the resizeBar for some member of the layout, the `vertical` property will be set to `true` if the layout is horizontal, meaning this resizeBar will be taller than it is wide, and will allow horizontal resizing of the member.

**Flags**: R

---
## Attr: Splitbar.hResizeCursor

### Description
Cursor to display if this Splitbar is to be used for horizontal resize of widgets.

### Groups

- cursor

**Flags**: IR

---
## Attr: Splitbar.gripImgSuffix

### Description
Suffix used the 'grip' image if [StretchImg.showGrip](StretchImg.md#attr-stretchimgshowgrip) is true.

### Groups

- grip

**Flags**: IRA

---
## Attr: Splitbar.showRollOverGrip

### Description
If [StretchImg.showGrip](StretchImg.md#attr-stretchimgshowgrip) is true, this property determines whether to show the 'Over' state on the grip image when the user rolls over on this widget. Has no effect if [StatefulCanvas.showRollOver](StatefulCanvas.md#attr-statefulcanvasshowrollover) is false.

### Groups

- grip

**Flags**: IRA

---
## Attr: Splitbar.target

### Description
When a `Splitbar` is created by a layout, the `target` property of the Splitbar will be a pointer to the member for which it is acting as a resizeBar. The Splitbar will be positioned next to its target, and will resize it on drag completion.

See [Layout.resizeBarClass](Layout.md#attr-layoutresizebarclass), [Canvas.showResizeBar](Canvas.md#attr-canvasshowresizebar) and [Canvas.resizeBarTarget](Canvas.md#attr-canvasresizebartarget) for details on configuring the resize bars shown in Layouts.

**Flags**: R

---
## Attr: Splitbar.showGrip

### Description
Should we show a "grip" image floating above the center of this widget?

### Groups

- grip

**Flags**: IRA

---
## Attr: Splitbar.cursor

### Description
Splitbars' cursors are set at init time based on whether they are to be used for vertical or horizontal resize. To customize the cursor for this class, modify [Splitbar.vResizeCursor](#attr-splitbarvresizecursor) or [Splitbar.hResizeCursor](#attr-splitbarhresizecursor) rather than this property.

### Groups

- cursor

**Flags**: IRW

---
## Attr: Splitbar.gripLength

### Description
Grip length in pixels (the long icon axis, perpendicular to the Layout direction).

If unset, grip will assume the natural length of image.

**Flags**: IR

---
## Attr: Splitbar.invertClosedGripIfTargetAfter

### Description
If [Splitbar.showClosedGrip](#attr-splitbarshowclosedgrip) is true, and [Splitbar.targetAfter](#attr-splitbartargetafter) is true should we show the "closed" state for the grip when the target is visible (rather than when it is hidden).

This property is useful for the case where the grip media is a simple directional arrow. The same image can be used for expanded state on one side of the bar or collapsed state on the other.

### Groups

- grip

**Flags**: IRWA

---
## Attr: Splitbar.gripBreadth

### Description
Grip breadth in pixels (the short icon axis, parallel to the Layout direction).

If unset, grip will assume the natural breadth of image.

**Flags**: IR

---
## Attr: Splitbar.canDrag

### Description
`canDrag` set to true to allow dragging of the split bar. Dragging the Splitbar will resize it's [target](#attr-splitbartarget)

**Flags**: IRW

---
## Attr: Splitbar.hSrc

### Description
Base URL for the image if [StretchImg.vertical](StretchImg.md#attr-stretchimgvertical) is false and [StretchImg.src](StretchImg.md#attr-stretchimgsrc) is unset.

### Groups

- appearance

### See Also

- [StretchImg.src](StretchImg.md#attr-stretchimgsrc)
- [StretchImg.vSrc](StretchImg.md#attr-stretchimgvsrc)

**Flags**: IR

---
