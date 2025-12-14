# DateTimeItem Documentation

[← Back to API Index](../reference.md)

---

## Class: DateTimeItem

*Inherits from:* [DateItem](DateItem.md#class-dateitem)

### Description
A simple [DateItem subclass](DateItem.md#class-dateitem) for editing [regular datetime](DateUtil.md#classmethod-dateutilcreatedatetime) values, where date and time elements are relevant.

The item edits datetimes directly as text-values, formatted according to your locale and settings such as [DateItem.dateFormatter](DateItem.md#attr-dateitemdateformatter).

To edit [logical-Date values](DateUtil.md#classmethod-dateutilcreatelogicaldate), see [DateItem](DateItem.md#class-dateitem), and to edit [logical-time values](DateUtil.md#classmethod-dateutilcreatelogicaltime), see [TimeItem](TimeItem.md#class-timeitem). For [relative-date features](../reference_2.md#type-relativedatestring), see [RelativeDateItem](RelativeDateItem.md#class-relativedateitem).

For detailed information on working with dates, times and datetimes, see the [Date and Time Format and Storage overview](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage).

---
## Attr: DateTimeItem.displayFormat

### Description
This property can be used to customize the format in which datetimes are displayed.  
Should be set to a standard [DateDisplayFormat](../reference.md#type-datedisplayformat) or a function which will return a formatted date time string.

If unset, the standard shortDateTime format as set up in [DateUtil.setShortDatetimeDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdatetimedisplayformat) will be used.

**NOTE: you may need to update the [inputFormat](#attr-datetimeiteminputformat) to ensure the DateItem is able to parse user-entered date strings back into Dates**

### See Also

- [DateTimeItem.inputFormat](#attr-datetimeiteminputformat)

**Flags**: IRW

---
## Attr: DateTimeItem.browserInputType

### Description
If [useTextField](#attr-datetimeitemusetextfield) is true and browserInputType is set to "datetime", then a native [HTML5 local datetime input](http://www.w3.org/TR/html5/forms.html#local-date-and-time-state-\(type=datetime-local\)) is used in place of a text input.

The use of a native HTML5 datetime input causes certain features to be disabled. Input masks, the picker icon, and a custom [datetimeFormatter](DynamicForm.md#attr-dynamicformdatetimeformatter) are not supported. In-field hints are currently supported in Chrome/Chromium/Opera 15 and iOS 5.0+, but future browser changes might force this support to be removed. Therefore, it is safest to _not_ use in-field hints (set showHintInField to false) in conjunction with a native HTML5 datetime input. In-field hints are not supported in Opera 12 when using a native HTML5 datetime input. If in-field hints are not supported in the browser, then showHintInField has no effect and any hint will be shown to the side of the input.

**NOTES:**

*   This feature requires specific CSS changes. Currently these changes have been made to the Enterprise, EnterpriseBlue, and Graphite skins only.
*   In Chrome/Chromium/Opera 15 and Opera 12, native datetime inputs need to be made wider in order to fit the full datetime value within the native control. However, on iOS 5.0+, the normal width is fine. Be sure to test the layout of the form in all browsers that you wish to support.

**Flags**: IRA

---
## Attr: DateTimeItem.inputFormat

### Description
If [DateItem.useTextField](DateItem.md#attr-dateitemusetextfield) is `true` this property can be used to specify the input format for date strings. If unset, the input format will be determined based on the specified [DateItem.dateFormatter](DateItem.md#attr-dateitemdateformatter) if possible (see [DateItem.getInputFormat](DateItem.md#method-dateitemgetinputformat)), otherwise picked up from the Date class (see [DateUtil.setInputFormat](DateUtil.md#classmethod-dateutilsetinputformat)).

Should be set to a standard [DateInputFormat](../reference.md#type-dateinputformat)

Note that the [DateInputFormat](../reference.md#type-dateinputformat) property is sufficient to parse date or datetime strings specified in most standard date formats. However should an entirely custom parsing function be required developers can implement a custom [DateItem.parseEditorValue](DateItem.md#method-dateitemparseeditorvalue) method.

This attribute does not have an effect if a native HTML5 date input is being used. See [DateItem.browserInputType](DateItem.md#attr-dateitembrowserinputtype).

### See Also

- [DateItem.displayFormat](DateItem.md#attr-dateitemdisplayformat)

**Flags**: IRW

---
## Attr: DateTimeItem.useTextField

### Description
This property defaults to true in DateTimeItems and cannot be altered, since editing is via [formatted](#attr-datetimeitemdisplayformat) text-entry only.

### Groups

- basics

**Flags**: R

---
