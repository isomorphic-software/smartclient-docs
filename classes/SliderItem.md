# SliderItem Documentation

[← Back to API Index](../reference.md)

---

## Class: SliderItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
FormItem that uses a [Slider](Slider.md#class-slider) component to present an interface for picking from either a continuous range or a range with a small number of discrete values.

---
## Attr: SliderItem.shouldSaveValue

### Description
Should this item's value be saved in the form's values and hence returned from [form.getValues()](DynamicForm.md#method-dynamicformgetvalues)?

`shouldSaveValue:false` is used to mark formItems which do not correspond to the underlying data model and should not save a value into the form's [values](DynamicForm.md#attr-dynamicformvalues). Example includes visual separators, password re-type fields, or checkboxes used to show/hide other form items.

A `shouldSaveValue:false` item should be given a value either via [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue) or by calling [form.setValue(item, value)](DynamicForm.md#method-dynamicformsetvalue) or [formItem.setValue(value)](FormItem.md#method-formitemsetvalue). Providing a value via [form.values](DynamicForm.md#attr-dynamicformvalues) or [form.setValues()](DynamicForm.md#method-dynamicformsetvalues) will automatically switch the item to `shouldSaveValue:true`.

Note that

*   if an item is shouldSaveValue true, but has no name, a warning is logged, and shouldSaveValue will be set to false.

### Groups

- formValues

**Flags**: IR

---
## Attr: SliderItem.vertical

### Description
Indicates whether this is a vertical or horizontal slider.

**Flags**: IR

---
## Attr: SliderItem.slider

### Description
This item is an autoChild generated [Canvas](Canvas.md#class-canvas) displayed by the SliderItem and is an instance of [Slider](Slider.md#class-slider) by default. It is customizable via the standard [AutoChild](../reference.md#type-autochild) pattern, by customizing [SliderItem.sliderProperties](#attr-slideritemsliderproperties) and [SliderItem.sliderConstructor](#attr-slideritemsliderconstructor).

**Flags**: R

---
## Attr: SliderItem.maxValue

### Description
The maximum slider value. The slider value is equal to maxValue when the thumb is at the top or right of the slider (unless flipValues is true, in which case the maximum value is at the bottom/left of the slider)

### See Also

- [Slider.flipValues](Slider.md#attr-sliderflipvalues)

**Flags**: IRW

---
## Attr: SliderItem.minValue

### Description
The minimum slider value. The slider value is equal to minValue when the thumb is at the bottom or left of the slider (unless flipValues is true, in which case the minimum value is at the top/right of the slider)

### See Also

- [Slider.flipValues](Slider.md#attr-sliderflipvalues)

**Flags**: IRW

---
## Attr: SliderItem.roundValues

### Description
Specifies whether the slider value should be rounded to the nearest integer. If set to false, values will be rounded to a fixed number of decimal places controlled by [SliderItem.roundPrecision](#attr-slideritemroundprecision).

**Flags**: IR

---
## Attr: SliderItem.sliderProperties

### Description
Properties to add to the automatically created [Slider](Slider.md#class-slider) used by this FormItem. See the [Slider](Slider.md#class-slider) class for reference.

**Flags**: IR

---
## Attr: SliderItem.width

### Description
Default width of this item.

### Groups

- appearance

**Flags**: IRW

---
## Attr: SliderItem.changeOnDrag

### Description
Should this sliderItem update its value and fire change handlers while the user is actively dragging the slider. Setting this attribute value to `false` will suppress any change notifications from the user dragging the slider thumb until the user releases the mouse at the final position. This can be useful to avoid repeatedly firing expensive operations such as server fetches while the user drags through a range of values.

**Flags**: IRW

---
## Attr: SliderItem.defaultValue

### Description
Default value for this sliderItems is 1.

**Flags**: IRW

---
## Attr: SliderItem.sliderConstructor

### Description
Constructor class for this item's [Slider](Slider.md#class-slider).

**Flags**: IR

---
## Attr: SliderItem.roundPrecision

### Description
If [Slider.roundValues](Slider.md#attr-sliderroundvalues) is false, the slider value will be rounded to this number of decimal places. If set to null the value will not be rounded

**Flags**: IR

---
## Attr: SliderItem.numValues

### Description
The number of discrete values represented by slider. If specified, the range of valid values (between `minValue` and `maxValue`) will be divided into this many steps. As the thumb is moved along the track it will only select these values and appear to jump between the steps.

**Flags**: IRW

---
## Method: SliderItem.setNumValues

### Description
Sets the [number of values](Slider.md#attr-slidernumvalues) for the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newNumValues | [Integer](../reference_2.md#type-integer) | false | — | the new number of values |

---
## Method: SliderItem.setMaxValue

### Description
Sets the [maximum value](Slider.md#attr-slidermaxvalue) of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [float](../reference.md#type-float) | false | — | the new maximum value |

---
## Method: SliderItem.pendingStatusChanged

### Description
Notification method called when [showPending](FormItem.md#attr-formitemshowpending) is enabled and this `SliderItem` should either clear or show its pending visual state.

The default behavior is that the [titleStyle](FormItem.md#attr-formitemtitlestyle) and [cellStyle](FormItem.md#attr-formitemcellstyle) are updated to include/exclude the "Pending" suffix. In addition, when displayed in the pending state the value label changes color. Returning `false` will cancel this default behavior.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| form | [DynamicForm](#type-dynamicform) | false | — | the managing `DynamicForm` instance. |
| item | [FormItem](#type-formitem) | false | — | the form item itself (also available as "this"). |
| pendingStatus | [boolean](../reference.md#type-boolean) | false | — | `true` if the item should show its pending visual state; `false` otherwise. |
| newValue | [Any](#type-any) | false | — | the current form item value. |
| value | [Any](#type-any) | false | — | the value that would be restored by a call to [DynamicForm.resetValues](DynamicForm.md#method-dynamicformresetvalues). |

### Returns

`[boolean](../reference.md#type-boolean)` — `false` to cancel the default behavior.

---
## Method: SliderItem.setMinValue

### Description
Sets the [minimum value](Slider.md#attr-sliderminvalue) of the slider

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [float](../reference.md#type-float) | false | — | the new minimum value |

---
