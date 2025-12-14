# CheckboxItem Documentation

[← Back to API Index](../reference.md)

---

## Class: CheckboxItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
Checkbox form item, implemented with customizable checkbox images.

---
## Attr: CheckboxItem.checkedDescription

### Description
The description shown in a hover when [FormItem.showOldValueInHover](FormItem.md#attr-formitemshowoldvalueinhover) is enabled and a value represents the checked state.

### Groups

- i18nMessages

**Flags**: IRA

---
## Attr: CheckboxItem.checkedImage

### Description
URL for the image to display when this checkbox is selected, or checked.

This image is implemented using the [valueIcons subsystem](FormItem.md#attr-formitemvalueicons), and may be modified via the standard valueIcons properties such as [CheckboxItem.valueIconWidth](#attr-checkboxitemvalueiconwidth)

Note that this is the base image name - if [CheckboxItem.showValueIconOver](#attr-checkboxitemshowvalueiconover) et al are set, the state (`"Over"`, `"Down"` and `"Disabled"`) will be added to this name as the user interacts with the checkbox, as well as the image extension

The special value "blank" means that no image will be shown.

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string. Alternatively developers can omit this property and instead use CSS directly in the [CheckboxItem.booleanBaseStyle](#attr-checkboxitembooleanbasestyle) property to provide a "checked" appearance.

### Groups

- appearance

### See Also

- [CheckboxItem.printCheckedImage](#attr-checkboxitemprintcheckedimage)

**Flags**: IRW

---
## Attr: CheckboxItem.printBooleanBaseStyle

### Description
If set, the [booleanBaseStyle](#attr-checkboxitembooleanbasestyle) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- printing

### See Also

- [CheckboxItem.booleanBaseStyle](#attr-checkboxitembooleanbasestyle)

**Flags**: IRA

---
## Attr: CheckboxItem.showValueIconOver

### Description
Should an "Over" state icon be shown when the user rolls over this checkbox

### Groups

- valueIcons

**Flags**: IRWA

---
## Attr: CheckboxItem.printUnsetImage

### Description
If set, the [CheckboxItem.unsetImage](#attr-checkboxitemunsetimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- printing

### See Also

- [CheckboxItem.unsetImage](#attr-checkboxitemunsetimage)

**Flags**: IRW

---
## Attr: CheckboxItem.valueIconWidth

### Description
Width of the checkbox image.

### Groups

- valueIcons

**Flags**: IRW

---
## Attr: CheckboxItem.showNullAsTrue

### Description
Should a null value be shown as checked (i.e. true)?

**Flags**: IRW

---
## Attr: CheckboxItem.showLabel

### Description
Should we show the label text next to the checkbox item.

**Flags**: IRW

---
## Attr: CheckboxItem.uncheckedImage

### Description
URL for the image to display when this checkbox is not selected, or unchecked.

The special value "blank" means that no image will be shown.

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string. Alternatively developers can omit this property and instead use CSS directly in the [CheckboxItem.booleanBaseStyle](#attr-checkboxitembooleanbasestyle) property to provide an "unchecked" appearance.

### Groups

- appearance

### See Also

- [CheckboxItem.printUncheckedImage](#attr-checkboxitemprintuncheckedimage)

**Flags**: IRW

---
## Attr: CheckboxItem.partialSelectedImage

### Description
URL for the image to display when this checkbox is partially selected.

The special value "blank" means that no image will be shown.

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string. Alternatively developers can omit this property and instead use CSS directly in the [CheckboxItem.booleanBaseStyle](#attr-checkboxitembooleanbasestyle) property to provide a "partially checked" appearance.

### Groups

- appearance

### See Also

- [CheckboxItem.printPartialSelectedImage](#attr-checkboxitemprintpartialselectedimage)

**Flags**: IRW

---
## Attr: CheckboxItem.booleanBaseStyle

### Description
An optional base CSS style to apply to the checkbox image. If supplied, the base style is suffixed with "True", "False", "Partial", or "Unset" if the checkbox is selected, unselected, partially selected, or unset. The style is then suffixed with the state of the value icon ("", "Over", "Down", "Disabled").

### See Also

- [CheckboxItem.printBooleanBaseStyle](#attr-checkboxitemprintbooleanbasestyle)

**Flags**: IRA

---
## Attr: CheckboxItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: CheckboxItem.showUnsetImage

### Description
Determines what image to display when the value for this checkbox is unset. Set to true to display the [CheckboxItem.unsetImage](#attr-checkboxitemunsetimage) for null values, or false to use the [CheckboxItem.uncheckedImage](#attr-checkboxitemuncheckedimage) for both null and explicitly unchecked values.

If this attribute is not set, the [CheckboxItem.unsetImage](#attr-checkboxitemunsetimage) for null values if [CheckboxItem.allowEmptyValue](#attr-checkboxitemallowemptyvalue) is true for this item, otherwise the unchecked image will be used.

**Flags**: IRA

---
## Attr: CheckboxItem.printCheckedImage

### Description
If set, the [CheckboxItem.checkedImage](#attr-checkboxitemcheckedimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- printing

### See Also

- [CheckboxItem.checkedImage](#attr-checkboxitemcheckedimage)

**Flags**: IRW

---
## Attr: CheckboxItem.titleStyle

### Description
Base CSS class for this item's title cell.

**Note:** This styling applies to the standard form item title cell for this item - it does not apply to item's [label](#attr-checkboxitemshowlabel). To modify the styling for that text, use [CheckboxItem.textBoxStyle](#attr-checkboxitemtextboxstyle) instead.

### Groups

- appearance

**Flags**: IRW

---
## Attr: CheckboxItem.printPartialSelectedImage

### Description
If set, the [CheckboxItem.partialSelectedImage](#attr-checkboxitempartialselectedimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- printing

### See Also

- [CheckboxItem.partialSelectedImage](#attr-checkboxitempartialselectedimage)

**Flags**: IRW

---
## Attr: CheckboxItem.sizeToCheckboxImage

### Description
If this checkbox item is [not showing a label](#attr-checkboxitemshowlabel), should it ignore any specified [FormItem.width](FormItem.md#attr-formitemwidth) and instead size to fit its [checkbox icon](#attr-checkboxitemcheckedimage)?

When set to true (the default), the checkbox item ignores any specified width, ensuring that it does not impact the the containing DynamicForm's table geometry unnecessarily.

**Flags**: IRWA

---
## Attr: CheckboxItem.unsetImage

### Description
URL for the image to display when this checkbox is unset. Note that if [CheckboxItem.showUnsetImage](#attr-checkboxitemshowunsetimage) is false or [CheckboxItem.allowEmptyValue](#attr-checkboxitemallowemptyvalue) is false the [CheckboxItem.uncheckedImage](#attr-checkboxitemuncheckedimage) will be used for null values rather than this image.

The special value "blank" means that no image will be shown.

[Spriting](../kb_topics/skinning.md#kb-topic-skinning--theming) can be used for this image, by setting this property to a [SCSpriteConfig](../reference.md#type-scspriteconfig) formatted string. Alternatively developers can omit this property and instead use CSS directly in the [CheckboxItem.booleanBaseStyle](#attr-checkboxitembooleanbasestyle) property to provide an "unset" appearance.

### Groups

- appearance

**Flags**: IRW

---
## Attr: CheckboxItem.partialSelectedDescription

### Description
The description shown in a hover when [FormItem.showOldValueInHover](FormItem.md#attr-formitemshowoldvalueinhover) is enabled and a value represents the partial selected state.

### Groups

- i18nMessages

**Flags**: IRA

---
## Attr: CheckboxItem.allowEmptyValue

### Description
By default checkboxes allow the user to toggle between true and false values only. Setting this property to true will allow the user to toggle between three values - `true`, `false` and unset.

**Flags**: IRW

---
## Attr: CheckboxItem.valueMap

### Description
Object defining how the checkbox "checked" state will be mapped to the field value.  
Checkboxes only support 2 states. By default a checked checkbox will have value `true`, and an unchecked one will have value `false` (or `null` if there is no default value and the value has never been set).

A valueMap can modify this in 2 ways:  
\- If the desired checked/unchecked values can be resolved to `true` and `false` directly in JavaScript, the valueMap may be specified as a 2-element array containing these values. Examples of this would include  
  `[0,1]`: In this case an unchecked checkbox would have value `0` and a checked box would have value `1`  
  `[null,"Some String"]`: In this case an unchecked checkbox would have value `null` and a checked box would have value `"Some String"`  
\- More arbitrary data values can be resolved to checked / unchecked values via an object mapping the arbitrary data values to display values of `true` and `false`. For example:  
  `{"A":false, "B":true}`  
In this case an unchecked checkbox would have value "A", and a checked box would have value "B"

Note: ValueMaps in other formats will be ignored by the CheckboxItem class. To update the valueMap at runtime, always use [CheckboxItem.setValueMap](#method-checkboxitemsetvaluemap)

### Groups

- valueMap

**Flags**: IRW

---
## Attr: CheckboxItem.textBoxStyle

### Description
Base CSS class for this item's title text

### Groups

- appearance

**Flags**: IRW

---
## Attr: CheckboxItem.showValueIconDisabled

### Description
Should a "Disabled" state icon be shown when the item is disabled

### Groups

- valueIcons

**Flags**: IRWA

---
## Attr: CheckboxItem.showValueIconDown

### Description
Should a "Down" state icon be shown when the mouse goes down over this checkbox

### Groups

- valueIcons

**Flags**: IRWA

---
## Attr: CheckboxItem.uncheckedDescription

### Description
The description shown in a hover when [FormItem.showOldValueInHover](FormItem.md#attr-formitemshowoldvalueinhover) is enabled and a value represents the unchecked state.

### Groups

- i18nMessages

**Flags**: IRA

---
## Attr: CheckboxItem.valueIconHeight

### Description
Height of the checkbox image.

### Groups

- valueIcons

**Flags**: IRW

---
## Attr: CheckboxItem.labelAsTitle

### Description
By default a checkboxItem sets [CheckboxItem.showTitle](#attr-checkboxitemshowtitle):true, and so takes up two cells with the default [TitleOrientation](../reference.md#type-titleorientation) of "left" (see [form layout\\n overview](../kb_topics/formLayout.md#kb-topic-form-layout)). However, the title cell is left blank by default, and the title specified by [FormItem.title](FormItem.md#attr-formitemtitle) is shown inside the formItem's cell instead, in an element called the "label".

To instead show the title in it's original location, set `labelAsTitle:true`. You can also set [CheckboxItem.showLabel](#attr-checkboxitemshowlabel):false to suppress the label and/or title altogether.

**Flags**: IRW

---
## Attr: CheckboxItem.width

### Description
Width for the CheckboxItem, including both checkbox image and [label](#attr-checkboxitemshowlabel). Note that if [CheckboxItem.showLabel](#attr-checkboxitemshowlabel) is false, this property will have no effect - the item will render at the size required to contain the icon.

### See Also

- [formLayout](../kb_topics/formLayout.md#kb-topic-form-layout)

**Flags**: IRW

---
## Attr: CheckboxItem.unsetDescription

### Description
The description shown in a hover when [FormItem.showOldValueInHover](FormItem.md#attr-formitemshowoldvalueinhover) is enabled and a value represents the unset state.

### Groups

- i18nMessages

**Flags**: IRA

---
## Attr: CheckboxItem.printUncheckedImage

### Description
If set, the [CheckboxItem.uncheckedImage](#attr-checkboxitemuncheckedimage) to use when [printing](../kb_topics/printing.md#kb-topic-printing).

### Groups

- printing

### See Also

- [CheckboxItem.uncheckedImage](#attr-checkboxitemuncheckedimage)

**Flags**: IRW

---
## Attr: CheckboxItem.showTitle

### Description
CheckboxItem has special behavior for titles, see [CheckboxItem.labelAsTitle](#attr-checkboxitemlabelastitle).

**Flags**: IR

---
## Attr: CheckboxItem.showNullAsTrueIf

### Description
Set this property to the name of another field in the same record, to have this field be shown as checked (i.e. true) if this field is null and the other field is not null. For example, you could use this to show a "US Citizen" field as true if a value is entered into another field "US Social Security Number"

**Flags**: IRW

---
## Method: CheckboxItem.setValueMap

### Description
Setter method to apply a valueMap to a checkbox item.  
Note that if this method is overridden, the override must call `this.Super("setValueMap", arguments);` to maintain functionality in this class.

### Groups

- valueMap

### See Also

- [CheckboxItem.valueMap](#attr-checkboxitemvaluemap)

---
## Method: CheckboxItem.getValueAsBoolean

### Description
Return the value tracked by this form item as a Boolean. If the value is not already a boolean, or is unset and [CheckboxItem.allowEmptyValue](#attr-checkboxitemallowemptyvalue) is true, then null will be returned.

### Returns

`[Boolean](#type-boolean)` — value of this element

### See Also

- [FormItem.getValue](FormItem.md#method-formitemgetvalue)

---
## Method: CheckboxItem.pendingStatusChanged

### Description
Notification method called when [showPending](FormItem.md#attr-formitemshowpending) is enabled and this checkbox item should either clear or show its pending visual state.

The default behavior is that the [cellStyle](FormItem.md#attr-formitemcellstyle) and checkbox label style are updated to include/exclude the "Pending" suffix. Returning `false` will cancel this default behavior.

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
