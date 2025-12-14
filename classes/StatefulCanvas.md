# StatefulCanvas Documentation

[← Back to API Index](../reference.md)

---

## Class: StatefulCanvas

*Inherits from:* [Canvas](Canvas.md#class-canvas)

### Description
A component that has a set of possible states, and which presents itself differently according to which state it is in. An example is a button, which can be "up", "down", "over" or "disabled".

---
## ClassAttr: StatefulCanvas.SELECTED

### Description
A declared value of the enum type [Selected](../reference.md#type-selected).

**Flags**: R

---
## ClassAttr: StatefulCanvas.STATE_DOWN

### Description
A declared value of the enum type [State](../reference.md#type-state).

**Flags**: R

---
## ClassAttr: StatefulCanvas.CHECKBOX

### Description
A declared value of the enum type [SelectionType](../reference.md#type-selectiontype).

**Flags**: R

---
## ClassAttr: StatefulCanvas.FOCUSED

### Description
A declared value of the enum type [Selected](../reference.md#type-selected).

**Flags**: R

---
## ClassAttr: StatefulCanvas.UNSELECTED

### Description
A declared value of the enum type [Selected](../reference.md#type-selected).

**Flags**: R

---
## ClassAttr: StatefulCanvas.STATE_OVER

### Description
A declared value of the enum type [State](../reference.md#type-state).

**Flags**: R

---
## ClassAttr: StatefulCanvas.STATE_DISABLED

### Description
A declared value of the enum type [State](../reference.md#type-state).

**Flags**: R

---
## ClassAttr: StatefulCanvas.BUTTON

### Description
A declared value of the enum type [SelectionType](../reference.md#type-selectiontype).

**Flags**: R

---
## ClassAttr: StatefulCanvas.STATE_UP

### Description
A declared value of the enum type [State](../reference.md#type-state).

**Flags**: R

---
## ClassAttr: StatefulCanvas.RADIO

### Description
A declared value of the enum type [SelectionType](../reference.md#type-selectiontype).

**Flags**: R

---
## Attr: StatefulCanvas.iconHeight

### Description
Height in pixels of the icon image.

If unset, defaults to [iconSize](#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.state

### Description
Current "state" of this widget. The state setting is automatically updated as the user interacts with the component (see [StatefulCanvas.showRollOver](#attr-statefulcanvasshowrollover), [StatefulCanvas.showDown](#attr-statefulcanvasshowdown), [StatefulCanvas.showDisabled](#attr-statefulcanvasshowdisabled)).

StatefulCanvases will have a different appearance based on their current state. By default this is handled by changing the css className applied to the StatefulCanvas - see [StatefulCanvas.baseStyle](#attr-statefulcanvasbasestyle) and [StatefulCanvas.getStateSuffix](#method-statefulcanvasgetstatesuffix) for a description of how this is done.

For [Img](Img.md#class-img) or [StretchImg](StretchImg.md#class-stretchimg) based subclasses of StatefulCanvas, the appearance may also be updated by changing the src of the rendered image. See [Img.src](Img.md#attr-imgsrc) and [StretchImgButton.src](StretchImgButton.md#attr-stretchimgbuttonsrc) for a description of how the URL is modified to reflect the state of the widget in this case.

### Groups

- state

### See Also

- [State](../reference.md#type-state)
- [state](../kb_topics/state.md#kb-topic-state)

**Flags**: IRWA

---
## Attr: StatefulCanvas.showMenuOnClick

### Description
If true, this widget will fire [showContextMenu()](Canvas.md#method-canvasshowcontextmenu) to show the [context menu](Canvas.md#attr-canvascontextmenu) if one is defined, rather than [click()](Canvas.md#method-canvasclick), when the left mouse is clicked.

Note that this property has a different interpretation in [IconButton](../reference.md#class-iconbutton) as [IconButton.showMenuOnClick](RibbonButton.md#attr-ribbonbuttonshowmenuonclick).

### Groups

- menu

**Flags**: IRW

---
## Attr: StatefulCanvas.showDisabledIcon

### Description
If using an icon for this button, whether to switch the icon image if the button becomes disabled.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.radioGroup

### Description
String identifier for this canvas's mutually exclusive selection group.

### Groups

- state
- event handling

**Flags**: IRWA

---
## Attr: StatefulCanvas.iconStyle

### Description
Base CSS style applied to the icon image. If set, as the `StatefulCanvas` changes [state](#attr-statefulcanvasstate) and/or is [selected](#attr-statefulcanvasselected), suffixes will be appended to `iconStyle` to form the className set on the image element.

The following table lists out the standard set of suffixes which may be appended:

| CSS Class Applied | Description |
|---|---|
| iconStyle | Default CSS style |
| iconStyle+Selected | Applied when [StatefulCanvas.selected](#attr-statefulcanvasselected) and [StatefulCanvas.showSelectedIcon](#attr-statefulcanvasshowselectedicon) are true. |
| iconStyle+Focused | Applied when the component has keyboard focus, if [StatefulCanvas.showFocusedIcon](#attr-statefulcanvasshowfocusedicon) is true, and [StatefulCanvas.showFocusedAsOver](#attr-statefulcanvasshowfocusedasover) is not true. |
| iconStyle+Over | Applied when [StatefulCanvas.showRollOverIcon](#attr-statefulcanvasshowrollovericon) is set to true and either the user rolls over the component or [StatefulCanvas.showFocusedAsOver](#attr-statefulcanvasshowfocusedasover) is true and the component has keyboard focus. |
| iconStyle+Down | Applied when the user presses the mouse button on the component if [StatefulCanvas.showDownIcon](#attr-statefulcanvasshowdownicon) is set to true |
| iconStyle+Disabled | Applied when the component is [disabled](Canvas.md#attr-canvasdisabled) if [StatefulCanvas.showDisabledIcon](#attr-statefulcanvasshowdisabledicon) is true. |
| Combined styles |
| iconStyle+SelectedFocused | Combined Selected and focused styling |
| iconStyle+SelectedOver | Combined Selected and rollOver styling |
| iconStyle+FocusedOver | Combined Focused and rollOver styling |
| iconStyle+SelectedFocusedOver | Combined Selected, Focused and rollOver styling |
| iconStyle+SelectedDown | Combined Selected and mouse-down styling |
| iconStyle+FocusedDown | Combined Focused and mouse-down styling |
| iconStyle+SelectedFocusedDown | Combined Selected, Focused and mouse-down styling |
| iconStyle+SelectedDisabled | Combined Selected and Disabled styling |

In addition, if [StatefulCanvas.showRTLIcon](#attr-statefulcanvasshowrtlicon) is true, then in RTL mode, a final "RTL" suffix will be appended.

### Groups

- buttonIcon

**Flags**: IRW

---
## Attr: StatefulCanvas.showFocusedAsOver

### Description
If [showFocused](#attr-statefulcanvasshowfocused) is true for this widget, should the `"over"` state be used to indicate the widget as focused. If set to false, a separate `"focused"` state will be used.

### Groups

- state

**Flags**: IRW

---
## Attr: StatefulCanvas.showRollOver

### Description
Should we visibly change state when the mouse goes over this object?

### Groups

- state

**Flags**: IRW

---
## Attr: StatefulCanvas.align

### Description
Horizontal alignment of this component's title.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StatefulCanvas.overCanvas

### Description
Auto generated child widget to be shown when the user rolls over this canvas if [StatefulCanvas.showOverCanvas](#attr-statefulcanvasshowovercanvas) is true. See documentation for [AutoChild](../reference.md#type-autochild) for information on how to customize this canvas.

**Flags**: R

---
## Attr: StatefulCanvas.showDisabled

### Description
Should we visibly change state when disabled?

### Groups

- state

**Flags**: IRW

---
## Attr: StatefulCanvas.redrawOnStateChange

### Description
Whether this widget needs to redraw to reflect state change

### Groups

- state

**Flags**: IRWA

---
## Attr: StatefulCanvas.showFocusedIcon

### Description
If using an icon for this button, whether to switch the icon image when the button receives focus.

If [StatefulCanvas.showFocusedAsOver](#attr-statefulcanvasshowfocusedasover) is true, the `"Over"` icon will be displayed when the canvas has focus, otherwise a separate `"Focused"` icon will be displayed

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.showFocus

### Description
Should we visibly change state when the canvas receives focus? Note that by default the `over` state is used to indicate focus.

### Groups

- state

**Deprecated**

**Flags**: IRW

---
## Attr: StatefulCanvas.showFocused

### Description
Should we visibly change state when the canvas receives focus? If [StatefulCanvas.showFocusedAsOver](#attr-statefulcanvasshowfocusedasover) is `true`, then **`"over"`** will be used to indicate focus. Otherwise a separate **`"focused"`** state will be used.

### Groups

- state

**Flags**: IRW

---
## Attr: StatefulCanvas.iconSize

### Description
Size in pixels of the icon image.

The [iconWidth](#attr-statefulcanvasiconwidth) and [iconHeight](#attr-statefulcanvasiconheight) properties can be used to configure width and height separately.

Note: When configuring the properties of a `StatefulCanvas` (or derivative) [AutoChild](../reference.md#type-autochild), it is best to set the `iconWidth` and `iconHeight` to the same value rather than setting an `iconSize`. This is because certain skins or customizations thereto might set the `iconWidth` and `iconHeight`, making the customization of the AutoChild's `iconSize` ineffective.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.showSelectedIcon

### Description
If using an icon for this button, whether to switch the icon image when the button becomes selected.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.icon

### Description
Optional icon to be shown with the button title text.

Specify as the partial URL to an image, relative to the imgDir of this component. A sprited image can be specified using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format.

Note that the string "blank" is a valid setting for this attribute and will always result in the system blank image, with no state suffixes applied. Typically, this might be used when an iconStyle is also specified and the iconStyle renders the icon via a stateful background-image or other CSS approach.

### Groups

- buttonIcon

**Flags**: IRW

---
## Attr: StatefulCanvas.overCanvasConstructor

### Description
Constructor class name for this widget's [overCanvas](#attr-statefulcanvasovercanvas)

**Flags**: IRWA

---
## Attr: StatefulCanvas.iconWidth

### Description
Width in pixels of the icon image.

If unset, defaults to [iconSize](#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.showRTLIcon

### Description
Is [RTL](Page.md#classmethod-pageisrtl) media available for the icon? If true, then in RTL mode, the image's src will have "\_rtl" inserted immediately before the file extension. For example, if [icon](#attr-statefulcanvasicon) is "myIcon.png" and showRTLIcon is true, then in RTL mode, the image's src will be set to "myIcon\_rtl.png".

### Groups

- RTL

**Flags**: IR

---
## Attr: StatefulCanvas.showRollOverIcon

### Description
If using an icon for this button, whether to switch the icon image on mouse rollover.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.actionType

### Description
Behavior on state changes -- BUTTON, RADIO or CHECKBOX

### Groups

- state
- event handling

**Flags**: IRW

---
## Attr: StatefulCanvas.height

### Description
Size for this component's vertical dimension. See [Canvas.height](Canvas.md#attr-canvasheight) for more details.

Note that if [StatefulCanvas.autoFit](#attr-statefulcanvasautofit) is set on non-[StretchImgButton](StretchImgButton.md#class-stretchimgbutton) instances, this property will be ignored so that the widget is always sized just large enough to accommodate the title.

### Groups

- sizing

### See Also

- [StatefulCanvas.autoFit](#attr-statefulcanvasautofit)

**Flags**: IRW

---
## Attr: StatefulCanvas.selected

### Description
Whether this component is selected. For some components, selection affects appearance.

### Groups

- state

**Flags**: IRW

---
## Attr: StatefulCanvas.autoFit

### Description
If true, ignore the specified size of this widget and always size just large enough to accommodate the title. If `setWidth()` is explicitly called on an autoFit:true button, autoFit will be reset to `false`.

Note that for StretchImgButton instances, autoFit will occur horizontally only, as unpredictable vertical sizing is likely to distort the media. If you do want vertical auto-fit, this can be achieved by simply setting a small height, and having overflow:"visible"

### Groups

- sizing

**Flags**: IRW

---
## Attr: StatefulCanvas.ariaLabel

### Description
If specified this property returns the [aria-label](#method-statefulcanvasgetarialabel) attribute to write out in [screenReaderMode](isc.md#staticmethod-iscsetscreenreadermode).

If unset, aria-label will default to [this.prompt](Canvas.md#attr-canvasprompt) if specified, otherwise [this.title](#attr-statefulcanvastitle).

**Flags**: IRWA

---
## Attr: StatefulCanvas.showOverCanvas

### Description
When this property is set to true, this widget will create and show the [StatefulCanvas.overCanvas](#attr-statefulcanvasovercanvas) on user rollover.

**Flags**: IRWA

---
## Attr: StatefulCanvas.title

### Description
The title HTML to display in this button.

### Groups

- basics

**Flags**: IRW

---
## Attr: StatefulCanvas.valign

### Description
Vertical alignment of this component's title.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StatefulCanvas.width

### Description
Size for this component's horizontal dimension. See [Canvas.width](Canvas.md#attr-canvaswidth) for more details.

Note that if [StatefulCanvas.autoFit](#attr-statefulcanvasautofit) is set, this property will be ignored so that the widget is always sized just large enough to accommodate the title.

### Groups

- sizing

### See Also

- [StatefulCanvas.autoFit](#attr-statefulcanvasautofit)

**Flags**: IRW

---
## Attr: StatefulCanvas.styleName

### Description
StatefulCanvases are styled by combining [StatefulCanvas.baseStyle](#attr-statefulcanvasbasestyle) with [State](../reference.md#type-state) to build a composite css style name. In most cases, `statefulCanvas.styleName` will have no effect on statefulCanvas styling and should not be used.

If the `baseStyle` is not explicitly specified for a class, the `styleName` will be used as a default baseStyle. Other than that, this attribute will be ignored.

**Flags**: IRW

---
## Attr: StatefulCanvas.showDown

### Description
Should we visibly change state when the mouse goes down in this object?

### Groups

- state

**Flags**: IRW

---
## Attr: StatefulCanvas.iconOrientation

### Description
If this button is showing an icon should it appear to the left or right of the title? valid options are `"left"` and `"right"`.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.showDownIcon

### Description
If using an icon for this button, whether to switch the icon image when the mouse goes down on the button.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.baseStyle

### Description
Base CSS style className applied to the component.

Note that if specified, this property takes precedence over any specified [StatefulCanvas.styleName](#attr-statefulcanvasstylename). If unset, the `styleName` will be used as a default `baseStyle` value.

As the component changes [StatefulCanvas.state](#attr-statefulcanvasstate) and/or is selected, suffixes will be added to the base style. In some cases more than one suffix will be appended to reflect a combined state ("Selected" + "Disabled", for example).

See [StatefulCanvas.getStateSuffix](#method-statefulcanvasgetstatesuffix) for a description of the default set of suffixes which may be applied to the baseStyle

#### Rotated Titles

The Framework doesn't have built-in support for rotating button titles in a fashion similar to [FacetChart.rotateLabels](FacetChart.md#attr-facetchartrotatelabels). However, you can manually configure a button to render with a rotated title by applying custom CSS via this property.

For example, given a button with a height of 120 and a width of 48, if you copied the existing buttonXXX style declarations from skin\_styles.css as new, rotatedTitleButtonXXX declarations, and then added the lines:

```
     -ms-transform:     translate(-38px,0px) rotate(270deg);
     -webkit-transform: translate(-38px,0px) rotate(270deg);
     transform:         translate(-38px,0px) rotate(270deg);
     overflow: hidden;
     text-overflow: ellipsis;
     width:116px;
```
in the declaration section beginning:
```
 .rotatedTitleButton,
 .rotatedTitleButtonSelected,
 .rotatedTitleButtonSelectedOver,
 .rotatedTitleButtonSelectedDown,
 .rotatedTitleButtonSelectedDisabled,
 .rotatedTitleButtonOver,
 .rotatedTitleButtonDown,
 .rotatedTitleButtonDisabled {
```
then applying that style to the button with [overflow](Canvas.md#attr-canvasoverflow): "clip\_h" would yield a vertically-rendered title with overflow via ellipsis as expected, and also wrap with [Button.wrap](Button.md#attr-buttonwrap). Note that:

*   The explicit width applied via CSS is needed because rotated elements don't inherit dimensions in their new orientation from the DOM - the transform/rotation occurs independently of layout.
*   The translation transform required along the x-axis is roughly (width - height) / 2, but may need slight offsetting for optimal centering.
*   We've explicitly avoided describing an approach based on CSS "writing-mode", since support is incomplete and bugs are present in popular browsers such as Firefox and Safari that would prevent it from being used without Framework assistance.

Note on css-margins: Developers should be aware that the css "margin" property is unreliable for certain subclasses of StatefulCanvas, including [buttons](Button.md#class-button). Developers may use the explicit [Canvas.margin](Canvas.md#attr-canvasmargin) property to specify button margins, or for a button within a layout, consider the layout properties [Layout.layoutMargin](Layout.md#attr-layoutlayoutmargin), [Layout.membersMargin](Layout.md#attr-layoutmembersmargin)

**Flags**: IRW

---
## Attr: StatefulCanvas.iconSpacing

### Description
Pixels between icon and title text.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StatefulCanvas.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: StatefulCanvas.overCanvasDefaults

### Description
Default properties for this widgets [overCanvas](#attr-statefulcanvasovercanvas). To modify these defaults, use [Class.changeDefaults](Class.md#classmethod-classchangedefaults)

**Flags**: IRWA

---
## Attr: StatefulCanvas.ignoreRTL

### Description
Should horizontal alignment-related attributes [align](#attr-statefulcanvasalign) and [iconOrientation](#attr-statefulcanvasiconorientation) be mirrored in RTL mode? This is the default behavior unless ignoreRTL is set to true.

### Groups

- RTL

**Flags**: IRWA

---
## Method: StatefulCanvas.getStateSuffix

### Description
Returns the suffix that will be appended to the [StatefulCanvas.baseStyle](#attr-statefulcanvasbasestyle) as the component changes [StatefulCanvas.state](#attr-statefulcanvasstate) and/or is selected / focused.

Note that suffixes will only be included if the relevant `show_[StateName]_` attributes (EG [StatefulCanvas.showRollOver](#attr-statefulcanvasshowrollover), [StatefulCanvas.showFocused](#attr-statefulcanvasshowfocused), etc) are set to true.

The following table lists out the standard set of suffixes which may be applied to the base style:

| CSS Class Applied | Description |
|---|---|
| baseStyle | Default css style |
| baseStyle+Selected | Applied when [StatefulCanvas.selected](#attr-statefulcanvasselected) is set to true. |
| baseStyle+Focused | Applied when the component has keyboard focus, if [StatefulCanvas.showFocused](#attr-statefulcanvasshowfocused) is true, and [StatefulCanvas.showFocusedAsOver](#attr-statefulcanvasshowfocusedasover) is not true. |
| baseStyle+Over | Applied when [StatefulCanvas.showRollOver](#attr-statefulcanvasshowrollover) is set to true and either the user rolls over the component or [StatefulCanvas.showFocusedAsOver](#attr-statefulcanvasshowfocusedasover) is true and the component has keyboard focus. |
| baseStyle+Down | Applied when the user presses the mouse button on the component if [StatefulCanvas.showDown](#attr-statefulcanvasshowdown) is set to true |
| baseStyle+Disabled | Applied when the component is [disabled](Canvas.md#attr-canvasdisabled) if [StatefulCanvas.showDisabled](#attr-statefulcanvasshowdisabled) is true. |
| Combined styles |
| baseStyle+SelectedFocused | Combined Selected and focused styling |
| baseStyle+SelectedOver | Combined Selected and rollOver styling |
| baseStyle+FocusedOver | Combined Focused and rollOver styling |
| baseStyle+SelectedFocusedOver | Combined Selected, Focused and rollOver styling |
| baseStyle+SelectedDown | Combined Selected and mouse-down styling |
| baseStyle+FocusedDown | Combined Focused and mouse-down styling |
| baseStyle+SelectedFocusedDown | Combined Selected, Focused and mouse-down styling |
| baseStyle+SelectedDisabled | Combined Selected and Disabled styling |

### Returns

`[String](#type-string)` — suffix to be appended to the baseStyle

---
## Method: StatefulCanvas.setBaseStyle

### Description
Sets the base CSS style. As the component changes state and/or is selected, suffixes will be added to the base style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| style | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new base style |

---
## Method: StatefulCanvas.setIgnoreRTL

### Description
Setter for [ignoreRTL](#attr-statefulcanvasignorertl).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| ignoreRTL | [boolean](../reference.md#type-boolean) | false | — | new value for ignoreRTL. |

**Flags**: A

---
## Method: StatefulCanvas.getAriaStateDefaults

### Description
Retrieves dynamically calculated default [ARIA state mapping](Canvas.md#attr-canvasariastate) properties for this canvas. These will be combined with explicitly specified aria state as described in [Canvas.getAriaState](Canvas.md#method-canvasgetariastate).

Overridden by StatefulCanvas to pick up [aria-label](#method-statefulcanvasgetarialabel).

### Returns

`[Object](../reference.md#type-object)` — dynamically calculated default aria state properties

**Flags**: A

---
## Method: StatefulCanvas.getActionType

### Description
Return the 'actionType' for this canvas (radio / checkbox / button)

### Groups

- state
- event handling

**Flags**: A

---
## Method: StatefulCanvas.setTitle

### Description
Setter for the [title](#attr-statefulcanvastitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | the new title HTML. |

### Groups

- appearance

---
## Method: StatefulCanvas.removeFromRadioGroup

### Description
Remove this widget from the specified mutually exclusive selection group with the ID passed in. No-op's if this widget is not a member of the groupID passed in. If no groupID is passed in, defaults to removing from whatever radioGroup this widget is a member of.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupID | [String](#type-string) | true | — | \- optional radio group ID (to ensure the widget is removed from the appropriate group. |

### Groups

- state
- event handling

**Flags**: A

---
## Method: StatefulCanvas.select

### Description
Select this object.

### Groups

- state

---
## Method: StatefulCanvas.isSelected

### Description
Find out if this object is selected

### Returns

`[Boolean](#type-boolean)` — —

### Groups

- state

---
## Method: StatefulCanvas.setAutoFit

### Description
Setter method for the [StatefulCanvas.autoFit](#attr-statefulcanvasautofit) property. Pass in true or false to turn autoFit on or off. When autoFit is set to `false`, canvas will be resized to it's previously specified size.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoFit | [boolean](../reference.md#type-boolean) | false | — | New autoFit setting. |

---
## Method: StatefulCanvas.getTitle

### Description
Return the title - HTML drawn inside the component.

Default is to simply return this.title.

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML for the title.

**Flags**: A

---
## Method: StatefulCanvas.getAriaLabel

### Description
Method to return the `aria-label` for this component (see [StatefulCanvas.getAriaStateDefaults](#method-statefulcanvasgetariastatedefaults)).

Returns [StatefulCanvas.ariaLabel](#attr-statefulcanvasarialabel) if specified, otherwise [prompt](Canvas.md#attr-canvasprompt), otherwise [StatefulCanvas.title](#attr-statefulcanvastitle)

### Returns

`[String](#type-string)` — aria label value

---
## Method: StatefulCanvas.setIcon

### Description
Change the icon being shown next to the title text.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [SCImgURL](../reference.md#type-scimgurl) | false | — | URL of new icon |

### Groups

- buttonIcon

---
## Method: StatefulCanvas.getState

### Description
Return the state of this StatefulCanvas

### Returns

`[State](../reference.md#type-state)` — —

### Groups

- state

**Flags**: A

---
## Method: StatefulCanvas.deselect

### Description
Deselect this object.

### Groups

- state

---
## Method: StatefulCanvas.setDisabled

### Description
Enable or disable this object

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| disabled | [boolean](../reference.md#type-boolean) | false | — | true if this widget is to be disabled |

### Groups

- enable
- state

---
## Method: StatefulCanvas.setSelected

### Description
Set this object to be selected or deselected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newIsSelected | [boolean](../reference.md#type-boolean) | false | — | new boolean value of whether or not the object is selected. |

### Groups

- state

---
## Method: StatefulCanvas.setActionType

### Description
Update the 'actionType' for this canvas (radio / checkbox / button) If the canvas is currently selected, and the passed in actionType is 'button' this method will deselect the canvas.

### Groups

- state
- event handling

**Flags**: A

---
## Method: StatefulCanvas.setIconOrientation

### Description
Changes the orientation of the icon relative to the text of the button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| orientation | [String](#type-string) | false | — | The new orientation of the icon relative to the text of the button. |

### Groups

- buttonIcon

---
## Method: StatefulCanvas.setState

### Description
Sets the [state](#attr-statefulcanvasstate) of this object, changing its appearance. Note: `newState` cannot be "Disabled" if [this.showDisabled](#attr-statefulcanvasshowdisabled) is `false`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newState | [State](../reference.md#type-state) | false | — | the new state. |

### Groups

- state
- appearance

**Flags**: A

---
## Method: StatefulCanvas.setIconStyle

### Description
Setter for [StatefulCanvas.iconStyle](#attr-statefulcanvasiconstyle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| iconStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | the new `iconStyle` (may be `null` to remove the className on the image). |

---
## Method: StatefulCanvas.addToRadioGroup

### Description
Add this widget to the specified mutually exclusive selection group with the ID passed in. Selecting this widget will then deselect any other StatefulCanvases with the same radioGroup ID. StatefulCanvases can belong to only one radioGroup, so this method will remove from any other radiogroup of which this button is already a member.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupID | [String](#type-string) | false | — | \- ID of the radiogroup to which this widget should be added |

### Groups

- state
- event handling

**Flags**: A

---
