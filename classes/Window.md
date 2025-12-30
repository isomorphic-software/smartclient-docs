# Window Documentation

[← Back to API Index](../reference.md)

---

## Class: Window

*Inherits from:* [Layout](Layout.md#class-layout)

### Description
A general purpose Window class for implementing dialogs, portlets, alerts, prompts, wizards and desktop-like windowing interfaces.

Windows can contain arbitrary SmartClient components, configured via the [Window.items](#attr-windowitems) property. Windows may be [modal](#attr-windowismodal) or non-modal.

Windows provide a series of highly configurable and skinnable [autoChildren](../reference.md#type-autochild) including a header, various header controls, footer, and corner resizer.

The more specialized [Dialog](Dialog.md#class-dialog) subclass of Window has additional functionality targetted at simple prompts and confirmations, such as buttons with default actions, and single-method [shortcuts](isc.md#staticmethod-iscwarn) for common application dialogs.

---
## ClassAttr: Window.HORIZONTAL

### Description
A declared value of the enum type [ContentLayoutPolicy](../reference.md#type-contentlayoutpolicy).

**Flags**: R

---
## ClassAttr: Window.VERTICAL

### Description
A declared value of the enum type [ContentLayoutPolicy](../reference.md#type-contentlayoutpolicy).

**Flags**: R

---
## ClassAttr: Window.NONE

### Description
A declared value of the enum type [ContentLayoutPolicy](../reference.md#type-contentlayoutpolicy).

**Flags**: R

---
## Attr: Window.hiliteHeaderStyle

### Description
Highlight style for the Window header. Displayed when a window is [flashed](#method-windowflash)

### Groups

- appearance
- header

**Flags**: IRWA

---
## Attr: Window.printBodyStyle

### Description
Style for the Window body in printed output.

**Flags**: IR

---
## Attr: Window.isModal

### Description
If true, when shown this Window will intercept and block events to all other existing components on the page.

Use [Window.showModalMask](#attr-windowshowmodalmask) to darken all other elements on the screen when a modal dialog is showing.

Chained modal windows - that is, modal windows that launch other modal windows - are allowed. You can accomplish this by simply creating a second modal Window while a modal Window is showing.

Note only top-level Windows (Windows without parents) can be modal.

### Groups

- modal

**Flags**: IRW

---
## Attr: Window.closeButton

### Description
Button show in the header that will close this Window by calling [Window.closeClick](#method-windowcloseclick).

**Flags**: R

---
## Attr: Window.restoreButton

### Description
ImgButton that restores the Window via [Window.restore](#method-windowrestore).

**Flags**: R

---
## Attr: Window.placement

### Description
Where should the window be placed on the screen? Valid settings include `"fillScreen"`, `"fillPanel"`, `"halfScreen"` and `"none"`

If not explicitly specified, default is to use [PanelPlacement](../reference.md#type-panelplacement) "fillScreen" if [Browser.isHandset](Browser.md#classattr-browserishandset), and "none" for non-handset devices.

If `window.placement` is something other than `"none"`, sizing and positioning settings (either explicit left, top, width, height settings or the [Window.autoCenter](#attr-windowautocenter) and [Window.autoSize](#attr-windowautosize) features) will have no effect.

**Flags**: IR

---
## Attr: Window.maximizeButton

### Description
Button that will make this Window fill the browser via [Window.maximize](#method-windowmaximize).

**Flags**: R

---
## Attr: Window.modalMaskStyle

### Description
Specifies the CSS style for the modal mask.

### Groups

- modal
- appearance

### See Also

- [Window.modalMask](#attr-windowmodalmask)

**Flags**: IR

---
## Attr: Window.showStatusBar

### Description
If true, show a statusBar for this Window, including resizer. Note that the status bar will only be displayed if the footer is showing for the window ([Window.showFooter](#attr-windowshowfooter)).

### Groups

- windowMembers
- appearance
- footer

**Flags**: IRW

---
## Attr: Window.showShadow

### Description
Whether to show a drop shadow for this Canvas.

Developers should be aware that the drop shadow is drawn outside the specified width and height of the widget meaning a widget with shadows takes up a little more space than it otherwise would. A full screen canvas with showShadow set to true as this would be likely to cause browser scrollbars to appear - developers can handle this by either setting this property to false on full-screen widgets, or by setting overflow to "hidden" on the `<body>` element browser-level scrolling is never intended to occur.

`showShadow` dynamically defaults to false when the [Window.placement](#attr-windowplacement) setting indicates the Window will be filling a portion of the screen or a panel.

**Flags**: IR

---
## Attr: Window.showTitle

### Description
Show a title (typically just text) on the header for this window.

### Groups

- windowHeader
- appearance
- headerLabel

**Flags**: IRW

---
## Attr: Window.headerControls

### Description
Array of members to show in the Window header.

The default value of `headerControls` is an Array of Strings listing the standard header controls in their default order:

```
    headerControls : ["headerIcon", "headerLabel", 
                      "minimizeButton", "maximizeButton", "closeButton"]
 
```
You can override `headerControls` to change the order of standard controls in the header. You can also omit standard controls this way, although it more efficient to use the related "show" property if available (eg [Window.showMinimizeButton](#attr-windowshowminimizebutton)).

By embedding a Canvas directly in this list you can add arbitrary additional controls to the header, for example, an additional button (eg return to dock) or a DynamicForm with various kinds of input controls.

Note that having added controls to headerControls, you can still call APIs directly on those controls to change their appearance, and you can also show() and hide() them if they should not be shown in some circumstances.

Tip: custom controls need to set layoutAlign:"center" to appear vertically centered.

**Component XML:**

To define `headerControls` in Component XML a special set of components are used as markers. The standard header controls can be explicitly specified as:

```
  <headerControls>
      <WindowHeaderIcon/>
      <WindowHeaderLabel/>
      <WindowMinimizeButton/>
      <WindowMaximizeButton/>
      <WindowCloseButton/>
  </headerControls>
 
```

### Groups

- windowHeader

**Flags**: IR

---
## Attr: Window.showBody

### Description
If true, draw the body contents when this Window is drawn.

### Groups

- windowMembers
- appearance
- body

**Flags**: IRWA

---
## Attr: Window.hiliteHeaderSrc

### Description
If [Window.showHeaderBackground](#attr-windowshowheaderbackground) is true, this governs the URL of the image to use in the header's highlighted state when the window is [flashed](#method-windowflash)

### Groups

- appearance
- header

**Flags**: IRWA

---
## Attr: Window.headerBackground

### Description
Img background component for the header, for gradient or image-based display

**Flags**: R

---
## Attr: Window.showHeader

### Description
If true, show a [Window.header](#attr-windowheader) for this Window.

Note that in certain Smartclient skins [Window.showHeaderBackground](#attr-windowshowheaderbackground) may be set to `false` and the header's appearance implemented as part of the window's [edge media](Canvas.md#attr-canvasshowedges). In this case suppressing the header can be achieved by overriding the edge media as well as setting this property to false. For example, to create a headerless window with a similar appearance to a [Menu](Menu.md#class-menu) in the `_TreeFrog_` skin, the following attributes could be used:

```
      showHeader:false,
      edgeImage:"[SKIN]/Menu/m.png",
      edgeSize:10, edgeTop:17, edgeBottom:17,
      edgeCenterBackgroundColor:"#F7F7F7"
 
```

### Groups

- windowMembers
- appearance
- header

**Flags**: IR

---
## Attr: Window.fillSpaceStyleName

### Description
Alternative style for the window used whenever [Window.placement](#attr-windowplacement) settings indicate the menu will be filling a portion of the screen or a panel. Generally this alternative style should not have rounded or excessively large edges.

**Flags**: IR

---
## Attr: Window.modalMask

### Description
A ScreenSpan instance used to darken the rest of a page when a modal window is active. To use, set [Window.showModalMask](#attr-windowshowmodalmask) to true, add a CSS style "modalMask" to the active skin (generally with background-color set), and adjust [Window.modalMaskOpacity](#attr-windowmodalmaskopacity).

### Groups

- modal
- appearance

**Flags**: R

---
## Attr: Window.headerIcon

### Description
Header icon shown at left end of header by default.

**Flags**: R

---
## Attr: Window.src

### Description
A URL to load as content for the Window's body. If specified, this attribute will take precedence over the items attribute.

Note that setting window.src is essentially a shortcut for setting [Window.items](#attr-windowitems) to a single HTMLflow with a specified [contentsURL](HTMLFlow.md#attr-htmlflowcontentsurl).

### Groups

- appearance
- body

### See Also

- [Window.contentsType](#attr-windowcontentstype)

**Flags**: IRW

---
## Attr: Window.maximized

### Description
Is this window maximized. If true at init time, the window will be drawn maximized. To set this property at runtime use [Window.maximize](#method-windowmaximize) or [Window.restore](#method-windowrestore).

### Groups

- appearance
- header

**Flags**: IRW

---
## Attr: Window.bringToFrontOnMouseUp

### Description
Should this window automatically be shown at the top of the page's z-order and be brought to front via [Canvas.bringToFront](Canvas.md#method-canvasbringtofront) whenever the user clicks it?

If [Window.isModal](#attr-windowismodal) is true for this window, this setting will have no effect - we always bring the window to the front on initial display and on mouseDown. By default we also do this for non-modal windows (which matches user expectation for most standard interfaces - think of switching between OS-level application windows), but this may be disabled for cases where it is not appropriate by setting this attribute to `false`

**Flags**: IRW

---
## Attr: Window.title

### Description
Title for this Window, shown if [Window.showTitle](#attr-windowshowtitle) is true in the [header](#attr-windowheader) (if drawn).

### Groups

- appearance
- headerLabel
- i18nMessages

**Flags**: IRW

---
## Attr: Window.dismissOnEscape

### Description
Should this window be dismissed (same effect as pressing the "Cancel" button) when the user presses the "Escape" key?  
Windows with this setting will dismiss on Escape keypresses in any of the following cases:

*   The window or one of its descendants has focus (and does not cancel the Escape keypress)
*   The window is [modal](#attr-windowismodal), and not itself masked. This ensures that focus is not on some unrelated element on the page.

If unset default behavior depends on whether a close / cancel button is visible for this item.

### See Also

- [Window.shouldDismissOnEscape](#method-windowshoulddismissonescape)

**Flags**: IRW

---
## Attr: Window.showResizer

### Description
If true, show a button in the lower right corner that allows users to resize the Window. Note that the resizer will only be displayed if the footer is showing for the window ([Window.showFooter](#attr-windowshowfooter)) and [Window.canDragResize](#attr-windowcandragresize) is true.

### Groups

- windowMembers
- appearance
- dragging

**Flags**: IRW

---
## Attr: Window.body

### Description
Body of the Window, where [contained components](../reference.md#kb-topic-form-items) or [loaded content](#attr-windowsrc) is shown.

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [bodyStyle](#attr-windowbodystyle) for the [Canvas.styleName](Canvas.md#attr-canvasstylename)
*   [printBodyStyle](#attr-windowprintbodystyle) for the `styleName` to use when printing
*   [bodyColor](#attr-windowbodycolor) / [hiliteBodyColor](#attr-windowhilitebodycolor) for the [Canvas.backgroundColor](Canvas.md#attr-canvasbackgroundcolor)

**Flags**: R

---
## Attr: Window.headerIconDefaults

### Description
This is an object literal property block specifying the various properties of the headerIcon - the icon that appears at the top left of the window and is by default the Isomorphic logo. Overrideable defaults are as follows:

*   width - default to `16` and specifies the width of the headerIcon.
*   height - default to `14` and specifies the height of the headerIcon.
*   src - defaults to `"[SKIN]/Window/minimize.gif"` and specifies the image for the headerIcon.

You can override the the above properties by calling [Class.changeDefaults](Class.md#classmethod-classchangedefaults).

### Groups

- appearance
- header

**Flags**: IRWA

---
## Attr: Window.showHeaderBackground

### Description
Should the window header show a background image? Default value is true for all browsers except for Internet Explorer.  
If set to true the image source is derived from [Window.headerSrc](#attr-windowheadersrc) and [Window.hiliteHeaderSrc](#attr-windowhiliteheadersrc), otherwise the background will be styled according to [Window.headerStyle](#attr-windowheaderstyle) / [Window.hiliteHeaderStyle](#attr-windowhiliteheaderstyle).

### Groups

- appearance
- header

**Flags**: IRA

---
## Attr: Window.minimizeButton

### Description
ImgButton shown in the header that will minimize this Window by calling [Window.minimize](#method-windowminimize).

**Flags**: R

---
## Attr: Window.bodyDefaults

### Description
Default properties for the body of the Window  
You can change the class-level bodyDefaults for all Windows by changing this item or set instance.body to be another object of properties to override for your instance only

### Groups

- appearance
- body

**Flags**: IRWA

---
## Attr: Window.canFocusInHeaderButtons

### Description
If true, the user can give the header buttons focus (see [Window.minimizeButton](#attr-windowminimizebutton), [Window.maximizeButton](#attr-windowmaximizebutton), [Window.restoreButton](#attr-windowrestorebutton) and [Window.closeButton](#attr-windowclosebutton)).

### Groups

- focus
- header

**Flags**: IRWA

---
## Attr: Window.bodyConstructor

### Description
The name of the widget class (as a string) to use for the body. If unset the appropriate constructor type will be determined as follows:  
\- if [Window.items](#attr-windowitems) is defined as an array of widgets, and [Window.contentLayout](#attr-windowcontentlayout) is not set to `"none"`, bodyConstructor defaults to a [VLayout](../reference.md#class-vlayout)  
\- if [Window.src](#attr-windowsrc) is set, bodyConstructor defaults to an [HTMLFlow](HTMLFlow.md#class-htmlflow)  
\- otherwise bodyConstructor will default to a simple [Canvas](Canvas.md#class-canvas)  
Note that if this property is overridden for some window, the specified constructor should be a subclass of one of these defaults to ensure the window renders out as expected.

### Groups

- appearance
- body

**Flags**: IRWA

---
## Attr: Window.minimizeHeight

### Description
Height for the window when minimized. If unset the window will shrink to the height of the header, if present, otherwise [this.defaultMinimizeHeight](#attr-windowdefaultminimizeheight)

### Groups

- appearance
- minimize

**Flags**: IRWA

---
## Attr: Window.headerSrc

### Description
If [Window.showHeaderBackground](#attr-windowshowheaderbackground) is `true`, this property provides the URL of the background image for the header.

### Groups

- appearance
- header

**Flags**: IRWA

---
## Attr: Window.header

### Description
Header for the Window, based on an HLayout. The header contains the title and some standard controls for the window, which may be configured via [Window.headerControls](#attr-windowheadercontrols).

The following [passthroughs](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) apply:

*   [headerStyle](#attr-windowheaderstyle) for [Canvas.styleName](Canvas.md#attr-canvasstylename)
*   [printHeaderStyle](#attr-windowprintheaderstyle) for the `styleName` to use when printing.

**Flags**: R

---
## Attr: Window.headerStyle

### Description
Style for the Window header.

### Groups

- appearance
- header

**Flags**: IRWA

---
## Attr: Window.hiliteBodyColor

### Description
Highlight color for the Window body (shown when the body is flashed).

### Groups

- appearance
- body

### See Also

- [Window.flash](#method-windowflash)

**Flags**: IRW

---
## Attr: Window.footerControls

### Description
Array of members to show in the Window footer.

The default value of `footerControls` is an Array of Strings listing the standard footer controls in their default order:

```
    footerControls : ["spacer", "resizer"]
 
```
As with [Window.headerControls](#attr-windowheadercontrols), you can override `footerControls` to change the order of standard controls in the footer. `"spacer"` is a special value which will create a [LayoutSpacer](../reference.md#class-layoutspacer) in the footer bar. `"resizer"` will show the [Window.resizer](#attr-windowresizer) in the footer.

By embedding a Canvas directly in this list you can add arbitrary additional controls to the footer.

Note that the [Window.statusBar](#attr-windowstatusbar) is not part of the set of footer controls - it is a separate canvas rendered behind all footer controls. If you include some custom status bar directly in the footerControls you may want to set [Window.showFooter](#attr-windowshowfooter) to false.

Tip: custom controls need to set layoutAlign:"center" to appear vertically centered.

**Component XML:**

To define `footerControls` in Component XML a special set of components are used as markers. The standard footer controls can be explicitly specified as:

```
  <footerControls>
      <WindowFooterSpacer/>
      <WindowResizer/>
  </footerControls>
 
```

**Flags**: IR

---
## Attr: Window.animateMinimize

### Description
Should this window minimize, maximize, and restore as an animation, or as a simple 1-step transition?

### Groups

- appearance
- header
- animation

**Flags**: IRWA

---
## Attr: Window.footer

### Description
Optional footer for the window, providing space for controls such as the resizer and status bar.

**Flags**: R

---
## Attr: Window.footerHeight

### Description
The height of the footer, in pixels.

### Groups

- appearance
- footer

**Flags**: IR

---
## Attr: Window.minimized

### Description
Is this window minimized. If true at init time, the window will be drawn minimized. To set this property at runtime use [Window.minimize](#method-windowminimize) or [Window.restore](#method-windowrestore).

### Groups

- appearance
- header

**Flags**: IRW

---
## Attr: Window.minimizeAcceleration

### Description
Default acceleration function for performing an animated minimize / maximize. If unset, `this.animateAcceleration` will be used by default instead

### Groups

- appearance
- header
- animation

**Flags**: IRWA

---
## Attr: Window.bodyColor

### Description
Color of the Window body. Overrides the background color specified in the style.

### Groups

- appearance
- body

### See Also

- [Window.flash](#method-windowflash)

**Flags**: IRW

---
## Attr: Window.defaultMinimizeHeight

### Description
If [Window.minimizeHeight](#attr-windowminimizeheight) is unset, by the window will shrink to the height of the header when minimized.  
If there is no header, the `defaultMinimizeHeight` will be used instead.

### Groups

- appearance
- header

**Flags**: IRWA

---
## Attr: Window.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: Window.canDragResize

### Description
Can the window be drag-resized? If true the window may be drag resized from its edges, and if showing, via the resizer icon in the footer.

### Groups

- dragging
- resizing

### See Also

- [Window.showResizer](#attr-windowshowresizer)

**Flags**: IRW

---
## Attr: Window.showHeaderIcon

### Description
If true, we show an icon on the left in the header.

### Groups

- windowHeader
- appearance
- header

**Flags**: IRW

---
## Attr: Window.contentLayout

### Description
The layout policy that should be used for widgets within the Window body.

See [ContentLayoutPolicy](../reference.md#type-contentlayoutpolicy) and [Window.bodyConstructor](#attr-windowbodyconstructor) for details.

### Groups

- appearance

**Flags**: IRWA

---
## Attr: Window.showCloseButton

### Description
If true, show a close button in the header, which will dismiss this window by calling [Window.closeClick](#method-windowcloseclick).

### Groups

- windowHeader
- appearance
- header

**Flags**: IRW

---
## Attr: Window.resizeFrom

### Description
When drag resizing is enabled via [Window.canDragResize](#attr-windowcandragresize), restricts resizes to only certain edges or corners.

This property on [Window](#class-window) overrides the default defined by [Canvas.resizeFrom](Canvas.md#attr-canvasresizefrom).

### Groups

- dragdrop

**Flags**: IRWA

---
## Attr: Window.resizer

### Description
ImgButton-based resizer, shown in the footer.

**Flags**: R

---
## Attr: Window.useBackMask

### Description
By default Windows show a [backMask](Canvas.md#attr-canvasusebackmask) in Internet Explorer versions predating Internet Explorer 9. This is a workaround for a native browser issue whereby certain DOM elements such as `IFRAME`s (whether rendered within SmartClient components via features such as [contentsURL](HTMLFlow.md#attr-htmlflowcontentsurl) or explicitly written into the HTML of the page) will not be properly occluded by DOM elements which overlap them but have a higher z-index.

A side-effect of this is that the [opacity](Canvas.md#attr-canvasopacity) can not be modified for the entire window. Developers may disable the backmask in order to support opacity in IE versions less than 9 by setting this property to false, however you should be aware that in doing this there is a potential for the "burn through" problem described above.

**Flags**: IRA

---
## Attr: Window.modalMaskOpacity

### Description
Controls the opacity of the modal mask displayed behind modal windows.

### Groups

- modal
- appearance

### See Also

- [Window.modalMask](#attr-windowmodalmask)

**Flags**: IR

---
## Attr: Window.keepInParentRect

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

### See Also

- [Window.canDragReposition](#attr-windowcandragreposition)

**Flags**: IRWA

---
## Attr: Window.showModalMask

### Description
If true, displays a translucent mask over the rest of the page when a modal window is displayed.

### Groups

- modal
- appearance

### See Also

- [Window.modalMask](#attr-windowmodalmask)

**Flags**: IR

---
## Attr: Window.showMinimizeButton

### Description
If true, show a minimize button in the header--clicking it minimizes the Window.

### Groups

- windowHeader
- appearance
- header

**Flags**: IRW

---
## Attr: Window.dismissOnOutsideClick

### Description
If true, a click outside the bounds of the Window will have the same effect as pressing its cancel button.  
**Note:** Applies only to modal windows.

### Groups

- modal

### See Also

- [Window.isModal](#attr-windowismodal)

**Flags**: IRW

---
## Attr: Window.showFooter

### Description
If true, show a footer for this Window, including resizer, statusBar, etc. This setting is commonly overridden for skinning purposes.

### Groups

- windowMembers
- appearance
- footer

**Flags**: IRW

---
## Attr: Window.showEdges

### Description
`showEdges` dynamically defaults to false when the [Window.placement](#attr-windowplacement) setting indicates the Window will be filling a portion of the screen or a panel.

**Flags**: IR

---
## Attr: Window.showMaximizeButton

### Description
If true, show a maximize button in the header - clicking it maximizes the Window

### Groups

- windowHeader
- appearance
- header

**Flags**: IRW

---
## Attr: Window.opacity

### Description
Renders the widget to be partly transparent. A widget's opacity property may be set to any number between 0 (transparent) to 100 (opaque). Null means don't specify opacity directly, 100 is fully opaque. Note that heavy use of opacity may have a performance impact on some older browsers.

In older versions of Internet Explorer (Pre IE9 / HTML5), opacity is achieved through proprietary filters. If [filters have been disabled](Canvas.md#classattr-canvasneverusefilters) within this application developers must set [Canvas.useOpacityFilter](Canvas.md#attr-canvasuseopacityfilter) to true for specific components on which opacity support is required.

Also note that opacity is incompatible with [backMasks](Canvas.md#attr-canvasusebackmask), and that this property is enabled by default for Window instances.

**Flags**: IRWA

---
## Attr: Window.items

### Description
The contents of the Window body. Can be specified three different ways:

*   an Array of Canvases that will become the children of the Window's body when it is initialized; the canvases in this array should be created, but not drawn (autodraw: false).
*   a single canvas that will become a child of the Window body.
*   a string that will be set as the body's contents.

### Groups

- appearance
- body

### See Also

- [Window.body](#attr-windowbody)

**Flags**: IR

---
## Attr: Window.autoSize

### Description
If true, the window is resized automatically to accommodate the contents of the body, if they would otherwise require scrolling.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Window.canDragReposition

### Description
If true, this Window may be moved around by the user by dragging on the Window header. Note that if the header is not showing, the Window can't be drag-repositioned regardless of this setting.

### Groups

- dragging

### See Also

- [Window.showHeader](#attr-windowshowheader)

**Flags**: IRW

---
## Attr: Window.statusBar

### Description
Simple Canvas-based status bar, shown in the footer. [Window.setStatus](#method-windowsetstatus) can be used to show text here.

**Flags**: R

---
## Attr: Window.headerLabel

### Description
Label that shows Window title in header.

The following [passthrough](../kb_topics/autoChildUsage.md#kb-topic-using-autochildren) applies: [title](#attr-windowtitle) for [Label.contents](Label.md#attr-labelcontents).

**Flags**: R

---
## Attr: Window.minimizeTime

### Description
If this window is minimizeable, and animateMinimize is true, what should the duration of the minimize / maximize be (in ms)? If unset defaults to `canvas.animationTime`.

### Groups

- appearance
- header
- animation

**Flags**: IRWA

---
## Attr: Window.printHeaderStyle

### Description
CSS Style for header in printed output

**Flags**: IR

---
## Attr: Window.autoCenter

### Description
If true, this Window widget will automatically be centered on the page when shown. If false, it will show up in the last position it was placed (either programmatically, or by user interaction).

**Note:** If an auto-centering Window is either programmatically moved or dragged by an end user, auto-centering behavior is automatically turned off. To manually center a Window, you can use [Window.centerInPage](#method-windowcenterinpage).

### Groups

- appearance
- location

**Flags**: IRW

---
## Attr: Window.status

### Description
Text to show in the status bar of the window (if one is visible)

### Groups

- appearance

**Flags**: IRW

---
## Attr: Window.headerLabelDefaults

### Description
This is an object literal property block specifying various properties of the header label that displays the [Window.title](#attr-windowtitle). Overrideable defaults are as follows:

*   styleName- defaults to `"windowHeaderText"` and specifies the css style that is used to render the [Window.title](#attr-windowtitle) text.

You can override the the above properties by calling [Class.changeDefaults](Class.md#classmethod-classchangedefaults).

### Groups

- appearance
- headerLabel

**Flags**: IRWA

---
## Attr: Window.bodyStyle

### Description
Style of the Window body.

### Groups

- appearance
- body

**Flags**: IRW

---
## Attr: Window.contentsType

### Description
If this window has [Window.src](#attr-windowsrc) specified, this property can be used to indicate whether the source is a standalone HTML page or an HTML fragment.

This is similar to the [HTMLFlow.contentsType](HTMLFlow.md#attr-htmlflowcontentstype) property - be sure to read the HTMLFlow documentation to understand circumstances where contentsType:"page" is **unsafe and not recommended**.

### Groups

- appearance
- body

### See Also

- [Window.src](#attr-windowsrc)

**Flags**: IR

---
## Method: Window.setHeaderStyle

### Description
Setter for [headerStyle](#attr-windowheaderstyle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newHeaderStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new [styleName](Canvas.md#attr-canvasstylename) for the [header](#attr-windowheader). |

---
## Method: Window.restore

### Description
Restores the window to its specified height and width after a call to [Window.minimize](#method-windowminimize) or [Window.maximize](#method-windowmaximize). Called from a click on the restore button shown in place of the minimize or maximize button when the window is minimized or maximized.  
Resizing will occur as an animation if [Window.animateMinimize](#attr-windowanimateminimize) is true.

---
## Method: Window.setStatus

### Description
Sets the text in the status bar of the window, redrawing if necessary.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| statusString | [String](#type-string) | false | — | new text for the status bar |

### Groups

- appearance

---
## Method: Window.setBodyStyle

### Description
Setter for [bodyStyle](#attr-windowbodystyle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newBodyStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new [styleName](Canvas.md#attr-canvasstylename) for the [body](#attr-windowbody). |

---
## Method: Window.addMembers

### Description
Same as [Layout.addMembers](Layout.md#method-layoutaddmembers). Note that in order to add items to [Window.body](#attr-windowbody), you use [Window.addItem](#method-windowadditem) rather than `addMembers`. Adding a member to a Window adds the member as a sibling to the header, body and other built-in Window subcomponents.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newMembers | [Array of Canvas](#type-array-of-canvas)|[Canvas](#type-canvas) | false | — | array of canvases to be added or single Canvas |
| position | [Number](#type-number) | true | — | position to add newMembers; if omitted newMembers will be added at the last position |

**Flags**: A

---
## Method: Window.flash

### Description
Makes the window header flash if it's visible; if there's no header, or the header is hidden, makes the window body flash instead.

This method is executed when users click outside the bounds of a modal window so they'll notice that they have to do something with the window.

### Groups

- modal

**Flags**: A

---
## Method: Window.centerInPage

### Description
Centers the Window in the page. This is called automatically in window.show() if Window.autoCenter is true. Note - if the Window is a child of another widget, we center in the parent widget rather than centering in the page.

### Groups

- appearance

### See Also

- [Window.autoCenter](#attr-windowautocenter)

**Flags**: A

---
## Method: Window.setAutoSize

### Description
Setter for [Window.autoSize](#attr-windowautosize)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoSize | [boolean](../reference.md#type-boolean) | false | — | true if the window should auto-size to its content |

---
## Method: Window.removeItem

### Description
Removes a widget from the body area of the window.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Canvas](#type-canvas) | false | — | the widget to be removed |

### Returns

`[Array](#type-array)` — the array of widgets removed

### Groups

- windowItems

**Flags**: A

---
## Method: Window.maximize

### Description
Maximize the window. Fired when the user clicks the maximize button if [this.showMaximizeButton](#attr-windowshowmaximizebutton) is true.  
Default implementation moves the window to `0, 0` and resizes the window to `"100%"` on both axes, so it will fill the browser window (or the parent of the Window instance, if appropriate).  
If [animateMinimize](#attr-windowanimateminimize) is true, the maximize will be animated. A restore button will be displayed in place of the maximize button when the window is maximized.

---
## Method: Window.closeClick

### Description
Handles a click on the close button of this window. The default implementation calls [close()](#method-windowclose) and returns false to prevent bubbling of the click event.

Override this method if you want other actions to be taken. Custom implementations may call `close()` to trigger the default behavior.

### Returns

`[Boolean](#type-boolean)` — Return false to cancel bubbling the click event

### Groups

- buttons

---
## Method: Window.setShowHeaderIcon

### Description
Dynamically update [Window.showHeaderIcon](#attr-windowshowheadericon) to show / hide the headerIcon

### See Also

- [Window.headerControls](#attr-windowheadercontrols)
- [Window.showHeaderIcon](#attr-windowshowheadericon)

---
## Method: Window.minimize

### Description
Minimize the window. Fired when the user clicks the minimize button if [this.showMinimizeButton](#attr-windowshowminimizebutton) is true.  
Default implementation shrinks the window to just the height of the header bar, hiding the body. If [animateMinimize](#attr-windowanimateminimize) is true, the resize will be animated. A restore button will be displayed in place of the minimize button when the window is minimized.

---
## Method: Window.setShowTitle

### Description
Updates whether the [title](#attr-windowtitle) is shown in the [header](#attr-windowheader). No impact unless the header is being shown. The header will be redrawn if necessary.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newShowTitle | [Boolean](#type-boolean) | false | — | new showTitle |

### Groups

- windowHeader
- appearance
- headerLabel

---
## Method: Window.revealChild

### Description
Reveals the child Canvas passed in by showing it if it is currently hidden. Note, in the case of Window, "child Canvas" means widgets in the Window's "items" collection as well as real children (the children of a Window - ie, the elements of its "children" array - are its component parts like header and body)

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| child | [GlobalId](../reference.md#type-globalid)|[Canvas](#type-canvas) | false | — | the child Canvas to reveal, or its global ID |

---
## Method: Window.shouldDismissOnEscape

### Description
Should this window be dismissed (same effect as pressing the "Cancel" button) when the user presses the "Escape" key?  
Default behavior: if [Window.dismissOnEscape](#attr-windowdismissonescape) is set, just return it. Otherwise return true if this window is showing a "close" control in the header (see [Window.headerControls](#attr-windowheadercontrols)).

### Returns

`[Boolean](#type-boolean)` — true if the window should be dismissed when the user hits escape

---
## Method: Window.addMember

### Description
Same as [Layout.addMember](Layout.md#method-layoutaddmember). Note that in order to add items to [Window.body](#attr-windowbody), you use [Window.addItem](#method-windowadditem) rather than `addMember`. Adding a member to a Window adds the member as a sibling to the header, body and other built-in Window subcomponents.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newMember | [Canvas](#type-canvas) | false | — | the canvas object to be added to the layout |
| position | [Integer](../reference_2.md#type-integer) | true | — | the position in the layout to place newMember (starts with 0); if omitted, it will be added at the last position |

### See Also

- [Window.addMembers](#method-windowaddmembers)

**Flags**: A

---
## Method: Window.setHiliteBodyColor

### Description
Setter for [hiliteBodyColor](#attr-windowhilitebodycolor).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newHiliteBodyColor | [CSSColor](../reference_2.md#type-csscolor) | false | — | new `hiliteBodyColor`. |

---
## Method: Window.setSrc

### Description
Sets the URL of the contents to display in the body of the window, redrawing if necessary.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| url | [String](#type-string) | false | — | URL of new contents to be displayed in the window body |

### Groups

- appearance
- body

---
## Method: Window.addItems

### Description
Adds an array of widgets to the window.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| items | [Array of Canvas](#type-array-of-canvas) | false | — | an array of widgets to be added |

### Returns

`[Array](#type-array)` — array of widgets added

### Groups

- windowItems

---
## Method: Window.close

### Description
Close this window. This method is fired by the default [Window.closeClick](#method-windowcloseclick) implementation. Default implementation will hide the window.

---
## Method: Window.setShowCloseButton

### Description
Dynamically update [Window.showCloseButton](#attr-windowshowclosebutton) to show / hide the closeButton

### Groups

- windowHeader

### See Also

- [Window.headerControls](#attr-windowheadercontrols)
- [Window.showCloseButton](#attr-windowshowclosebutton)

---
## Method: Window.addItem

### Description
Adds a widget to the body area of the window.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| item | [Canvas](#type-canvas) | false | — | the widget to be added |

### Returns

`[Array](#type-array)` — array of widgets added

### Groups

- windowItems

**Flags**: A

---
## Method: Window.setBodyColor

### Description
Setter for [bodyColor](#attr-windowbodycolor).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newBodyColor | [CSSColor](../reference_2.md#type-csscolor) | false | — | new [backgroundColor](Canvas.md#attr-canvasbackgroundcolor) for the [body](#attr-windowbody). |

---
## Method: Window.setShowMaximizeButton

### Description
Dynamically update [Window.showMaximizeButton](#attr-windowshowmaximizebutton) to show / hide the maximizeButton

### See Also

- [Window.headerControls](#attr-windowheadercontrols)
- [Window.showMaximizeButton](#attr-windowshowmaximizebutton)

---
## Method: Window.removeItems

### Description
Removes an array of widgets from the window.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| items | [Array of Canvas](#type-array-of-canvas) | false | — | an array of widgets to be removed |

### Returns

`[Array](#type-array)` — the array of widgets removed

### Groups

- windowItems

---
## Method: Window.setShowMinimizeButton

### Description
Dynamically update [Window.showMinimizeButton](#attr-windowshowminimizebutton) to show / hide the minimizeButton

### See Also

- [Window.headerControls](#attr-windowheadercontrols)
- [Window.showMinimizeButton](#attr-windowshowminimizebutton)

---
## Method: Window.setTitle

### Description
Sets the [title](#attr-windowtitle) that appears in the window [header](#attr-windowheader). The header will be redrawn if necessary.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | new title. |

### Groups

- appearance
- headerLabel
- i18nMessages

---
