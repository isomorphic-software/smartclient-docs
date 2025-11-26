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

**Note:** If an auto-centering Window is either programmatically moved or dragged by an end user, auto-centering behavior is automatically turned off. To manually center a Window, you can use [centerInPage()](Window.md#method-windowcenterinpage). Auto-centering will also be disabled if you pass an explicit [left](Canvas.md#attr-canvasleft) or [top](Canvas.md#attr-canvastop) value at [create time](Class.md#classmethod-classcreate).

### Groups

- appearance
- location

**Flags**: IRW

---
## Attr: ModalWindow.width

### Description
The `canvas.width` attribute specifies the size for a component's horizontal dimension; `canvas.height` specifies the size for the vertical dimension.

May be set to an integer value (a number of pixels), a percentage value like "50%", or "\*".

See [percentSizing](../kb_topics/percentSizing.md#kb-topic-canvas-percentage-sizing) for details on how percentage or `"*"` values are resolved actual size.

If [overflow](Canvas.md#attr-canvasoverflow) is set to "visible", the specified size acts as a minimum, and the component may overflow to show all content and/or children.

Note that developers wishing to set a default width or height for a component class should set [defaultWidth](Canvas.md#attr-canvasdefaultwidth) or [Canvas.defaultHeight](Canvas.md#attr-canvasdefaultheight) instead of specifying an explicit default `width` or `height`. This is important for components added to a [Layout](Layout.md#class-layout) as members - it allows the Layout to determine whether the canvas has an explicitly specified size that must be respected, or whether it can participate in its [sizing policies](../reference_2.md#type-layoutpolicy).

### Groups

- sizing

**Flags**: IRW

---
## Attr: ModalWindow.height

### Description
The `canvas.width` attribute specifies the size for a component's horizontal dimension; `canvas.height` specifies the size for the vertical dimension.

May be set to an integer value (a number of pixels), a percentage value like "50%", or "\*".

See [percentSizing](../kb_topics/percentSizing.md#kb-topic-canvas-percentage-sizing) for details on how percentage or `"*"` values are resolved actual size.

If [overflow](Canvas.md#attr-canvasoverflow) is set to "visible", the specified size acts as a minimum, and the component may overflow to show all content and/or children.

Note that developers wishing to set a default width or height for a component class should set [defaultWidth](Canvas.md#attr-canvasdefaultwidth) or [Canvas.defaultHeight](Canvas.md#attr-canvasdefaultheight) instead of specifying an explicit default `width` or `height`. This is important for components added to a [Layout](Layout.md#class-layout) as members - it allows the Layout to determine whether the canvas has an explicitly specified size that must be respected, or whether it can participate in its [sizing policies](../reference_2.md#type-layoutpolicy).

### Groups

- sizing

**Flags**: IRW

---
## Attr: ModalWindow.visibility

### Description
Controls widget visibility when the widget is initialized. See [Visibility](../reference_2.md#type-visibility) type for details.

Specifying "visible" sets the CSS visiblity to "visible", forcing a child to be visible even if the parent is hidden. **Not supported for use with SmartClient layouts, scrolling or auto-sizing** but may be useful when working with third-party or legacy DOM layout systems.

Note that if [hideUsingDisplayNone](Canvas.md#attr-canvashideusingdisplaynone) is set for a hidden ancestor, setting `visibility` will have no effect at all until that ancestor becomes visible.

### Groups

- appearance

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
