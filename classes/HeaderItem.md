# HeaderItem Documentation

[← Back to API Index](../reference.md)

---

## Class: HeaderItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
FormItem for showing a header within a DynamicForm.

Set the `defaultValue` of this item to the HTML you want to embed in the form.

---
## Attr: HeaderItem.colSpan

### Description
by default, headers span all remaining columns

### Groups

- appearance

**Flags**: IRW

---
## Attr: HeaderItem.showTitle

### Description
Don't show a separate title cell for headers

### Groups

- appearance

**Flags**: IRW

---
## Attr: HeaderItem.align

### Description
Alignment of this `HeaderItem` in its cell.

Note: Because a `HeaderItem` fills its cell by default, if the [applyAlignToText](#attr-headeritemapplyaligntotext) setting is changed to false, then the [textAlign](FormItem.md#attr-formitemtextalign) setting (rather than the `align` setting) of this `HeaderItem` should be used to control the alignment of the header text.

### Groups

- appearance

### See Also

- [FormItem.applyAlignToText](FormItem.md#attr-formitemapplyaligntotext)

**Flags**: IRW

---
## Attr: HeaderItem.defaultValue

### Description
Header text

### Groups

- appearance

**Flags**: IRW

---
## Attr: HeaderItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: HeaderItem.startRow

### Description
these items are in a row by themselves by default

### Groups

- appearance

**Flags**: IRW

---
## Attr: HeaderItem.canSelectText

### Description
Should the user be able to select the text in this item?

**Flags**: IRW

---
## Attr: HeaderItem.endRow

### Description
these items are in a row by themselves by default

### Groups

- appearance

**Flags**: IRW

---
## Attr: HeaderItem.textBoxStyle

### Description
Base CSS class for this item

### Groups

- appearance

**Flags**: IRW

---
## Attr: HeaderItem.applyAlignToText

### Description
If the [textAlign](FormItem.md#attr-formitemtextalign) is unset, should the [align](#attr-headeritemalign) setting, if set, be used for this `HeaderItem`'s `textAlign`?

### Groups

- appearance

**Flags**: IRA

---
