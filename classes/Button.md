# Button Documentation

[← Back to API Index](../reference.md)

---

## Class: Button

*Inherits from:* [StatefulCanvas](StatefulCanvas.md#class-statefulcanvas)

### Description
The Button widget class implements interactive, style-based button widgets.

---
## Attr: Button.selected

### Description
Whether this component is selected. For some components, selection affects appearance.

### Groups

- state

**Flags**: IRW

---
## Attr: Button.iconAlign

### Description
If this button is showing an icon should it be right or left aligned?

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.canAdaptWidth

### Description
This flag enables [adaptive width](Canvas.md#attr-canvascanadaptwidth) for the button.

If enabled the button will support rendering in a 'collapsed' view if there isn't enough space in a layout to render it at normal size. There are a couple of ways this can be achieved.

*   If [Button.adaptWidthShowIconOnly](#attr-buttonadaptwidthshowicononly) is true and this button shows an icon, the title will be hidden if there isn't enough space to render it, allowing it to shrink to either the rendered icon width, or any specified [minWidth](Canvas.md#attr-canvasminwidth), whichever is larger.
*   Otherwise, if the button has a specified [minWidth](Canvas.md#attr-canvasminwidth), and [Button.autoFit](#attr-buttonautofit) is true, autoFit will be temporarily disabled, if there isn't enough room, allowing the title to be clipped

In either case the title will show on hover unless an explicit hover has been specified such as by overriding [Button.titleHoverHTML](#method-buttontitlehoverhtml).

### See Also

- [Canvas.canAdaptWidth](Canvas.md#attr-canvascanadaptwidth)

**Flags**: IR

---
## Attr: Button.iconStyle

### Description
Base CSS style applied to the icon image. If set, as the `StatefulCanvas` changes [state](StatefulCanvas.md#attr-statefulcanvasstate) and/or is [selected](StatefulCanvas.md#attr-statefulcanvasselected), suffixes will be appended to `iconStyle` to form the className set on the image element.

The following table lists out the standard set of suffixes which may be appended:

| CSS Class Applied | Description |
|---|---|
| iconStyle | Default CSS style |
| iconStyle+Selected | Applied when [StatefulCanvas.selected](StatefulCanvas.md#attr-statefulcanvasselected) and [StatefulCanvas.showSelectedIcon](StatefulCanvas.md#attr-statefulcanvasshowselectedicon) are true. |
| iconStyle+Focused | Applied when the component has keyboard focus, if [StatefulCanvas.showFocusedIcon](StatefulCanvas.md#attr-statefulcanvasshowfocusedicon) is true, and [StatefulCanvas.showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is not true. |
| iconStyle+Over | Applied when [StatefulCanvas.showRollOverIcon](StatefulCanvas.md#attr-statefulcanvasshowrollovericon) is set to true and either the user rolls over the component or [StatefulCanvas.showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is true and the component has keyboard focus. |
| iconStyle+Down | Applied when the user presses the mouse button on the component if [StatefulCanvas.showDownIcon](StatefulCanvas.md#attr-statefulcanvasshowdownicon) is set to true |
| iconStyle+Disabled | Applied when the component is [disabled](Canvas.md#attr-canvasdisabled) if [StatefulCanvas.showDisabledIcon](StatefulCanvas.md#attr-statefulcanvasshowdisabledicon) is true. |
| Combined styles |
| iconStyle+SelectedFocused | Combined Selected and focused styling |
| iconStyle+SelectedOver | Combined Selected and rollOver styling |
| iconStyle+FocusedOver | Combined Focused and rollOver styling |
| iconStyle+SelectedFocusedOver | Combined Selected, Focused and rollOver styling |
| iconStyle+SelectedDown | Combined Selected and mouse-down styling |
| iconStyle+FocusedDown | Combined Focused and mouse-down styling |
| iconStyle+SelectedFocusedDown | Combined Selected, Focused and mouse-down styling |
| iconStyle+SelectedDisabled | Combined Selected and Disabled styling |

In addition, if [StatefulCanvas.showRTLIcon](StatefulCanvas.md#attr-statefulcanvasshowrtlicon) is true, then in RTL mode, a final "RTL" suffix will be appended.

### Groups

- buttonIcon

**Flags**: IRW

---
## Attr: Button.showDisabled

### Description
Should we visibly change state when disabled?

### Groups

- state

**Flags**: IRW

---
## Attr: Button.iconSpacing

### Description
Pixels between icon and title text.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.showRollOver

### Description
Should we visibly change state when the mouse goes over this object?

### Groups

- state

**Flags**: IRW

---
## Attr: Button.showFocused

### Description
Should we visibly change state when the canvas receives focus? If [StatefulCanvas.showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is `true`, then **`"over"`** will be used to indicate focus. Otherwise a separate **`"focused"`** state will be used.

### Groups

- state

**Flags**: IRW

---
## Attr: Button.styleName

### Description
StatefulCanvases are styled by combining [Button.baseStyle](#attr-buttonbasestyle) with [State](../reference.md#type-state) to build a composite css style name. In most cases, `statefulCanvas.styleName` will have no effect on statefulCanvas styling and should not be used.

If the `baseStyle` is not explicitly specified for a class, the `styleName` will be used as a default baseStyle. Other than that, this attribute will be ignored.

**Flags**: IRW

---
## Attr: Button.width

### Description
Size for this component's horizontal dimension. See [Canvas.width](Canvas.md#attr-canvaswidth) for more details.

Note that if [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit) is set, this property will be ignored so that the widget is always sized just large enough to accommodate the title.

### Groups

- sizing

### See Also

- [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit)

**Flags**: IRW

---
## Attr: Button.iconSize

### Description
Size in pixels of the icon image.

The [iconWidth](StatefulCanvas.md#attr-statefulcanvasiconwidth) and [iconHeight](StatefulCanvas.md#attr-statefulcanvasiconheight) properties can be used to configure width and height separately.

Note: When configuring the properties of a `StatefulCanvas` (or derivative) [AutoChild](../reference.md#type-autochild), it is best to set the `iconWidth` and `iconHeight` to the same value rather than setting an `iconSize`. This is because certain skins or customizations thereto might set the `iconWidth` and `iconHeight`, making the customization of the AutoChild's `iconSize` ineffective.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.iconHeight

### Description
Height in pixels of the icon image.

If unset, defaults to [iconSize](StatefulCanvas.md#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.wrap

### Description
A boolean indicating whether the button's title should word-wrap, if necessary.

### Groups

- basics

**Flags**: IRW

---
## Attr: Button.align

### Description
Horizontal alignment of this component's title.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Button.overflow

### Description
Clip the contents of the button if necessary.

### See Also

- [Canvas.overflow](Canvas.md#attr-canvasoverflow)

**Flags**: IRWA

---
## Attr: Button.iconOnlyBaseStyle

### Description
if defined, `iconOnlyBaseStyle` is used as the base CSS style className, instead of [Button.baseStyle](#attr-buttonbasestyle), if [Button.canAdaptWidth](#attr-buttoncanadaptwidth) is set and the [title is not being shown](#attr-buttonadaptwidthshowicononly).

### See Also

- [Canvas.canAdaptWidth](Canvas.md#attr-canvascanadaptwidth)
- [TabSet.simpleTabIconOnlyBaseStyle](TabSet.md#attr-tabsetsimpletabicononlybasestyle)

**Flags**: IRW

---
## Attr: Button.autoFit

### Description
If true, ignore the specified size of this widget and always size just large enough to accommodate the title. If `setWidth()` is explicitly called on an autoFit:true button, autoFit will be reset to `false`.

Note that for StretchImgButton instances, autoFit will occur horizontally only, as unpredictable vertical sizing is likely to distort the media. If you do want vertical auto-fit, this can be achieved by simply setting a small height, and having overflow:"visible"

### Groups

- sizing

**Flags**: IRW

---
## Attr: Button.showDisabledIcon

### Description
If using an icon for this button, whether to switch the icon image if the button becomes disabled.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.baseStyle

### Description
Base CSS style className applied to the component.

Note that if specified, this property takes precedence over any specified [StatefulCanvas.styleName](StatefulCanvas.md#attr-statefulcanvasstylename). If unset, the `styleName` will be used as a default `baseStyle` value.

As the component changes [StatefulCanvas.state](StatefulCanvas.md#attr-statefulcanvasstate) and/or is selected, suffixes will be added to the base style. In some cases more than one suffix will be appended to reflect a combined state ("Selected" + "Disabled", for example).

See [StatefulCanvas.getStateSuffix](StatefulCanvas.md#method-statefulcanvasgetstatesuffix) for a description of the default set of suffixes which may be applied to the baseStyle

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
then applying that style to the button with [overflow](Canvas.md#attr-canvasoverflow): "clip\_h" would yield a vertically-rendered title with overflow via ellipsis as expected, and also wrap with [Button.wrap](#attr-buttonwrap). Note that:

*   The explicit width applied via CSS is needed because rotated elements don't inherit dimensions in their new orientation from the DOM - the transform/rotation occurs independently of layout.
*   The translation transform required along the x-axis is roughly (width - height) / 2, but may need slight offsetting for optimal centering.
*   We've explicitly avoided describing an approach based on CSS "writing-mode", since support is incomplete and bugs are present in popular browsers such as Firefox and Safari that would prevent it from being used without Framework assistance.

Note on css-margins: Developers should be aware that the css "margin" property is unreliable for certain subclasses of StatefulCanvas, including [buttons](#class-button). Developers may use the explicit [Canvas.margin](Canvas.md#attr-canvasmargin) property to specify button margins, or for a button within a layout, consider the layout properties [Layout.layoutMargin](Layout.md#attr-layoutlayoutmargin), [Layout.membersMargin](Layout.md#attr-layoutmembersmargin)

### See Also

- [Button.iconOnlyBaseStyle](#attr-buttonicononlybasestyle)

**Flags**: IRW

---
## Attr: Button.showDown

### Description
Should we visibly change state when the mouse goes down in this object?

### Groups

- state

**Flags**: IRW

---
## Attr: Button.showRollOverIcon

### Description
If using an icon for this button, whether to switch the icon image on mouse rollover.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.actionType

### Description
Behavior on state changes -- BUTTON, RADIO or CHECKBOX

### Groups

- state
- event handling

**Flags**: IRW

---
## Attr: Button.icon

### Description
Optional icon to be shown with the button title text.

Specify as the partial URL to an image, relative to the imgDir of this component. A sprited image can be specified using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format.

Note that the string "blank" is a valid setting for this attribute and will always result in the system blank image, with no state suffixes applied. Typically, this might be used when an iconStyle is also specified and the iconStyle renders the icon via a stateful background-image or other CSS approach.

### Groups

- buttonIcon

**Flags**: IRW

---
## Attr: Button.valign

### Description
Vertical alignment of this component's title.

### Groups

- appearance

**Flags**: IRW

---
## Attr: Button.showDownIcon

### Description
If using an icon for this button, whether to switch the icon image when the mouse goes down on the button.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.state

### Description
Current "state" of this widget. The state setting is automatically updated as the user interacts with the component (see [StatefulCanvas.showRollOver](StatefulCanvas.md#attr-statefulcanvasshowrollover), [StatefulCanvas.showDown](StatefulCanvas.md#attr-statefulcanvasshowdown), [StatefulCanvas.showDisabled](StatefulCanvas.md#attr-statefulcanvasshowdisabled)).

StatefulCanvases will have a different appearance based on their current state. By default this is handled by changing the css className applied to the StatefulCanvas - see [StatefulCanvas.baseStyle](StatefulCanvas.md#attr-statefulcanvasbasestyle) and [StatefulCanvas.getStateSuffix](StatefulCanvas.md#method-statefulcanvasgetstatesuffix) for a description of how this is done.

For [Img](Img.md#class-img) or [StretchImg](StretchImg.md#class-stretchimg) based subclasses of StatefulCanvas, the appearance may also be updated by changing the src of the rendered image. See [Img.src](Img.md#attr-imgsrc) and [StretchImgButton.src](StretchImgButton.md#attr-stretchimgbuttonsrc) for a description of how the URL is modified to reflect the state of the widget in this case.

### Groups

- state

### See Also

- [State](../reference.md#type-state)
- [state](../kb_topics/state.md#kb-topic-state)

**Flags**: IRWA

---
## Attr: Button.iconOrientation

### Description
If this button is showing an icon should it appear to the left or right of the title? valid options are `"left"` and `"right"`.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.iconCursor

### Description
Specifies the cursor to display when the mouse pointer is over the icon image.

### Groups

- cues

### See Also

- [Button.disabledIconCursor](#attr-buttondisablediconcursor)

**Flags**: IR

---
## Attr: Button.disabledIconCursor

### Description
Specifies the cursor to display when the mouse pointer is over the icon image and this `StatefulCanvas` is [disabled](Canvas.md#attr-canvasdisabled).

If not set and the mouse pointer is over the icon image, [iconCursor](#attr-buttoniconcursor) will be used.

### Groups

- cues

**Flags**: IR

---
## Attr: Button.showSelectedIcon

### Description
If using an icon for this button, whether to switch the icon image when the button becomes selected.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.title

### Description
The title HTML to display in this button.

### Groups

- basics
- i18nMessages

**Flags**: IRW

---
## Attr: Button.iconWidth

### Description
Width in pixels of the icon image.

If unset, defaults to [iconSize](StatefulCanvas.md#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.adaptWidthShowIconOnly

### Description
If [Button.canAdaptWidth](#attr-buttoncanadaptwidth) is true, and this button has a specified [Button.icon](#attr-buttonicon), should the title be hidden, allowing the button to shrink down to just show the icon when there isn't enough horizontal space in a layout to show the default sized button?

### See Also

- [Button.canAdaptWidth](#attr-buttoncanadaptwidth)
- [Button.iconOnlyBaseStyle](#attr-buttonicononlybasestyle)

**Flags**: IRW

---
## Attr: Button.radioGroup

### Description
String identifier for this canvas's mutually exclusive selection group.

### Groups

- state
- event handling

**Flags**: IRWA

---
## Attr: Button.hiliteAccessKey

### Description
If set to true, if the [title](StatefulCanvas.md#attr-statefulcanvastitle) of this button contains the specified [accessKey](Canvas.md#attr-canvasaccesskey), when the title is displayed to the user it will be modified to include HTML to underline the accessKey.  
Note that this property may cause titles that include HTML (rather than simple strings) to be inappropriately modified, so should be disabled if your title string includes HTML characters.

**Flags**: IRW

---
## Attr: Button.height

### Description
Size for this component's vertical dimension. See [Canvas.height](Canvas.md#attr-canvasheight) for more details.

Note that if [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit) is set on non-[StretchImgButton](StretchImgButton.md#class-stretchimgbutton) instances, this property will be ignored so that the widget is always sized just large enough to accommodate the title.

### Groups

- sizing

### See Also

- [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit)

**Flags**: IRW

---
## Attr: Button.showFocusedIcon

### Description
If using an icon for this button, whether to switch the icon image when the button receives focus.

If [StatefulCanvas.showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is true, the `"Over"` icon will be displayed when the canvas has focus, otherwise a separate `"Focused"` icon will be displayed

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Button.showClippedTitleOnHover

### Description
If true and the title is clipped, then a hover containing the full title of this button is enabled.

### Groups

- hovers

**Flags**: IRW

---
## Method: Button.setIconOrientation

### Description
Changes the orientation of the icon relative to the text of the button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| orientation | [String](#type-string) | false | — | The new orientation of the icon relative to the text of the button. |

### Groups

- buttonIcon

---
## Method: Button.isSelected

### Description
Find out if this object is selected

### Returns

`[Boolean](#type-boolean)` — —

### Groups

- state

---
## Method: Button.select

### Description
Select this object.

### Groups

- state

---
## Method: Button.removeFromRadioGroup

### Description
Remove this widget from the specified mutually exclusive selection group with the ID passed in. No-op's if this widget is not a member of the groupID passed in. If no groupID is passed in, defaults to removing from whatever radioGroup this widget is a member of.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupID | [String](#type-string) | true | — | \- optional radio group ID (to ensure the widget is removed from the appropriate group. |

### Groups

- state
- event handling

---
## Method: Button.getTitle

### Description
Return the title - HTML drawn inside the component.

Default is to simply return this.title.

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML for the title.

**Flags**: A

---
## Method: Button.titleClipped

### Description
Is the title of this button clipped?

### Returns

`[boolean](../reference.md#type-boolean)` — whether the title is clipped.

**Flags**: A

---
## Method: Button.action

### Description
This property contains the default 'action' for the Button to fire when activated.

---
## Method: Button.deselect

### Description
Select this object.

### Groups

- state

---
## Method: Button.setVAlign

### Description
Sets the vertical alignment of this buttons content.

### Groups

- positioning

---
## Method: Button.titleHoverHTML

### Description
Returns the HTML that is displayed by the default [titleHover](#method-buttontitlehover) handler. Return null or an empty string to cancel the hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| defaultHTML | [HTMLString](../reference.md#type-htmlstring) | false | — | the HTML that would have been displayed by default |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover. If null or an empty string, then the hover is canceled.

---
## Method: Button.setState

### Description
Sets the [state](StatefulCanvas.md#attr-statefulcanvasstate) of this object, changing its appearance. Note: `newState` cannot be "Disabled" if [this.showDisabled](StatefulCanvas.md#attr-statefulcanvasshowdisabled) is `false`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newState | [State](../reference.md#type-state) | false | — | the new state. |

### Groups

- state
- appearance

---
## Method: Button.getState

### Description
Return the state of this StatefulCanvas

### Returns

`[State](../reference.md#type-state)` — —

### Groups

- state

---
## Method: Button.titleHover

### Description
Optional stringMethod to fire when the user hovers over this button and the title is clipped. If [Button.showClippedTitleOnHover](#attr-buttonshowclippedtitleonhover) is true, the default behavior is to show a hover canvas containing the HTML returned by [Button.titleHoverHTML](#method-buttontitlehoverhtml). Return false to suppress this default behavior.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard hover

### Groups

- hovers

### See Also

- [Button.titleClipped](#method-buttontitleclipped)

---
## Method: Button.setSelected

### Description
Select this object.

### Groups

- state

---
## Method: Button.setBaseStyle

### Description
Sets the base CSS style. As the component changes state and/or is selected, suffixes will be added to the base style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| style | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new base style |

---
## Method: Button.setActionType

### Description
Update the 'actionType' for this canvas (radio / checkbox / button) If the canvas is currently selected, and the passed in actionType is 'button' this method will deselect the canvas.

### Groups

- state
- event handling

---
## Method: Button.setWrap

### Description
Set whether the title of this button should be allowed to wrap if too long for the button's specified width.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newWrap | [boolean](../reference.md#type-boolean) | false | — | whether to wrap the title |

---
## Method: Button.getActionType

### Description
Return the 'actionType' for this canvas (radio / checkbox / button)

### Groups

- state
- event handling

---
## Method: Button.setDisabled

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
## Method: Button.setAlign

### Description
Sets the (horizontal) alignment of this buttons content.

### Groups

- positioning

---
## Method: Button.iconClick

### Description
If this button is showing an [icon](#attr-buttonicon), a separate click handler for the icon may be defined as `this.iconClick`. Returning false will suppress the standard button click handling code.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard button click event

### Groups

- buttonIcon

---
## Method: Button.addToRadioGroup

### Description
Add this widget to the specified mutually exclusive selection group with the ID passed in. Selecting this widget will then deselect any other StatefulCanvases with the same radioGroup ID. StatefulCanvases can belong to only one radioGroup, so this method will remove from any other radiogroup of which this button is already a member.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| groupID | [String](#type-string) | false | — | \- ID of the radiogroup to which this widget should be added |

### Groups

- state
- event handling

---
## Method: Button.setIcon

### Description
Change the icon being shown next to the title text.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [SCImgURL](../reference.md#type-scimgurl) | false | — | URL of new icon |

### Groups

- buttonIcon

---
## Method: Button.setAutoFit

### Description
Setter method for the [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit) property. Pass in true or false to turn autoFit on or off. When autoFit is set to `false`, canvas will be resized to it's previously specified size.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoFit | [boolean](../reference.md#type-boolean) | false | — | New autoFit setting. |

---
## Method: Button.setTitle

### Description
Setter for the [title](StatefulCanvas.md#attr-statefulcanvastitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | the new title HTML. |

### Groups

- appearance

---
