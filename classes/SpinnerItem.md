# SpinnerItem Documentation

[← Back to API Index](../reference.md)

---

## Class: SpinnerItem

*Inherits from:* [TextItem](TextItem.md#class-textitem)

### Description
Item for picking a number. Includes arrow buttons to increase / decrease the value

---
## Attr: SpinnerItem.mask

### Description
Not applicable to a SpinnerItem.

**Flags**: IRWA

---
## Attr: SpinnerItem.decreaseIconProperties

### Description
FormItemIcon properties applied to the [decreaseIcon](#attr-spinneritemdecreaseicon) AutoChild of this SpinnerItem.

**Flags**: IR

---
## Attr: SpinnerItem.unstackedReadOnlyTextBoxStyle

### Description
—

### Groups

- appearance

**Flags**: IR

---
## Attr: SpinnerItem.defaultValue

### Description
Overridden to assign class-appropriate type.

### Groups

- basics

### See Also

- [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue)

**Flags**: IRW

---
## Attr: SpinnerItem.max

### Description
Maximum valid value for this item. If this and [min](#attr-spinneritemmin) are both null or unspecified, then [SpinnerItem.getNextValue](#method-spinneritemgetnextvalue) and [SpinnerItem.getPreviousValue](#method-spinneritemgetpreviousvalue) are used to increase or decrease the value and these methods are also used to determine the maximum value.

**Flags**: IRW

---
## Attr: SpinnerItem.step

### Description
How much should the value be incremented / decremented when the user hits the icons to increase / decrease the value?

When overriding [SpinnerItem.getNextValue](#method-spinneritemgetnextvalue) and/or [SpinnerItem.getPreviousValue](#method-spinneritemgetpreviousvalue), the sign of the step value determines whether these methods are expected to induce monotonically increasing or decreasing functions.

**Flags**: IRW

---
## Attr: SpinnerItem.maskOverwriteMode

### Description
Not applicable to a SpinnerItem.

**Flags**: IRWA

---
## Attr: SpinnerItem.unstackedPrintTextBoxStyle

### Description
In [unstacked mode](#attr-spinneritemwritestackedicons), the base CSS class name for the `SpinnerItem`'s text box element when printed. If unset, then [SpinnerItem.unstackedTextBoxStyle](#attr-spinneritemunstackedtextboxstyle) is used.

### Groups

- appearance

**Flags**: IR

---
## Attr: SpinnerItem.maskPromptChar

### Description
Not applicable to a SpinnerItem.

**Flags**: IRWA

---
## Attr: SpinnerItem.min

### Description
Minimum valid value for this item. If this and [max](#attr-spinneritemmax) are both null or unspecified, then [SpinnerItem.getNextValue](#method-spinneritemgetnextvalue) and [SpinnerItem.getPreviousValue](#method-spinneritemgetpreviousvalue) are used to increase or decrease the value and these methods are also used to determine the minimum value.

**Flags**: IRW

---
## Attr: SpinnerItem.increaseIcon

### Description
In [stacked mode](#attr-spinneritemwritestackedicons), the icon to increase the spinner's value (an up arrow by default). This icon is generated automatically using the [AutoChild](../reference.md#type-autochild) pattern. For skinning purposes, `increaseIconDefaults` may be modified using [changeDefaults()](Class.md#classmethod-classchangedefaults).

If sizes for the increase and decrease icons are not explicitly specified in their autoChild configuration, they will be derived from the specified [SpinnerItem.stackedIconsHeight](#attr-spinneritemstackediconsheight) and [SpinnerItem.stackedIconsWidth](#attr-spinneritemstackediconswidth) properties.

See the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for details on how to provide a sprited image for these icons.

**Flags**: R

---
## Attr: SpinnerItem.maskSaveLiterals

### Description
Not applicable to a SpinnerItem.

**Flags**: IRWA

---
## Attr: SpinnerItem.increaseIconProperties

### Description
FormItemIcon properties applied to the [increaseIcon](#attr-spinneritemincreaseicon) AutoChild of this SpinnerItem.

**Flags**: IR

---
## Attr: SpinnerItem.unstackedDecreaseIcon

### Description
In [unstacked mode](#attr-spinneritemwritestackedicons), the icon to decrease the `SpinnerItem`'s value.

By default, `"[SKIN]/DynamicForm/Spinner_decrease_icon.png"` is stretched to an 18x18 icon.

When [spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) is enabled, this property will not be used to locate an image, instead, the image is drawn via CSS based on the [FormItemIcon.baseStyle](FormItemIcon.md#attr-formitemiconbasestyle) property.

**Flags**: R

---
## Attr: SpinnerItem.maskPadChar

### Description
Not applicable to a SpinnerItem.

**Flags**: IRWA

---
## Attr: SpinnerItem.decreaseIcon

### Description
In [stacked mode](#attr-spinneritemwritestackedicons), the icon to decrease the spinner's value (a down arrow by default). This icon is generated automatically using the [AutoChild](../reference.md#type-autochild) pattern. For skinning purposes, `decreaseIconDefaults` may be modified using [changeDefaults()](Class.md#classmethod-classchangedefaults).

If sizes for the increase and decrease icons are not explicitly specified in their autoChild configuration, they will be derived from the specified [SpinnerItem.stackedIconsHeight](#attr-spinneritemstackediconsheight) and [SpinnerItem.stackedIconsWidth](#attr-spinneritemstackediconswidth) properties.

See the [skinning overview](../kb_topics/skinning.md#kb-topic-skinning--theming) for details on how to provide a sprited image for these icons.

**Flags**: R

---
## Attr: SpinnerItem.unstackedIncreaseIcon

### Description
In [unstacked mode](#attr-spinneritemwritestackedicons), the icon to increase the `SpinnerItem`'s value.

By default, `"[SKIN]/DynamicForm/Spinner_increase_icon.png"` is stretched to an 18x18 icon.

When [spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) is enabled, this property will not be used to locate an image, instead, the image is drawn via CSS based on the [FormItemIcon.baseStyle](FormItemIcon.md#attr-formitemiconbasestyle) property.

**Flags**: R

---
## Attr: SpinnerItem.unstackedTextBoxStyle

### Description
In [unstacked mode](#attr-spinneritemwritestackedicons), the base CSS class name for the `SpinnerItem`'s text box element.

NOTE: See the [CompoundFormItem_skinning](../reference.md#kb-topic-compoundformitem_skinning) discussion for special skinning considerations.

### Groups

- appearance

**Flags**: IR

---
## Attr: SpinnerItem.writeStackedIcons

### Description
When set to `true`, the increase and decrease icons are stacked on top of each other, also called stacked mode. When `false`, the increase and decrease icons are placed on the same line as the `SpinnerItem`'s text box, also called unstacked mode. When `null`, a default setting depending on [Browser.isTouch](Browser.md#classattr-browseristouch) is used (for touch browsers, the default is `false`/unstacked mode).

In stacked mode, [SpinnerItem.increaseIcon](#attr-spinneritemincreaseicon) and [SpinnerItem.decreaseIcon](#attr-spinneritemdecreaseicon) control the appearance of the stacked icons.

In unstacked mode, [SpinnerItem.unstackedIncreaseIcon](#attr-spinneritemunstackedincreaseicon) and [SpinnerItem.unstackedDecreaseIcon](#attr-spinneritemunstackeddecreaseicon) control the appearance of the unstacked icons.

### Groups

- appearance

**Flags**: IR

---
## Attr: SpinnerItem.stackedIconsHeight

### Description
In [stacked icons mode](#attr-spinneritemwritestackedicons) this property can be used to specify the height of both the increase and decrease icon. Since the icons are stacked vertically, each icon will be sized to half this specified value. If a height property is explicitly set for the icon via [SpinnerItem.increaseIconProperties](#attr-spinneritemincreaseiconproperties), [SpinnerItem.decreaseIconProperties](#attr-spinneritemdecreaseiconproperties), or related `Defaults` property blocks, that will take precedence over any specified stackedIconsHeight.

See also [SpinnerItem.stackedIconsWidth](#attr-spinneritemstackediconswidth).

**Flags**: IR

---
## Attr: SpinnerItem.stackedIconsWidth

### Description
In [stacked icons mode](#attr-spinneritemwritestackedicons) this property can be used to specify the width of both the increase and decrease icon. If a width property is explicitly set for the icon via [SpinnerItem.increaseIconProperties](#attr-spinneritemincreaseiconproperties), [SpinnerItem.decreaseIconProperties](#attr-spinneritemdecreaseiconproperties), or related `Defaults` property blocks, that will take precedence over any specified stackedIconsWidth.

See also [SpinnerItem.stackedIconsHeight](#attr-spinneritemstackediconsheight).

**Flags**: IR

---
## Method: SpinnerItem.getPreviousValue

### Description
When [min](#attr-spinneritemmin) and [max](#attr-spinneritemmax) are both null or unspecified, this method is called to get the previous lower value from the currentValue. The default implementation returns (currentValue **+** step) because the step parameter is based on _the opposite_ of [this.step](#attr-spinneritemstep).

To indicate that the given currentValue is the minimum value, return currentValue again.

Implementations should expect to be passed any value for currentValue. Also, if [SpinnerItem.step](#attr-spinneritemstep) is non-negative, getPreviousValue() must induce a [monotonically decreasing (non-increasing) function](http://en.wikipedia.org/wiki/Monotonic_function); otherwise, getPreviousValue() must induce a monotonically increasing function.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| currentValue | [number](#type-number) | false | — | the current value of this SpinnerItem |
| step | [number](#type-number) | false | — | a suggested step value based on the opposite of [this.step](#attr-spinneritemstep) and how long the user has been continuously decreasing the value. |

### Returns

`[number](#type-number)` — the next higher value

### See Also

- [SpinnerItem.getNextValue](#method-spinneritemgetnextvalue)

**Flags**: A

---
## Method: SpinnerItem.getNextValue

### Description
When [min](#attr-spinneritemmin) and [max](#attr-spinneritemmax) are both null or unspecified, this method is called to get the next higher value from the currentValue. The default implementation returns (currentValue + step).

To indicate that the given currentValue is the maximum value, return currentValue again.

Implementations should expect to be passed any value for currentValue. Also, if [SpinnerItem.step](#attr-spinneritemstep) is non-negative, getNextValue() must induce a [monotonically increasing (non-decreasing) function](http://en.wikipedia.org/wiki/Monotonic_function); otherwise, getNextValue() must induce a monotonically decreasing function.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| currentValue | [number](#type-number) | false | — | the current value of this SpinnerItem |
| step | [number](#type-number) | false | — | a suggested step value based on [this.step](#attr-spinneritemstep) and how long the user has been continuously increasing the value. |

### Returns

`[number](#type-number)` — the next higher value

### See Also

- [SpinnerItem.getPreviousValue](#method-spinneritemgetpreviousvalue)

**Flags**: A

---
