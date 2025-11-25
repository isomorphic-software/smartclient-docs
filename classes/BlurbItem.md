# BlurbItem Documentation

[← Back to API Index](../main.md)

---

## Class: BlurbItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
FormItem intended for inserting blurbs of instructional HTML into DynamicForms.

Set the `defaultValue` of this item to the HTML you want to embed in the form.

---
## Attr: BlurbItem.textBoxStyle

### Description
Base css style for this item.

### Groups

- appearance

**Flags**: IRW

---
## Attr: BlurbItem.clipValue

### Description
If true, text that exceeds the specified size of the form item will be clipped.

### Groups

- appearance

**Flags**: IRW

---
## Attr: BlurbItem.colSpan

### Description
By default, texts span all remaining columns

### Groups

- appearance

**Flags**: IRW

---
## Attr: BlurbItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: BlurbItem.canSelectText

### Description
Should the user be able to select the text in this item?

**Flags**: IRW

---
## Attr: BlurbItem.showTitle

### Description
Blurb items show no title by default.

### Groups

- appearance

**Flags**: IRW

---
## Attr: BlurbItem.wrap

### Description
If true, item contents can wrap. If false, all the contents should appear on a single line.

### Groups

- appearance

**Flags**: IRW

---
