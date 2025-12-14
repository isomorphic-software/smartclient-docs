# TimeItem Documentation

[← Back to API Index](../reference.md)

---

## Class: TimeItem

*Inherits from:* [FormItem](FormItem.md#class-formitem)

### Description
A [FormItem](FormItem.md#class-formitem) for editing [logical-time](DateUtil.md#classmethod-dateutilcreatelogicaltime) values, which are Date instances where only the time-portion is relevant.

The item renders with one of two appearances, depending on the value of [TimeItem.useTextField](#attr-timeitemusetextfield) - when set to true, the default appearance, times are edited directly as text-values. In this mode, values are formatted according to [TimeItem.timeFormatter](#attr-timeitemtimeformatter), with defaults coming from [TimeItem.timeFormatter24Hour](#attr-timeitemtimeformatter24hour) and [TimeItem.timeFormatter12Hour](#attr-timeitemtimeformatter12hour), depending on the value of [use24HourTime](#attr-timeitemuse24hourtime). See also [Time.setNormalDisplayFormat](Time.md#classmethod-timesetnormaldisplayformat) for system-wide settings.

TimeItem automatically accepts both 12 and 24 hour time as well as partial times and a variety of possible time value separators. Examples:

```
		11:34:45 AM	=> 11:34:45
		1:3:5 AM	=> 01:30:50
		1:3p		=> 13:30:00
		11 34 am	=> 11:34:00
		11-34		=> 11:34:00
		113445		=> 11:34:45
		13445		=> 01:34:45
		1134		=> 11:34:00
		134			=> 01:34:00
 
```

When `useTextField` is set to false, the item provides separate pickers for [hour](#attr-timeitemhouritem), [minute](#attr-timeitemminuteitem) and [second](#attr-timeitemseconditem) values. By default, the pickers edit times in [24-hour format](#attr-timeitemuse24hourtime), meaning the `hourItem` shows values from 0-23. When [use24HourTime](#attr-timeitemuse24hourtime) is set to false, the `hourItem` is limited to a range of 1-12, and the [am/pm picker](#attr-timeitemampmitem) is displayed. Note that [getValue()](FormItem.md#method-formitemgetvalue) always returns a Date instance that represents a [logical-time](DateUtil.md#classmethod-dateutilcreatelogicaltime) in 24-hour format.

Values entered by the user are stored as JavaScript `Date` objects in local time. The day, month and year values of this `Date` object are not relevant and should be ignored.

By default, when used in a [SearchForm](SearchForm.md#class-searchform) or as a field in a [ListGrid](ListGrid_1.md#class-listgrid)'s [filter editor](ListGrid_1.md#attr-listgridshowfiltereditor), TimeItems will automatically generate AdvancedCriteria - for example, entering "11:00" into the item will generate a [betweenInclusive](../reference.md#type-operatorid) Criterion that selects all times between 11:00:00 and 11:59:59. If the form is databound and the DataSource is marked as being [allowAdvancedCriteria](DataSource.md#attr-datasourceallowadvancedcriteria):false, the criteria generated will be simple, checking for data with logical time values equal to the displayed value.

To edit [logical-Date values](DateUtil.md#classmethod-dateutilcreatelogicaldate), see [DateItem](DateItem.md#class-dateitem), and to edit [datetime values](DateUtil.md#classmethod-dateutilcreatedatetime), see [DateTimeItem](DateTimeItem.md#class-datetimeitem). For [relative-date features](../reference_2.md#type-relativedatestring), see [RelativeDateItem](RelativeDateItem.md#class-relativedateitem).

For detailed information on working with dates, times and datetimes, see the [Date and Time Format and Storage overview](../kb_topics/dateFormatAndStorage.md#kb-topic-date-and-time-format-and-storage).

---
## Attr: TimeItem.millisecondIncrement

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [millisecondValues](#attr-timeitemmillisecondvalues) is unset, this attribute specifies the increment to use when generating entries for the millisecond picker. For example, if this attribute is set to 5, the millisecond picker will contain only every fifth value between the [millisecondMinValue](#attr-timeitemmillisecondminvalue) and [millisecondMaxValue](#attr-timeitemmillisecondmaxvalue).

**Flags**: IRW

---
## Attr: TimeItem.hourMinValue

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [hourValues](#attr-timeitemhourvalues) is unset, this attribute specifies the minimum value present in the hour picker.

Used for specifying a limited set of valid Hour values, or when using the TimeItem to record duration, rather than time per-se. The default is zero in all cases.

See also [hourMaxValue](#attr-timeitemhourmaxvalue) and [hourIncrement](#attr-timeitemhourincrement).

**Flags**: IRW

---
## Attr: TimeItem.secondIncrement

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [secondValues](#attr-timeitemsecondvalues) is unset, this attribute specifies the increment to use when generating entries for the second picker. For example, if this attribute is set to 5, the second picker will contain only every fifth value between the [secondMinValue](#attr-timeitemsecondminvalue) and [secondMaxValue](#attr-timeitemsecondmaxvalue).

**Flags**: IRW

---
## Attr: TimeItem.ampmItem

### Description
Select item to hold the AM/PM value for the timeItem when [useTextField](#attr-timeitemusetextfield) is false.

**Flags**: R

---
## Attr: TimeItem.hourItemPrompt

### Description
The hover prompt to show for the [hour picker](#attr-timeitemhouritem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.showMillisecondItem

### Description
Controls whether to display the [TimeItem.millisecondItem](#attr-timeitemmilliseconditem) when [TimeItem.useTextField](#attr-timeitemusetextfield) is false.

**Flags**: IRW

---
## Attr: TimeItem.minuteItemProperties

### Description
Custom properties to apply to this timeItem's generated [minute picker](#attr-timeitemminuteitem).

**Flags**: IRA

---
## Attr: TimeItem.hourValues

### Description
An array of values to make available in the [hour picker](#attr-timeitemhouritem) when [useTextField](#attr-timeitemusetextfield) is false.

Used for specifying a limited set of valid Hour values, or when using the TimeItem to record duration, rather than time per-se.

See [hourMinValue](#attr-timeitemhourminvalue), [hourMaxValue](#attr-timeitemhourmaxvalue) and [hourIncrement](#attr-timeitemhourincrement) for another method of controlling the content in the hour picker.

**Flags**: IRW

---
## Attr: TimeItem.textBoxStyle

### Description
Base CSS class for this item's text box. If specified this style will be applied to the [TimeItem.textField](#attr-timeitemtextfield) if [TimeItem.useTextField](#attr-timeitemusetextfield) is set to `true`.

**Flags**: IRW

---
## Attr: TimeItem.itemTitleAlign

### Description
When [useTextField](#attr-timeitemusetextfield) is false, the default title-alignment of child-items such as the [hour](#attr-timeitemhouritem), [minute](#attr-timeitemminuteitem) and [second](#attr-timeitemseconditem) pickers, within their cells.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: TimeItem.secondMaxValue

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [secondValues](#attr-timeitemsecondvalues) is unset, this attribute specifies the maximum value present in the second picker.

Used for specifying a limited set of valid Second values, or when using the TimeItem to record duration, rather than time per-se. The default is 59.

See also [secondMinValue](#attr-timeitemsecondminvalue) and [secondIncrement](#attr-timeitemsecondincrement).

**Flags**: IRW

---
## Attr: TimeItem.ampmItemProperties

### Description
Custom properties to apply to this timeItem's generated [AM/PM picker](#attr-timeitemampmitem).

**Flags**: IRA

---
## Attr: TimeItem.showSecondItem

### Description
Controls whether to display the [TimeItem.secondItem](#attr-timeitemseconditem) when [TimeItem.useTextField](#attr-timeitemusetextfield) is false.

**Flags**: IRW

---
## Attr: TimeItem.millisecondItemPrompt

### Description
The hover prompt to show for the [millisecond picker](#attr-timeitemmilliseconditem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.textFieldProperties

### Description
Custom properties to apply to the [text field](#attr-timeitemtextfield) generated for this timeItem when [useTextField](#attr-timeitemusetextfield) is true.

**Flags**: IRA

---
## Attr: TimeItem.showMinuteItem

### Description
Controls whether to display the [TimeItem.minuteItem](#attr-timeitemminuteitem) when [TimeItem.useTextField](#attr-timeitemusetextfield) is false.

**Flags**: IRW

---
## Attr: TimeItem.textAlign

### Description
If [TimeItem.useTextField](#attr-timeitemusetextfield) is `true`, this property governs the alignment of text within the text field. Defaults to `"left"` by default or `"right"` if the page is in [rtl mode](Page.md#classmethod-pageisrtl).

This attribute does not have an effect if a native HTML5 time input is being used. See [TimeItem.browserInputType](#attr-timeitembrowserinputtype).

**Flags**: IRW

---
## Attr: TimeItem.secondMinValue

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [secondValues](#attr-timeitemsecondvalues) is unset, this attribute specifies the minimum value present in the second picker.

Used for specifying a limited set of valid Second values, or when using the TimeItem to record duration, rather than time per-se. The default is zero in all cases.

See also [secondMaxValue](#attr-timeitemsecondmaxvalue) and [secondIncrement](#attr-timeitemsecondincrement).

**Flags**: IRW

---
## Attr: TimeItem.minuteItemTitle

### Description
Title to show for the [minute picker](#attr-timeitemminuteitem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.useTextField

### Description
Should we show the time in a text field, or as a number of SelectItems?

**Flags**: IR

---
## Attr: TimeItem.secondItem

### Description
Select item to hold the seconds portion of the time or [duration](#method-timeitemgetduration) when [useTextField](#attr-timeitemusetextfield) is false.

**Flags**: R

---
## Attr: TimeItem.timeFormatter

### Description
If [TimeItem.useTextField](#attr-timeitemusetextfield) is true, what format should this item's time string be presented in?

If unset, the default formatter will be [TimeItem.timeFormatter24Hour](#attr-timeitemtimeformatter24hour) or [TimeItem.timeFormatter12Hour](#attr-timeitemtimeformatter12hour) depending on the value of [TimeItem.use24HourTime](#attr-timeitemuse24hourtime). If the property cannot be derived in this way (none of these properties are set), we'll check [DynamicForm.timeFormatter](DynamicForm.md#attr-dynamicformtimeformatter), or finally back off to the standard system-wide [Time.displayFormat](Time.md#classattr-timedisplayformat) will be applied.

This attribute does not have an effect if a native HTML5 time input is being used. See [TimeItem.browserInputType](#attr-timeitembrowserinputtype).

**Flags**: IRW

---
## Attr: TimeItem.timeFormatter24Hour

### Description
If [TimeItem.useTextField](#attr-timeitemusetextfield) is true, and [TimeItem.use24HourTime](#attr-timeitemuse24hourtime) is true, what format should this item's time string be presented in?

May be overridden via an explicitly specified [TimeItem.timeFormatter](#attr-timeitemtimeformatter).

This attribute does not have an effect if a native HTML5 time input is being used. See [TimeItem.browserInputType](#attr-timeitembrowserinputtype).

**Flags**: IRW

---
## Attr: TimeItem.hourItemProperties

### Description
Custom properties to apply to this timeItem's generated [hour picker](#attr-timeitemhouritem).

**Flags**: IRA

---
## Attr: TimeItem.textField

### Description
Text field to hold the entire time in "type in" format, if [useTextField](#attr-timeitemusetextfield) is true.

**Flags**: R

---
## Attr: TimeItem.millisecondItemTitle

### Description
Title to show for the [millisecond picker](#attr-timeitemmilliseconditem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.wrapHintText

### Description
If this item is showing a [FormItem.hint](FormItem.md#attr-formitemhint), should the hint text be allowed to wrap? Setting this property to `false` will render the hint on a single line without wrapping, expanding the width required to render the item if necessary.

If unset this property will be picked up from the [DynamicForm.wrapHintText](DynamicForm.md#attr-dynamicformwraphinttext) setting.

This setting does not apply to hints that are [shown in field](TextItem.md#attr-textitemshowhintinfield).

### See Also

- [FormItem.minHintWidth](FormItem.md#attr-formitemminhintwidth)

**Flags**: IR

---
## Attr: TimeItem.itemTitleOrientation

### Description
When [useTextField](#attr-timeitemusetextfield) is false, the default orientation of titles for child-items, such as the [hour](#attr-timeitemhouritem), [minute](#attr-timeitemminuteitem) and [second](#attr-timeitemseconditem) pickers. [TitleOrientation](../reference.md#type-titleorientation) lists valid options.

Note that titles on the left or right take up a cell in tabular [form layouts](../kb_topics/formLayout.md#kb-topic-form-layout), but titles on top do not.

### Groups

- formTitles

**Flags**: IRW

---
## Attr: TimeItem.useMask

### Description
If true, a data entry mask will be enabled in the field based on the [TimeItem.timeFormatter](#attr-timeitemtimeformatter).

Note that if a non-padded [TimeItem.timeFormatter](#attr-timeitemtimeformatter) is specified, it will be changed to the corresponding padded version (ex. "toShort24HourTime" will be changed to "toShortPadded24HourTime").

This attribute does not have an effect if a native HTML5 time input is being used. See [TimeItem.browserInputType](#attr-timeitembrowserinputtype).

**Flags**: IRA

---
## Attr: TimeItem.timeFormatter12Hour

### Description
If [TimeItem.useTextField](#attr-timeitemusetextfield) is true, and [TimeItem.use24HourTime](#attr-timeitemuse24hourtime) is false, what format should this item's time string be presented in?

May be overridden via an explicitly specified [TimeItem.timeFormatter](#attr-timeitemtimeformatter).

This attribute does not have an effect if a native HTML5 time input is being used. See [TimeItem.browserInputType](#attr-timeitembrowserinputtype).

**Flags**: IRW

---
## Attr: TimeItem.secondItemProperties

### Description
Custom properties to apply to this timeItem's generated [seconds picker](#attr-timeitemseconditem).

**Flags**: IRA

---
## Attr: TimeItem.use24HourTime

### Description
Whether to enforce 24-hour time in the UI. If unset, assumes to the [global default](Time.md#classattr-timeuse24hourtime).

**Flags**: IRW

---
## Attr: TimeItem.millisecondValues

### Description
An array of values to make available in the [millisecond picker](#attr-timeitemmilliseconditem) when [useTextField](#attr-timeitemusetextfield) is false.

Used for specifying a limited set of valid Millisecond values, or when using the TimeItem to record duration, rather than time per-se.

See [millisecondMinValue](#attr-timeitemmillisecondminvalue), [millisecondMaxValue](#attr-timeitemmillisecondmaxvalue) and [millisecondIncrement](#attr-timeitemmillisecondincrement) for another method of controlling the content in the millisecond picker.

**Flags**: IRW

---
## Attr: TimeItem.showHourItem

### Description
Controls whether to display the [TimeItem.hourItem](#attr-timeitemhouritem) when [TimeItem.useTextField](#attr-timeitemusetextfield) is false.

**Flags**: IRW

---
## Attr: TimeItem.secondItemTitle

### Description
Title to show for the [second picker](#attr-timeitemseconditem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.displayFormat

### Description
What format should this item's time string be presented in?

This attribute does not have an effect if a native HTML5 time input is being used. See [TimeItem.browserInputType](#attr-timeitembrowserinputtype).

**Deprecated**

**Flags**: IRW

---
## Attr: TimeItem.showHintInField

### Description
If [useTextField](#attr-timeitemusetextfield) is true and a [hint](FormItem.md#attr-formitemhint) is set, should the hint be shown within the field?

Note that when using a native HTML5 time input (see [TimeItem.browserInputType](#attr-timeitembrowserinputtype)), in-field hints are currently supported, but future browser changes might not allow in-field hints to be supported. Therefore, it is safest to _not_ use in-field hints in conjunction with a native HTML5 time input.

To change this attribute after being drawn, it is necessary to call [FormItem.redraw](FormItem.md#method-formitemredraw) or redraw the form.

### Groups

- appearance

### See Also

- [FormItem.hint](FormItem.md#attr-formitemhint)
- [TimeItem.usePlaceholderForHint](#attr-timeitemuseplaceholderforhint)

**Flags**: IRW

---
## Attr: TimeItem.secondValues

### Description
An array of values to make available in the [second picker](#attr-timeitemseconditem) when [useTextField](#attr-timeitemusetextfield) is false.

Used for specifying a limited set of valid Second values, or when using the TimeItem to record duration, rather than time per-se.

See [secondMinValue](#attr-timeitemsecondminvalue), [secondMaxValue](#attr-timeitemsecondmaxvalue) and [secondIncrement](#attr-timeitemsecondincrement) for another method of controlling the content in the second picker.

**Flags**: IRW

---
## Attr: TimeItem.hourIncrement

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [hourValues](#attr-timeitemhourvalues) is unset, this attribute specifies the increment to use when generating entries for the hour picker. For example, if this attribute is set to 5, the hour picker will contain only every fifth value between the [hourMinValue](#attr-timeitemhourminvalue) and [hourMaxValue](#attr-timeitemhourmaxvalue).

**Flags**: IRW

---
## Attr: TimeItem.millisecondMaxValue

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [millisecondValues](#attr-timeitemmillisecondvalues) is unset, this attribute specifies the maximum value present in the millisecond picker.

Used for specifying a limited set of valid Millisecond values, or when using the TimeItem to record duration, rather than time per-se. The default is 999.

See also [millisecondMinValue](#attr-timeitemmillisecondminvalue) and [millisecondIncrement](#attr-timeitemmillisecondincrement).

**Flags**: IRW

---
## Attr: TimeItem.ampmItemTitle

### Description
Title to show for the [AM/PM picker](#attr-timeitemampmitem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.minuteIncrement

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [minuteValues](#attr-timeitemminutevalues) is unset, this attribute specifies the increment to use when generating entries for the minute picker. For example, if this attribute is set to 5, the minute picker will contain only every fifth value between the [minuteMinValue](#attr-timeitemminuteminvalue) and [minuteMaxValue](#attr-timeitemminutemaxvalue).

**Flags**: IRW

---
## Attr: TimeItem.minuteItemPrompt

### Description
The hover prompt to show for the [minute picker](#attr-timeitemminuteitem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.minuteMinValue

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [minuteValues](#attr-timeitemminutevalues) is unset, this attribute specifies the minimum value present in the minute picker.

Used for specifying a limited set of valid Minute values, or when using the TimeItem to record duration, rather than time per-se. The default is zero in all cases.

See also [minuteMaxValue](#attr-timeitemminutemaxvalue) and [minuteIncrement](#attr-timeitemminuteincrement).

**Flags**: IRW

---
## Attr: TimeItem.millisecondMinValue

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [millisecondValues](#attr-timeitemmillisecondvalues) is unset, this attribute specifies the minimum value present in the millisecond picker.

Used for specifying a limited set of valid Millisecond values, or when using the TimeItem to record duration, rather than time per-se. The default is zero in all cases.

See also [millisecondMaxValue](#attr-timeitemmillisecondmaxvalue) and [millisecondIncrement](#attr-timeitemmillisecondincrement).

**Flags**: IRW

---
## Attr: TimeItem.millisecondItemProperties

### Description
Custom properties to apply to this timeItem's generated [millisecond picker](#attr-timeitemmilliseconditem).

**Flags**: IRA

---
## Attr: TimeItem.millisecondItem

### Description
Select item to hold the milliseconds portion of the time or [duration](#method-timeitemgetduration) when [useTextField](#attr-timeitemusetextfield) is false.

**Flags**: R

---
## Attr: TimeItem.showItemTitles

### Description
When [useTextField](#attr-timeitemusetextfield) is false, whether titles should be shown for for child-items in this TimeItem. By default, `showItemTitles` is true, and titles are displayed [above the items](FormItem.md#attr-formitemtitleorientation).

### Groups

- formTitles

**Flags**: IRW

---
## Attr: TimeItem.hourMaxValue

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [hourValues](#attr-timeitemhourvalues) is unset, this attribute specifies the maximum value present in the hour picker.

Used for specifying a limited set of valid Hour values, or when using the TimeItem to record duration, rather than time per-se. The default is 11 or 23, according to the value of [use24HourTime](#attr-timeitemuse24hourtime) and [timeFormatter](#attr-timeitemtimeformatter).

See also [hourMinValue](#attr-timeitemhourminvalue) and [hourIncrement](#attr-timeitemhourincrement).

**Flags**: IRW

---
## Attr: TimeItem.invalidTimeStringMessage

### Description
Validation error message to display if the user enters an invalid time string.

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.usePlaceholderForHint

### Description
If [showing the hint in field](#attr-timeitemshowhintinfield) and if supported by the browser, should the HTML5 [`placeholder` attribute](http://www.whatwg.org/specs/web-apps/current-work/multipage/forms.html#attr-input-placeholder) be used to display the hint within the field? If set to `false`, then use of the `placeholder` attribute is disabled and an alternative technique to display the hint in-field is used instead.

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
## Attr: TimeItem.minuteMaxValue

### Description
When [useTextField](#attr-timeitemusetextfield) is false and [minuteValues](#attr-timeitemminutevalues) is unset, this attribute specifies the maximum value present in the minute picker.

Used for specifying a limited set of valid Minute values, or when using the TimeItem to record duration, rather than time per-se. The default 59.

See also [minuteMinValue](#attr-timeitemminuteminvalue) and [minuteIncrement](#attr-timeitemminuteincrement).

**Flags**: IRW

---
## Attr: TimeItem.secondItemPrompt

### Description
The hover prompt to show for the [second picker](#attr-timeitemseconditem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.browserInputType

### Description
If [useTextField](#attr-timeitemusetextfield) is true and browserInputType is set to "time", then a native [HTML5 time input](http://www.w3.org/TR/html5/forms.html#time-state-\(type=time\)) is used in place of a text input.

The use of a native HTML5 time input causes certain features to be disabled. Input masks and a custom [timeFormatter](#attr-timeitemtimeformatter) are not supported. [In-field hints](#attr-timeitemshowhintinfield) are currently supported, but future browser changes might force this support to be removed. Therefore, it is safest to _not_ use in-field hints (set showHintInField to false) in conjunction with a native HTML5 time input.

**NOTE:** This feature requires specific CSS changes. Currently these changes have been made to the Enterprise, EnterpriseBlue, and Graphite skins only.

**Flags**: IRA

---
## Attr: TimeItem.minuteItem

### Description
Select item to hold the minutes portion of the time or [duration](#method-timeitemgetduration) when [useTextField](#attr-timeitemusetextfield) is false.

**Flags**: R

---
## Attr: TimeItem.minuteValues

### Description
An array of values to make available in the [minute picker](#attr-timeitemminuteitem) when [useTextField](#attr-timeitemusetextfield) is false.

Used for specifying a limited set of valid Minute values, or when using the TimeItem to record duration, rather than time per-se.

See [minuteMinValue](#attr-timeitemminuteminvalue), [minuteMaxValue](#attr-timeitemminutemaxvalue) and [minuteIncrement](#attr-timeitemminuteincrement) for another method of controlling the content in the minute picker.

**Flags**: IRW

---
## Attr: TimeItem.hourItemTitle

### Description
Title to show for the [hour picker](#attr-timeitemhouritem).

### Groups

- i18nMessages

**Flags**: IRW

---
## Attr: TimeItem.hourItem

### Description
Select item to hold the hours portion of the time or [duration](#method-timeitemgetduration) when [useTextField](#attr-timeitemusetextfield) is false.

**Flags**: R

---
## Method: TimeItem.setSelectionRange

### Description
If [TimeItem.useTextField](#attr-timeitemusetextfield) is true, falls through to standard [setSelectionRange](TextItem.md#method-textitemsetselectionrange) implementation on this items freeform text entry field. Otherwise has no effect.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [int](../reference.md#type-int) | false | — | character index for start of new selection |
| end | [int](../reference.md#type-int) | false | — | character index for end of new selection |

---
## Method: TimeItem.setValue

### Description
Set the value of the form item to the value passed in

NOTE: for valueMap'd items, newValue should be data value not displayed value

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| newValue | [Any](#type-any) | false | — | value to set the element to |

---
## Method: TimeItem.getDuration

### Description
When [useTextField](#attr-timeitemusetextfield) is set to false, this method returns the value of the time expressed as a duration in the [timeUnit](../reference_2.md#type-timeunit) provided. If no timeUnit is passed, the default is the smallest unit for which a picker is visible.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| timeUnit | [TimeUnit](../reference_2.md#type-timeunit) | true | — | the unit of the return value |

### Returns

`[int](../reference.md#type-int)` — the item's value, expressed as a duration in the TimeUnit passed

**Flags**: A

---
## Method: TimeItem.getMillisecondValues

### Description
Returns an array of the current valid millisecond values, whether set directly as [TimeItem.millisecondValues](#attr-timeitemmillisecondvalues) or generated according to [millisecondMinValue](#attr-timeitemmillisecondminvalue), [millisecondMaxValue](#attr-timeitemmillisecondmaxvalue) and [millisecondIncrement](#attr-timeitemmillisecondincrement).

### Returns

`[Array of Number](#type-array-of-number)` — array of available Millisecond values

**Flags**: A

---
## Method: TimeItem.setMinutes

### Description
Set the minute value of this TimeItem. If the item value has not been initialized with [setValue()](#method-timeitemsetvalue), the hour will be established to current hour.

You can use [setValue()](#method-timeitemsetvalue) to set both hours and minutes at the same time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| minutes | [Number](#type-number) | false | — | new minutes value for this TimeItem. |

**Flags**: A

---
## Method: TimeItem.pendingStatusChanged

### Description
Notification method called when [showPending](FormItem.md#attr-formitemshowpending) is enabled and this time item should either clear or show its pending visual state.

The default behavior is that the [titleStyle](FormItem.md#attr-formitemtitlestyle) and [cellStyle](FormItem.md#attr-formitemcellstyle) are updated to include/exclude the "Pending" suffix. In addition, when displayed in the pending state:

*   If [useTextField](#attr-timeitemusetextfield) is `true`, then the "Pending" suffix will be appended to the [textBoxStyle](FormItem.md#attr-formitemtextboxstyle) applied to the [textField](#attr-timeitemtextfield); otherwise
*   (`useTextField` is `false`) the color of the [hourItem](#attr-timeitemhouritem), [minuteItem](#attr-timeitemminuteitem), [secondItem](#attr-timeitemseconditem), [millisecondItem](#attr-timeitemmilliseconditem), and/or [ampmItem](#attr-timeitemampmitem) will change when the hour, minute, second, millisecond, or whether the time is AM or PM is different, respectively.

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
## Method: TimeItem.setMinuteValues

### Description
Sets the array of valid [minute values](#attr-timeitemminutevalues) to use when [useTextField](#attr-timeitemusetextfield) is false.

Used for limiting available valid Minute values, or when using the TimeItem to record duration, rather than time per-se.

See [minuteMinValue](#attr-timeitemminuteminvalue), [minuteMaxValue](#attr-timeitemminutemaxvalue) and [minuteIncrement](#attr-timeitemminuteincrement) for another method of controlling the content in the minute picker.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Array of Number](#type-array-of-number) | false | — | array of available Minute values |

**Flags**: A

---
## Method: TimeItem.setHourValues

### Description
Sets the array of valid [hour values](#attr-timeitemhourvalues) to use when [useTextField](#attr-timeitemusetextfield) is false.

Used for limiting available valid Hour values, or when using the TimeItem to record duration, rather than time per-se.

See [hourMinValue](#attr-timeitemhourminvalue), [hourMaxValue](#attr-timeitemhourmaxvalue) and [hourIncrement](#attr-timeitemhourincrement) for another method of controlling the content in the hour picker.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Array of Number](#type-array-of-number) | false | — | array of available Hour values |

**Flags**: A

---
## Method: TimeItem.getHourValues

### Description
Returns an array of the current valid hour values, whether set directly as [TimeItem.hourValues](#attr-timeitemhourvalues) or generated according to [hourMinValue](#attr-timeitemhourminvalue), [hourMaxValue](#attr-timeitemhourmaxvalue) and [hourIncrement](#attr-timeitemhourincrement).

### Returns

`[Array of Number](#type-array-of-number)` — array of available Hour values

**Flags**: A

---
## Method: TimeItem.selectValue

### Description
If [TimeItem.useTextField](#attr-timeitemusetextfield) is true, falls through to standard [selectValue()](TextItem.md#method-textitemselectvalue) implementation on this items freeform text entry field. Otherwise has no effect.

---
## Method: TimeItem.getEnteredValue

### Description
Returns the raw text value typed into this items text field if [TimeItem.useTextField](#attr-timeitemusetextfield) is true (otherwise returns the result of this.getValue()).

### Returns

`[String](#type-string)` — value the user entered

---
## Method: TimeItem.setHours

### Description
Set the hour value of this TimeItem. If the item value has not been initialized with [setValue()](#method-timeitemsetvalue), the minute will be established to current minute.

You can use [setValue()](#method-timeitemsetvalue) to set both hours and minutes at the same time.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| hours | [Number](#type-number) | false | — | new hours value for this TimeItem. |

**Flags**: A

---
## Method: TimeItem.getSelectionRange

### Description
If [TimeItem.useTextField](#attr-timeitemusetextfield) is true, falls through to standard [getSelectionRange](TextItem.md#method-textitemgetselectionrange) implementation on this items freeform text entry field. Otherwise has no effect.

### Returns

`[Array](#type-array)` — 2 element array indicating start/end character index of current selection within our text entry field. Returns null if this item is undrawn or doesn't have focus.

---
## Method: TimeItem.getSecondValues

### Description
Returns an array of the current valid second values, whether set directly as [TimeItem.secondValues](#attr-timeitemsecondvalues) or generated according to [secondMinValue](#attr-timeitemsecondminvalue), [secondMaxValue](#attr-timeitemsecondmaxvalue) and [secondIncrement](#attr-timeitemsecondincrement).

### Returns

`[Array of Number](#type-array-of-number)` — array of available Second values

**Flags**: A

---
## Method: TimeItem.setSecondValues

### Description
Sets the array of valid [second values](#attr-timeitemsecondvalues) to use when [useTextField](#attr-timeitemusetextfield) is false.

Used for limiting available valid Second values, or when using the TimeItem to record duration, rather than time per-se.

See [secondMinValue](#attr-timeitemsecondminvalue), [secondMaxValue](#attr-timeitemsecondmaxvalue) and [secondIncrement](#attr-timeitemsecondincrement) for another method of controlling the content in the second picker.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Array of Number](#type-array-of-number) | false | — | array of available Second values |

**Flags**: A

---
## Method: TimeItem.getMinuteValues

### Description
Returns an array of the current valid minute values, whether set directly as [TimeItem.minuteValues](#attr-timeitemminutevalues) or generated according to [minuteMinValue](#attr-timeitemminuteminvalue), [minuteMaxValue](#attr-timeitemminutemaxvalue) and [minuteIncrement](#attr-timeitemminuteincrement).

### Returns

`[Array of Number](#type-array-of-number)` — array of available Minute values

**Flags**: A

---
## Method: TimeItem.setMilliseconds

### Description
Set the milliseconds value of this TimeItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| milliseconds | [Number](#type-number) | false | — | new milliseconds value for this TimeItem. |

**Flags**: A

---
## Method: TimeItem.deselectValue

### Description
If [TimeItem.useTextField](#attr-timeitemusetextfield) is true, falls through to standard [deselectValue()](TextItem.md#method-textitemdeselectvalue) implementation on this items freeform text entry field. Otherwise has no effect.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| start | [Boolean](#type-boolean) | true | — | If this parameter is passed, new cursor insertion position will be moved to the start, rather than the end of this item's value. |

---
## Method: TimeItem.setSeconds

### Description
Set the seconds value of this TimeItem.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| seconds | [Number](#type-number) | false | — | new seconds value for this TimeItem. |

**Flags**: A

---
## Method: TimeItem.setMillisecondValues

### Description
Sets the array of valid [millisecond values](#attr-timeitemmillisecondvalues) to use when [useTextField](#attr-timeitemusetextfield) is false.

Used for limiting available valid Millisecond values, or when using the TimeItem to record duration, rather than time per-se.

See [millisecondMinValue](#attr-timeitemmillisecondminvalue), [millisecondMaxValue](#attr-timeitemmillisecondmaxvalue) and [millisecondIncrement](#attr-timeitemmillisecondincrement) for another method of controlling the content in the millisecond picker.

### Parameters

| Name | Type | Optional | Default | Description |
|------|------|----------|---------|-------------|
| values | [Array of Number](#type-array-of-number) | false | — | array of available Millisecond values |

**Flags**: A

---
