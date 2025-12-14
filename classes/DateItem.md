# DateItem Documentation

[← Back to API Index](../reference.md)

---

## Class: DateItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
A [FormItem](FormItem.md#class-formitem) for editing [logical-Date](DateUtil.md#classmethod-dateutilcreatelogicaldate) values, where times are ignored.

The item renders with one of two appearances, depending on the value of [DateItem.useTextField](#attr-dateitemusetextfield) - when set to true, dates are edited directly [in a text field](#attr-dateitemtextfield), and formatted according to your locale and settings such as [DateItem.dateFormatter](#attr-dateitemdateformatter).

When set to false, the default appearance, the item uses separate selectors for [year](#attr-dateitemyearselector), [month](#attr-dateitemmonthselector) and [day](#attr-dateitemdayselector) values. To control which selectors are visible and in what order, use [DateItem.selectorFormat](#attr-dateitemselectorformat). In this mode, the selectable dates may be limited by the item's [start](#attr-dateitemstartdate) and [end](#attr-dateitemenddate) dates. See those two settings for more information.

In either mode, a [popup picker](DateChooser.md#class-datechooser) is provided assuming that the [pickerIcon](#attr-dateitemshowpickericon) is visible.

As noted, this item is for editing [logical-Date values](DateUtil.md#classmethod-dateutilcreatelogicaldate). To edit [logical-Time values](DateUtil.md#classmethod-dateutilcreatelogicaltime), see [TimeItem](TimeItem.md#class-timeitem), and to edit [datetime values](DateUtil.md#classmethod-dateutilcreatedatetime), see [DateTimeItem](DateTimeItem.md#class-datetimeitem). For [relative-date features](../reference_2.md#type-relativedatestring), see [RelativeDateItem](RelativeDateItem.md#class-relativedateitem).

For detailed information on working with dates, times and datetimes, see the [Date and Time Format and Storage overview](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage).

---
## ClassAttr: DateItem.MONTH_YEAR

### Description
A declared value of the enum type [DateItemSelectorFormat](../reference.md#type-dateitemselectorformat).

**Flags**: R

---
## ClassAttr: DateItem.YEAR_MONTH_DAY

### Description
A declared value of the enum type [DateItemSelectorFormat](../reference.md#type-dateitemselectorformat).

**Flags**: R

---
## ClassAttr: DateItem.DAY_MONTH

### Description
A declared value of the enum type [DateItemSelectorFormat](../reference.md#type-dateitemselectorformat).

**Flags**: R

---
## ClassAttr: DateItem.YEAR_MONTH

### Description
A declared value of the enum type [DateItemSelectorFormat](../reference.md#type-dateitemselectorformat).

**Flags**: R

---
## ClassAttr: DateItem.MONTH_DAY

### Description
A declared value of the enum type [DateItemSelectorFormat](../reference.md#type-dateitemselectorformat).

**Flags**: R

---
## ClassAttr: DateItem.MONTH_DAY_YEAR

### Description
A declared value of the enum type [DateItemSelectorFormat](../reference.md#type-dateitemselectorformat).

**Flags**: R

---
## ClassAttr: DateItem.DAY_MONTH_YEAR

### Description
A declared value of the enum type [DateItemSelectorFormat](../reference.md#type-dateitemselectorformat).

**Flags**: R

---
## Attr: DateItem.inputFormat

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is `true` this property can be used to specify the input format for date strings. If unset, the input format will be determined based on the specified [DateItem.dateFormatter](#attr-dateitemdateformatter) if possible (see [DateItem.getInputFormat](#method-dateitemgetinputformat)), otherwise picked up from the Date class (see [DateUtil.setInputFormat](DateUtil.md#classmethod-dateutilsetinputformat)).

Should be set to a standard [DateInputFormat](../reference.md#type-dateinputformat)

Note that the [DateInputFormat](../reference.md#type-dateinputformat) property is sufficient to parse date or datetime strings specified in most standard date formats. However should an entirely custom parsing function be required developers can implement a custom [DateItem.parseEditorValue](#method-dateitemparseeditorvalue) method.

This attribute does not have an effect if a native HTML5 date input is being used. See [DateItem.browserInputType](#attr-dateitembrowserinputtype).

### See Also

- [DateItem.displayFormat](#attr-dateitemdisplayformat)

**Flags**: IRW

---
## Attr: DateItem.monthSelector

### Description
[SelectItem](SelectItem.md#class-selectitem) for picking a month.

To control which selectors are visible and in what order, use [DateItem.selectorFormat](#attr-dateitemselectorformat).

### Groups

- dateItemAppearance

### See Also

- [DateItem.selectorFormat](#attr-dateitemselectorformat)

**Flags**: R

---
## Attr: DateItem.autoUseTextField

### Description
When set to true, the default, and when [useTextField](#attr-dateitemusetextfield) is set to false, such that the item displays multiple separate pickers, `useTextField` is automatically switched on when the item is rendering in a non-interactive way, such as when printing, or when [canEdit](FormItem.md#attr-formitemcanedit) is false and the read-only display-mode is [static](FormItem.md#attr-formitemreadonlydisplay).

### Groups

- basics

**Flags**: IR

---
## Attr: DateItem.useTextField

### Description
When set to true, the item uses a [single text field](#attr-dateitemtextfield) for working with the item's value.

When false or unset, the default, the item's value is represented by separate [day](#attr-dateitemdayselector), [month](#attr-dateitemmonthselector), and/or [year](#attr-dateitemyearselector) selectors. In this mode, null values are not supported, and a default value of Today will be enforced if no [defaultValue](FormItem.md#attr-formitemdefaultvalue) is specified. This means that a DateItem with `useTextField` set to false is effectively a [required](FormItem.md#attr-formitemrequired) field.

If you want to change the appearance of a DateItem, you will need to configure some autoChildren such as [DateItem.textField](#attr-dateitemtextfield) via [DateItem.textFieldProperties](#attr-dateitemtextfieldproperties), or in `useTextField:false` mode, the [DateItem.daySelector](#attr-dateitemdayselector) and other selectors, configured via `daySelectorProperties` et al.

### Groups

- basics

**Flags**: IR

---
## Attr: DateItem.dateFormatter

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is `true` this property can be used to customize the format in which dates are displayed for this item.  
Should be set to a standard [DateDisplayFormat](../reference.md#type-datedisplayformat).

As with any formItem rendering out a date value, if no explicit dateFormatter is supplied, dateFormatter will be derived from [DynamicForm.dateFormatter](DynamicForm.md#attr-dynamicformdateformatter) or [DynamicForm.datetimeFormatter](DynamicForm.md#attr-dynamicformdatetimeformatter), depending on the specified [FormItem.type](FormItem.md#attr-formitemtype) for this field, if set, otherwise from the standard default [DateUtil.setShortDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdisplayformat) or [DateUtil.setShortDatetimeDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdatetimedisplayformat).

NOTE: For entirely custom formats, developers may apply a custom [DateItem.formatEditorValue](#method-dateitemformateditorvalue) method. To ensure the DateItem is able to parse user-entered date strings back into Dates, for most cases developers can specify an explicit [DateItem.inputFormat](#attr-dateiteminputformat), or if necessary a custom [DateItem.parseEditorValue](#method-dateitemparseeditorvalue).

This attribute does not have an effect if a native HTML5 date or datetime input is being used. See [DateItem.browserInputType](#attr-dateitembrowserinputtype).

**Flags**: IRW

---
## Attr: DateItem.wrapHintText

### Description
If this item is showing a [FormItem.hint](FormItem.md#attr-formitemhint), should the hint text be allowed to wrap? Setting this property to `false` will render the hint on a single line without wrapping, expanding the width required to render the item if necessary.

If unset this property will be picked up from the [DynamicForm.wrapHintText](DynamicForm.md#attr-dynamicformwraphinttext) setting.

This setting does not apply to hints that are [shown in field](TextItem.md#attr-textitemshowhintinfield).

### See Also

- [FormItem.minHintWidth](FormItem.md#attr-formitemminhintwidth)

**Flags**: IR

---
## Attr: DateItem.showHintInField

### Description
If [useTextField](#attr-dateitemusetextfield) is true and a [hint](FormItem.md#attr-formitemhint) is set, should the hint be shown within the field?

Note that when using a native HTML5 date input (see [DateItem.browserInputType](#attr-dateitembrowserinputtype)), in-field hints are currently supported, but future browser changes might not allow in-field hints to be supported. Therefore, it is safest to _not_ use in-field hints in conjunction with a native HTML5 date input.

To change this attribute after being drawn, it is necessary to call [FormItem.redraw](FormItem.md#method-formitemredraw) or redraw the form.

### Groups

- appearance

### See Also

- [FormItem.hint](FormItem.md#attr-formitemhint)
- [DateItem.usePlaceholderForHint](#attr-dateitemuseplaceholderforhint)

**Flags**: IRW

---
## Attr: DateItem.pickerTimeItemProperties

### Description
A set of properties to apply to the [TimeItem](TimeItem.md#class-timeitem) displayed in the picker when [DateItem.showPickerTimeItem](#attr-dateitemshowpickertimeitem) is true.

Has no effect for fields of type `"date"`.

**Flags**: IRWA

---
## Attr: DateItem.textFieldProperties

### Description
Custom properties to apply to this dateItem's generated [DateItem.textField](#attr-dateitemtextfield). Only applies if [DateItem.useTextField](#attr-dateitemusetextfield) is true.

### Groups

- dateItemAppearance

**Flags**: IRA

---
## Attr: DateItem.browserInputType

### Description
If [useTextField](#attr-dateitemusetextfield) is true and browserInputType is set to "date", then a native [HTML5 date input](http://www.w3.org/TR/html5/forms.html#date-state-\(type=date\)) is used in place of a text input.

The use of a native HTML5 date input causes certain features to be disabled. Input masks, the picker icon, and a custom [dateFormatter](#attr-dateitemdateformatter) are not supported. [In-field hints](#attr-dateitemshowhintinfield) are currently supported, but future browser changes might force this support to be removed. Therefore, it is safest to _not_ use in-field hints (set showHintInField to false) in conjunction with a native HTML5 date input.

**NOTE:** For optimal appearance this feature requires specific CSS which may not be present in certain legacy skins.

**Flags**: IRA

---
## Attr: DateItem.invalidDateStringMessage

### Description
Validation error message to display if the user enters an invalid date

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: DateItem.daySelector

### Description
[SelectItem](SelectItem.md#class-selectitem) for picking a day of the month.

To control which selectors are visible and in what order, use [DateItem.selectorFormat](#attr-dateitemselectorformat).

### Groups

- dateItemAppearance

### See Also

- [DateItem.selectorFormat](#attr-dateitemselectorformat)

**Flags**: R

---
## Attr: DateItem.startDate

### Description
Minimum date the selectors will allow the user to pick. The default value is January 1st, 10 years before the current year.

**NOTE:** by design, setting `startDate` and `endDate` will not always prevent the user from picking invalid values. In particular:

*   the set of available days will only be restricted if the start and end dates fall within the same month
*   the set of available months will only be restricted if the start and end dates fall within the same year

This is **by design** as it allows the user to set the day, month and year in whatever order is convenient, rather than forcing them to pick in a specific order.

For actual enforcement of a date being in correct range before data is submitted, a [Validator](Validator.md#class-validator) of type "dateRange" should always be declared.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DateItem.textField

### Description
Text field to hold the entire date in "type in" format, if [useTextField](#attr-dateitemusetextfield) is true.

### Groups

- dateItemAppearance

**Flags**: R

---
## Attr: DateItem.defaultChooserDate

### Description
Default date to show in the date chooser. If this items value is currently unset, this property may be specified to set a default date to highlight in the dateChooser for this item. If unset, the date chooser will highlight the current date by default. Note that this has no effect if the item as a whole currently has a value - in that case the date chooser will always highlight the current value for the item.

**Flags**: IRW

---
## Attr: DateItem.use24HourTime

### Description
When showing the [DateChooser](DateChooser.md#class-datechooser) and the field is of type "datetime", whether the [time field](DateChooser.md#attr-datechoosershowtimeitem) should be set to use 24-hour time. The default is true.

Has no effect if [DateItem.showPickerTimeItem](#attr-dateitemshowpickertimeitem) is explicitly set to `false`.

**Flags**: IRW

---
## Attr: DateItem.usePlaceholderForHint

### Description
If [showing the hint in field](#attr-dateitemshowhintinfield) and if supported by the browser, should the HTML5 [`placeholder` attribute](http://www.whatwg.org/specs/web-apps/current-work/multipage/forms.html#attr-input-placeholder) be used to display the hint within the field? If set to `false`, then use of the `placeholder` attribute is disabled and an alternative technique to display the hint in-field is used instead.

The HTML5 `placeholder` attribute is supported in the following major browsers:

*   Chrome 4+
*   Firefox 4+
*   Internet Explorer 10+
*   Safari 5+
*   Opera 11.50+
*   Android 2.1+ `WebView` (used by the stock Browser app and when [packaging with PhoneGap](../kb_topics/phonegapIntegration.md#kb-topic-integration-with-phonegap))
*   Mobile Safari for iOS 3.2+

In browsers other than the above, in-field hints are implemented via a different technique.

Note that placeholder behavior is known to differ in Internet Explorer and certain old versions of the above browsers due to a recent change in the HTML5 specification regarding the `placeholder` attribute. Under the old rules, the placeholder is cleared when the element is focused. In the latest HTML5 spec as published by WHATWG, the placeholder is still displayed when the element is focused as long as the value is an empty string.

#### Styling the placeholder
While there isn't a standard way to style the placeholder text, Chrome, Firefox, Internet Explorer, and Safari provide vendor-prefixed pseudo-classes and/or pseudo-elements that can be used in CSS selectors:

| Browser | Pseudo-class or pseudo-element |
|---|---|
| Chrome, Safari | ::-webkit-input-placeholder |
| Firefox 4 - 18 | :-moz-placeholder |
| Firefox 19+ | ::-moz-placeholder |
| Internet Explorer | :-ms-input-placeholder |

Note that unlike other browsers, Firefox 19+ applies opacity:0.4 to the placeholder text. See [Bug 556145 - Placeholder text default style should use opacity instead of GrayText](https://bugzilla.mozilla.org/show_bug.cgi?id=556145)

Because browsers are required to ignore the entire rule if a selector is invalid, separate rules are needed for each browser. For example:

```
::-webkit-input-placeholder {
    color: blue;
    opacity: 1;
}
:-moz-placeholder {
    color: blue;
    opacity: 1;
}
::-moz-placeholder {
    color: blue;
    opacity: 1;
}
:-ms-input-placeholder {
    color: blue;
    opacity: 1;
}
```

If using [Sass](http://sass-lang.com), it may be useful to utilize Sass' [parent selector feature](http://sass-lang.com/documentation/file.SASS_REFERENCE.html#parent-selector). For example:

```
.myCustomItem,
.myCustomItemRTL,
.myCustomItemDisabled,
.myCustomItemDisabledRTL,
.myCustomItemError,
.myCustomItemErrorRTL,
.myCustomItemFocused,
.myCustomItemFocusedRTL,
.myCustomItemHint,
.myCustomItemHintRTL,
.myCustomItemDisabledHint,
.myCustomItemDisabledHintRTL {
    // ...

    &::-webkit-input-placeholder {
        color: blue;
        opacity: 1;
    }
    &:-moz-placeholder {
        color: blue;
        opacity: 1;
    }
    &::-moz-placeholder {
        color: blue;
        opacity: 1;
    }
    &:-ms-input-placeholder {
        color: blue;
        opacity: 1;
    }
}
```

If using [Compass](http://compass-style.org), the [`input-placeholder` mixin](http://compass-style.org/reference/compass/css3/user_interface/#mixin-input-placeholder) that was added in version 1.0 can further simplify the code to style the placeholder text For example:

```
.myCustomItem,
.myCustomItemRTL,
.myCustomItemDisabled,
.myCustomItemDisabledRTL,
.myCustomItemError,
.myCustomItemErrorRTL,
.myCustomItemFocused,
.myCustomItemFocusedRTL,
.myCustomItemHint,
.myCustomItemHintRTL,
.myCustomItemDisabledHint,
.myCustomItemDisabledHintRTL {
    // ...

    @include input-placeholder {
        color: blue;
        opacity: 1;
    }
}
```
#### Accessibility concerns
The HTML5 specification notes that a placeholder should not be used as a replacement for a title. The placeholder is intended to be a _short_ hint that assists the user who is entering a value into the empty field. The placeholder can be mistaken by some users for a pre-filled value, particularly in Internet Explorer because the same color is used, and the placeholder text color may provide insufficient contrast, particularly in Firefox 19+ because of the default 0.4 opacity. Furthermore, not having a title reduces the hit area available for setting focus on the item.

### Groups

- appearance

### See Also

- [FormItem.hint](FormItem.md#attr-formitemhint)

**Flags**: IRA

---
## Attr: DateItem.textAlign

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is `true` this property governs the alignment of text within the text field. Defaults to `"right"` by default or `"left"` if the page is in [rtl mode](Page.md#classmethod-pageisrtl).

This attribute does not have an effect if a native HTML5 date input is being used. See [DateItem.browserInputType](#attr-dateitembrowserinputtype).

### Groups

- appearance

**Flags**: IRW

---
## Attr: DateItem.showChooserFiscalYearPicker

### Description
When set to true, show a button that allows the calendar to be navigated by fiscal year.

**Flags**: IRW

---
## Attr: DateItem.itemTitleOrientation

### Description
When [useTextField](#attr-dateitemusetextfield) is false, the default orientation of titles for the [day](#attr-dateitemdayselector), [month](#attr-dateitemmonthselector) and [year](#attr-dateitemyearselector) selectors. [TitleOrientation](../reference.md#type-titleorientation) lists valid options.

Note that titles on the left or right take up a cell in tabular [form layouts](../kb_topics/formLayout.md#kb-topic-form-layout), but titles on top do not.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DateItem.endDate

### Description
Maximum date the selectors will allow the user to pick. The default value is December 31st, 5 years after the current year.

See [DateItem.startDate](#attr-dateitemstartdate) for details on how this restriction works.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DateItem.yearSelector

### Description
[SelectItem](SelectItem.md#class-selectitem) for picking a year.

To control which selectors are visible and in what order, use [DateItem.selectorFormat](#attr-dateitemselectorformat).

### Groups

- dateItemAppearance

### See Also

- [DateItem.selectorFormat](#attr-dateitemselectorformat)

**Flags**: R

---
## Attr: DateItem.enforceValueRange

### Description
Dictates whether values applied to this item via [setValue()](#method-dateitemsetvalue) or [form.values](DynamicForm.md#attr-dynamicformvalues) will be accepted if they fall outside the range specified by the item's [start](#attr-dateitemstartdate) and [end](#attr-dateitemenddate) dates.

When set to false, values outside the valid range will be accepted, which may result in additional entries being added to the various pickers, when [useTextField](#attr-dateitemusetextfield) is false.

When set to true, [FormItem.setValue](FormItem.md#method-formitemsetvalue) will return false for values that fall outside the range, the value will be rejected and the item defaulted to the start of its defined range. When this happens, [change()](FormItem.md#method-formitemchange) will not fire, the item will not show the [pending style](FormItem.md#attr-formitemshowpending), and [valuesHaveChanged()](DynamicForm.md#method-dynamicformvalueshavechanged) will return false, even though calling [saveData()](DynamicForm.md#method-dynamicformsavedata) will result in a changed record, if the [parent form](FormItem.md#attr-formitemform) is [data-bound](DynamicForm.md#attr-dynamicformdatasource) and the current record came from the dataSource.

This attribute does not have an effect if a native HTML5 date input is being used. See [DateItem.browserInputType](#attr-dateitembrowserinputtype).

### See Also

- [DateItem.startDate](#attr-dateitemstartdate)
- [DateItem.endDate](#attr-dateitemenddate)

**Flags**: IRWA

---
## Attr: DateItem.pickerDefaults

### Description
Defaults for the [DateChooser](DateChooser.md#class-datechooser) created by this form item. The picker for a particular item may be further customized via [DateItem.pickerProperties](#attr-dateitempickerproperties).

By default the following DateChooser properties are set:

*   border:"1px solid black"
*   showTodayButton:true
*   showCancelButton:true
*   autoHide:true
*   closeOnEscapeKeypress:true

These may be modified or overridden by the loaded skin. Note that as with any defaults block, modifications should be made using the the [Class.changeDefaults](Class.md#classmethod-classchangedefaults) to apply changes on top of existing settings.

**Flags**: IR

---
## Attr: DateItem.maskDateSeparator

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) and [DateItem.useMask](#attr-dateitemusemask) are both `true` this value is the separator between date components. If unset [DateUtil.getDefaultDateSeparator](DateUtil.md#classmethod-dateutilgetdefaultdateseparator) will be used.

### Groups

- basics

**Flags**: IA

---
## Attr: DateItem.showPickerTimeItem

### Description
If this field is of type `"datetime"`, when showing the [DateChooser](DateChooser.md#class-datechooser), should the [time field](DateChooser.md#attr-datechoosershowtimeitem) be displayed?

Has no effect for fields of type `"date"`.

This attribute does not have an effect if a native HTML5 date input is being used. See [DateItem.browserInputType](#attr-dateitembrowserinputtype).

**Flags**: IRW

---
## Attr: DateItem.yearSelectorProperties

### Description
Custom properties to apply to this dateItem's generated [DateItem.yearSelector](#attr-dateitemyearselector).

### Groups

- dateItemAppearance

**Flags**: IRA

---
## Attr: DateItem.monthSelectorProperties

### Description
Custom properties to apply to this dateItem's generated [DateItem.monthSelector](#attr-dateitemmonthselector).

### Groups

- dateItemAppearance

**Flags**: IRA

---
## Attr: DateItem.pickerIconPrompt

### Description
Prompt to show when the user hovers the mouse over the picker icon for this DateItem. May be overridden for localization of your application.

### Groups

- i18nMessages

**Flags**: IR

---
## Attr: DateItem.showChooserWeekPicker

### Description
When set to true, show a button that allows the calendar to be navigated by week or fiscal week, depending on the value of [DateItem.showChooserFiscalYearPicker](#attr-dateitemshowchooserfiscalyearpicker).

**Flags**: IRW

---
## Attr: DateItem.useMask

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is not `false` this property determines if an input mask should be used. The format of the mask is determined by the [DateItem.inputFormat](#attr-dateiteminputformat) or [DateItem.dateFormatter](#attr-dateitemdateformatter) (in that order).

This attribute does not have an effect if a native HTML5 date input is being used. See [DateItem.browserInputType](#attr-dateitembrowserinputtype).

### Groups

- basics

### See Also

- [DateItem.maskDateSeparator](#attr-dateitemmaskdateseparator)

**Flags**: IA

---
## Attr: DateItem.editProxyConstructor

### Description
Default class used to construct the [EditProxy](EditProxy.md#class-editproxy) for this component when the component is [first placed into edit mode](Canvas.md#method-canvasseteditmode).

**Flags**: IR

---
## Attr: DateItem.daySelectorProperties

### Description
Custom properties to apply to this dateItem's generated [DateItem.daySelector](#attr-dateitemdayselector).

### Groups

- dateItemAppearance

**Flags**: IRA

---
## Attr: DateItem.displayFormat

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is `true` this property can be used to customize the format in which dates are displayed.  
Should be set to a standard [DateDisplayFormat](../reference.md#type-datedisplayformat) or a function which will return a formatted date string.

If unset, the standard shortDate format as set up via [DateUtil.setShortDisplayFormat](DateUtil.md#classmethod-dateutilsetshortdisplayformat) will be used.

**NOTE: you may need to update the [inputFormat](#attr-dateiteminputformat) to ensure the DateItem is able to parse user-entered date strings back into Dates**

This attribute does not have an effect if a native HTML5 date input is being used. See [DateItem.browserInputType](#attr-dateitembrowserinputtype).

### See Also

- [DateItem.inputFormat](#attr-dateiteminputformat)

**Deprecated**

**Flags**: IRW

---
## Attr: DateItem.pickerConstructor

### Description
SmartClient class for the [FormItem.picker](FormItem.md#attr-formitempicker) autoChild displayed to allow the user to directly select dates.

**Flags**: IR

---
## Attr: DateItem.enforceDate

### Description
Can this field be set to a non-date value \[other than null\]?

When set to true, [FormItem.setValue](FormItem.md#method-formitemsetvalue) will return false without setting the item value and log a warning if passed something other than a valid date value. If the dateItem is showing a [free-form text entry field](#attr-dateitemusetextfield), and a user enters a text value which cannot be parsed into a valid date, the item will automatically redraw and display the [DateItem.invalidDateStringMessage](#attr-dateiteminvaliddatestringmessage) (though at this point calling [FormItem.getValue](FormItem.md#method-formitemgetvalue) will return the string entered by the user).

When set to false, a user may enter a value that is not a valid date (for example, "Not applicable") and the value will not immediately be flagged as an error. However note that for the value to actually pass validation you would need to declare the field as not of "date" type, for example:

```
     {name:"startDate", type:"dateOrOther", editorType:"DateItem", useTextField:true },
 
```
The type "dateOrOther" could be declared as a [SimpleType](SimpleType.md#class-simpletype), with validators that will accept either a valid date or certain special Strings (like "Not Available").

Only applies to dateItems where [DateItem.useTextField](#attr-dateitemusetextfield) is true. Non-Date values are never supported in items where useTextField is false.

This attribute does not have an effect if a native HTML5 date input is being used. See [DateItem.browserInputType](#attr-dateitembrowserinputtype).

**Flags**: IRWA

---
## Attr: DateItem.showItemTitles

### Description
When [useTextField](#attr-dateitemusetextfield) is false, whether titles should be shown for for child-items in this DateItem. By default, `showItemTitles` is false.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DateItem.selectorFormat

### Description
If showing date selectors rather than the date text field (so when `this.useTextField` is false), this property allows customization of the order of the day, month and year selector fields. If unset, these fields will match the specified [DateItem.inputFormat](#attr-dateiteminputformat) for this item, but note that the attribute default will likely be set by [localization](../kb_topics/i18n.md#kb-topic-internationalization-and-localization) to a valid [DateItemSelectorFormat](../reference.md#type-dateitemselectorformat).

Note: selectors may be omitted entirely by setting selectorFormat to (for example) `"MD"`. In this case the value for the omitted selector will match the [defaultValue](FormItem.md#attr-formitemdefaultvalue) specified for the item. For example, if the selector format is "MD" (month and day only), the year comes from the Date specified as the defaultValue.

### See Also

- [DateItem.daySelector](#attr-dateitemdayselector)
- [DateItem.monthSelector](#attr-dateitemmonthselector)
- [DateItem.yearSelector](#attr-dateitemyearselector)

**Flags**: IRW

---
## Attr: DateItem.itemTitleAlign

### Description
When [useTextField](#attr-dateitemusetextfield) is false, the default alignment of titles for the [day](#attr-dateitemdayselector), [month](#attr-dateitemmonthselector) and [year](#attr-dateitemyearselector) selectors, within their cells.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: DateItem.centuryThreshold

### Description
Only used if we're showing the date in a text field. When parsing a date, if the year is specified with 1 or 2 digits and is less than the centuryThreshold, then the year will be assumed to be 20xx; otherwise it will be interpreted according to default browser behavior, which will consider it to be 19xx.

By default, the _centuryThreshold_ is calculated as the current year + 25.

If you need to allow 1 and 2 digit years, set this attribute to `null` to have the control retain your year-value as entered.

### Groups

- appearance

**Flags**: IRW

---
## Attr: DateItem.pickerProperties

### Description
Properties for the [DateChooser](DateChooser.md#class-datechooser) created by this form item. If specified these will be applied on top of the [DateItem.pickerDefaults](#attr-dateitempickerdefaults)

**Flags**: IR

---
## Attr: DateItem.useSharedPicker

### Description
When set to true (the default), use a single shared date-picker across all widgets that use one. When false, create a new picker using the autoChild system. See [picker](#attr-dateitempickerdefaults) and [pickerProperties](#attr-dateitempickerproperties) for details on setting up an unshared picker.

**Flags**: IR

---
## Method: DateItem.setSelectionRange

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is true, falls through to standard [setSelectionRange()](TextItem.md#method-textitemsetselectionrange) implementation on this items freeform text entry field. Otherwise has no effect.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [int](../reference.md#type-int) | false | — | character index for start of new selection |
| end | [int](../reference.md#type-int) | false | — | character index for end of new selection |

---
## Method: DateItem.getEnteredValue

### Description
Returns the raw text value typed into this items text field if [DateItem.useTextField](#attr-dateitemusetextfield) is true (otherwise returns the result of this.getValue()).

### Returns

`[String](#type-string)` — value the user entered

---
## Method: DateItem.getFiscalCalendar

### Description
Returns the [FiscalCalendar](../reference.md#object-fiscalcalendar) object that will be used by this item's DateChooser.

### Returns

`[FiscalCalendar](#type-fiscalcalendar)` — the fiscal calendar for this chooser, if set, or the global one otherwise

---
## Method: DateItem.getInputFormat

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is `true` this method returns a standard [DateInputFormat](../reference.md#type-dateinputformat), determining how values entered by the user are to be converted to Javascript Date objects.

If an explicit [DateItem.inputFormat](#attr-dateiteminputformat) has been specified it will be returned, otherwise, if a custom [DateItem.dateFormatter](#attr-dateitemdateformatter) or [format](FormItem.md#attr-formitemformat) are specified, the input format will be automatically derived from that property.

Otherwise, the global [inputFormat](DateUtil.md#classmethod-dateutilsetinputformat) is used.

Note that the inputFormat will ignore any separator characters and padding of values. However if necessary entirely custom date formatting and parsing may be achieved via the [DateItem.formatEditorValue](#method-dateitemformateditorvalue) and [DateItem.parseEditorValue](#method-dateitemparseeditorvalue) methods.

### Returns

`[DateInputFormat](../reference.md#type-dateinputformat)` — expected format of date strings to parse

**Flags**: A

---
## Method: DateItem.getDefaultChooserDate

### Description
Returns the default date to display in the date chooser if this form items value is currently unset.

Default implementation returns [DateItem.defaultChooserDate](#attr-dateitemdefaultchooserdate)

### Returns

`[Date](#type-date)` — date to display, or null, indicating the current system date should be displayed.

---
## Method: DateItem.setFiscalCalendar

### Description
Sets the [FiscalCalendar](../reference.md#object-fiscalcalendar) object that will be used by this item's DateChooser. If unset, the [global fiscal calendar](DateUtil.md#classmethod-dateutilgetfiscalcalendar) is used.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| fiscalCalendar | [FiscalCalendar](#type-fiscalcalendar) | true | — | the fiscal calendar for this chooser, if set, or the global one otherwise |

---
## Method: DateItem.setEndDate

### Description
Setter for [DateItem.endDate](#attr-dateitemenddate).

**Note:** A [LogicalDate](DateUtil.md#classmethod-dateutilcreatelogicaldate) is expected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| endDate | [Date](#type-date)|[String](#type-string) | false | — | the new endDate. |

**Flags**: A

---
## Method: DateItem.parseEditorValue

### Description
Convert a text value entered in this item's text field to a final data value for storage.

If [DateItem.useTextField](#attr-dateitemusetextfield) is true, entirely custom date formatting and parsing logic may be applied via overrides to [DateItem.parseEditorValue](#method-dateitemparseeditorvalue) and [DateItem.formatEditorValue](#method-dateitemformateditorvalue). These methods apply to this FormItem only - system-wide Date and Datetime formatting and parsing may also be customized via the APIs on the [Date](../reference_2.md#object-date) class. See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more on this.

Note: custom parsing for this item may also be achieved by modifying the [DateItem.inputFormat](#attr-dateiteminputformat). This mechanism provides support many common date formats without the need for an entirely custom parser function.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [String](#type-string) | false | — | value as entered by the user |
| form | [DynamicForm](#type-dynamicform) | false | — | pointer to the dynamicForm containing this item |
| item | [FormItem](#type-formitem) | false | — | pointer to this item |

### Returns

`[Any](#type-any)` — Data value to store for this item.

**Flags**: A

---
## Method: DateItem.getSelectionRange

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is true, falls through to standard [getSelectionRange()](TextItem.md#method-textitemgetselectionrange) implementation on this items freeform text entry field. Otherwise has no effect.

### Returns

`[Array](#type-array)` — 2 element array indicating start/end character index of current selection within our text entry field. Returns null if this item is undrawn or doesn't have focus.

---
## Method: DateItem.setStartDate

### Description
Setter for [DateItem.startDate](#attr-dateitemstartdate).

**Note:** A [LogicalDate](DateUtil.md#classmethod-dateutilcreatelogicaldate) is expected.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| startDate | [Date](#type-date)|[String](#type-string) | false | — | the new startDate. |

**Flags**: A

---
## Method: DateItem.pendingStatusChanged

### Description
Notification method called when [showPending](FormItem.md#attr-formitemshowpending) is enabled and this date item should either clear or show its pending visual state.

The default behavior is that the [titleStyle](FormItem.md#attr-formitemtitlestyle) and [cellStyle](FormItem.md#attr-formitemcellstyle) are updated to include/exclude the "Pending" suffix. In addition, when displayed in the pending state:

*   If [useTextField](#attr-dateitemusetextfield) is `true`, then the "Pending" suffix will be appended to the [textBoxStyle](FormItem.md#attr-formitemtextboxstyle) applied to the [textField](#attr-dateitemtextfield); otherwise
*   (`useTextField` is `false`) the color of the [daySelector](#attr-dateitemdayselector), [monthSelector](#attr-dateitemmonthselector) and/or [yearSelector](#attr-dateitemyearselector) will change when the day, month, or year is different, respectively.

Returning `false` will cancel this default behavior.

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
## Method: DateItem.deselectValue

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is true, falls through to standard [deselectValue()](TextItem.md#method-textitemdeselectvalue) implementation on this items freeform text entry field. Otherwise has no effect.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [Boolean](#type-boolean) | true | — | If this parameter is passed, new cursor insertion position will be moved to the start, rather than the end of this item's value. |

---
## Method: DateItem.selectValue

### Description
If [DateItem.useTextField](#attr-dateitemusetextfield) is true, falls through to standard [selectValue()](TextItem.md#method-textitemselectvalue) implementation on this items freeform text entry field. Otherwise has no effect.

---
## Method: DateItem.formatEditorValue

### Description
Convert this item's data value to a text value for display in this item's text field.

If [DateItem.useTextField](#attr-dateitemusetextfield) is true, entirely custom date formatting and parsing logic may be applied via overrides to [DateItem.parseEditorValue](#method-dateitemparseeditorvalue) and [DateItem.formatEditorValue](#method-dateitemformateditorvalue). These methods apply to this FormItem only - system-wide Date and Datetime formatting and parsing may also be customized via the APIs on the [Date](../reference_2.md#object-date) class. See [dateFormatAndStorage](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage) for more on this.

Note: custom formatting for this item may also be achieved via the [DateItem.dateFormatter](#attr-dateitemdateformatter) which allows you to directly specify various standard date display formats.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| value | [Any](#type-any) | false | — | Underlying data value to format. May be null. |
| record | [ListGridRecord](#type-listgridrecord) | false | — | The record currently being edited by this form. Essentially the form's current values object. |
| form | [DynamicForm](#type-dynamicform) | false | — | pointer to the DynamicForm |
| item | [FormItem](#type-formitem) | false | — | pointer to the FormItem |

### Returns

`[String](#type-string)` — display value to show in the editor.

**Flags**: A

---
