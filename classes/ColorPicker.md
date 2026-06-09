# ColorPicker Documentation

[← Back to API Index](../reference.md)

---

## Class: ColorPicker

*Inherits from:* [Window](Window.md#class-window)

### Description
The ColorPicker widget allows the user to select a color from anywhere in the color spectrum. It also supports selecting the alpha (opacity) value of the color. The picker supports a simple mode - which allows for one-click selection from a standard palette of colors - and a complex mode which allow the user to define any conceivable color. It is possible for the user to switch from simple mode to complex by interacting with the widget. In general, the widget provides very similar functionality to the color picker dialogs found in graphics packages and other desktop software.

---
## Attr: ColorPicker.cancelButton

### Description
Cancel button for the ColorPicker

**Flags**: R

---
## Attr: ColorPicker.satFieldTitle

### Description
—

### Groups

- i18nMessages

**Deprecated**

**Flags**: IR

---
## Attr: ColorPicker.lessButtonTitle

### Description
The title for the button that switches to a less complex view.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.basicColorLabel

### Description
The label shown above the basic color blocks.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.color

### Description
The current color of the picker. Accepts a CSS color string in any [ColorFormat](../reference_2.md#type-colorformat) (including [named colors](Colors.md#classattr-colorscolornames)) or an existing [Color](../reference_2.md#object-color) object. When not set, the picker initializes to [ColorPicker.defaultColor](#attr-colorpickerdefaultcolor).

Use [ColorPicker.getColor](#method-colorpickergetcolor) to retrieve the current color as a [Color](../reference_2.md#object-color) object, or [ColorPicker.getColorString](#method-colorpickergetcolorstring) to retrieve it as a CSS string in any [ColorFormat](../reference_2.md#type-colorformat).

### See Also

- [ColorPicker.getColor](#method-colorpickergetcolor)
- [ColorPicker.getColorString](#method-colorpickergetcolorstring)

**Flags**: IRW

---
## Attr: ColorPicker.lumWidth

### Description
Width of the lightness bar

**Flags**: IR

---
## Attr: ColorPicker.autoHide

### Description
When this property is set to true, the `ColorPicker` will automatically hide when a color has been selected using the swatch picker, even in "complex" mode. By default it will only hide the `ColorPicker` in "simple" defaultPickMode.

Set this property to false to disable the `ColorPicker` from automatically hiding, this can be especially useful when for instance embedding this component inside another component.

### See Also

- [ColorPicker.defaultPickMode](#attr-colorpickerdefaultpickmode)

**Flags**: IR

---
## Attr: ColorPicker.moreButtonTitle

### Description
The title for the button that switches to a more complex view.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.showOkButton

### Description
Should the OK button be visible. Set to false to hide the OK button.

**Flags**: IRA

---
## Attr: ColorPicker.showCancelButton

### Description
Should the Cancel button be visible. Set to false to hide the Cancel button.

**Flags**: IRA

---
## Attr: ColorPicker.colorButtonSize

### Description
Width and height of the basic color boxes (they are always square, and they are all the same size).

**Flags**: IR

---
## Attr: ColorPicker.paletteMode

### Description
Controls which palette visualization is shown in complex mode.

*   `"square"` - Hue x Saturation grid (X=hue 0-360, Y=saturation 100-0), fixed at L=50. Best for precise color selection.
*   `"wheel"` - Oklch color wheel (angle=hue, radius=chroma). Perceptually uniform hue spacing; lightness tracks the current lightness slider value.

**Flags**: IRW

---
## Attr: ColorPicker.lumFieldTitle

### Description
—

### Groups

- i18nMessages

**Deprecated**

**Flags**: IR

---
## Attr: ColorPicker.defaultColor

### Description
The default color. This is the color selected when the picker first loads if no [Color](../reference_2.md#object-color) is specified, and the color to which the picker reverts when [ColorPicker.getSharedColorPicker](#classmethod-colorpickergetsharedcolorpicker) is called without `keepCurrentState`.

### See Also

- [Color](../reference_2.md#object-color)

**Flags**: IR

---
## Attr: ColorPicker.blueFieldTitle

### Description
—

### Groups

- i18nMessages

**Deprecated**

**Flags**: IR

---
## Attr: ColorPicker.showHarmonyRow

### Description
Whether to show the [ColorPicker.harmonyRow](#attr-colorpickerharmonyrow) of color harmonies below the palette in complex mode.

**Flags**: IR

---
## Attr: ColorPicker.selectedColorLabel

### Description
The label shown next to the selected color box.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.okButton

### Description
"OK" button for the ColorPicker

**Flags**: R

---
## Attr: ColorPicker.blueFieldPrompt

### Description
The text to show when the mouse hovers over the 'Blue' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.autoCenterOnShow

### Description
If [ColorPicker.autoPosition](#attr-colorpickerautoposition) is false, this property controls whether to automatically center the colorPicker every time it is redisplayed with the show() method.

### See Also

- [ColorPicker.autoPosition](#attr-colorpickerautoposition)

**Flags**: IR

---
## Attr: ColorPicker.autoPosition

### Description
If true, causes the ColorPicker to appear near where the mouse was last clicked. If false, the ColorPicker is centered on first show; depending on the value of [ColorPicker.autoCenterOnShow](#attr-colorpickerautocenteronshow), it either reappears wherever it was last shown after hide/show(), or centered regardless of where it was last shown.

### See Also

- [ColorPicker.autoCenterOnShow](#attr-colorpickerautocenteronshow)

**Flags**: IR

---
## Attr: ColorPicker.satFieldPrompt

### Description
The text to show when the mouse hovers over the 'Saturation' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.greenFieldPrompt

### Description
The text to show when the mouse hovers over the 'Green' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.showModeToggleButton

### Description
Should the Mode Toggle button be visible. Set to false to hide the Mode Toggle button.

**Flags**: IRA

---
## Attr: ColorPicker.allowComplexMode

### Description
Should the "complex" mode be allowed for this ColorPicker? If false, no "More" button is shown on the simple picker

**Flags**: IR

---
## Attr: ColorPicker.okButtonTitle

### Description
The title for the 'OK' button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.defaultOpacity

### Description
The initial opacity value for the component, as a percentage value between 0 and 100

**Flags**: IR

---
## Attr: ColorPicker.supportsTransparency

### Description
Determines whether to show the opacity slider. This allows the user to select colors with an alpha element (ie, semi-transparent colors). If this attribute is set to false, no opacity slider is shown, and all colors are completely opaque.

**Flags**: IR

---
## Attr: ColorPicker.htmlFieldTitle

### Description
The title for the hex color field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.hueFieldTitle

### Description
—

### Groups

- i18nMessages

**Deprecated**

**Flags**: IR

---
## Attr: ColorPicker.harmonyRow

### Description
Row of clickable swatches showing oklch-computed color harmonies (analogous, triadic, complement) of the currently-selected color. Visible only in [complex mode](../reference.md#type-colorpickermode).

**Flags**: R

---
## Attr: ColorPicker.rgbItemHover

### Description
Hover text shown when the mouse is over the RGB form row title.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.swatchHeight

### Description
Displayed height of the color swatch image. The default height is approximately that used by the Windows® XP color picking window

**Flags**: IR

---
## Attr: ColorPicker.redFieldPrompt

### Description
The text to show when the mouse hovers over the 'Red' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.htmlFieldPrompt

### Description
The text to show when the mouse hovers over the hex field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.redFieldTitle

### Description
—

### Groups

- i18nMessages

**Deprecated**

**Flags**: IR

---
## Attr: ColorPicker.swatchWidth

### Description
Displayed width of the color swatch image. The default width is approximately that used by the Windows® XP color picking window

**Flags**: IR

---
## Attr: ColorPicker.greenFieldTitle

### Description
—

### Groups

- i18nMessages

**Deprecated**

**Flags**: IR

---
## Attr: ColorPicker.hueFieldPrompt

### Description
The text to show when the mouse hovers over the 'Hue' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.cancelButtonTitle

### Description
The title for the 'Cancel' button.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.cancelButtonConstructor

### Description
The class of the Cancel button. It is intended that you use either IButton or Button - other classes are unlikely to work correctly.

**Flags**: IRWA

---
## Attr: ColorPicker.hslItemTitle

### Description
Title shown on the HSL form row in the complex chooser.

**Flags**: IR

---
## Attr: ColorPicker.okButtonConstructor

### Description
The class of the "OK" button. It is intended that you use either IButton or Button - other classes are unlikely to work correctly.

**Flags**: IRWA

---
## Attr: ColorPicker.modeToggleButton

### Description
"More"/"Less" button for the ColorPicker

**Flags**: R

---
## Attr: ColorPicker.swatchImageURL

### Description
The location of the color swatch image file

**Flags**: IR

---
## Attr: ColorPicker.crosshairImageURL

### Description
The location of the crosshair image file

**Flags**: IR

---
## Attr: ColorPicker.lumFieldPrompt

### Description
The text to show when the mouse hovers over the 'Lightness' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.colorArray

### Description
Array of 40 HTML color strings, used to render the basic color selection boxes.

**Flags**: IR

---
## Attr: ColorPicker.opacitySliderLabel

### Description
The label shown next to the opacity slider. Ignored if [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) is false.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.hslItemHover

### Description
Hover text shown when the mouse is over the HSL form row title.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.colorButtonBaseStyle

### Description
Base CSS style applied to the basic color boxes

**Flags**: IR

---
## Attr: ColorPicker.defaultPickMode

### Description
The `ColorPicker` can operate in either a "simple" mode (where it displays just the 40 basic colors and allows the user to click one), or a "complex" mode (where the user can specify a color from anywhere in the spectrum, with an optional alpha element). The `defaultPickMode` attribute specifies which of these two modes is in force when the picker first loads.

### See Also

- [ColorPicker.allowComplexMode](#attr-colorpickerallowcomplexmode)

**Flags**: IR

---
## Attr: ColorPicker.opacityText

### Description
The text to show underneath the selected color box, so that it can be seen through semi-transparent colors. If you do not want such text, set this value to blank. This value is irrelevant if [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) is false.

**Flags**: IR

---
## Attr: ColorPicker.rgbItemTitle

### Description
Title shown on the RGB form row in the complex chooser.

**Flags**: IR

---
## Attr: ColorPicker.modeToggleButtonConstructor

### Description
The class of the mode toggle button. It is intended that you use either IButton or Button - other classes are unlikely to work correctly.

**Flags**: IRWA

---
## ClassMethod: ColorPicker.getSharedColorPicker

### Description
Returns the shared global ColorPicker. Many applications will only need one ColorPicker instance; for such use cases, it is a good idea to use the shared object for performance reasons.

The optional second parameter to this method indicates whether the shared picker should retain the state (mode, color and opacity) it was in last time it was used, or revert to defaults. Generally, you will want the picker to revert to default state; this gives the same user experience as creating a new instance without incurring the overhead. However, some use cases will benefit from the picker remembering what the user did last time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| properties | [Object](../reference.md#type-object) | true | — | Properties to apply to the global ColorPicker object |
| keepCurrentState | [boolean](../reference.md#type-boolean) | true | — | Should we keep the current state? If false (or not provided), revert to default state |

### Returns

`[ColorPicker](#type-colorpicker)` — the shared ColorPicker instance

---
## Method: ColorPicker.getColorString

### Description
Returns the currently-selected color as a CSS string in any [ColorFormat](../reference_2.md#type-colorformat). Equivalent to `getColor().getString(format)`. When [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) is false or the color is fully opaque, the alpha channel is omitted from the output.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| format | [ColorFormat](../reference_2.md#type-colorformat) | true | — | output format (defaults to "hex") |

### Returns

`[String](#type-string)` — CSS color string

### See Also

- [ColorPicker.getColor](#method-colorpickergetcolor)

---
## Method: ColorPicker.getRed

### Description
Returns the Red element of the currently-selected color, as an integer from 0-255.

### Returns

`[int](../reference.md#type-int)` — red color component

### See Also

- [ColorPicker.setRed](#method-colorpickersetred)

**Deprecated**

---
## Method: ColorPicker.getBlue

### Description
Returns the Blue element of the currently-selected color, as an integer from 0-255.

### Returns

`[int](../reference.md#type-int)` — blue color component

### See Also

- [ColorPicker.setBlue](#method-colorpickersetblue)

**Deprecated**

---
## Method: ColorPicker.setHue

### Description
Sets the Hue of the selected color.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 360 |

### See Also

- [ColorPicker.getHue](#method-colorpickergethue)

---
## Method: ColorPicker.setSaturation

### Description
Sets the Saturation of the selected color.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 100 |

### See Also

- [ColorPicker.getSaturation](#method-colorpickergetsaturation)

---
## Method: ColorPicker.setOpacity

### Description
Sets the Opacity of the selected color. Ignored if opacity is switched off.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 100 |

### See Also

- [ColorPicker.getOpacity](#method-colorpickergetopacity)

---
## Method: ColorPicker.getGreen

### Description
Returns the Green element of the currently-selected color, as an integer from 0-255.

### Returns

`[int](../reference.md#type-int)` — green color component

### See Also

- [ColorPicker.setGreen](#method-colorpickersetgreen)

**Deprecated**

---
## Method: ColorPicker.colorUpdated

### Description
Notification fired in real-time as the user manipulates the color picker (dragging the crosshair, adjusting sliders, typing in fields). The `color` parameter is an [Color](../reference_2.md#object-color) object; when [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) is true it carries the current alpha, otherwise alpha is always 1.

This is the preferred replacement for [ColorPicker.colorChanged](#method-colorpickercolorchanged), which passes no parameters and requires the caller to use getter methods.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [Color](#type-color) | false | — | the current color |

### See Also

- [ColorPicker.colorPicked](#method-colorpickercolorpicked)

---
## Method: ColorPicker.setBlue

### Description
Sets the Blue element of the selected color.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 255 |

### See Also

- [ColorPicker.getBlue](#method-colorpickergetblue)

---
## Method: ColorPicker.setGreen

### Description
Sets the Green element of the selected color.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 255 |

### See Also

- [ColorPicker.getGreen](#method-colorpickergetgreen)

---
## Method: ColorPicker.getOpacity

### Description
Returns the opacity of the currently-selected color, as an integer from 0-100. If opacity is switched off, this is always 100.

### Returns

`[int](../reference.md#type-int)` — opacity value

---
## Method: ColorPicker.setRed

### Description
Sets the Red element of the selected color.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 255 |

### See Also

- [ColorPicker.getRed](#method-colorpickergetred)

---
## Method: ColorPicker.colorPicked

### Description
Notification fired when the user commits a color selection - either by clicking a swatch in [simple mode](../reference.md#type-colorpickermode) or clicking OK in complex mode. The `color` parameter is an [Color](../reference_2.md#object-color) object; when [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) is true it carries the selected alpha, otherwise alpha is always 1.

This is the preferred replacement for [ColorPicker.colorSelected](#method-colorpickercolorselected), which passes color and opacity as separate parameters.

The `ColorPicker` may automatically hide itself after calling this method depending on [ColorPicker.autoHide](#attr-colorpickerautohide) and [ColorPicker.defaultPickMode](#attr-colorpickerdefaultpickmode).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [Color](#type-color) | false | — | the selected color |

### See Also

- [ColorPicker.colorUpdated](#method-colorpickercolorupdated)

---
## Method: ColorPicker.getSaturation

### Description
Returns the Saturation of the currently-selected color, as an integer from 0-100 (CSS-standard HSL percentage).

### Returns

`[int](../reference.md#type-int)` — saturation value

### See Also

- [ColorPicker.setSaturation](#method-colorpickersetsaturation)

**Deprecated**

---
## Method: ColorPicker.getLuminosity

### Description
—

### Returns

`[int](../reference.md#type-int)` — lightness value (0-100)

**Deprecated**

---
## Method: ColorPicker.setLightness

### Description
Sets the Lightness of the selected color (CSS-standard HSL: 0 is black, 50 is full chroma, 100 is white).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 100 |

### See Also

- [ColorPicker.getLightness](#method-colorpickergetlightness)

---
## Method: ColorPicker.colorChanged

### Description
Override this method to be kept informed when the ColorPicker changes in real-time (for example, if you need to update your own GUI accordingly). Then use the getXxxx() methods (for example, [getBlue()](#method-colorpickergetblue) or [getLuminosity()](#method-colorpickergetluminosity)) to obtain current state as required.

### See Also

- [ColorPicker.colorUpdated](#method-colorpickercolorupdated)
- [ColorPicker.colorSelected](#method-colorpickercolorselected)

**Deprecated**

---
## Method: ColorPicker.getHtmlColor

### Description
Returns the currently-selected color as a hex string. When [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) is true and the color has alpha < 1, the string includes the alpha channel as two additional hex digits (e.g. `"#F17F1D80"`); otherwise it is a standard 6-digit hex string (e.g. `"#F17F1D"`).

### Returns

`[String](#type-string)` — HTML color value

### See Also

- [ColorPicker.setHtmlColor](#method-colorpickersethtmlcolor)

**Deprecated**

---
## Method: ColorPicker.setCurrentPickMode

### Description
Changes the pick mode of this `ColorPicker` to `pickMode`.

Note: It is not allowed to set the pick mode to "complex" if [allowComplexMode](#attr-colorpickerallowcomplexmode) is `false`.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| pickMode | [ColorPickerMode](../reference.md#type-colorpickermode) | false | — | the new pick mode. |

---
## Method: ColorPicker.getColor

### Description
Returns the currently-selected color as an [Color](../reference_2.md#object-color) object. If [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) is true the returned Color includes the selected alpha; otherwise alpha is 1.

### Returns

`[Color](#type-color)` — the current color

### See Also

- [ColorPicker.getColorString](#method-colorpickergetcolorstring)

---
## Method: ColorPicker.getLightness

### Description
Returns the Lightness of the currently-selected color, as an integer from 0-100 (CSS-standard HSL percentage). 0 is black, 50 is full chroma, 100 is white.

### Returns

`[int](../reference.md#type-int)` — lightness value

### See Also

- [ColorPicker.setLightness](#method-colorpickersetlightness)

**Deprecated**

---
## Method: ColorPicker.setSupportsTransparency

### Description
Set the [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) flag.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| transparencyFlag | [boolean](../reference.md#type-boolean) | false | — | Set to true to enable transparency/opacity |

---
## Method: ColorPicker.setLuminosity

### Description
—

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 100 |

**Deprecated**

---
## Method: ColorPicker.setColor

### Description
Sets the currently-selected color. Accepts any value that [Colors.getColor](Colors.md#classmethod-colorsgetcolor) accepts: a CSS color string, a structured `{r,g,b}` / `{h,s,l}` / `{L,C,h}` object, or an existing [Color](../reference_2.md#object-color).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string)|[Color](#type-color)|[Object](../reference.md#type-object) | false | — | new color value |

### See Also

- [ColorPicker.getColor](#method-colorpickergetcolor)
- [ColorPicker.getColorString](#method-colorpickergetcolorstring)

---
## Method: ColorPicker.colorSelected

### Description
Override this method to be notified when the user selects a color either by clicking a basic color box in simple mode, or by clicking the OK button in complex mode. It is not intended that client code call this method. The `ColorPicker` may automatically hide itself after calling this method depending on [ColorPicker.autoHide](#attr-colorpickerautohide) and [ColorPicker.defaultPickMode](#attr-colorpickerdefaultpickmode).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string) | false | — | The color selected, in HTML format. |
| opacity | [Integer](../reference_2.md#type-integer) | false | — | The selected opacity, from 0 (transparent) to 100 (opaque), or null if [ColorPicker.supportsTransparency](#attr-colorpickersupportstransparency) is false or the picker selected a color while in [simple mode](../reference.md#type-colorpickermode). |

### See Also

- [ColorPicker.colorPicked](#method-colorpickercolorpicked)
- [ColorPicker.colorChanged](#method-colorpickercolorchanged)

**Deprecated**

---
## Method: ColorPicker.getHue

### Description
Returns the Hue of the currently-selected color, as an integer from 0-360 (CSS-standard HSL hue wheel).

### Returns

`[int](../reference.md#type-int)` — hue value

### See Also

- [ColorPicker.setHue](#method-colorpickersethue)

**Deprecated**

---
## Method: ColorPicker.setHtmlColor

### Description
Changes the selected color to the one represented by the supplied HTML color string. Accepts any valid CSS color string (hex, rgb(), hsl(), named colors, "transparent"). Invalid values are ignored.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | a CSS color string |

### See Also

- [ColorPicker.getHtmlColor](#method-colorpickergethtmlcolor)

**Deprecated**

---
