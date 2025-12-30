# StretchImgButton Documentation

[← Back to API Index](../reference.md)

---

## Class: StretchImgButton

*Inherits from:* [StretchImg](StretchImg.md#class-stretchimg)

### Description
A StretchImg that behaves like a button, going through up/down/over state transitions in response to user events. Supports an optional title, and will auto-size to accommodate the title text if `overflow` is set to "visible".

Examples of use include fancy buttons, poplist headers, and tabs.

---
## Attr: StretchImgButton.showRollOverIcon

### Description
If using an icon for this button, whether to switch the icon image on mouse rollover.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.icon

### Description
Optional icon to be shown with the button title text.

Specify as the partial URL to an image, relative to the imgDir of this component. A sprited image can be specified using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format.

Note that the string "blank" is a valid setting for this attribute and will always result in the system blank image, with no state suffixes applied. Typically, this might be used when an iconStyle is also specified and the iconStyle renders the icon via a stateful background-image or other CSS approach.

### Groups

- buttonIcon

**Flags**: IRW

---
## Attr: StretchImgButton.iconAlign

### Description
If this button is showing an icon should it be right or left aligned?

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.showFocus

### Description
Should we visibly change state when the canvas receives focus? Note that by default the `over` state is used to indicate focus.

### Groups

- state

**Deprecated**

**Flags**: IRW

---
## Attr: StretchImgButton.height

### Description
Size for this component's vertical dimension. See [Canvas.height](Canvas.md#attr-canvasheight) for more details.

Note that if [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit) is set on non-[StretchImgButton](#class-stretchimgbutton) instances, this property will be ignored so that the widget is always sized just large enough to accommodate the title.

### Groups

- sizing

### See Also

- [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit)

**Flags**: IRW

---
## Attr: StretchImgButton.autoFit

### Description
If true, ignore the specified size of this widget and always size just large enough to accommodate the title. If `setWidth()` is explicitly called on an autoFit:true button, autoFit will be reset to `false`.

Note that for StretchImgButton instances, autoFit will occur horizontally only, as unpredictable vertical sizing is likely to distort the media. If you do want vertical auto-fit, this can be achieved by simply setting a small height, and having overflow:"visible"

### Groups

- sizing

**Flags**: IRW

---
## Attr: StretchImgButton.labelHPad

### Description
The padding for a StretchImgButton's label is determined as follows.

If `labelHPad` is set it will specify the horizontal padding applied to the label. Similarly if `labelVPad` is set it will specify the vertical padding for the label, regardless of the button's [vertical](#attr-stretchimgbuttonvertical) setting.

Otherwise `labelLengthPad` can be set to specify the label padding along the length axis (ie: horizontal padding if [StretchImgButton.vertical](#attr-stretchimgbuttonvertical) is false, otherwise vertical padding), and `labelBreadthPad` can be set to specify the label padding along the other axis.

Otherwise the padding on the length axis will match the [StretchImgButton.capSize](#attr-stretchimgbuttoncapsize) and will be set to zero on the breadth axis.

So by default the label will be sized to match the center image of the StretchImgButton, but these settings allow the label to partially or wholly overlap the caps.

**Flags**: IRW

---
## Attr: StretchImgButton.showSelectedIcon

### Description
If using an icon for this button, whether to switch the icon image when the button becomes selected.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.iconWidth

### Description
Width in pixels of the icon image.

If unset, defaults to [iconSize](StatefulCanvas.md#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.align

### Description
Horizontal alignment of this component's title.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StretchImgButton.iconOrientation

### Description
If this button is showing an icon should it appear to the left or right of the title? valid options are `"left"` and `"right"`.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.showDisabledIcon

### Description
If using an icon for this button, whether to switch the icon image if the button becomes disabled.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.actionType

### Description
Behavior on state changes -- BUTTON, RADIO or CHECKBOX

### Groups

- state
- event handling

**Flags**: IRW

---
## Attr: StretchImgButton.showClippedTitleOnHover

### Description
If true and the title is clipped, then a hover containing the full title of this button is enabled.

### Groups

- hovers

**Flags**: IRW

---
## Attr: StretchImgButton.wrap

### Description
Should the title for this button wrap? If unset, default behavior is to allow wrapping if this.vertical is true, otherwise disallow wrapping

**Flags**: IRW

---
## Attr: StretchImgButton.radioGroup

### Description
String identifier for this canvas's mutually exclusive selection group.

### Groups

- state
- event handling

**Flags**: IRWA

---
## Attr: StretchImgButton.showTitle

### Description
Determines whether any specified [title](StatefulCanvas.md#method-statefulcanvasgettitle) will be displayed for this component.  
Applies to Image-based components only, where the title will be rendered out in a label floating over the component

**Flags**: IRW

---
## Attr: StretchImgButton.title

### Description
The title HTML to display in this button.

### Groups

- basics

**Flags**: IRW

---
## Attr: StretchImgButton.showFocusedIcon

### Description
If using an icon for this button, whether to switch the icon image when the button receives focus.

If [StatefulCanvas.showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is true, the `"Over"` icon will be displayed when the canvas has focus, otherwise a separate `"Focused"` icon will be displayed

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.labelLengthPad

### Description
The padding for a StretchImgButton's label is determined as follows.

If `labelHPad` is set it will specify the horizontal padding applied to the label. Similarly if `labelVPad` is set it will specify the vertical padding for the label, regardless of the button's [vertical](#attr-stretchimgbuttonvertical) setting.

Otherwise `labelLengthPad` can be set to specify the label padding along the length axis (ie: horizontal padding if [StretchImgButton.vertical](#attr-stretchimgbuttonvertical) is false, otherwise vertical padding), and `labelBreadthPad` can be set to specify the label padding along the other axis.

Otherwise the padding on the length axis will match the [StretchImgButton.capSize](#attr-stretchimgbuttoncapsize) and will be set to zero on the breadth axis.

So by default the label will be sized to match the center image of the StretchImgButton, but these settings allow the label to partially or wholly overlap the caps.

**Flags**: IRW

---
## Attr: StretchImgButton.titleStyle

### Description
CSS style applied to the title text only. Defaults to [StretchImgButton.baseStyle](#attr-stretchimgbuttonbasestyle) when unset.

With a separate `titleStyle` and [StretchImgButton.baseStyle](#attr-stretchimgbuttonbasestyle) set, you can provide a backgroundColor via `baseStyle` that will allow translucent .png media to be "tinted" by the underlying background color, so that a single set of media can provide range of color options. In this usage, the `titleStyle` should generally not specify a background color as this would block out the media that appears behind the title.

**Flags**: IRW

---
## Attr: StretchImgButton.src

### Description
Base URL for the image. By default, StretchImgButtons consist of three image parts: A start image (displayed at the top or left), a scalable central image and an end image displayed at the bottom or right.

The images displayed in the stretchImgButton are derived from this property in the following way:

*   When the button is in its standard state the suffixes "\_start", "\_end" and "\_stretch" are applied to the src (before the file extension), so by default the images displayed will be "button\_start.gif" (sized to be `this.capSize` by the specified width of the stretchImgButton), "button\_stretch.gif" (stretched to the necessary width) and "button\_end.gif" (sized the same as the start image).
*   As the button's state changes, the images will have suffixes appended **before** the "\_start" / "\_end" / "\_stretch" to represent the button state. See [Img.src](Img.md#attr-imgsrc) for an overview of how states are combined into a compound URL.

For example the center piece of a selected stretchImgButton with the mouse hovering over it might have the URL: `"button_Selected_Down_stretch.gif"`.

Media should be present for each possible state of the \_start, \_end and \_stretch images.

**Flags**: IRW

---
## Attr: StretchImgButton.showDownIcon

### Description
If using an icon for this button, whether to switch the icon image when the mouse goes down on the button.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.iconHeight

### Description
Height in pixels of the icon image.

If unset, defaults to [iconSize](StatefulCanvas.md#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.state

### Description
Current "state" of this widget. The state setting is automatically updated as the user interacts with the component (see [StatefulCanvas.showRollOver](StatefulCanvas.md#attr-statefulcanvasshowrollover), [StatefulCanvas.showDown](StatefulCanvas.md#attr-statefulcanvasshowdown), [StatefulCanvas.showDisabled](StatefulCanvas.md#attr-statefulcanvasshowdisabled)).

StatefulCanvases will have a different appearance based on their current state. By default this is handled by changing the css className applied to the StatefulCanvas - see [StatefulCanvas.baseStyle](StatefulCanvas.md#attr-statefulcanvasbasestyle) and [StatefulCanvas.getStateSuffix](StatefulCanvas.md#method-statefulcanvasgetstatesuffix) for a description of how this is done.

For [Img](Img.md#class-img) or [StretchImg](StretchImg.md#class-stretchimg) based subclasses of StatefulCanvas, the appearance may also be updated by changing the src of the rendered image. See [Img.src](Img.md#attr-imgsrc) and [StretchImgButton.src](#attr-stretchimgbuttonsrc) for a description of how the URL is modified to reflect the state of the widget in this case.

### Groups

- state

### See Also

- [State](../reference.md#type-state)
- [state](../kb_topics/state.md#kb-topic-state)

**Flags**: IRWA

---
## Attr: StretchImgButton.vertical

### Description
Default is a horizontal button. Vertical StretchImgButtons are allowed, but title text, if any, will not be automatically rotated.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StretchImgButton.showRollOver

### Description
Should we visibly change state when the mouse goes over this object?

### Groups

- state

**Flags**: IRW

---
## Attr: StretchImgButton.iconSpacing

### Description
Pixels between icon and title text.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.capSize

### Description
How big are the end pieces by default

### Groups

- appearance

**Flags**: IRW

---
## Attr: StretchImgButton.iconSize

### Description
Size in pixels of the icon image.

The [iconWidth](StatefulCanvas.md#attr-statefulcanvasiconwidth) and [iconHeight](StatefulCanvas.md#attr-statefulcanvasiconheight) properties can be used to configure width and height separately.

Note: When configuring the properties of a `StatefulCanvas` (or derivative) [AutoChild](../reference.md#type-autochild), it is best to set the `iconWidth` and `iconHeight` to the same value rather than setting an `iconSize`. This is because certain skins or customizations thereto might set the `iconWidth` and `iconHeight`, making the customization of the AutoChild's `iconSize` ineffective.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: StretchImgButton.showDisabled

### Description
Should we visibly change state when disabled?

### Groups

- state

**Flags**: IRW

---
## Attr: StretchImgButton.width

### Description
Size for this component's horizontal dimension. See [Canvas.width](Canvas.md#attr-canvaswidth) for more details.

Note that if [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit) is set, this property will be ignored so that the widget is always sized just large enough to accommodate the title.

### Groups

- sizing

### See Also

- [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit)

**Flags**: IRW

---
## Attr: StretchImgButton.labelBreadthPad

### Description
The padding for a StretchImgButton's label is determined as follows.

If `labelHPad` is set it will specify the horizontal padding applied to the label. Similarly if `labelVPad` is set it will specify the vertical padding for the label, regardless of the button's [vertical](#attr-stretchimgbuttonvertical) setting.

Otherwise `labelLengthPad` can be set to specify the label padding along the length axis (ie: horizontal padding if [StretchImgButton.vertical](#attr-stretchimgbuttonvertical) is false, otherwise vertical padding), and `labelBreadthPad` can be set to specify the label padding along the other axis.

Otherwise the padding on the length axis will match the [StretchImgButton.capSize](#attr-stretchimgbuttoncapsize) and will be set to zero on the breadth axis.

So by default the label will be sized to match the center image of the StretchImgButton, but these settings allow the label to partially or wholly overlap the caps.

**Flags**: IRW

---
## Attr: StretchImgButton.labelVPad

### Description
The padding for a StretchImgButton's label is determined as follows.

If `labelHPad` is set it will specify the horizontal padding applied to the label. Similarly if `labelVPad` is set it will specify the vertical padding for the label, regardless of the button's [vertical](#attr-stretchimgbuttonvertical) setting.

Otherwise `labelLengthPad` can be set to specify the label padding along the length axis (ie: horizontal padding if [StretchImgButton.vertical](#attr-stretchimgbuttonvertical) is false, otherwise vertical padding), and `labelBreadthPad` can be set to specify the label padding along the other axis.

Otherwise the padding on the length axis will match the [StretchImgButton.capSize](#attr-stretchimgbuttoncapsize) and will be set to zero on the breadth axis.

So by default the label will be sized to match the center image of the StretchImgButton, but these settings allow the label to partially or wholly overlap the caps.

**Flags**: IRW

---
## Attr: StretchImgButton.hiliteAccessKey

### Description
If set to true, if the [title](StatefulCanvas.md#attr-statefulcanvastitle) of this button contains the specified [accessKey](Canvas.md#attr-canvasaccesskey), when the title is displayed to the user it will be modified to include HTML to underline the accessKey.  
Note that this property may cause titles that include HTML (rather than simple strings) to be inappropriately modified, so should be disabled if your title string includes HTML characters.

**Flags**: IRW

---
## Attr: StretchImgButton.showDown

### Description
Should we visibly change state when the mouse goes down in this object?

### Groups

- state

**Flags**: IRW

---
## Attr: StretchImgButton.valign

### Description
Vertical alignment of this component's title.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StretchImgButton.baseStyle

### Description
Base CSS style className applied to the component.

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
then applying that style to the button with [overflow](Canvas.md#attr-canvasoverflow): "clip\_h" would yield a vertically-rendered title with overflow via ellipsis as expected, and also wrap with [Button.wrap](Button.md#attr-buttonwrap). Note that:

*   The explicit width applied via CSS is needed because rotated elements don't inherit dimensions in their new orientation from the DOM - the transform/rotation occurs independently of layout.
*   The translation transform required along the x-axis is roughly (width - height) / 2, but may need slight offsetting for optimal centering.
*   We've explicitly avoided describing an approach based on CSS "writing-mode", since support is incomplete and bugs are present in popular browsers such as Firefox and Safari that would prevent it from being used without Framework assistance.

**Flags**: IRW

---
## Attr: StretchImgButton.labelSkinImgDir

### Description
Specifies a skinImgDir to apply to the label containing the title of this StretchImgButton. May be null in which case `this.skinImgDir` will be applied to the label as well.

Note that icons displayed in the title may make use of the skin img dir set here

**Flags**: IRWA

---
## Attr: StretchImgButton.selected

### Description
Whether this component is selected. For some components, selection affects appearance.

### Groups

- state

**Flags**: IRW

---
## Attr: StretchImgButton.showFocused

### Description
Should we visibly change state when the canvas receives focus? If [StatefulCanvas.showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is `true`, then **`"over"`** will be used to indicate focus. Otherwise a separate **`"focused"`** state will be used.

### Groups

- state

**Flags**: IRW

---
## Method: StretchImgButton.addToRadioGroup

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
## Method: StretchImgButton.setBaseStyle

### Description
Sets the base CSS style. As the component changes state and/or is selected, suffixes will be added to the base style.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| style | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new base style |

---
## Method: StretchImgButton.getState

### Description
Return the state of this StatefulCanvas

### Returns

`[State](../reference.md#type-state)` — —

### Groups

- state

---
## Method: StretchImgButton.titleHover

### Description
Optional stringMethod to fire when the user hovers over this button and the title is clipped. If [StretchImgButton.showClippedTitleOnHover](#attr-stretchimgbuttonshowclippedtitleonhover) is true, the default behavior is to show a hover canvas containing the HTML returned by [StretchImgButton.titleHoverHTML](#method-stretchimgbuttontitlehoverhtml). Return false to suppress this default behavior.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard hover

### Groups

- hovers

### See Also

- [StretchImgButton.titleClipped](#method-stretchimgbuttontitleclipped)

---
## Method: StretchImgButton.removeFromRadioGroup

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
## Method: StretchImgButton.getActionType

### Description
Return the 'actionType' for this canvas (radio / checkbox / button)

### Groups

- state
- event handling

---
## Method: StretchImgButton.action

### Description
This property contains the default 'action' for the Button to fire when activated.

---
## Method: StretchImgButton.iconClick

### Description
If this button is showing an [icon](#attr-stretchimgbuttonicon), a separate click handler for the icon may be defined as `this.iconClick`. Returning false will suppress the standard button click handling code.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard button click event

### Groups

- buttonIcon

---
## Method: StretchImgButton.setIconOrientation

### Description
Changes the orientation of the icon relative to the text of the button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| orientation | [String](#type-string) | false | — | The new orientation of the icon relative to the text of the button. |

### Groups

- buttonIcon

---
## Method: StretchImgButton.setTitleStyle

### Description
Sets the [StretchImgButton.titleStyle](#attr-stretchimgbuttontitlestyle), which is applied to the title text.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| style | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new title style |

---
## Method: StretchImgButton.setIcon

### Description
Change the icon being shown next to the title text.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [SCImgURL](../reference_2.md#type-scimgurl) | false | — | URL of new icon |

### Groups

- buttonIcon

---
## Method: StretchImgButton.titleHoverHTML

### Description
Returns the HTML that is displayed by the default [titleHover](#method-stretchimgbuttontitlehover) handler. Return null or an empty string to cancel the hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| defaultHTML | [HTMLString](../reference.md#type-htmlstring) | false | — | the HTML that would have been displayed by default |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover. If null or an empty string, then the hover is canceled.

---
## Method: StretchImgButton.isSelected

### Description
Find out if this object is selected

### Returns

`[Boolean](#type-boolean)` — —

### Groups

- state

---
## Method: StretchImgButton.deselect

### Description
Select this object.

### Groups

- state

---
## Method: StretchImgButton.select

### Description
Select this object.

### Groups

- state

---
## Method: StretchImgButton.setTitle

### Description
Setter for the [title](StatefulCanvas.md#attr-statefulcanvastitle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTitle | [HTMLString](../reference.md#type-htmlstring) | false | — | the new title HTML. |

### Groups

- appearance

---
## Method: StretchImgButton.setState

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
## Method: StretchImgButton.setLabelSkinImgDir

### Description
setter for [StretchImgButton.labelSkinImgDir](#attr-stretchimgbuttonlabelskinimgdir).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| URL | [URL](../reference.md#type-url) | false | — | new skin img dir to apply to the label holding title text for this widget. |

---
## Method: StretchImgButton.setAutoFit

### Description
Setter method for the [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit) property. Pass in true or false to turn autoFit on or off. When autoFit is set to `false`, canvas will be resized to it's previously specified size.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| autoFit | [boolean](../reference.md#type-boolean) | false | — | New autoFit setting. |

---
## Method: StretchImgButton.getTitle

### Description
Return the title - HTML drawn inside the component.

Default is to simply return this.title.

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML for the title.

**Flags**: A

---
## Method: StretchImgButton.setDisabled

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
## Method: StretchImgButton.titleClipped

### Description
Is the title of this button clipped?

### Returns

`[boolean](../reference.md#type-boolean)` — whether the title is clipped.

**Flags**: A

---
## Method: StretchImgButton.setActionType

### Description
Update the 'actionType' for this canvas (radio / checkbox / button) If the canvas is currently selected, and the passed in actionType is 'button' this method will deselect the canvas.

### Groups

- state
- event handling

---
## Method: StretchImgButton.setSelected

### Description
Select this object.

### Groups

- state

---
