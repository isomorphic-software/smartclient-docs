# RichTextItem Documentation

[← Back to API Index](../reference.md)

---

## Class: RichTextItem

*Inherits from:* [CanvasItem](CanvasItem.md#class-canvasitem)

### Description
FormItem for rich text (HTML) editing. Makes use of a [RichTextEditor](RichTextEditor.md#class-richtexteditor) as the editing interface.

---
## Attr: RichTextItem.shouldSaveValue

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
## Attr: RichTextItem.showTitle

### Description
Don't show the title for rich text items by default

**Flags**: IR

---
## Attr: RichTextItem.defaultValue

### Description
Overridden to assign class-appropriate type.

### Groups

- basics

### See Also

- [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue)

**Flags**: IRW

---
## Attr: RichTextItem.startRow

### Description
By default RichTextItems take up an entire row

**Flags**: IRW

---
## Attr: RichTextItem.endRow

### Description
By default RichTextItems take up an entire row

**Flags**: IRW

---
## Attr: RichTextItem.controlGroups

### Description
[RichTextEditor.controlGroups](RichTextEditor.md#attr-richtexteditorcontrolgroups) to display for this editor. Each controlGroup should be a property set either on this item or on the RichTextEditor prototype and should be set to an array of [ControlName](../reference.md#type-controlname)s.

**Flags**: IA

---
## Attr: RichTextItem.colSpan

### Description
By default RichTextItems take up an entire row

**Flags**: IRW

---
## Attr: RichTextItem.moveFocusOnTab

### Description
If the user presses the "Tab" key, should focus be taken from this editor? If set to `false` a "Tab" keypress will cause a Tab character to be inserted into the text, and focus will be left in the edit area.

**Flags**: IRW

---
## Method: RichTextItem.setMoveFocusOnTab

### Description
Setter for [RichTextItem.moveFocusOnTab](#attr-richtextitemmovefocusontab).

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| moveFocusOnTab | [boolean](../reference.md#type-boolean) | false | — | new value for moveFocusOnTab |

---
