# DrawLabel Documentation

[← Back to API Index](../reference.md)

---

## Class: DrawLabel

*Inherits from:* [DrawItem](DrawItem.md#class-drawitem)

### Description
DrawItem subclass to render a single-line text label.

---
## ClassAttr: DrawLabel.defaultSerifFont

### Description
This setting exists due to platform limitations in some versions of Internet Explorer where the browser does not recognize the five generic font families (`cursive`, `fantasy`, `monospace`, `sans-serif`, and `serif`) and instead uses a non-configurable, default font. This setting specifies a specific font to replace the `serif` keyword should a DrawLabel list it in its [font family](#attr-drawlabelfontfamily).

**Flags**: IRW

---
## ClassAttr: DrawLabel.defaultCursiveFont

### Description
This setting exists due to platform limitations in some versions of Internet Explorer where the browser does not recognize the five generic font families (`cursive`, `fantasy`, `monospace`, `sans-serif`, and `serif`) and instead uses a non-configurable, default font. This setting specifies a specific font to replace the `cursive` keyword should a DrawLabel list it in its [font family](#attr-drawlabelfontfamily).

**Flags**: IRW

---
## ClassAttr: DrawLabel.LEFT

### Description
A declared value of the enum type [LabelAlignment](../reference.md#type-labelalignment).

**Flags**: R

---
## ClassAttr: DrawLabel.defaultSansSerifFont

### Description
This setting exists due to platform limitations in some versions of Internet Explorer where the browser does not recognize the five generic font families (`cursive`, `fantasy`, `monospace`, `sans-serif`, and `serif`) and instead uses a non-configurable, default font. This setting specifies a specific font to replace the `sans-serif` keyword should a DrawLabel list it in its [font family](#attr-drawlabelfontfamily).

**Flags**: IRW

---
## ClassAttr: DrawLabel.CENTER

### Description
A declared value of the enum type [LabelAlignment](../reference.md#type-labelalignment).

**Flags**: R

---
## ClassAttr: DrawLabel.defaultMonospaceFont

### Description
This setting exists due to platform limitations in some versions of Internet Explorer where the browser does not recognize the five generic font families (`cursive`, `fantasy`, `monospace`, `sans-serif`, and `serif`) and instead uses a non-configurable, default font. This setting specifies a specific font to replace the `monospace` keyword should a DrawLabel list it in its [font family](#attr-drawlabelfontfamily).

**Flags**: IRW

---
## ClassAttr: DrawLabel.RIGHT

### Description
A declared value of the enum type [LabelAlignment](../reference.md#type-labelalignment).

**Flags**: R

---
## ClassAttr: DrawLabel.END

### Description
A declared value of the enum type [LabelAlignment](../reference.md#type-labelalignment).

**Flags**: R

---
## ClassAttr: DrawLabel.START

### Description
A declared value of the enum type [LabelAlignment](../reference.md#type-labelalignment).

**Flags**: R

---
## ClassAttr: DrawLabel.defaultFantasyFont

### Description
This setting exists due to platform limitations in some versions of Internet Explorer where the browser does not recognize the five generic font families (`cursive`, `fantasy`, `monospace`, `sans-serif`, and `serif`) and instead uses a non-configurable, default font. This setting specifies a specific font to replace the `fantasy` keyword should a DrawLabel list it in its [font family](#attr-drawlabelfontfamily).

**Flags**: IRW

---
## Attr: DrawLabel.fontStyle

### Description
Font style, similar to the CSS font-style attribute, eg "normal", "italic".

### See Also

- [DrawLabel.styleName](#attr-drawlabelstylename)

**Flags**: IR

---
## Attr: DrawLabel.knobs

### Description
DrawLabel only supports the "move" knob type.

### See Also

- [DrawItem.knobs](DrawItem.md#attr-drawitemknobs)

**Flags**: IR

---
## Attr: DrawLabel.styleName

### Description
For [drawingType](DrawPane.md#attr-drawpanedrawingtype) "svg" only, the CSS class applied to this label. Similar to [Canvas.styleName](Canvas.md#attr-canvasstylename). The font properties [DrawLabel.fontSize](#attr-drawlabelfontsize), [DrawLabel.fontWeight](#attr-drawlabelfontweight), [DrawLabel.fontStyle](#attr-drawlabelfontstyle), and [DrawLabel.fontFamily](#attr-drawlabelfontfamily), unless set to null, take priority over any CSS settings. This property can be used in combination with [DrawLabel.escapeContents](#attr-drawlabelescapecontents) if needed. but note that in SVG, the precedence of CSS and inline styling applied to an element works differently that it does in HTML. See [Mozilla SVG Developer Reference](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/text)

Note that only font sizes defined in pixels are supported through this property.

### See Also

- [DrawLabel.escapeContents](#attr-drawlabelescapecontents)

**Flags**: IRW

---
## Attr: DrawLabel.fontWeight

### Description
Font weight, similar to the CSS font-weight attribute, eg "normal", "bold".

### See Also

- [DrawLabel.styleName](#attr-drawlabelstylename)

**Flags**: IR

---
## Attr: DrawLabel.escapeContents

### Description
For [SVG-based](DrawPane.md#attr-drawpanedrawingtype) [DrawPane](DrawPane.md#class-drawpane)s, whether to escape the specified [DrawLabel.contents](#attr-drawlabelcontents) of this label so that any markup syntax is rendered "as is," without being interpreted as SVG. This setting should not be customized when working with other [drawingType](DrawPane.md#attr-drawpanedrawingtype)s, as the [DrawLabel.contents](#attr-drawlabelcontents) are always escaped in such case.

In SVG, a [DrawLabel](#class-drawlabel)'s [DrawLabel.contents](#attr-drawlabelcontents) are rendered inside a ``<text>`` tag, so any SVG that's legal inside that tag can be set as the [DrawLabel.contents](#attr-drawlabelcontents) when [DrawLabel.escapeContents](#attr-drawlabelescapecontents) is false. See [Mozilla SVG Developer Reference](https://developer.mozilla.org/en-US/docs/Web/SVG/Element/text) for more information about what exactly is supported.

Note that the Framework will not be able to determine the width or height of a [DrawLabel](#class-drawlabel) when this property is false, so the Framework will consider both dimensions to be zero, and centering will not work (e.g. for [DrawItem.titleLabel](DrawItem.md#attr-drawitemtitlelabel) autochildren). For top-level [DrawLabel](#class-drawlabel)s, you may be able to get the DOM to center your content by setting [alignment](#attr-drawlabelalignment) as "center" - the DOM will then interpret the [DrawLabel.left](#attr-drawlabelleft), [DrawLabel.top](#attr-drawlabeltop) coordinates of the label as its centerpoint even though our Framework doesn't know the label's actual size.

For a [titleLabel](DrawItem.md#attr-drawitemtitlelabel), the [alignment](#attr-drawlabelalignment) setting is ignored, as the Framework always positions it using "start" alignment, but SVG code such as the following demonstrates that centering is possible (via the "style" setting):

```
 <tspan text-decoration='underline' font-size='20px' 
        style='dominant-baseline:central; text-anchor:middle;'>MyLabel
 </tspan>
 
```

### See Also

- [DrawLabel.contents](#attr-drawlabelcontents)
- [DrawLabel.alignment](#attr-drawlabelalignment)

**Flags**: IRW

---
## Attr: DrawLabel.alignment

### Description
Sets the text alignment from the x position. Similar to HTML5 context.textAlign with alignment values such as "start", "center", and "end".

Note that this setting is ignored for [DrawItem.titleLabel](DrawItem.md#attr-drawitemtitlelabel) autochildren, which are always considered to have "start" alignment to make handling of [DrawItem.titleRotationMode](DrawItem.md#attr-drawitemtitlerotationmode) simpler.

**Flags**: IR

---
## Attr: DrawLabel.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: DrawLabel.fontSize

### Description
Font size in pixels, similar to the CSS font-size attribute.

### See Also

- [DrawLabel.styleName](#attr-drawlabelstylename)

**Flags**: IRW

---
## Attr: DrawLabel.lineColor

### Description
The text color of the label.

### Groups

- line

**Flags**: IRW

---
## Attr: DrawLabel.contents

### Description
This is the content that will exist as the label.

### See Also

- [DrawLabel.escapeContents](#attr-drawlabelescapecontents)

**Flags**: IRW

---
## Attr: DrawLabel.fontFamily

### Description
Font family name, similar to the CSS font-family attribute.

### See Also

- [DrawLabel.styleName](#attr-drawlabelstylename)

**Flags**: IR

---
## Attr: DrawLabel.rotation

### Description
Rotation in degrees about the [top](#attr-drawlabeltop) [left](#attr-drawlabelleft) corner. The positive direction is clockwise.

**Flags**: IR

---
## Attr: DrawLabel.top

### Description
Sets the amount from the top of its positioning that the element should be placed.

**Flags**: IR

---
## Attr: DrawLabel.left

### Description
Sets the amount from the left of its positioning that the element should be placed.

**Flags**: IR

---
## Method: DrawLabel.setContents

### Description
Sets this DrawLabel's [contents](#attr-drawlabelcontents).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| contents | [String](#type-string) | false | — | the new contents. |

---
## Method: DrawLabel.setLineColor

### Description
Sets the text color of the label.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [CSSColor](../reference_2.md#type-csscolor) | false | — | new text color. |

---
## Method: DrawLabel.setStyleName

### Description
Sets this DrawLabel's [styleName](#attr-drawlabelstylename).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| styleName | [CSSStyleName](../reference.md#type-cssstylename) | false | — | the new styleName |

---
## Method: DrawLabel.setFontSize

### Description
Sets this DrawLabel's [fontSize](#attr-drawlabelfontsize).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| size | [int](../reference.md#type-int) | false | — | the new font size in pixels. |

---
## Method: DrawLabel.setEscapeContents

### Description
Sets the [DrawLabel.escapeContents](#attr-drawlabelescapecontents) property for this DrawLabel.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| escapeContents | [boolean](../reference.md#type-boolean) | false | — | whether to escape [DrawLabel.contents](#attr-drawlabelcontents) |

---
## Method: DrawLabel.getCenter

### Description
Get the center point of the label.

### Returns

`[Point](#type-point)` — the center point

---
## Method: DrawLabel.getBoundingBox

### Description
Returns the left, top, left + textWidth, top + textHeight

### Returns

`[Array of double](#type-array-of-double)` — x1, y1, x2, y2 coordinates

---
