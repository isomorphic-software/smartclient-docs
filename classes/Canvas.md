# Canvas Documentation

[← Back to API Index](../reference.md)

---

## Class: Canvas

*Inherits from:* [BaseWidget](../reference.md#class-basewidget)

### Description
Base class for all SmartClient visual components (except [FormItems](FormItem.md#class-formitem)).

Canvas provides:

*   basic visual lifecycle support - creation and destruction of HTML via [draw()](#method-canvasdraw) and [clear()](#method-canvasclear), visibility via [show()](#method-canvasshow) and [hide()](#method-canvashide), z-layering via [bringToFront()](#method-canvasbringtofront) and [sendToBack()](#method-canvassendtoback).
*   consistent cross-browser [positioning](#method-canvasmoveto), [sizing](#method-canvasresizeto) and [size detection](#method-canvasgetscrollheight), with automatic compensation for [browser CSS behavior differences](../reference.md#type-cssstylename).
*   clipping, scrolling and overflow management of content via [Canvas.overflow](#attr-canvasoverflow)
*   consistent cross-browser [key](#method-canvaskeypress) and [mouse](#method-canvasmousedown) events, including [mapping touch events](../kb_topics/mobileDevelopment.md#kb-topic-mobile-application-development) to mouse events
*   built-in drag and drop capabilities including [moving](#attr-canvascandragreposition), [resizing](#attr-canvascandragresize), [drag scrolling](#attr-canvascandragscroll) and [snap-to-grid](#attr-canvassnaptogrid) behavior.
*   the ability to either contain [HTML content](#attr-canvascontents) or [contain other Canvases](#attr-canvaschildren), including [an edge-based positioning](#attr-canvassnapto) and [percent sizing system](#attr-canvaspercentsource) for children. For more advanced layout capabilities, see [Layout](Layout.md#class-layout).
*   various other details like [cursors](#attr-canvascursor), [modal masking](#method-canvasshowclickmask), [animation](#method-canvasanimatemove), [accessibility properties](#attr-canvasariarole), and [settings](#attr-canvaslocatechildrenby) for [automated testing](../kb_topics/automatedTesting.md#kb-topic-automated-testing).

---
## ClassAttr: Canvas.REPEAT

### Description
A declared value of the enum type [BackgroundRepeat](../reference_2.md#type-backgroundrepeat).

**Flags**: R

---
## ClassAttr: Canvas.defaultPageSpace

### Description
A fixed number of pixels at the top of the page in which components will not be placed. This is overridable per-instance via the [Canvas.leavePageSpace](#attr-canvasleavepagespace) attribute. Essentially, the effect is that all top-level components are shifted down this number of pixels, and the page height is treated as this number of pixels _less_ than the real page height.

This attribute can be useful on certain mobile devices, when components should not be placed in a top portion of the screen. For example, on iOS devices in certain configurations, this can be set to 20 to avoid placing any component into the status bar area. Or, if using iOS 7.1's 'minimal-ui' viewport parameter, this can be set to 20 to avoid placing any component into the top 20px area of the screen, which if tapped on iPhone in landscape, causes Mobile Safari's address bar and tab bar to be shown.

This setting can be changed at runtime by calling [Canvas.setDefaultPageSpace](#classmethod-canvassetdefaultpagespace).

**Note:** As documented by the [Mobile Application Development](../kb_topics/mobileDevelopment.md#kb-topic-mobile-application-development) page, when the SmartClient application is running in Mobile Safari on iPhone running iOS 7.1 or later, and neither the `isc_useDefaultViewport` nor the `isc_useMinimalUI` global is set to `false` when the framework is loaded, then the framework will automatically set the `defaultPageSpace` to 0 in portrait orientation, and to 20 in landscape orientation.

### Groups

- positioning

**Flags**: IRA

---
## ClassAttr: Canvas.loadingImageSrc

### Description
Image URL to be displayed while data is being loaded (if enabled for the widget waiting for data). Must be square; [Canvas.loadingImageSize](#classattr-canvasloadingimagesize) specifies the width and height.

### Groups

- animation

### See Also

- [ListGrid.loadingDataMessage](ListGrid_1.md#attr-listgridloadingdatamessage)
- [DetailViewer.loadingMessage](DetailViewer.md#attr-detailviewerloadingmessage)
- [HTMLFlow.loadingMessage](HTMLFlow.md#attr-htmlflowloadingmessage)
- [ViewLoader.loadingMessage](ViewLoader.md#attr-viewloaderloadingmessage)

**Flags**: RWA

---
## ClassAttr: Canvas.CLIP_H

### Description
A declared value of the enum type [Overflow](../reference.md#type-overflow).

**Flags**: R

---
## ClassAttr: Canvas.ABSOLUTE

### Description
A declared value of the enum type [Positioning](../reference.md#type-positioning).

**Flags**: R

---
## ClassAttr: Canvas.allowExternalFilters

### Description
If enabled, uses a moderately expensive workaround to allow the use of IE filters in CSS to produce gradient effects for buttons, grid rows, and other elements, without the use of image backgrounds.

See [IEFilters](../kb_topics/IEFilters.md#kb-topic-internet-explorer-filter-effects) for background.

### Groups

- IEFilters

**Flags**: IR

---
## ClassAttr: Canvas.RELATIVE

### Description
A declared value of the enum type [Positioning](../reference.md#type-positioning).

**Flags**: R

---
## ClassAttr: Canvas.MOVE

### Description
A declared value of the enum type s [DragDataAction](../reference.md#type-dragdataaction) and [Cursor](../reference.md#type-cursor).

**Flags**: R

---
## ClassAttr: Canvas.TEXT

### Description
A declared value of the enum type [Cursor](../reference.md#type-cursor).

**Flags**: R

---
## ClassAttr: Canvas.REPEAT_X

### Description
A declared value of the enum type [BackgroundRepeat](../reference_2.md#type-backgroundrepeat).

**Flags**: R

---
## ClassAttr: Canvas.CLIP_V

### Description
A declared value of the enum type [Overflow](../reference.md#type-overflow).

**Flags**: R

---
## ClassAttr: Canvas.neverUsePNGWorkaround

### Description
If set, the AlphaImageLoader IE filter will never be used. Does not remove AlphaImageLoader usage in already-drawn components.

See [IEFilters](../kb_topics/IEFilters.md#kb-topic-internet-explorer-filter-effects) for background.

### Groups

- IEFilters

**Flags**: IR

---
## ClassAttr: Canvas.HIDDEN

### Description
A declared value of the enum type s [Overflow](../reference.md#type-overflow) and [Visibility](../reference_2.md#type-visibility).

**Flags**: R

---
## ClassAttr: Canvas.LEFT

### Description
A declared value of the enum type s [Side](../reference.md#type-side), [Alignment](../reference.md#type-alignment) and [Direction](../reference_2.md#type-direction).

**Flags**: R

---
## ClassAttr: Canvas.INHERIT

### Description
A declared value of the enum type [Visibility](../reference_2.md#type-visibility).

**Flags**: R

---
## ClassAttr: Canvas.TAB_INDEX_FLOOR

### Description
Specifies the lower limit for automatically assigned tab indices for focusable canvii.

### Groups

- focus

**Flags**: R

---
## ClassAttr: Canvas.loadingImageSize

### Description
Specifies the width and height of [Canvas.loadingImageSrc](#classattr-canvasloadingimagesrc).

### Groups

- animation

**Flags**: RWA

---
## ClassAttr: Canvas.HELP

### Description
A declared value of the enum type [Cursor](../reference.md#type-cursor).

**Flags**: R

---
## ClassAttr: Canvas.NO_REPEAT

### Description
A declared value of the enum type [BackgroundRepeat](../reference_2.md#type-backgroundrepeat).

**Flags**: R

---
## ClassAttr: Canvas.SCROLL

### Description
A declared value of the enum type [Overflow](../reference.md#type-overflow).

**Flags**: R

---
## ClassAttr: Canvas.UP

### Description
A declared value of the enum type [Direction](../reference_2.md#type-direction).

**Flags**: R

---
## ClassAttr: Canvas.BOTTOM

### Description
A declared value of the enum type s [VerticalAlignment](../reference.md#type-verticalalignment) and [Side](../reference.md#type-side).

**Flags**: R

---
## ClassAttr: Canvas.AUTO

### Description
A declared value of the enum type s [Overflow](../reference.md#type-overflow) and [Cursor](../reference.md#type-cursor).

**Flags**: R

---
## ClassAttr: Canvas.POINTER

### Description
A declared value of the enum type [Cursor](../reference.md#type-cursor).

**Flags**: R

---
## ClassAttr: Canvas.NORMAL

### Description
A declared value of the enum type [ImageStyle](../reference.md#type-imagestyle).

**Flags**: R

---
## ClassAttr: Canvas.STRETCH

### Description
A declared value of the enum type [ImageStyle](../reference.md#type-imagestyle).

**Flags**: R

---
## ClassAttr: Canvas.DEFAULT

### Description
A declared value of the enum type [Cursor](../reference.md#type-cursor).

**Flags**: R

---
## ClassAttr: Canvas.TOP

### Description
A declared value of the enum type s [VerticalAlignment](../reference.md#type-verticalalignment) and [Side](../reference.md#type-side).

**Flags**: R

---
## ClassAttr: Canvas.HAND

### Description
A declared value of the enum type [Cursor](../reference.md#type-cursor).

**Flags**: R

---
## ClassAttr: Canvas.RIGHT

### Description
A declared value of the enum type s [Side](../reference.md#type-side), [Alignment](../reference.md#type-alignment) and [Direction](../reference_2.md#type-direction).

**Flags**: R

---
## ClassAttr: Canvas.CENTER

### Description
A declared value of the enum type s [ImageStyle](../reference.md#type-imagestyle), [VerticalAlignment](../reference.md#type-verticalalignment) and [Alignment](../reference.md#type-alignment).

**Flags**: R

---
## ClassAttr: Canvas.WAIT

### Description
A declared value of the enum type [Cursor](../reference.md#type-cursor).

**Flags**: R

---
## ClassAttr: Canvas.DOWN

### Description
A declared value of the enum type [Direction](../reference_2.md#type-direction).

**Flags**: R

---
## ClassAttr: Canvas.REPEAT_Y

### Description
A declared value of the enum type [BackgroundRepeat](../reference_2.md#type-backgroundrepeat).

**Flags**: R

---
## ClassAttr: Canvas.neverUseFilters

### Description
Disables automatic use of filters in IE by default. Filters will only be used if [Canvas.useOpacityFilter](#attr-canvasuseopacityfilter) is explicitly set to true on a component.

Does not remove filters on already drawn components, or which are applied via CSS.

See [IEFilters](../kb_topics/IEFilters.md#kb-topic-internet-explorer-filter-effects) for background.

### Groups

- IEFilters

**Flags**: IR

---
## ClassAttr: Canvas.COPY

### Description
A declared value of the enum type [DragDataAction](../reference.md#type-dragdataaction).

**Flags**: R

---
## ClassAttr: Canvas.VISIBLE

### Description
A declared value of the enum type s [Overflow](../reference.md#type-overflow) and [Visibility](../reference_2.md#type-visibility).

**Flags**: R

---
## ClassAttr: Canvas.TILE

### Description
A declared value of the enum type [ImageStyle](../reference.md#type-imagestyle).

**Flags**: R

---
## Attr: Canvas.locatePeersType

### Description
[LocatorTypeStrategy](../reference.md#type-locatortypestrategy) to use when finding peers of this canvas.

### Groups

- autoTest

**Flags**: IRWA

---
## Attr: Canvas.maxHeight

### Description
Maximum height available to this Canvas. See [Canvas.maxWidth](#attr-canvasmaxwidth) for details of behavior.

### Groups

- sizing

### See Also

- [Canvas.dragMaxHeight](#attr-canvasdragmaxheight)

**Flags**: IRWA

---
## Attr: Canvas.dropTarget

### Description
Delegates a different widget that should actually be dropped on if the cursor is over this widget when the drop completes. If you're building your own "drop indicator" widget, it may need this property set to the main canvas (receiving the drop) to avoid itself being considered a drop target (causing the indicator to flicker).

### Groups

- dragdrop

### See Also

- [EventHandler.getDragTarget](EventHandler.md#classmethod-eventhandlergetdragtarget)
- [Canvas.dragTarget](#attr-canvasdragtarget)

**Flags**: IRWA

---
## Attr: Canvas.resizeBarTarget

### Description
When this Canvas is included as a member in a Layout, and [Canvas.showResizeBar](#attr-canvasshowresizebar) is set to `true` so that a resizeBar is created, `resizeBarTarget:"next"` can be set to indicate that the resizeBar should resize the next member of the layout rather than this one. For resizeBars that support hiding their target member when clicked on, `resizeBarTarget:"next"` also means that the next member will be the one hidden.

This is typically used to create a 3-way split pane, where left and right-hand sections can be resized or hidden to allow a center section to expand.

**NOTE:** as with any Layout, to ensure all available space is used, one or more members must maintain a flexible size (eg 75%, or \*). In a two pane Layout with a normal resize bar, to fill all space after a user resizes, the member on the **right** should have flexible size. With resizeBarTarget:"next", the member on the **left** should have flexible size.

### Groups

- layoutMember

### See Also

- [Canvas.showResizeBar](#attr-canvasshowresizebar)

**Flags**: IR

---
## Attr: Canvas.editNode

### Description
The component's [EditNode](../reference.md#object-editnode) for a component that has been created by a [Palette](../reference.md#interface-palette) from a [PaletteNode](../reference.md#object-palettenode).

**Flags**: R

---
## Attr: Canvas.autoDraw

### Description
If true, this canvas will draw itself immediately after it is created.

**Note** that you should turn this OFF for any canvases that are provided as children of other canvases, or they will draw initially, then be clear()ed and drawn again when added as children, causing a large performance penalty.

For example, the following code is incorrect and will cause extra draw()s:

```
     isc.Layout.create({
         members : [
             isc.ListGrid.create()
         ]
     });
 
```
It should instead be:
```
     isc.Layout.create({
         members : [
             isc.ListGrid.create({ autoDraw: false })
         ]
     });
 
```
In order to avoid unwanted autoDrawing systematically, it is recommend that you call [isc.setAutoDraw(false)](isc.md#staticmethod-iscsetautodraw) immediately after SmartClient is loaded and before any components are created, then set `autoDraw:true` or call draw() explicitly to draw components.

Otherwise, if the global setting for autoDraw remains `true`, you must set autoDraw:false, as shown above, on every component in your application that should not immediately draw: all Canvas children, Layout members, Window items, Tab panes, etc, however deeply nested. Forgetting to set autoDraw:false will result in one more clear()s - these are reported on the Results tab of the [Developer Console](../kb_topics/debugging.md#kb-topic-debugging), and can be tracked to individual components by using the "clears" log category in the Developer Console.

### Groups

- drawing

**Flags**: IR

---
## Attr: Canvas.proportionalResizing

### Description
If [Canvas.canDragResize](#attr-canvascandragresize) is true, this property specifies the conditions for when proportional resizing is used. The default is "none" , which means that proportional resizing is disabled.

### Groups

- dragdrop

### See Also

- [Canvas.proportionalResizeModifiers](#attr-canvasproportionalresizemodifiers)

**Flags**: IR

---
## Attr: Canvas.autoShowParent

### Description
If set to true, the widget's parent (if any) will automatically be shown whenever the widget is shown.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: Canvas.edgeSize

### Description
Size in pixels for corners and edges

### Groups

- imageEdges

**Flags**: IR

---
## Attr: Canvas.htmlElement

### Description
If specified as a pointer to an HTML element present in the DOM, this canvas will be rendered inside that element on [draw()](#method-canvasdraw). If provided as a String, the String will be replaced by a DOM node as returned from document.getElementById(htmlElement) on initialization.

_NOTES:_  
This feature is intended for integration with other JavaScript frameworks and legacy page architectures only; the native browser's reaction to DOM insertion is unspecified and unsupported. For consistent cross-browser layout and positioning semantics, use Canvas parents (especially Layouts) and use absolute positioning at top level.

In some cases, the target element may need a specified height to be rendered correctly. In this cases, you can expect to find a message like the following in the JavaScript console: "isc\_DataView\_0:can't resize to height: 0; clamping to 1 \[enable 'sizing' log for stack trace\]"

Persistence of htmlElement: If [Canvas.htmlPosition](#attr-canvashtmlposition) is set to `"replace"` the htmlElement will be removed from the DOM when the canvas is drawn - therefore the htmlElement attribute will be cleared at this time. Otherwise if a Canvas is clear()d and then draw()n again it will be rendered inside the same htmlElement.  
If a Canvas is added as a child to Canvas parent, its htmlElement will be dropped.

[Canvas.position](#attr-canvasposition) should typically be set to `"relative"` if the widget is to be rendered inline within a standard page.

### Groups

- htmlElement
- positioning

**Flags**: IRWA

---
## Attr: Canvas.animateScrollTime

### Description
Default time for performing an animated scroll. If unset, `this.animateTime` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.leavePageSpace

### Description
If set, overrides the global [Canvas.defaultPageSpace](#classattr-canvasdefaultpagespace).

### Groups

- positioning

**Flags**: IRWA

---
## Attr: Canvas.isGroup

### Description
Should a grouping frame be shown around this canvas if a non-empty string has been specified for [Canvas.groupTitle](#attr-canvasgrouptitle).

### Groups

- appearance

### See Also

- [Canvas.groupBorderCSS](#attr-canvasgroupbordercss)
- [Canvas.groupLabelStyleName](#attr-canvasgrouplabelstylename)
- [Canvas.groupLabelBackgroundColor](#attr-canvasgrouplabelbackgroundcolor)

**Flags**: IR

---
## Attr: Canvas.shadowSoftness

### Description
Softness, or degree of blurring, of the shadow.

A shadow with `softness:x` is 2x pixels larger in each direction than the element throwing the shadow, and the media for each edge should be x pixels wide/tall.

Defaults to `shadowDepth` if unset.

### Groups

- shadow

**Flags**: IRWA

---
## Attr: Canvas.hoverHeight

### Description
If `this.showHover` is true, this property can be used to customize the height of the hover canvas shown.

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.isSnapAlignCandidate

### Description
Flag to disable snapping to alignment against this Canvas when _other_ Canvases dragged into the same parent when [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign) is enabled on this Canvas' parent.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.hoverMoveWithMouse

### Description
If `this.showHover` is true, should this widget's hover canvas be moved with the mouse while visible?

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.keepInParentRect

### Description
Constrains drag-resizing and drag-repositioning of this canvas to either the rect of its parent (if set to true) or an arbitrary rect based on its parent (if set to a \[Left,Top,Width,Height\] rect array). In the latter mode you may use negative offsets for left/top and a width/height greater than the visible or scroll width of the parent to allow positioning beyond the confines of the parent.

If this canvas has no parent, constrains dragging to within the browser window.

Affects target and outline dragAppearance, not tracker.

Note: keepInParentRect affects only user drag interactions, not programmatic moves.

Example use cases:  
`keepInParentRect: true` - confine to parent  
`keepInParentRect: [0, 0, 500, 500]` - confine to top left 500x500 region within parent  
`keepInParentRect: [0, 0, 10000, 10000]` - in combination with overflow: "auto", confine to parent, but allow moving off the right and bottom of the parent to force scrolling (and hence enlarge the scrollWidth of the parent).

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.opacity

### Description
Renders the widget to be partly transparent. A widget's opacity property may be set to any number between 0 (transparent) to 100 (opaque). Null means don't specify opacity directly, 100 is fully opaque. Note that heavy use of opacity may have a performance impact on some older browsers.

In older versions of Internet Explorer (Pre IE9 / HTML5), opacity is achieved through proprietary filters. If [filters have been disabled](#classattr-canvasneverusefilters) within this application developers must set [Canvas.useOpacityFilter](#attr-canvasuseopacityfilter) to true for specific components on which opacity support is required.

Also note that opacity is incompatible with [backMasks](#attr-canvasusebackmask).

### Groups

- cues

**Flags**: IRWA

---
## Attr: Canvas.updateTabPositionOnReparent

### Description
Should canvases with a [parent canvas](#method-canvasgetparentcanvas) be added to the TabIndexManager under the parent as described in [Canvas.updateChildTabPositions](#method-canvasupdatechildtabpositions) and [Canvas.updateChildTabPosition](#method-canvasupdatechildtabposition)?

If set to false, the tab-position will not be modified on parent change.

This property is useful for cases where the tab position of a widget will be managed by something other than the parent canvas, for example for [canvasItem canvases](CanvasItem.md#attr-canvasitemcanvas).

**Flags**: IRWA

---
## Attr: Canvas.canFocus

### Description
Can this widget be allowed to become the target of keyboard events?

If canFocus is unset (the default), only scrollable widgets with visible scrollbars are focusable, to allow for keyboard scrolling.

A widget normally receives focus by being clicked on or tabbed to.

### Groups

- focus
- events

**Flags**: IRWA

---
## Attr: Canvas.testDataContext

### Description
A [DataContext](../reference.md#object-datacontext) to be used if no [Canvas.dataContext](#attr-canvasdatacontext) is provided (directly or indirectly via a parent). If a DataContext is provided it completely replaces the `testDataContext`.

DataSources included in the `testDataContext` are immediately provided to [rule context](#attr-canvasrulescope) when used if no other component has done so already. These records are found in rule context 'dataContext' section (ex. `dataContext.Customer` for a Customer record in `testDataContext`) so they do not conflict with normal DataSource records.

### Groups

- dataContext

### See Also

- [DataContext](../reference.md#object-datacontext)

**Flags**: IR

---
## Attr: Canvas.mouseStillDownInitialDelay

### Description
Amount of time (in milliseconds) before mouseStillDown events start to be fired repeatedly for this canvas. See [Canvas.mouseStillDown](#method-canvasmousestilldown) for details.

### Groups

- events

**Flags**: IRWA

---
## Attr: Canvas.skinImgDir

### Description
Default directory for skin images (those defined by the class), relative to the Page-wide [skinDir](Page.md#classmethod-pagegetskindir).

### Groups

- images

**Flags**: IRWA

---
## Attr: Canvas.animateMoveAcceleration

### Description
Default acceleration effect for performing an animated move. If unset, `this.animateAcceleration` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.shadowVOffset

### Description
Vertical offset for the [shadow](#attr-canvasshowshadow). Takes precedence over [Canvas.shadowOffset](#attr-canvasshadowoffset) if set. Has no effect if [css-shadows](#attr-canvasusecssshadow) are not being used for this canvas.

### Groups

- shadow

**Flags**: IRWA

---
## Attr: Canvas.useOpacityFilter

### Description
Configures where the Opacity filter is used for IE6-8.

With the default of null, opacity filters are used unless [Canvas.neverUseFilters](#classattr-canvasneverusefilters) has been set. When set explicitly to true, opacity filters are used even if `neverUseFilters` is true.

See [IEFilters](../kb_topics/IEFilters.md#kb-topic-internet-explorer-filter-effects) for background.

### Groups

- IEFilters

**Flags**: IR

---
## Attr: Canvas.hoverDelay

### Description
If `this.canHover` is true, how long should the mouse be kept over this widget before the hover event is fired

### Groups

- hovers

### See Also

- [Canvas.canHover](#attr-canvascanhover)
- [Canvas.hover](#method-canvashover)

**Flags**: IRW

---
## Attr: Canvas.dragResizeAppearance

### Description
If [Canvas.canDragResize](#attr-canvascandragresize) is true, this attribute specifies the visual appearance to show during drag resize. If unset [Canvas.dragAppearance](#attr-canvasdragappearance) will be used.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.hideUsingDisplayNone

### Description
When this widget is hidden (see [Canvas.visibility](#attr-canvasvisibility) and [Canvas.hide](#method-canvashide)), should display:none be applied to the [outer element](#method-canvasgetouterelement)?

This setting is not supported for general use, but in certain cases, it has been shown that display:none is a work-around for browser bugs involving burn-through of iframes or plugins, where the content of the iframe or plugin may still be visible despite the containing widget being hidden.

### Groups

- appearance

### See Also

- [Visibility](../reference_2.md#type-visibility)

**Flags**: IRA

---
## Attr: Canvas.left

### Description
Number of pixels the left side of the widget is offset to the right from its default drawing context (either its parent's topleft corner, or the document flow, depending on the value of the [Canvas.position](#attr-canvasposition) property).

Can also be set as a percentage, specified as a String ending in '%', eg, "50%". In this case the top coordinate is considered as a percentage of the specified width of the [parent](#method-canvasgetparentcanvas).

### Groups

- positioning

**Flags**: IRW

---
## Attr: Canvas.childrenResizeSnapAlign

### Description
Flag to disable snapping to alignment when children of this Canvas are resized

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.shadowOffset

### Description
Offset of the shadow. Defaults to half of `shadowDepth` if unset.

Because of the blurred edges, a shadow is larger than the originating component by 2xsoftness. An `shadowOffset` of 0 means that the shadow will extend around the originating component equally in all directions.

If [css shadows](#attr-canvasusecssshadow) are being used, separate vertical and horizontal offsets may be specified via [Canvas.shadowHOffset](#attr-canvasshadowhoffset) and [Canvas.shadowVOffset](#attr-canvasshadowvoffset).

### Groups

- shadow

**Flags**: IRWA

---
## Attr: Canvas.isRuleScope

### Description
Marks this Canvas as the [Canvas.ruleScope](#attr-canvasrulescope) that will be discovered by any contained [DataBoundComponent](../reference.md#interface-databoundcomponent)s which do not specify an explicit `ruleScope`.

**Flags**: IR

---
## Attr: Canvas.canDragReposition

### Description
Indicates whether this widget can be moved by a user of your application by simply dragging with the mouse.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.dragRepositionAppearance

### Description
If [Canvas.canDragReposition](#attr-canvascandragreposition) is true, this attribute specifies the visual appearance to show during drag reposition. If unset [Canvas.dragAppearance](#attr-canvasdragappearance) will be used.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.childrenSnapResizeToGrid

### Description
If true, causes this canvas's children to snap to its grid when resizing. This behavior can be overridden on a per-child basis by setting the [snapToGrid](#attr-canvassnaptogrid) or [snapResizeToGrid](#attr-canvassnapresizetogrid) value on the child.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.shadowHOffset

### Description
Horizontal offset for the [shadow](#attr-canvasshowshadow). Takes precedence over [Canvas.shadowOffset](#attr-canvasshadowoffset) if set. Has no effect if [css-shadows](#attr-canvasusecssshadow) are not being used for this canvas.

### Groups

- shadow

**Flags**: IRWA

---
## Attr: Canvas.dragMinHeight

### Description
Minimum height that this Canvas can be resized to by a user. See [Canvas.dragMinWidth](#attr-canvasdragminwidth) for details of behavior.

### Groups

- sizing

### See Also

- [Canvas.minHeight](#attr-canvasminheight)

**Flags**: IRWA

---
## Attr: Canvas.padding

### Description
Set the CSS padding of this component, in pixels. Padding provides space between the border and the component's contents.

This property sets the same thickness of padding on every side. Differing per-side padding can be set in a CSS style and applied via [Canvas.styleName](#attr-canvasstylename).

Note that CSS padding does not affect the placement of [Canvas.children](#attr-canvaschildren). To provide a blank area around children, either use [CSS margins](#attr-canvasmargin) or use a [Layout](Layout.md#class-layout) as the parent instead, and use properties such as [Layout.layoutMargin](Layout.md#attr-layoutlayoutmargin) to create blank space.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.enableWhen

### Description
Criteria to be evaluated to determine whether this Canvas should be enabled. Re-evaluated whenever data in the [Canvas.ruleScope](#attr-canvasrulescope) changes.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

### Groups

- ruleCriteria

**Flags**: IR

---
## Attr: Canvas.animateResizeAcceleration

### Description
Default acceleration function for performing an animated resize. If unset, `this.animateAcceleration` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.useTouchScrolling

### Description
On [touch devices](Browser.md#classattr-browseristouch), if this `Canvas` can be scrolled, should touch-dragging the content area result in scrolling? Set to `false` if touch-dragging should not cause scrolling. Note that setting to `false` enables the use of [custom scrollbars](#attr-canvasshowcustomscrollbars) on touch devices.

`useTouchScrolling` can default to `false` if [disableTouchScrollingForDrag](#attr-canvasdisabletouchscrollingfordrag) is `true` and various built-in drag operations are enabled that normally interfere with touch scrolling (e.g. [ListGrid.canDragSelect](ListGrid_1.md#attr-listgridcandragselect) and [ListGrid.canReorderRecords](ListGrid_1.md#attr-listgridcanreorderrecords)).

When touch scrolling is disabled, it can be difficult to interact with parts of the custom scrollbars at their default size of 16 pixels. In touch browsers, any touch 8px before the thumb of a [custom scrollbar](Scrollbar.md#class-scrollbar) will be mapped to the thumb, but the other parts of the scrollbar do not have a similar tolerance applied. The width of the custom scrollbars can be increased by setting the [Canvas.scrollbarSize](#attr-canvasscrollbarsize) to a larger value, but note that when [spriting is enabled](../kb_topics/skinning.md#kb-topic-skinning--theming), changing the `scrollbarSize` may cause tiling of certain images and backgrounds that make up the custom scrollbar. This can be fixed for a component by creating it with [Canvas.scrollbarConstructor](#attr-canvasscrollbarconstructor) set to "Scrollbar"—a basic scrollbar class that does not employ spriting.

### Groups

- scrolling

**Flags**: IRA

---
## Attr: Canvas.dragMaxWidth

### Description
Maximum width that this Canvas can be resized to by a user. Actual limit will be minimum of `dragMaxWidth` and [Canvas.maxWidth](#attr-canvasmaxwidth).

### Groups

- sizing

**Flags**: IRWA

---
## Attr: Canvas.dragStartDistance

### Description
Number of pixels the cursor needs to move before the EventHandler starts a drag operation.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.matchElement

### Description
If [Canvas.htmlElement](#attr-canvashtmlelement) is specified, should this canvas be drawn at the same dimensions as the htmlElement?  
See also [Canvas.matchElementWidth](#attr-canvasmatchelementwidth) and [Canvas.matchElementHeight](#attr-canvasmatchelementheight)

By default, if [Canvas.htmlPosition](#attr-canvashtmlposition) is anything other than `"replace"`, setting this property will cause the canvas resize with the element if the element itself subsequently resizes (for example due to page reflow).

To disable this behavior for backwards compatibility or other reasons, use [Canvas.persistentMatchElement](#attr-canvaspersistentmatchelement)

**Flags**: IRWA

---
## Attr: Canvas.leaveGroupLabelSpace

### Description
When showing this widget in a [group](#attr-canvasisgroup), should any content be shifted down so that the group-label doesn't sit in front of it?

### Groups

- appearance

**Flags**: IR

---
## Attr: Canvas.canDragResize

### Description
Indicates whether this widget can be resized by dragging on the edges and/or corners of the widget with the mouse.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.position

### Description
Absolute or relative, corresponding to the "absolute" (with respect to parent) or "relative" (with respect to document flow) values for the CSS position attribute.

Setting `position:"relative"` enables SmartClient components to be embedded directly into the native HTML flow of a page, causing the component to be rendered within an existing DOM structure. This attribute should only be set to `"relative"` on a top level component (a component with no [Canvas.getParentCanvas](#method-canvasgetparentcanvas)).

There are 2 ways to embed relatively positioned canvases in the DOM - by default the component will be written out inline when it gets [drawn()n](#method-canvasdraw). For example to embed a canvas in an HTML table you could use this code:

```
 <table>
   <tr>
     <td>
       <script>
         isc.Canvas.create({autoDraw:true, backgroundColor:"red", position:"relative"});
       </script>
     <td>
   </tr>
 </table>
 
```
Alternatively you can make use of the [Canvas.htmlElement](#attr-canvashtmlelement) attribute.

Relative positioning is intended as a short-term integration scenario while incrementally upgrading existing applications. Note that relative positioning is not used to manage layout within SmartClient components - instead the [Layout](Layout.md#class-layout) class would typically be used. For best consistency and flexibility across browsers, all SmartClient layout managers use absolute positioning.

For canvases with a specified [Canvas.htmlElement](#attr-canvashtmlelement), this attribute defaults to `"relative"`. In all other cases the default value will be `"absolute"`. Note that if you plan to call [Canvas.setHtmlElement](#method-canvassethtmlelement) after init, you will need to set this value to "relative" explicitly.

### Groups

- positioning

**Flags**: IRWA

---
## Attr: Canvas.edgeCursorMap

### Description
Cursor to use when over each edge of a Canvas that is drag resizable.

To disable drag resize cursors, set the edgeCursorMap property to null.

### Groups

- dragdrop

### See Also

- [Canvas.resizeFrom](#attr-canvasresizefrom)

**Flags**: IRWA

---
## Attr: Canvas.animateMoveTime

### Description
Default time for performing an animated move. If unset, `this.animateTime` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.layoutAlign

### Description
When this Canvas is included as a member in a Layout, layoutAlign controls alignment on the breadth axis of the layout. Default is "left" for a VLayout, "top" for an HLayout.

### Groups

- layoutMember

**Flags**: IRW

---
## Attr: Canvas.groupPadding

### Description
Padding to apply inside the border when this canvas is showing a group [border and label](#attr-canvasisgroup).

### Groups

- appearance

### See Also

- [Canvas.isGroup](#attr-canvasisgroup)

**Flags**: IR

---
## Attr: Canvas.height

### Description
The `canvas.width` attribute specifies the size for a component's horizontal dimension; `canvas.height` specifies the size for the vertical dimension.

May be set to an integer value (a number of pixels), a percentage value like "50%", or "\*".

See [percentSizing](../kb_topics/percentSizing.md#kb-topic-canvas-percentage-sizing) for details on how percentage or `"*"` values are resolved actual size.

If [overflow](#attr-canvasoverflow) is set to "visible", the specified size acts as a minimum, and the component may overflow to show all content and/or children.

Note that developers wishing to set a default width or height for a component class should set [defaultWidth](#attr-canvasdefaultwidth) or [Canvas.defaultHeight](#attr-canvasdefaultheight) instead of specifying an explicit default `width` or `height`. This is important for components added to a [Layout](Layout.md#class-layout) as members - it allows the Layout to determine whether the canvas has an explicitly specified size that must be respected, or whether it can participate in its [sizing policies](../reference_2.md#type-layoutpolicy).

### Groups

- sizing

**Flags**: IRW

---
## Attr: Canvas.animateShowEffect

### Description
Default animation effect to use if [Canvas.animateShow](#method-canvasanimateshow) is called without an explicit `effect` parameter

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.disabledCursor

### Description
Specifies the cursor image to display when the mouse pointer is over this widget if this widget is disabled. It corresponds to the CSS cursor attribute. See Cursor type for different cursors.

### Groups

- cues

**Flags**: IRWA

---
## Attr: Canvas.parentCanvas

### Description
This Canvas's immediate parent, if any.  
Can be initialized, but any subsequent manipulation should be via [addChild()](#method-canvasaddchild) and [removeChild()](#method-canvasremovechild) calls on the parent. The parent Canvas should be fetched using [getParentCanvas()](#method-canvasgetparentcanvas).

See [containment](../kb_topics/containment.md#kb-topic-component-containment-and-hierarchy) for an overview of parent/child relationships.

### Groups

- containment

**Flags**: IR

---
## Attr: Canvas.animateRectTime

### Description
Default time for performing an animated setRect. If unset, `this.animateTime` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.animateHideTime

### Description
Default time for performing an animated hide. If unset, `this.animateTime` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.menuConstructor

### Description
Default class used to construct menus created by this component, including context menus.

### Groups

- cues

### See Also

- [Canvas.showContextMenu](#method-canvasshowcontextmenu)

**Flags**: IR

---
## Attr: Canvas.contextMenu

### Description
Context menu to show for this object, an instance of the Menu widget.

Note: if [Canvas.destroy](#method-canvasdestroy) is called on a canvas, any specified context menu is not automatically destroyed as well. This is in contrast to [MenuButton](MenuButton.md#class-menubutton)s which automatically destroy their specified [MenuButton.menu](MenuButton.md#attr-menubuttonmenu) by default. The behavior is intentional as context menus are commonly reused across components.

### Groups

- cues

### See Also

- [Canvas.showContextMenu](#method-canvasshowcontextmenu)

**Flags**: IRWA

---
## Attr: Canvas.shadowColor

### Description
Color for the css-based drop shadow shown if [Canvas.useCSSShadow](#attr-canvasusecssshadow) is true and [Canvas.showShadow](#attr-canvasshowshadow) is true.

Has no effect if we are not using css-based shadows - in that case, use [Canvas.shadowImage](#attr-canvasshadowimage) instead.

### Groups

- shadow

**Flags**: IRWA

---
## Attr: Canvas.groupTitle

### Description
The title/label for the grouping. Only applicable when [isGroup](#attr-canvasisgroup) is set to true. No [grouping frame](#attr-canvasisgroup) or title/label will be shown unless this property is a non-empty string.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.forwardSVGeventsToObject

### Description
If true, events sent to the SVG inside an object tag are forwarded to the object itself by Framework handlers. If false, "pointer-events:none" CSS is set on the object so that events are directly sent to the object by the browser, if supported.

The advantage of forwarding events is that it allows hover CSS or any other event-driven logic on the SVG to work as expected. If "pointer-events:none" is written out, no GUI interaction will trigger events in the SVG, including hover CSS. The disadvantage is that only a few critical events are forwarded, such as "mouseDown", "mouseMove", and "mouseUp" for non-touch platforms, and "click" for touch platforms. Other events will be delivered to the SVG, but not forwarded up to the parent document/object tag.

### Groups

- images

### See Also

- [EventHandler](EventHandler.md#class-eventhandler)
- [Canvas.useImageForSVG](#attr-canvasuseimageforsvg)

**Flags**: IRA

---
## Attr: Canvas.groupBorderCSS

### Description
Sets the style for the grouping frame around the canvas. Only necessary when showing a [grouping frame](#attr-canvasisgroup).

### Groups

- appearance

**Flags**: IR

---
## Attr: Canvas.redrawOnResize

### Description
Should this element be redrawn in response to a resize?

Should be set to true for components whose [inner HTML](#method-canvasgetinnerhtml) will not automatically reflow to fit the component's new size.

### Groups

- drawing

**Flags**: IRWA

---
## Attr: Canvas.shadowDepth

### Description
Depth of the shadow, or the virtual height above the page of the widget throwing the shadow.

This is a single parameter that can be used to control both `shadowSoftness` and `shadowOffset`.

### Groups

- shadow

**Flags**: IR

---
## Attr: Canvas.backgroundColor

### Description
The background color for this widget. It corresponds to the CSS background-color attribute. You can set this property to an RGB value (e.g. #22AAFF) or a named color (e.g. red) from a list of browser supported color names.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.border

### Description
Set the CSS border of this component, as a CSS string including border-width, border-style, and/or color (eg "2px solid blue").

This property applies the same border to all four sides of this component. Different per-side borders can be set in a CSS style and applied via [Canvas.styleName](#attr-canvasstylename).

If a [grouping frame](#attr-canvasisgroup) is being shown then border is derived from the [Canvas.groupBorderCSS](#attr-canvasgroupbordercss) attribute, not from the explicit border property.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.snapAlignCenterLineStyle

### Description
CSS border declaration used for the line shown to indicate snapping to a center line when [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign) is set.

### Groups

- snapGridDragging

**Flags**: IR

---
## Attr: Canvas.mouseStillDownDelay

### Description
Amount of time (in milliseconds) between repeated 'mouseStillDown' events for this canvas. See [Canvas.mouseStillDown](#method-canvasmousestilldown) for details.

### Groups

- events

**Flags**: IRWA

---
## Attr: Canvas.dragOpacity

### Description
If this widget has dragAppearance `"target"`, this value specifies the opacity to render the target while it is being dragged. A null value implies we do not modify the opacity.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.backgroundPosition

### Description
Specifies how the background image should be positioned on the widget. It corresponds to the CSS background-position attribute. If unset, no background-position attribute is specified if a background image is specified.

### Groups

- appearance

**Flags**: IR

---
## Attr: Canvas.autoPopulateData

### Description
If a [Canvas.dataContext](#attr-canvasdatacontext) is provided, should subcomponents automatically bind to the data?

In general, if you provide a [primaryKey](DataSourceField.md#attr-datasourcefieldprimarykey) value for a record, that specific record will be shown or edited, or have its related records loaded. If you provide other field values _without the primaryKey value_, those values will be treated as either criteria (for a grid) or as initial values (for a form).

Components will respond to `dataContext` differently depending on whether they typically work with just a single record (such as [form](DynamicForm.md#class-dynamicform) or a [DetailViewer](DetailViewer.md#class-detailviewer)), or whether they usually work with lists of records (such as [ListGrid](ListGrid_1.md#class-listgrid) or [TileGrid](TileGrid.md#class-tilegrid), which have [component.dataArity](DataBoundComponent.md#attr-databoundcomponentdataarity) set to `multipe` by default).

Specifically, the following rules are used:

1.  for a singular component (eg forms, detailViewers):
    *   if only the PK (primary key) value is provided, the component will fetch the singular record and display or edit it
    *   if the PK is provided _along with other values_, the component will assume it has a complete record, and display or edit it
    *   if only non-PK values are provided, the component will assume these are initial values
2.  for a multiple component (eg listGrid, tileGrid):
    *   if only non-PK values are provided, the component will use these as criteria. For example, a grid bound to an _Orders_ DataSource with `dataContext` of Status:"In Process" would fetch records with that status
    *   if the PK is provided, and the component's DataSource is _related_ to one of the DataSources in the `dataContext`, related records will be fetched, using the PK value (similarly to if [fetchRelatedData()](ListGrid_2.md#method-listgridfetchrelateddata) had been called. For example, if an _orderNumber_ value was provided, a grid bound to _OrderDetail_ would fetch line items for that _orderNumber_.
    *   if an array of multiple records is provided, that data is used as if setData() had been called on the component

If any of these behaviors is not desired, you can just set `autoPopulateData` to false on the specific component that should not be auto-populated.

Specific examples, using the _Order_ and _OrderDetail_ sample DataSources, where _OrderDetail_ records are associated (many-to-1) with _Order_ records, and the PK of _Order_ is _orderNumber_:

1.  a form or DetailViewer bound to _Order_ and a ListGrid bound to _OrderDetail_:
    
    *   if an _orderNumber_ is provided, the form or DetailViewer would show that order, and the grid would show related _OrderDetail_ records
    *   if **only** _orderNumber_ is provided (no additional fields), the full _Order_ record is automatically fetched for the form or DetailViewer
    
    This fulfills a common use case of viewing or editing an _Order_ and its related _OrderDetail_ records.
    
2.  a grid bound to _Order_ and a second grid bound to _OrderDetail_
    
    *   if values such as _orderStatus_ : "On Hold" were provided, the _Order_ grid uses those as criteria
    *   the _OrderDetail_ grid does nothing
    
    This fulfills a common use case of viewing _Order_ records that match certain criteria. The _OrderDetail_ grid would generally be populated only by an event handler installed on the _Order_ grid, which would call [fetchRelatedData](ListGrid_2.md#method-listgridfetchrelateddata).
    
3.  a grid and form both bound to _Order_
    
    *   if values such as _orderStatus_ : "On Hold" were provided, the _Order_ grid uses those as criteria, and the form uses those as initial values
    
    This fulfills two possible use cases:
    
    *   the form is a SearchForm for searching the grid, so it should show the same criteria as are applied to the grid
    *   the form is for editing the selected record in the grid, or adding new ones. It is ready to either add a new record, or for the user to select a record to show in the form, typically via logic added to the grid (e.g. [recordClick](ListGrid_2.md#method-listgridrecordclick) -> [form.editSelectedData()](DynamicForm.md#method-dynamicformeditselecteddata).

By default, `autoPopulateData` is true for any component that is contained with a "screen" [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen) and false for any component that is an [AutoChild](../reference.md#type-autochild).

Note that, if there is a non-DBC in your screen that wants to access fields in the expected dataContext, the DynamicProperty can refer to properties that auto-populated DBCs will place into the ruleContext. For example, with a DynamicForm "itemEditor" bound to "supplyItem", a header above could use itemEditor.values.itemName to display the name of the item. The header will then show the expected value as soon as the DynamicForm is auto-populated.

Similarly, the [DataView.drawn()](#method-canvasdrawn) StringMethod fires after auto-population has occurred, so any startup actions in a screen will likewise be able to utilize data from the `dataContext` by just referring to it via `ruleScope`.

### Groups

- dataContext

**Flags**: IR

---
## Attr: Canvas.destroyed

### Description
If this property is set to `true`, the [destroy()](#method-canvasdestroy) method has been called on this canvas. This implies the canvas is no longer valid. Its ID has been removed from global scope, and calling standard canvas APIs on it is likely to result in errors.

### See Also

- [Canvas.destroy](#method-canvasdestroy)

**Flags**: RA

---
## Attr: Canvas.dropTypes

### Description
When a drag and drop interaction occurs, if a [dragType](#attr-canvasdragtype) is configured on the source widget, it is compared to the `dropTypes` configured on the target widget, and a drop is only allowed if the `dragType` is listed in the target widget's `dropTypes` array.

The default setting means any `dragType` is eligible for dropping on this widget, including no `dragType` setting.

See also [Canvas.willAcceptDrop](#method-canvaswillacceptdrop) for dynamic determination of drop eligibility.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.showHoverComponents

### Description
When set to true, shows a widget hovering at the mouse point instead of the builtin hover label. Override [getHoverComponent](#method-canvasgethovercomponent) to provide the Canvas to show as the hoverComponent.

### Groups

- hoverComponents

**Flags**: IRWA

---
## Attr: Canvas.accessKey

### Description
If specified this governs the HTML accessKey for the widget.

This should be set to a character - when a user hits the html accessKey modifier for the browser, plus this character, focus will be given to the widget in question. The accessKey modifier can vary by browser and platform.

The following list of default behavior is for reference only, developers should also consult browser documentation for additional information.

*   **Internet Explorer (all platforms)**: `Alt` + _accessKey_
*   **Mozilla Firefox (Windows, Unix)**: `Alt+Shift` + _accessKey_
*   **Mozilla Firefox (Mac)**: `Ctrl+Opt` + _accessKey_
*   **Chrome and Safari (Windows, Unix)**: `Alt` + _accessKey_
*   **Chrome and Safari (Mac)**: `Ctrl+Opt` + _accessKey_

### Groups

- focus

**Flags**: IRWA

---
## Attr: Canvas.dataContext

### Description
A mapping from [DataSource](DataSource.md#class-datasource) IDs to specific [Records](../reference.md#object-record) from those DataSources, that [DataBoundComponents](../reference.md#interface-databoundcomponent) contained within this Canvas should automatically bind to if a DataSource is provided but data is not provided (directly or indirectly, for example, indirectly via setting [ListGrid.autoFetchData](ListGrid_1.md#attr-listgridautofetchdata).

See [Canvas.autoPopulateData](#attr-canvasautopopulatedata) for details on how this is done.

DataSources included in the `dataContext` are immediately provided to [rule context](#attr-canvasrulescope) when used if no other component has done so already. These records are found in rule context 'dataContext' section (ex. `dataContext.Customer` for a Customer record in `dataContext`) so they do not conflict with normal DataSource records.

### Groups

- dataContext

**Flags**: IWR

---
## Attr: Canvas.receiveScrollbarEvents

### Description
Whether this canvas should receive [events](../reference.md#kb-topic-eventhandling) from its scrollbars, which are [peers](#attr-canvaspeers). Normally, a canvas only gets bubbled events from its [children](#attr-canvaschildren).

Note that this property only has an impact if [Canvas.showCustomScrollbars](#attr-canvasshowcustomscrollbars) is true.

### Groups

- scrolling

### See Also

- [Canvas.showCustomScrollbars](#attr-canvasshowcustomscrollbars)

**Flags**: IR

---
## Attr: Canvas.snapAxis

### Description
Describes which axes to apply snap-to-grid to. Valid values are "horizontal", "vertical" or "both".

### Groups

- snapGridDragging

### See Also

- [Canvas.snapToGrid](#attr-canvassnaptogrid)
- [Canvas.snapResizeToGrid](#attr-canvassnapresizetogrid)
- [Canvas.childrenSnapToGrid](#attr-canvaschildrensnaptogrid)
- [Canvas.childrenSnapResizeToGrid](#attr-canvaschildrensnapresizetogrid)

**Flags**: IRW

---
## Attr: Canvas.childrenSnapToGrid

### Description
If true, causes this canvas's children to snap to its grid when dragging. This behavior can be overridden on a per-child basis by setting the [snapToGrid](#attr-canvassnaptogrid) value on the child.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.canDropBefore

### Description
When explicitly set to false, disallows drop before this member in the Layout.

### Groups

- layoutMember

### See Also

- [Layout](Layout.md#class-layout)

**Flags**: IRWA

---
## Attr: Canvas.valuesManager

### Description
[ValuesManager](ValuesManager.md#class-valuesmanager) for managing values displayed in this component. If specified at initialization time, this component will be added to the valuesManager via [ValuesManager.addMember](ValuesManager.md#method-valuesmanageraddmember).

ValuesManagers allow different fields of a single object to be displayed or edited across multiple UI components. Given a single values object, a valuesManager will handle determining the appropriate field values for its member components and displaying them / responding to edits if the components support this.

Data may be derived simply from the specified fieldNames within the member components, or for complex nested data structures can be specified by both component and field-level [DataPath](../reference_2.md#type-datapath).

Note that components may be automatically bound to an existing valuesManager attached to a parent component if dataPath is specified. See [Canvas.dataPath](#attr-canvasdatapath) for more information. Also note that if a databound component has a specified dataSource and dataPath but no specified valuesManager object one will be automatically generated as part of the databinding process

**Flags**: IRWA

---
## Attr: Canvas.scrollbarConstructor

### Description
The class that will be used to create custom scrollbars for this component. Set this attribute to a Scrollbar subclass with e.g. a different skinImgDir, to customize scrollbar appearance for this component only.

When [spriting is enabled](../kb_topics/skinning.md#kb-topic-skinning--theming) and supported by the skin, the default `scrollbarConstructor` is changed to a different scrollbar class which handles scrollbar spriting. Spriting of the scrollbars of an individual component can therefore be disabled by creating the component with `scrollbarConstructor` set to the "Scrollbar" class. "Scrollbar" is a basic scrollbar class that does not employ spriting.

### Groups

- scrolling

**Flags**: IA

---
## Attr: Canvas.snapGridStyle

### Description
Specifies indication style to use for snap points, either a grid of lines or an array of crosses. The lines can be configured using the property [Canvas.snapGridLineProperties](#attr-canvassnapgridlineproperties).

### Groups

- snapGridDragging

**Flags**: IR

---
## Attr: Canvas.dragMaxHeight

### Description
Sets maximum height that this Canvas can be resized to by a user. Actual limit will be minimum of `dragMaxHeight` and [Canvas.maxHeight](#attr-canvasmaxheight).

### Groups

- sizing

**Flags**: IRWA

---
## Attr: Canvas.contents

### Description
The contents of a canvas or label widget. Any HTML string is acceptable.

### Groups

- contents

### See Also

- [Canvas.dynamicContents](#attr-canvasdynamiccontents)

**Flags**: IRWA

---
## Attr: Canvas.showShadow

### Description
Whether to show a drop shadow for this Canvas.

Shadows may be rendered using [css](#attr-canvasusecssshadow) or via images. The appearance of shadows can be customized via [Canvas.shadowColor](#attr-canvasshadowcolor) (for css-based shadows) or [Canvas.shadowImage](#attr-canvasshadowimage) (for image based shadows), [Canvas.shadowDepth](#attr-canvasshadowdepth), [Canvas.shadowOffset](#attr-canvasshadowoffset) and [Canvas.shadowSoftness](#attr-canvasshadowsoftness).

When [Canvas.useCSSShadow](#attr-canvasusecssshadow) is false, developers should be aware that the drop shadow is rendered as a [peer](#attr-canvaspeers) and is drawn outside the specified width and height of the widget meaning a widget with shadows takes up a little more space than it otherwise would. A full screen canvas with showShadow set to true as this would be likely to cause browser scrollbars to appear - developers can handle this by either setting this property to false on full-screen widgets, or by setting overflow to "hidden" on the `<body>` element if browser-level scrolling is never intended to occur.

### Groups

- shadow

**Flags**: IRW

---
## Attr: Canvas.alwaysShowScrollbars

### Description
Should this browser always show custom scrollbars if [Canvas.showCustomScrollbars](#attr-canvasshowcustomscrollbars) is true?

On [touch devices](Browser.md#classattr-browseristouch) that support native touch scrolling, if [showCustomScrollbars](#attr-canvasshowcustomscrollbars) is `true` and touch scrolling has not been disabled by the [Canvas.useTouchScrolling](#attr-canvasusetouchscrolling) and/or [Canvas.disableTouchScrollingForDrag](#attr-canvasdisabletouchscrollingfordrag) settings, should custom scrollbars _and_ native touch scrolling be enabled for this component? If `false` or unset, then only native touch scrolling will be enabled. If `true`, then both scrolling mechanisms will be enabled.

**NOTE:** Because native touch scrolling (also called momentum scrolling) is computationally intensive, some mobile browsers implement an optimization where the state of the DOM for the element being scrolled will be frozen or partially frozen during the scroll animation. This results in a delay between when the scroll position reaches a certain point in the animation and when the positions of the custom scrollbar thumbs are updated to reflect that scroll position.

For non-touch devices, setting this property to `true` will override [Canvas.nativeAutoHideScrollbars](#attr-canvasnativeautohidescrollbars), and ensure custom scrollbars are shown for the component

### Groups

- scrolling

**Flags**: IRA

---
## Attr: Canvas.scrollbarSize

### Description
How thick should we make the scrollbars for this canvas. This only applies if [Canvas.showCustomScrollbars](#attr-canvasshowcustomscrollbars) is `true`.

**NOTE:** When [spriting is enabled](../kb_topics/skinning.md#kb-topic-skinning--theming), changing the `scrollbarSize` may cause tiling of certain images and backgrounds that make up the custom scrollbar. This can be fixed for a component by creating it with [Canvas.scrollbarConstructor](#attr-canvasscrollbarconstructor) set to "Scrollbar"—a basic scrollbar class that does not employ spriting.

### Groups

- scrolling

### See Also

- [Canvas.getScrollbarSize](#method-canvasgetscrollbarsize)

**Flags**: IRWA

---
## Attr: Canvas.borderRadius

### Description
The CSS border-radius for this widget. The value can be any variant of a CSS border-radius value - that is, from 1 to 4 space-separated px values, where one value affects all corners and 4 values affects individual corners. For example "10px" applies a 10px radius to all corners, where "5px 10px 15px 20px" applies a different radius to each corner, clockwise from Top-Left: "TL TR BR BL".

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.doubleClickDelay

### Description
Amount of time (in milliseconds) between which two clicks are considered a single click

### Groups

- events

**Flags**: IRWA

---
## Attr: Canvas.htmlPosition

### Description
If [Canvas.htmlElement](#attr-canvashtmlelement) is specified, this attribute specifies the position where the canvas should be inserted relative to the `htmlElement` in the DOM.

### Groups

- htmlElement
- positioning

**Flags**: IRWA

---
## Attr: Canvas.snapOnDrop

### Description
When this canvas is dropped onto an object supporting snap-to-grid, should it snap to the grid (true, the default) or just drop wherever the mouse is (false).

### Groups

- snapGridDragging

### See Also

- [Canvas.snapToGrid](#attr-canvassnaptogrid)
- [Canvas.shouldSnapOnDrop](#method-canvasshouldsnapondrop)

**Flags**: IRWA

---
## Attr: Canvas.useBackMask

### Description
In earlier versions of Internet Explorer (pre IE9), a native limitation exists whereby if HTML elements are overlapping on the page, certain elements can appear to "burn through" elements in the same position with a higher z-index. Specific cases in which this have been observed include Applets, `<IFRAME>` elements, and for older versions of IE, native `<SELECT>` items.

The backMask is a workaround for this issue. If `useBackMask` is set to `true`, the component will render an empty `<IFRAME>` element behind the canvas, which prevents this effect in all known cases.

Has no effect in other browsers.

**Flags**: IRWA

---
## Attr: Canvas.destroying

### Description
This property is set to true when the [Canvas.destroy](#method-canvasdestroy) method is called on a widget. If this property is true, but [Canvas.destroyed](#attr-canvasdestroyed) is not, this indicates the canvas is in the process of being destroyed.

### See Also

- [Canvas.destroy](#method-canvasdestroy)

**Flags**: RA

---
## Attr: Canvas.dynamicContentsVars

### Description
An optional map of name:value parameters that will be available within the scope of the dynamicContents evaluation. For example - if you have e.g:
```
 Canvas.create({
   dynamicContents: true,
   dynamicContentsVars: {
       name: "Bob"
   },
   contents: "hello ${name}"
 });
 
```
The above will create a canvas with contents `hello Bob`. You can add, remove, and change values in the dynamicContentsVars object literal, just call `markForRedraw()` on the canvas to have the dynamicContents template re-evaluated.

Note that `this` is always available inside a dynamic contents string and points to the canvas instance containing the dynamic contents.

Used only if [Canvas.dynamicContents](#attr-canvasdynamiccontents) : true has been set.

### See Also

- [Canvas.dynamicContents](#attr-canvasdynamiccontents)

**Flags**: IRWA

---
## Attr: Canvas.ariaRole

### Description
ARIA role of this component. Usually does not need to be manually set - see [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance).

### Groups

- accessibility

**Flags**: IR

---
## Attr: Canvas.dynamicContents

### Description
Dynamic contents allows the contents string to be treated as a simple but powerful template. When this attribute is set to true, JavaScript expressions may be embedded within the contents string, using the format: `${_[JavaScript to evaluate]_}`.

For example, to include the current date in a templated message, `canvas.contents` could be set to:  
`"Today's date is `<b>`${new Date().toUSShortDate()}`</b>`"`

Embedded expressions will be evaluated when the canvas is drawn or redrawn, and the result of the evaluated expression will be displayed to the user. If the expression does not evaluate to a String, the `toString()` representation of the returned object will be displayed automatically

Dynamic expressions are evaluated in the scope of the canvas displaying the content, so the `this` keyword may be used within your expression to refer to the canvas. Developers may also explicitly supply values for variables to be used within the evaluation via the [Canvas.dynamicContentsVars](#attr-canvasdynamiccontentsvars) property.

Notes:

*   Calling markForRedraw() on the canvas will evaluate any embedded expressions.
*   Multiple such expressions may be embedded within the contents string for a component.
*   If an error occurs during evaluation, a warning is logged to the [Developer Console](../kb_topics/debugging.md#kb-topic-debugging) and the error string will be embedded in place of the expected value in the Canvas.

### Groups

- contents
- dynamicStrings

### See Also

- [Canvas.contents](#attr-canvascontents)
- [Canvas.dynamicContentsVars](#attr-canvasdynamiccontentsvars)

**Flags**: IRWA

---
## Attr: Canvas.showDragShadow

### Description
When this widget is dragged, if its dragAppearance is `"target"`, should we show a shadow behind the canvas during the drag.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.canHover

### Description
Will this Canvas fire hover events when the user hovers over it, or one of its children?

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)
- [Canvas.hover](#method-canvashover)

**Flags**: IRW

---
## Attr: Canvas.sizeMayChangeOnRedraw

### Description
Is it possible that a call to [Canvas.redraw](#method-canvasredraw) on this widget will change its size?

Used by framework layout code when determining whether a component which has been [marked as dirty](#method-canvasmarkforredraw) needs an immediate redraw to determine its drawn size.

If unset, default behavior assumes any component with overflow set to "visible" may change size on redraw, and any component with overflow set to "hidden", "scroll", or "auto" will not. This property overrides that behavior, and may be used to indicate that some component with non visible overflow can change size on redraw. An example use case would be a custom component with an override to explicitly resize the component as part of the redraw() flow.

**Flags**: IRWA

---
## Attr: Canvas.momentumScrollMinSpeed

### Description
The minimum speed in pixels per second that must be reached for momentum scrolling to kick in. This setting only applies to touch-enabled devices.

**Flags**: IRWA

---
## Attr: Canvas.snapToAlign

### Description
Flag to disable snapping to alignment when this Canvas is dragged when [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign) is enabled on this Canvas' parent.

To control snapping to align for the children dragged _within_ this Canvas, see [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign) instead.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.startLine

### Description
Whether this canvas should always start a new line when used as a tile in a [FlowLayout](../reference.md#class-flowlayout). This property is not supported in a [TileLayout](TileLayout.md#class-tilelayout) with [TileLayout.layoutPolicy](TileLayout.md#attr-tilelayoutlayoutpolicy): "fit" or if databound (i.e. for a [TileGrid](TileGrid.md#class-tilegrid)).

### Groups

- layoutPolicy

### See Also

- [TileLayout.autoWrapLines](TileLayout.md#attr-tilelayoutautowraplines)

**Flags**: IRW

---
## Attr: Canvas.canSelectText

### Description
Whether native drag selection of contained text is allowed within this Canvas.

Note that setting this property to `false` will not avoid text selection which is initiated outside this Canvas from continuing into this Canvas, even if text selection began in another Canvas.

### Groups

- events

**Flags**: IRWA

---
## Attr: Canvas.hoverAutoFitWidth

### Description
if [Canvas.showHover](#attr-canvasshowhover) is true, this property will cause the specified [Canvas.hoverWidth](#attr-canvashoverwidth) to be treated as a minimum width for the hover. If the hover content string exceeds this, the hover will expand to accommodate it up to [Canvas.hoverAutoFitMaxWidth](#attr-canvashoverautofitmaxwidth) (without the text wrapping).

Using this settings differs from simply disabling wrapping via [hoverWrap:false](#attr-canvashoverwrap) as the content will wrap if the [Canvas.hoverAutoFitMaxWidth](#attr-canvashoverautofitmaxwidth) is exceeded.

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRWA

---
## Attr: Canvas.peers

### Description
Array of all Canvii that are peers of this Canvas.

Use [Canvas.addPeer](#method-canvasaddpeer) and [Canvas.removePeer](#method-canvasremovepeer) to add and remove peers after a Canvas has been created/drawn.

See [containment](../kb_topics/containment.md#kb-topic-component-containment-and-hierarchy) for an overview of master/peer relationships.

### Groups

- containment

**Flags**: IRA

---
## Attr: Canvas.childrenSnapCenterAlign

### Description
See [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign). This setting enables or disables snapping on center alignment only.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.hoverScreen

### Description
Screen to create (via [createScreen()](RPCManager.md#classmethod-rpcmanagercreatescreen)) in lieu of calling [Canvas.getHoverComponent](#method-canvasgethovercomponent).

### Groups

- hoverComponents

**Flags**: IR

---
## Attr: Canvas.canAdaptWidth

### Description
Indicates that this component is able to render itself at multiple possible sizes, in order to fit into less space when very little space is available, or to display more information or provide more immediate access to functionality when more space is available.

Unlike simply indicating a flexible size via width:"\*", setting `canAdaptWidth` indicates that a component has 2 (or more) different ways of rendering itself with different _discrete_ sizes, but does not have the ability to use every additional available pixel.

For example, a menu embedded in a toolbar might show as only a fixed-size icon which reveals menu options when clicked, or if enough space is available, could show all of the menu options directly in the toolbar. In this example, the menu should either be allocated just enough space for an icon, or enough space for _all_ options to appear inline; any other amount of space being allocated is just a waste.

When a component with `canAdaptWidth` is part of a Layout, [Canvas.adaptWidthBy](#method-canvasadaptwidthby) will be called every time component sizes are being calculated, passing a positive or negative pixel value:

*   a _positive_ pixel value indicates a surplus - all other component's minimum sizes can be accommodated, including any [Canvas.minWidth](#attr-canvasminwidth) declared on the `canAdaptWidth` component itself
*   a _negative_ pixel value indicates that the containing layout is going to be forced to [Overflow](../reference.md#type-overflow) (introduce scrollbars, clip content, etc) unless some component or set of components gives up at least this many pixels

If a non-zero value is returned from `adaptWidthBy`, this means that the component is willing to shrink or expand by that many pixels. Returning 0 means that the component is unable to reduce size further, or for a surplus, cannot make good use of the surplus space.

*   A call to [Canvas.adaptWidthBy](#method-canvasadaptwidthby) may surrender as many pixels as desired (as long as the widget won't drop below its minimum allowed width), no matter whether a positive (surplus) or negative (overflow) pixel value is supplied, but
*   A call to [Canvas.adaptWidthBy](#method-canvasadaptwidthby) may not increase its size by more than the number of offered pixels - so if an overflow is present, it may not increase its size at all.

Note that when the initial width is specified as a stretch size (e.g. "\*"), then after [Canvas.adaptWidthBy](#method-canvasadaptwidthby) is called, the Framework will stretch (but not shrink) the member like any other stretch-size Layout member, but the `unadaptedWidth` argument will always reflect the unstretched width requested by the previous call to [Canvas.adaptWidthBy](#method-canvasadaptwidthby). This behavior may be disabled by specifying the initial width as a number, or leaving it unspecified.

Behavior is slightly different for overflow: "visible" members - in this case the `unadaptedWidth` passed in will reflect the current visible width of the member, rather than the last width requested by the previous call to [Canvas.adaptWidthBy](#method-canvasadaptwidthby) or the specified width (on the first call). However, note that the visible length will match your requested width unless the member is actually overflowed. Stretch sizing is not supported for adaptive-width members with overflow: "visible".

Caution: you must either determine the current size of the canvas by maintaining your own internal state, or use the `unadaptedWidth` parameter passed to [Canvas.adaptWidthBy](#method-canvasadaptwidthby). You must not call [Canvas.getWidth](#method-canvasgetwidth) or [Canvas.getVisibleWidth](#method-canvasgetvisiblewidth) on the canvas itself inside [Canvas.adaptWidthBy](#method-canvasadaptwidthby) as the size is in the processing of being determined, but you may draw children or call [Canvas.getVisibleWidth](#method-canvasgetvisiblewidth) on them, as we guarantee that the adaptive-width canvas is drawn before the first call to [Canvas.adaptWidthBy](#method-canvasadaptwidthby). An example of drawing children in [Canvas.adaptWidthBy](#method-canvasadaptwidthby) to compute overall width may be seen in the *Inlined Menu Mobile Sample*.

Note that reasonable settings for [Canvas.minWidth](#attr-canvasminwidth) should be applied to all other flexible-sized members of a layout where a `canAdaptWidth` component appears, because when too little space is available, a `canAdaptWidth` component will absorb all available space until minimums for other components are hit (or the `canAdaptWidth` component reaches its maximum size). If more than one `canAdaptWidth` component is present, [Canvas.adaptiveWidthPriority](#attr-canvasadaptivewidthpriority) to give priority to a particular component when allocating space.

All of the above behaviors are exactly the same for height, using [Canvas.canAdaptHeight](#attr-canvascanadaptheight) and [Canvas.adaptHeightBy](#method-canvasadaptheightby).

### See Also

- [Canvas.canAdaptHeight](#attr-canvascanadaptheight)
- [Canvas.adaptWidthBy](#method-canvasadaptwidthby)
- [Canvas.adaptHeightBy](#method-canvasadaptheightby)

**Flags**: IRW

---
## Attr: Canvas.showCustomScrollbars

### Description
Whether to use the browser's native scrollbars or SmartClient-based scrollbars.

SmartClient-based scrollbars are skinnable, giving you complete control over look and feel. SmartClient-based scrollbars also enable some interactions not possible with native scrollbars, such as [variable height records](ListGrid_1.md#attr-listgridfixedrecordheights) in grids in combination with [data paging](ListGrid_1.md#attr-listgriddatapagesize).

Native browser scrollbars are slightly faster simply because there are less SmartClient components that need to be created, drawn and updated. Each visible SmartClient-based scrollbar on the screen has roughly the impact of two StretchImgButtons.

SmartClient is always aware of the size of the scrollbar, regardless of whether native or custom scrollbars are used, and regardless of what operating system and/or operating system "theme" or "skin" is in use. This means SmartClient will correctly report the [viewport size](#method-canvasgetviewportheight), that is, the interior area of the widget excluding space taken by scrollbars, which is key for exactly filling a component with content without creating unnecessary scrolling.

The `showCustomScrollbars` setting is typically overridden in load\_skin.js in order to change the default for all SmartClient components at once. This may be achieved via the static [Canvas.setShowCustomScrollbars](#classmethod-canvassetshowcustomscrollbars) method or via a simple addProperties block , like so:

```
     isc.Canvas.addProperties({ showCustomScrollbars:false });
 
```

On [touch devices](Browser.md#classattr-browseristouch), custom scrollbars are disabled in favor of enabling native touch scrolling if available. However, custom scrollbars _and_ native touch scrolling can be enabled for the component by setting [Canvas.alwaysShowScrollbars](#attr-canvasalwaysshowscrollbars) to `true`.

### Groups

- scrolling

### See Also

- [Canvas.receiveScrollbarEvents](#attr-canvasreceivescrollbarevents)

**Flags**: IRA

---
## Attr: Canvas.canDrop

### Description
Indicates that this object can be dropped on top of other widgets. Only valid if canDrag or canDragReposition is true.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.percentBox

### Description
Governs the model to be used when sizing canvases with percentage width or height, or positioning widgets with a specified [snapTo](#attr-canvassnapto).

Only affects widgets with a a specified [percentSource](#attr-canvaspercentsource), or widgets that have [Canvas.snapTo](#attr-canvassnapto) set and are peers of some [other canvas](#method-canvasgetmastercanvas).

Determines whether the coordinates used for sizing (for percentage sized widgets) and positioning (if `snapTo` is set) should be relative to the visible size or the viewport size of the percentSource or [master canvas](#method-canvasgetmastercanvas) widget.

### Groups

- sizing

**Flags**: IRA

---
## Attr: Canvas.correctZoomOverflow

### Description
Whether the Framework should correct for erroneous scrollHeight and scrollWidth values reported by the browser when zoomed (via browser or OS-level zoom) by allowing [Canvas.maxZoomOverflowError](#attr-canvasmaxzoomoverflowerror) of overflow before enabling scrolling and displaying custom scrollbars. Only relevant when [Canvas.overflow](#attr-canvasoverflow) is "auto".

This property is defaulted to true in the [Canvas](#class-canvas) prototype for those browsers where the situation has been observed, except for Firefox, where a better solution is applied that doesn't rely on [Canvas.maxZoomOverflowError](#attr-canvasmaxzoomoverflowerror) and never clips any content. Setting this property false will disable the workaround for all browsers, including Firefox. Without a workaround, scrollbars may oscillate rapidly when the browser or OS is zoomed.

### See Also

- [browserZoom](../kb_topics/browserZoom.md#kb-topic-native-browser-zoom-support)

**Flags**: IRWA

---
## Attr: Canvas.groupLabelStyleName

### Description
Sets the style for the grouping label. Only necessary when showing a [grouping frame](#attr-canvasisgroup).

Note that [Canvas.groupLabelBackgroundColor](#attr-canvasgrouplabelbackgroundcolor) overrides any background-color of this style.

### Groups

- appearance

**Flags**: IR

---
## Attr: Canvas.resizeFrom

### Description
When drag resizing is enabled via [Canvas.canDragResize](#attr-canvascandragresize), restricts resizes to only certain edges or corners.

The default of null indicates the widget can be resized from any corner or edge (if `canDragResize` is true).

To restrict resizing to only certain corners, set `resizeFrom` to an Array of [EdgeName](../reference.md#type-edgename)s.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.minNonEdgeSize

### Description
If the widget has drag resize configured on one or more of it's edges, and the edgeMarginSize is large enough that the remaining space is less than `minNonEdgeSize`, the edgeMarginSize will be reduced such that the non-edge part of the widget is at least 1/3 of the total space (with two draggable edges) or half of it (with one draggable edge).

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.snapOffsetLeft

### Description
If [snapTo](#attr-canvassnapto) is defined for this widget, this property can be used to specify an offset in px or percentage for the left coordinate of this widget.

For example if `snapTo` is specified as `"L"` and `snapOffsetLeft` is set to 6, this widget will be rendered 6px inside the left edge of its parent or master element. Alternatively if `snapTo` was set to `"R"`, a `snapOffsetLeft` value of -6 would cause the component to be rendered 6px inside the right edge of its parent or [master canvas](#method-canvasgetmastercanvas).

### Groups

- snapPositioning

### See Also

- [Canvas.snapTo](#attr-canvassnapto)

**Flags**: IRW

---
## Attr: Canvas.snapHGap

### Description
The horizontal grid size to use, in pixels, when snap-to-grid is enabled.

### Groups

- snapGridDragging

### See Also

- [Canvas.snapToGrid](#attr-canvassnaptogrid)
- [Canvas.snapResizeToGrid](#attr-canvassnapresizetogrid)
- [Canvas.childrenSnapToGrid](#attr-canvaschildrensnaptogrid)
- [Canvas.childrenSnapResizeToGrid](#attr-canvaschildrensnapresizetogrid)

**Flags**: IRW

---
## Attr: Canvas.animateShowTime

### Description
Default time for performing an animated show. If unset, `this.animateTime` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.canDrag

### Description
Indicates whether this widget can initiate custom drag-and-drop operations (other than reposition or resize). Normally [Canvas.canDragReposition](#attr-canvascandragreposition) or [Canvas.canDragResize](#attr-canvascandragresize) would be used instead of this property.

Note: this property may be manipulated by higher-level dragging semantics.

If [Canvas.useNativeDrag](#attr-canvasusenativedrag) is true and this widget has been drawn, then this widget must be [redrawn](#method-canvasredraw) in order for a change of the value of this attribute to take effect.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.dataPath

### Description
A dataPath may be specified on any canvas. This provides a straightforward way to display or edit complex nested data.

**NOTE: the dataPath feature is intended to help certain legacy architectures, such as systems that work in terms of exchanging large messages with several different entity types in one message, and are incapable of providing separate access to each entity type.  
See the [DataPath overview](../reference_2.md#type-datapath) for more information.**

For components which support displaying or editing data values, (such as [DynamicForm](DynamicForm.md#class-dynamicform) or [ListGrid](ListGrid_1.md#class-listgrid) components), the dataPath may be set to specify how the components data is accessed. In this case the dataPath essentially specifies a nested object to edit - typically a path to a field value within a dataSource record. Note that a ValuesManager will be required to handle connecting the dataBoundcomponent to the appropriate sub object. This may be explicitly specified on the component, or a parent of the component, or automatically generated if a DataSource is specified on either the component or a parent thereof.

To provide a simple example - if a complex object existed with the following format:

```
 { companyName:"Some Company",
   address:{    street:"123 Main Street", city:"New York", state:"NY"  }
 }
 
```
a developer could specify a DynamicForm instance with 'dataPath' set to "address" to edit the nested address object:
```
 isc.ValuesManager.create({
      ID:'vm',
      values: { companyName:"Some Company",
              address:{    street:"123 Main Street", city:"New York", state:"NY"  }
      }
 });

 isc.DynamicForm.create({
      valuesManager:"vm",
      dataPath:"address",
      items:[{name:"street"}, {name:"city"}, {name:"state"}]
 });
 
```
If a component is specified with a `dataPath` attribute but does not have an explicitly specified valuesManager, it will check its parent element chain for a specified valuesManager and automatically bind to that. This simplifies binding multiple components used to view or edit a nested data structure as the valuesManager needs only be defined once at a reasonably high level component. Here's an example of this approach:
```
 isc.ValuesManager.create({
      ID:'vm',
      values: { companyName:"Some Company",
              address:{    street:"123 Main Street", city:"New York", state:"NY"  }
      }
 });

 isc.Layout.create({
      valuesManager:vm,
      members:[
          isc.DynamicForm.create({
              dataPath:"/",
              items:[{name:"companyName"}]
          }),
          isc.DynamicForm.create({
              dataPath:"address",
              items:[{name:"street"}, {name:"city"}, {name:"state"}]
          })
      ]
 });
 
```
Note that in this case the valuesManager is specified on a Layout, which has no 'values' management behavior of its own, but contains items with a specified dataPath which do. In this example you'd see 2 forms allowing editing of the nested data structure.

dataPaths from multiple nested components may also be combined. For example:

```
 isc.ValuesManager.create({
      ID:'vm',
      values: { companyName:"Some Company",
              address:{    street:"123 Main Street", city:"New York", state:"NY"  }
              parentCompany:{
                  companyName:"Some Corporation",
                  address:{   street:"1 High Street", city:"New York", state:"NY" }
              }
      }
 });

 isc.Layout.create({
      valuesManager:vm,
      members:[
          isc.DynamicForm.create({
              dataPath:"/",
              items:[{name:"companyName"}]
          }),
          isc.DynamicForm.create({
              dataPath:"address",
              items:[{name:"street"}, {name:"city"}, {name:"state"}]
          }),
          isc.Layout.create({
              dataPath:"parentCompany",
              members:[
                  isc.DynamicForm.create({
                      dataPath:"",
                      items:[{name:"companyName", type:"staticText"}]
                  }),
                  isc.DetailViewer.create({
                      dataPath:"address",
                      fields:[{name:"street", name:"city", name:"state"}]
                  })
              ]
          })
      ]
 });
 
```
In this example the detailViewer will display data from the `parentCompany.address` object within the base record.

Note that if a component has a specified dataSource and shows child components with a specified dataPath, there is no need to explicitly declare a valuesManager at all. If a component with a dataPath has a dataSource, or an ancestor with a dataSource specified, it will, a valuesManager will automatically be generated on the higher level component (and be available as `component.valuesManager`).

#### Difference between "" and "/" - relative and absolute datapaths
In the above example, note how the form for entering the "main" company name is given a dataPath of "/", while the form for entering the parent company name is given a dataPath of "". The difference here is exactly the same as you would find in a filesystem path: a dataPath starting with "/" is absolute, so "/" by itself means "root". A dataPath that does not start with "/" is relative, and the empty string indicates that dataPaths for items below this one in the hierarchy should apply the dataPath so far from the hierarchy above.

If that isn't clear, consider the form for entering the parent company name in the above example. The correct dataPath to the field is `/parentCompany/companyName`. We have the "parentCompany" part of that path provided by the containing Layout, so we cannot reiterate it on the form itself. However, if we omit the dataPath property altogether, the framework will not seek to apply dataPath at all. So, we specify the empty string, which tells SmartClient to use dataPath and to retain the portion of the path derived so far from the containment hierarchy.

One further clarification: relative paths are only different from absolute paths if they are relative to something other than the root. So in the above example, although we specify "/" as the dataPath of the "main" company name form, we would get exactly the same behavior by specifying it as "", because the correct dataPath for the companyName field is "/companyName" - ie, it is relative to the root.

### See Also

- [Canvas.ruleScope](#attr-canvasrulescope)

**Flags**: IRWA

---
## Attr: Canvas.matchElementWidth

### Description
For canvases with a specified [Canvas.htmlElement](#attr-canvashtmlelement) where [Canvas.persistentMatchElement](#attr-canvaspersistentmatchelement) is set to true, how should the canvas match the element's width?

**Flags**: IRA

---
## Attr: Canvas.visibleWhen

### Description
Criteria to be evaluated to determine whether this Canvas should be visible. Re-evaluated whenever data in the [Canvas.ruleScope](#attr-canvasrulescope) changes.

A basic criteria uses textMatchStyle:"exact". When specified in [Component XML](../kb_topics/componentXML.md#kb-topic-component-xml) this property allows [shorthand formats](../kb_topics/xmlCriteriaShorthand.md#kb-topic-xmlcriteriashorthand) for defining criteria.

### Groups

- ruleCriteria

**Flags**: IR

---
## Attr: Canvas.edgeCenterBackgroundColor

### Description
Background color for the center section only. Can be used as a surrogate background color for the decorated Canvas, if the Canvas is set to partially overlap the edges and hence can't show a background color itself without occluding media.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: Canvas.width

### Description
The `canvas.width` attribute specifies the size for a component's horizontal dimension; `canvas.height` specifies the size for the vertical dimension.

May be set to an integer value (a number of pixels), a percentage value like "50%", or "\*".

See [percentSizing](../kb_topics/percentSizing.md#kb-topic-canvas-percentage-sizing) for details on how percentage or `"*"` values are resolved actual size.

If [overflow](#attr-canvasoverflow) is set to "visible", the specified size acts as a minimum, and the component may overflow to show all content and/or children.

Note that developers wishing to set a default width or height for a component class should set [defaultWidth](#attr-canvasdefaultwidth) or [Canvas.defaultHeight](#attr-canvasdefaultheight) instead of specifying an explicit default `width` or `height`. This is important for components added to a [Layout](Layout.md#class-layout) as members - it allows the Layout to determine whether the canvas has an explicitly specified size that must be respected, or whether it can participate in its [sizing policies](../reference_2.md#type-layoutpolicy).

### Groups

- sizing

**Flags**: IRW

---
## Attr: Canvas.maxWidth

### Description
Maximum width available to this Canvas.

The `maxWidth` and [Canvas.maxHeight](#attr-canvasmaxheight) settings apply to:

*   For a canvas being managed as a member of a [Layout](Layout.md#class-layout), the maximum size the layout should apply to the canvas.
*   For a canvas with a width or height specified as a percent value, a maximum numeric pixel value to limit how large the canvas is sized.
*   determining size for a Canvas in a [CanvasItem](CanvasItem.md#class-canvasitem) (`maxHeight` only)
*   end user [drag resizing](#attr-canvascandragresize)

Maximum sizes do not apply in various other circumstances where sizes are being determined, such as [ListGrid recordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents).

### Groups

- sizing

### See Also

- [Canvas.dragMaxWidth](#attr-canvasdragmaxwidth)

**Flags**: IRWA

---
## Attr: Canvas.animateRectAcceleration

### Description
Default acceleration function for performing an animated move and resize. If unset, `this.animateAcceleration` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.maxZoomOverflowError

### Description
When [Canvas.correctZoomOverflow](#attr-canvascorrectzoomoverflow) is true and browser or OS-level zoom is active, determines how much overflow must occur before the Framework enables scrolling for this canvas.

The larger the value, the more clipping that can occur before scrolling is enabled. So, this property should never be set larger than the minimum amount needed to prevent scrollbar oscillation when zoomed - which is the maximum scrollHeight or scrollWidth error.

### See Also

- [browserZoom](../kb_topics/browserZoom.md#kb-topic-native-browser-zoom-support)

**Flags**: IRWA

---
## Attr: Canvas.alwaysManageFocusNavigation

### Description
Should focus navigation for this canvas and its descendents be handled explicitly by intercepting "Tab" key events and calling the [TabIndexManager.shiftFocus](TabIndexManager.md#classmethod-tabindexmanagershiftfocus) API?

Setting this property to `true` will cause the registered TabIndexManager entry for this canvas to be marked as [useExplicitFocusNavigation:true](TabIndexManager.md#classmethod-tabindexmanagersetuseexplicitfocusnavigation), and will cause standard event handling for the canvas and its descendents to intercept Tab keystrokes and explicitly call [TabIndexManager.shiftFocus](TabIndexManager.md#classmethod-tabindexmanagershiftfocus) rather than relying on native browser Tab navigation

**Flags**: IR

---
## Attr: Canvas.hoverWidth

### Description
If [this.showHover](#attr-canvasshowhover) is true, this property can be used to customize the width of the hover canvas shown. See also [Canvas.hoverAutoFitWidth](#attr-canvashoverautofitwidth) and [Canvas.hoverAutoFitMaxWidth](#attr-canvashoverautofitmaxwidth).

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.children

### Description
Array of all Canvii that are immediate children of this Canvas.

Use [Canvas.addChild](#method-canvasaddchild) and [Canvas.removeChild](#method-canvasremovechild) to add and remove children after a Canvas has been created/drawn.

See [containment](../kb_topics/containment.md#kb-topic-component-containment-and-hierarchy) for an overview of parent/child relationships.

### Groups

- containment

**Flags**: IR

---
## Attr: Canvas.persistentMatchElement

### Description
If this canvas has a specified [Canvas.htmlElement](#attr-canvashtmlelement) and [Canvas.matchElement](#attr-canvasmatchelement) is set to true, should the canvas perform a one time resize to fit the target element on draw, or should it continue to match the target element as its size changes due to page reflows?

**Flags**: IRA

---
## Attr: Canvas.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](#method-canvasseteditmode).

**Flags**: IR

---
## Attr: Canvas.useImageForSVG

### Description
If set, forces the main SVG image or icon in the canvas to be rendered in an image tag rather than an object tag, the default. Typical use cases might be configuring the image of an [Img](Img.md#class-img) or [ImgButton](ImgButton.md#class-imgbutton), or the icon of a [Button](Button.md#class-button).

Rendering via object tag provides the maximum support for CSS in SVG, but may result in a flicker at the browser level when changing images - either manually such as with [Canvas.setImage](#method-canvassetimage) or via state change from rollover, mouseDown, etc. Using image tags to inline the images breaks CSS support but may avoid flickering.

If this property is _not_ set, then you can also control whether an SVG image is rendered in an object or image tag by setting the query param "tag" on the image URL - see [SCImgURL](../reference.md#type-scimgurl) for details.

Note that if multiple icons are potentially present in a canvas (e.g. [removeIcons](ListGrid_1.md#attr-listgridremoveicon) in the cells of a grid body), then setting this property on the widget instance may have no effect. In such case, the [Canvas](#class-canvas) prototype is consulted.

### Groups

- images

### See Also

- [Img.src](Img.md#attr-imgsrc)
- [Button.icon](Button.md#attr-buttonicon)
- [Class.addProperties](Class.md#method-classaddproperties)
- [Canvas.forwardSVGeventsToObject](#attr-canvasforwardsvgeventstoobject)

**Flags**: IRA

---
## Attr: Canvas.childrenSnapAlign

### Description
If enabled while [Canvas.childrenSnapToGrid](#attr-canvaschildrensnaptogrid) is enabled, children dragged within this Canvas will also snap to positions where their edges or center lines would be aligned with the edges or centers of other components, and lines will be shown to point out the possible alignment (with appearance controlled by [Canvas.snapAlignCenterLineStyle](#attr-canvassnapaligncenterlinestyle) and [Canvas.snapAlignEdgeLineStyle](#attr-canvassnapalignedgelinestyle) respectively.

By default, edge- or center-snapping is enabled for all components, but the set of eligible components can be explicitly set via [Canvas.snapAlignCandidates](#attr-canvassnapaligncandidates).

See also [Canvas.childrenSnapCenterAlign](#attr-canvaschildrensnapcenteralign) and [Canvas.childrenSnapEdgeAlign](#attr-canvaschildrensnapedgealign) for enabling or disabling center alignment or edge alignment individually.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.dragIntersectStyle

### Description
This indicates how the system will test for droppable targets: either by intersection with the mouse or intersection with the rectangle of the dragMoveTarget.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.edgeShowCenter

### Description
Whether to show media in the center section, that is, behind the decorated Canvas.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: Canvas.canvasItem

### Description
If this canvas is being displayed in a [CanvasItem](CanvasItem.md#class-canvasitem), this property will be set to point at the item. Otherwise this property will be null.

**Flags**: R

---
## Attr: Canvas.matchElementHeight

### Description
For canvases with a specified [Canvas.htmlElement](#attr-canvashtmlelement) where [Canvas.persistentMatchElement](#attr-canvaspersistentmatchelement) is set to true, how should the canvas match the element's height?

**Flags**: IRA

---
## Attr: Canvas.defaultHeight

### Description
For custom components, establishes a default height for the component.

For a component that should potentially be sized automatically by a Layout, set this property rather than [Canvas.height](#attr-canvasheight) directly, because Layouts regard a height setting as an explicit size that shouldn't be changed.

### Groups

- sizing

**Flags**: IRWA

---
## Attr: Canvas.dragMinWidth

### Description
Minimum width that this Canvas can be resized to by a user. Actual limit will be maximum of `dragMinWidth` and [Canvas.minWidth](#attr-canvasminwidth).

Note that a Canvas with overflow:"visible" has an implicit minimize size based on it's contents.

Note that `dragMinWidth` affects only user-initiated drag resizes. To set the minimum width of a Canvas embedded in a Layout, you can set +{minWidth}, or [Layout.minMemberLength](Layout.md#attr-layoutminmemberlength) to constrain the minimum size along the length axis of all members of the [Layout](Layout.md#class-layout).

### Groups

- sizing

**Flags**: IRWA

---
## Attr: Canvas.percentSource

### Description
If this canvas has its size specified as a percentage, this property allows the user to explicitly designate another canvas upon which sizing will be based.

If unset percentage sizing is based on  
\- the [master canvas](#method-canvasgetmastercanvas) if there is one and [snapTo](#attr-canvassnapto) is set,  
\- otherwise on the amount of space available in this widget's parent canvas, if this is a child of some other widget  
\- otherwise the page size.

### Groups

- sizing

### See Also

- [Canvas.percentBox](#attr-canvaspercentbox)

**Flags**: IRWA

---
## Attr: Canvas.isPrinting

### Description
This boolean flag will be set to true by framework logic while generating print HTML for this widget as a result to a call to [Canvas.showPrintPreview](#classmethod-canvasshowprintpreview) (or just [Canvas.getPrintHTML](#method-canvasgetprinthtml)). Note that this flag is set recursively as parent widgets generate print HTML for their children.

This is a read-only property and should not be modified by application code.

**Flags**: R

---
## Attr: Canvas.snapVGap

### Description
The vertical grid size to use, in pixels, when snap-to-grid is enabled.

### Groups

- snapGridDragging

### See Also

- [Canvas.snapToGrid](#attr-canvassnaptogrid)
- [Canvas.snapResizeToGrid](#attr-canvassnapresizetogrid)
- [Canvas.childrenSnapToGrid](#attr-canvaschildrensnaptogrid)
- [Canvas.childrenSnapResizeToGrid](#attr-canvaschildrensnapresizetogrid)

**Flags**: IRW

---
## Attr: Canvas.animateShowAcceleration

### Description
Default acceleration function for performing an animated show. If unset, `this.animateAcceleration` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.animateFadeTime

### Description
Default time for performing an animated fade. If unset, `this.animateTime` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.animateScrollAcceleration

### Description
Default acceleration function for performing an animated scroll. If unset, `this.animateAcceleration` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.pointerTarget

### Description
This property in conjunction with the [pointerSettings.snapTo](../reference.md#object-pointersettings) places the canvas in relation to the target canvas.

Depending on the `pointerSettings.snapTo` and the [pointerSettings.targetSnapTo](../reference.md#object-pointersettings) the canvas will be positioned so the pointer correctly points to the target.

**Flags**: IR

---
## Attr: Canvas.childrenSnapEdgeAlign

### Description
See [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign). This setting enables or disables snapping on edge alignment only.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.shadowSpread

### Description
Explicit spread for the css-based drop shadow shown if [Canvas.useCSSShadow](#attr-canvasusecssshadow) is true and [Canvas.showShadow](#attr-canvasshowshadow) is true. This property governs how much larger than the widget the shadow will appear. A negative value (coupled with an explicit offset) will result in a smaller shadow.

Has no effect if we are not using css-based shadows - in that case, use [Canvas.shadowImage](#attr-canvasshadowimage) instead.

### Groups

- shadow

**Flags**: IRWA

---
## Attr: Canvas.printStyleName

### Description
The CSS class to apply when printing this widget. If unset, falls back to the [specified style](#attr-canvasstylename).

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.cursor

### Description
Specifies the cursor image to display when the mouse pointer is over this widget. It corresponds to the CSS cursor attribute. See Cursor type for different cursors.

See also [Canvas.disabledCursor](#attr-canvasdisabledcursor) and [Canvas.noDropCursor](#attr-canvasnodropcursor).

### Groups

- cues

**Flags**: IRWA

---
## Attr: Canvas.snapHDirection

### Description
The horizontal snap direction. Set this value to "before" to snap to the nearest gridpoint to the left; set it to "after" to snap to the nearest gridpoint to the right; and set it to "nearest" to snap to the nearest gridpoint in either direction.

### Groups

- snapGridDragging

### See Also

- [Canvas.snapToGrid](#attr-canvassnaptogrid)
- [Canvas.snapResizeToGrid](#attr-canvassnapresizetogrid)
- [Canvas.childrenSnapToGrid](#attr-canvaschildrensnaptogrid)
- [Canvas.childrenSnapResizeToGrid](#attr-canvaschildrensnapresizetogrid)

**Flags**: IRW

---
## Attr: Canvas.backgroundImage

### Description
URL for a background image for this widget (corresponding to the CSS "background-image" attribute).

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.componentMask

### Description
Automatically generated mask canvas displayed when [Canvas.showComponentMask](#method-canvasshowcomponentmask) is called.

### See Also

- [Canvas.componentMaskDefaults](#attr-canvascomponentmaskdefaults)

**Flags**: R

---
## Attr: Canvas.locatorName

### Description
Local name for referencing this canvas from an autoTest locator string. It will be used instead of `index` if found. This name must by unique within the parent component.

By setting a static ID on certain top-level components and then using locatorName in contained components, stable locators can be created for these components without the need to pervasively assign IDs.

### Groups

- autoTest

**Flags**: IRWA

---
## Attr: Canvas.snapGridLineProperties

### Description
Specifies line styling to use when drawing the grid of lines for [SnapGridStyle](../reference.md#type-snapgridstyle): "lines".

### Groups

- snapGridDragging

**Flags**: IR

---
## Attr: Canvas.animateHideEffect

### Description
Default animation effect to use if [Canvas.animateHide](#method-canvasanimatehide) is called without an explicit `effect` parameter

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.locateChildrenBy

### Description
Strategy to use when locating children in this canvas from an autoTest locator string.

### Groups

- autoTest

**Flags**: IRWA

---
## Attr: Canvas.appImgDir

### Description
Default directory for app-specific images, relative to the Page-wide [appImgDir](Page.md#classmethod-pagegetappimgdir).

### Groups

- images

**Flags**: IRWA

---
## Attr: Canvas.minWidth

### Description
Minimum width available to this Canvas.

The `minWidth` and [Canvas.minHeight](#attr-canvasminheight) settings apply to:

*   For a canvas being managed as a member of a [Layout](Layout.md#class-layout), the minimum size the layout should apply to the canvas.
*   For a canvas with a width or height specified as a percent value, a minimum numeric pixel value to limit how large the canvas is sized.
*   determining size for a Canvas in a [CanvasItem](CanvasItem.md#class-canvasitem) (`minHeight` only)
*   end user [drag resizing](#attr-canvascandragresize)
*   minimum size when using [Overflow](../reference.md#type-overflow) "visible" outside of a Layout - minimum size will be the greater of this setting or the minimum size needed to make all content visible

Minimum sizes do not apply in various other circumstances where sizes are being determined, such as [ListGrid recordComponents](ListGrid_1.md#attr-listgridshowrecordcomponents).

See also [Layout.minMemberLength](Layout.md#attr-layoutminmemberlength) as a way of establishing minimum sizes along the length axis for all members of a [Layout](Layout.md#class-layout) with a single setting.

### Groups

- sizing

### See Also

- [Canvas.dragMinWidth](#attr-canvasdragminwidth)

**Flags**: IRWA

---
## Attr: Canvas.shouldPrint

### Description
Whether this canvas should be included in a printable view.

Default is to:

*   omit all peers (edges generated by showEdges:true, etc)
*   omit anything considered a "control", such as a button or menu (see [PrintProperties.omitControls](PrintProperties.md#attr-printpropertiesomitcontrols))
*   include everything else not marked shouldPrint:false

### Groups

- printing

**Flags**: IRW

---
## Attr: Canvas.useNativeDrag

### Description
If set, native HTML5 drag and drop will be used for all drags initiated on this widget (on browsers where this is supported), and native HTML5 drop events occurring over this widget will be processed.

When using native HTML5 drags, the same series of events fires as for a normal drag ([Canvas.dragStart](#method-canvasdragstart), [Canvas.dropMove](#method-canvasdropmove), etc.), and the [dragType](#attr-canvasdragtype) / [dropTypes](#attr-canvasdroptypes) system works. [dragAppearance](#attr-canvasdragappearance) is not supported; however, basic customization of the browser's tracker image is supported in certain browsers via the [EventHandler.setDragTrackerImage](EventHandler.md#classmethod-eventhandlersetdragtrackerimage) API.

The primary difference with a native drag is that it can be cross-frame; that is, the user can drag out of the current browser window and drop into a different window or tab.

To provide information that will be available to a foreign frame, use [EventHandler.setNativeDragData](EventHandler.md#classmethod-eventhandlersetnativedragdata). This API must be called when the [Canvas.dragStart](#method-canvasdragstart) event fires, and will not work if called at any other time.

However, due to browser bugs and/or browser-imposed limitations, the information provided to `setNativeDragData` cannot be accessed in the foreign frame until the actual drop occurs (mouse button released). This means drop eligibility cannot be determined dynamically based on the dragged data; instead, eligibility can only be determined based on the [Canvas.dragType](#attr-canvasdragtype) / [Canvas.dropTypes](#attr-canvasdroptypes) system. For this reason, a [Canvas.dragType](#attr-canvasdragtype) **must** be set on the source of a drag.

NOTE: Although Internet Explorer 10+ supports a subset of the [HTML5 drag and drop standard](http://www.w3.org/TR/html5/editing.html#dnd), native drag and drop is disabled in IE (and Microsoft Edge Legacy) because cross-window drags—the primary purpose of this API—are not possible.

### Groups

- dragdrop

**Flags**: IR

---
## Attr: Canvas.noDoubleClicks

### Description
If true, this canvas will receive all mouse-clicks as single [click](#method-canvasclick) events rather than as [doubleClick](#method-canvasdoubleclick) events.

### Groups

- events

**Flags**: IRWA

---
## Attr: Canvas.proportionalResizeModifiers

### Description
If [Canvas.proportionalResizing](#attr-canvasproportionalresizing) is set to "modifier" or "modifierOff" then proportional resizing of the widget is activated or deactivated, respectively, whenever at least one key in this set of modifier keys is pressed.

The keys allowed in this set are: "Alt", "Ctrl", and "Shift". If this set of keys is empty then proportional resizing is always used if `proportionalResizing` is "modifier" and is never used if `proportionalResizing` is "modifierOff" .

### Groups

- dragdrop

**Flags**: IR

---
## Attr: Canvas.snapResizeToAlign

### Description
Flag to disable snapping to alignment when this Canvas is resized.

To control snapping to align for the children resized _within_ this Canvas, see [childrenResizeSnapAlign](#attr-canvaschildrenresizesnapalign) instead.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.overflow

### Description
Controls what happens when the drawn size of the content of a Canvas is either greater or smaller than the specified size of the Canvas. Similar to the CSS property overflow, but consistent across browsers. See Overflow type for details.

### Groups

- sizing

**Flags**: IRW

---
## Attr: Canvas.edgeOffset

### Description
Amount the contained Canvas should be offset. Defaults to edgeSize; set to less than edgeSize to allow the contained Canvas to overlap the edge and corner media.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: Canvas.snapAlignEdgeLineStyle

### Description
CSS border declaration used for the line shown to indicate snapping to a edge line when [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign) is set.

### Groups

- snapGridDragging

**Flags**: IR

---
## Attr: Canvas.snapToEdgeAlign

### Description
Flag to disable snapping to edge alignment when this Canvas is dragged when [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign) is enabled on this Canvas' parent.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.customEdges

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
## Attr: Canvas.snapOffsetTop

### Description
If [snapTo](#attr-canvassnapto) is defined for this widget, this property can be used to specify an offset in px or percentage for the top coordinate of this widget.

For example if `snapTo` is specified as `"T"` and `snapOffsetTop` is set to 6, this widget will be rendered 6px below the top edge of its parent or master element. Alternatively if `snapTo` was set to `"B"`, a `snapOffsetTop` value of -6 would cause the component to be rendered 6px inside the bottom edge of its parent or [master canvas](#method-canvasgetmastercanvas).

### Groups

- snapPositioning

### See Also

- [Canvas.snapTo](#attr-canvassnapto)

**Flags**: IRW

---
## Attr: Canvas.animateAcceleration

### Description
Default acceleration effect to apply to all animations on this Canvas. Can be overridden by setting animationAcceleration for specific animations or by passing an acceleration function directly into the appropriate method.

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.tabIndex

### Description
If specified this governs the tabIndex of the widget in the page's tab order. Setting this value to `-1` will ensure the canvas does not show up in the page's tab order, though if [canFocus](#attr-canvascanfocus) is true, the user may still give it keyboard focus by clicking on the widget directly.

By default SmartClient auto-assigns tab-indices, ensuring focusable widgets are reachable by tabbing in an intuitive order based on widget hierarchy and draw order. Specifying an explicit tab index means a widget will not participate in this automatic tab position allocation and is typically not recommended except for very simple cases.

For more information on automatic tab index assignment, including recommended approaches for customizing tab order assignation, see the [tabOrderOverview](../kb_topics/tabOrderOverview.md#kb-topic-tab-order-overview). Developers may call [Canvas.clearExplicitTabIndex](#method-canvasclearexplicittabindex) to clear any explicitly assigned tab index, and have the widget participate in automatic tab position allocation.

`canvas.tabIndex` cannot be set to greater than [Canvas.TAB_INDEX_FLOOR](#classattr-canvastab_index_floor) - as we reserve the values above this range for auto-assigned tab-indices.

### Groups

- focus

**Flags**: IRWA

---
## Attr: Canvas.locateChildrenType

### Description
[LocatorTypeStrategy](../reference.md#type-locatortypestrategy) to use when finding children within this canvas.

### Groups

- autoTest

**Flags**: IRWA

---
## Attr: Canvas.shadowImage

### Description
If [Canvas.useCSSShadow](#attr-canvasusecssshadow) is false, (or for browsers that do not support css3), this property supplies the base name of the series of images for the sides, corners, and center of the shadow.

The actual image names fetched for the dropShadow combine the segment name and the `shadowDepth` setting. For example, given "ds.png" as the base name, a depth of 4, and the top-left segment of the shadow, we'd use "ds4\_TL.png".

The names for segments are the same as those given for controlling resizable edges; see [Canvas.resizeFrom](#attr-canvasresizefrom). The center segment has the name "center". The center segment is the only segment that doesn't include the depth in the URL, so the final image name for the center given a baseName of "ds.png" would be just "ds\_center.png".

### Groups

- shadow

**Flags**: IRA

---
## Attr: Canvas.hoverAutoFitMaxWidth

### Description
Maximum auto-fit width for a hover if [Canvas.hoverAutoFitWidth](#attr-canvashoverautofitwidth) is enabled. May be specified as a pixel value, or a percentage of page width.

### Groups

- hovers

**Flags**: IRW

---
## Attr: Canvas.enabled

### Description
If set to true, this widget will be enabled, if set to false, or null, this widget will be disabled.

### Groups

- enable

**Deprecated**

**Flags**: IRWA

---
## Attr: Canvas.groupLabelBackgroundColor

### Description
If set, the background color of the grouping label. Only applicable when showing a [grouping frame](#attr-canvasisgroup).

This corresponds to the CSS background-color property on the grouping label. You can set this property to an RGB value (e.g. #22AAFF) or a named color (e.g. red) from a list of browser supported color names.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.showResizeBar

### Description
When this Canvas is included as a member in a [Layout](Layout.md#class-layout), whether a resizeBar should be shown after this member in the layout, to allow it to be resized.

Whether a resizeBar is actually shown also depends on the [defaultResizeBars](Layout.md#attr-layoutdefaultresizebars) attribute of the layout, and whether this Canvas is the last layout member.

By default the resize bar acts on the Canvas that it is declared on. If you want the resize bar to instead act on the next member of the Layout (e.g. to collapse down or to the right), set [Canvas.resizeBarTarget](#attr-canvasresizebartarget) as well.

### Groups

- layoutMember

### See Also

- [Canvas.resizeBarTarget](#attr-canvasresizebartarget)
- [Layout.defaultResizeBars](Layout.md#attr-layoutdefaultresizebars)

**Flags**: IRW

---
## Attr: Canvas.defaultWidth

### Description
For custom components, establishes a default width for the component.

For a component that should potentially be sized automatically by a Layout, set this property rather than [Canvas.width](#attr-canvaswidth) directly, because Layouts regard a width setting as an explicit size that shouldn't be changed.

### Groups

- sizing

**Flags**: IRWA

---
## Attr: Canvas.topElement

### Description
The top-most Canvas (i.e., not a child of any other Canvas), if any, in this widget's containment hierarchy.

### Groups

- containment

**Flags**: RA

---
## Attr: Canvas.dragMaskType

### Description
This property controls what kind of mask is used in case [Canvas.useDragMask](#attr-canvasusedragmask) is enabled.

### Groups

- dragdrop

**Flags**: IRW

---
## Attr: Canvas.animateTime

### Description
Default total duration of animations. Can be overridden by setting animation times for specific animations, or by passing a `duration` parameter into the appropriate animate...() method.

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.dragTarget

### Description
A different widget that should be actually dragged when dragging initiates on this widget. One example of this is to have a child widget that drags its parent, as with a drag box. Because the parent automatically repositions its children, setting the drag target of the child to the parent and then dragging the child will result in both widgets being moved.

Valid `dragTarget` values are:

*   `null` (default) \[this widget is its own drag target\]
*   another widget, or widget ID
*   `"parent"` drag target is this widget's [parentCanvas](#method-canvasgetparentcanvas)
*   `"top"` drag target is this widget's [topElement](#attr-canvastopelement)

Note that for dragging to work as intended, the [Canvas.resizeFrom](#attr-canvasresizefrom) setting on the `dragTarget` must be null or a superset of the [Canvas.resizeFrom](#attr-canvasresizefrom) on this canvas.

### Groups

- dragdrop

### See Also

- [EventHandler.getDragTarget](EventHandler.md#classmethod-eventhandlergetdragtarget)

**Flags**: IRWA

---
## Attr: Canvas.canAcceptDrop

### Description
Indicates that this object can receive dropped widgets (i.e. other widgets can be dropped on top of it).

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.animateResizeTime

### Description
Default time for performing an animated resize. If unset, `this.animateTime` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.disableTouchScrollingForDrag

### Description
Disables [Canvas.useTouchScrolling](#attr-canvasusetouchscrolling) whenever a built-in drag operation has been enabled which is known to be non-functional if touch scrolling is enabled. Default behavior is to leave touch scrolling enabled even if it makes other enabled drag operations non-functional, since any [accessible](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) application must provide an alternative way to perform drag and drop operations anyway.

`disableTouchScrollingForDrag` exists so that applications can change the default setting on a per-component basis (via [Class.changeDefaults](Class.md#classmethod-classchangedefaults)), in order to make a system-wide or per-component-type decision about whether to favor touch scrolling vs retaining the ability to drag and drop via finger drags, instead of having to set `useTouchScrolling` on each individual instance.

See the [Mobile Development overview](../kb_topics/mobileDevelopment.md#kb-topic-mobile-application-development) for more background information.

### Groups

- scrolling

**Flags**: IR

---
## Attr: Canvas.nativeAutoHideScrollbars

### Description
In some platform/browser configurations, scrollable regions do not show visible scrollbars until the user attempts to interact with the region. The interaction to show the scrollbar varies by browser/OS but may include starting a trackpad scroll or simply rolling over the scrollable element.

If `nativeAutoHideScrollbars` is set to true, we detect platforms that show scrollbars dynamically on user interaction and for components with [Canvas.showCustomScrollbars](#attr-canvasshowcustomscrollbars) we ignore the specified [Canvas.scrollbarConstructor](#attr-canvasscrollbarconstructor), and instead create system-managed native scrollbars via the special [NativeScrollbar](../reference.md#class-nativescrollbar) class, and set [Canvas.floatingScrollbars](#attr-canvasfloatingscrollbars) to true.

Not applicable to [touch devices](Browser.md#classattr-browseristouch)

Has no impact if [Canvas.alwaysShowScrollbars](#attr-canvasalwaysshowscrollbars) is true.

If [Canvas.showCustomScrollbars](#attr-canvasshowcustomscrollbars) is false this setting will have no effect (we would be showing custom scrollbars in any case)  

Also does not apply to [touch scrolling interfaces](#attr-canvasusetouchscrolling) (where scrollbars are always hidden unless [Canvas.alwaysShowScrollbars](#attr-canvasalwaysshowscrollbars) is true).

### Groups

- scrolling

**Flags**: IRA

---
## Attr: Canvas.snapToCenterAlign

### Description
Flag to disable snapping to center alignment when this Canvas is dragged when [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign) is enabled on this Canvas' parent.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.canAdaptHeight

### Description
See [Canvas.canAdaptWidth](#attr-canvascanadaptwidth).

**Flags**: IRW

---
## Attr: Canvas.shrinkElementOnHide

### Description
This is an advanced setting. If set to `true`, when a widget is [hidden](#method-canvashide), the widget's handle will be resized such that it takes up no space, in addition to having its css `visibility` property set to `"hidden"`.

In addition to preventing the size of this widget from impacting the [scroll size](#method-canvasgetscrollwidth) of any parent widget while hidden, this setting works around a native bug observed in Internet Explorer 10, whereby an ``<IFRAME>`` element with visibility set to hidden can cause rendering problems, if the HTML loaded by the ``<IFRAME>`` contains a ``<frameset>``. In this case the browser may refuse to draw other elements at the same coordinates with a lower z-index than the hidden frame. Setting this property to `true` works around this problem for cases where an ``<IFRAME>`` containing a `<frameset` will be rendered out, for example in an [HTMLFlow](HTMLFlow.md#class-htmlflow) with `contentsType` set to `"page"`.

### Groups

- visibility

**Flags**: IRWA

---
## Attr: Canvas.ariaState

### Description
Explicit set of ARIA state mappings for this component. Any values specified in this object will be combined with [Canvas.getAriaStateDefaults](#method-canvasgetariastatedefaults) as described in [Canvas.getAriaState](#method-canvasgetariastate).

Usually this does not need to be manually set - see [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance).

Usage: This attribute should be set to a mapping of aria state-names to values - for example to have the "aria-haspopup" property be present with a value "true", you'd specify:

```
  { haspopup : true }
 
```

### Groups

- accessibility

**Flags**: IRA

---
## Attr: Canvas.canDragScroll

### Description
If this Canvas is canAcceptDrop:true, when the user drags a droppable widget over an edge of the widget, should we scroll to show the rest of the widget's content? Returned from canvas.shouldDragScroll() if there are scrollbars.

### Groups

- dragging

### See Also

- [Canvas.shouldDragScroll](#method-canvasshoulddragscroll)

**Flags**: IRWA

---
## Attr: Canvas.edgeBackgroundColor

### Description
Background color for the EdgedCanvas created to decorate this component. This can be used to provide an underlying "tint" color for translucent edge media

### Groups

- imageEdges

**Flags**: IR

---
## Attr: Canvas.animateResizeLayoutMode

### Description
When to update the [child layout](#method-canvaslayoutchildren) for a [size animation](#method-canvasanimateresize). Updating the child layout more often may improve appearance, but risks prohibitive overhead with more complicated widget hierarchies.

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.edgeImage

### Description
Base name of images for edges. Extensions for each corner or edge piece will be added to this image URL, before the extension. For example, with the default base name of "edge.gif", the top-left corner image will be "edge\_TL.gif".

The full list of extensions is: "\_TL", "\_TR", "\_BL", "\_BR", "\_T", "\_L", "\_B", "\_R", "\_center".

### Groups

- imageEdges

**Flags**: IR

---
## Attr: Canvas.showPointer

### Description
Should a pointer be shown? A pointer can be placed on the border to identify the target of the canvas contents. The default position for the pointer is top-right. The position and additional properties of the pointer is specified by [Canvas.pointerSettings](#attr-canvaspointersettings).

If a [pointerTarget](#attr-canvaspointertarget) is specified, `showPointer` will be enabled unless it is explicitly set to `false`.

**Flags**: IRW

---
## Attr: Canvas.edgeMarginSize

### Description
How far into the edge of an object do we consider the "edge" for drag resize purposes?

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.hoverPersist

### Description
Allows interaction with hovers when the cursor is positioned over them.

### Groups

- hovers

### See Also

- [Hover.persistent](Hover.md#classattr-hoverpersistent)

**Flags**: IRW

---
## Attr: Canvas.autoParent

### Description
This initialization property allows developers to create a canvas using the [Class.addAutoChild](Class.md#method-classaddautochild) method, and have it added as a child to some other component. This property may be set to the `_childName_` of another already-created auto-child, or `"none"` to cause the component to be created without being added as a child to any other widget.  
If unset, the canvas will be added as a child to the component on which `addAutoChild(...)` was called.

See [autoChildren](../kb_topics/autoChildren.md#kb-topic-autochildren) for an overview of the autoChild subsystem.

### Groups

- autoChildren

**Flags**: IRA

---
## Attr: Canvas.pointerSettings

### Description
Detail settings of the [pointer](#attr-canvasshowpointer) such as where it should be located along the outside of the canvas.

**Flags**: IR

---
## Attr: Canvas.locatePeersBy

### Description
Strategy to use when locating peers of this canvas from an autoTest locator string.

### Groups

- autoTest

**Flags**: IRWA

---
## Attr: Canvas.snapToGrid

### Description
Causes this canvas to snap to its parent's grid when dragging.

### Groups

- snapGridDragging

### See Also

- [Canvas.childrenSnapToGrid](#attr-canvaschildrensnaptogrid)

**Flags**: IRW

---
## Attr: Canvas.endLine

### Description
Whether this canvas should end the line it's in when used as a tile in a [FlowLayout](../reference.md#class-flowlayout). This property is not supported in a [TileLayout](TileLayout.md#class-tilelayout) with [TileLayout.layoutPolicy](TileLayout.md#attr-tilelayoutlayoutpolicy): "fit" or if databound (i.e.[TileGrid](TileGrid.md#class-tilegrid)).

### Groups

- layoutPolicy

### See Also

- [TileLayout.autoWrapLines](TileLayout.md#attr-tilelayoutautowraplines)

**Flags**: IRW

---
## Attr: Canvas.snapVDirection

### Description
The vertical snap direction. Set this value to "before" to snap to the nearest gridpoint above; set it to "after" to snap to the nearest gridpoint below; and set it to "nearest" to snap to the nearest gridpoint in either direction.

### Groups

- snapGridDragging

### See Also

- [Canvas.snapToGrid](#attr-canvassnaptogrid)
- [Canvas.snapResizeToGrid](#attr-canvassnapresizetogrid)
- [Canvas.childrenSnapToGrid](#attr-canvaschildrensnaptogrid)
- [Canvas.childrenSnapResizeToGrid](#attr-canvaschildrensnapresizetogrid)

**Flags**: IRW

---
## Attr: Canvas.editProxy

### Description
An [EditProxy](EditProxy.md#class-editproxy) controls the behaviors of a component when it is placed into [editing mode](../kb_topics/devTools.md#kb-topic-dashboards--tools-framework-overview).

The `editProxy` AutoChild is created when a component is first placed into edit mode via [Canvas.setEditMode](#method-canvasseteditmode).

`editProxy` properties can be supplied on a [PaletteNode](../reference.md#object-palettenode) or [EditNode](../reference.md#object-editnode) as [editProxyProperties](PaletteNode.md#attr-palettenodeeditproxyproperties), but must be provided before the component is first placed into edit mode.

Most editable components use a custom EditProxy. See the documentation for each class' [editProxyConstructor](#attr-canvaseditproxyconstructor) to determine the class.

### See Also

- [Canvas.setEditMode](#method-canvasseteditmode)

**Flags**: IR

---
## Attr: Canvas.dragRepositionCursor

### Description
Cursor to switch to if the mouse is over a widget that is drag repositionable.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.hoverFocusKey

### Description
For canvases [showing a hover](#attr-canvasshowhover), this attribute gives users a way to pin the hover in place so they can interact with it (scroll it, click embedded links, etc). Clicking outside the hover (on some other component) will still dismiss it.

When enabled, the standard hover canvas will display the [Hover.focusKeyHintLabel](Hover.md#classattr-hoverfocuskeyhintlabel) to prompt the user on how to give the hover focus. This behavior may be disabled by setting [Hover.showFocusKeyHint](Hover.md#classattr-hovershowfocuskeyhint) to false

Note that setting a hoverFocusKey also sets [hoverPersist](#attr-canvashoverpersist) to "clickPin". This makes hovers stay visible while the cursor is over them, and become pinned if clicked, the same as pressing the hoverFocusKey.

**Flags**: IRW

---
## Attr: Canvas.locateByIDOnly

### Description
If `true`, when retrieving a [locator](AutoTest.md#classmethod-autotestgetlocator) for this component always return a reference directly to this component by [widget ID](#attr-canvasid), using the compact format `"///_canvasID_"`, ignoring any parent elements and ignoring any configured [testRoot](AutoTest.md#classattr-autotesttestroot). This format of locator will always be resolved back to the component by ID regardless of any changes in its position in the UI structure of an application.

This setting is appropriate for components which are expected to always be present in an application with a stable [Canvas.ID](#attr-canvasid).

**Flags**: IRWA

---
## Attr: Canvas.margin

### Description
Set the CSS Margin, in pixels, for this component. Margin provides blank space outside of the border.

This property sets the same thickness of margin on every side. Differing per-side margins can be set in a CSS style and applied via [Canvas.styleName](#attr-canvasstylename).

Note that the specified size of the widget will be the size **including** the margin thickness on each side.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.ID

### Description
Global identifier for referring to a widget in JavaScript. The ID property is optional if you do not need to refer to the widget from JavaScript, or can refer to it indirectly (for example, by storing the reference returned by [create()](Class.md#classmethod-classcreate)).

An internal, unique ID will automatically be created upon instantiation for any canvas where one is not provided.

The ID property should be unique in the global scope. If `window[_ID_]` is already assigned to something else a warning will be logged using the developer console, and the existing reference will be replaced, calling [destroy()](#method-canvasdestroy) on the previous object if it is a SmartClient Class instance.

Automatically generated IDs will be unique as long as the canvases they refer to remain active - once a canvas with an automatically generated ID has been destroyed, its ID may be reused for the next canvas created with no explicitly specified ID.

### Groups

- basics

### See Also

- [Canvas.name](#attr-canvasname)

**Flags**: IR

---
## Attr: Canvas.visibility

### Description
Controls widget visibility when the widget is initialized. See [Visibility](../reference_2.md#type-visibility) type for details.

Specifying "visible" sets the CSS visiblity to "visible", forcing a child to be visible even if the parent is hidden. **Not supported for use with SmartClient layouts, scrolling or auto-sizing** but may be useful when working with third-party or legacy DOM layout systems.

Note that if [Canvas.hideUsingDisplayNone](#attr-canvashideusingdisplaynone) is set for a hidden ancestor, setting `visibility` will have no effect at all until that ancestor becomes visible.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.adaptiveWidthPriority

### Description
If multiple widgets in the same Layout have [adaptive width](#attr-canvascanadaptwidth), `adaptiveWidthPriority` can be set to indicate which of the components should be given priority access to space.

The widget with the highest priority setting will be offered surplus space first, and asked to give up space last. Lack of a priority setting is treated as zero. Any adaptive widgets with the same priority setting will be asked to give up or release space according to their order in [Layout.members](Layout.md#attr-layoutmembers).

### See Also

- [Canvas.canAdaptWidth](#attr-canvascanadaptwidth)

**Flags**: IR

---
## Attr: Canvas.hoverVAlign

### Description
If `this.showHover` is true, this property can be used to customize the vertical alignment of content in the hover canvas.

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.floatingScrollbars

### Description
If [Canvas.showCustomScrollbars](#attr-canvasshowcustomscrollbars) is true, should the scrollbars be drawn floating over the component handle, or should the handle shrink to accommodate them?

Floating scrollbars are typically only appropriate for scrollbars that are hidden by default and get shown as the user actively scrolls the widget handle, such as in the [Canvas.nativeAutoHideScrollbars](#attr-canvasnativeautohidescrollbars) case. If floating scrollbars are permanently visible over the component handle, they may block some of the widget's content.

**Flags**: IRA

---
## Attr: Canvas.extraSpace

### Description
When this Canvas is included as a member in a Layout, extra blank space that should be left after this member in a Layout.

### Groups

- layoutMember

### See Also

- [LayoutSpacer](../reference.md#class-layoutspacer)

**Flags**: IR

---
## Attr: Canvas.showEdges

### Description
Whether an [EdgedCanvas](EdgedCanvas.md#class-edgedcanvas) should be used to show image-based edges around this component.

### Groups

- imageEdges

**Flags**: IR

---
## Attr: Canvas.useCSSShadow

### Description
If [Canvas.showShadow](#attr-canvasshowshadow) is true, should we use the css `box-shadow` property (where supported) to achieve the shadow?

Set this property to false to switch to a media-based approach, achieved by rendering the [Canvas.shadowImage](#attr-canvasshadowimage) in an automatically generated peer. This approach is also used regardless of this property value in older browsers where the css `box-shadow` property isn't supported.

See also [Canvas.shadowColor](#attr-canvasshadowcolor), [Canvas.shadowDepth](#attr-canvasshadowdepth), [Canvas.shadowOffset](#attr-canvasshadowoffset), [Canvas.shadowSoftness](#attr-canvasshadowsoftness) and [Canvas.shadowSpread](#attr-canvasshadowspread)

### Groups

- shadow

**Flags**: IRA

---
## Attr: Canvas.printChildrenAbsolutelyPositioned

### Description
Should this canvas print its children absolutely positioned when generating [printable HTML](#classmethod-canvasgetprinthtml).

By default explicitly specified absolute positioning and sizing is ignored when generating print HTML. This is done intentionally: there is no way for the framework to predict how explicit sizes will translate to a the printed page and if HTML for printing includes the same absolute positioning and sizing as is displayed within an application it is very common to encounter undesirable effects, such as seeing tables get broken over several pages horizontally when there is enough room to print them on a single page of paper.

In some cases, however, a developer may wish to have explicit sizing and positioning respected within the print-view. Setting this attribute to `true` will cause this to occur.

### Groups

- printing

**Flags**: IRWA

---
## Attr: Canvas.componentMaskDefaults

### Description
Defaults for the [Canvas.componentMask](#attr-canvascomponentmask) autoChild. Default properties include [Canvas.backgroundColor](#attr-canvasbackgroundcolor) being set to `"black"` and [Canvas.opacity](#attr-canvasopacity) being set to `20`.

**Flags**: IR

---
## Attr: Canvas.autoMaskComponents

### Description
When nodes are added to an EditContext, should they be masked by setting [EditProxy.useEditMask](EditProxy.md#attr-editproxyuseeditmask) `true` if not explicitly set?

**Deprecated**

**Flags**: IR

---
## Attr: Canvas.top

### Description
Number of pixels the top of the widget is offset down from its default drawing context (either its parent's top-left corner, or the document flow, depending on the value of the [Canvas.position](#attr-canvasposition) property).

Can also be set as a percentage, specified as a String ending in '%', eg, "50%". In this case the top coordinate is considered as a percentage of the specified height of the [parent](#method-canvasgetparentcanvas).

### Groups

- positioning

**Flags**: IRW

---
## Attr: Canvas.backgroundRepeat

### Description
Specifies how the background image should be tiled if this widget is larger than the image. It corresponds to the CSS `background-repeat` attribute.

The default of null means no `background-repeat` CSS will be written out. See [BackgroundRepeat](../reference_2.md#type-backgroundrepeat) type for details on other settings.

NOTE: this setting directly sets the CSS property `background-repeat` but does not attempt to work around various known bugs with this setting, or lack of support in IE6. If you need to apply CSS-based workarounds for browser limitations with this setting, it's best to do so via setting [Canvas.styleName](#attr-canvasstylename).

### Groups

- appearance

**Flags**: IR

---
## Attr: Canvas.masterElement

### Description
This Canvas's "master" (the Canvas to which it was added as a peer), if any.

### Groups

- containment

**Deprecated**

**Flags**: RA

---
## Attr: Canvas.prompt

### Description
Prompt displayed in hover canvas if [showHover](#attr-canvasshowhover) is true.

### Groups

- hovers

**Flags**: IRW

---
## Attr: Canvas.dragType

### Description
Sets a `dragType` for this widget used, to be compared to [dropTypes](#attr-canvasdroptypes) on possible drop target widgets. See [Canvas.dropTypes](#attr-canvasdroptypes) for a full explanation.

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.hoverAlign

### Description
If `this.showHover` is true, this property can be used to customize the alignment of content in the hover canvas.

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.parentElement

### Description
This Canvas's immediate parent, if any.  
Can be initialized, but any subsequent manipulation should be via [addChild()](#method-canvasaddchild) and [removeChild()](#method-canvasremovechild) calls on the parent.

### Groups

- containment

**Deprecated**

**Flags**: IRA

---
## Attr: Canvas.hoverOpacity

### Description
If `this.showHover` is true, should the hover canvas be shown with opacity other than 100?

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.hoverStyle

### Description
If `this.showHover` is true, this property can be used to specify the css style to apply to the hover canvas.

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.snapAlignCandidates

### Description
When [Canvas.childrenSnapAlign](#attr-canvaschildrensnapalign) is enabled, list of candidates to check for alignment.

If a list of `snapAlignCandidates` is never provided, the default is to use all children that are not explicitly excluded via [Canvas.isSnapAlignCandidate](#attr-canvasissnapaligncandidate), including automatically adding newly added children as candidates, and ignoring children that have been removed. Use [Canvas.addSnapAlignCandidate](#method-canvasaddsnapaligncandidate) and [Canvas.removeSnapAlignCandidate](#method-canvasremovesnapaligncandidate) to add and remove special candidates while retaining all children as default candidates.

Possible candidates which are not drawn or are hidden are automatically ignored.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.styleName

### Description
The CSS class applied to this widget as a whole.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Canvas.snapTo

### Description
Position this widget such that it is aligned with ("snapped to") an edge of its [master](#method-canvasgetmastercanvas) (if specified), or its [parent canvas](#method-canvasgetparentcanvas).

Note that this property also impacts the sizing of this widget. If this widgets size is specified as a percent value, and has no explicit [Canvas.percentSource](#attr-canvaspercentsource), sizing will be calculated based on the size of the [master canvas](#method-canvasgetmastercanvas) when snapTo is set.

Possible values: BR, BL, TR, TL, R, L, B, T, C where B=Bottom, T=Top, L=Left, R=right and C=center

Standard snapTo behavior will attach the outer edge of the widget to the parent or master element - for example setting `snapTo` to `"B"` would align the bottom edge of this component with the bottom edge of the master or parent element (and center this component horizontally over its master or parent element). [Canvas.snapEdge](#attr-canvassnapedge) can be specified to change this behavior allowing the developer to, for example, align the top edge of this component with the bottom edge of its [master canvas](#method-canvasgetmastercanvas).

[Canvas.snapOffsetLeft](#attr-canvassnapoffsetleft) and [Canvas.snapOffsetTop](#attr-canvassnapoffsettop) may also be specified to offset the element from exact snapTo alignment.

### Groups

- snapPositioning

### See Also

- [Canvas.snapEdge](#attr-canvassnapedge)
- [Canvas.percentBox](#attr-canvaspercentbox)

**Flags**: IRW

---
## Attr: Canvas.ruleScope

### Description
[Canvas.ID](#attr-canvasid) of the component that gathers the context for evaluation of criteria-based rules specified by properties such as [FormItem.visibleWhen](FormItem.md#attr-formitemvisiblewhen), [Dynamic Properties](Class.md#attr-classdynamicproperties), and [dynamicCriteria](../kb_topics/dynamicCriteria.md#kb-topic-dynamiccriteria) such as [ListGrid.initialCriteria](ListGrid_1.md#attr-listgridinitialcriteria).

If `ruleScope` is not specified, this component will search through its [Canvas.parentCanvas](#attr-canvasparentcanvas) chain until it either reaches the top or reaches a parent marked [Canvas.isRuleScope](#attr-canvasisrulescope). This means that typically, `ruleScope` does not have to be explicitly specified, since components that want to reference each other often have the same top-level parent (eg, they are part of the same screen). However, you would need to specify `ruleScope` in scenarios such as a modal Window that wants to reference values in the component it was launched from.

Determination of the `ruleScope` happens when the component is first drawn.

The component designated as the `ruleScope` manages a nested data structure called the "rule context" which contains information from all [DataBoundComponent](../reference.md#interface-databoundcomponent)s that are registered with the `ruleScope`. By specifying [Criterion.fieldName](Criterion.md#attr-criterionfieldname) as a [DataPath](../reference_2.md#type-datapath), AdvancedCriteria defined in properties such as [FormItem.visibleWhen](FormItem.md#attr-formitemvisiblewhen) can access any part of the rule context.

By default, the rule context contains data as follows:

*   any `DataBoundComponent` that has a DataSource contributes the values of the selected record or record being edited under the ID of the DataSource. For any collision an editable display (such as a form or editable grid) wins over a static display (such as a non-editable grid with a selection.) Hidden or cleared components have lowest priority even if editable. For two editable components the first becomes the contributor.
*   any ListGrid or other component that manages a selection and has been assigned an explicit [Canvas.ID](#attr-canvasid) will contribute the values of the selected record under ``<componentId>`.selectedRecord`, the values of the grid summary record under ``<componentId>`.summaryRecord`, and also contributes 3 flags for checking for selection: `anySelected`, `multiSelected`, `numSelected`.
*   any DynamicForm or other component that edits values and has been assigned an explicit [Canvas.ID](#attr-canvasid) contributes its current values under ``<componentId>`.values`, and contributes a flag `hasChanges`.
*   any DynamicForm or ListGrid that has been assigned an explicit [Canvas.ID](#attr-canvasid) contributes a value ``<componentId>`.focusField`. When present the value indicates the component has focus along with the name of the field that has focus. Its absense indicates the component does not have focus at all.
*   any ListGrid that has been assigned an explicit [Canvas.ID](#attr-canvasid) contributes a flag `isGrouped` under ``<componentId>``.
*   any DataSource included in a [DataContext](../reference.md#object-datacontext) or [Canvas.testDataContext](#attr-canvastestdatacontext) that is being used for this ruleScope contributes the values into the `dataContext` section of the ruleContext (ex. `dataContext.Customer`) so the values do not conflict with normal DataSource contributions. Note that the `dataContext` is immutable so only the first contribution is actually saved.

For example, given a screen where:

*   a ListGrid with ID "itemGrid" and DynamicForm with ID "itemForm" are both bound to the `supplyItem` sample DataSource
*   the ListGrid has a single selection, and the record selected in the ListGrid is being edited in the form, and has been changed

The default rule context available from [Canvas.getRuleContext](#method-canvasgetrulecontext), expressed as JSON, would be:
```
 {
  supplyItem : {
     itemID : "654321",
     itemName : "Sewing Machine",
     price : 5.50, // note: user change
     ..other properties..
  },
  itemForm.values : {
     itemID : "654321",
     itemName : "Sewing Machine",
     price : 5.50, // note: user change
     ..other properties..
  },
  itemForm.focusField : "itemName",
  itemForm.hasChanges : true,
  itemGrid.selectedRecord : {
     itemID : "654321",
     itemName : "Sewing Machine",
     price : 3.50, // note: old price
     ..other properties..
  },
  itemGrid.anySelected : true,
  itemGrid.multiSelected : false,
  itemGrid.numSelected : 1,
  itemGrid.isGrouped : false
 }
 
```
In addition, an application can put custom data into the ruleScope via [Canvas.provideRuleContext](#method-canvasproviderulecontext).

## Troubleshooting RuleScope issues

The ruleScope system consists of two major parts: managing the rule context and using the rule context. The former is handled by [Canvas.provideRuleContext](#method-canvasproviderulecontext) and [Canvas.removeRuleContext](#method-canvasremoverulecontext). Users of rule context are the criteria-based rules noted above.

A number of [Log](Log.md#class-log) categories are provided to make diagnosing ruleScope issues easier:

*   _ruleContext_
*   _whenRules_
*   _dynamicProperties_
*   _dynamicCriteria_

Except for configuration warnings, nothing is logged for these categories unless the log priority is set to either _Info_ or _Debug_. The priorities can be configured and the log messages reviewed in [SmartClient Developer Console](../kb_topics/debugging.md#kb-topic-debugging). By default none of these categories are included in the `Logging Preferences` category choices. To add one or more of these categories, select `More...` then click `Add...`. Be sure to enter the category with the correct capitalization.

At the _Info_ log priority one or two basic log messages are generated per action. The _Debug_ priority generally includes additional information like the full criteria or a message for each evaluation even when no change is made.

#### Using and Interpreting log messages
To address a specific issue on rules, select the _Info_ priority for the target category in the Developer Console then perform your application actions that are being diagnosed. You may want to re-run your application to get a clean start on the changes.
#### whenRules and dynamicProperties
Both of these types of properties are triggered by a criteria that can reference the ruleContext and/or the component's values (for forms). The criteria is re-evaluated on each rule context change and based on the criteria being matched or not, the action is taken or property updated.

Below are some example _Info_ log messages:

```
 16:53:39.032:TMR8[E0]:INFO:whenRules:Hide Canvas 'isc_Canvas_1'
 16:53:39.034:TMR8[E1]:INFO:whenRules:Disabling Canvas 'isc_Button_3'
 16:53:39.509:TMR9[E0]:INFO:whenRules:Hide Canvas 'isc_Canvas_2'
 16:53:39.510:TMR9[E1]:INFO:whenRules:Hide Canvas 'isc_Button_4'
 16:53:39.527:TMR4:INFO:whenRules:Show Canvas 'isc_Canvas_2'
 16:53:39.527:TMR4:INFO:whenRules:Show Canvas 'isc_Button_4'
 16:53:39.528:TMR4:INFO:whenRules:Disabling Canvas 'isc_Button_4'
 16:53:39.529:TMR4:INFO:whenRules:Set read-only (appearance disabled) FormItem 'itemForm3.field2'
 16:53:39.974:TMR6:INFO:whenRules:Set editable (appearance disabled) FormItem 'itemForm3.field2'
 16:53:40.540:TMR2:INFO:whenRules:Enabling FormItemIcon 'itemForm4.field2.remove'
 16:53:40.541:TMR2:INFO:whenRules:Hide FormItemIcon 'itemForm4.field4.edit'
 
```
These indicate various responses to `visibleWhen`, `enableWhen`, and `readOnlyWhen` actions.

By setting the priority to _Debug_ you can see the creation of the rule for the criteria and the evaluation of the criteria before action is taken:

```
 16:53:41.569:TMR7:DEBUG:whenRules:itemForm6:Create whenRule: itemForm6_field2_readOnly, applyWhen {
     "_constructor":"AdvancedCriteria", 
     "operator":"and", 
     "criteria":[
         {
             "fieldName":"layout1.date1", 
             "operator":"greaterOrEqualField", 
             "value":"layout1.date2"
         }
     ]
 } to target {component: [DynamicForm ID:itemForm6], fieldName: "field2", formIconName: undef}
 16:53:41.571:TMR7:DEBUG:whenRules:isc_RulesEngine_5:Applying readOnly rule 'itemForm6_field2_readOnly' for FormItem itemForm6.field2 with action result true. applyWhen criteria matched: {
     "__normalized":true, 
     "_constructor":"AdvancedCriteria", 
     "operator":"and", 
     "criteria":[
         {
             "__normalized":true, 
             "fieldName":"layout1.date1", 
             "operator":"greaterOrEqualField", 
             "value":"layout1.date2"
         }
     ]
 }
 16:53:41.571:TMR7:DEBUG:whenRules:Set read-only (appearance disabled) FormItem 'itemForm6.field2'
 
```
dynamicProperties are similar:
```
 16:59:13.588:XRP8:INFO:dynamicProperties:Set (populateFromDataPath) 'isc_Button_0.title' to [initial value]: Special Title
 16:59:13.650:TMR2:WARN:Class:isc_Class_0:Attempt to evaluate formulaFunction itemForm.values.count * 2 + 10 failed. Error message:undefined is not an object (evaluating 'itemForm.values')
 16:59:13.657:TMR9:INFO:dynamicProperties:Set (populate) 'isc_Class_0.contents' to [initial value]: 34
 
```
This example shows a failed formula indicating that the 'itemForm.values' isn't valid in the ruleContext. In this case the form values haven't been provided to ruleContext yet. When they are the next log message shows the result.
#### dynamicCriteria
Each time a dynamic criteria is evaluated (as triggered by a `ruleContextChanged` event) a log entry is made:
```
 14:54:46.436:INP9:INFO:dynamicCriteria:isc_ListGrid_0:Evaluated dynamic criteria: filterCriteria
 
```
This indicates that dynamicCriteria for isc\_ListGrid\_0 is being evaluated/re-evaluated. By changing the priority to _Debug_ the resolved criteria is also included:
```
 14:55:16.231:INP9:DEBUG:dynamicCriteria:isc_ListGrid_0:Evaluated dynamic criteria: filterCriteria {
     "fieldName":"orderNumber", 
     "operator":"equals", 
     "valuePath":"orderSearchForm.values.orderNumber", 
     "value":10104, 
     "_constructor":"AdvancedCriteria"
 }
 
```
Note the valuePath of `orderSearchForm.values.orderNumber` is resolved to the value of `10104`.
#### ruleContext
If none of the logging above provides details needed to understand what is going on, enabling the _ruleContext_ category can be enabled. At _Info_ a single log message is reported for each ruleContext change.

For example, below are the rule context changes that occurred to trigger the above dynamicCriteria messages above:

```
 14:54:46.432:INP9:INFO:ruleContext:isc_SearchForm_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_SearchForm_0]: Order.orderNumber = 10104
 14:54:46.433:INP9:INFO:ruleContext:isc_SearchForm_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_SearchForm_0]: orderSearchForm.values.orderNumber = 10104
 14:54:46.434:INP9:INFO:ruleContext:isc_SearchForm_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_SearchForm_0]: orderSearchForm.hasChanges = true
 
```
This indicates that isc\_SearchForm\_0 updated rule context with three changed values. There is no indication of when a `ruleContextChanged` event is raised. If that is important, change the log priority to _Debug_ to see more details:
```
 15:16:43.291:INP9:DEBUG:ruleContext:isc_SearchForm_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_SearchForm_0] START TRANSACTION
 15:16:43.292:INP9:DEBUG:ruleContext:isc_SearchForm_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_SearchForm_0]: Order.orderNumber = 10104
 15:16:43.292:INP9:DEBUG:ruleContext:isc_SearchForm_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_SearchForm_0]: orderSearchForm.values.orderNumber = 10104
 15:16:43.293:INP9:DEBUG:ruleContext:isc_SearchForm_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_SearchForm_0]: orderSearchForm.hasChanges = true
 15:16:43.294:INP9:DEBUG:ruleContext:isc_SearchForm_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_SearchForm_0] END TRANSACTION
 
```
Here the isc\_SearchForm\_0 provides rule context changes as part of a 'transaction'. That is, the three values are provided separately but a single `ruleContextChanged` event is raised at the end of the 'transaction'. If only one change is part of a 'transaction' the start/end log messages are suppressed. For example, the isc\_ListGrid\_0 updates rule context as a result of the change in the dynamic criteria. The criteria is provided to rule context separately from `dataLoading` updates:
```
 15:16:43.305:INP9:DEBUG:ruleContext:isc_ListGrid_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_ListGrid_0]: orderDetailGrid.criteria = {fieldName: "orderNumber",
              operator: "equals", valuePath: "orderSearchForm.values.orderNumber", value: 10104, _constructor: "AdvancedCriteria"}
 15:16:43.317:INP9:DEBUG:ruleContext:isc_ListGrid_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_ListGrid_0]: orderDetailGrid.dataLoading = true
 15:16:44.228:TMR2:DEBUG:ruleContext:isc_ListGrid_0:provideRuleContext [ruleScope: isc_DataView_0, dbcID: isc_ListGrid_0]: orderDetailGrid.dataLoading = null
 
```

**Flags**: IR

---
## Attr: Canvas.snapResizeToGrid

### Description
Causes this canvas to snap to its parent's grid when resizing. Note that this value defaults to the Canvas's [snapToGrid](#attr-canvassnaptogrid) value if undefined.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.name

### Description
Optional name for the canvas, which can later be used to reference it. Need not be globally unique, but should be unique within the [parent](#attr-canvasparentcanvas) to get defined results for [Layout.getMember](Layout.md#method-layoutgetmember) and [Layout.getMemberNumber](Layout.md#method-layoutgetmembernumber).

### See Also

- [Canvas.ID](#attr-canvasid)

**Flags**: IR

---
## Attr: Canvas.noDropCursor

### Description
Specifies the cursor image to display when the user drags a droppable canvas over this if it is not a valid drop target for the event and [EventHandler.showNoDropIndicator](EventHandler.md#classattr-eventhandlershownodropindicator) is true.

### Groups

- cues

**Flags**: IRWA

---
## Attr: Canvas.className

### Description
The CSS class applied to this widget as a whole.

### Groups

- appearance

**Deprecated**

**Flags**: IRW

---
## Attr: Canvas.animateHideAcceleration

### Description
Default acceleration function for performing an animated hide. If unset, `this.animateAcceleration` will be used by default instead

### Groups

- animation

**Flags**: IRWA

---
## Attr: Canvas.hoverWrap

### Description
If `this.showHover` is true, this property can be used to customize the whether content in the hover canvas is displayed in a single line, or wraps.

Note that if developers wish to have hovers expand horizontally to fit their text without wrapping \*up to some maximum\*, and then wrap rather than exceeding that maximum, the [Canvas.hoverAutoFitWidth](#attr-canvashoverautofitwidth) and [Canvas.hoverAutoFitMaxWidth](#attr-canvashoverautofitmaxwidth) attributes may be used instead of simply setting hoverWrap to false.

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.dragAppearance

### Description
Visual appearance to show when the object is being dragged. May be overridden for dragResize or dragReposition events via [Canvas.dragResizeAppearance](#attr-canvasdragresizeappearance) and [Canvas.dragRepositionAppearance](#attr-canvasdragrepositionappearance).

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Canvas.hoverAutoDestroy

### Description
If `this.showHover` is true and [Canvas.getHoverComponent](#method-canvasgethovercomponent) is implemented, should the hoverCanvas returned from it be automatically destroyed when it is hidden?

The default of null indicates that the component **will** be automatically destroyed. Set to false to prevent this.

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

**Flags**: IRW

---
## Attr: Canvas.dragScrollDelay

### Description
If this widget supports drag-scrolling, This property specifies how many ms the user must hover over the drag-scroll threshold before scrolling begins.

### Groups

- dragging

**Flags**: IRWA

---
## Attr: Canvas.disabled

### Description
If set to true, the widget will be disabled. A widget is only considered enabled if it is individually enabled and all parents above it in the containment hierarchy are enabled. This allows you to enable or disable all components of a complex nested widget by enabling or disabling the top-level parent only.

### Groups

- enable

**Flags**: IRW

---
## Attr: Canvas.edgeOpacity

### Description
Opacity of the edges. Defaults to matching this.opacity. if [Canvas.setOpacity](#method-canvassetopacity) is called on a Canvas where edgeOpacity is set, edgeOpacity will be considered a percentage of the parent's opacity (so 50% opaque parent plus edgeOpacity 50 means 25% opaque edges)

### Groups

- imageEdges

**Flags**: IR

---
## Attr: Canvas.showSnapGrid

### Description
Whether to show a snap grid for this Canvas. Note that the grid is only shown when either [childrenSnapToGrid](#attr-canvaschildrensnaptogrid) or [childrenSnapResizeToGrid](#attr-canvaschildrensnapresizetogrid) is `true`.

Grid is based on [snapHGap](#attr-canvassnaphgap) and [snapVGap](#attr-canvassnapvgap) properties.

### Groups

- snapGridDragging

**Flags**: IRW

---
## Attr: Canvas.snapEdge

### Description
If [snapTo](#attr-canvassnapto) is defined to this widget, this property can be used to define which edge of this widget should be snapped to an edge of the master or parent element.

If unspecified the, default snapTo behavior is set up to align the "snapTo" edge of this widget with the snapTo edge of the master or parent.

### Groups

- snapPositioning

### See Also

- [Canvas.snapTo](#attr-canvassnapto)

**Flags**: IRW

---
## Attr: Canvas.minHeight

### Description
Minimum height available to this Canvas. Minimum sizes do not apply to all situations. See [Canvas.minWidth](#attr-canvasminwidth) for details.

### Groups

- sizing

### See Also

- [Canvas.dragMinHeight](#attr-canvasdragminheight)

**Flags**: IRWA

---
## Attr: Canvas.adaptiveHeightPriority

### Description
See [Canvas.adaptiveWidthPriority](#attr-canvasadaptivewidthpriority).

**Flags**: IR

---
## Attr: Canvas.showHover

### Description
If `this.canHover` is true, should we show the global hover canvas by default when the user hovers over this canvas?

### Groups

- hovers

### See Also

- [Canvas.getHoverHTML](#method-canvasgethoverhtml)

**Flags**: IRW

---
## Attr: Canvas.updateTabPositionOnDraw

### Description
Should canvases with no [parent canvas](#method-canvasgetparentcanvas) be moved to the end of the TabIndexManager tree on draw()?

If set to false, the tab-position will not be modified on draw.

This property is useful for cases where the tab position of a widget will be managed by some explicit tabIndex management code.

**Flags**: IRWA

---
## Attr: Canvas.useDragMask

### Description
This flag controls whether we register the component as a maskable item with the EventHandler. If enabled, a backmask will be automatically created for the dragMoveTarget on the fly to avoid burnthrough e.g. by plugins or frames.

Note that this property will be defaulted to false unless the canvas contains an IFrame, in which case it will be defaulted to true.

The [Canvas.dragMaskType](#attr-canvasdragmasktype) property controls what kind of mask is used in case useDragMask is enabled.

### Groups

- dragdrop

**Flags**: IRW

---
## ClassMethod: Canvas.getSnapPosition

### Description
Return the position for `snapper` to be placed in order to "snap to" an edge or corner of `target`, in the same sense as [Canvas.snapTo](#attr-canvassnapto).

Default for `snapEdge` is the **opposite** edge or corner from `snapTo`. For example, `snapTo` of "T" (top) means `snapEdge` will default to "B" (bottom), so the returned coordinates would place `snapper` centered along the top edge of `target`. A `snapTo` of "TL" (top left) means `snapEdge` will default to "BR" (bottom right), so the returned coordinates would place the bottom right of `snapper` at the top left corner of `target`.

`target` can be passed as either a Canvas or 4-element Array giving the top, left, width and height of the target. `snapper` can be passed as either a Canvas or a two-element Array of the width and height of the rectangle to be placed.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| target | [Canvas](#type-canvas)|[Array of Integer](#type-array-of-integer) | false | — | canvas to snap to |
| snapTo | [String](#type-string) | false | — | edge against which to snap |
| snapper | [Canvas](#type-canvas)|[Array of Integer](#type-array-of-integer) | false | — | canvas being snapped |
| snapEdge | [String](#type-string) | true | — | optional edge to snapTo. Default is the **opposite** edge or corner from `snapTo` |

### Returns

`[Point](#type-point)` — the position for `snapper` to be placed in order to "snap to" an edge or corner of `target`

### Groups

- snapPositioning

---
## ClassMethod: Canvas.showPrintPreview

### Description
Generate and show a [PrintWindow](../reference.md#class-printwindow) containing a [PrintCanvas](PrintCanvas.md#class-printcanvas) showing a printable view of the components passed in.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| components | [Array of Canvas](#type-array-of-canvas) | false | — | components to get the print HTML for. May also include raw HTML strings which will be folded into the generated print output |
| printProperties | [PrintProperties](#type-printproperties) | true | — | PrintProperties object for customizing the print HTML output |
| printWindowProperties | [PrintWindow Properties](#type-printwindow-properties) | true | — | Properties to apply to the generated print window. |
| callback | [Callback](../reference.md#type-callback) | true | — | callback to fire when the print preview canvas has been populated with the printable HTML. This callback takes 2 parameters: `printPreview` - a pointer to the generated print canvas shown in the body of the print window. `printWindow` - a pointer to the generated print window and |
| separator | [String](#type-string) | true | — | Optional HTML separator to render between each component's printable HTML |

### Groups

- printing

---
## ClassMethod: Canvas.getPrintPreview

### Description
Creates a printCanvas containing the full printHTML for a series of components, passing it as an argument to the callback (if supplied) when it fires. Note that the generated preview canvas will be drawn automatically by this method. Developers may also explicitly create a PrintCanvas instance and populate it with HTML derived from the [Canvas.getPrintHTML](#method-canvasgetprinthtml) for finer grained control over when the print canvas is drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| components | [Array of Canvas](#type-array-of-canvas) | false | — | components to get the print HTML for. May also include raw HTML strings which will be folded into the generated print output |
| printProperties | [PrintProperties](#type-printproperties) | true | — | PrintProperties object for customizing the print HTML output |
| previewProperties | [Canvas Properties](#type-canvas-properties) | true | — | properties to apply to the generated printPreview Canvas. |
| callback | [PrintCanvasCallback](#type-printcanvascallback) | true | — | callback to fire when the print preview canvas has been populated with the printable HTML. The generated canvas will be passed to the callback as a single `printPreview` parameter. |
| separator | [String](#type-string) | true | — | optional string of HTML to render between each component |

### Groups

- printing

---
## ClassMethod: Canvas.setAutoResizeAutoChildAttributes

### Description
Should registered autoChild attributes be automatically resized with [controls](#classmethod-canvasresizecontrols) and [text](#classmethod-canvasresizefonts)?

If true, attributes registered for resize with policy `"controls"` will be resized when `resizeControls()` runs, and icons registered with policy `"fonts"` will resize when `resizeFonts()` runs.

To resize autoChild attributes with other policies, developers should call [Canvas.resizeAutoChildAttributes](#classmethod-canvasresizeautochildattributes) directly

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoResize | [boolean](../reference.md#type-boolean) | false | — | true if attributes should be auto-resized |

---
## ClassMethod: Canvas.resizeControlsTo

### Description
Resizes controls as if calling [Canvas.resizeControls](#classmethod-canvasresizecontrols), but takes a final target size instead of a delta representing the change from a current size. Note that all the same limitations apply.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetDelta | [int](../reference.md#type-int) | false | — | the final size, expressed as a differential from the default |

---
## ClassMethod: Canvas.setAllowExternalFilters

### Description
Changes the system-wide [Canvas.allowExternalFilters](#classattr-canvasallowexternalfilters) setting.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| allExternalFilters | [boolean](../reference.md#type-boolean) | false | — | new setting |

### Groups

- IEFilters

---
## ClassMethod: Canvas.resizePadding

### Description
Modify the amount of padding for some CSS styles defined for the page. Only CSS styles registered by [Canvas.registerFontScaledPaddingStyles](#classmethod-canvasregisterfontscaledpaddingstyles) are modified.

`resizePadding()` must be called after the skin has been loaded, and before any components have been created. Calling `resizePadding()` at a later time is not supported (you will notice that padding is modified, however, this approach is not supported).

This method has similar browser security limitations as [Canvas.resizeFonts](#classmethod-canvasresizefonts).

The intent is that the same font size change be passed to this method as is passed to [Canvas.resizeFonts](#classmethod-canvasresizefonts), so that the `targetSizeChange` in the call to [Canvas.registerFontScaledPaddingStyles](#classmethod-canvasregisterfontscaledpaddingstyles) represents the right font size for the unadjusted styles being registered.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fontSizeChange | [int](../reference.md#type-int) | false | — | size change to apply to the padding of registered styles, so that they aren't changed at all at the size change passed to [Canvas.registerFontScaledPaddingStyles](#classmethod-canvasregisterfontscaledpaddingstyles), and the padding is reduced to baseline style levels at a zero size change. |
| styleSheets | [String](#type-string) | true | — | optional regular expression pattern for matching stylesheets |

### See Also

- [Canvas.resizeFonts](#classmethod-canvasresizefonts)
- [Canvas.resizeControls](#classmethod-canvasresizecontrols)

---
## ClassMethod: Canvas.resizeIcons

### Description
Change the basic size of icons in the current skin by "delta" pixels. This method may be invoked automatically from [Canvas.resizeControls](#classmethod-canvasresizecontrols).

Must be called after the skin has been loaded, but before any components are created.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| policy | [String](#type-string) | false | — | Which set of icons should be resized? This should correspond to the iconSizingPolicy argument applied when [registering the icon sizing attributes](#classmethod-canvasregistericonsizingattributes). |
| delta | [int](../reference.md#type-int) | false | — | number of pixels to increase or decrease from current size |

---
## ClassMethod: Canvas.getPrintHTML

### Description
Returns print-formatted HTML for the specified list of components.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| components | [Array of Canvas](#type-array-of-canvas) | false | — | Components to get the print HTML for. Strings of raw HTML may also be included in this array, and will be integrated into the final HTML at the appropriate point. |
| printProperties | [PrintProperties](#type-printproperties) | false | — | properties affecting print output |
| callback | [Callback](../reference.md#type-callback) | true | — | Callback to fire when the method completes. The generated print HTML will be passed in as the first parameter `HTML`. |
| separator | [HTMLString](../reference.md#type-htmlstring) | true | — | Optional HTML separator to render between each component's printable HTML |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — print HTML for the components passed in. This will be `null` if a callback parameter was passed into this method, or if the print HTML was generated asynchronously by the component\[s\].

---
## ClassMethod: Canvas.resizeFontsTo

### Description
Resizes fonts as if calling [Canvas.resizeFonts](#classmethod-canvasresizefonts), but takes a final target size instead of a delta representing the change from a current size. Note that all the same limitations apply.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| targetDelta | [int](../reference.md#type-int) | false | — | the final size, expressed as a differential from the default |

---
## ClassMethod: Canvas.resizeFonts

### Description
Modify the size of fonts for some or all stylesheets defined in the page.

This method can be used to dynamically increase or decrease font size for all of the fonts in your application, or just fonts defined in your chosen SmartClient skin (the latter can be achieved by passing `styleSheets` as "skin\_styles.css" - the default name for the CSS file used in each SmartClient skin).

`resizeFonts()` must be called after the skin has been loaded, and before any components have been created. Calling `resizeFonts()` at a later time is not supported (you will notice that font sizes still increase, however, this approach is not supported).

Some browsers will disallow access or modification of styleSheets if they are loaded from a domain that is different from the loading page. In this case `resizeFonts()` cannot be used.

This method has a small performance penalty which depends on the browser, number of stylesheets being modified, and age of your machine. With modern browsers on modern machines resizing just skin fonts, the impact is basically negligible (<5ms).

Certain controls such as icons are resized when fonts are resized (see [Canvas.setAutoResizeIcons](#classmethod-canvassetautoresizeicons) and [Canvas.setAutoResizeAutoChildAttributes](#classmethod-canvassetautoresizeautochildattributes)) so you might want to set `resizeRelatedControls` to `false` where you are just trying to make fonts in a dynamically loaded stylesheet match previously loaded fonts, but controls such as icons should not be resized upwards again.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sizeChange | [int](../reference.md#type-int) | false | — | size to change fonts by. Can be negative to shrink fonts |
| styleSheets | [String](#type-string) | true | — | optional regular expression pattern for matching stylesheets |
| resizeRelatedControls | [Boolean](#type-boolean) | true | — | resize icons and autoChild attributes? Set to false to suppress default behavior. |

---
## ClassMethod: Canvas.printComponents

### Description
Generate printable HTML for the designated components and trigger the native print dialog, without never showing the printable HTML to the user.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| components | [Array of Canvas](#type-array-of-canvas) | false | — | components to get the print HTML for. May also include raw HTML strings which will be folded into the generated print output |
| printProperties | [PrintProperties](#type-printproperties) | true | — | object for customizing the print HTML output |

### Groups

- printing

---
## ClassMethod: Canvas.setAutoResizeIcons

### Description
Should icons be automatically resized with [controls](#classmethod-canvasresizecontrols) and [text](#classmethod-canvasresizefonts)?

If true, icon attributes registered for resize with policy `"controls"` will be resized when `resizeControls()` runs, and icons registered with policy `"fonts"` will resize when `resizeFonts()` runs.

To resize icons with other policies, developers should call [Canvas.resizeIcons](#classmethod-canvasresizeicons) directly

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoResizeIcons | [boolean](../reference.md#type-boolean) | false | — | true if icons should be auto-resized |

---
## ClassMethod: Canvas.hiliteCharacter

### Description
Given a string and a character, hilite the first occurrence of the character in the string (if it occurs), preferring uppercase to lowercase.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| string | [String](#type-string) | false | — | String to return with hilited character |
| character | [Character](#type-character) | false | — | Character to hilite |
| hilitePrefix | [String](#type-string) | true | — | Prefix to apply to hilighted character - defaults to "`<span style='text-decoration:underline;'>`" |
| hiliteSuffix | [String](#type-string) | true | — | Suffix to apply to hilited character - defaults to "`</span>`" |

### Returns

`[String](#type-string)` — The string passed in, with the first occurrence of the hilite character enclosed by the 'hilitePrefix' and 'hiliteSuffix'

### Groups

- utils

**Flags**: A

---
## ClassMethod: Canvas.resizeAutoChildAttributes

### Description
Change the value of attributes registered via [Canvas.registerAutoChildSizingAttributes](#classmethod-canvasregisterautochildsizingattributes) by some number of pixels. This method may be invoked automatically from [Canvas.resizeControls](#classmethod-canvasresizecontrols) or [Canvas.resizeFonts](#classmethod-canvasresizefonts)

Must be called after the skin has been loaded, but before any components are created.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| policy | [String](#type-string) | false | — | Which set of attributes should be resized? This should correspond to the sizing policy argument applied when [registering the icon sizing attributes](#classmethod-canvasregisterautochildsizingattributes). |
| delta | [int](../reference.md#type-int) | false | — | number of pixels to increase or decrease from current size |

---
## ClassMethod: Canvas.registerAutoChildSizingAttributes

### Description
Register numeric or measure type properties of on autoChild properties blocks for some class(es). These are properties that should be adjusted when [Canvas.resizeAutoChildAttributes](#classmethod-canvasresizeautochildattributes) is called. Typically these will consist of width and height attributes on some autoChild defaults block for some SmartClient class, such as `Window.closeButtonDefaults` (to modify width and height of [Window.closeButton](Window.md#attr-windowclosebutton)).

As with [Canvas.registerIconSizingAttributes](#classmethod-canvasregistericonsizingattributes), the policy parameter allows attributes to be grouped together into sets so particular types of UI element can be resized in a targeted manner. For example, the width and height of an icon which will appear aligned with a line of text would typically want to be resized at the same time as font sizes are adjusted, whereas an icon that corresponds to a block of control UI (such as a picker icon that sits outside of an associated FormItem), should be resized when that control element is resized.

A policy can be any string. To modify the sizes of attributes registered under some policy, that same policy string should be passed to the [Canvas.resizeAutoChildAttributes](#classmethod-canvasresizeautochildattributes) method.

The className should be the name of the class on which the auto child properties block exists.

The attributes parameter consists of a JavaScript object where each key specifies the name of the autoChild properties block to modify, with its value set to an array, indicating the attribute(s) to register.

Sizing attributes can be specified individually or in pairs. When a single attribute passed in, a call to [Canvas.resizeAutoChildAttributes](#classmethod-canvasresizeautochildattributes) will modify that attribute by the `delta` parameter. If a pair of attributes is passed in, this is assumed to be a _height,width_ pair. When [Canvas.resizeAutoChildAttributes](#classmethod-canvasresizeautochildattributes) is called in this case, both attributes will be modified such that they maintain the same scale. In other words, the first registered attribute (typically the height) will be adjusted by the specified `delta` (a simple numeric adjustment). The second attribute will be adjusted by a numeric delta calculated to have the same ratio to the original width as the provided delta had to the original height. This allows icons to be resized without becoming distorted.

For example, the following code would register the attributes "width" and "height" properties on the `"closeButtonDefaults"` properties block, within the Window class - thus customizing the default size of the [Window.closeButton](Window.md#attr-windowclosebutton) autoChild. It registers them as part of the "controls" policy.

```
 isc.Canvas.registerAutoChildSizingAttributes(
   "fonts",
   "Window",
   {
      closeButtonDefaults:[
          ["height", "width"]
      ]
   }
 );
 
```

The [autoResizeAutoChildAttributes](#classmethod-canvassetautoresizeautochildattributes) feature will cause registered autoChild attributes to resize automatically. Those registered with policy `"controls"` to be resized when [Canvas.resizeControls](#classmethod-canvasresizecontrols) is run and attributes registered as `"fonts"` to be resized when [Canvas.resizeFonts](#classmethod-canvasresizefonts) is run.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| policy | [String](#type-string) | false | — | Sizing policy for this set of attributes |
| className | [String](#type-string) | false | — | Name of the class containing the autoChild configuration block to edit |
| attributes | [Object](../reference.md#type-object) | false | — | The attribute(s) to register for resizing. |

---
## ClassMethod: Canvas.resizeControls

### Description
Change the basic size of UI components in the current skin by "delta" pixels. Must be called after the skin has been loaded, but before any components are created.

In general, this method changes the _height_ of various controls, except for certain controls that appear in alternate orientations (such as resizeBars and tabs), in which case thickness properties (resizeBarThickness, tabBarThickness) are adjusted.

The height of a text input control implies the height of most other controls:

*   all other FormItems (eg selects) need to be the same height or mixed controls will look odd. This includes Buttons
*   anything that potentially contains a FormItem needs to be as tall or slightly taller: this includes grid row (inline editing), [Window headers](Window.md#attr-windowheadercontrols), TabBar and SectionHeaders

Because of this necessary uniformity, just specifying a single pixel value is enough for the framework to resize all core controls, with several caveats:

*   skins that make extensive use of images (eg TreeFrog) will stretch those images, which may result in ugly artifacts in some combinations of operating system and browser, for which no workaround is possible. For this reason, `resizeControls()` is only officially supported in [CSS3 Mode](../kb_topics/skinning.md#kb-topic-skinning--theming), which includes any of the skins in our `Flat series` (Tahoe, Stratus, Obsidian and Twilight) or `Enterprise series` (Enterprise/Blue and Graphite), or a custom skin based on one of those - including any skin generated by the `Skin Editor`.
*   even in Enterprise-series skins, [tree connector lines](TreeGrid.md#attr-treegridshowconnectors) vertically stretch, becoming obviously blurry and misshapen with an increase of 4-5px. To avoid this, replace the tree connector media (see [TreeGrid.connectorImage](TreeGrid.md#attr-treegridconnectorimage)).
*   [FormItemIcon](../reference.md#object-formitemicon)s are not resized by default, because stretched icons generally look worse than non-scaled icons that are a bit smaller than the input field
*   images that use [spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) will not be stretched because the sizes for these controls are embedded in CSS. In most cases, this is desirable; for example, the downward chevron shape used for SelectItem controls doesn't stretch, and looks better that way.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| delta | [int](../reference.md#type-int) | false | — | number of pixels to increase or decrease from current size |

---
## ClassMethod: Canvas.setNeverUseFilters

### Description
Changes the system-wide [Canvas.neverUseFilters](#classattr-canvasneverusefilters) setting.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| neverUseFilters | [boolean](../reference.md#type-boolean) | false | — | new setting |

### Groups

- IEFilters

---
## ClassMethod: Canvas.setShowCustomScrollbars

### Description
Whether to use the browser's native scrollbars or SmartClient-based scrollbars by default for all canvases.

This method changes the default value of [Canvas.showCustomScrollbars](#attr-canvasshowcustomscrollbars).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showCustomScrollbars | [boolean](../reference.md#type-boolean) | false | — | whether to show custom (SmartClient-based) scrollbars rather than css-scrollbars by default. |

---
## ClassMethod: Canvas.getById

### Description
Retrieve a Canvas by it's global [ID](#attr-canvasid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | false | — | global ID of the Canvas |

### Returns

`[Canvas](#type-canvas)` — the Canvas, or null if not found

---
## ClassMethod: Canvas.registerFontScaledPaddingStyles

### Description
Registers one or more CSS classes to have their padding adjusted (independently on all edges) according to the [padding size change](#classmethod-canvasresizepadding) applied to the page. Each class to be registered is provided along with a corresponding baseline class, and a single `targetSizeChange` is specified for all the classes. The padding in each registered class is adjusted downward towards the baseline as the padding size change approaches 0 (no resizing), and upward as it increases, so that it exactly equals the declared style's padding at a padding size change of `targetSizeChange`.

Note that each call to this method replaces the registration of the previous call (if any), and will have no effect until [Canvas.resizePadding](#classmethod-canvasresizepadding) is called.

For example:

```
    isc.Canvas.registerFontScaledPaddingStyles(
        [        "tabButtonTop",         "tabButtonBottom"], 
        ["iconOnlyTabButtonTop", "iconOnlyTabButtonBottom"],
        3
    );
 
```
In this case, the CSS style "tabButtonTop" will have its padding adjusted downward to the padding from the baseline CSS style "iconOnlyTabButtonTop" style at a `sizeChange` of 0, and be left unchanged at a `sizeChange` of 3.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| scaledStyles | [Array of CSSStyleName](#type-array-of-cssstylename) | false | — | styles whose padding should be adjusted |
| baselineStyles | [Array of CSSStyleName](#type-array-of-cssstylename) | false | — | corresponding baseline reference styles |
| targetSizeChange | [int](../reference.md#type-int) | false | — | sizeChange at which scaledStyles are unchanged |

### See Also

- [Canvas.resizeFonts](#classmethod-canvasresizefonts)
- [Canvas.resizePadding](#classmethod-canvasresizepadding)
- [Canvas.resizeControls](#classmethod-canvasresizecontrols)
- [Canvas.registerIconSizingAttributes](#classmethod-canvasregistericonsizingattributes)

---
## ClassMethod: Canvas.registerIconSizingAttributes

### Description
Register numeric or measure type properties of some class(es) as "icon sizing attributes". These are properties that should be adjusted when [Canvas.resizeIcons](#classmethod-canvasresizeicons) is called. Typically these will consist of icon width and height attributes on some SmartClient class, such as [ListGrid.checkboxFieldImageHeight](ListGrid_1.md#attr-listgridcheckboxfieldimageheight) and [ListGrid.checkboxFieldImageWidth](ListGrid_1.md#attr-listgridcheckboxfieldimagewidth).

The policy parameter allows icons to be grouped together into sets so particular types of UI element can be resized in a targeted manner. For example, the width and height of an icon which will appear aligned with a line of text would typically want to be resized at the same time as font sizes are adjusted, whereas an icon that corresponds to a block of control UI (such as a picker icon that sits outside of an associated FormItem), should be resized when that control element is resized.

A policy can be any string. To modify the sizes of attributes registered under some policy, that same policy string should be passed to the [Canvas.resizeIcons](#classmethod-canvasresizeicons) method.

The attributes parameter consists of a JavaScript object where each key specifies the name of the class on which the attributes, with its value set to an array, indicating the attribute(s) to register within that class.

Icon sizing attributes can be specified individually or in pairs. When a single attribute passed in, a call to [Canvas.resizeIcons](#classmethod-canvasresizeicons) will modify that attribute by the `delta` parameter. If a pair of attributes is passed in, this is assumed to be a _height,width_ pair. When [Canvas.resizeIcons](#classmethod-canvasresizeicons) is called in this case, both attributes will be modified such that they maintain the same scale. In other words, the first registered attribute (typically the height) will be adjusted by the specified `delta` (a simple numeric adjustment). The second attribute will be adjusted by a numeric delta calculated to have the same ratio to the original width as the provided delta had to the original height. This allows icons to be resized without becoming distorted.

For example, the following code would register FormItem attributes "valueIconSize", "valueIconWidth" and "valueIconHeight" for resizing as part of the "fonts" policy, such that both "valueIconSize" and "valueIconHeight" would be changed by the value passed to `resizeIcons(..)`, and "valueIconWidth" would be changed such that the width/height ratio was retained.

```
 isc.Canvas.registerIconSizingAttributes(
   "fonts",
   {
      FormItem:[
          "valueIconSize",
          ["valueIconHeight", "valueIconWidth"]
      ]
   }
 );
 
```

The [autoResizeIcons](#classmethod-canvassetautoresizeicons) feature will cause icon attributes registered with policy `"controls"` to be resized when [Canvas.resizeControls](#classmethod-canvasresizecontrols) is run and attributes registered as `"fonts"` to be resized when [Canvas.resizeFonts](#classmethod-canvasresizefonts) is run.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| policy | [String](#type-string) | false | — | Icon sizing policy for this set of attributes |
| attributes | [Object](../reference.md#type-object) | false | — | The attribute(s) to register for resizing. |

---
## ClassMethod: Canvas.getEventEdge

### Description
Check if an event is within an "edge" of this canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| edgeMask | [Array of EdgeName](#type-array-of-edgename) | true | — | Array of legal edges. Default is all the edges that allow resizing (see [Canvas.resizeFrom](#attr-canvasresizefrom)) |

### Returns

`[EdgeName](../reference.md#type-edgename)` — edge where the mouse is positioned, or null if not within a legal edge (including being in the center)

### Groups

- dragdrop
- dragResize

### See Also

- [Canvas.resizeFrom](#attr-canvasresizefrom)

---
## ClassMethod: Canvas.setDefaultPageSpace

### Description
Changes the global [Canvas.defaultPageSpace](#classattr-canvasdefaultpagespace).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newDefaultPageSpace | [int](../reference.md#type-int) | false | — | the new value for `defaultPageSpace`. |

**Flags**: A

---
## ClassMethod: Canvas.imgHTML

### Description
Generates the HTML for an image. Also available at the [instance level](#method-canvasimghtml).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| src | [SCImgURL](../reference.md#type-scimgurl) | false | — | URL local to the skin or application directory.  
NOTE: instead of passing several parameters, you can pass an object as the 'src' parameter with properties for all the various function parameters with, eg:  
canvas.imgHTML( {src:"foo", width:10, height:10} ); |
| width | [number](#type-number) | true | — | width of the image |
| height | [number](#type-number) | true | — | height of the image |
| name | [String](#type-string) | true | — | name for the image |
| extraStuff | [String](#type-string) | true | — | additional attributes to write in the tag |
| imgDir | [String](#type-string) | true | — | image-specific image directory |

### Returns

`[String](#type-string)` — HTML to draw the image.

### Groups

- images

**Flags**: A

---
## Method: Canvas.visibilityChanged

### Description
Notification fired when this canvas becomes visible or hidden to the user. Note - this method is fired when the [Canvas.isVisible](#method-canvasisvisible) state of this component changes. It may be fired in response an explicit call to [Canvas.show](#method-canvasshow) or [Canvas.hide](#method-canvashide), or in response to a parent component being shown or hidden when this widgets [Canvas.visibility](#attr-canvasvisibility) is set to "inherit".

Note that a call to [Canvas.show](#method-canvasshow) or [Canvas.hide](#method-canvashide) will not **always** fire this notification. If this widget has a hidden parent, show or hide would change this components [Canvas.visibility](#attr-canvasvisibility) property, and may update the CSS visibility attribute of the drawn handle in the DOM, but would not actually hide or reveal the component to the user and as such the notification would not fire.

Note also that this notification will only be fired for components which have been [drawn](#method-canvasdraw).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| isVisible | [boolean](../reference.md#type-boolean) | false | — | whether the canvas is visible to the user |

---
## Method: Canvas.dragResizeMove

### Description
Executed every time the mouse moves while drag-resizing. If this method does not return false, the [Canvas.dragTarget](#attr-canvasdragtarget) (or outline if [Canvas.dragAppearance](#attr-canvasdragappearance) is set to "outline") will automatically be moved as appropriate whenever the mouse moves.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress auto-resize of the [Canvas.dragTarget](#attr-canvasdragtarget) or outline.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)
- [EventHandler.getDragRect](EventHandler.md#classmethod-eventhandlergetdragrect)

**Flags**: A

---
## Method: Canvas.animateResize

### Description
Animate a resize of this canvas from its current size to the specified size

Note that [Canvas.animateResizeLayoutMode](#attr-canvasanimateresizelayoutmode) allows you to control whether child layout is rerun during every step of the animation, or just at the end, since the former may incur significant overhead depending on the widget hierarchy.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Integer](../reference_2.md#type-integer) | false | — | new width (or null for unchanged) |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height (or null for unchanged) |
| callback | [AnimationCallback](#type-animationcallback) | true | — | When the resize completes this callback will be fired. Single 'earlyFinish' parameter will be passed if the animation was cut short, for example by a call to the non-animated APIs [Canvas.resizeTo](#method-canvasresizeto) or [Canvas.resizeBy](#method-canvasresizeby). |
| duration | [Integer](../reference_2.md#type-integer) | true | — | Duration in ms of the animated resize |
| acceleration | [AnimationAcceleration](../reference.md#type-animationacceleration) | true | — | Optional acceleration effect to apply to the resize |

### Groups

- animation

---
## Method: Canvas.getContents

### Description
Returns the contents of a Canvas. The contents are an HTML string.

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — contents of this Canvas

---
## Method: Canvas.shouldDragScroll

### Description
If this widget is showing scrollbars, and a user drags close to the edge of the viewport, should we scroll the viewport in the appropriate direction? Returns this.canDragScroll if there are scrollbars, else false.

### Groups

- events
- dragdrop

**Flags**: A

---
## Method: Canvas.moveTo

### Description
Moves the widget so that its top-left corner is at the specified coordinates.

This method will also accept a single parameter as an object array with left and top given as properties.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number)|[Object](../reference.md#type-object) | true | — | x-coordinate to move to in LOCAL coordinates or Object with left and top properties. |
| top | [number](#type-number) | true | — | y-coordinate to move to in LOCAL coordinates |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the component actually moved

### Groups

- positioning

---
## Method: Canvas.getWidth

### Description
Return the width of this object, in pixels.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[Number](#type-number)` — width

### Groups

- sizing

---
## Method: Canvas.setBottom

### Description
Resizes the widget vertically to position its bottom edge at the specified coordinate.

NOTE: if you're setting multiple coordinates, use setRect(), moveTo() or resizeTo() instead

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| bottom | [number](#type-number) | false | — | new bottom coordinate |

### Groups

- sizing

---
## Method: Canvas.encloses

### Description
Returns true if the rectangle of this widget encloses the rectangle of the specified widget.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| other | [Canvas](#type-canvas) | false | — | other canvas to test for enclosure |

### Returns

`[Boolean](#type-boolean)` — true if this canvas encloses other; false otherwise

### Groups

- positioning

---
## Method: Canvas.pageScrollUp

### Description
This method is the programmatic equivalent of the user pressing the "Page Up" key while this widget has the focus. It scrolls the widget's content upwards by the viewport height, if the content can be scrolled that far upwards

---
## Method: Canvas.setAriaState

### Description
Set a specific [ARIA state](#attr-canvasariastate) for this component.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| stateName | [String](#type-string) | false | — | aria state to update |
| stateValue | [String](#type-string)|[Boolean](#type-boolean)|[Integer](../reference_2.md#type-integer)|[Float](../reference.md#type-float) | false | — | value for the aria state |

### Groups

- accessibility

---
## Method: Canvas.dropOut

### Description
Executed when the dragged object is no longer over this drop target, including when the drag interaction is ending with a drop on this drop target. If you have set a visual indication in dropOver or dropMove, you should reset it to its normal state in dropOut.

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.linkHTML

### Description
Generates the HTML for a standard link (anchor) element.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| href | [String](#type-string) | false | — | URL for the link to point to |
| text | [HTMLString](../reference.md#type-htmlstring) | true | — | HTML to display in the link element (defaults to the href) |
| target | [String](#type-string) | true | — | Target window for the link (defaults to opening in a new, unnamed window) |
| ID | [String](#type-string) | true | — | optional ID for the link element to be written out |
| tabIndex | [Integer](../reference_2.md#type-integer) | true | — | optional tabIndex for the link |
| accessKey | [String](#type-string) | true | — | optional accessKey for the link |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML for the link

**Flags**: A

---
## Method: Canvas.getViewportWidth

### Description
Returns the width of the viewport onto the scrollable content.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — width of the viewport, in pixels

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.dragMove

### Description
Executed every time the mouse moves while dragging this canvas.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel drag interaction.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.moveBy

### Description
Moves the widget deltaX pixels to the right and deltaY pixels down. Pass negative numbers to move up and/or to the left.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| deltaX | [int](../reference.md#type-int) | false | — | amount to move horizontally (may be negative) |
| deltaY | [int](../reference.md#type-int) | false | — | amount to move vertically (may be negative) |

### Returns

`[Boolean](#type-boolean)` — whether the component actually moved

### Groups

- positioning

---
## Method: Canvas.enable

### Description
Enables this widget and any children / peers of this widget.

### Groups

- enable

---
## Method: Canvas.moveBelow

### Description
Puts this widget just below the specified widget in the stacking order, so it appears behind the specified widget if both widgets have the same parent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [Canvas](#type-canvas) | false | — | canvas to move below |

### Groups

- zIndex

---
## Method: Canvas.enclosesRect

### Description
Returns true if the rectangle of this widget encloses the rectangle coordinates passed in, and false otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number)|[Array of number](#type-array-of-number) | false | — | left coord of rect (or rect array) |
| top | [number](#type-number) | false | — | top coord of rect |
| width | [number](#type-number) | false | — | width of rect |
| height | [number](#type-number) | false | — | height of rect |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this canvas encloses the rectangle passed in; false otherwise

### Groups

- positioning

---
## Method: Canvas.getImgURL

### Description
Return the full URL for an image to be drawn in this canvas.

If the passed URL begins with the special prefix "\[SKIN\]", it will have the widget.skinImgDir and Page.skinImgDir prepended. Otherwise the image is assumed to be application-specific, and will have the widget.appImgDir and Page.appImgDir automatically prepended.

Note that if passed an absolute path (starting with "/" or "http://" for example), no extra image directory information will be prepended to the generated URL.//

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [String](#type-string) | false | — | URL local to skin or application image directory |
| imgDir | [String](#type-string) | true | — | optional image directory to override the default for this Canvas |

### Returns

`[String](#type-string)` — URL to use

### Groups

- images

**Flags**: A

---
## Method: Canvas.mouseWheel

### Description
Executed when the mouse wheel is actuated.

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [EventHandler.getWheelDelta](EventHandler.md#classmethod-eventhandlergetwheeldelta)
- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.setShowPointer

### Description
Set the showPointer property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../reference.md#type-boolean) | false | — | — |

---
## Method: Canvas.clickMaskUp

### Description
Determines whether a clickmask is showing

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | true | — | optional ID of specific clickMask to check. If not passed, checks for the click mask associated with this widget only. |

### Returns

`[Boolean](#type-boolean)` — whether or not a clickmask is showing

### Groups

- clickMask

### See Also

- [Canvas.showClickMask](#method-canvasshowclickmask)

---
## Method: Canvas.getSnapTo

### Description
Return the snapTo value of this object

### Returns

`[String](#type-string)` — snapTo

### Groups

- snapPositioning

---
## Method: Canvas.setCanFocus

### Description
Change whether a widget can accept keyboard focus.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canFocus | [boolean](../reference.md#type-boolean) | false | — | whether the widget should now accept focus |

### See Also

- [Canvas.canFocus](#attr-canvascanfocus)

**Flags**: A

---
## Method: Canvas.getPageRight

### Description
Return the page-relative right coordinate of this object, in pixels.

### Returns

`[number](#type-number)` — GLOBAL right coordinate

### Groups

- positioning

---
## Method: Canvas.getZIndex

### Description
Get the z-Index of this canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| resolveToNumber | [boolean](../reference.md#type-boolean) | false | — | If passed `true`, for undrawn widgets, resolve "auto" to the next available zIndex. |

### Returns

`[number](#type-number)` — —

### Groups

- zIndex

**Flags**: A

---
## Method: Canvas.getUISummary

### Description
Returns a summary of this canvas and its child canvii and/or fields that is useful to an AI in understanding the hierarchy.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| settings | [UISummarySettings](#type-uisummarysettings) | false | — | settings controlling the summary |

### Returns

`[Object](../reference.md#type-object)` — the summary

---
## Method: Canvas.setEditMode

### Description
Enable or disable edit mode for this component. Components in editMode must be associated with an [EditNode](../reference.md#object-editnode) within an [EditContext](EditContext.md#class-editcontext).

Components with editMode enabled support certain editing interactions which vary depending on the componentType and settings on the [editProxy](#attr-canvaseditproxy).

To disable edit mode just pass `editingOn` as false. The other parameters are not needed.

To enable edit mode on this component all three parameters are required. The `editNode` is the edit node for this component as it exists within the `editContext`.

An alternative method, [EditContext.enableEditing](EditContext.md#method-editcontextenableediting), can be used when only an editContext and editNode are available.

Placing a component into `editMode` causes the component's [Canvas.editProxy](#attr-canvaseditproxy) to be created.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editingOn | [boolean](../reference.md#type-boolean) | false | — | true to enable editMode; false to disable |
| editContext | [EditContext](#type-editcontext) | true | — | the EditContext |
| editNode | [EditNode](#type-editnode) | true | — | the EditNode |

### See Also

- [EditTree](EditTree.md#class-edittree)
- [EditContext](EditContext.md#class-editcontext)

---
## Method: Canvas.getPanelContainer

### Description
Returns this Canvas's "panel container". A panel container is a widget that manages a collection of panels, like a [TabSet](TabSet.md#class-tabset) or [SectionStack](SectionStack.md#class-sectionstack). If this Canvas is not a child of such a panel container, this method returns null.

### Returns

`[Canvas](#type-canvas)` — the Canvas's panel container, or null if the Canvas is not a chlld of a panel container

---
## Method: Canvas.placeNear

### Description
Move this canvas to the specified point, or as close to the specified point as possible without this widget extending beyond the edge of the browser viewport on any side.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number) | true | — | Left coordinate (defaults to mouse position) |
| top | [number](#type-number) | true | — | Top coordinate (defaults to mouse position) |

### Groups

- positioning
- events

---
## Method: Canvas.scrollToRight

### Description
Horizontally scrolls the content of the widget to the end of its content

### Groups

- scrolling

---
## Method: Canvas.intersectsRect

### Description
Returns true if the rectangle of this widget intersects with the rectangle coordinates passed in, and false otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number)|[Array](#type-array) | false | — | left coord of rect (or rect array) |
| top | [number](#type-number) | false | — | top coord of rect |
| width | [number](#type-number) | false | — | width of rect |
| height | [number](#type-number) | false | — | height of rect |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this canvas intersects the rectangle passed in; false otherwise

### Groups

- positioning

---
## Method: Canvas.hideContextMenu

### Description
The default implementation of this method hides the contextMenu currently being shown for this component (which occurs when the mouse button that toggles the context menu is released). Override if you want some other behavior.

### Groups

- widgetEvents

### See Also

- [Canvas.showContextMenu](#method-canvasshowcontextmenu)
- [Menu.hideContextMenu](Menu.md#method-menuhidecontextmenu)
- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.setStyleName

### Description
Sets the CSS class for this widget

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new CSS style name |

### Groups

- appearance

---
## Method: Canvas.setEnabled

### Description
set the enabled state of this object.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newState | [boolean](../reference.md#type-boolean) | false | — | pass false to disable or anything else to enable |

### Groups

- enable

**Deprecated**

**Flags**: A

---
## Method: Canvas.containsEventTarget

### Description
Returns true if the current [mouse event target](EventHandler.md#classmethod-eventhandlergettarget) is this component or a descendent of this component.

Note that, unlike [Canvas.containsEvent](#method-canvascontainsevent), this method is not based on reported event coordinates and there are cases where `containsEvent()` and `containsEventTarget()` will return different values, including when the mouse is within the bounds of a target component, but another canvas is rendered in front of it in the page's z-order.

### Returns

`[Boolean](#type-boolean)` — true if the event occurred over this canvas or a descendant of this canvas

---
## Method: Canvas.hideClickMask

### Description
Hides the click mask associated with this canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ID | [String](#type-string) | true | — | optional ID of specific clickMask to hide. If not passed, defaults to hiding the click mask associated with this widget only. |

### Groups

- clickMask

### See Also

- [Canvas.showClickMask](#method-canvasshowclickmask)

---
## Method: Canvas.focusInPreviousTabElement

### Description
Shifts focus to the previous focusable element before this one. This programatically simulates the user experience of a Shift+Tab keypress.

This method makes use of the [TabIndexManager.shiftFocus](TabIndexManager.md#classmethod-tabindexmanagershiftfocus) method to request focus be changed to the adjacent registered entry. By default standard focusable SmartClient UI elements, including Canvases, FormItems, FormItemIcons, etc are registered with the TabIndexManager in the appropriate order, and will accept focus if [focusable](#attr-canvascanfocus), and not [disabled](FormItem.md#attr-formitemdisabled) or [masked](#method-canvasshowclickmask).

**NOTE:** Focusable elements created directly in the raw HTML bootstrap or by application code will not be passed focus by this method unless they have also been explicitly registered with the TabIndexManager. See the [tabOrderOverview](../kb_topics/tabOrderOverview.md#kb-topic-tab-order-overview) for more information.

### Groups

- focus

### See Also

- [Canvas.tabIndex](#attr-canvastabindex)
- [Canvas.focusInNextTabElement](#method-canvasfocusinnexttabelement)

---
## Method: Canvas.depeer

### Description
Make this Canvas no longer a peer of its master

### Groups

- containment

---
## Method: Canvas.getVisibleWidth

### Description
Return the visible width of the Canvas.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — visible width in pixels

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.scrollToBottom

### Description
Vertically scrolls the content of the widget to the end of its content

### Groups

- scrolling

---
## Method: Canvas.updateTabPositionForDraw

### Description
This method is executed on draw. Default implementation for top-level widgets ensures this widget is at the end of the tab-sequence.

Has no effect if this canvas is embedded in a [parent](#method-canvasgetparentcanvas).

---
## Method: Canvas.getScrollWidth

### Description
Returns the scrollable width of the widget's contents, including children, ignoring clipping.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — the scrollable width of the widget's contents

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.initWidget

### Description
For custom components, perform any initialization specific to your widget subclass.

When creating a subclass of any Canvas-based component, you should generally override this method rather than overriding [Class.init](Class.md#method-classinit). This is because Canvas has its own [Class.init](Class.md#method-classinit) override which performs some generally desirable initialization - see [Canvas.init](#method-canvasinit) for details.

This method is called by [Canvas.init](#method-canvasinit) when a component is create()d. When overriding this method, You must call the superClass initWidget implementation, like so:

```
    this.Super("initWidget", arguments);
 
```

In general, if you are going to call functionality supported by your superclass (eg calling addTab() when your superclass is a TabSet), call Super() first. However, you can generally assign properties to `this` before calling Super() as a way of mimicking the effect of the property being passed to [create()](Class.md#classmethod-classcreate) on normal instance construction. For example, when subclassing a DynamicForm, you could set this.items to a generated set of items before calling Super().

NOTE: child creation: if you are creating a component that auto-creates certain children (eg a Window which creates a Header child), typical practice is to create those children immediately before drawing by overriding draw(). This postpones work until it is really necessary and avoids having to update children if settings are changed between creation and draw(). Alternatively, if you prefer callers to directly manipulate auto-created children, it's best to create them earlier in initWidget(), in order to allow manipulation before draw.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Any](#type-any) | true | — | All arguments initially passed to [Class.create](Class.md#classmethod-classcreate) |

---
## Method: Canvas.showComponentMask

### Description
Temporariy block all user interaction with children of this widget, with the exception of those passed in in the `unmaskedChildren` parameter. Children will remain blocked until [Canvas.hideComponentMask](#method-canvashidecomponentmask) is called.

This method will show the [Canvas.componentMask](#attr-canvascomponentmask) canvas to block mouse interaction with children, and temporarily remove masked children from the page's tab-order.

This behavior differs from the standard [click mask](#method-canvasshowclickmask) in that the modal mask shown by [Canvas.showClickMask](#method-canvasshowclickmask) will cover the entire screen and typically only allow "unmasking" of top level components.

Use [Canvas.hideComponentMask](#method-canvashidecomponentmask) to hide the component level mask.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| unmaskedChildren | [Array of Canvas](#type-array-of-canvas) | true | — | Children passed into this parameter will continue to be interactive while other children are blocked. They will be moved above the componentMask in the page's z-order and remain accessible via keyboard navigation. Note that this array should contain direct children of this widget only. |

---
## Method: Canvas.contains

### Description
Returns true if element is a descendant of this widget (i.e., exists below this widget in the containment hierarchy); and false otherwise.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [Canvas](#type-canvas) | false | — | the canvas to be tested |
| testSelf | [Boolean](#type-boolean) | true | — | If passed this method will return true if the canvas parameter is a pointer to this widget. |

### Returns

`[Boolean](#type-boolean)` — true if specified element is a descendant of this canvas; false otherwise

### Groups

- containment

**Flags**: A

---
## Method: Canvas.setBorder

### Description
Set the CSS border of this component, as a CSS string including border-width, border-style, and/or color (eg "2px solid blue").

This property applies the same border to all four sides of this component. Different per-side borders can be set in a CSS style and applied via [Canvas.styleName](#attr-canvasstylename).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newBorder | [String](#type-string) | false | — | new border to set to (eg: "2px solid black") |

### Groups

- appearance

---
## Method: Canvas.getInnerHeight

### Description
Returns the amount of space available for (an) absolutely positioned child widget(s) or absolutely positioned HTML content, without introducing clipping, scrolling or overflow.

This is the space within the viewport of the widget (including padding, but excluding margins, borders or scrollbars) rendered at its specified size.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — inner height of the widget in pixels

### Groups

- sizing

### See Also

- [Canvas.getInnerWidth](#method-canvasgetinnerwidth)
- [Canvas.getInnerContentHeight](#method-canvasgetinnercontentheight)
- [Canvas.getInnerContentWidth](#method-canvasgetinnercontentwidth)

**Flags**: A

---
## Method: Canvas.setValuesManager

### Description
Setter for the [Canvas.valuesManager](#attr-canvasvaluesmanager) attribute. This method may be called directly at runtime to set the ValuesManager for a component; it has the same effect as calling [ValuesManager.addMember](ValuesManager.md#method-valuesmanageraddmember), passing in this DataBoundComponent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataPath | [ValuesManager](#type-valuesmanager) | false | — | new dataPath |

---
## Method: Canvas.getParentElements

### Description
Returns an array of object references to all ancestors of this widget in the containment hierarchy, starting with the direct parent and ending with the top element.

### Returns

`[Array of Canvas](#type-array-of-canvas)` — array of parents, closest first; empty array if no parents

### Groups

- containment

---
## Method: Canvas.setBackgroundColor

### Description
Sets the background color of this component to `newColor`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newColor | [CSSColor](../reference_2.md#type-csscolor) | false | — | new background color, or `null` to remove the current background color. |

### Groups

- appearance

---
## Method: Canvas.animateMove

### Description
Animate a reposition of this canvas from its current position to the specified position

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left position (or null for unchanged) |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top position (or null for unchanged) |
| callback | [AnimationCallback](#type-animationcallback) | true | — | When the move completes this callback will be fired. Single 'earlyFinish' parameter will be passed if the animation was cut short, for example by a call to the non-animated APIs [Canvas.moveTo](#method-canvasmoveto) or [Canvas.moveBy](#method-canvasmoveby). |
| duration | [Integer](../reference_2.md#type-integer) | true | — | Duration in ms of the animated move |
| acceleration | [AnimationAcceleration](../reference.md#type-animationacceleration) | true | — | Optional acceleration effect to bias the ratios |

### Groups

- animation

---
## Method: Canvas.scrollBy

### Description
Scroll this widget by some pixel increment in either (or both) direction(s).

Note: If you attempt to call this API before the widget is drawn, the call will be ignored.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [number](#type-number) | false | — | Number of pixels to scroll horizontally |
| dY | [number](#type-number) | false | — | Number of pixels to scroll vertically |

### Groups

- scrolling

---
## Method: Canvas.adjustForContent

### Description
This method tells a component to adjust for changes in the size of its content that happen outside of SmartClient APIs. This may include:

1.  size changes due to "replaced" HTML elements (elements that may change size after their content loads, such as `<img>` tags with no sizes). To avoid the need to call `adjustForContent()`, specify sizes on replaced elements wherever possible.
2.  modification of HTML contained in a Canvas by direct manipulation of the DOM - see the [DOM-level Integration overview](../kb_topics/domIntegration.md#kb-topic-dom-integration--third-party-components). Note that only contents supplied to a widget via [Canvas.contents](#attr-canvascontents) or via an override of [Canvas.getInnerHTML](#method-canvasgetinnerhtml) should be manipulated directly. Contents automatically generated by SmartClient components (such as the basic structure of a Button) should never be manipulated: these structures are considered internal, differ by platform, and will change without notice.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| immediate | [boolean](../reference.md#type-boolean) | false | — | By default the adjustment will occur on a small delay for performance reasons. Pass in this parameter to force immediate adjustment. |

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.showRecursively

### Description
Recursively show the canvas and all its parents so the canvas will be visible.

If the widget has not yet been drawn, this method calls the draw method as well.

### Groups

- visibility

---
## Method: Canvas.setWidth

### Description
Resizes the widget horizontally to the specified width (moves the right side of the widget). The width parameter can be expressed as a percentage of viewport size or as the number of pixels.

NOTE: if you're setting multiple coordinates, use resizeTo() or setRect() instead

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [Number](#type-number)|[String](#type-string) | false | — | new width |

### Groups

- sizing

---
## Method: Canvas.getID

### Description
When a widget instance is created, it is assigned a unique global identifier that can be used to access the instance by name. The getID method returns this ID for a particular instance. Global IDs are essential when you need to embed a widget reference in a string, usually a string that will be evaluated in the future and/or in another object, where you may not have access to a variable or parameter holding the widget's reference.

### Returns

`[GlobalId](../reference.md#type-globalid)` — global identifier for this canvas

---
## Method: Canvas.animateHide

### Description
Hide a canvas by shrinking it vertically to zero height over a period of time. This method will not fire if the widget is already drawn and visible, or has overflow other than `"visible"` or `"hidden"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| effect | [AnimateShowEffectId](../reference_2.md#type-animateshoweffectid)|[AnimateShowEffect](#type-animateshoweffect) | true | — | How should the content of the window be hidden during the hide? If ommitted, default behavior can be configured via [Canvas.animateHideEffect](#attr-canvasanimatehideeffect) |
| callback | [AnimationCallback](#type-animationcallback) | true | — | When the hide completes this callback will be fired. Single 'earlyFinish' parameter will be passed if the animation was cut short, for example by a call to the non-animated API [Canvas.hide](#method-canvashide). |
| duration | [Integer](../reference_2.md#type-integer) | true | — | Duration in ms of the animated hide. If unset, duration will be picked up from [Canvas.animateHideTime](#attr-canvasanimatehidetime) |
| acceleration | [AnimationAcceleration](../reference.md#type-animationacceleration) | true | — | Optional acceleration effect function to bias the animation ratios. If unset, acceleration will be picked up from [Canvas.animateShowTime](#attr-canvasanimateshowtime) |

### Groups

- animation

---
## Method: Canvas.getPrintHTML

### Description
Retrieves printable HTML for this component and all printable subcomponents.

By default any Canvas with children will simply collect the printable HTML of its children by calling getPrintHTML() on each child that is considered [printable](#attr-canvasshouldprint). If a callback is provided, then null is always returned and the callback is fired asynchronously.

If overriding this method for a custom component, you should **either** return a String of printable HTML directly **or** return null and fire the provided callback using [Class.fireCallback](Class.md#method-classfirecallback).

To return an empty print representation, return an empty string ("") rather than null.

The `printProperties` argument, if passed, must be passed to any subcomponents on which `getPrintHTML()` is called.

Default implementation will set [Canvas.isPrinting](#attr-canvasisprinting) flag to `true` to indicate printing is in progress, and clear this flag when the printing has completed (possibly via an asynchronous callback).

**NOTE:** Expecting a direct return value from the default implementation is deprecated usage. This is because small changes to an application (such as adding a few more data points to a chart or adding another button) or using certain browsers can make it necessary to generate the HTML asynchronously. Thus, application code should not rely on the return value and always pass a callback.

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
## Method: Canvas.setPercentSource

### Description
Setter method for the [percentSource](#attr-canvaspercentsource) attribute.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| sourceWidget | [Canvas](#type-canvas) | true | — | eterNew percent source (if omitted existing percentSource will just be cleared). |

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.animateShow

### Description
Show a canvas by growing it vertically to its fully drawn height over a period of time. This method will not fire if the widget is already drawn and visible, or has overflow other than `"visible"` or `"hidden"`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| effect | [AnimateShowEffectId](../reference_2.md#type-animateshoweffectid)|[AnimateShowEffect](#type-animateshoweffect) | true | — | Animation effect to use when revealing the widget. If ommitted, default behavior can be configured via [Canvas.animateShowEffect](#attr-canvasanimateshoweffect) |
| callback | [AnimationCallback](#type-animationcallback) | true | — | When the show completes this callback will be fired. Single 'earlyFinish' parameter will be passed if the animation was cut short, for example by a call to the non-animated API [Canvas.show](#method-canvasshow). |
| duration | [Integer](../reference_2.md#type-integer) | true | — | Duration in ms of the animated show. If unset, duration will be picked up from [Canvas.animateShowTime](#attr-canvasanimateshowtime) |
| acceleration | [AnimationAcceleration](../reference.md#type-animationacceleration) | true | — | Optional acceleration effect function to bias the animation ratios. If unset, acceleration will be picked up from [Canvas.animateShowAcceleration](#attr-canvasanimateshowacceleration) |

### Groups

- animation

---
## Method: Canvas.animateFade

### Description
Animate a change in opacity from the widget's current opacity to the specified opacity.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| opacity | [Integer](../reference_2.md#type-integer) | false | — | desired final opacity |
| callback | [AnimationCallback](#type-animationcallback) | true | — | When the fade completes this callback will be fired. Single 'earlyFinish' parameter will be passed if the animation was cut short, for example by a call to the non-animated API [Canvas.setOpacity](#method-canvassetopacity). |
| duration | [Integer](../reference_2.md#type-integer) | true | — | Duration in ms of the animated fade |
| acceleration | [AnimationAcceleration](../reference.md#type-animationacceleration) | true | — | Optional animation acceleration to bias the ratios |

### Groups

- animation

---
## Method: Canvas.getVSnapPosition

### Description
Override this method to provide a custom snap-to grid. Note that you do not need to do this if your grid is regular (ie, grid points are every x pixels) - regular grids should be defined using [Canvas.snapHGap](#attr-canvassnaphgap) and [Canvas.snapVGap](#attr-canvassnapvgap). You should only override this method if you want to provide support for a grid of irregularly-placed points

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| coordinate | [int](../reference.md#type-int) | false | — | y-coordinate of the drag event relative to the inside of this widget |
| direction | [String](#type-string) | true | — | "before" or "after" denoting whether the returned coordinate should match the top or bottom edge of the current square. If unset [Canvas.snapHDirection](#attr-canvassnaphdirection) will be used by default |

### Returns

`[int](../reference.md#type-int)` — The vertical coordinate to snap to

### Groups

- snapGridDragging

**Flags**: A

---
## Method: Canvas.getFullDataPath

### Description
Returns a fully qualified [DataPath](../reference_2.md#type-datapath) for this canvas. This is calculated by combining the canvas' specified [DataPath](../reference_2.md#type-datapath) with the `dataPath` of any parent canvases up to whichever canvas has a specified [Canvas.valuesManager](#attr-canvasvaluesmanager) specified to actually manage values from this component.

### Returns

`[DataPath](../reference_2.md#type-datapath)` — fully qualified dataPath for this component

---
## Method: Canvas.setGroupTitle

### Description
Setter for [Canvas.groupTitle](#attr-canvasgrouptitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | The new title for the grouping. |

### Groups

- appearance

---
## Method: Canvas.isDrawn

### Description
Returns the boolean true, if the widget has been completely drawn, and false otherwise.

### Returns

`[Boolean](#type-boolean)` — true if drawn, false if not drawn

### Groups

- drawing

---
## Method: Canvas.scrolled

### Description
Notification that this component has just scrolled. Use with [observation](Class.md#method-classobserve).

Fires for both CSS and ["synthetic" scrollbars](Scrollbar.md#class-scrollbar).

### Groups

- scrolling

---
## Method: Canvas.layoutChildren

### Description
`layoutChildren()` is where a Canvas should implement a sizing policy for it's Canvas children. Since `layoutChildren` calls parentResized() on its children, [Canvas.parentResized](#method-canvasparentresized) is a good place for a child to implement a layout policy that can be used within any parent.

Recommended practice for a Canvas that manages Canvas children is to create those children without any initial coordinate or size settings and do all sizing when layoutChildren() is called.

layoutChildren() is always called at least once before children are drawn, and is called automatically whenever the viewport size changes (which includes both resizing and introduction/removal of scrolling). layoutChildren() can also be manually invoked in any other component-specific situation which changes the layout.

NOTE: layoutChildren() may be called before draw() if a widget is resized before draw(), so be sure to avoid errors such as assuming that any children you automatically create have already been created.

NOTE: auto-sizing: layoutChildren() is also called once during the initial draw(), before children are drawn, with a "reason" of "initial draw". During this invocation of layoutChildren() it is legal to directly draw children (call child.draw()), which is otherwise never allowed. This allows a Canvas to implement an auto-sizing layout policy by drawing some children before deciding on the sizes of remaining children, which is far more efficient than drawing all children and resizing some of them after they are drawn.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [String](#type-string) | false | — | reason why layoutChildren() is being called, passed when framework code invokes layoutChildren() |

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.doubleClick

### Description
Executed when the left mouse button is clicked twice in rapid succession (within [Canvas.doubleClickDelay](#attr-canvasdoubleclickdelay) by default) in this object.

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.doubleClickDelay](#attr-canvasdoubleclickdelay)

**Flags**: A

---
## Method: Canvas.getPageBottom

### Description
Return the page-relative bottom coordinate of this object, in pixels.

### Returns

`[number](#type-number)` — GLOBAL bottom coordinate

### Groups

- positioning

---
## Method: Canvas.hideComponentMask

### Description
Hide the [component level clickMask](#method-canvasshowcomponentmask) for this widget

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| suppressFocusReset | [boolean](../reference.md#type-boolean) | true | — | By default when the component-level mask is hidden it will attempt to reset focus to whatever had focus before the mask was shown. Pass this parameter to suppress this behavior. |

---
## Method: Canvas.getHeight

### Description
Return the height of this object, in pixels.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[Number](#type-number)` — height

### Groups

- sizing

---
## Method: Canvas.addPeer

### Description
Adds newPeer as a peer of this widget (also making it a child of this widget's parent, if any), set up a named object reference (i.e., this\[name\]) to the new widget if name is provided, and draw the peer if this widget has been drawn already.  

The widget to be added as a peer will be removed from its old master and/or parent, if any, and it will be added as a child to the parent of this canvas (if any)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newPeer | [Canvas](#type-canvas) | false | — | new peer widget to add |
| name | [String](#type-string) | true | — | name to assign to peer (eg: this\[peer\] == child) |
| autoDraw | [Boolean](#type-boolean) | true | — | if false, peer will not automatically be drawn (only for advanced use) |
| preDraw | [Boolean](#type-boolean) | true | — | if true, when draw is called on the master widget, the peer will be drawn before the master |

### Returns

`[Canvas](#type-canvas)` — the new peer, or null if it couldn't be added

### Groups

- containment

---
## Method: Canvas.getOffsetY

### Description
Return the Y-coordinate of the last event, relative to the top edge of the content of this Canvas.  
  
NOTE: To get a coordinate relative to the **viewport** of this Canvas, subtract this.getScrollTop()

### Returns

`[number](#type-number)` — —

### Groups

- events
- positioning

---
## Method: Canvas.clearExplicitTabIndex

### Description
If an explicit [Canvas.tabIndex](#attr-canvastabindex) was assigned to this widget, clear it. This will enable automatic tab index managment behaviors via the [TabIndexManager](TabIndexManager.md#class-tabindexmanager) class as described in the [tabOrderOverview](../kb_topics/tabOrderOverview.md#kb-topic-tab-order-overview)

---
## Method: Canvas.getInnerHTML

### Description
Return the inner HTML for this canvas. Called when the canvas is drawn or redrawn; override to customize.

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML contents of this canvas

### Groups

- drawing

**Flags**: A

---
## Method: Canvas.getInnerContentHeight

### Description
Returns the amount of space available for interior content (or relatively positioned child widget(s)) without introducing clipping, scrolling or overflow.  
This is the space within the viewport of the widget (not including padding, and excluding margins, borders or scrollbars) rendered at its specified size.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — inner height of the widget in pixels

### Groups

- sizing

### See Also

- [Canvas.getInnerContentWidth](#method-canvasgetinnercontentwidth)
- [Canvas.getInnerHeight](#method-canvasgetinnerheight)
- [Canvas.getInnerWidth](#method-canvasgetinnerwidth)

**Flags**: A

---
## Method: Canvas.hide

### Description
Sets the widget's CSS visibility attribute to "hidden".

### Groups

- visibility

---
## Method: Canvas.getLocalId

### Description
Retrieve the local ID of this canvas. If no local ID is assigned the normal canvas ID is returned making this method a safe replacement for [getID()](#method-canvasgetid).

A "local ID" is name for a child widget which is unique only for this parent, and not globally unique as is required for [Canvas.ID](#attr-canvasid). Widgets receive local IDs when loaded via [RPCManager.loadScreen](RPCManager.md#classmethod-rpcmanagerloadscreen) or [RPCManager.cacheScreens](RPCManager.md#classmethod-rpcmanagercachescreens) and [RPCManager.createScreen](RPCManager.md#classmethod-rpcmanagercreatescreen).

### Returns

`[String](#type-string)` — the local ID or standard ID of the Canvas

---
## Method: Canvas.parentResized

### Description
Fires when the interior size of the parent changes, including parent resize and scrollbar introduction or removal.

This method allows a child to implement a layout policy that can be used within any parent, such as a Resizer component that always snaps to the parent's bottom-right corner. The default implementation of this method applies a child's percent sizes, if any, or implements layout based on the [Canvas.snapTo](#attr-canvassnapto) property

### Groups

- sizing

---
## Method: Canvas.mouseMove

### Description
Executed when the mouse moves within this widget. No default implementation.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.removeSnapAlignCandidate

### Description
Remove a candidate from [Canvas.snapAlignCandidates](#attr-canvassnapaligncandidates). If the passed widget was not actually a candidate, nothing happens and no warning is logged.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| candidate | [Canvas](#type-canvas) | false | — | — |

### Groups

- snapGridDragging

---
## Method: Canvas.bringToFront

### Description
Puts this widget at the top of the stacking order, so it appears in front of all other widgets in the same parent.

### Groups

- zIndex

---
## Method: Canvas.setImage

### Description
Set the URL of an image or SVG object element by name.

The element must have been created from HTML generated by calling `canvas.imgHTML()` on this particular Canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| identifier | [String](#type-string) | false | — | name of the image to change, as originally passed to `imgHTML` |
| URL | [SCImgURL](../reference.md#type-scimgurl) | false | — | URL for the image |
| imgDir | [String](#type-string) | true | — | optional image directory, overrides the default for this Canvas |

### Groups

- images

**Flags**: A

---
## Method: Canvas.keyPress

### Description
Executed when a key is pressed and released on a focusable widget ([Canvas.canFocus](#attr-canvascanfocus): true).

Use [EventHandler.getKey](EventHandler.md#classmethod-eventhandlergetkey) to find out the [keyName](../reference.md#type-keyname) of the key that was pressed, and use [EventHandler.shiftKeyDown](EventHandler.md#classmethod-eventhandlershiftkeydown) and related functions to determine whether modifier keys were down.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress native behavior in response to the keyPress, and prevent this event from bubbling to this widget's parent, or true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.canFocus](#attr-canvascanfocus)

**Flags**: A

---
## Method: Canvas.clear

### Description
Remove all visual representation of a Canvas, including all child or member Canvases, or managed top-level components such as the ListGrid drop location indicator.

This is more expensive than hide(), because in order to become visible again, the Canvas must be draw()n again. Generally, application code has no reason to call clear() unless it is attempting to do advanced memory management. If you want to temporarily hide a Canvas, use hide() and show(), and if you want to permanently destroy a Canvas, use [Canvas.destroy](#method-canvasdestroy).

You would only use clear() if you were managing a very large pool of components and you wanted to reclaim some of the memory used by components that had not been used in a while, while still being able to just draw() them to make them active and visible again.

Note: a clear() will happen as part of moving a Canvas to a different parent. See [Canvas.addChild](#method-canvasaddchild).

**Flags**: A

---
## Method: Canvas.containsFocus

### Description
Returns true if the keyboard focus is in this Canvas or any child of this Canvas.

### Returns

`[Boolean](#type-boolean)` — whether this Canvas contains the keyboard focus

### Groups

- focus

---
## Method: Canvas.isDisabled

### Description
Is this canvas disabled? Note that the disabled state is inherited - this method will return true if this widget, or any of its ancestors are marked disabled.

### Returns

`[Boolean](#type-boolean)` — true if the widget or any widget above it in the containment hierarchy are disabled.

### Groups

- enable

---
## Method: Canvas.dragRepositionMove

### Description
Executed every time the mouse moves while drag-repositioning. If this method does not return false, the [Canvas.dragTarget](#attr-canvasdragtarget) (or outline if [Canvas.dragAppearance](#attr-canvasdragappearance) is set to "outline") will automatically be moved as appropriate whenever the mouse moves.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress auto-move of the [Canvas.dragTarget](#attr-canvasdragtarget) or outline.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)
- [EventHandler.getDragRect](EventHandler.md#classmethod-eventhandlergetdragrect)

**Flags**: A

---
## Method: Canvas.updateChildTabPositions

### Description
Update the childrens' tab positions, slotting them under this widget in the [TabIndexManager](TabIndexManager.md#class-tabindexmanager), in the order defined by [Canvas.getChildTabPosition](#method-canvasgetchildtabposition). This method will skip any children where [Canvas.updateTabPositionOnReparent](#attr-canvasupdatetabpositiononreparent) is false.

This method is called automatically on canvas draw(). It may be overridden by subclasses for custom tab-order behavior.

---
## Method: Canvas.setContents

### Description
Changes the contents of a widget to newContents, an HTML string.

When [dynamicContents](#attr-canvasdynamiccontents) is set, `setContents()` can also be called with no arguments to cause contents to be re-evaluated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newContents | [HTMLString](../reference.md#type-htmlstring) | true | — | an HTML string to be set as the contents of this widget |

---
## Method: Canvas.drop

### Description
Executed when the mouse button is released over a compatible drop target at the end of a drag sequence. Your widget should implement whatever it wants to do when receiving a drop here. For example, in a file moving interface, a drop might mean that you should move or copy the dragged file into the folder it was dropped on, or dropping something in a trash can might mean to clear it from the screen.

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)
- [EventHandler.getDragTarget](EventHandler.md#classmethod-eventhandlergetdragtarget)

**Flags**: A

---
## Method: Canvas.keyUp

### Description
Executed when a key is released on a focusable widget ([Canvas.canFocus](#attr-canvascanfocus): true).

Use [EventHandler.getKey](EventHandler.md#classmethod-eventhandlergetkey) to find out the [keyName](../reference.md#type-keyname) of the key that was pressed, and use [EventHandler.shiftKeyDown](EventHandler.md#classmethod-eventhandlershiftkeydown) and related functions to determine whether modifier keys were down.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.canFocus](#attr-canvascanfocus)

**Flags**: A

---
## Method: Canvas.resizeTo

### Description
Resizes the widget to the specified width and height (moves the right and/ or bottom sides of the widget). The width and height parameters can be expressed as a percentage of viewport size or as the number of pixels. See [Canvas.width](#attr-canvaswidth) or [Canvas.height](#attr-canvasheight) for more on canvas sizing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [number](#type-number) | true | — | new width for canvas. |
| height | [number](#type-number) | true | — | new height for canvas |

### Returns

`[Boolean](#type-boolean)` — whether the size actually changed

### Groups

- sizing

---
## Method: Canvas.isEnabled

### Description
Returns true if the widget and all widgets above it in the containment hierarchy are enabled. Returns false otherwise.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the widget and all widgets above it in the containment hierarchy are enabled; false otherwise

### Groups

- enable

**Deprecated**

---
## Method: Canvas.getHoverHTML

### Description
If `this.showHover` is true, when the user holds the mouse over this Canvas for long enough to trigger a hover event, a hover canvas is shown by default. This method returns the contents of that hover canvas. Default implementation returns `this.prompt` - override for custom hover HTML. Note that returning `null` or an empty string will suppress the hover canvas altogether.

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — the string to show in the hover

### Groups

- hovers

### See Also

- [Canvas.showHover](#attr-canvasshowhover)

---
## Method: Canvas.handleHover

### Description
Handler fired on a delay when the user hovers the mouse over this hover-target. Default implementation will fire `this.hover()` (if defined), and handle showing the hover canvas if `this.showHover` is true.

### Groups

- hovers

### See Also

- [Canvas.canHover](#attr-canvascanhover)
- [Canvas.showHover](#attr-canvasshowhover)
- [Canvas.hover](#method-canvashover)

**Flags**: A

---
## Method: Canvas.ruleContextChanged

### Description
Notification that the rule context gathered by the [Canvas.ruleScope](#attr-canvasrulescope) has changed.

This notification fires only on the component designated as the [Canvas.ruleScope](#attr-canvasrulescope); components that are merely contributing data to the rule context do not fire `ruleContextChanged`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| data | [Object](../reference.md#type-object) | false | — | the new rule context |

---
## Method: Canvas.getChildTabPosition

### Description
For a given child widget where [Canvas.updateTabPositionOnReparent](#attr-canvasupdatetabpositiononreparent) is true, return the expected tab position within this parent. Default implementation will any explicit relative tab position specified by [Canvas.setRelativeTabPosition](#method-canvassetrelativetabposition), and otherwise put children in the same order as defined in the children array

Overridden in the [Layout](Layout.md#class-layout) class to return the position in the members array.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [Canvas](#type-canvas) | false | — | Child to get local tab position for |

### Returns

`[Integer](../reference_2.md#type-integer)` — tab position of child within this parent

---
## Method: Canvas.blur

### Description
If this canvas has keyboard focus, blur it. After this method, the canvas will no longer appear focused and will stop receiving keyboard events.

### Groups

- focus

---
## Method: Canvas.draw

### Description
Draws the widget on the page.

### Returns

`[Canvas](#type-canvas)` — Pointer to this canvas. Returned so statements like the following will work:  
var myCanvas = Canvas.newInstance({...}).draw();

### Groups

- drawing

---
## Method: Canvas.willAcceptDrop

### Description
Returns true if the widget object being dragged can be dropped on this widget, and false otherwise. The default implementation of this method simply compares the [dragType](#attr-canvasdragtype) of the `dragTarget` (the component being dragged from) with the list of [dropTypes](#attr-canvasdroptypes) on this Canvas. If the [dropTypes](#attr-canvasdroptypes) list contains the [dragType](#attr-canvasdragtype) value, then this method returns true. Otherwise it returns false.

No matter what you return, [dropOver()](#method-canvasdropover) and [dropMove()](#method-canvasdropmove) will still be called, and their return values will determine whether those events are bubbled to parent elements.

However, what you return from `willAcceptDrop()` does determine whether [drop()](#method-canvasdrop) will be called.

*   If you return true, then `drop()` will be called, and its return value will determine whether the event is bubbled to parent elements
*   If you return false, then `drop()` will not be called, and the event will not be bubbled.
*   If you return null, then `drop()` will not be called, but the event will be bubbled to parent elements (giving them a chance to handle the drop).

So, you should return false to definitively deny a drop, and return null if it could make sense to allow a parent element, such as a [Layout](Layout.md#class-layout), to handle the drop.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the widget object being dragged can be dropped on this widget, false if it cannot (and `drop()` should not bubble), null to permit `drop()` to bubble to parent elements

### Groups

- dragdrop

### See Also

- [Canvas.dragType](#attr-canvasdragtype)
- [Canvas.dropTypes](#attr-canvasdroptypes)
- [Canvas.dragTarget](#attr-canvasdragtarget)
- [Canvas.drop](#method-canvasdrop)

**Flags**: A

---
## Method: Canvas.setTop

### Description
Set the top coordinate of this object, relative to its enclosing context, in pixels.

NOTE: if you're setting multiple coordinates, use setRect() or moveTo() instead

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| top | [Number](#type-number)|[String](#type-string) | false | — | new top coordinate |

### Groups

- positioning

---
## Method: Canvas.sendToBack

### Description
Puts this widget at the bottom of the stacking order, so it appears behind all other widgets in the same parent.

### Groups

- zIndex

---
## Method: Canvas.dragRepositionStop

### Description
Executed when the mouse button is released at the end of the drag. Your widget can use this opportunity to fire custom code based upon where the mouse button was released, etc.

Returning true from this handler will cause the [Canvas.dragTarget](#attr-canvasdragtarget) (or outline if [Canvas.dragAppearance](#attr-canvasdragappearance) is set to "outline") to be left in its current location. Returning false from this handler will cause it to snap back to its original location.

### Returns

`[boolean](../reference.md#type-boolean)` — false to snap the [Canvas.dragTarget](#attr-canvasdragtarget) (or outline) back to its original location or true to leave it at the current cursor position.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)
- [EventHandler.getDragRect](EventHandler.md#classmethod-eventhandlergetdragrect)

**Flags**: A

---
## Method: Canvas.getHSnapPosition

### Description
Override this method to provide a custom snap-to grid. Note that you do not need to do this if your grid is regular (ie, grid points are every x pixels); regular grids should be defined using [Canvas.snapHGap](#attr-canvassnaphgap) and [Canvas.snapVGap](#attr-canvassnapvgap). You should only override this method if you want to provide support for a grid of irregularly-placed points

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| coordinate | [int](../reference.md#type-int) | false | — | x-coordinate of the drag event relative to the inside of this widget |
| direction | [String](#type-string) | true | — | "before" or "after" denoting whether the returned coordinate should match the left or right edge of the current square. If unset [Canvas.snapHDirection](#attr-canvassnaphdirection) will be used by default |

### Returns

`[int](../reference.md#type-int)` — The horizontal coordinate to snap to

### Groups

- dragdrop

**Flags**: A

---
## Method: Canvas.scrollByPercent

### Description
Scroll this widget by some percentage of scroll size in either (or both) direction(s).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dX | [number](#type-number)|[String](#type-string) | false | — | Percentage to scroll horizontally. Will accept either a numeric percent value, or a string like "10%". |
| dY | [number](#type-number)|[String](#type-string) | false | — | Percentage to scroll horizontally. Will accept either a numeric percent value, or a string like "10%". |

### Groups

- scrolling

---
## Method: Canvas.setCursor

### Description
Sets the cursor for this widget to cursor. See the cursor property for possible values.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCursor | [Cursor](../reference.md#type-cursor) | false | — | new cursor |

### Groups

- cues

---
## Method: Canvas.show

### Description
Sets this widget's visibility to "inherit", so that it becomes visible if all of its parents are visible or it has no parents.

If the widget has not yet been drawn (and doesn't have a parent or master), this method calls the draw method as well.

### Groups

- visibility

---
## Method: Canvas.hoverHidden

### Description
If [showHover](#attr-canvasshowhover) is true for this canvas, this notification method will be fired whenever the hover shown in response to [handleHover()](#method-canvashandlehover) is hidden. This method may be observed or overridden.

### Groups

- hovers

**Flags**: A

---
## Method: Canvas.dropMove

### Description
Executed whenever the compatible dragged object is moved over this drop target. You can use this to show a custom visual indication of where the drop would occur within the widget, or to show the [no-drop cursor](#attr-canvasnodropcursor) to indicate that this is not a valid drop target, typically if [Canvas.willAcceptDrop](#method-canvaswillacceptdrop) returns false.

For details on showing a 'no drop' cursor when the user drags over all invalid drop targets, see [EventHandler.showNoDropIndicator](EventHandler.md#classattr-eventhandlershownodropindicator).

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.scrollToLeft

### Description
Horizontally scrolls the content of the widget to 0

### Groups

- scrolling

---
## Method: Canvas.getOuterElement

### Description
Returns the outer DOM element of this Canvas. This method is provided for the very rare cases where a programmer needs to examine the DOM hierarchy created by a drawn SmartClient component.

Direct manipulation of the DOM elements created by SmartClient components is not supported. SmartClient components should be rendered or cleared using standard methods such as [Canvas.draw](#method-canvasdraw), [Canvas.clear](#method-canvasclear). If direct integration with existing DOM structures is required, this should be achieved via the [Canvas.htmlElement](#attr-canvashtmlelement) attribute, rather than by attempting to move the component's outer element via native browser APIs.  
The content of SmartClient components' DOM elements should also not be directly manipulated using native browser APIs - standard methods such as [Canvas.setContents](#method-canvassetcontents), [Canvas.addChild](#method-canvasaddchild), [Canvas.removeChild](#method-canvasremovechild), [Canvas.markForRedraw](#method-canvasmarkforredraw) and [Canvas.redraw](#method-canvasredraw) should be used instead.

In some cases, the element returned may match the element returned by [Canvas.getContentElement](#method-canvasgetcontentelement), but this will not always be the case.

If the widget is undrawn, this method will return `null`.

### Returns

`[DOMElement](#type-domelement)` — The outer DOM element for a drawn Canvas.

**Flags**: A

---
## Method: Canvas.parentMoved

### Description
Notification method fired when an ancestor of this component's position changes.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| parent | [Canvas](#type-canvas) | false | — | the ancestor that moved |
| deltaX | [int](../reference.md#type-int) | false | — | horizontal difference between current and previous position |
| deltaY | [int](../reference.md#type-int) | false | — | vertical difference between current and previous position |

### See Also

- [Canvas.moved](#method-canvasmoved)

---
## Method: Canvas.getTop

### Description
Return the top coordinate of this object, relative to its enclosing context, in pixels.

### Returns

`[Number](#type-number)` — top coordinate

### Groups

- positioning

---
## Method: Canvas.getPageTop

### Description
Returns the page-relative top coordinate of the widget on the page, in pixels

### Returns

`[number](#type-number)` — GLOBAL top coordinate

### Groups

- positioning

**Flags**: A

---
## Method: Canvas.setAccessKey

### Description
Set the accessKey for this canvas.

The accessKey can be set to any alphanumeric character (symbols not supported) Having set an accessKey, the canvas will be given focus when the user hits Alt+\[accessKey\], or in Mozilla Firefox 2.0 and above, Shift+Alt+\[accessKey\].

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| accessKey | [String](#type-string) | false | — | Character to use as an accessKey for this widget. Case Insensitive. |

### Groups

- focus

**Flags**: A

---
## Method: Canvas.mouseOut

### Description
Executed when the mouse leaves this widget. No default implementation.

Note that if the mouse goes over a child of this canvas, the mouseOut event will fire as it would if the user rolled entirely off the canvas. Developers may determine whether the mouse is still over a descendant of this component via [Canvas.containsEventTarget](#method-canvascontainseventtarget).

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

**Flags**: A

---
## Method: Canvas.setDragTracker

### Description
If [Canvas.dragAppearance](#attr-canvasdragappearance) is set to `"tracker"`, this method will be called (if defined), when the user starts to drag this widget. It is an opportunity to update the drag tracker to display something relative to this canvas. Typical implementation will be to call [EventHandler.setDragTracker](EventHandler.md#classmethod-eventhandlersetdragtracker), passing in the desired custom tracker HTML as a string

### Returns

`[boolean](../reference.md#type-boolean)` — Return false to suppress bubbling, and prevent `setDragTracker()` from being called on this widget's ancestors.

### Groups

- dragdrop

---
## Method: Canvas.animateRect

### Description
Animate a reposition / resize of this canvas from its current size and position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | false | — | new left position (or null for unchanged) |
| top | [Integer](../reference_2.md#type-integer) | false | — | new top position (or null for unchanged) |
| width | [Integer](../reference_2.md#type-integer) | false | — | new width (or null for unchanged) |
| height | [Integer](../reference_2.md#type-integer) | false | — | new height (or null for unchanged) |
| callback | [AnimationCallback](#type-animationcallback) | true | — | When the setRect completes this callback will be fired. Single 'earlyFinish' parameter will be passed if the animation was cut short, for example by a call to the non-animated API [Canvas.setRect](#method-canvassetrect). |
| duration | [Integer](../reference_2.md#type-integer) | true | — | Duration in ms of the animated setRect |
| acceleration | [AnimationAcceleration](../reference.md#type-animationacceleration) | true | — | Optional acceleration effect to apply to the animation |

### Groups

- animation

---
## Method: Canvas.getPrintStyleName

### Description
Get the CSS class to apply when printing this widget. Returns the [print style](#attr-canvasprintstylename), if specified, falling back to the [specified style](#attr-canvasstylename) otherwise.

### Returns

`[CSSStyleName](../reference.md#type-cssstylename)` — printStyleName

### Groups

- appearance

---
## Method: Canvas.setShowResizeBar

### Description
When this Canvas is included as a member in a [Layout](Layout.md#class-layout), dynamically updates whether a resizeBar should be shown after this member in the layout, to allow it to be resized.

Whether a resizeBar is actually shown also depends on the [defaultResizeBars](Layout.md#attr-layoutdefaultresizebars) attribute of the layout, and whether this Canvas is the last layout member.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../reference.md#type-boolean) | false | — | setting for this.showResizeBar |

### Groups

- layoutMember

### See Also

- [Layout.defaultResizeBars](Layout.md#attr-layoutdefaultresizebars)

---
## Method: Canvas.resized

### Description
Observable method called whenever a Canvas changes size. Note that if this canvas is [overflow:"visible"](#attr-canvasoverflow), and is waiting for a queued redraw (see [Canvas.isDirty](#method-canvasisdirty)), the value for [Canvas.getVisibleWidth](#method-canvasgetvisiblewidth) and [Canvas.getVisibleHeight](#method-canvasgetvisibleheight) will be unreliable until `redraw()` fires.  
In this case, if the delayed redraw does change the drawn size of the component, this notification will be fired a second time when it completes.

---
## Method: Canvas.markForRedraw

### Description
Marks the widget as "dirty" so that it will be added to a queue for redraw. Redraw of dirty components is handled by a looping timer and will after a very short delay (typically less than 100ms). In most cases it is recommended that developers use `markForRedraw()` instead of calling [Canvas.redraw](#method-canvasredraw) directly. Since this method queues the redraw, multiple calls to markForRedraw() within a single thread of execution will only lead to a single DOM manipulation which greatly improves application performance.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [String](#type-string) | true | "no reason provided" | reason for performing the redraw |

### Groups

- drawing

---
## Method: Canvas.shouldSnapOnDrop

### Description
Override this method to give programmatic control over whether or not the parameter `dragTarget` should snap to this object's grid when dropped. Note that this only applies if snap-to-grid is enabled on either `dragTarget` or this object. See [Canvas.snapToGrid](#attr-canvassnaptogrid) and [Canvas.childrenSnapToGrid](#attr-canvaschildrensnaptogrid).

The default implementation simply returns true.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dragTarget | [Canvas](#type-canvas) | false | — | The object about to be dropped |

### Returns

`[boolean](../reference.md#type-boolean)` — true if `dragTarget` should snap to this object's grid; otherwise false

### Groups

- snapGridDragging

**Flags**: A

---
## Method: Canvas.setRelativeTabPosition

### Description
Assign a relative tab position for this canvas. The meaning of a "relative" tab position varies depending on where the canvas is in the page.

For canvases with no specified [parent canvas](#method-canvasgetparentcanvas), (or where [Canvas.updateTabPositionOnReparent](#attr-canvasupdatetabpositiononreparent) is false), this method will and move the canvas to the appropriate tab-position among other top level canvases. It will also disable [Canvas.updateTabPositionOnDraw](#attr-canvasupdatetabpositionondraw) so if this method is called before draw, drawing this canvas will not cause its tab position to change.

For canvases embedded in a [Canvas.getParentCanvas](#method-canvasgetparentcanvas), this method will move the canvas to the appropriate tab position among the other children of the parent.  
**Implementation note:** This is achieved by setting an internal property to indicate the new tab position which will be respected by the default [Canvas.getChildTabPosition](#method-canvasgetchildtabposition) implementation, and calling [Canvas.updateChildTabPositions](#method-canvasupdatechildtabpositions) to implement a reflow. Therefore if [Canvas.getChildTabPosition](#method-canvasgetchildtabposition) has been overridden, this method may have no effect.

As with other APIs related to [tab index management](TabIndexManager.md#class-tabindexmanager), tab indices are treated as a hierarchy by default. By setting the relative tab position of a canvas which is not itself focusable but has focusable descendents, these descendents' tab position will be updated.

Note that after this method has been called, the tab position can be modified by subsequent code to shift another sibling in front of this one, or reparent this canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| position | [Integer](../reference_2.md#type-integer) | false | — | new relative tab position |

---
## Method: Canvas.setSnapEdge

### Description
Set the snapEdge property of this canvas, and handle repositioning.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| snapEdge | [String](#type-string) | false | — | new snapEdge value |

### Groups

- snapPositioning

---
## Method: Canvas.mouseDown

### Description
Executed when the left mouse button is pressed on this widget. No default implementation.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.getImage

### Description
Retrieve a native image or SVG object element by name.

The element must have been created from HTML generated by calling [Canvas.imgHTML](#method-canvasimghtml) on this particular Canvas.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| identifier | [String](#type-string) | false | — | name of the image or SVG object to get, as originally passed to `imgHTML()` |

### Returns

`[DOMElement](#type-domelement)` — DOM image or SVG object element if found, else null

### Groups

- images

**Flags**: A

---
## Method: Canvas.getAriaState

### Description
Gets the ARIA state mappings to apply to this component's handle. See [accessibility](../kb_topics/accessibility.md#kb-topic-accessibility--section-508-compliance) for more information on WAI-ARIA support in SmartClient.

The returned object consists of a mapping of aria attribute names to values to write into the component HTML. For example, the following mapping:

```
  { haspopup:true, label:"Settings submenu"}
 
```
Would result in ARIA html attributes like `aria-haspopup="true" aria-label="Settings submenu"`.

The returned state mappings include [default mappings](#method-canvasgetariastatedefaults) combined with any [explicitly specified aria state](#attr-canvasariastate).

Note that if a property is explicitly specified it will take precedence over the dynamically calculated default value. For example a [disabled](#attr-canvasdisabled) canvas will include `aria-disabled` in its markup by default, but a developer may change this behavior by explicitly setting ariaState to an object with the property `disabled` explicitly set to `false` or `null`.

This method will be invoked during on [Canvas.draw](#method-canvasdraw) and [Canvas.redraw](#method-canvasredraw) and the resulting state attributes will be applied to the component handle.

### Returns

`[Object](../reference.md#type-object)` — object containing aria attribute names and values

**Flags**: A

---
## Method: Canvas.setLocatorParent

### Description
This method will set mark the target canvas as the "locator parent" for this canvas, using the specified child name. After calling this method, [locators](#method-canvasgetlocator) that reference this canvas will use the `childName` to navigate from the specified parent to this component, exactly how named [autoChildren](../reference.md#type-autochild) are referenced in locators.

Note that, as with SmartClient autoChildren, the locator parent does not need to be the direct parent of this component, or even a true ancestor, in the widget hierarchy. However, you should never set the locatorParent to a descendant of this widget as that would lead to infinite loops when attempting to create or resolve locators.

This method will also set `locatorParent.attributeName`, (or `locatorParent.childName` if no explicit attributeName was specified) to refer to this canvas, if this is not already the case.

If the attribute is already set to refer to some other object, this method will return false without taking any further action.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| locatorParent | [Canvas](#type-canvas) | false | — | New locator parent for this canvas |
| childName | [String](#type-string) | false | — | Name to refer from the locator parent to this canvas in the locator |
| attributeName | [String](#type-string) | true | — | Optional attribute to refer from the parent to this canvas. If unset the childName will be used instead. |

### Returns

`[boolean](../reference.md#type-boolean)` — returns true if the locatorParent was successfully updated

---
## Method: Canvas.getRight

### Description
Return the right coordinate of this object as rendered, relative to its enclosing context, in pixels.

### Returns

`[number](#type-number)` — right coordinate

### Groups

- positioning
- sizing

---
## Method: Canvas.getContentElement

### Description
Returns the DOM element for this Canvas which contains the [Canvas.contents](#attr-canvascontents), or for [parent components](#method-canvasgetparentcanvas), the DOM elements for any drawn children. This method is provided for the very rare cases where a programmer needs to examine the DOM hierarchy created by a drawn SmartClient component.

Direct manipulation of the DOM elements created by SmartClient components is not supported. SmartClient components should be rendered or cleared using standard methods such as [Canvas.draw](#method-canvasdraw), [Canvas.clear](#method-canvasclear). If direct integration with existing DOM structures is required, this should be achieved via the [Canvas.htmlElement](#attr-canvashtmlelement) attribute, rather than by attempting to move the component's outer element via native browser APIs.  
The content of SmartClient components' DOM elements should also not be directly manipulated using native browser APIs - standard methods such as [Canvas.setContents](#method-canvassetcontents), [Canvas.addChild](#method-canvasaddchild), [Canvas.removeChild](#method-canvasremovechild), [Canvas.markForRedraw](#method-canvasmarkforredraw) and [Canvas.redraw](#method-canvasredraw) should be used instead.

In some cases, the element returned may match the element returned by [Canvas.getOuterElement](#method-canvasgetouterelement), but this will not always be the case.

If the widget is undrawn, this method will return `null`.

### Returns

`[DOMElement](#type-domelement)` — The outer DOM element for a drawn Canvas.

**Flags**: A

---
## Method: Canvas.adaptWidthBy

### Description
See [Canvas.canAdaptWidth](#attr-canvascanadaptwidth).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pixelDifference | [Integer](../reference_2.md#type-integer) | false | — | surplus (if positive) or overflow (if negative) |
| unadaptedWidth | [Integer](../reference_2.md#type-integer) | false | — | width of member currently assumed by parent layout |

### Returns

`[Integer](../reference_2.md#type-integer)` — sizeDelta

---
## Method: Canvas.redraw

### Description
Redraws the widget immediately with its current property values. Generally, if you want a Canvas to redraw, call markForRedraw() - this will cause the Canvas to be redrawn when current processing ends, so that a series of modifications made to a Canvas will cause it to redraw only once. Only call redraw() directly if you need immediate responsiveness, for example you are redrawing in response to continuous mouse motion.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| reason | [String](#type-string) | true | "no reason provided" | reason for performing the redraw |

### Groups

- drawing

**Flags**: A

---
## Method: Canvas.containsEvent

### Description
Return true if the last event's mouse coordinates are within the bounds of this component.

NOTE: Z-ordering is not considered for the purposes of this test. If the coordinate you're testing is occluded by other component, but the X,Y coordinates are still within the bounds that component, this method will return true.

See the related [Canvas.containsEventTarget](#method-canvascontainseventtarget) method for checking whether a canvas contains the target canvas for the current mouse event.

### Returns

`[Boolean](#type-boolean)` — true if the event occurred within the bounds of this component

### Groups

- events
- positioning

---
## Method: Canvas.animateScroll

### Description
Animate a scroll from the current scroll position to the specified position.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| scrollLeft | [Integer](../reference_2.md#type-integer) | false | — | desired final left scroll position |
| scrollTop | [Integer](../reference_2.md#type-integer) | false | — | desired final top scroll position |
| callback | [AnimationCallback](#type-animationcallback) | true | — | When the scroll completes this callback will be fired. Single 'earlyFinish' parameter will be passed if the animation was cut short, for example by a call to the non-animated APIs [Canvas.scrollTo](#method-canvasscrollto) or [Canvas.scrollBy](#method-canvasscrollby). |
| duration | [Integer](../reference_2.md#type-integer) | true | — | Duration in ms of the animated scroll |
| acceleration | [AnimationAcceleration](../reference.md#type-animationacceleration) | true | — | Optional acceleration to bias the animation ratios |

### Groups

- animation

---
## Method: Canvas.destroy

### Description
Permanently destroy a Canvas and all of it's children / members, recursively.

Like [Canvas.clear](#method-canvasclear), calling `destroy()` removes all HTML for the component; unlike clear(), a destroyed Canvas is permanently unusable: it cannot be draw()'n again, cannot be referenced by its global ID, and is eligible for garbage collection (assuming that application code is not holding a reference to the Canvas).

Any attempt to call a method on a destroyed Canvas will generally result in an error. If your application is forced to hold onto Canvas's that might be destroy()d without warning, you can avoid errors by checking for the [Canvas.destroyed](#attr-canvasdestroyed) property. If you override certain Canvas methods, your code may be called while a Canvas is being destroy()d; in this case you can avoid extra work (and possibly errors) by checking for the [Canvas.destroying](#attr-canvasdestroying) property.

Note that `destroy()` should not be called directly in event handling code for this canvas. For this reason, wherever possible we recommend using [Canvas.markForDestroy](#method-canvasmarkfordestroy) instead of calling this method directly.

Also note that developers should not `destroy()` or `markForDestroy()` a component while it is in the middle of an asynchronous operation. For example, if you need to submit and then destroy a single-use dynamic form, the call to `markForDestroy()` should be invoked from the callback to [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata), rather than being invoked synchronously after the the call to `saveData()`.

### See Also

- [Canvas.markForDestroy](#method-canvasmarkfordestroy)
- [memoryLeaks](../kb_topics/memoryLeaks.md#kb-topic-memory-leaks)

**Flags**: A

---
## Method: Canvas.setOpacity

### Description
Sets the opacity for the widget to the newOpacity value. This newOpacity value must be within the range of 0 (transparent) to 100 (opaque). Null means don't specify opacity directly. Note that heavy use of opacity may have a performance impact on some older browsers.

In older versions of Internet Explorer (Pre IE9 / HTML5), opacity is achieved through proprietary filters. If [filters have been disabled](#classattr-canvasneverusefilters) within this application developers must set [Canvas.useOpacityFilter](#attr-canvasuseopacityfilter) to true for specific components on which opacity support is required.

Also note that opacity is incompatible with [backMasks](#attr-canvasusebackmask).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newOpacity | [number](#type-number) | false | — | new opacity level |

### Groups

- cues

---
## Method: Canvas.setUpdateTabPositionOnReparent

### Description
Setter for the [Canvas.updateTabPositionOnReparent](#attr-canvasupdatetabpositiononreparent) attribute.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| updateOnReparent | [boolean](../reference.md#type-boolean) | false | — | new value for canvas.updateTabPositionOnReparent |

---
## Method: Canvas.setEdgeOpacity

### Description
Set the [Canvas.edgeOpacity](#attr-canvasedgeopacity) and mark the canvas for redraw

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newOpacity | [int](../reference.md#type-int) | false | — | new edge-opacity level |

---
## Method: Canvas.dataContextChanged

### Description
Notification method fired when [DataContext](../reference.md#object-datacontext) is bound. This can occur on the initial draw or by an explicit call to [Canvas.setDataContext](#method-canvassetdatacontext).

This feature allows the use of the `dataContext` as a general-purpose API to the screen. For example, if you wanted your screen to support _dynamically_ showing or hiding parts of itself based on a button that is external to the screen, you could do that by implementing this handler to show/hide that part of the screen based on the current state of the `dataContext`.

### Groups

- dataContext

---
## Method: Canvas.setShowSnapGrid

### Description
Set the showSnapGrid property.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| show | [boolean](../reference.md#type-boolean) | false | — | — |

### Groups

- snapGridDragging

---
## Method: Canvas.getScrollTop

### Description
Get the number of pixels this Canvas is scrolled from its top edge.

### Returns

`[number](#type-number)` — scrollTop

### Groups

- positioning
- scrolling

**Flags**: A

---
## Method: Canvas.getMasterCanvas

### Description
Returns this canvas's "master" (the canvas to which it was added as a peer), if any.

See [containment](../kb_topics/containment.md#kb-topic-component-containment-and-hierarchy) for an overview of master/peer relationships.

### Returns

`[Canvas](#type-canvas)` — the master canvas, null if none exists.

### Groups

- containment

---
## Method: Canvas.setHtmlElement

### Description
Setter for the [Canvas.htmlElement](#attr-canvashtmlelement).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [DOMElement](#type-domelement)|[String](#type-string) | false | — | New htmlElement for this canvas or Null to clear the existing htmlElement. You may also provide a string with the elements ID, which will have the effect of setting [Canvas.htmlElement](#attr-canvashtmlelement) to the node returned by document.getElementById(element). Note that you may need to set position:relative explicitly following a call to this function. |

### Groups

- htmlElement

---
## Method: Canvas.setMargin

### Description
Set the CSS Margin, in pixels, for this component. Margin provides blank space outside of the border.

This property sets the same thickness of margin on every side. Differing per-side margins can be set in a CSS style and applied via [Canvas.styleName](#attr-canvasstylename).

Note that the specified size of the widget will be the size **including** the margin thickness on each side.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| margin | [number](#type-number) | false | — | new margin in pixels |

---
## Method: Canvas.markForDestroy

### Description
[destroy()](#method-canvasdestroy) this canvas on a timeout. This method should be used instead of calling `canvas.destroy()` directly unless there's a reason a the canvas needs to be destroyed synchronously. By using a timeout, this method ensures the `destroy()` will occur after the current thread of execution completes. This allows you to easily mark canvases for destruction while they're handling events, which must complete before the canvas can be destroyed.

Notes:

*   `markForDestroy()` performs some immediate cleanup and puts a component into a "pending destroy" state. As far as application code is concerned, once a component has been is in this state it should be considered invalid to invoke methods on the component.
*   Developers should not `destroy()` or `markForDestroy()` a component while it is in the middle of an asynchronous operation. For example, if you need to submit and then destroy a single-use dynamic form, the call to `markForDestroy()` should be invoked from the callback to [DynamicForm.saveData](DynamicForm.md#method-dynamicformsavedata), rather than being invoked synchronously after the call to `saveData()`

### See Also

- [Canvas.destroy](#method-canvasdestroy)

---
## Method: Canvas.click

### Description
Executed when the left mouse is clicked (pressed and then released) on this widget. No default implementation.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.updateChildTabPosition

### Description
Ensure that a specific child is slotted correctly into the page's tab order. Default implementation will, if [Canvas.updateTabPositionOnReparent](#attr-canvasupdatetabpositiononreparent) is true, ensure the child canvas shows up in the [TabIndexManager](TabIndexManager.md#class-tabindexmanager) tree under the entry for this widget (the parent), in the position returned by [Canvas.getChildTabPosition](#method-canvasgetchildtabposition).

This method is called automatically in cases where a single child's tab position may need to be updated - such as if a child is added to a drawn parent.

See also [Canvas.updateChildTabPositions](#method-canvasupdatechildtabpositions)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [Canvas](#type-canvas) | false | — | child to have tab position updated. |

---
## Method: Canvas.revealChild

### Description
For "panel container" widgets like [TabSet](TabSet.md#class-tabset) or [SectionStack](SectionStack.md#class-sectionstack), this method reveals the child Canvas passed in by whatever means is applicable for the particular type of container. For example, when called on a TabSet, it selects the tab containing the passed-in child.

For other types of Canvas, this method simply shows the passed-in child if it is not currently visible.

If the passed-in widget is not a child of this Canvas, this method has no effect

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [GlobalId](../reference.md#type-globalid)|[Canvas](#type-canvas) | false | — | the child Canvas to reveal, or its global ID |

---
## Method: Canvas.setRight

### Description
Resizes the widget horizontally to position its right side at the specified coordinate.

NOTE: if you're setting multiple coordinates, use setRect(), moveTo() or resizeTo() instead

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| right | [number](#type-number) | false | — | new right coordinate |

### Groups

- sizing

---
## Method: Canvas.mouseStillDown

### Description
Repeating notification method for the user holding the left mouse button down over this canvas.

The `mouseStillDown` event is fired immediately when the mouse goes down. If the user holds the mouse down, after a pause of [Canvas.mouseStillDownInitialDelay](#attr-canvasmousestilldowninitialdelay), it will begin to fire repeatedly every [Canvas.mouseStillDownDelay](#attr-canvasmousestilldowndelay) milliseconds.

This provides developers with a simple way to handle the common "repeated action" use case where a user can click a UI element to perform an action once, or click and hold to perform the action repeatedly.  
Examples of this include standard scrollbar button behavior and buttons to increase or decrease the value in a spinner type input element.

This event is not native to JavaScript, but is provided by the ISC system.

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.mouseStillDownInitialDelay](#attr-canvasmousestilldowninitialdelay)
- [Canvas.mouseStillDownDelay](#attr-canvasmousestilldowndelay)
- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.scrollToPercent

### Description
Scroll this widget to some position specified as a percentage of scroll size in either (or both) direction(s).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number)|[String](#type-string) | false | — | Left Percentage position to scroll to Will accept either a numeric percent value, or a string like "10%". |
| top | [number](#type-number)|[String](#type-string) | false | — | Top Percentage position to scroll to Will accept either a numeric percent value, or a string like "10%". |

### Groups

- scrolling

---
## Method: Canvas.setSnapOffsetTop

### Description
Setter for [Canvas.snapOffsetTop](#attr-canvassnapoffsettop).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| snapOffsetTop | [Integer](../reference_2.md#type-integer) | false | — | new snapOffsetTop value. |

### Groups

- snapPositioning

---
## Method: Canvas.dragResizeStop

### Description
Executed when the mouse button is released at the end of the drag resize. Your widget can use this opportunity to fire custom code based upon where the mouse button was released, etc.

Returning true from this handler will cause the [Canvas.dragTarget](#attr-canvasdragtarget) (or outline if [Canvas.dragAppearance](#attr-canvasdragappearance) is set to "outline") to be left at its current size. Returning false from this handler will cause it to snap back to its original location size

### Returns

`[boolean](../reference.md#type-boolean)` — false to snap the [Canvas.dragTarget](#attr-canvasdragtarget) (or outline) back to its original size or true to leave it at the current cursor position.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)
- [EventHandler.getDragRect](EventHandler.md#classmethod-eventhandlergetdragrect)

**Flags**: A

---
## Method: Canvas.setGroupLabelBackgroundColor

### Description
Setter for [Canvas.groupLabelBackgroundColor](#attr-canvasgrouplabelbackgroundcolor).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupLabelBackgroundColor | [CSSColor](../reference_2.md#type-csscolor) | false | — | the new grouping label background color. |

---
## Method: Canvas.imgHTML

### Description
Generates the HTML for an image unique to this Canvas.

The full URL for the image will be formed according to the rules documented for `[Canvas.getImgURL](#method-canvasgetimgurl)`.

The created image will have an identifier unique to this Canvas, and subsequent calls to `[Canvas.getImage](#method-canvasgetimage)` and `[Canvas.setImage](#method-canvassetimage)` with the name passed to this function will act on the image object produced by the HTML returned from this call.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| src | [SCImgURL](../reference.md#type-scimgurl) | false | — | URL local to the skin or application directory.  
NOTE: instead of passing several parameters, you can pass an object as the 'src' parameter with properties for all the various function parameters with, eg:  
canvas.imgHTML( {src:"foo", width:10, height:10} ); |
| width | [number](#type-number) | true | — | width of the image |
| height | [number](#type-number) | true | — | height of the image |
| name | [String](#type-string) | true | — | name for the image |
| extraStuff | [String](#type-string) | true | — | additional attributes to write in the tag |
| imgDir | [String](#type-string) | true | — | image-specific image directory to override the default for this Canvas |

### Returns

`[String](#type-string)` — HTML to draw the image.

### Groups

- images

**Flags**: A

---
## Method: Canvas.getScrollRight

### Description
Returns the scrollLeft required to scroll horizontally to the end of this widget's content.

### Returns

`[int](../reference.md#type-int)` — scroll bottom coordinate

### Groups

- scrolling

---
## Method: Canvas.dragStop

### Description
Executed when the mouse button is released at the end of the drag. Your widget can use this opportunity to fire code based on the last location of the drag or reset any visual state that was sent.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel drag interaction.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.updateEditNode

### Description
When using the [Dashboards & Tools](../kb_topics/devTools.md#kb-topic-dashboards--tools-framework-overview) framework and asking an [EditContext](EditContext.md#class-editcontext) to [serialize EditNodes](EditContext.md#method-editcontextserializealleditnodes), `updateEditNode` is called during the serialization process on each [liveObject](EditNode.md#attr-editnodeliveobject).

You can implement `updateEditNode` on your `liveObject` and make updates to [EditNode.defaults](EditNode.md#attr-editnodedefaults) to save state "lazily" - just as serialization is occurring - instead of updating `editNode.defaults` as the end user makes changes. This can be useful if constantly calculating changes to `editNode.defaults` would slow down interactivity.

Note: best practice is to use [EditContext.setNodeProperties](EditContext.md#method-editcontextsetnodeproperties) and [EditContext.removeNodeProperties](EditContext.md#method-editcontextremovenodeproperties) to change properties, rather than directly modifying [EditNode.defaults](EditNode.md#attr-editnodedefaults).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| editContext | [EditContext](#type-editcontext) | false | — | the EditContext |
| editNode | [EditNode](#type-editnode) | false | — | the EditNode |

---
## Method: Canvas.removeRuleContext

### Description
Remove data in the rule context at the specified `path` along with any user-provided schema.

Normally data is removed from the ruleContext by passing `null` to `data` in [Canvas.provideRuleContext](#method-canvasproviderulecontext), however, this call will do the same but also removes the schema as explicitly provided to provideRuleContext.

Data automatically provided to the ruleContext, as described by [Canvas.ruleScope](#attr-canvasrulescope), along with the associated schema is automatically removed when the contributing DataBoundComponent is destroyed. Therefore there is no need to clean up those ruleContext paths manually.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| path | [String](#type-string) | false | — | path where data and schema should be removed |

---
## Method: Canvas.getOffsetX

### Description
Return the X-coordinate of the last event relative to the left edge of the content of this Canvas.  
  
NOTE: To get a coordinate relative to the **viewport** of this Canvas, subtract this.getScrollLeft()

### Returns

`[number](#type-number)` — —

### Groups

- events
- positioning

---
## Method: Canvas.focus

### Description
If this canvas can accept focus, give it keyboard focus. After this method, the canvas will appear focused and will receive keyboard events.

### Groups

- focus

---
## Method: Canvas.resizeBy

### Description
Resizes the widget, adding deltaX to its width and deltaY to its height (moves the right and/or bottom sides of the widget).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| deltaX | [number](#type-number) | true | — | amount to resize horizontally (may be negative) |
| deltaY | [number](#type-number) | true | — | amount to resize vertically (may be negative) |

### Returns

`[Boolean](#type-boolean)` — whether the component actually changed size

### Groups

- sizing

---
## Method: Canvas.showClickMask

### Description
Show a clickMask over the entire screen that intercepts mouse clicks and fires some action. The mask created will be associated with this canvas - calling this method multiple times will not show multiple (stacked) clickMasks if the mask associated with this canvas is already up.

The clickMask useful for modal dialogs, menus and similar uses, where any click outside of some Canvas should either be suppressed (as in a modal dialog) or just cause something (like dismissing a menu).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| clickAction | [Callback](../reference.md#type-callback) | false | — | action to fire when the user clicks on the mask |
| mode | [ClickMaskMode](../reference.md#type-clickmaskmode) | false | — | whether to automatically hide the clickMask on mouseDown and suppress the mouseDown event from reaching the target under the mouse |
| unmaskedTargets | [Widget](#type-widget)|[Array of Widget](#type-array-of-widget) | false | — | initially unmasked targets for this clickMask. Note that if this is a `"hard"` mask, unmasked children of masked parents are not supported so any non-top-level widgets passed in will have their parents unmasked. Children of unmasked parents can never be masked, so you need only include the top widget of a hierarchy. |

### Returns

`[String](#type-string)` — clickMask ID

### Groups

- clickMask

### See Also

- [Canvas.hideClickMask](#method-canvashideclickmask)
- [Canvas.showComponentMask](#method-canvasshowcomponentmask)

---
## Method: Canvas.dropOver

### Description
Executed when the compatible dragged object is first moved over this drop target. Your implementation can use this to show a custom visual indication that the object can be dropped here.

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.getByLocalId

### Description
Retrieve a child of this Canvas by it's [local ID](#method-canvasgetlocalid).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| localId | [String](#type-string) | false | — | local ID of the Canvas |

### Returns

`[Canvas](#type-canvas)` — the Canvas, or null if not found

---
## Method: Canvas.focusInNextTabElement

### Description
Shifts focus to the next focusable element after this one. This programatically simulates the user experience of a Tab keypress, and is used automatically when a blocking [clickMask](#method-canvasshowclickmask) is up to ensure focus does not move to any masked elements in the UI.

This method makes use of the [TabIndexManager.shiftFocus](TabIndexManager.md#classmethod-tabindexmanagershiftfocus) method to request focus be changed to the adjacent registered entry. By default standard focusable SmartClient UI elements, including Canvases, FormItems, FormItemIcons, etc are registered with the TabIndexManager in the appropriate order, and will accept focus if [focusable](#attr-canvascanfocus), and not [disabled](FormItem.md#attr-formitemdisabled) or [masked](#method-canvasshowclickmask).

The TabIndexManager maintains a hierarchy of focusable targets - so if a parent canvas contains focusable children, they will typically be nested under the parent canvas in this hierarchy. If you want to shift focus to the next target outside this hierarchy (IE: skip any children and put focus into the next widget on the page outside this one), you can use use [Canvas.focusAfterGroup](#method-canvasfocusaftergroup).

**NOTE:** Focusable elements created directly in the raw HTML bootstrap or by application code will not be passed focus by this method unless they have also been explicitly registered with the TabIndexManager. See the [tabOrderOverview](../kb_topics/tabOrderOverview.md#kb-topic-tab-order-overview) for more information.

### Groups

- focus

### See Also

- [Canvas.tabIndex](#attr-canvastabindex)
- [Canvas.focusInPreviousTabElement](#method-canvasfocusinprevioustabelement)
- [Canvas.focusAfterGroup](#method-canvasfocusaftergroup)

---
## Method: Canvas.getRuleContext

### Description
Get the current value of the rule context collected by the [Canvas.ruleScope](#attr-canvasrulescope) of this component (which may be this component itself or whatever component is managing the `ruleScope` for this component).

If the `databoundOnly` parameter is passed as true, only data from components that actually have a [DataSource](DataSource.md#class-datasource) is included.

Use [Canvas.ruleContextChanged](#method-canvasrulecontextchanged) to get a notification of changes to the rule context.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| databoundOnly | [boolean](../reference.md#type-boolean) | true | — | whether to include only data from components that have a [DataSource](DataSource.md#class-datasource) |

### Returns

`[Object](../reference.md#type-object)` — the ruleContext object, or null if canvas is not part of a ruleScope

---
## Method: Canvas.setRect

### Description
Set all four coordinates, relative to the enclosing context, at once.

Moves the widget so that its top-left corner is at the specified top-left coordinates, then resizes it to the specified width and height.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number)|[Array](#type-array)|[Object](../reference.md#type-object) | true | — | new left coordinate, Array of coordinates in parameter order, or Object with left, top, width, height properties. If an Array or Object is passed, the remaining parameters are ignored. |
| top | [number](#type-number) | true | — | new top coordinate |
| width | [number](#type-number) | true | — | new width |
| height | [number](#type-number) | true | — | new height |

### Returns

`[boolean](../reference.md#type-boolean)` — whether the component's size actually changed

### Groups

- positioning
- sizing

---
## Method: Canvas.dragRepositionStart

### Description
Executed when dragging first starts. No default implementation. Create this handler to set things up for the drag reposition.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel the drag reposition action

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.showNextTo

### Description
Show this widget next to another widget on the page, positioned such that it will not extend beyond the browser viewport.

Note that this method simply sets the coordinates of the widget and displays it (using a [Canvas.animateShow](#method-canvasanimateshow) by default). It will not change the [Canvas.parentElement](#attr-canvasparentelement) of either component.

An example use case might be showing a menu next to a menu-button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| otherWidget | [Canvas](#type-canvas) | false | — | Canvas to show next to |
| side | [String](#type-string) | true | — | Which side of the other canvas should we put. Options are "top", "bottom", "left", "right". (Defaults to "right") |
| canOcclude | [boolean](../reference.md#type-boolean) | true | — | This argument controls whether this canvas can be positioned on top of the other widget if there isn't room to put it next to the other widget extending out of the browser viewport  
If 'canOcclude' is true, simply shift this widget over the other widget, so that it ends up onscreen. If 'canOcclude' is false, avoid extending offscreen by positioning this widget on the other side of the other widget. |
| skipAnimation | [boolean](../reference.md#type-boolean) | true | — | If `false` do not use an animation to show the component. |

---
## Method: Canvas.showContextMenu

### Description
Executed when the right mouse button is clicked. The default implementation of this method auto-creates a [Menu](Menu.md#class-menu) from the [Canvas.contextMenu](#attr-canvascontextmenu) property on this component and then calls [Menu.showContextMenu](Menu.md#method-menushowcontextmenu) on it to show it.

If you want to show a standard context menu, you can simply define your Menu and set it as the contextMenu property on your component - you do not need to override this method.

If you want to do some other processing before showing a menu or do something else entirely, then you should override this method. Note that the return value from this method controls whether or not the native browser context menu is shown.

### Returns

`[boolean](../reference.md#type-boolean)` — false == don't show native context menu, true == show native context menu

### Groups

- widgetEvents

### See Also

- [Canvas.contextMenu](#attr-canvascontextmenu)
- [Menu.showContextMenu](Menu.md#method-menushowcontextmenu)
- [Canvas.hideContextMenu](#method-canvashidecontextmenu)
- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.isVisible

### Description
Returns true if the widget is visible, taking all parents into account, so that a widget which is not hidden might still report itself as not visible if it is within a hidden parent.

NOTE: Undrawn widgets will report themselves as visible if they would be visible if drawn.

### Returns

`[boolean](../reference.md#type-boolean)` — true if the widget is visible, false otherwise

### Groups

- visibility

---
## Method: Canvas.scrollTo

### Description
Scrolls the content of the widget so that the origin (top-left corner) of the content is left pixels to the left and top pixels above the widget's top-left corner (but still clipped by the widget's dimensions).

This is guaranteed to be called whenever this Canvas is scrolled, whether scrolling is initiated programmatically, by custom scrollbars, or a by a native scrollbar.

Note: If you attempt to call this API before the widget is drawn, the call will be ignored.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Integer](../reference_2.md#type-integer) | true | — | the left coordinate |
| top | [Integer](../reference_2.md#type-integer) | true | — | the top coordinate |

### Groups

- scrolling

---
## Method: Canvas.focusAtEnd

### Description
Shifts focus to the start or end of this canvas and its descendants.

This method makes use of the [TabIndexManager.shiftFocusWithinGroup](TabIndexManager.md#classmethod-tabindexmanagershiftfocuswithingroup) API to request focus be changed within the set of focusable targets registered under this canvas.

If the `start` parameter is true, if the canvas itself is focusable it will be given focus, otherwise the first focusable descendant will be given focus. If the `start` parameter is false, the last focusable descendant will be given focus (or if the canvas itself is focusable but there are no focusable descendants, it will receive focus).

A use case for this might be to programmatically shift focus to the first or last button in a toolbar or similar.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [boolean](../reference.md#type-boolean) | false | — | Should we focus at the start or the end of this widget and its descendants. |

---
## Method: Canvas.getAriaStateDefaults

### Description
Retrieves dynamically calculated default ARIA state properties for this canvas. These will be combined with [explicitly specified aria state](#attr-canvasariastate) and applied to the widget handle as described in [Canvas.getAriaState](#method-canvasgetariastate).

For [disabled canvases](#attr-canvasdisabled), this method returns an object with `disabled` set to true. May be overridden to apply additional defaults in canvas subclasses.

### Returns

`[Object](../reference.md#type-object)` — dynamically calculated default aria state properties

**Flags**: A

---
## Method: Canvas.rightMouseDown

### Description
Executed when the right mouse button is pressed on this widget. No default implementation.

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.disable

### Description
Disables this widget and any children and peers of this widget.

### Groups

- enable

---
## Method: Canvas.pageScrollDown

### Description
This method is the programmatic equivalent of the user pressing the "Page Down" key while this widget has the focus. It scrolls the widget's content downwards by the viewport height, if the content can be scrolled that far downwards

---
## Method: Canvas.getViewportHeight

### Description
Returns the height of the viewport onto the scrollable content.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — height of the viewport, in pixels

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.getBottom

### Description
Return the bottom coordinate of this object as rendered, relative to its enclosing context, in pixels.

### Returns

`[number](#type-number)` — bottom coordinate

### Groups

- positioning
- sizing

---
## Method: Canvas.setDisabled

### Description
set the disabled state of this object

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| disabled | [boolean](../reference.md#type-boolean) | false | — | new disabled state of this object - pass `true` to disable the widget |

### Groups

- enable

**Flags**: A

---
## Method: Canvas.setTabIndex

### Description
Assign an explicit [Canvas.tabIndex](#attr-canvastabindex) to this widget at runtime.

Developers may also call [Canvas.clearExplicitTabIndex](#method-canvasclearexplicittabindex) to clear any explicitly assigned tab index, and have the widget participate in automatic tab position allocation. For more information see [Canvas.tabIndex](#attr-canvastabindex)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| tabIndex | [number](#type-number) | false | — | New tabIndex for this widget. Must be less than [Canvas.TAB_INDEX_FLOOR](#classattr-canvastab_index_floor) to avoid interfering with auto-assigned tab indices on the page. |

### Groups

- focus

### See Also

- [Canvas.tabIndex](#attr-canvastabindex)

**Flags**: A

---
## Method: Canvas.containsPoint

### Description
Return whether or not this object contains the specified global (x,y) coordinates.

Will return false if any parent canvas does not contain the specified point, (EG: you're hovering over an element's absolute location, but it is scrolled out of view in a parent element)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [int](../reference.md#type-int) | false | — | GLOBAL x-coordinate |
| y | [int](../reference.md#type-int) | false | — | GLOBAL y-coordinate |
| withinViewport | [Boolean](#type-boolean) | true | — | point lies specifically within our viewport (drawn area excluding margins and scrollbars if present) |

### Returns

`[Boolean](#type-boolean)` — true if this object contains the specified point; false otherwise

### Groups

- positioning

**Flags**: A

---
## Method: Canvas.setDataContext

### Description
Provides a new [DataContext](../reference.md#object-datacontext) to the Canvas. If the DataContext is new, [DataBoundComponents](../reference.md#interface-databoundcomponent) contained within this Canvas will be automatically bound as described in [Canvas.dataContext](#attr-canvasdatacontext). If the DataContext replaces an existing one, any contained components that were originally bound against the DataContext will be re-bound.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataContext | [DataContext](#type-datacontext) | false | — | dataContext to use for automatic binding |

### Groups

- dataContext

---
## Method: Canvas.setSnapOffsetLeft

### Description
Setter for [Canvas.snapOffsetLeft](#attr-canvassnapoffsetleft).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| snapOffsetLeft | [Integer](../reference_2.md#type-integer) | false | — | new snapOffsetLeft value. |

### Groups

- snapGridDragging

---
## Method: Canvas.setPanelContainer

### Description
Sets this Canvas's "panel container". A panel container is a widget that manages a collection of panels, like a [TabSet](TabSet.md#class-tabset) or [SectionStack](SectionStack.md#class-sectionstack). SmartClient uses this method internally when child panels are added to panel container widgets; if you need to create a panel container widget that does not extend one of the built-in ones (these are `TabSet`, `SectionStack` and [Window](Window.md#class-window)), your code should do the same thing.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| container | [Canvas](#type-canvas) | false | — | The container widget for this canvas |

---
## Method: Canvas.getHoverComponent

### Description
When [Canvas.showHoverComponents](#attr-canvasshowhovercomponents) is true, this method is called to get the component to show as a hover for this Canvas. There is no default implementation of this method, so you need to override it with an implementation that returns a Canvas that suits your needs.

By default, components returned by `getHoverComponent()` will not be automatically destroyed when the hover is hidden. To enforce this, set [Canvas.hoverAutoDestroy](#attr-canvashoverautodestroy) to true on the returned component.

### Returns

`[Canvas](#type-canvas)|[Canvas Properties](#type-canvas-properties)` — the component to show as a hover

### Groups

- hoverComponents

### See Also

- [Canvas.hoverScreen](#attr-canvashoverscreen)

---
## Method: Canvas.dragStart

### Description
Executed when dragging first starts. Your widget can use this opportunity to set things up for the drag, such as setting the drag tracker. Returning false from this event handler will cancel the drag action entirely.

A drag action is considered to be begin when the mouse has moved [Canvas.dragStartDistance](#attr-canvasdragstartdistance) with the left mouse down.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel drag action.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.focusChanged

### Description
Notification function fired when this widget receives or loses keyboard focus.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hasFocus | [boolean](../reference.md#type-boolean) | false | — | If true this widget now has keyboard focus |

### Groups

- focus

---
## Method: Canvas.getScrollLeft

### Description
Get the number of pixels this Canvas is scrolled from its left edge.

### Returns

`[number](#type-number)` — scrollLeft

### Groups

- positioning
- scrolling

**Flags**: A

---
## Method: Canvas.focusAfterGroup

### Description
Shifts focus to the next focusable element after this one, skipping any elements nested inside the tabbing group for this canvas, such as focusable children.

This method makes use of the [TabIndexManager.shiftFocusAfterGroup](TabIndexManager.md#classmethod-tabindexmanagershiftfocusaftergroup) method to request focus be changed to the next registered entry. By default standard focusable SmartClient UI elements, including Canvases, FormItems, FormItemIcons, etc are registered with the TabIndexManager in the appropriate order, and will accept focus if [focusable](#attr-canvascanfocus), and not [disabled](FormItem.md#attr-formitemdisabled) or [masked](#method-canvasshowclickmask).

This method differs from [Canvas.focusInNextTabElement](#method-canvasfocusinnexttabelement) in that it will skip any descendants of this widget in the TabIndexManager's hierarchy of potential focus target. By default this means focus will be moved to the next target on the page which is not a descendant of this widget.

FormItems support a similar method: [FormItem.focusAfterItem](FormItem.md#method-formitemfocusafteritem).

**NOTE:** Focusable elements created directly in the raw HTML bootstrap or by application code will not be passed focus by this method unless they have also been explicitly registered with the TabIndexManager. See the [tabOrderOverview](../kb_topics/tabOrderOverview.md#kb-topic-tab-order-overview) for more information.

### Groups

- focus

### See Also

- [Canvas.tabIndex](#attr-canvastabindex)
- [Canvas.focusInNextTabElement](#method-canvasfocusinnexttabelement)

---
## Method: Canvas.getScrollHeight

### Description
Returns the scrollable height of the widget's contents, including children, ignoring clipping.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — height of the element that can scroll

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.getScrollbarSize

### Description
Returns the thickness of this widget's scrollbars.  
For canvases showing custom scrollbars this is determined from `this.scrollbarSize`

### Returns

`[number](#type-number)` — thickness of the scrollbars, in pixels

### Groups

- scrolling

### See Also

- [Canvas.scrollbarSize](#attr-canvasscrollbarsize)

**Flags**: A

---
## Method: Canvas.setPageTop

### Description
Set the page-relative top coordinate of this widget.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| top | [number](#type-number) | false | — | new top coordinate in pixels |

### Groups

- positioning

---
## Method: Canvas.hover

### Description
If `canHover` is true for this widget, the `hover` string method will be fired when the user hovers over this canvas. If this method returns false, it will suppress the default behavior of showing a hover canvas if `this.showHover` is true.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel the hover event.

### Groups

- hovers

### See Also

- [Canvas.canHover](#attr-canvascanhover)

---
## Method: Canvas.isFocused

### Description
Returns true if this Canvas has the keyboard focus. Note that in Internet Explorer focus notifications can be asynchronous (see [EventHandler.synchronousFocusNotifications](EventHandler.md#classattr-eventhandlersynchronousfocusnotifications)). In this case, `canvas.isFocused()` method can correctly return false when, intuitively, you would expect it to return true:
```
     someCanvas.focus();
     if (someCanvas.isFocused()) {
         // In most browsers we would get here, but not in Internet Explorer with
         // EventHandler.synchronousFocusNotifications disabled.
     }
```

### Returns

`[Boolean](#type-boolean)` — whether this Canvas has the keyboard focus

### See Also

- [Canvas.containsFocus](#method-canvascontainsfocus)

---
## Method: Canvas.getLeft

### Description
Return the left coordinate of this object, relative to its enclosing context, in pixels.

### Returns

`[Number](#type-number)` — left coordinate

### Groups

- positioning

---
## Method: Canvas.provideRuleContext

### Description
Provide data to the [Canvas.ruleScope](#attr-canvasrulescope) component, to be made available in the rule context at the specified `path`.

`path` must be one or more valid identifiers with either dot (.) or slash (/) used as a separator.

`data` can be any value, including both atomic values like a Boolean or String, or a nested data structure. Pass `data` as `null` to remove data from the context at the specified `path`. When a DataSource is passed to define the provided data type (described below) a call to [Canvas.removeRuleContext](#method-canvasremoverulecontext) is the correct way to remove the data along with the schema.

`dbc` is the DataBoundComponent to be identified as the owner of the rule context contribution. This component is used to handle any conflicts between multiple components contributing to the same base path (i.e. first segment of path). For any collision an editable display (such as a form or editable grid) wins over a static display (such as a non-editable grid with a selection). Hidden or cleared components have lowest priority even if editable. For two editable components the first becomes the owner.

`dbc` can also be a DataSource to define the data type of the provided data. For example, when a singular Date value is provided to the ruleContext the type is not known when using the value in a ruleCriteria. To counter that, a data type can be specified using a DataSource and optionally a `fieldName`. The path will then be associated with the DataSource and fieldName so criteria processing knows to compare the value correctly. When providing data as a Record or array of Records only the DataSource is needed.

See [ruleCriteria](../kb_topics/ruleCriteria.md#kb-topic-dynamic-rules) for details on matching values within criteria when schema is not provided.

Note that DataBoundComponents automatically contribute to the ruleContext as described in [Canvas.ruleScope](#attr-canvasrulescope).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| path | [String](#type-string) | false | — | path where data should be made available |
| data | [Any](#type-any) | false | — | data to contribute to rule context |
| dbc | [DataBoundComponent](#type-databoundcomponent)|[DataSource](#type-datasource) | true | — | dataBoundComponent contributing to ruleContext or DataSource defining the provided data type |
| fieldName | [String](#type-string) | true | — | field name within DataSource defining the data type for a singular value (i.e. not a Record and not an Array of Records) |

---
## Method: Canvas.setDataPath

### Description
Setter for the [Canvas.dataPath](#attr-canvasdatapath) attribute. This method may be called directly at runtime to set the dataPath on a component, and will also be re-run automatically whenever a canvas' parent changes due to a call to addChild(). This method handles automatically binding the component to the appropriate valuesManager if necessary.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| dataPath | [DataPath](../reference_2.md#type-datapath) | false | — | new dataPath |

---
## Method: Canvas.getSnapEdge

### Description
Return the snapEdge value of this object

### Returns

`[String](#type-string)` — snapEdge

### Groups

- snapPositioning

---
## Method: Canvas.setHtmlPosition

### Description
Setter for the [Canvas.htmlPosition](#attr-canvashtmlposition).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| element | [DrawPosition](../reference_2.md#type-drawposition) | false | — | New htmlPosition for this canvas |

### Groups

- htmlElement

---
## Method: Canvas.print

### Description
Generate and show a [PrintWindow](../reference.md#class-printwindow) containing a [PrintCanvas](PrintCanvas.md#class-printcanvas) showing a printable view of this component.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| printProperties | [PrintProperties](#type-printproperties) | true | — | PrintProperties object for customizing the print HTML output |
| printWindowProperties | [PrintWindow Properties](#type-printwindow-properties) | true | — | Properties to apply to the generated print window. |
| callback | [Callback](../reference.md#type-callback) | true | — | callback to fire when the print preview canvas has been populated with the printable HTML. This callback takes 2 parameters: `printPreview` - a pointer to the generated print canvas shown in the body of the print window. `printWindow` - a pointer to the generated print window and |

### Groups

- printing

### See Also

- [Canvas.showPrintPreview](#classmethod-canvasshowprintpreview)

---
## Method: Canvas.intersects

### Description
Returns true if the rectangles of this widget and the specified widget overlap.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| other | [Canvas](#type-canvas) | false | — | other canvas to test for intersection |

### Returns

`[Boolean](#type-boolean)` — true if this canvas intersects other; false otherwise

### Groups

- positioning

---
## Method: Canvas.adaptHeightBy

### Description
See [Canvas.canAdaptWidth](#attr-canvascanadaptwidth).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pixelDifference | [Integer](../reference_2.md#type-integer) | false | — | surplus (if positive) or overflow (if negative) |
| unadaptedHeight | [Integer](../reference_2.md#type-integer) | false | — | height of member currently assumed by parent layout |

### Returns

`[Integer](../reference_2.md#type-integer)` — sizeDelta

---
## Method: Canvas.drawn

### Description
Notification method fired when a canvas has been drawn into the page.

---
## Method: Canvas.setMinWidth

### Description
Resizes the widget horizontally if required to satisfy the specified [Canvas.minWidth](#attr-canvasminwidth).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| width | [number](#type-number) | false | — | new minimum width |

### Groups

- sizing

---
## Method: Canvas.setShowShadow

### Description
Method to update [Canvas.showShadow](#attr-canvasshowshadow).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| showShadow | [boolean](../reference.md#type-boolean) | false | — | true if the shadow should be visible false if not |

### Groups

- shadow

---
## Method: Canvas.dragResizeStart

### Description
Executed when resize dragging first starts. No default implementation. Create this handler to set things up for the drag resize.

### Returns

`[boolean](../reference.md#type-boolean)` — false to cancel the drag reposition action

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.getParentCanvas

### Description
Returns the parent of this canvas, if any.

See [containment](../kb_topics/containment.md#kb-topic-component-containment-and-hierarchy) for an overview of parent/child relationships.

### Returns

`[Canvas](#type-canvas)` — the parent canvas, null if none exists.

### Groups

- containment

---
## Method: Canvas.setBackgroundImage

### Description
Sets the background to an image file given by newImage. This URL should be given as a string relative to the image directory for the page (./images by default).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newImage | [SCImgURL](../reference.md#type-scimgurl) | false | — | new URL (local to Page image directory) for background image |

### Groups

- appearance

---
## Method: Canvas.getInnerWidth

### Description
Returns the amount of space available for absolutely positioned child widget(s) or absolutely positioned HTML content, without introducing clipping, scrolling or overflow.

This is the space within the viewport of the widget (including padding, but excluding margins, borders or scrollbars) rendered at its specified size.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — inner width of the widget in pixels

### Groups

- sizing

### See Also

- [Canvas.getInnerHeight](#method-canvasgetinnerheight)
- [Canvas.getInnerContentHeight](#method-canvasgetinnercontentheight)
- [Canvas.getInnerContentWidth](#method-canvasgetinnercontentwidth)

**Flags**: A

---
## Method: Canvas.setLeavePageSpace

### Description
Setter for [leavePageSpace](#attr-canvasleavepagespace).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newPageSpace | [Integer](../reference_2.md#type-integer) | false | — | new value for `leavePageSpace`. |

### Groups

- positioning

**Flags**: A

---
## Method: Canvas.updateHover

### Description
If this canvas is currently showing a hover (see [Canvas.handleHover](#method-canvashandlehover)), this method can be called to update the HTML contents of the hover. Has no effect if this widget is showing [hover-components instead of simple HTML](#attr-canvasshowhovercomponents), or if the hover canvas is not showing for this widget.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hoverHTML | [String](#type-string) | true | — | Option to specify new HTML for the hover. If not passed, the result of [this.getHoverHTML()](#method-canvasgethoverhtml) will be used instead. Note that if the hover HTML is empty the hover will be hidden. |

### Groups

- hovers

**Flags**: A

---
## Method: Canvas.keyDown

### Description
Executed when a key is pressed on a focusable widget ([Canvas.canFocus](#attr-canvascanfocus): true).

Use [EventHandler.getKey](EventHandler.md#classmethod-eventhandlergetkey) to find out the [keyName](../reference.md#type-keyname) of the key that was pressed, and use [EventHandler.shiftKeyDown](EventHandler.md#classmethod-eventhandlershiftkeydown) and related functions to determine whether modifier keys were down.

### Returns

`[boolean](../reference.md#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.canFocus](#attr-canvascanfocus)

**Flags**: A

---
## Method: Canvas.removePeer

### Description
Remove a peer from this Canvas

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| peer | [Canvas](#type-canvas) | false | — | Peer to be removed from this canvas |
| name | [String](#type-string) | true | — | If this peer was assigned a name when added via addPeer(), it should be passed in here to ensure no reference is kept to the peer |

### Groups

- containment

---
## Method: Canvas.moved

### Description
Notification method fired when this component is explicitly moved. Note that a component's position on the screen may also changed due to an ancestor being moved. The [Canvas.parentMoved](#method-canvasparentmoved) method provides a notification entry point to catch that case as well.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| deltaX | [int](../reference.md#type-int) | false | — | horizontal difference between current and previous position |
| deltaY | [int](../reference.md#type-int) | false | — | vertical difference between current and previous position |

---
## Method: Canvas.addChild

### Description
Adds newChild as a child of this widget, set up a named object reference (i.e., this\[name\]) to the new widget if name argument is provided, and draw the child if this widget has been drawn already.

If newChild has a parent it will be removed from it. If it has a master, it will be detached from it if the master is a child of a different parent. If newChild has peers, they'll be added to this widget as children as well.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newChild | [Canvas](#type-canvas) | false | — | new child canvas to add |
| name | [String](#type-string) | true | — | name to assign to child (eg: this\[name\] == child) |
| autoDraw | [Boolean](#type-boolean) | true | — | if false, child will not automatically be drawn (only for advanced use) |

### Returns

`[Canvas](#type-canvas)` — the new child, or null if it couldn't be added

### Groups

- containment

---
## Method: Canvas.mouseUp

### Description
Executed when the left mouse is released on this widget. No default implementation.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.setPageLeft

### Description
Set the page-relative left coordinate of this widget.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [number](#type-number) | false | — | new left coordinate in pixels |

### Groups

- positioning

---
## Method: Canvas.addSnapAlignCandidate

### Description
Add a candidate to [Canvas.snapAlignCandidates](#attr-canvassnapaligncandidates). Duplicates are automatically avoided.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newCandidate | [Canvas](#type-canvas) | false | — | — |

---
## Method: Canvas.isDirty

### Description
Returns whether a canvas is waiting to be redrawn. Will return true if [Canvas.markForRedraw](#method-canvasmarkforredraw) has been called, but this canvas has not yet been redrawn.

### Returns

`[Boolean](#type-boolean)` — true is this canvas needs to be redrawn; false otherwise

### Groups

- drawing

**Flags**: A

---
## Method: Canvas.mouseOver

### Description
Executed when mouse enters this widget. No default implementation.

### Returns

`[Boolean](#type-boolean)` — false to prevent this event from bubbling to this widget's parent, true or undefined to bubble.

### Groups

- widgetEvents

### See Also

- [Canvas.getOffsetX](#method-canvasgetoffsetx)
- [Canvas.getOffsetY](#method-canvasgetoffsety)

**Flags**: A

---
## Method: Canvas.init

### Description
This method performs some basic initialization common to all UI components. To do custom UI component initialization, you should generally override [Canvas.initWidget](#method-canvasinitwidget). This method does the following, in order:

*   Sets up a global reference to this instance as described in [Canvas.ID](#attr-canvasid).
*   Ensures certain numeric properties have numeric values (e.g. width, height, padding, margin)
*   Ensures [Canvas.children](#attr-canvaschildren) and [Canvas.peers](#attr-canvaspeers) are Arrays.
*   Calls [Canvas.initWidget](#method-canvasinitwidget)
*   Creates [edges](#attr-canvasshowedges) and [shadow](#attr-canvasshowshadow), if so configured.
*   Calls [Canvas.draw](#method-canvasdraw) if [Canvas.autoDraw](#attr-canvasautodraw) is set on instance or globally.

Unless you're in an advanced scenario where you need to inject code before the above logic executes, place your initialization logic in initWidget() rather than init(). If you do decided to override this method, you must call the superclass implementation like so:
```
    this.Super("init", arguments);
 
```

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| arguments 0-N | [Any](#type-any) | true | — | All arguments initially passed to [Class.create](Class.md#classmethod-classcreate) |

**Flags**: A

---
## Method: Canvas.setHeight

### Description
Resizes the widget vertically to the specified height (moves the bottom side of the widget). The height parameter can be expressed as a percentage of viewport size or as the number of pixels.

NOTE: if you're setting multiple coordinates, use resizeTo() or setRect() instead

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [Number](#type-number)|[String](#type-string) | false | — | new height |

### Groups

- sizing

---
## Method: Canvas.getPageLeft

### Description
Returns the page-relative left coordinate of the widget on the page, in pixels.

### Returns

`[number](#type-number)` — global left coordinate

### Groups

- positioning

**Flags**: A

---
## Method: Canvas.moveAbove

### Description
Puts this widget just above the specified widget in the stacking order, so it appears in front of the specified widget if both widgets have the same parent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| canvas | [Canvas](#type-canvas) | false | — | canvas to move above |

### Groups

- zIndex

---
## Method: Canvas.getVisibleHeight

### Description
Return the visible height of the Canvas.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — visible height in pixels

### Groups

- sizing

**Flags**: A

---
## Method: Canvas.getInnerContentWidth

### Description
Returns the amount of space available for interior content (or relatively positioned child widget(s)) without introducing clipping, scrolling or overflow.  
This is the space within the viewport of the widget (not including padding, and excluding margins, borders or scrollbars) rendered at its specified size.

See [gettingCanvasSize](../kb_topics/gettingCanvasSize.md#kb-topic-determining-the-size-of-a-drawn-canvas)

### Returns

`[number](#type-number)` — inner height of the widget in pixels

### Groups

- sizing

### See Also

- [Canvas.getInnerContentHeight](#method-canvasgetinnercontentheight)
- [Canvas.getInnerHeight](#method-canvasgetinnerheight)
- [Canvas.getInnerWidth](#method-canvasgetinnerwidth)

**Flags**: A

---
## Method: Canvas.visibleAtPoint

### Description
Does this widget contain the specified global (x,y) coordinates, and have no other widgets also at the specified position, obscuring this one? This is commonly used for (for example) drag and drop interactions.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| x | [number](#type-number) | false | — | GLOBAL x-coordinate |
| y | [number](#type-number) | false | — | GLOBAL y-coordinate |
| withinViewport | [boolean](../reference.md#type-boolean) | true | — | point lies within our viewport rather than just our drawn area |
| ignoreWidgets | [Canvas](#type-canvas) | true | — | If passed ignore widget(s), do not check whether those widgets occludes this one. |
| upToParent | [Canvas](#type-canvas) | true | — | If passed, only check for siblings occluding the component up as far as the specified parent widget. |

### Returns

`[boolean](../reference.md#type-boolean)` — true if this object contains the specified point; false otherwise

### Groups

- positioning

**Flags**: A

---
## Method: Canvas.removeChild

### Description
Remove a child from this parent.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [Canvas](#type-canvas) | false | — | Child canvas to remove from this parent. |
| name | [String](#type-string) | true | — | If the child canvas was assigned a name when added via addChild(), it should be passed in here to ensure no reference is kept to the child |

### Groups

- containment

---
## Method: Canvas.getAriaHandleID

### Description
Returns the DOM ID for the main element for this canvas which will have ARIA [role](#attr-canvasariarole) and [attributes](#attr-canvasariastate) applied to it. This can be useful when applying [custom aria state attributes](#attr-canvasariastate) which need to refer to the DOM handle of another canvas, such as [aria-controls](https://www.w3.org/TR/2017/REC-wai-aria-1.1-20171214/#aria-controls).

Note that we do not recommend using this ID to identify the element in the DOM for integration with automated testing tools. The [AutoTest.getLocator](AutoTest.md#classmethod-autotestgetlocator) and [AutoTest.getElement](AutoTest.md#classmethod-autotestgetelement) APIs should be used instead. These locators are much finer grained - they allow developers to identify sub-elements within the widget handle that map to specific logical SmartClient objects (for example FormItem Icons within a DynamicForm). They are also more stable - AutoTest locators are able to reliably identify components based on their position in the application hierarchy and other context, while the DOM element IDs are not guaranteed not to change across page reloads.

### Returns

`[String](#type-string)` — ID written into the DOM element for this component

**Flags**: A

---
## Method: Canvas.deparent

### Description
Remove this canvas from its parent if it has one.

### Groups

- containment

---
## Method: Canvas.setSnapTo

### Description
Set the snapTo property of this canvas, and handle repositioning.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| snapTo | [String](#type-string) | false | — | new snapTo value |

### Groups

- snapGridDragging

---
## Method: Canvas.setLeft

### Description
Set the left coordinate of this object, relative to its enclosing context, in pixels. NOTE: if you're setting multiple coordinates, use setRect(), moveTo() or resizeTo() instead

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| left | [Number](#type-number)|[String](#type-string) | false | — | new left coordinate |

### Groups

- positioning

---
## Method: Canvas.setOverflow

### Description
Update the [overflow](#attr-canvasoverflow) of a Canvas after it has been created.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newOverflow | [Overflow](../reference.md#type-overflow) | false | — | New overflow value. |

### Groups

- positioning
- sizing
- sizing

**Flags**: A

---
## Method: Canvas.setPadding

### Description
Set the CSS padding of this component, in pixels. Padding provides space between the border and the component's contents.

This property sets the same thickness of padding on every side. Differing per-side padding can be set in a CSS style and applied via [Canvas.styleName](#attr-canvasstylename).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newPadding | [number](#type-number) | false | — | new padding in pixels |

### Groups

- appearance

---
## Method: Canvas.getScrollBottom

### Description
Returns the scrollTop required to scroll vertically to the end of this widget's content.

### Returns

`[int](../reference.md#type-int)` — scroll bottom coordinate

### Groups

- scrolling

---
## Method: Canvas.scrollToTop

### Description
Vertically scrolls the content of the widget to 0

### Groups

- scrolling

---
## Method: Canvas.setMinHeight

### Description
Resizes the widget vertically if required to satisfy the specified [Canvas.minHeight](#attr-canvasminheight).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| height | [number](#type-number) | false | — | new minimum height |

### Groups

- sizing

---
