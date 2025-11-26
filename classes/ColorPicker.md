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
The title for the 'Sat' field in the complex chooser.

### Groups

- i18nMessages

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
## Attr: ColorPicker.lumWidth

### Description
Width of the Luminosity bar

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
## Attr: ColorPicker.lumFieldTitle

### Description
The title for the 'Luminosity' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.defaultColor

### Description
The default color. This is the color that is selected when the picker first loads

**Flags**: IR

---
## Attr: ColorPicker.blueFieldTitle

### Description
The title for the 'Blue' field in the complex chooser.

### Groups

- i18nMessages

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
The title for the 'HTML' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.hueFieldTitle

### Description
The title for the 'Hue' field in the complex chooser.

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
The text to show when the mouse hovers over the 'HTML' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.redFieldTitle

### Description
The title for the 'Red' field in the complex chooser.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorPicker.swatchWidth

### Description
Displayed width of the color swatch image. The default width is approximately that used by the Windows® XP color picking window

**Flags**: IR

---
## Attr: ColorPicker.greenFieldTitle

### Description
The title for the 'Green' field in the complex chooser.

### Groups

- i18nMessages

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
The text to show when the mouse hovers over the 'Luminosity' field in the complex chooser.

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
| properties | [Object](../reference.md#type-object) | false | — | Properties to apply to the global ColorPicker object |
| keepCurrentState | [boolean](../reference.md#type-boolean) | true | — | Should we keep the current state? If false (or not provided), revert to default state |

---
## Method: ColorPicker.getRed

### Description
Returns the Red element of the currently-selected color, as an integer from 0-255

### Returns

`[int](../reference.md#type-int)` — red color component

### See Also

- [ColorPicker.setRed](#method-colorpickersetred)

---
## Method: ColorPicker.getBlue

### Description
Returns the Blue element of the currently-selected color, as an integer from 0-255

### Returns

`[int](../reference.md#type-int)` — blue color component

### See Also

- [ColorPicker.setBlue](#method-colorpickersetblue)

---
## Method: ColorPicker.setHue

### Description
Sets the Hue of the selected color

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 239 |

### See Also

- [ColorPicker.getHue](#method-colorpickergethue)

---
## Method: ColorPicker.setSaturation

### Description
Sets the Saturation of the selected color

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 240 |

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
Returns the Green element of the currently-selected color, as an integer from 0-255

### Returns

`[int](../reference.md#type-int)` — green color component

### See Also

- [ColorPicker.setGreen](#method-colorpickersetgreen)

---
## Method: ColorPicker.setBlue

### Description
Sets the Blue element of the selected color

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 255 |

### See Also

- [ColorPicker.getBlue](#method-colorpickergetblue)

---
## Method: ColorPicker.setGreen

### Description
Sets the Green element of the selected color

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
Sets the Red element of the selected color

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 255 |

### See Also

- [ColorPicker.getRed](#method-colorpickergetred)

---
## Method: ColorPicker.getSaturation

### Description
Returns the Saturation of the currently-selected color, as an integer from 0-240

### Returns

`[int](../reference.md#type-int)` — saturation value

### See Also

- [ColorPicker.setSaturation](#method-colorpickersetsaturation)

---
## Method: ColorPicker.getLuminosity

### Description
Returns the Luminosity (brightness) of the currently-selected color, as an integer from 0-240

### Returns

`[int](../reference.md#type-int)` — luminosity value

### See Also

- [ColorPicker.setLuminosity](#method-colorpickersetluminosity)

---
## Method: ColorPicker.colorChanged

### Description
Override this method to be kept informed when the ColorPicker changes in real-time (for example, if you need to update your own GUI accordingly). Then use the getXxxx() methods (for example, [getBlue()](#method-colorpickergetblue) or [getLuminosity()](#method-colorpickergetluminosity))to obtain current state as required.

### See Also

- [ColorPicker.colorSelected](#method-colorpickercolorselected)

---
## Method: ColorPicker.getHtmlColor

### Description
Returns the currently-selected color, in HTML color representation form, as a string. HTML color representation is a hash sign, followed by the red, green and blue elements of the color in 2-digit hex form - for example "#F17F1D"

### Returns

`[String](#type-string)` — HTML color value

### See Also

- [ColorPicker.setHtmlColor](#method-colorpickersethtmlcolor)

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
Sets the Luminosity (brightness) of the selected color

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Number](#type-number) | false | — | An integer between 0 and 240 |

### See Also

- [ColorPicker.getLuminosity](#method-colorpickergetluminosity)

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

- [ColorPicker.colorChanged](#method-colorpickercolorchanged)

---
## Method: ColorPicker.getHue

### Description
Returns the Hue of the currently-selected color, as an integer from 0-239

### Returns

`[int](../reference.md#type-int)` — hue value

### See Also

- [ColorPicker.setHue](#method-colorpickersethue)

---
## Method: ColorPicker.setHtmlColor

### Description
Changes the selected color to the one represented by the supplied HTML color string. Note that the method only accepts the parameter if it represents a valid color (otherwise it is simply ignored).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [String](#type-string) | false | — | A string in HTML color representation format (#RRGGBB) |

### See Also

- [ColorPicker.getHtmlColor](#method-colorpickergethtmlcolor)

---
