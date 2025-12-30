# ModalWindow Documentation

[← Back to API Index](../reference.md)

---

## Class: ModalWindow

*Inherits from:* [Window](Window.md#class-window)

### Description
A simple subclass of Window whose default configuration is appropriate for a standalone, modal window. This includes appropriate default settings for [Window.isModal](Window.md#attr-windowismodal) and [Window.autoCenter](Window.md#attr-windowautocenter), and sizing information, as well as having the window be initially [hidden](#attr-modalwindowvisibility)

This class is used by some development tools to simplify the creation of a modal window.

---
## Attr: ModalWindow.autoCenter

### Description
If true, this Window widget will automatically be centered on the page when shown. If false, it will show up in the last position it was placed (either programmatically, or by user interaction).

**Note:** If an auto-centering Window is either programmatically moved or dragged by an end user, auto-centering behavior is automatically turned off. To manually center a Window, you can use [centerInPage()](Window.md#method-windowcenterinpage).

### Groups

- appearance
- location

**Flags**: IRW

---
## Attr: ModalWindow.width

### Description
Size for this component's horizontal dimension.

Can be a number of pixels, or a percentage like "50%". Percentage sizes are resolved to pixel values as follows:

*   If a canvas has a specified [percentSource](Canvas.md#attr-canvaspercentsource), sizing will be a percentage of the size of that widget (see also [Canvas.percentBox](Canvas.md#attr-canvaspercentbox)).
*   Otherwise, if a canvas has a [master canvas](Canvas.md#method-canvasgetmastercanvas), and [snapTo](Canvas.md#attr-canvassnapto) is set for the widget, sizing will be a percentage of the size of that widget (see also [Canvas.percentBox](Canvas.md#attr-canvaspercentbox)).
*   Otherwise if this is a child of some other canvas, percentages will be based on the inner size of the [parent canvas](Canvas.md#method-canvasgetparentcanvas)'s viewport.
*   Otherwise, for top level widgets, sizing is calculated as a percentage of page size.

Note that if a [Canvas.maxWidth](Canvas.md#attr-canvasmaxwidth) or [Canvas.minWidth](Canvas.md#attr-canvasminwidth) are specified (or [Canvas.maxHeight](Canvas.md#attr-canvasmaxheight) / [Canvas.minHeight](Canvas.md#attr-canvasminheight) for heights), these properties act as explicit pixel limits on the canvas' size. For example, a canvas with [Canvas.maxWidth](Canvas.md#attr-canvasmaxwidth) set to `500`, and width specified as "100%" will not render larger than 500 pixels in width even if there is more space available in the parent canvas or percentSource.

[Layouts](Layout.md#class-layout) may specially interpret percentage sizes on their children, and also allow "\*" as a size.

Note that if [overflow](Canvas.md#attr-canvasoverflow) is set to "visible", this size is a minimum, and the component may overflow to show all content and/or children.

If trying to establish a default width for a custom component, set [defaultWidth](Canvas.md#attr-canvasdefaultwidth) instead.

### Groups

- sizing

**Flags**: IRW

---
## Attr: ModalWindow.isModal

### Description
If true, when shown this Window will intercept and block events to all other existing components on the page.

Use [showModalMask](Window.md#attr-windowshowmodalmask) to darken all other elements on the screen when a modal dialog is showing.

Chained modal windows - that is, modal windows that launch other modal windows - are allowed. You can accomplish this by simply creating a second modal Window while a modal Window is showing.

Note only top-level Windows (Windows without parents) can be modal.

### Groups

- modal

**Flags**: IRW

---
## Attr: ModalWindow.height

### Description
Size for this component's vertical dimension.

Can be a number of pixels, or a percentage like "50%". See documentation for [Canvas.width](Canvas.md#attr-canvaswidth) for details on how percentage values are resolved actual size.

Note that if [overflow](Canvas.md#attr-canvasoverflow) is set to "visible", this size is a minimum, and the component may overflow to show all content and/or children.

If trying to establish a default height for a custom component, set [defaultHeight](Canvas.md#attr-canvasdefaultheight) instead.

### Groups

- sizing

**Flags**: IRW

---
## Attr: ModalWindow.visibility

### Description
Controls widget visibility when the widget is initialized. See [Visibility](../reference.md#type-visibility) type for details.

Specifying "visible" sets the CSS visiblity to "visible", forcing a child to be visible even if the parent is hidden. **Not supported for use with SmartClient layouts, scrolling or auto-sizing** but may be useful when working with third-party or legacy DOM layout systems.

Note that if [hideUsingDisplayNone](Canvas.md#attr-canvashideusingdisplaynone) is set for a hidden ancestor, setting `visibility` will have no effect at all until that ancestor becomes visible.

### Groups

- appearance

**Flags**: IRW

---
## Attr: ModalWindow.maxWidth

### Description
Maximum width available to this Canvas.

The `maxWidth` and [ModalWindow.maxHeight](#attr-modalwindowmaxheight) settings apply to:

*   For a canvas being managed as a member of a [Layout](Layout.md#class-layout), the maximum size the layout should apply to the canvas.
*   For a canvas with a width or height specified as a percent value, a maximum numeric pixel value to limit how large the canvas is sized.
*   determining size for a Canvas in a [CanvasItem](CanvasItem.md#class-canvasitem) (`maxHeight` only)
*   end user [drag resizing](Window.md#attr-windowcandragresize)

Maximum sizes do not apply in various other circumstances where sizes are being determined, such as [ListGrid recordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents).

### Groups

- sizing

### See Also

- [Canvas.dragMaxWidth](Canvas.md#attr-canvasdragmaxwidth)

**Flags**: IRW

---
## Attr: ModalWindow.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: ModalWindow.maxHeight

### Description
Maximum height available to this Canvas. See [ModalWindow.maxWidth](#attr-modalwindowmaxwidth) for details of behavior.

### Groups

- sizing

### See Also

- [Canvas.dragMaxHeight](Canvas.md#attr-canvasdragmaxheight)

**Flags**: IRW

---
