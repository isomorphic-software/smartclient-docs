# ImgSplitbar Documentation

[← Back to API Index](../reference.md)

---

## Class: ImgSplitbar

*Inherits from:* [Img](Img.md#class-img)

### Description
Resize bar for use in [Layouts](Layout.md#attr-layoutresizebarclass), based on the [Img](Img.md#class-img) class. As with the [Splitbar](Splitbar.md#class-splitbar) class, widgets of this class can be displayed as a resize-bar for widgets in Layouts where showResizeBar is set to true. Provides a different appearance from the `Splitbar` class.

To specify the resizeBar class for some layout, use the [Layout.resizeBarClass](Layout.md#attr-layoutresizebarclass) property.

### See Also

- [Layout](Layout.md#class-layout)
- [Splitbar](Splitbar.md#class-splitbar)

---
## Attr: ImgSplitbar.src

### Description
The base filename or stateful image configuration for the image. Note that as the [state](StatefulCanvas.md#attr-statefulcanvasstate) of the component changes, the image displayed will be updated as described in [statefulImages](../kb_topics/statefulImages.md#kb-topic-stateful-images).

### Groups

- appearance

**Flags**: IR

---
## Attr: ImgSplitbar.vSrc

### Description
Default src to display when [ImgSplitbar.vertical](#attr-imgsplitbarvertical) is true, and [ImgSplitbar.src](#attr-imgsplitbarsrc) is unset.

### See Also

- [ImgSplitbar.src](#attr-imgsplitbarsrc)

**Flags**: IR

---
## Attr: ImgSplitbar.canCollapse

### Description
If this property is true, a click on the Splitbar will collapse its [target](Splitbar.md#attr-splitbartarget), hiding it and shifting the Splitbar and other members of the layout across to fill the newly available space. If the target is already hidden a click will expand it again (showing it at its normal size).

Note that on touch devices, to enable collapsing/uncollapsing the `target` in response to a tap, [canCollapseOnTap](Splitbar.md#attr-splitbarcancollapseontap) must be set to `true`.

**Flags**: IRW

---
## Attr: ImgSplitbar.hSrc

### Description
Default src to display when [ImgSplitbar.vertical](#attr-imgsplitbarvertical) is false, and [ImgSplitbar.src](#attr-imgsplitbarsrc) is unset.

### See Also

- [ImgSplitbar.src](#attr-imgsplitbarsrc)

**Flags**: IR

---
## Attr: ImgSplitbar.canDrag

### Description
`canDrag` set to true to allow dragging of the split bar. Dragging the Splitbar will resize it's [target](Splitbar.md#attr-splitbartarget)

**Flags**: IRW

---
## Attr: ImgSplitbar.skinImgDir

### Description
Default directory for skin images (those defined by the class), relative to the Page-wide [skinDir](Page.md#classmethod-pagegetskindir).

### Groups

- images

**Flags**: IR

---
## Attr: ImgSplitbar.vertical

### Description
Is this split bar vertically orientated?  
When a `Splitbar` is created by a layout to be the resizeBar for some member of the layout, the `vertical` property will be set to `true` if the layout is horizontal, meaning this resizeBar will be taller than it is wide, and will allow horizontal resizing of the member.

**Flags**: R

---
## Attr: ImgSplitbar.target

### Description
When a `Splitbar` is created by a layout, the `target` property of the Splitbar will be a pointer to the member for which it is acting as a resizeBar. The Splitbar will be positioned next to its target, and will resize it on drag completion.

See [Layout.resizeBarClass](Layout.md#attr-layoutresizebarclass), [Canvas.showResizeBar](Canvas.md#attr-canvasshowresizebar) and [Canvas.resizeBarTarget](Canvas.md#attr-canvasresizebartarget) for details on configuring the resize bars shown in Layouts.

**Flags**: R

---
