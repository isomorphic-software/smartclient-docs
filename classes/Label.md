# Label Documentation

[← Back to API Index](../reference.md)

---

## Class: Label

*Inherits from:* [Button](Button.md#class-button)

### Description
Labels display a small amount of [alignable](#attr-labelalign) [text](#attr-labelcontents) with optional [icon](#attr-labelicon) and [autoFit](#attr-labelautofit).

For a general-purpose container for HTML content, use [HTMLFlow](HTMLFlow.md#class-htmlflow) or [HTMLPane](../reference.md#class-htmlpane) instead.

---
## Attr: Label.valign

### Description
Vertical alignment of label text. See VerticalAlignment type for details.

### Groups

- positioning

**Flags**: IRW

---
## Attr: Label.iconWidth

### Description
Width in pixels of the icon image.

If unset, defaults to [iconSize](StatefulCanvas.md#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.iconSize

### Description
Size in pixels of the icon image.

The [iconWidth](StatefulCanvas.md#attr-statefulcanvasiconwidth) and [iconHeight](StatefulCanvas.md#attr-statefulcanvasiconheight) properties can be used to configure width and height separately.

Note: When configuring the properties of a `StatefulCanvas` (or derivative) [AutoChild](../reference.md#type-autochild), it is best to set the `iconWidth` and `iconHeight` to the same value rather than setting an `iconSize`. This is because certain skins or customizations thereto might set the `iconWidth` and `iconHeight`, making the customization of the AutoChild's `iconSize` ineffective.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.iconSpacing

### Description
Pixels between icon and title text.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.contents

### Description
The contents of a canvas or label widget. Any HTML string is acceptable.

### Groups

- contents

### See Also

- [Label.dynamicContents](#attr-labeldynamiccontents)

**Flags**: IRW

---
## Attr: Label.dynamicContents

### Description
Dynamic contents allows the contents string to be treated as a simple but powerful template. When this attribute is set to true, JavaScript expressions may be embedded within the contents string, using the format: `${_[JavaScript to evaluate]_}`.

For example, to include the current date in a templated message, `canvas.contents` could be set to:  
`"Today's date is `<b>`${new Date().toUSShortDate()}`</b>`"`

Embedded expressions will be evaluated when the canvas is drawn or redrawn, and the result of the evaluated expression will be displayed to the user. If the expression does not evaluate to a String, the `toString()` representation of the returned object will be displayed automatically

Dynamic expressions are evaluated in the scope of the canvas displaying the content, so the `this` keyword may be used within your expression to refer to the canvas. Developers may also explicitly supply values for variables to be used within the evaluation via the [Canvas.dynamicContentsVars](Canvas.md#attr-canvasdynamiccontentsvars) property.

Notes:

*   Calling markForRedraw() on the canvas will evaluate any embedded expressions.
*   Multiple such expressions may be embedded within the contents string for a component.
*   If an error occurs during evaluation, a warning is logged to the [Developer Console](../kb_topics/debugging.md#kb-topic-debugging) and the error string will be embedded in place of the expected value in the Canvas.

### Groups

- contents

### See Also

- [Label.contents](#attr-labelcontents)
- [Canvas.dynamicContentsVars](Canvas.md#attr-canvasdynamiccontentsvars)

**Flags**: IRWA

---
## Attr: Label.wrap

### Description
If false, the label text will not be wrapped to the next line.

### Groups

- sizing

**Flags**: IRW

---
## Attr: Label.align

### Description
Horizontal alignment of label text. See Alignment type for details.

### Groups

- positioning

**Flags**: IRW

---
## Attr: Label.showRollOverIcon

### Description
If using an icon for this button, whether to switch the icon image on mouse rollover.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.iconOrientation

### Description
If this button is showing an icon should it appear to the left or right of the title? valid options are `"left"` and `"right"`.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.iconHeight

### Description
Height in pixels of the icon image.

If unset, defaults to [iconSize](StatefulCanvas.md#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.autoFit

### Description
If true, ignore the specified size of this widget and always size just large enough to accommodate the title. If `setWidth()` is explicitly called on an autoFit:true button, autoFit will be reset to `false`.

Note that for StretchImgButton instances, autoFit will occur horizontally only, as unpredictable vertical sizing is likely to distort the media. If you do want vertical auto-fit, this can be achieved by simply setting a small height, and having overflow:"visible"

### Groups

- sizing

**Flags**: IRW

---
## Attr: Label.height

### Description
Size for this component's vertical dimension. See [Canvas.height](Canvas.md#attr-canvasheight) for more details.

Note that if [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit) is set on non-[StretchImgButton](StretchImgButton.md#class-stretchimgbutton) instances, this property will be ignored so that the widget is always sized just large enough to accommodate the title.

### Groups

- sizing

### See Also

- [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit)

**Flags**: IRW

---
## Attr: Label.showDisabledIcon

### Description
If using an icon for this button, whether to switch the icon image if the button becomes disabled.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: Label.width

### Description
Size for this component's horizontal dimension. See [Canvas.width](Canvas.md#attr-canvaswidth) for more details.

Note that if [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit) is set, this property will be ignored so that the widget is always sized just large enough to accommodate the title.

### Groups

- sizing

### See Also

- [StatefulCanvas.autoFit](StatefulCanvas.md#attr-statefulcanvasautofit)

**Flags**: IRW

---
## Attr: Label.showFocusedIcon

### Description
If using an icon for this button, whether to switch the icon image when the button receives focus.

If [StatefulCanvas.showFocusedAsOver](StatefulCanvas.md#attr-statefulcanvasshowfocusedasover) is true, the `"Over"` icon will be displayed when the canvas has focus, otherwise a separate `"Focused"` icon will be displayed

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.showDownIcon

### Description
If using an icon for this button, whether to switch the icon image when the mouse goes down on the button.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.styleName

### Description
Set the CSS class for this widget. For a Label, this is equivalent to setting [Button.baseStyle](Button.md#attr-buttonbasestyle).

**Flags**: IRW

---
## Attr: Label.icon

### Description
Optional icon to be shown with the button title text.

Specify as the partial URL to an image, relative to the imgDir of this component. A sprited image can be specified using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format.

Note that the string "blank" is a valid setting for this attribute and will always result in the system blank image, with no state suffixes applied. Typically, this might be used when an iconStyle is also specified and the iconStyle renders the icon via a stateful background-image or other CSS approach.

### Groups

- buttonIcon

**Flags**: IRW

---
## Attr: Label.showSelectedIcon

### Description
If using an icon for this button, whether to switch the icon image when the button becomes selected.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: Label.iconAlign

### Description
If this button is showing an icon should it be right or left aligned?

### Groups

- buttonIcon

**Flags**: IR

---
## Method: Label.setIconOrientation

### Description
Changes the orientation of the icon relative to the text of the button.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| orientation | [String](#type-string) | false | — | The new orientation of the icon relative to the text of the button. |

### Groups

- buttonIcon

---
## Method: Label.setStyleName

### Description
Dynamically change the CSS class for this widget. For a Label, this is equivalent to [setBaseStyle()](StatefulCanvas.md#method-statefulcanvassetbasestyle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newStyle | [CSSStyleName](../reference.md#type-cssstylename) | false | — | new CSS style name |

---
## Method: Label.setIcon

### Description
Change the icon being shown next to the title text.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [SCImgURL](../reference_2.md#type-scimgurl) | false | — | URL of new icon |

### Groups

- buttonIcon

---
## Method: Label.setContents

### Description
Changes the contents of a widget to newContents, an HTML string.

When [dynamicContents](Canvas.md#attr-canvasdynamiccontents) is set, `setContents()` can also be called with no arguments to cause contents to be re-evaluated.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newContents | [HTMLString](../reference.md#type-htmlstring) | true | — | an HTML string to be set as the contents of this widget |

---
