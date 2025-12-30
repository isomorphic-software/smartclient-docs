# FormItemEventInfo Documentation

[← Back to API Index](../reference.md)

---

## Attr: FormItemEventInfo.overInlineError

### Description
True if the event occurred over the form's [single error item](DynamicForm.md#attr-dynamicformerroritemproperties).

**Flags**: R

---
## Attr: FormItemEventInfo.overTitle

### Description
True if the event occurred over the item's title.

**Flags**: R

---
## Attr: FormItemEventInfo.icon

### Description
If this event occurred over a formItemIcon this attribute contains the [FormItemIcon.name](FormItemIcon.md#attr-formitemiconname) for the icon.

**Flags**: IR

---
## Attr: FormItemEventInfo.item

### Description
Item over which the event occurred.

**Flags**: R

---
## Attr: FormItemEventInfo.overTextBox

### Description
True if the event occurred within the item's [textBox](FormItem.md#attr-formitemtextboxstyle).

**Flags**: R

---
## Attr: FormItemEventInfo.overElement

### Description
True if the event occurred over the item's data or input element. Note that it can be bad practice to implement custom context menus when overElement is true, since this will replace browser-default menus that users might expect.

**Flags**: R

---
## Attr: FormItemEventInfo.overItem

### Description
True if the event occurred over the main body of the item (for example the text-box), rather than over the title or within the form item's cell in the DynamicForm but outside the text box area.

**Flags**: R

---
