# RadioGroupItem Documentation

[← Back to API Index](../reference.md)

---

## Class: RadioGroupItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
FormItem that shows a set of mutually exclusive options as a group of radio buttons.

---
## Attr: RadioGroupItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: RadioGroupItem.wrap

### Description
Should the text for items within this radio group wrap?

### Groups

- appearance

**Flags**: IRW

---
## Attr: RadioGroupItem.fillHorizontalSpace

### Description
If [RadioGroupItem.vertical](#attr-radiogroupitemvertical) is false, and this item has a specified width, should options be spread out evenly to fill the specified width?

### Groups

- appearance

**Flags**: IRW

---
## Attr: RadioGroupItem.allowEmptyValue

### Description
When set to true, allows a checked [RadioItem](../reference.md#class-radioitem) to be unchecked when clicked, clearing the value from the `RadioGroupItem`.

Note that this is not a default behavior of native radios and could impact compliance with accessibility standards depending on the application.

**Flags**: IRW

---
## Attr: RadioGroupItem.itemProperties

### Description
Map of properties to apply to generated items within this RadioGroup. This allows you to customize the generated radio items for this item.

**Flags**: IR

---
## Attr: RadioGroupItem.checkboxItemProperties

### Description
Properties to apply to the customized [CheckboxItem](CheckboxItem.md#class-checkboxitem) used for radioGroupItems when [useNativeRadioItems](#attr-radiogroupitemusenativeradioitems) is false.

### Groups

- appearance

**Flags**: IRW

---
## Attr: RadioGroupItem.disabledValues

### Description
This property allows you to specify an initial set of disabled options within this radioGroup. Once the RadioGroupItem has been created, [RadioGroupItem.setValueDisabled](#method-radiogroupitemsetvaluedisabled) should be used to enable and disable options.

**Flags**: I

---
## Attr: RadioGroupItem.textBoxStyle

### Description
Base CSS class applied to the text for items within this radio group.

### Groups

- appearance

**Flags**: IRW

---
## Attr: RadioGroupItem.useNativeRadioItems

### Description
When set to false, replaces each native radio element in the group with a [CheckboxItem](CheckboxItem.md#class-checkboxitem) which can be customized via [RadioGroupItem.checkboxItemProperties](#attr-radiogroupitemcheckboxitemproperties).

### Groups

- appearance

**Flags**: IRW

---
## Attr: RadioGroupItem.vertical

### Description
True == display options vertically, false == display in a single row

### Groups

- appearance

**Flags**: IRW

---
## Method: RadioGroupItem.valueHoverHTML

### Description
If defined, this method should return the HTML to display in a hover canvas when the user holds the mouse-pointer over one of the radio-items in this RadioGroupItem. Return null to suppress the hover canvas altogether.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | The sub-value (radio-item) to get the hoverHTML for |
| item | [RadioGroupItem](#type-radiogroupitem) | false | — | Pointer to this item |
| form | [DynamicForm](#type-dynamicform) | false | — | This item's form |

### Returns

`[HTMLString](../reference.md#type-htmlstring)` — HTML to be displayed in the hover

### Groups

- Hovers

**Flags**: A

---
## Method: RadioGroupItem.setValueDisabled

### Description
Disable or Enable a specific option within this radioGroup

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | value of option to disable |
| disabled | [boolean](../reference.md#type-boolean) | false | — | true to disable the option, false to enable it |

---
## Method: RadioGroupItem.setTextBoxStyle

### Description
Setter for [RadioGroupItem.textBoxStyle](#attr-radiogroupitemtextboxstyle).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newTextBoxStyle | [FormItemBaseStyle](../reference.md#type-formitembasestyle) | false | — | new `textBoxStyle`. |

---
## Method: RadioGroupItem.pendingStatusChanged

### Description
Notification method called when [showPending](FormItem.md#attr-formitemshowpending) is enabled and this radio group should either clear or show its pending visual state.

The default behavior is that the [titleStyle](FormItem.md#attr-formitemtitlestyle) and [cellStyle](FormItem.md#attr-formitemcellstyle) are updated to include/exclude the "Pending" suffix. In addition, the label for the newly-selected option will have a different color. Returning `false` will cancel this default behavior.

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
