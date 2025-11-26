# ColorItem Documentation

[← Back to API Index](../reference.md)

---

## Class: ColorItem

*Inherits from:* [TextItem](TextItem.md#class-textitem)

### Description
Form item for selecting a color via a pop-up [ColorPicker](ColorPicker.md#class-colorpicker).

---
## Attr: ColorItem.pickerIconWidth

### Description
If [showPickerIcon](#attr-coloritemshowpickericon) is true for this item, this property governs the size of the picker icon. If unset, the picker icon will be sized as a square to fit in the available height for the icon.

Note that if spriting is being used, and the image to be displayed is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.

### Groups

- pickerIcon

**Flags**: IRW

---
## Attr: ColorItem.allowComplexMode

### Description
Should "complex" mode be allowed for the [ColorPicker](ColorPicker.md#class-colorpicker) window associated with this ColorItem?

If false, no "More" button is shown on the simple picker

**Flags**: IR

---
## Attr: ColorItem.pickerIconSrc

### Description
If [showPickerIcon](#attr-coloritemshowpickericon) is true for this item, this property governs the [src](FormItemIcon.md#attr-formitemiconsrc) of the picker icon image to be displayed.

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string.

### Groups

- pickerIcon

**Flags**: IRW

---
## Attr: ColorItem.pickerIconPrompt

### Description
Prompt to show when the user hovers the mouse over the picker icon.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: ColorItem.defaultPickerMode

### Description
The [defaultPickMode](ColorPicker.md#attr-colorpickerdefaultpickmode) for the [ColorPicker](ColorPicker.md#class-colorpicker) associated with this `ColorItem`.

### See Also

- [ColorPicker.defaultPickMode](ColorPicker.md#attr-colorpickerdefaultpickmode)

**Flags**: IR

---
## Attr: ColorItem.showPickerIcon

### Description
Should the pick button icon be shown for choosing colors from a ColorPicker

**Flags**: IRW

---
## Attr: ColorItem.pickerIconHeight

### Description
If [showPickerIcon](#attr-coloritemshowpickericon) is true for this item, this property governs the size of the picker icon. If unset, the picker icon will be sized as a square to fit in the available height for the icon.

Note that if spriting is being used, and the image to be displayed is specified using css properties such as `background-image`, `background-size`, changing this value may result in an unexpected appearance as the image will not scale.  
Scaleable spriting can be achieved using the [SCSpriteConfig](../reference.md#type-scspriteconfig) format. See the section on spriting in the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for further information.

### Groups

- pickerIcon

**Flags**: IRW

---
## Attr: ColorItem.supportsTransparency

### Description
Determines whether the [ColorPicker](ColorPicker.md#class-colorpicker) associated with this ColorItem allows the user to set transparency/opacity information whilst selecting a color. If false, no opacity slider is shown and all colors are 100% opaque.

When an opacity value is selected, the HTML color string produced is 8 characters long because the opacity setting is included. You can also capture the the separate color and opacity information by overriding [ColorItem.pickerColorSelected](#method-coloritempickercolorselected).

**Flags**: IRW

---
## Method: ColorItem.pickerColorSelected

### Description
Store the color value selected by the user from the color picker. You will need to override this method if you wish to capture opacity information from the [ColorPicker](ColorPicker.md#class-colorpicker).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| color | [String](#type-string) | false | — | The selected color as a string. |
| opacity | [Integer](../reference_2.md#type-integer) | false | — | The selected opacity, from 0 (transparent) to 100 (opaque), or null if [ColorItem.supportsTransparency](#attr-coloritemsupportstransparency) is false or the [color picker](ColorPicker.md#class-colorpicker) selected a color while in [simple mode](../reference.md#type-colorpickermode). |

---
