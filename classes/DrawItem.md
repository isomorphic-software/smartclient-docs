# DrawItem Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawItem

*Inherits from:* [BaseWidget](../reference.md#class-basewidget)

### Description
Base class for graphical elements drawn in a DrawPane. All properties and methods documented here are available on all DrawItems unless otherwise specified.

Each DrawItem has its own local transform that maps its [local coordinate system](#class-drawitem) to the drawing coordinate system that is shared by all DrawItems in the same DrawPane (explained [here](DrawPane.md#class-drawpane)). The local transform is a combination of rotation, scaling, and other affine transformations. The DrawItem is first [translated](#attr-drawitemtranslate), then [scaled](#attr-drawitemscale), then [sheared](#attr-drawitemxshearfactor) in the direction of the x-axis, then [sheared](#attr-drawitemyshearfactor) in the directiton of the y-axis, and then finally [rotated](#attr-drawitemrotation).

Note that DrawItems as such should never be created, only concrete subclasses such as [DrawGroup](DrawGroup.md#class-drawgroup) and [DrawLine](DrawLine.md#class-drawline).

See [DrawPane](DrawPane.md#class-drawpane) for the different approaches to create DrawItems.

---
## Attr: DrawItem.resizeViaLocalTransformOnly

### Description
If this DrawItem is showing "resize" [control knobs](#attr-drawitemknobs), should resizing the shape solely update the local transform (for example, the DrawItem's [scale](#attr-drawitemscale) or [translation](#attr-drawitemtranslate))?.

The default is `false`, which means that the DrawItem is allowed to modify its shape properties in order to fit within a given width and height. Some examples:

*   A [DrawOval](DrawOval.md#class-drawoval) might decrease its [radius](DrawOval.md#attr-drawovalradius) when resized to a smaller size.
*   A [DrawPath](DrawPath.md#class-drawpath) might change its [points](DrawPath.md#attr-drawpathpoints) to lengthen all line segments in the path by some proportion so that it fits into a larger size.

This approach allows a DrawItem to maintain the same [line width](#attr-drawitemlinewidth) even as it is being resized.

If this property is set to `true` then all visual aspects of the DrawItem, including the line width and the fill, will be magnified or reduced during resizes as if the DrawItem were placed under a lens.

**Flags**: IR

---
## Attr: DrawItem.titleAutoFitRotationMode

### Description
Whether to rotate the [DrawItem.titleLabel](#attr-drawitemtitlelabel) 90 degrees clockwise while trying to maximize its size in accordance with [DrawItem.titleAutoFit](#attr-drawitemtitleautofit). If automatic rotation is specified, the default, the label will be rotated if and only if it allows the label to become larger.

### See Also

- [DrawItem.titleLabel](#attr-drawitemtitlelabel)
- [DrawItem.titleAutoFit](#attr-drawitemtitleautofit)

**Flags**: IR

---
## Attr: DrawItem.knobs

### Description
Array of control knobs to display for this item. Each [KnobType](../reference.md#type-knobtype) specified in this array will turn on UI element(s) allowing the user to manipulate this drawItem. To update the set of knobs at runtime use [DrawItem.showKnobs](#method-drawitemshowknobs) and [DrawItem.hideKnobs](#method-drawitemhideknobs).

**NOTE:** Unless otherwise documented, DrawItem types only support "resize" and "move" knobs.

**Flags**: IR

---
## Attr: DrawItem.proportionalResizeModifiers

### Description
If [DrawItem.proportionalResizing](#attr-drawitemproportionalresizing) is set to "modifier" or "modifierOff" then proportional resizing of the DrawItem is activated or deactivated, respectively, whenever at least one key in this set of modifier keys is pressed.

The keys allowed in this set are: "Alt", "Ctrl", and "Shift". If this set of keys is empty then proportional resizing is always used if `proportionalResizing` is "modifier" and is never used if `proportionalResizing` is "modifierOff" .

**Flags**: IR

---
## Attr: DrawItem.zIndex

### Description
Relative stacking order of this draw item with respect to other items in the same [DrawPane](DrawPane.md#class-drawpane) or [DrawGroup](DrawGroup.md#class-drawgroup).

null means that the zIndex has not been resolved. Upon adding this draw item to a `DrawPane` or `DrawGroup`, this item's zIndex will be resolved to the next higher auto-assigned zIndex. Note that this may still be less than another item's zIndex if [bringToFront()](#method-drawitembringtofront) was called on that item.

If two items within the same `DrawPane` or `DrawGroup` have the same zIndex, then they are stacked in the order in which they were added to the `DrawPane` or `DrawGroup`.

When the `DrawPane`'s [drawingType](DrawPane.md#attr-drawpanedrawingtype) is "bitmap", zIndex, [DrawItem.bringToFront](#method-drawitembringtofront), and [DrawItem.sendToBack](#method-drawitemsendtoback) are not supported for [DrawLabel](DrawLabel.md#class-drawlabel)s on iOS due to platform limitations.

### Groups

- zIndex

**Flags**: IR

---
## Attr: DrawItem.moveKnobOffset

### Description
If this item is showing a `"move"` [control knob](#attr-drawitemknobs), this attribute allows you to specify an offset in pixels from the [DrawItem.moveKnobPoint](#attr-drawitemmoveknobpoint) for the move knob. Offset should be specified as a 2-element array of \[left offset, top offset\].

This offset overrides the built-in offset used when showing both resize and move knobs.

### See Also

- [DrawItem.moveKnobPoint](#attr-drawitemmoveknobpoint)

**Flags**: IRWA

---
## Attr: DrawItem.fillOpacity

### Description
Opacity of the fillColor, as a number between 0 (transparent) and 1 (opaque).

### Groups

- fill

**Flags**: IRW

---
## Attr: DrawItem.keepInParentRect

### Description
Constrains drag-resizing and drag-repositioning of this draw item to either the current visible area of the [draw pane](DrawPane.md#class-drawpane) or an arbitrary bounding box (if set to an array of the form `[left, top, left + width, top + height]`). When using a bounding box-type argument the left/top values can be negative, or the width/height values can be greater than the dimensions of the viewable area, to allow positioning or resizing the draw item beyond the confines of the draw pane.

Note: keepInParentRect affects only user drag interactions, not programmatic moves or resizes.

**Flags**: IRWA

---
## Attr: DrawItem.showHover

### Description
If [canHover](#attr-drawitemcanhover) is true, should we show the global hover canvas by default when the user hovers over this DrawItem?

### Groups

- hovers

### See Also

- [DrawItem.getHoverHTML](#method-drawitemgethoverhtml)

**Flags**: IRW

---
## Attr: DrawItem.resizeKnobPoints

### Description
If this item is showing "resize" [control knobs](#attr-drawitemknobs), this attribute specifies the points with respect to the draw item where resize knobs should appear.

**Flags**: IR

---
## Attr: DrawItem.lineColor

### Description
Line color

### Groups

- line

**Flags**: IRW

---
## Attr: DrawItem.drawPane

### Description
[DrawPane](DrawPane.md#class-drawpane) this drawItem should draw in.

If this item has a [DrawGroup](DrawGroup.md#class-drawgroup), the drawGroup's drawPane is automatically used.

**Flags**: IRW

---
## Attr: DrawItem.destroying

### Description
Flag indicating a drawItem is mid-destruction, similar to [Canvas.destroying](Canvas.md#attr-canvasdestroying).

**Flags**: RA

---
## Attr: DrawItem.moveKnobPoint

### Description
If this item is showing a "move" [control knob](#attr-drawitemknobs), this attribute specifies where the knob should appear with respect to the draw item.

The resize and move knobs show at the same position by default. However, when both knobs are shown the move knob is offset slightly to allow access to both. This position can be adjusted manually with [DrawItem.moveKnobOffset](#attr-drawitemmoveknoboffset).

### See Also

- [DrawItem.moveKnobOffset](#attr-drawitemmoveknoboffset)

**Flags**: IR

---
## Attr: DrawItem.destroyed

### Description
Flag indicating a drawItem has been destroyed, similar to [Canvas.destroyed](Canvas.md#attr-canvasdestroyed).

**Flags**: RA

---
## Attr: DrawItem.titleLabel

### Description
When a non-null [title](#attr-drawitemtitle) is set, this AutoChild is created automatically and positioned at the [center](#method-drawitemgetcenter) of this `DrawItem` . The `titleLabel` moves with this `DrawItem` and, depending on [titleRotationMode](../reference.md#type-titlerotationmode), can rotate with this `DrawItem` as well.

The following [passthrough](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) applies:  
[title](#attr-drawitemtitle) for [DrawLabel.contents](DrawLabel.md#attr-drawlabelcontents).

Related to the `titleLabel` is the [titleLabelBackground](#attr-drawitemtitlelabelbackground) which allows a border to be placed around the `titleLabel` and/or a background added. By default, shapes that are commonly filled such as [DrawTriangle](../reference.md#class-drawtriangle)s, with the exception of [DrawSector](DrawSector.md#class-drawsector)s, do not show the `titleLabelBackground` (see [showTitleLabelBackground](#attr-drawitemshowtitlelabelbackground)).

### See Also

- [DrawItem.showTitleLabelBackground](#attr-drawitemshowtitlelabelbackground)

**Flags**: RA

---
## Attr: DrawItem.titleLabelPadding

### Description
If the [titleLabelBackground](#attr-drawitemtitlelabelbackground) is visible, how much padding should be left between the bounds of the [titleLabel](#attr-drawitemtitlelabel) and the edges of the `titleLabelBackground`?

**Flags**: IRA

---
## Attr: DrawItem.titleAutoFit

### Description
Whether the [DrawItem.titleLabel](#attr-drawitemtitlelabel) should be scaled to the maximum possible size that fits inside the bounds of this item. Currently only [DrawRect](DrawRect.md#class-drawrect)s and [DrawPolygon](DrawPolygon.md#class-drawpolygon)s with 90 degree angles are supported.

Note that [DrawItem.titleAutoFit](#attr-drawitemtitleautofit) isn't supported for rotated, sheared, or scaled [DrawItem](#class-drawitem)s, and that therefore the value of [TitleRotationMode](../reference.md#type-titlerotationmode), which relates to rotation of the item, is ignored when this property is set. However, we do support having the label automatically rotate to run vertically if there's more space - see [DrawItem.titleAutoFitRotationMode](#attr-drawitemtitleautofitrotationmode).

### See Also

- [DrawItem.titleLabel](#attr-drawitemtitlelabel)

**Flags**: IR

---
## Attr: DrawItem.hoverDelay

### Description
If `this.canHover` is true, how long should the mouse be kept over this widget before the hover event is fired

### Groups

- hovers

### See Also

- [DrawItem.canHover](#attr-drawitemcanhover)
- [DrawItem.hover](#method-drawitemhover)

**Flags**: IRW

---
## Attr: DrawItem.cursor

### Description
If set, specifies the cursor to display when the mouse pointer is over this DrawItem.

**Flags**: IRWA

---
## Attr: DrawItem.rotation

### Description
Rotation in degrees about the [center point](#method-drawitemgetcenter). The positive direction is clockwise.

**Flags**: IR

---
## Attr: DrawItem.titleAutoFitMargin

### Description
Specifies margin between label and item edges when using [DrawItem.titleAutoFit](#attr-drawitemtitleautofit).

### See Also

- [DrawItem.titleLabel](#attr-drawitemtitlelabel)

**Flags**: IR

---
## Attr: DrawItem.dragStartDistance

### Description
Number of pixels the cursor needs to move before the EventHandler starts a drag operation.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: DrawItem.prompt

### Description
Default [hover HTML](#method-drawitemgethoverhtml) that is displayed in the global hover canvas if the user hovers over this DrawItem and [showHover](#attr-drawitemshowhover) is true.

### Groups

- hovers

**Flags**: IRW

---
## Attr: DrawItem.xShearFactor

### Description
The slope of an x-shearing transformation applied to this DrawItem. Each point in the shape is moved along the x-axis a distance that is proportional to the initial y-coordinate of the point.

**Flags**: IRA

---
## Attr: DrawItem.drawGroup

### Description
[DrawGroup](DrawGroup.md#class-drawgroup) this drawItem is a member of.

**Flags**: IR

---
## Attr: DrawItem.fillGradient

### Description
Fill gradient to use for shapes. If a string it uses the gradient identifier parameter provided in [DrawPane.addGradient](DrawPane.md#method-drawpaneaddgradient). Otherwise it expects one of [SimpleGradient](../reference.md#object-simplegradient), [LinearGradient](../reference.md#object-lineargradient) or [RadialGradient](../reference.md#object-radialgradient).

### Groups

- fill

### See Also

- [Gradient](../reference.md#object-gradient)

**Flags**: IRW

---
## Attr: DrawItem.sideResizeKnob

### Description
If this item is showing "resize" [control knobs](#attr-drawitemknobs), this attribute specifies the MultiAutoChild for the [DrawKnob](DrawKnob.md#class-drawknob) that allows a user to resize the DrawItem with help of knobs located at centers of edges of a bounding rectangle of current DrawItem. The default shape is a light teal square.

**Flags**: IR

---
## Attr: DrawItem.linePattern

### Description
Pattern for lines, eg "solid" or "dash".

Note that support in old browsers, such as Internet Explorer versions before IE11, is limited for [drawingType](DrawPane.md#attr-drawpanedrawingtype) "bitmap" to items with straight edges - [DrawLine](DrawLine.md#class-drawline)s, [DrawPath](DrawPath.md#class-drawpath)s, and [DrawRect](DrawRect.md#class-drawrect)s with no [rounding](DrawRect.md#attr-drawrectrounding).

### Groups

- line

**Flags**: IRW

---
## Attr: DrawItem.title

### Description
A string to show at the [center point](#method-drawitemgetcenter) of this `DrawItem`.

When set to a non-null value (including an empty string), the [titleLabel](#attr-drawitemtitlelabel) [DrawLabel](DrawLabel.md#class-drawlabel) AutoChild will be created automatically and positioned at the center of this `DrawItem`.

### See Also

- [DrawItem.titleRotationMode](#attr-drawitemtitlerotationmode)

**Flags**: IRWA

---
## Attr: DrawItem.moveKnob

### Description
If this item is showing "move" [control knobs](#attr-drawitemknobs), this attribute specifies the AutoChild for the [DrawKnob](DrawKnob.md#class-drawknob) that allows a user to move the DrawItem with help of a knob located at [DrawItem.moveKnobPoint](#attr-drawitemmoveknobpoint). Default move knob shape is green circle.

**Flags**: IR

---
## Attr: DrawItem.showResizeOutline

### Description
If this item is showing "resize" [control knobs](#attr-drawitemknobs) will the resize outline be shown or not.

### See Also

- [DrawItem.resizeOutline](#attr-drawitemresizeoutline)

**Flags**: IRW

---
## Attr: DrawItem.fillColor

### Description
Fill color to use for shapes. The default of 'null' is transparent.

### Groups

- fill

**Flags**: IRW

---
## Attr: DrawItem.titleLabelBackground

### Description
When the [titleLabel](#attr-drawitemtitlelabel) is showing and [showTitleLabelBackground](#attr-drawitemshowtitlelabelbackground) is `true`, this [DrawRect](DrawRect.md#class-drawrect) AutoChild is created and placed behind the `titleLabel`.

### See Also

- [DrawItem.titleLabelPadding](#attr-drawitemtitlelabelpadding)

**Flags**: RA

---
## Attr: DrawItem.startArrow

### Description
Style of arrow head to draw at the beginning of the line or path.

**Flags**: IRW

---
## Attr: DrawItem.resizeOutline

### Description
If this item is showing "resize" [control knobs](#attr-drawitemknobs), this attribute specifies the AutoChild for the [DrawRect](DrawRect.md#class-drawrect) that draws a rectangle frame which connects all resize knobs of current DrawItem.

**Flags**: R

---
## Attr: DrawItem.titleRotationMode

### Description
The mode in which the [titleLabel](#attr-drawitemtitlelabel) (if shown) is rotated with this draw item.

### See Also

- [DrawItem.title](#attr-drawitemtitle)

**Flags**: IRA

---
## Attr: DrawItem.eventOpaque

### Description
Should events inside this DrawItem be attributed to it regardless of which pixels are actually set, if no fill is specified? If set for DrawItems that aren't closed, will capture events occurring in the region that would filled if a fill were specified. This property is true by default for closed shapes, and false for paths, lines, etc.

**Note:** this property must be true if you're writing to an HTML5 `<canvas>` element directly in your code (only applies to [DrawingType](../reference.md#type-drawingtype) "bitmap" ).

### See Also

- [DrawItem.fillColor](#attr-drawitemfillcolor)
- [DrawItem.fillOpacity](#attr-drawitemfillopacity)
- [DrawPane.getBitmap](DrawPane.md#method-drawpanegetbitmap)

**Flags**: IRA

---
## Attr: DrawItem.yShearFactor

### Description
The slope of a y-shearing transformation applied to this DrawItem. Each point in the shape is moved along the y-axis a distance that is proportional to the initial x-coordinate of the point.

**Flags**: IRA

---
## Attr: DrawItem.canDrag

### Description
Is this DrawItem draggable? If true, then the DrawItem can be drag-repositioned by the user.

**Flags**: IRWA

---
## Attr: DrawItem.shapeData

### Description
An opaque object specifying the local transformation that should be applied to this `DrawItem`, obtained through a call to [DrawItem.getShapeData](#method-drawitemgetshapedata).

**Note:** if this property is specified, you should avoid also specifying a [DrawItem.translate](#attr-drawitemtranslate), [DrawItem.scale](#attr-drawitemscale), [DrawItem.xShearFactor](#attr-drawitemxshearfactor), [DrawItem.yShearFactor](#attr-drawitemyshearfactor), or [DrawItem.rotation](#attr-drawitemrotation).

**Flags**: I

---
## Attr: DrawItem.startKnob

### Description
If this item is showing "startPoint" [control knobs](#attr-drawitemknobs), this attribute specifies the AutoChild for the [DrawKnob](DrawKnob.md#class-drawknob) for start point of current drawItem.

**Flags**: IR

---
## Attr: DrawItem.contextMenu

### Description
Context menu to show for this object, an instance of the Menu widget.

Note: if [Canvas.destroy](Canvas.md#method-canvasdestroy) is called on a canvas, any specified context menu is not automatically destroyed as well. This is in contrast to [MenuButton](MenuButton.md#class-menubutton)s which automatically destroy their specified [MenuButton.menu](MenuButton.md#attr-menubuttonmenu) by default. The behavior is intentional as context menus are commonly reused across components.

### Groups

- cues

### See Also

- [Canvas.showContextMenu](Canvas.md#method-canvasshowcontextmenu)

**Flags**: IRW

---
## Attr: DrawItem.showTitleLabelBackground

### Description
If the [titleLabel](#attr-drawitemtitlelabel) is showing, should the [titleLabelBackground](#attr-drawitemtitlelabelbackground) be created and placed behind the `titleLabel`?

This defaults to true for [DrawSector](DrawSector.md#class-drawsector)s and shapes that are not commonly filled (e.g. [DrawLine](DrawLine.md#class-drawline)s).

**Flags**: IRA

---
## Attr: DrawItem.cornerResizeKnob

### Description
If this item is showing "resize" [control knobs](#attr-drawitemknobs), this attribute specifies the MultiAutoChild for the [DrawKnob](DrawKnob.md#class-drawknob) that allows a user to resize the DrawItem with help of knobs located at corners of a bounding rectangle of current DrawItem. The default shape is a light teal circle.

**Flags**: IR

---
## Attr: DrawItem.scale

### Description
Array holds 2 values representing scaling along x and y dimensions.

**Flags**: IRA

---
## Attr: DrawItem.endArrow

### Description
Style of arrow head to draw at the end of the line or path.

**Flags**: IRW

---
## Attr: DrawItem.translate

### Description
Array holds two values representing translation along the x and y dimensions.

**Flags**: IRA

---
## Attr: DrawItem.shadow

### Description
Shadow used for all DrawItem subtypes.

**Flags**: IRW

---
## Attr: DrawItem.lineCap

### Description
Style of drawing the endpoints of a line.

Note that for dashed and dotted lines, the lineCap style affects each dash or dot.

### Groups

- line

**Flags**: IRW

---
## Attr: DrawItem.lineWidth

### Description
Pixel width for lines.

### Groups

- line

**Flags**: IRW

---
## Attr: DrawItem.rotateKnob

### Description
If this item is showing "rotate" [control knobs](#attr-drawitemknobs), this attribute specifies the AutoChild for the [DrawKnob](DrawKnob.md#class-drawknob) that allows a user to rotate the DrawItem with help of a knob located above. Default rotate knob shape is green circle.

**Flags**: IR

---
## Attr: DrawItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: DrawItem.useSimpleTransform

### Description
If true, when a DrawItem is [moved](#method-drawitemmoveto) or [resized](#method-drawitemresizeto), the transform is applied by manipulating the shape coordinates, if possible, rather than by introducing scaling, shearing, rotation, or translation. This is only supported currently for [DrawRect](DrawRect.md#class-drawrect), [DrawOval](DrawOval.md#class-drawoval), [DrawDiamond](DrawDiamond.md#class-drawdiamond), [DrawImage](DrawImage.md#class-drawimage), and [DrawLabel](DrawLabel.md#class-drawlabel), and only if no shearing is already present. Further, it's only possible to keep the transform simple if both axes are scaled by the same amount during the resize (or end up at the same scale if the DrawItem is already scaled unevenly), unless the rotation angle is a multiple of 90 degrees.

For [DrawPolygon](DrawPolygon.md#class-drawpolygon) and other shapes not based on a box (top/left/width/height), we can't safely just modify coordinates to effect a resize as we can do for [DrawRect](DrawRect.md#class-drawrect) (and similar), so resizing will normally introduce or modify the transform, potentially introducing scaling or shearing, rather than modifying coordinates. For such [DrawItem](#class-drawitem)s, we avoid trying to manipulate the coordinates, in part, because there's a danger that the floating point error may accumulate over time and warp the shape.

### See Also

- [DrawItem.moveTo](#method-drawitemmoveto)
- [DrawItem.moveBy](#method-drawitemmoveby)
- [DrawItem.resizeTo](#method-drawitemresizeto)
- [DrawItem.resizeBy](#method-drawitemresizeby)

**Flags**: IRWA

---
## Attr: DrawItem.canHover

### Description
Will this DrawItem fire hover events when the user hovers over it?

### Groups

- hovers

### See Also

- [DrawItem.showHover](#attr-drawitemshowhover)

**Flags**: IRW

---
## Attr: DrawItem.proportionalResizing

### Description
This property specifies the conditions for when proportional resizing is used.

By default the DrawItem is forced to only resize proportionally while any modifier key specified in [DrawItem.proportionalResizeModifiers](#attr-drawitemproportionalresizemodifiers) is pressed. For example, the DrawItem will change its width and height by the same percentage as long as the "Shift" key is held down.

Note that this property only has an effect if the DrawItem is showing "resize" [control knobs](#attr-drawitemknobs).

**Flags**: IR

---
## Attr: DrawItem.lineOpacity

### Description
Opacity for lines, as a number between 0 (transparent) and 1 (opaque).

### Groups

- line

**Flags**: IRW

---
## Attr: DrawItem.endKnob

### Description
If this item is showing "endPoint" [control knobs](#attr-drawitemknobs), this attribute specifies the AutoChild for the [DrawKnob](DrawKnob.md#class-drawknob) for end point of current drawItem.

**Flags**: IR

---
## ClassMethod: DrawItem.computeAngle

### Description
Computes the angle in degrees from the positive X axis to the difference vector **v**2 - **v**1 between the two given vectors.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| px1 | [double](../reference.md#type-double) | false | — | X coordinate of **v**1 |
| py1 | [double](../reference.md#type-double) | false | — | Y coordinate of **v**1 |
| px2 | [double](../reference.md#type-double) | false | — | X coordinate of **v**2 |
| py2 | [double](../reference.md#type-double) | false | — | Y coordinate of **v**2 |

### Returns

`[double](../reference.md#type-double)` — the angle in degrees, in the range \[0, 360).

---
## Method: DrawItem.dragStop

### Description
Notification fired when the user stops dragging this DrawItem. Will only fire if [canDrag](#attr-drawitemcandrag) is true.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel drag interaction.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawItem.scaleBy

### Description
Scale the shape by the x, y multipliers

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [float](../reference.md#type-float) | false | — | scale in the x direction |
| y | [float](../reference.md#type-float) | false | — | scale in the y direction |

---
## Method: DrawItem.setStartArrow

### Description
Set the arrowhead at the beginning of this path.

**NOTE:** Not all DrawItem classes support arrowheads. You can use [DrawItem.supportsStartArrow](#method-drawitemsupportsstartarrow) to dynamically check whether a DrawItem instance supports this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arrowStyle | [ArrowStyle](../reference.md#type-arrowstyle) | false | — | style of arrow to use |

---
## Method: DrawItem.setFillOpacity

### Description
Update fillOpacity for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| opacity | [float](../reference.md#type-float) | false | — | new opacity, as a number between 0 (transparent) and 1 (opaque). |

---
## Method: DrawItem.showAllKnobs

### Description
Shows all supported control knobs for this drawItem. Updates [DrawItem.knobs](#attr-drawitemknobs) to include the supported knobTypes and if necessary draws out the appropriate control knobs.

---
## Method: DrawItem.drawStart

### Description
Called when we start drawing for this DrawItem to the [DrawItem.drawPane](#attr-drawitemdrawpane)'s underlying HTML5 `<canvas>` element. Only called if the [DrawingType](../reference.md#type-drawingtype) is "bitmap".

There is no default implementation of this method.

**Flags**: A

---
## Method: DrawItem.moveBy

### Description
Move the shape by the specified deltas for the left and top coordinate.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [int](../reference.md#type-int) | false | — | change to left coordinate in pixels |
| dY | [int](../reference.md#type-int) | false | — | change to top coordinate in pixels |

---
## Method: DrawItem.setPropertyValue

### Description
Sets a property on this DrawItem, calling the appropriate setter method if one is found and is [supported](Class.md#classmethod-classismethodsupported).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| propertyName | [String](#type-string) | false | — | name of the property to set |
| newValue | [Any](#type-any) | false | — | new value for the property |

### See Also

- [Class.setProperty](Class.md#method-classsetproperty)

---
## Method: DrawItem.setMoveKnobOffset

### Description
Setter for [DrawItem.moveKnobOffset](#attr-drawitemmoveknoboffset).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newMoveKnobOffset | [Array of int](#type-array-of-int)[] | true | — | the new move knob offset. This is a 2-element array of \[left offset, top offset\]. If null, then `[0,0]` is assumed. |

**Flags**: A

---
## Method: DrawItem.getBoundingBox

### Description
Calculates the bounding box of the shape in the [local coordinate system](DrawPane.md#class-drawpane).

Note that the bounding box of the shape when transformed into the global coordinate system is available from the method [DrawItem.getResizeBoundingBox](#method-drawitemgetresizeboundingbox).

### Returns

`[Array of double](#type-array-of-double)` — the x1, y1, x2, y2 coordinates. When the width and height are both positive, point (x1, y1) is the top-left point of the bounding box and point (x2, y2) is the bottom-right point of the bounding box.

### See Also

- [DrawPane](DrawPane.md#class-drawpane)

---
## Method: DrawItem.setLineWidth

### Description
Update lineWidth for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [int](../reference.md#type-int) | false | — | new pixel lineWidth |

---
## Method: DrawItem.supportsEndArrow

### Description
Does this DrawItem [support](Class.md#classmethod-classismethodsupported) [DrawItem.setEndArrow](#method-drawitemsetendarrow)? For example, this is false for [DrawRect](DrawRect.md#class-drawrect) and [DrawOval](DrawOval.md#class-drawoval), and true for [DrawLine](DrawLine.md#class-drawline).

### Returns

`[boolean](../reference.md#type-boolean)` — whether setEndArrow() is supported by this DrawItem.

**Flags**: A

---
## Method: DrawItem.computeAngle

### Description
Computes the angle in degrees from the positive X axis to the difference vector **v**2 - **v**1 between the two given vectors.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| px1 | [double](../reference.md#type-double) | false | — | X coordinate of **v**1 |
| py1 | [double](../reference.md#type-double) | false | — | Y coordinate of **v**1 |
| px2 | [double](../reference.md#type-double) | false | — | X coordinate of **v**2 |
| py2 | [double](../reference.md#type-double) | false | — | Y coordinate of **v**2 |

### Returns

`[double](../reference.md#type-double)` — the angle in degrees, in the range \[0, 360).

---
## Method: DrawItem.setEndArrow

### Description
Set the arrowhead at the end of this path.

**NOTE:** Not all DrawItem classes support arrowheads. You can use [DrawItem.supportsEndArrow](#method-drawitemsupportsendarrow) to dynamically check whether a DrawItem instance supports this method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arrowStyle | [ArrowStyle](../reference.md#type-arrowstyle) | false | — | style of arrow to use |

---
## Method: DrawItem.setDrawPane

### Description
Setter for [drawPane](#attr-drawitemdrawpane).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| drawPane | [DrawPane](#type-drawpane) | false | — | new value for `this.drawPane`. |

---
## Method: DrawItem.hover

### Description
If [canHover](#attr-drawitemcanhover) is true for this DrawItem, the hover() string method will be fired when the user hovers over this DrawItem. If this method returns false, it will suppress the default behavior of showing a hover canvas if [showHover](#attr-drawitemshowhover) is true.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel the hover event.

### Groups

- hovers

---
## Method: DrawItem.moved

### Description
Notification method fired when this component is explicitly moved. Note that a component's position on the screen may also be changed due to an ancestor being moved. The [parentMoved()](Canvas.md#method-canvasparentmoved) method provides a notification entry point to catch that case as well.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| deltaX | [int](../reference.md#type-int) | false | — | horizontal difference between current and previous position |
| deltaY | [int](../reference.md#type-int) | false | — | vertical difference between current and previous position |

---
## Method: DrawItem.getCenter

### Description
Returns the center point of this draw item in local coordinates. Generally this is the center of the [bounding box](#method-drawitemgetboundingbox), but some item types may use a different point. For example, [DrawTriangle](../reference.md#class-drawtriangle) uses the [incenter](http://en.wikipedia.org/wiki/Incenter#Cartesian_coordinates) of the triangle.

### Returns

`[Point](#type-point)` — the center point in local coordinates

---
## Method: DrawItem.setLineOpacity

### Description
Update lineOpacity for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| opacity | [float](../reference.md#type-float) | false | — | new opacity, as a number between 0 (transparent) and 1 (opaque). |

---
## Method: DrawItem.setLineColor

### Description
Update lineColor for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [CSSColor](../reference_2.md#type-csscolor) | false | — | new line color. Pass null for transparent. |

---
## Method: DrawItem.getPageTop

### Description
Returns the page-relative top coordinate of the widget on the page, in pixels

### Returns

`[number](#type-number)` — GLOBAL top coordinate

### Groups

- positioning

**Flags**: A

---
## Method: DrawItem.setZIndex

### Description
Setter for [DrawItem.zIndex](#attr-drawitemzindex).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newZIndex | [Integer](../reference_2.md#type-integer) | false | — | new `zIndex`. If null and this draw item is already in a `DrawPane` or `DrawGroup`, then this item's zIndex will be set to the next higher auto-assigned zIndex.

Note that when setting draw items' zIndexes via this advanced API, the application should take over management of all draw items' zIndexes, and [bringToFront()](#method-drawitembringtofront) / [sendToBack()](#method-drawitemsendtoback) should not be used, as those APIs assume automatic management of zIndexes. |

### Groups

- zIndex

**Flags**: A

---
## Method: DrawItem.hideKnobs

### Description
Hides a set of control knobs for this drawItem. Updates [DrawItem.knobs](#attr-drawitemknobs) to remove the specified knobType, and clears any drawn knobs for this knobType.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| knobType | [KnobType](../reference.md#type-knobtype)|[Array of KnobType](#type-array-of-knobtype) | false | — | knobs to hide |

---
## Method: DrawItem.isPointInPath

### Description
Returns true if the given point in the drawing coordinate system is within this DrawItem's shape, taking into account local transforms.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [int](../reference.md#type-int) | false | — | X coordinate of the test point. |
| y | [int](../reference.md#type-int) | false | — | Y coordinate of the test point. |

### Returns

`[boolean](../reference.md#type-boolean)` — —

---
## Method: DrawItem.resized

### Description
Observable method called whenever a DrawItem changes size.

---
## Method: DrawItem.mouseOver

### Description
Notification fired when the mouse enters this DrawItem.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawItem.supportsStartArrow

### Description
Does this DrawItem [support](Class.md#classmethod-classismethodsupported) [DrawItem.setStartArrow](#method-drawitemsetstartarrow)? For example, this is false for [DrawRect](DrawRect.md#class-drawrect) and [DrawOval](DrawOval.md#class-drawoval), and true for [DrawLine](DrawLine.md#class-drawline).

### Returns

`[boolean](../reference.md#type-boolean)` — whether setStartArrow() is supported by this DrawItem.

**Flags**: A

---
## Method: DrawItem.resizeTo

### Description
Resize to the specified size

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Integer](../reference_2.md#type-integer) | false | — | new width |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height |

---
## Method: DrawItem.dragStart

### Description
Notification fired when the user starts to drag this DrawItem. Will only fire if [canDrag](#attr-drawitemcandrag) is true.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel drag action.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawItem.getResizeBoundingBox

### Description
Calculates the bounding box of the shape reflected by the [resize outline](#attr-drawitemshowresizeoutline) shown when dragging the [resize knobs](#attr-drawitemresizeknobpoints). This method is similar to [DrawItem.getBoundingBox](#method-drawitemgetboundingbox) except that the coordinates returned by this method are in the global coordinate system (described [here](DrawPane.md#class-drawpane)) rather than the local coordinate system.

### Returns

`[Array](#type-array)` — the x1, y1, x2, y2 coordinates. When the width and height are both positive, point (x1, y1) is the top-left point of the bounding box and point (x2, y2) is the bottom-right point of the bounding box.

### See Also

- [DrawItem.getBoundingBox](#method-drawitemgetboundingbox)

---
## Method: DrawItem.bringToFront

### Description
Places this draw item at the top of the stacking order so that it appears in front of other draw items in the same [DrawPane](DrawPane.md#class-drawpane) or [DrawGroup](DrawGroup.md#class-drawgroup).

When the `DrawPane`'s [drawingType](DrawPane.md#attr-drawpanedrawingtype) is "bitmap", [DrawItem.zIndex](#attr-drawitemzindex), bringToFront(), and [DrawItem.sendToBack](#method-drawitemsendtoback) are not supported for [DrawLabel](DrawLabel.md#class-drawlabel)s on iOS due to platform limitations.

### Groups

- zIndex

### See Also

- [DrawItem.sendToBack](#method-drawitemsendtoback)
- [DrawItem.setZIndex](#method-drawitemsetzindex)

---
## Method: DrawItem.setShadow

### Description
Update shadow for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| shadow | [Shadow](#type-shadow) | false | — | new shadow |

---
## Method: DrawItem.setFillGradient

### Description
Update fillGradient for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| gradient | [Gradient](#type-gradient) | false | — | new gradient to use. Pass null for transparent. |

---
## Method: DrawItem.isInBounds

### Description
Returns true if the given point in the drawing coordinate system, when converted to coordinates in this DrawItem's local coordinate system, is within the [bounding box](#method-drawitemgetboundingbox) of this DrawItem's shape.

This method can be used to quickly check whether the given point is definitely _not_ within the DrawItem shape. To check whether the point is within the DrawItem shape, use the slower but exact [DrawItem.isPointInPath](#method-drawitemispointinpath) method.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [int](../reference.md#type-int) | false | — | X coordinate of the point in the drawing coordinate system. |
| y | [int](../reference.md#type-int) | false | — | Y coordinate of the point in the drawing coordinate system. |

### Returns

`[boolean](../reference.md#type-boolean)` — —

---
## Method: DrawItem.mouseOut

### Description
Notification fired when the mouse leaves this DrawItem.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

---
## Method: DrawItem.drawEnd

### Description
Called when we finish drawing for this DrawItem to the [DrawItem.drawPane](#attr-drawitemdrawpane)'s underlying HTML5 `<canvas>` element. Only called if the [DrawingType](../reference.md#type-drawingtype) is "bitmap".

There is no default implementation of this method.

**Flags**: A

---
## Method: DrawItem.getZIndex

### Description
Returns the [zIndex](#attr-drawitemzindex) of this draw item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| resolveToNumber | [Boolean](#type-boolean) | true | — | if true and this item's `zIndex` is null, resolve to the next higher zIndex. |

### Returns

`[Integer](../reference_2.md#type-integer)` — this draw item's zIndex, or null if not resolved yet. If the `resolveToNumber` parameter is true, then the returned integer is guaranteed to be non-null.

### Groups

- zIndex

---
## Method: DrawItem.erase

### Description
Erase this drawItem's visual representation and remove it from its DrawGroup (if any) and DrawPane.

To re-draw the item within the DrawPane, call [DrawItem.draw](#method-drawitemdraw) again, or use [DrawPane.addDrawItem](DrawPane.md#method-drawpaneadddrawitem) to move to another DrawGroup.

---
## Method: DrawItem.dragMove

### Description
Notification fired for every mouseMove event triggered while the user is dragging this DrawItem. Will only fire if [canDrag](#attr-drawitemcandrag) is true.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel drag interaction.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawItem.getSvgString

### Description
Generates a string containing the SVG source of this DrawItem.

**NOTE:** The generated SVG source assumes that the default namespace is `http://www.w3.org/2000/svg` and that namespace prefix `xlink` refers to namespace name `http://www.w3.org/1999/xlink`.

---
## Method: DrawItem.show

### Description
Make this drawItem visible.

---
## Method: DrawItem.showKnobs

### Description
Shows a set of control knobs for this drawItem. Updates [DrawItem.knobs](#attr-drawitemknobs) to include the specified knobType, and if necessary draws out the appropriate control knobs.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| knobType | [KnobType](../reference.md#type-knobtype)|[Array of KnobType](#type-array-of-knobtype) | false | — | knobs to show |

---
## Method: DrawItem.sendToBack

### Description
Places this draw item at the bottom of the stacking order so that it appears behind other draw items in the same [DrawPane](DrawPane.md#class-drawpane) or [DrawGroup](DrawGroup.md#class-drawgroup).

When the `DrawPane`'s [drawingType](DrawPane.md#attr-drawpanedrawingtype) is "bitmap", [DrawItem.zIndex](#attr-drawitemzindex), [DrawItem.bringToFront](#method-drawitembringtofront), and sendToBack() are not supported for [DrawLabel](DrawLabel.md#class-drawlabel)s on iOS due to platform limitations.

### Groups

- zIndex

### See Also

- [DrawItem.bringToFront](#method-drawitembringtofront)
- [DrawItem.setZIndex](#method-drawitemsetzindex)

---
## Method: DrawItem.setLineCap

### Description
Update lineCap for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| cap | [LineCap](../reference.md#type-linecap) | false | — | new lineCap to use |

---
## Method: DrawItem.rotateBy

### Description
Rotate the shape by the relative rotation in degrees

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| degrees | [float](../reference.md#type-float) | false | — | number of degrees to rotate from current orientation. |

---
## Method: DrawItem.dragResizeMove

### Description
If [DrawItem.canDrag](#attr-drawitemcandrag) is true and the [control knobs](#attr-drawitemknobs) include "resize" knobs, then this notification method will be fired when the user drag-resizes the draw item.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| position | [String](#type-string) | false | — | provides which knob of the [DrawItem.resizeKnobPoints](#attr-drawitemresizeknobpoints) was dragged |
| x | [Integer](../reference_2.md#type-integer) | false | — | new x-coordinate of the knob |
| y | [Integer](../reference_2.md#type-integer) | false | — | new y-coordinate of the knob |
| dX | [Integer](../reference_2.md#type-integer) | false | — | horizontal distance moved |
| dY | [Integer](../reference_2.md#type-integer) | false | — | vertical distance moved |

**Flags**: A

---
## Method: DrawItem.showContextMenu

### Description
Executed when the right mouse button is clicked. The default implementation of this method auto-creates a [Menu](Menu.md#class-menu) from the [Canvas.contextMenu](Canvas.md#attr-canvascontextmenu) property on this component and then calls [Menu.showContextMenu](Menu.md#method-menushowcontextmenu) on it to show it.

If you want to show a standard context menu, you can simply define your Menu and set it as the contextMenu property on your component - you do not need to override this method.

If you want to do some other processing before showing a menu or do something else entirely, then you should override this method. Note that the return value from this method controls whether or not the native browser context menu is shown.

### Returns

`[boolean](../reference.md#type-boolean)` — false == don't show native context menu, true == show native context menu

### Groups

- widgetEvents

### See Also

- [DrawItem.contextMenu](#attr-drawitemcontextmenu)
- [Menu.showContextMenu](Menu.md#method-menushowcontextmenu)
- [Canvas.hideContextMenu](Canvas.md#method-canvashidecontextmenu)
- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

**Flags**: A

---
## Method: DrawItem.setCursor

### Description
—

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCursor | [Cursor](../reference.md#type-cursor) | false | — | new cursor. |

---
## Method: DrawItem.setTitle

### Description
Setter for the [title](#attr-drawitemtitle) of this `DrawItem`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [String](#type-string) | true | — | new `title`. |

**Flags**: A

---
## Method: DrawItem.getPageLeft

### Description
Returns the page-relative left coordinate of the widget on the page, in pixels.

### Returns

`[number](#type-number)` — global left coordinate

### Groups

- positioning

**Flags**: A

---
## Method: DrawItem.setCanDrag

### Description
Setter for [canDrag](#attr-drawitemcandrag).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canDrag | [Boolean](#type-boolean) | false | — | new value for `this.canDrag`. |

---
## Method: DrawItem.setCenterPoint

### Description
Change the center point for this DrawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [int](../reference.md#type-int) | false | — | X coordinate of the center point (in the global coordinate system). |
| top | [int](../reference.md#type-int) | false | — | Y coordinate of the center point (in the global coordinate system). |

---
## Method: DrawItem.setFillColor

### Description
Update fillColor for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [CSSColor](../reference_2.md#type-csscolor) | false | — | new fillColor to use. Pass null for transparent. |

---
## Method: DrawItem.resizeBy

### Description
Resize the shape by the specified deltas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [int](../reference.md#type-int) | false | — | number of pixels to resize by horizontally |
| dY | [int](../reference.md#type-int) | false | — | number of pixels to resize by vertically |

---
## Method: DrawItem.getHoverHTML

### Description
If [showHover](#attr-drawitemshowhover) is true, when the user holds the mouse over this DrawItem for long enough to trigger a hover event, a hover canvas is shown by default. This method returns the contents of that hover canvas. Default implementation returns [prompt](#attr-drawitemprompt) - override for custom hover HTML. Note that returning `null` or an empty string will suppress the hover canvas altogether.

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the HTML to show in the hover

### Groups

- hovers

---
## Method: DrawItem.moveTo

### Description
Move the DrawItem to the specified coordinates in the global coordinate system. The specified coordinates will become the top-left point of the [resize bounding box](#method-drawitemgetresizeboundingbox).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left coordinate in pixels |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top coordinate in pixels |

---
## Method: DrawItem.mouseUp

### Description
Notification fired when the user releases the left mouse button on this DrawItem.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawItem.setLinePattern

### Description
Update linePattern for this drawItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pattern | [LinePattern](../reference.md#type-linepattern) | false | — | new linePattern to use |

---
## Method: DrawItem.destroy

### Description
Permanently destroys this DrawItem, similar to [Canvas.destroy](Canvas.md#method-canvasdestroy).

### See Also

- [memoryLeaks](../kb_topics/memoryLeaks.md#kb-topic-memory-leaks)

---
## Method: DrawItem.mouseDown

### Description
Notification fired when the user presses the left mouse button on this DrawItem.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawItem.rotateTo

### Description
Rotate the shape by the absolute rotation in degrees

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| degrees | [float](../reference.md#type-float) | false | — | number of degrees to rotate |

---
## Method: DrawItem.hideAllKnobs

### Description
Hides all control knobs for this drawItem. Updates [DrawItem.knobs](#attr-drawitemknobs) to remove all knobTypes and clears any drawn knobs.

---
## Method: DrawItem.draw

### Description
Draws this item into its current [drawPane](#attr-drawitemdrawpane).

NOTE: For performance reasons, the `DrawPane` may draw this item on a delay to allow multiple items to be added and drawn at one time. The [DrawPane.refreshNow](DrawPane.md#method-drawpanerefreshnow) API will force this item to be drawn immediately.

---
## Method: DrawItem.scaleTo

### Description
Scale the shape by the x, y multipliers

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [float](../reference.md#type-float) | false | — | scale in the x direction |
| y | [float](../reference.md#type-float) | false | — | scale in the y direction |

---
## Method: DrawItem.click

### Description
Notification fired when the user clicks on this DrawItem.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
## Method: DrawItem.hide

### Description
Hide this drawItem.

---
## Method: DrawItem.getShapeData

### Description
Returns an opaque JavaScript object representing the current local transformation applied to the DrawItem's local coordinates, as defined by [DrawItem.translate](#attr-drawitemtranslate), [DrawItem.scale](#attr-drawitemscale), [DrawItem.xShearFactor](#attr-drawitemxshearfactor), [DrawItem.yShearFactor](#attr-drawitemyshearfactor), and [DrawItem.rotation](#attr-drawitemrotation). The object may be serialized and deserialized as JSON, and passed into the constructor block as [DrawItem.shapeData](#attr-drawitemshapedata) to restore the local transformation.

**Note:** this doesn't include any sepatate configuration, such as for a [DrawRect](DrawRect.md#class-drawrect) the current values of [left](DrawRect.md#attr-drawrectleft), [top](DrawRect.md#attr-drawrecttop), [width](DrawRect.md#attr-drawrectwidth), or [height](DrawRect.md#attr-drawrectheight).

### Returns

`[Object](../reference_2.md#type-object)` — opaque tranformation data

### See Also

- [JSON.encode](JSON.md#classmethod-jsonencode)

---
## Method: DrawItem.mouseMove

### Description
Notification fired when the user moves the mouse over this DrawItem.

Note that if this item is part of a [DrawGroup](DrawGroup.md#class-drawgroup), then the group's [useGroupRect](DrawGroup.md#attr-drawgroupusegrouprect) setting affects whether this item receives the notification. If useGroupRect is true, then this item will _not_ receive the notification. Otherwise, the item receives the notification and notification bubbles up to the group.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](Canvas.md#method-canvasgetoffsetx)
- [Canvas.getOffsetY](Canvas.md#method-canvasgetoffsety)

---
