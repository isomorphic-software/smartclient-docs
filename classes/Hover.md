# Hover Documentation

[← Back to API Index](../main.md)

---

## Class: Hover

### Description
The Hover class handles showing a simple SmartClient canvas containing arbitrary HTML, or triggering some other action in response to a user holding the mouse-pointer (or hovering) over a specific widget.

---
## ClassAttr: Hover.hoverCanvas

### Description
This is a single-instance widget, used to show contextual hover HTML and created lazily on the first call to [Hover.show](#classmethod-hovershow).

This component is created using the [autoChild pattern](../main.md#type-autochild), so you can configure it using [autoChild defaults](#classattr-hoverhovercanvasdefaults) and [properties](#classattr-hoverhovercanvasproperties), or change its type with [Hover.hoverCanvasConstructor](#classattr-hoverhovercanvasconstructor). Note that size and position are managed by the Hover subsystem, so not all [Canvas settings](Canvas.md#class-canvas) are supported.

To fully customize what a hover looks like, see [Hover.showHoverComponent](#classmethod-hovershowhovercomponent), which allows entirely custom widgets such as [grids](ListGrid_1.md#class-listgrid) to be shown as hovers.

**Flags**: RA

---
## ClassAttr: Hover.hoverCanvasDefaults

### Description
Defaults to apply to the Hover canvas shown when the user hovers over some widget. By default this property is set to this object:  
```
       { defaultWidth:100, 
         defaultHeight:1,
         baseStyle:"canvasHover",
         align:"left",
         valign:"top",
         opacity:null
        }
 
```
  
Note that these properties can be overridden by individual widgets showing hovers, by modifying [Canvas.hoverWidth](Canvas.md#attr-canvashoverwidth), [Canvas.hoverHeight](Canvas.md#attr-canvashoverheight), [Canvas.hoverStyle](Canvas.md#attr-canvashoverstyle), [Canvas.hoverAlign](Canvas.md#attr-canvashoveralign), [Canvas.hoverVAlign](Canvas.md#attr-canvashovervalign), [Canvas.hoverOpacity](Canvas.md#attr-canvashoveropacity), and [Canvas.hoverWrap](Canvas.md#attr-canvashoverwrap).

**Flags**: IRW

---
## ClassAttr: Hover.topOffset

### Description
When positioning the hover canvas, this will be the default top offset from the mousepointer, if no explicit position was passed to the [Hover.show](#classmethod-hovershow) method

**Flags**: RW

---
## ClassAttr: Hover.focusKeyHintLabelOffset

### Description
The [Hover.focusKeyHintLabel](#classattr-hoverfocuskeyhintlabel) appears floated over the bottom-right edge of the hover canvas. This property determines how far to offset the label from the edge.

**Flags**: IRW

---
## ClassAttr: Hover.focusKeyHintLabelHeight

### Description
Height for the [Hover.focusKeyHintLabel](#classattr-hoverfocuskeyhintlabel)

**Flags**: IRW

---
## ClassAttr: Hover.leftOffset

### Description
When positioning the hover canvas, this will be the default left offset from the mousepointer, if no explicit position was passed to the [Hover.show](#classmethod-hovershow) method

**Flags**: RW

---
## ClassAttr: Hover.moveWithMouse

### Description
When the Hover canvas is shown by default, should it move as the user moves the mouse pointer?  
May be overridden by including a `moveWithMouse` attribute on the properties block passed to [Hover.show](#classmethod-hovershow)

**Flags**: RWA

---
## ClassAttr: Hover.hoverCanvasConstructor

### Description
[SmartClient Class](../main.md#type-scclassname) to use for showing hover HTML; a [Label](Label.md#class-label) by default and instantiated lazily as the first hover is requested.

**Flags**: IR

---
## ClassAttr: Hover.focusKeyHintLabelWidth

### Description
Width for the [Hover.focusKeyHintLabel](#classattr-hoverfocuskeyhintlabel)

**Flags**: IRW

---
## ClassAttr: Hover.persistent

### Description
Allows interaction with hovers when the cursor is positioned over them.

It is recommended to use [hoverPersist](Canvas.md#attr-canvashoverpersist) on canvas-instances for most cases of controlling hover persistence. Changing the system-wide default hover setting could interfere with features of built-in components, but is allowed for rare cases like manually showing a hover via [Hover.show](#classmethod-hovershow) - you should just restore the default mode after the hover is hidden.

### Groups

- hovers

**Flags**: IRA

---
## ClassAttr: Hover.focusKeyHintLabel

### Description
The focusKeyHintLabel is automatically generated when showing the standard hover for canvases with a specified [Canvas.hoverFocusKey](Canvas.md#attr-canvashoverfocuskey), if [Hover.showFocusKeyHint](#classattr-hovershowfocuskeyhint) is true.

Its content is determined via [Hover.focusKeyHintMessage](#classattr-hoverfocuskeyhintmessage) and its sizing and placement may be configured via [Hover.focusKeyHintLabelWidth](#classattr-hoverfocuskeyhintlabelwidth), [Hover.focusKeyHintLabelHeight](#classattr-hoverfocuskeyhintlabelheight) and [Hover.focusKeyHintLabelOffset](#classattr-hoverfocuskeyhintlabeloffset). Other configuration can be applied via the standard [autoChild configuration pattern](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren).

**Flags**: IRW

---
## ClassAttr: Hover.hoverCanvasProperties

### Description
Properties to apply to the [hoverCanvas](#classattr-hoverhovercanvas) used to show contextual HTML when the user holds the mouse over some widget.

**Flags**: IRW

---
## ClassAttr: Hover.showFocusKeyHint

### Description
If [Canvas.hoverFocusKey](Canvas.md#attr-canvashoverfocuskey) is set, should we show a [hint label autoChild](#classattr-hoverfocuskeyhintlabel) within the standard hover canvas, prompting the user which focus key to press?

**Flags**: IRW

---
## ClassAttr: Hover.focusKeyHintLabelConstructor

### Description
Constructor for the [Hover.focusKeyHintLabel](#classattr-hoverfocuskeyhintlabel)

**Flags**: IRA

---
## ClassAttr: Hover.focusKeyHintMessage

### Description
Dynamic string message to display within the [Hover.focusKeyHintLabel](#classattr-hoverfocuskeyhintlabel).

The specified hover focus key name is available via the variable _${focusKey}_.

**Flags**: IRW

---
## ClassAttr: Hover.edgeOffset

### Description
When positioning the hover canvas, this will be the minimum offset from page edge. The hover is always positioned not to show outside the page but this offset keeps the canvas from possibly being positioned adjoining the page edge.

**Flags**: RW

---
## ClassMethod: Hover.hide

### Description
Hide hoverCanvas shown via [Hover.show](#classmethod-hovershow)

---
## ClassMethod: Hover.show

### Description
Displays a standard Hover canvas containing the specified HTML content.  
This method may also be called to modify the content of the hover if it is already showing. Call [Hover.hide](#classmethod-hoverhide) to hide the canvas again.  
A common use case for calling this method is to asynchronously fetch detail data from the server about some component, and display it in the Hover canvas when the data is returned. Note that in this case you will typically need to verify that the user is still hovering over the component in question before calling Hover.show() - if the user has moved the mouse off the component, the information will not apply to whatever is now under the mouse. Suggested approaches for handling this are to either use a [Canvas.mouseOut](Canvas.md#method-canvasmouseout) handler to track when the user moves off the component, or checking [EventHandler.getTarget](EventHandler.md#classmethod-eventhandlergettarget) as part of the asynchronous callback

The default Hover canvas position will be based on the mouse pointer position, adjusted by [Hover.leftOffset](#classattr-hoverleftoffset) and [Hover.topOffset](#classattr-hovertopoffset). If this position would render the Hover canvas partially clipped, it will be automatically modified to ensure the Hover is entirely visible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| contents | [HTMLString](../main.md#type-htmlstring)|[Canvas](#type-canvas) | false | — | contents for the hover |
| properties | [Label Properties](#type-label-properties) | false | — | object containing attributes for managing the hover canvas' appearance. Valid properties include:

*   left, top, width, height
*   baseStyle
*   opacity
*   wrap
*   moveWithMouse \[overrides [Hover.moveWithMouse](#classattr-hovermovewithmouse)\]
*   autoFitWidth: If true, any specified width will be treated as a minimum and the hover canvas will expand horizontally to fit the content string (without wrapping) up to the specified autoFitMaxWidth. This setting differs from simply setting [wrap:false](Label.md#attr-labelwrap) for the hover in that wrapping of text will occur if the autoFitMaxWidth is exceeded.
*   autoFitMaxWidth: Maximum width to expand to without wrapping (if autoFitWidth is true). |

---
## ClassMethod: Hover.showHoverComponent

### Description
Similar to [Hover.show()](#classmethod-hovershow) but uses the hover mechanism to display some [component](Canvas.md#class-canvas) instead of showing [HTML text](Canvas.md#method-canvasgethoverhtml) in the builtin [hoverCanvas](#classattr-hoverhovercanvas). _Hover.showHoverComponent()_ is called automatically instead of _Hover.show()_ when [Canvas.showHoverComponents](Canvas.md#attr-canvasshowhovercomponents) is true.

As with `Hover.show()`, the component-position is based on the mouse pointer position, adjusted by [Hover.leftOffset](#classattr-hoverleftoffset) and [Hover.topOffset](#classattr-hovertopoffset). If this position would render the component partially clipped or off-screen, it is moved to ensure the component is entirely visible.

See [show()](#classmethod-hovershow) for more information.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| component | [Canvas](#type-canvas) | false | — | component to show using the hover mechanism |

---
