# ImgSectionHeader Documentation

[← Back to API Index](../reference.md)

---

## Class: ImgSectionHeader

*Inherits from:* [HLayout](../reference.md#class-hlayout)

### Description
SectionHeader class based on an HLayout with [StretchImg](StretchImg.md#class-stretchimg) background.

---
## Attr: ImgSectionHeader.controlsLayout

### Description
A [Layout](Layout.md#class-layout) containing specified [ImgSectionHeader.controls](#attr-imgsectionheadercontrols) if any. Sets [Layout.membersMargin](Layout.md#attr-layoutmembersmargin):5, [Layout.defaultLayoutAlign](Layout.md#attr-layoutdefaultlayoutalign):"center", and RTL-sensitive [Layout.align](Layout.md#attr-layoutalign) (right by default).

**Flags**: IR

---
## Attr: ImgSectionHeader.clipTitle

### Description
If the title for this section header is too large for the available space, should the title be clipped?

This feature is supported only in browsers that support the CSS UI text-overflow property (IE6+, Firefox 7+, Safari, Chrome, Opera 9+).

**Flags**: IR

---
## Attr: ImgSectionHeader.icon

### Description
Optional icon to be shown with the button title text.

Specify as the partial URL to an image, relative to the imgDir of this component. A sprited image can be specified using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format.

Note that the string "blank" is a valid setting for this attribute and will always result in the system blank image, with no state suffixes applied. Typically, this might be used when an iconStyle is also specified and the iconStyle renders the icon via a stateful background-image or other CSS approach.

### Groups

- buttonIcon

**Flags**: IRW

---
## Attr: ImgSectionHeader.iconWidth

### Description
Width in pixels of the icon image.

If unset, defaults to [iconSize](StatefulCanvas.md#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: ImgSectionHeader.background

### Description
Background of the section header, based on a [StretchImg](StretchImg.md#class-stretchimg).

**Flags**: R

---
## Attr: ImgSectionHeader.iconOrientation

### Description
If this button is showing an icon should it appear to the left or right of the title? valid options are `"left"` and `"right"`.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: ImgSectionHeader.controls

### Description
Custom controls to be shown on top of this section header.

These controls are shown in the [ImgSectionHeader.controlsLayout](#attr-imgsectionheadercontrolslayout).

Note that this is an init-time property. If you need to dynamically change what controls are displayed to the user, we would recommend embedding the controls in a Layout or similar container. This will allow you to show/hide or add/remove members at runtime by manipulating the existing control(s) set up at init time.

**Flags**: IR

---
## Attr: ImgSectionHeader.noDoubleClicks

### Description
By default doubleClicks are disabled for SectionHeaders. All mouse click events will be handled as single clicks. Set this property to `false` to enable standard double-click handling.

**Flags**: IRA

---
## Attr: ImgSectionHeader.showClippedTitleOnHover

### Description
If true and the title is clipped, then a hover containing the full title of this section header is enabled.

### Groups

- hovers

**Flags**: IRW

---
## Attr: ImgSectionHeader.iconSize

### Description
Size in pixels of the icon image.

The [iconWidth](StatefulCanvas.md#attr-statefulcanvasiconwidth) and [iconHeight](StatefulCanvas.md#attr-statefulcanvasiconheight) properties can be used to configure width and height separately.

Note: When configuring the properties of a `StatefulCanvas` (or derivative) [AutoChild](../reference.md#type-autochild), it is best to set the `iconWidth` and `iconHeight` to the same value rather than setting an `iconSize`. This is because certain skins or customizations thereto might set the `iconWidth` and `iconHeight`, making the customization of the AutoChild's `iconSize` ineffective.

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: ImgSectionHeader.iconAlign

### Description
If this button is showing an icon should it be right or left aligned?

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: ImgSectionHeader.iconHeight

### Description
Height in pixels of the icon image.

If unset, defaults to [iconSize](StatefulCanvas.md#attr-statefulcanvasiconsize).

### Groups

- buttonIcon

**Flags**: IR

---
## Attr: ImgSectionHeader.title

### Description
Title to show for the section

**Flags**: IRW

---
## Attr: ImgSectionHeader.prompt

### Description
Prompt displayed in hover canvas if [showHover](Canvas.md#attr-canvasshowhover) is true.

### Groups

- hovers

**Flags**: IRW

---
## Method: ImgSectionHeader.titleHover

### Description
Optional stringMethod to fire when the user hovers over this section header and the title is clipped. If [ImgSectionHeader.showClippedTitleOnHover](#attr-imgsectionheadershowclippedtitleonhover) is true, the default behavior is to show a hover canvas containing the HTML returned by [ImgSectionHeader.titleHoverHTML](#method-imgsectionheadertitlehoverhtml). Return false to suppress this default behavior.

### Returns

`[boolean](../reference.md#type-boolean)` — false to suppress the standard hover

### Groups

- hovers

### See Also

- [ImgSectionHeader.clipTitle](#attr-imgsectionheadercliptitle)
- [ImgSectionHeader.titleClipped](#method-imgsectionheadertitleclipped)

---
## Method: ImgSectionHeader.setIcon

### Description
Change the icon being shown for the header.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| icon | [SCImgURL](../reference_2.md#type-scimgurl) | false | — | URL of new icon |

---
## Method: ImgSectionHeader.getSectionStack

### Description
For a SectionHeader embedded in a SectionStack, this method will return a pointer to the [SectionStack](SectionStack.md#class-sectionstack) in which this section header is embedded.

### Returns

`[SectionStack](#type-sectionstack)` — Section Stack containing this section header

---
## Method: ImgSectionHeader.titleHoverHTML

### Description
Returns the HTML that is displayed by the default [titleHover](#method-imgsectionheadertitlehover) handler. Return null or an empty string to cancel the hover.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| defaultHTML | [HTMLString](../reference.md#type-htmlstring) | false | — | the HTML that would have been displayed by default |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover. If null or an empty string, then the hover is canceled.

---
## Method: ImgSectionHeader.titleClipped

### Description
Is the title of this section header clipped by [section controls](#attr-imgsectionheadercontrols) or the edge of the header?

### Returns

`[boolean](../reference.md#type-boolean)` — whether the title is clipped.

### See Also

- [ImgSectionHeader.clipTitle](#attr-imgsectionheadercliptitle)

**Flags**: A

---
## Method: ImgSectionHeader.setAlign

### Description
Sets the horizontal alignment of the title.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| align | [String](#type-string) | false | — | the new alignment |

---
## Method: ImgSectionHeader.setIconOrientation

### Description
If this header is showing an icon should it appear to the left or right of the title? Valid options are "left" and "right".

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| orientation | [String](#type-string) | false | — | the new orientation |

---
## Method: ImgSectionHeader.setPrompt

### Description
Sets the text shown as a tooltip for the header.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| prompt | [HTMLString](../reference.md#type-htmlstring) | false | — | the new tooltip |

---
