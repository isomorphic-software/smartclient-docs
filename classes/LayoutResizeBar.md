# LayoutResizeBar Documentation

[← Back to API Index](../reference.md)

---

## Class: LayoutResizeBar

*Inherits from:* [Splitbar](Splitbar.md#class-splitbar)

### Description
This class exists principally to make it easier to create resize bars when using visual design tools, since a `LayoutResizeBar` can be dropped into a Layout like any other [Canvas](Canvas.md#class-canvas). The recommended way to create a resize bar is to simply set [Canvas.showResizeBar](Canvas.md#attr-canvasshowresizebar) on the member that you want to be able to resize or collapse, creating it as an [autochild](Layout.md#attr-layoutresizebar).

Note that this class extends whatever class is specified as the prototype default for [Layout.resizeBarClass](Layout.md#attr-layoutresizebarclass) in the current skin. So for some skins it may actually extend [Snapbar](Snapbar.md#class-snapbar) rather than [Splitbar](Splitbar.md#class-splitbar).

### See Also

- [Layout](Layout.md#class-layout)
- [Canvas.resizeBarTarget](Canvas.md#attr-canvasresizebartarget)

---
## Attr: LayoutResizeBar.canCollapse

### Description
If this property is true, a click on the Splitbar will collapse its [target](Splitbar.md#attr-splitbartarget), hiding it and shifting the Splitbar and other members of the layout across to fill the newly available space. If the target is already hidden a click will expand it again (showing it at its normal size).

Note that on touch devices, to enable collapsing/uncollapsing the `target` in response to a tap, [canCollapseOnTap](Splitbar.md#attr-splitbarcancollapseontap) must be set to `true`.

**Flags**: IRW

---
## Attr: LayoutResizeBar.resizeDirection

### Description
Whether this `LayoutResizeBar` [layout member](Layout.md#attr-layoutmembers) should resize the member before or after it in the layout. If [LayoutResizeBar.canCollapse](#attr-layoutresizebarcancollapse) is true, this property also determines which member is hidden when the `LayoutResizeBar` is clicked.

Compare this property with the corresponding setting [Canvas.resizeBarTarget](Canvas.md#attr-canvasresizebartarget), meaningful when an autochild resize bar is created with [Canvas.showResizeBar](Canvas.md#attr-canvasshowresizebar). Note that if such an autochild would be shown right before an `LayoutResizeBar` member, due to [showResizeBar](Canvas.md#attr-canvasshowresizebar) or [Layout.defaultResizeBars](Layout.md#attr-layoutdefaultresizebars), it will be disabled in favor of the `LayoutResizeBar`, though the [resizeBarTarget](Canvas.md#attr-canvasresizebartarget) setting will be applied if this property's prototype default hasn't been overridden in the resize bar instance.

**Flags**: IRW

---
## Attr: LayoutResizeBar.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Method: LayoutResizeBar.setResizeDirection

### Description
Setter for [ResizeDirection](../reference.md#type-resizedirection).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| direction | [ResizeDirection](../reference.md#type-resizedirection) | false | — | the new direction to target |

---
