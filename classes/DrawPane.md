# DrawPane Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawPane

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
A DrawPane is a container for drawing bitmap and vector graphics using browser's built-in freeform drawing capabilities. These include the HTML5 ``<canvas>`` tag and `SVG (Scalable Vector Graphics)` where available, and the `VML (Vector Markup Language)` for legacy browsers (Internet Explorer 8 and earlier).

To draw in a `DrawPane` you create [DrawLine](DrawLine.md#class-drawline)s, [DrawOval](DrawOval.md#class-drawoval)s, [DrawPath](DrawPath.md#class-drawpath)s and other [DrawItem](DrawItem.md#class-drawitem)-based components, and place them in the `DrawPane` via [DrawPane.drawItems](#attr-drawpanedrawitems) or add them incrementally via [DrawPane.addDrawItem](#method-drawpaneadddrawitem).

`DrawItems` support a variety of common features, such as [gradient fills](../reference.md#object-gradient), [arrowheads](DrawItem.md#attr-drawitemstartarrow), events such as [click()](DrawItem.md#method-drawitemclick) and built-in [control knobs](DrawItem.md#attr-drawitemknobs) for end user resizing and manipulation of shapes.

Common shapes such as [rectangles](DrawRect.md#class-drawrect), [ovals](DrawOval.md#class-drawoval) and [triangles](../reference.md#class-drawtriangle) have dedicated DrawItem subclasses. For other shapes, consider:

*   [DrawPath](DrawPath.md#class-drawpath) - a multi-segment line with straight segments, defined by a series of [points](DrawPath.md#attr-drawpathpoints)
*   [DrawPolygon](DrawPolygon.md#class-drawpolygon) - a closed shape with straight sides, defined by a series of [points](DrawPolygon.md#attr-drawpolygonpoints)
*   [DrawShape](DrawShape.md#class-drawshape) - a multi-segment line or closed shape whose sides can be defined by a series of commands, including curved arcs

#### Note on Coordinate Systems
There are three different coordinate systems involved when a DrawItem is drawn onto a DrawPane:

*   The "local coordinate system" for a DrawItem refers to the Cartesian coordinate system in which dimensional and positional values are interpreted. For example, when a [DrawRect](DrawRect.md#class-drawrect) is configured with left:20, top:30, width:200, and height:100, the DrawRect represents a rectangle from (20, 30) to (220, 130) in its local coordinate system. For this same DrawRect, [top](DrawRect.md#attr-drawrecttop) is going to be 30 even if the shape is scaled by 3x, such that the (transformed) top coordinate in the drawing coordinate system actually lies outside the visible region of the DrawPane. Similarly, no matter what rotation is applied, [top](DrawRect.md#attr-drawrecttop) will continue to be 30.
    
    Use [DrawItem.getBoundingBox](DrawItem.md#method-drawitemgetboundingbox) to obtain the bounding box of the item in local coordinates. Subclass properties also typically provide data in the local coordinate system, such as [DrawRect.left](DrawRect.md#attr-drawrectleft), [DrawRect.top](DrawRect.md#attr-drawrecttop), [DrawRect.width](DrawRect.md#attr-drawrectwidth), [DrawRect.height](DrawRect.md#attr-drawrectheight), [DrawPath.points](DrawPath.md#attr-drawpathpoints), and [DrawTriangle.points](../reference.md#attr-drawtrianglepoints).
    
    There is a local coordinate system for each DrawItem.
    
*   The "drawing coordinate system" refers to the Cartesian coordinate system shared by all DrawItems after their local transforms, such as [DrawItem.scale](DrawItem.md#attr-drawitemscale) or [DrawItem.rotation](DrawItem.md#attr-drawitemrotation), have been applied.
    
    Since [DrawGroup](DrawGroup.md#class-drawgroup)s pass through applied transforms to the underlying items, [DrawGroup](DrawGroup.md#class-drawgroup) properties such as [DrawGroup.left](DrawGroup.md#attr-drawgroupleft), [DrawGroup.top](DrawGroup.md#attr-drawgrouptop), [DrawGroup.width](DrawGroup.md#attr-drawgroupwidth), and [DrawGroup.height](DrawGroup.md#attr-drawgroupheight), represent coordinates in the drawing coordinate system, as does therefore [DrawGroup.getBoundingBox](DrawGroup.md#method-drawgroupgetboundingbox). The APIs [DrawPane.getDrawingPoint](#method-drawpanegetdrawingpoint), [DrawPane.getDrawingX](#method-drawpanegetdrawingx), and [DrawPane.getDrawingY](#method-drawpanegetdrawingy), also return drawing coordinates.
    
    For DrawItems with no local transforms, the drawing coordinate system is identical to the local coordinate system.
    
*   The "global coordinate system" refers to the drawing coordinate system with global DrawPane transforms [DrawPane.translate](#attr-drawpanetranslate), [DrawPane.zoomLevel](#attr-drawpanezoomlevel) and [DrawPane.rotation](#attr-drawpanerotation) applied.
    
    Use [DrawItem.getResizeBoundingBox](DrawItem.md#method-drawitemgetresizeboundingbox) to obtain the bounding box of a [DrawItem](DrawItem.md#class-drawitem) in global coordinates. The APIs [DrawItem.getPageLeft](DrawItem.md#method-drawitemgetpageleft) and [DrawItem.getPageTop](DrawItem.md#method-drawitemgetpagetop) reflect global coordinates rounded to the nearest pixel and offset by the page-relative coordinates of the [DrawPane](#class-drawpane)'s top left corner. (See for example [Canvas.getPageLeft](Canvas.md#method-canvasgetpageleft) and [Canvas.getPageTop](Canvas.md#method-canvasgetpagetop).)
    
    With the default global transforms, the global coordinate system is identical to the drawing coordinate system.
    

The view port of the DrawPane is the rectangle in the global coordinate system from (0, 0) that is as wide as the DrawPane's [inner content width](Canvas.md#method-canvasgetinnercontentwidth) and as high as the DrawPane's [inner content height](Canvas.md#method-canvasgetinnercontentheight). Note: In the case of a [FacetChart](FacetChart.md#class-facetchart) showing a [zoom chart](FacetChart.md#attr-facetchartcanzoom), the view port height is decreased by the height of the zoom chart.

One other coordinate system in use by a DrawPane when [drag-scrolling](#attr-drawpanecandragscroll) is enabled is the "viewbox coordinate system". The viewbox coordinate system is the drawing coordinate system with the [DrawPane.translate](#attr-drawpanetranslate) and [DrawPane.zoomLevel](#attr-drawpanezoomlevel) transforms applied.

---
## Attr: DrawPane.drawingType

### Description
Which type of drawing back-end should be used by this `DrawPane`? A default drawing back-end is automatically selected based on the browser.

The `drawingType` can only be set to a drawing back-end type that is supported by the browser. It is provided for cases where the browser supports more than one drawing back-end. See the [DrawingType](../reference.md#type-drawingtype) documentation for the supported drawing back-ends and the list of browsers that support each type of drawing back-end.

**Flags**: IRA

---
## Attr: DrawPane.gradients

### Description
Array of gradients that can be referenced by DrawItems placed on this DrawPane. Each gradient must have an ID assigned to be used for reference.

**Flags**: IR

---
## Attr: DrawPane.canDragScroll

### Description
Can the user drag-scroll the DrawPane?

### See Also

- [DrawPane.drawingWidth](#attr-drawpanedrawingwidth)
- [DrawPane.drawingHeight](#attr-drawpanedrawingheight)

**Flags**: IR

---
## Attr: DrawPane.drawItems

### Description
Array of DrawItems to initially display in this DrawPane.

**Flags**: IR

---
## Attr: DrawPane.drawingHeight

### Description
When [canDragScroll](#attr-drawpanecandragscroll) is enabled, this is the height of the area in viewbox coordinates that can be accessed through drag-scrolling.

**Flags**: IR

---
## Attr: DrawPane.rotation

### Description
Rotation in degrees for the `DrawPane` as a whole about the center of the `DrawPane`. The positive direction corresponds to clockwise rotation (for example, 45 is rotation clockwise by 45 degrees and -10 is rotation counterclockwise by 10 degrees).

**Flags**: IRW

---
## Attr: DrawPane.zoomLevel

### Description
Zoom for the `DrawPane` as a whole, where 1 is normal size.

**Flags**: IRW

---
## Attr: DrawPane.translate

### Description
Global translation. This array has two numbers. The first number is the X translation amount in pixels and the second number is the Y translation amount in pixels.

**Flags**: IR

---
## Attr: DrawPane.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: DrawPane.drawingWidth

### Description
When [canDragScroll](#attr-drawpanecandragscroll) is enabled, this is the width of the area in viewbox coordinates that can be accessed through drag-scrolling.

**Flags**: IR

---
## ClassMethod: DrawPane.getPolygonPoints

### Description
Computes an array of Points for a polygon that has an equal distance from its center to any of its vertices and that fits in the given width and height.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [int](../reference.md#type-int) | false | — | width of target space |
| height | [int](../reference.md#type-int) | false | — | height of target space |
| xc | [int](../reference.md#type-int) | false | — | center point x |
| yc | [int](../reference.md#type-int) | false | — | center point y |
| angles | [Array of double](#type-array-of-double) | false | — | the complete list of angles (in radians) with respect to the center point at which the polygon must have vertices |

### Returns

`[Array of Point](#type-array-of-point)` — list of the vertices of the polygon

---
## ClassMethod: DrawPane.scaleAndCenterBezier

### Description
Computes the top-, left-, bottom-, and right-most coordinates containing the Bézier curve defined by `startPoint`, `controlPoint1`, `controlPoint2`, and `endPoint`, then translates and scales these four points to fit the entire curve into the given width and height.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [int](../reference.md#type-int) | false | — | width of target space |
| height | [int](../reference.md#type-int) | false | — | height of target space |
| xc | [int](../reference.md#type-int) | false | — | center point x |
| yc | [int](../reference.md#type-int) | false | — | center point y |
| startPoint | [Point](#type-point) | false | — | start point of the curve |
| endPoint | [Point](#type-point) | false | — | end point of the curve |
| controlPoint1 | [Point](#type-point) | false | — | first cubic Bézier control point |
| controlPoint2 | [Point](#type-point) | false | — | second cubic Bézier control point |

---
## ClassMethod: DrawPane.bezierExtrema

### Description
Computes the minimum and maximum value of the cubic Bézier curve polynomial defined in [DrawPane.bezier](#classmethod-drawpanebezier), for `0 ≤ t ≤ 1`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| p1 | [double](../reference.md#type-double) | false | — | starting point coordinate |
| cp1 | [double](../reference.md#type-double) | false | — | first control point coordinate |
| cp2 | [double](../reference.md#type-double) | false | — | second control point coordinate |
| p2 | [double](../reference.md#type-double) | false | — | end point coordinate |

### Returns

`[Array of double](#type-array-of-double)` — the minimum and maximum value of the cubic Bézier curve polynomial

---
## ClassMethod: DrawPane.bezier

### Description
Computes a cubic Bézier curve polynomial: `B(t) = (1 - t)3P1 + 3(1 - t)2tCP1 + 3(1 - t)t2CP2 + t3P2`

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| p1 | [double](../reference.md#type-double) | false | — | starting point coordinate |
| cp1 | [double](../reference.md#type-double) | false | — | first control point coordinate |
| cp2 | [double](../reference.md#type-double) | false | — | second control point coordinate |
| p2 | [double](../reference.md#type-double) | false | — | end point coordinate |
| t | [double](../reference.md#type-double) | false | — | the value of the parameter of the curve, between 0 and 1 |

### Returns

`[double](../reference.md#type-double)` — the value of the polynomial `B(t)` at `t`

---
## ClassMethod: DrawPane.getBezierBoundingBox

### Description
Calculate the bounding box of the cubic Bézier curve with endpoints `p1` and `p2` and control points `cp1` and `cp2`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| p1 | [Point](#type-point) | false | — | start point of the curve |
| cp1 | [Point](#type-point) | false | — | first cubic Bézier control point |
| cp2 | [Point](#type-point) | false | — | second cubic Bézier control point |
| p2 | [Point](#type-point) | false | — | end point of the curve |

### Returns

`[Array of double](#type-array-of-double)` — the x1, y1, x2, y2 coordinates. The point `(x1, y1)` is the top-left point of the bounding box and the point `(x2, y2)` is the bottom-right point of the bounding box.

---
## ClassMethod: DrawPane.getRegularPolygonPoints

### Description
Calls [DrawPane.getPolygonPoints](#classmethod-drawpanegetpolygonpoints) with angles spread evenly over the full 360 degrees.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| n | [int](../reference.md#type-int) | false | — | the number of vertices the polygon |
| width | [int](../reference.md#type-int) | false | — | width of target space |
| height | [int](../reference.md#type-int) | false | — | height of target space |
| xc | [int](../reference.md#type-int) | false | — | center point x |
| yc | [int](../reference.md#type-int) | false | — | center point y |
| startAngle | [double](../reference.md#type-double) | false | — | the angle (in radians) with respect to the center point of the first vertex of the polygon |

### Returns

`[Array of Point](#type-array-of-point)` — list of the vertices of the regular polygon

---
## ClassMethod: DrawPane.scaleAndCenter

### Description
Computes the top-, left-, bottom-, and right-most coordinates in a list of points, then translates and scales all points to fit the entire shape into the given width and height.

The example call below scales a set of points into a 100x100 thumbnail:

```
    var scaledPoints = DrawPane.scaleAndCenter(100, 100, 50, 50,
            [[500, 50], [525, 50], [550, 75], [575, 75],
             [600, 75], [600, 125], [575, 125], [550, 125],
             [525, 150], [500, 150]]);
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [int](../reference.md#type-int) | false | — | width of target space |
| height | [int](../reference.md#type-int) | false | — | height of target space |
| xc | [int](../reference.md#type-int) | false | — | center point x |
| yc | [int](../reference.md#type-int) | false | — | center point y |
| points | [Array of Point](#type-array-of-point) | false | — | list of points to scale and translate |

---
## Method: DrawPane.zoom

### Description
Synonym of [DrawPane.setZoomLevel](#method-drawpanesetzoomlevel).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zoomLevel | [float](../reference.md#type-float) | false | — | Desired zoom level as a float where `1.0` is equivalent to 100% magnification. Must be greater than 0. |

---
## Method: DrawPane.getDrawingX

### Description
Returns the X coordinate in the [drawing coordinate system](#class-drawpane) of the last event. Note: If you need both the X and Y coordinates in the drawing coordinate system of the last event, it is more efficient to call [getDrawingPoint()](#method-drawpanegetdrawingpoint) instead.

See the documentation of [getDrawingPoint()](#method-drawpanegetdrawingpoint) for a clarifying example.

### Returns

`[int](../reference.md#type-int)` — X coordinate in the drawing coordinate system of the last event.

**Flags**: A

---
## Method: DrawPane.setRotation

### Description
Sets the [rotation](#attr-drawpanerotation) of the `DrawPane`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| degrees | [float](../reference.md#type-float) | false | — | the new rotation in degrees. The positive direction corresponds to clockwise rotation. |

---
## Method: DrawPane.destroyItems

### Description
Permanently [destroy](DrawItem.md#method-drawitemdestroy) all DrawItems currently associated with this DrawPane, leaving the DrawPane itself intact

---
## Method: DrawPane.getDataURL

### Description
Get a "data:" URL encoding the current contents of the `DrawPane`.

The returned "data:" URLs can be used anywhere a URL to an image is valid, for example, [Img.src](Img.md#attr-imgsrc).

This method will directly return the data URL on modern browsers when using `<canvas>`-style rendering (the default), and if there are no [DrawImage](DrawImage.md#class-drawimage)s in this `DrawPane` that load cross-domain images.

On legacy browers (any version of IE in "quirks" mode, all versions of IE prior to 9.0), or if there is a `DrawImage` that loads a cross-domain image, data URL generation requires a server trip and requires the SmartClient Server to be installed with the same set of [required .jars](../kb_topics/javaModuleDependencies.md#kb-topic-java-module-dependencies) as are required for PDF export of charts in legacy IE. The method will return null and a callback must be passed, which fires when the data URL has been retrieved from the server.

If the callback is passed but no server trip is required, the callback is fired immediately.

For obtaining PNG or other image data for use in server-side processing (such as attaching to automated emails or saving to a database), see also the server-side APIs in com.isomorphic.contentexport.ImageExport.

Note: It is recommended to pass a callback instead of relying on the method returning the data URL directly. This is because the callback will always be called with the generated data URL, whereas work-arounds for browser bugs may require asynchronous generation of the data URL, meaning that a data URL might not be returned immediately in certain browsers for certain `DrawPane` contents.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| callback | [DataURLCallback](#type-dataurlcallback) | true | — | callback to fire when the data URL is available. The callback is called regardless of whether the data URL is also returned. |
| format | [DataURLFormat](../reference.md#type-dataurlformat) | true | — | the format of the data URL. If not specified, then "all" is assumed. |

### Returns

`[String](#type-string)` — the data URL if synchronously generated.

---
## Method: DrawPane.refreshNow

### Description
Immediately draws or redraws any items of this `DrawPane` that are scheduled to be drawn or redrawn after a delay.

For performance reasons, this `DrawPane` may delay refreshing its display to allow for multiple draw item updates to be drawn at the same time. If this is occurring, refreshNow() will immediately refresh the display instead of refreshing the display in a timer.

**Flags**: A

---
## Method: DrawPane.drawEnd

### Description
Called after we finish drawing to the underlying HTML5 `<canvas>` element of a DrawPane, after the last [DrawItem](DrawItem.md#class-drawitem) has been drawn. Only called if the [DrawingType](../reference.md#type-drawingtype) is "bitmap".

There is no default implementation of this method.

**Flags**: A

---
## Method: DrawPane.rotate

### Description
Synonym of [DrawPane.setRotation](#method-drawpanesetrotation).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| degrees | [float](../reference.md#type-float) | false | — | the new rotation in degrees. The positive direction corresponds to clockwise rotation. |

---
## Method: DrawPane.erase

### Description
Call [DrawItem.erase](DrawItem.md#method-drawitemerase) on all DrawItems currently associated with the DrawPane.

The DrawItems will continue to exist, and you can call draw() on them to make them appear again, or [destroy](DrawItem.md#method-drawitemdestroy) to get rid of them permanetly. Use [DrawPane.destroyItems](#method-drawpanedestroyitems) to permanently get rid of all DrawItems.

---
## Method: DrawPane.getDrawingPoint

### Description
Returns the point of the last event in the [drawing coordinate system](#class-drawpane).

To give a concrete example, suppose that this `DrawPane` has [zoomLevel](#attr-drawpanezoomlevel) 2 and drag-panning is not enabled (just to simplify this example). If [getOffsetX()](Canvas.md#method-canvasgetoffsetx) and [getOffsetY()](Canvas.md#method-canvasgetoffsety) is (0, 0) (i.e. the mouse pointer is located at the top left point of this `DrawPane`), then getDrawingPoint() would return (0, 0). If getOffsetX/Y() is (20, 40), then getDrawingPoint() would return (10, 20) because when the 2× zoom level is applied, (10, 20) is translated to (20, 40) on the screen. You could, for example, create a new [DrawLine](DrawLine.md#class-drawline) with [startPoint](DrawLine.md#attr-drawlinestartpoint) (10, 20) and when this line is drawn on screen, the position of the line's start point would be at offset (20, 40) on screen.

### Returns

`[Point](#type-point)` — the point in drawing coordinates of the last event.

**Flags**: A

---
## Method: DrawPane.addDrawItem

### Description
Adds a draw item to this `DrawPane`. If already added to a `DrawPane`, the draw item is removed from its current `DrawPane` and added to this `DrawPane`.

NOTE: For performance reasons, this `DrawPane` may draw the new item on a delay to allow multiple items to be added and drawn at one time. The [DrawPane.refreshNow](#method-drawpanerefreshnow) API will force the item to be drawn immediately.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [DrawItem](#type-drawitem) | false | — | item to add. |
| autoDraw | [boolean](../reference.md#type-boolean) | false | — | If explicitly set to false, and this drawPane is drawn, don't draw the newly added item |

---
## Method: DrawPane.getPrintHTML

### Description
Retrieves printable HTML for this component and all printable subcomponents.

By default any Canvas with children will simply collect the printable HTML of its children by calling getPrintHTML() on each child that is considered [printable](Canvas.md#attr-canvasshouldprint).

If overriding this method for a custom component, you should **either** return a String of printable HTML string directly **or** return null, and fire the callback (if provided) using [Class.fireCallback](Class.md#method-classfirecallback).

To return an empty print representation, return an empty string ("") rather than null.

The `printProperties` argument, if passed, must be passed to any subcomponents on which `getPrintHTML()` is called.

**Notes on printing**

To print a `DrawPane` for export on IE8 and earlier, it is important to pass [PrintProperties](../reference.md#object-printproperties) with [printForExport](PrintProperties.md#attr-printpropertiesprintforexport):true:

```
var exportHTML = drawPane.getPrintHTML({ printForExport:true });
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| printProperties | [PrintProperties](#type-printproperties) | true | — | properties to configure printing behavior - may be null. |
| callback | [Callback](../reference.md#type-callback) | true | — | optional callback. This is required to handle cases where HTML generation is asynchronous - if a method generates HTML asynchronously, it should return null, and fire the specified callback on completion of HTML generation. The first parameter `HTML` should contain the generated print HTML. The callback is only called if null is returned. Furthermore, the default getPrintHTML() implementation always returns null and fires the callback when a callback is provided. |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — null if the print HTML is being generated asynchronously and/or a callback is provided; otherwise, the direct print HTML for this component (but note that returning direct print HTML is a deprecated feature).

### Groups

- printing

**Flags**: A

---
## Method: DrawPane.addGradient

### Description
Add a new gradient to the drawPane shared gradient list ([DrawPane.gradients](#attr-drawpanegradients)). If the gradient does not have an ID a new one will be assigned.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| gradient | [Gradient](#type-gradient) | false | — | gradient to add |

### Returns

`[Identifier](../reference.md#type-identifier)` — the ID of the gradient (either provided or auto-assigned)

---
## Method: DrawPane.getGradient

### Description
Returns gradient for gradientID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| gradientID | [Identifier](../reference.md#type-identifier) | false | — | ID of gradient to retrieve |

### Returns

`[Gradient](#type-gradient)` — the gradient or null if not found

---
## Method: DrawPane.drawStart

### Description
Called when we start drawing to the underlying HTML5 `<canvas>` element of a DrawPane, right after the element is cleared. Only called if the [DrawingType](../reference.md#type-drawingtype) is "bitmap".

There is no default implementation of this method.

**Flags**: A

---
## Method: DrawPane.getDrawingY

### Description
Returns the Y coordinate in the [drawing coordinate system](#class-drawpane) of the last event. Note: If you need both the X and Y coordinates in the drawing coordinate system of the last event, it is more efficient to call [getDrawingPoint()](#method-drawpanegetdrawingpoint) instead.

See the documentation of [getDrawingPoint()](#method-drawpanegetdrawingpoint) for a clarifying example.

### Returns

`[int](../reference.md#type-int)` — Y coordinate in the drawing coordinate system of the last event.

**Flags**: A

---
## Method: DrawPane.createRadialGradient

### Description
Creates a radial gradient which can be used by any DrawItem of this DrawPane. Any DrawItem's [fillGradient](DrawItem.md#attr-drawitemfillgradient) can reference the gradient by the given ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [Identifier](../reference.md#type-identifier) | false | — | the ID of the radial gradient |
| radialGradient | [RadialGradient](#type-radialgradient) | false | — | the radial gradient |

### Returns

`[Identifier](../reference.md#type-identifier)` — id

**Deprecated**

---
## Method: DrawPane.getSvgString

### Description
Converts this DrawPane to the source of an ``<svg>`` element equivalent to the current drawing.

In Pro edition and above, the returned string can be used with [RPCManager.exportImage](RPCManager.md#classmethod-rpcmanagerexportimage) to download an image, or with server-side APIs in com.isomorphic.contentexport.ImageExport to obtain various kinds of images for further server-side processing.

### Returns

`[String](#type-string)` — the source of an ``<svg>`` element.

---
## Method: DrawPane.setZoomLevel

### Description
Sets the zoom on this `DrawPane` to the specified magnification, maintaining the current viewport position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| zoomLevel | [float](../reference.md#type-float) | false | — | Desired zoom level as a float where `1.0` is equivalent to 100% magnification. Must be greater than 0. |

---
## Method: DrawPane.createLinearGradient

### Description
Creates a linear gradient which can be used by any DrawItem of this DrawPane. Any DrawItem's [fillGradient](DrawItem.md#attr-drawitemfillgradient) can reference the gradient by the given ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [Identifier](../reference.md#type-identifier) | false | — | the ID of the linear gradient |
| linearGradient | [LinearGradient](#type-lineargradient) | false | — | the linear gradient |

### Returns

`[Identifier](../reference.md#type-identifier)` — id

**Deprecated**

---
## Method: DrawPane.getBitmap

### Description
Returns the DrawPane's underlying HTML5 `<canvas>` element. Will only return a valid element if the [DrawingType](../reference.md#type-drawingtype) is "bitmap".

To create a DrawItem drawn by custom HTML5 `<canvas>` drawing code, you should:

*   Subclass the [DrawRect](DrawRect.md#class-drawrect) class, setting [DrawItem.lineOpacity](DrawItem.md#attr-drawitemlineopacity) to 0, and [DrawItem.eventOpaque](DrawItem.md#attr-drawitemeventopaque) to true.
*   Define your HTML5 `<canvas>` drawing routine as [DrawItem.drawStart](DrawItem.md#method-drawitemdrawstart) or [DrawItem.drawEnd](DrawItem.md#method-drawitemdrawend).
*   Limit your drawing to the DrawItem's [bounding box](DrawItem.md#method-drawitemgetresizeboundingbox).

### Returns

`[DOMElement](#type-domelement)` — HTML5 `<canvas>` element underlying this [DrawPane](#class-drawpane)

### See Also

- [DrawPane.drawStart](#method-drawpanedrawstart)
- [DrawPane.drawEnd](#method-drawpanedrawend)

**Flags**: A

---
## Method: DrawPane.createSimpleGradient

### Description
Creates a simple linear gradient which can be used by any DrawItem of this DrawPane. Any DrawItem's [fillGradient](DrawItem.md#attr-drawitemfillgradient) can reference the gradient by the given ID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| id | [Identifier](../reference.md#type-identifier) | false | — | the ID of the simple linear gradient |
| simple | [SimpleGradient](#type-simplegradient) | false | — | the simple linear gradient |

### Returns

`[Identifier](../reference.md#type-identifier)` — id

**Deprecated**

---
## Method: DrawPane.removeGradient

### Description
Removes gradient for gradientID.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| gradientID | [Identifier](../reference.md#type-identifier) | false | — | ID of gradient to remove |

---
