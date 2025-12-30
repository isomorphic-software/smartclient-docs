# Hover Documentation

[← Back to API Index](../reference.md)

---

## Class: Hover

### Description
The Hover class handles showing a simple SmartClient canvas containing arbitrary HTML, or triggering some other action in response to a user holding the mouse-pointer (or hovering) over a specific widget.

---
## ClassAttr: Hover.moveWithMouse

### Description
When the Hover canvas is shown by default, should it move as the user moves the mouse pointer?  
May be overridden by including a `moveWithMouse` attribute on the properties block passed to [Hover.show](#classmethod-hovershow)

**Flags**: RWA

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
## ClassAttr: Hover.leftOffset

### Description
When positioning the hover canvas, this will be the default left offset from the mousepointer, if no explicit position was passed to the [Hover.show](#classmethod-hovershow) method

**Flags**: RW

---
## ClassAttr: Hover.edgeOffset

### Description
When positioning the hover canvas, this will be the minimum offset from page edge. The hover is always positioned not to show outside the page but this offset keeps the canvas from possibly being positioned adjoining the page edge.

**Flags**: RW

---
## ClassMethod: Hover.hide

### Description
Hide hover hover Canvas shown via [Hover.show](#classmethod-hovershow)

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
| contents | [HTMLString](../reference.md#type-htmlstring)|[Canvas](#type-canvas) | false | — | contents for the hover |
| properties | [Label Properties](#type-label-properties) | false | — | object containing attributes for managing the hover canvas' appearance. Valid properties include:

*   left, top, width, height
*   baseStyle
*   opacity
*   wrap
*   moveWithMouse \[overrides [Hover.moveWithMouse](#classattr-hovermovewithmouse)\]
*   autoFitWidth: If true, any specified width will be treated as a minimum and the hover canvas will expand horizontally to fit the content string (without wrapping) up to the specified autoFitMaxWidth. This setting differs from simply setting [wrap:false](Label.md#attr-labelwrap) for the hover in that wrapping of text will occur if the autoFitMaxWidth is exceeded.
*   autoFitMaxWidth: Maximum width to expand to without wrapping (if autoFitWidth is true). |

---
