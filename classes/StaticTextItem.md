# StaticTextItem Documentation

[← Back to API Index](../main.md)

---

## Class: StaticTextItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
A FormItem that displays an uneditable value.

---
## Attr: StaticTextItem.applyAlignToText

### Description
If the [textAlign](FormItem.md#attr-formitemtextalign) is unset, should the [align](FormItem.md#attr-formitemalign) setting, if set, be used for this `StaticTextItem`'s `textAlign`?

### Groups

- appearance

**Flags**: IRA

---
## Attr: StaticTextItem.canSelectText

### Description
Should the user be able to select the text in this item?

**Flags**: IRW

---
## Attr: StaticTextItem.wrap

### Description
If true, item contents can wrap. If false, all the contents should appear on a single line.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StaticTextItem.applyHeightToTextBox

### Description
If [FormItem.height](FormItem.md#attr-formitemheight) is specified, should it be applied to the item's text box element?

Overridden to be `false` for StaticTextItems by default.

See [shouldApplyHeightToTextBox()](FormItem.md#method-formitemshouldapplyheighttotextbox) for more information.

**Flags**: IRA

---
## Attr: StaticTextItem.defaultValue

### Description
Overridden to assign class-appropriate type.

### Groups

- basics

### See Also

- [FormItem.defaultValue](FormItem.md#attr-formitemdefaultvalue)

**Flags**: IRW

---
## Attr: StaticTextItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: StaticTextItem.clipValue

### Description
If true, text that exceeds the specified size of the form item will be clipped. Note that for horizontal clipping to occur, [StaticTextItem.wrap](#attr-statictextitemwrap) should be set to false - otherwise the text will typically wrap at the specified width. For vertical clipping to occur, [StaticTextItem.applyHeightToTextBox](#attr-statictextitemapplyheighttotextbox) should be explicitly set to `true` as the Text Box element is responsible for clipping the content.

### Groups

- appearance

**Flags**: IRW

---
## Attr: StaticTextItem.escapeHTML

### Description
By default HTML values in a staticTextItem will be interpreted by the browser. Setting this flag to true causes HTML characters to be escaped, meaning the raw value of the field (for example `"`<b>`AAA`</b>`"`) is displayed to the user rather than the interpreted HTML (for example `"**AAA**"`)

### Groups

- appearance

**Flags**: IRW

---
## Attr: StaticTextItem.outputAsHTML

### Description
By default HTML values in a staticTextItem will be interpreted by the browser. Setting this flag to true will causes HTML characters to be escaped, meaning the raw value of the field (for example `"`<b>`AAA`</b>`"`) is displayed to the user rather than the interpreted HTML (for example `"**AAA**"`)

### Groups

- appearance

**Deprecated**

**Flags**: IRW

---
## Attr: StaticTextItem.dateFormatter

### Description
Display format to use for date type values within this formItem.

Note that Fields of type `"date"`, `"datetime"` or `"time"` will be edited using a [DateItem](DateItem.md#class-dateitem) or [TimeItem](TimeItem.md#class-timeitem) by default, but this can be overridden - for `canEdit:false` fields, a [StaticTextItem](#class-statictextitem) is used by default, and the developer can always specify a custom [FormItem.editorType](FormItem.md#attr-formitemeditortype) as well as [data type](FormItem.md#attr-formitemtype).

The [FormItem.timeFormatter](FormItem.md#attr-formitemtimeformatter) may also be used to format underlying Date values as times (ommitting the date part entirely). If both `dateFormatter` and `timeFormatter` are specified on an item, for fields specified as [type "time"](FormItem.md#attr-formitemtype) the `timeFormatter` will be used, otherwise the `dateFormatter`

If `item.dateFormatter` and `item.timeFormatter` is unspecified, date display format may be defined at the component level via [DynamicForm.dateFormatter](DynamicForm.md#attr-dynamicformdateformatter), or for fields of type `"datetime"` [DynamicForm.datetimeFormatter](DynamicForm.md#attr-dynamicformdatetimeformatter). Otherwise for fields of type "date", default is to use the system-wide default short date format, configured via [DateUtil.setShortDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdisplayformat). For fields of type "datetime" or for Date values in fields whose type does not inherit from the logical "date" type, default is to use the system-wide normal date format configured via [DateUtil.setNormalDisplayFormat](DateUtil.md#classmethod-dateutilsetnormaldisplayformat) (using "toNormalDate()" on logical `"date"` type fields is not desirable as this would display the time component of the date object to the user).  
Specify any valid [DateDisplayFormat](../main.md#type-datedisplayformat) to change the format used by this item.

### Groups

- appearance

### See Also

- [FormItem.timeFormatter](FormItem.md#attr-formitemtimeformatter)

**Flags**: IRWA

---
## Attr: StaticTextItem.textBoxStyle

### Description
Base CSS class for this item

### Groups

- appearance

**Flags**: IRW

---
